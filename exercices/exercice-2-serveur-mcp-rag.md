# Exercice 2 : Serveur MCP + RAG pour base d'avis

**Durée** : 2 heures  
**Format** : Semi-ouvert avec checkpoints  
**Binômes** : Possibles mais non obligatoires

---

## 🎯 Objectifs pédagogiques

À la fin de cet exercice, vous saurez :

- ✅ Comprendre et utiliser le Model Context Protocol (MCP)
- ✅ Générer des embeddings avec l'API OpenAI
- ✅ Stocker et interroger une base vectorielle (ChromaDB)
- ✅ Créer un serveur MCP exposant des tools
- ✅ Connecter Claude Code à votre serveur MCP
- ✅ Implémenter un système RAG (Retrieval Augmented Generation)

---

## 📖 Contexte métier

Vous avez une base de données d'**avis clients** sur des agences immobilières Immodvisor.

**Problème** :

- Claude Code ne connaît pas ces avis (données privées)
- Vous voulez interroger sémantiquement : "Quels sont les avis positifs sur l'accueil ?" ou "Trouve les problèmes récurrents"

**Solution : RAG via MCP**

1. Indexer les avis dans une base vectorielle (embeddings OpenAI)
2. Créer un serveur MCP qui expose des tools de recherche
3. Connecter Claude Code au serveur MCP
4. Claude peut maintenant interroger vos avis !

---

## 🏗️ Architecture globale

```
┌─────────────────┐
│   Claude Code   │
│   (MCP Client)  │
└────────┬────────┘
         │ MCP Protocol (stdio/SSE)
         │
┌────────┴────────┐
│   MCP Server    │
│   (Node.js ou   │
│    Python)      │
└────────┬────────┘
         │
         ├── Tool: search_reviews(query, limit)
         ├── Tool: get_stats(agencyId?)
         └── Tool: analyze_sentiment(agencyId?)
         │
┌────────┴────────┐
│   ChromaDB      │
│   (Base         │
│    vectorielle) │
└────────┬────────┘
         │
         └── Embeddings (OpenAI Ada)
              └── Avis Immodvisor
```

---

## 🚀 Déroulé de l'exercice

### Checkpoint 1 : Génération du dataset (30 min)

#### 1.1 Créer un jeu de données réaliste (15 min)

**Tâche** : Générer 50-100 faux avis Immodvisor avec l'IA.

**Prompt suggéré pour Claude Code** :

```markdown
Génère 100 avis d'agences immobilières réalistes en français pour Immodvisor.

Critères :

- Variété de notes : 20% de 1-2 étoiles, 30% de 3 étoiles, 50% de 4-5 étoiles
- Longueur variable : 50 à 400 caractères
- Ton naturel et authentique (pas marketing)
- Mix de types : achat, vente, location
- Thèmes variés : accueil, professionnalisme, réactivité, prix, qualité du conseil, etc.
- Inclure quelques avis négatifs réalistes (lenteur, manque de suivi, frais cachés)

Format JSON :
{
"reviews": [
{
"id": "uuid v4",
"agencyId": "uuid v4",
"agencyName": "Nom de l'agence (var iée : Immo Paris 15, Century 21 Lyon, etc.)",
"rating": 1-5,
"comment": "Texte de l'avis",
"authorEmail": "email",
"authorName": "Prénom Nom",
"prestationType": "achat|vente|location",
"createdAt": "2024-01-01T10:00:00Z"
}
]
}

Sauvegarde dans `data/reviews-dataset.json`
```

**Livrable** : `data/reviews-dataset.json` (50-100 avis)

---

#### 1.2 Vérifier la qualité du dataset (5 min)

**Tâche** : S'assurer que les avis sont diversifiés.

**Commandes** :

```bash
# Compter les avis par note
cat data/reviews-dataset.json | jq '.reviews | group_by(.rating) | map({rating: .[0].rating, count: length})'

# Vérifier les thèmes (mots-clés)
cat data/reviews-dataset.json | jq -r '.reviews[].comment' | grep -i "professionnel\|accueil\|réactif\|lent\|cher"
```

---

#### 1.3 Installer les dépendances (10 min)

**Tâche** : Préparer l'environnement Python ou Node.js.

**Option A : Python** (recommandé si déjà installé)

```bash
# Créer un environnement virtuel
cd exercice-2-mcp-rag
python3 -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate

# Installer les dépendances
pip install chromadb openai python-dotenv mcp

# Créer .env
echo "OPENAI_API_KEY=sk-..." > .env
```

**Option B : Node.js** (si préférence TypeScript)

```bash
# Initialiser le projet
cd exercice-2-mcp-rag
npm init -y

# Installer les dépendances
npm install chromadb openai dotenv @modelcontextprotocol/sdk

# Créer .env
echo "OPENAI_API_KEY=sk-..." > .env
```

**Livrable** : Environnement prêt avec dépendances installées

---

### Checkpoint 2 : Indexation des avis (45 min)

#### 2.1 Générer les embeddings (20 min)

**Tâche** : Transformer chaque avis en vecteur (embedding) avec l'API OpenAI.

**Script Python suggéré** : `scripts/index_reviews.py`

```python
import json
import os
from openai import OpenAI
from chromadb import Client
from chromadb.config import Settings
from dotenv import load_dotenv

load_dotenv()

# Configuration
client_openai = OpenAI(api_key=os.getenv("OPENAI_API_KEY"))
client_chroma = Client(Settings(
    persist_directory="./chroma_db"
))

# Créer ou récupérer la collection
collection = client_chroma.get_or_create_collection(
    name="immodvisor_reviews",
    metadata={"description": "Avis clients Immodvisor"}
)

# Charger les avis
with open("../data/reviews-dataset.json") as f:
    data = json.load(f)
    reviews = data["reviews"]

print(f"📊 Indexation de {len(reviews)} avis...")

# Générer les embeddings et indexer
for i, review in enumerate(reviews):
    # Créer le texte à embedder (combinaison de champs pertinents)
    text_to_embed = f"""
    Agence: {review['agencyName']}
    Note: {review['rating']}/5
    Type: {review['prestationType']}
    Avis: {review['comment']}
    Auteur: {review['authorName']}
    """

    # Générer l'embedding avec OpenAI
    response = client_openai.embeddings.create(
        model="text-embedding-3-small",  # Modèle économique
        input=text_to_embed
    )
    embedding = response.data[0].embedding

    # Ajouter à ChromaDB
    collection.add(
        ids=[review["id"]],
        embeddings=[embedding],
        metadatas=[{
            "agencyId": review["agencyId"],
            "agencyName": review["agencyName"],
            "rating": review["rating"],
            "prestationType": review["prestationType"],
            "authorName": review["authorName"],
            "createdAt": review["createdAt"]
        }],
        documents=[review["comment"]]  # Texte de l'avis
    )

    if (i + 1) % 10 == 0:
        print(f"✅ {i + 1}/{len(reviews)} avis indexés")

print("🎉 Indexation terminée !")
print(f"📁 Base vectorielle sauvegardée dans ./chroma_db")
```

**Prompt pour Claude Code** (si génération assistée) :

```markdown
Crée un script Python qui :

1. Charge les avis depuis `data/reviews-dataset.json`
2. Pour chaque avis, génère un embedding avec OpenAI API (model: text-embedding-3-small)
3. Stocke dans ChromaDB avec métadonnées (agencyId, rating, etc.)
4. Affiche la progression

Dépendances : openai, chromadb, python-dotenv
Fichier : scripts/index_reviews.py
```

**Lancer le script** :

```bash
python scripts/index_reviews.py
```

**Livrable** : Base ChromaDB peuplée dans `./chroma_db/`

---

#### 2.2 Tester la recherche vectorielle (10 min)

**Tâche** : Vérifier que la recherche sémantique fonctionne.

**Script de test** : `scripts/test_search.py`

```python
from chromadb import Client
from chromadb.config import Settings
from openai import OpenAI
import os
from dotenv import load_dotenv

load_dotenv()

client_openai = OpenAI(api_key=os.getenv("OPENAI_API_KEY"))
client_chroma = Client(Settings(persist_directory="./chroma_db"))

collection = client_chroma.get_collection("immodvisor_reviews")

# Test de recherche sémantique
query = "avis positifs sur l'accueil et le professionnalisme"

print(f"🔍 Recherche : {query}\n")

# Générer l'embedding de la requête
response = client_openai.embeddings.create(
    model="text-embedding-3-small",
    input=query
)
query_embedding = response.data[0].embedding

# Rechercher les avis similaires
results = collection.query(
    query_embeddings=[query_embedding],
    n_results=5
)

# Afficher les résultats
for i, (doc, metadata, distance) in enumerate(zip(
    results["documents"][0],
    results["metadatas"][0],
    results["distances"][0]
)):
    print(f"--- Résultat {i+1} (similarité: {1 - distance:.2f}) ---")
    print(f"Agence: {metadata['agencyName']}")
    print(f"Note: {metadata['rating']}/5")
    print(f"Avis: {doc}")
    print()
```

**Lancer le test** :

```bash
python scripts/test_search.py
```

**Résultat attendu** : 5 avis pertinents sur l'accueil et le professionnalisme

---

#### 2.3 Optimiser le chunking (15 min - optionnel)

**Si les avis sont très longs**, découper en chunks pour améliorer la précision.

**Stratégie** : Comme les avis sont courts (< 400 caractères), **pas de chunking nécessaire**.

**Si vous voulez expérimenter** :

```python
# Pour des avis plus longs, découper par phrases
def chunk_text(text, max_length=200):
    sentences = text.split('. ')
    chunks = []
    current_chunk = ""

    for sentence in sentences:
        if len(current_chunk) + len(sentence) < max_length:
            current_chunk += sentence + ". "
        else:
            chunks.append(current_chunk.strip())
            current_chunk = sentence + ". "

    if current_chunk:
        chunks.append(current_chunk.strip())

    return chunks
```

---

### Checkpoint 3 : Création du serveur MCP (45 min)

#### 3.1 Structure du serveur MCP (10 min)

**Tâche** : Créer la structure du serveur MCP.

**Architecture** :

```
mcp-server/
├── server.py (ou index.js)
├── tools/
│   ├── search_reviews.py
│   ├── get_stats.py
│   └── analyze_sentiment.py
├── chroma_db/ (lien symbolique ou copie)
└── .env
```

---

#### 3.2 Implémenter le serveur MCP Python (25 min)

**Fichier** : `mcp-server/server.py`

```python
import json
import os
from mcp.server import Server
from mcp.server.stdio import stdio_server
from chromadb import Client
from chromadb.config import Settings
from openai import OpenAI
from dotenv import load_dotenv

load_dotenv()

# Configuration
client_openai = OpenAI(api_key=os.getenv("OPENAI_API_KEY"))
client_chroma = Client(Settings(persist_directory="../chroma_db"))
collection = client_chroma.get_collection("immodvisor_reviews")

# Créer le serveur MCP
server = Server("immodvisor-reviews")

# Tool 1: Recherche sémantique
@server.tool()
async def search_reviews(query: str, limit: int = 5) -> str:
    """
    Recherche sémantique dans les avis d'agences immobilières.

    Args:
        query: Requête en langage naturel (ex: "avis positifs sur l'accueil")
        limit: Nombre de résultats à retourner (défaut: 5)

    Returns:
        JSON avec les avis pertinents
    """
    # Générer l'embedding de la requête
    response = client_openai.embeddings.create(
        model="text-embedding-3-small",
        input=query
    )
    query_embedding = response.data[0].embedding

    # Rechercher les avis similaires
    results = collection.query(
        query_embeddings=[query_embedding],
        n_results=limit
    )

    # Formater les résultats
    reviews = []
    for doc, metadata, distance in zip(
        results["documents"][0],
        results["metadatas"][0],
        results["distances"][0]
    ):
        reviews.append({
            "agencyName": metadata["agencyName"],
            "rating": metadata["rating"],
            "comment": doc,
            "similarity": round(1 - distance, 3)
        })

    return json.dumps({"query": query, "results": reviews}, ensure_ascii=False, indent=2)


# Tool 2: Statistiques
@server.tool()
async def get_stats(agencyId: str = None) -> str:
    """
    Retourne des statistiques sur les avis.

    Args:
        agencyId: (Optionnel) ID de l'agence pour filtrer

    Returns:
        JSON avec les statistiques
    """
    # Récupérer tous les avis (ou filtrés par agence)
    if agencyId:
        results = collection.get(where={"agencyId": agencyId})
    else:
        results = collection.get()

    # Calculer les statistiques
    ratings = [meta["rating"] for meta in results["metadatas"]]

    stats = {
        "total": len(ratings),
        "averageRating": round(sum(ratings) / len(ratings), 2) if ratings else 0,
        "distribution": {
            "1star": ratings.count(1),
            "2stars": ratings.count(2),
            "3stars": ratings.count(3),
            "4stars": ratings.count(4),
            "5stars": ratings.count(5),
        }
    }

    return json.dumps(stats, ensure_ascii=False, indent=2)


# Tool 3: Analyse de sentiment
@server.tool()
async def analyze_sentiment(agencyId: str = None) -> str:
    """
    Analyse le sentiment global des avis (positif/négatif/neutre).

    Args:
        agencyId: (Optionnel) ID de l'agence pour filtrer

    Returns:
        JSON avec l'analyse de sentiment
    """
    # Récupérer les avis
    if agencyId:
        results = collection.get(where={"agencyId": agencyId})
    else:
        results = collection.get()

    # Analyser les sentiments basés sur les notes
    ratings = [meta["rating"] for meta in results["metadatas"]]

    positive = sum(1 for r in ratings if r >= 4)
    neutral = sum(1 for r in ratings if r == 3)
    negative = sum(1 for r in ratings if r <= 2)

    total = len(ratings)

    sentiment = {
        "totalReviews": total,
        "sentiment": {
            "positive": {"count": positive, "percentage": round(positive / total * 100, 1)},
            "neutral": {"count": neutral, "percentage": round(neutral / total * 100, 1)},
            "negative": {"count": negative, "percentage": round(negative / total * 100, 1)},
        }
    }

    return json.dumps(sentiment, ensure_ascii=False, indent=2)


# Lancer le serveur
if __name__ == "__main__":
    import asyncio
    asyncio.run(stdio_server(server))
```

**Prompt pour Claude Code** (si génération assistée) :

```markdown
Crée un serveur MCP Python qui expose 3 tools :

1. search_reviews(query: str, limit: int = 5)

   - Recherche sémantique dans ChromaDB
   - Génère embedding de la query avec OpenAI
   - Retourne les top-k avis similaires

2. get_stats(agencyId: str = None)

   - Statistiques : total, moyenne, distribution des notes
   - Filtrage optionnel par agence

3. analyze_sentiment(agencyId: str = None)
   - Analyse positive/neutre/négatif basé sur les notes
   - Retourne count et pourcentages

Utilise : mcp.server, chromadb, openai
Fichier : mcp-server/server.py
```

---

#### 3.3 Configurer Claude Code pour utiliser le serveur MCP (10 min)

**Tâche** : Connecter Claude Code à votre serveur MCP.

**Fichier de config** : `.cursor/mcp.json` ou `~/.config/claude/mcp.json` (selon votre installation)

```json
{
  "mcpServers": {
    "immodvisor-reviews": {
      "command": "python",
      "args": ["/chemin/absolu/vers/mcp-server/server.py"],
      "env": {
        "OPENAI_API_KEY": "sk-..."
      }
    }
  }
}
```

**Redémarrer Claude Code** pour charger la config.

**Vérifier** :

- Ouvrir Claude Code
- Taper : "Liste les tools MCP disponibles"
- Vous devriez voir : `search_reviews`, `get_stats`, `analyze_sentiment`

---

### Checkpoint 4 : Tests et démo (30 min)

#### 4.1 Tester le serveur MCP depuis Claude Code (15 min)

**Tâche** : Interroger vos avis via Claude Code.

**Exemples de requêtes** :

1. **Recherche sémantique** :

   ```
   Utilise le tool search_reviews pour trouver les avis positifs sur l'accueil.
   ```

2. **Statistiques globales** :

   ```
   Donne-moi les statistiques de tous les avis avec get_stats.
   ```

3. **Analyse de sentiment** :

   ```
   Analyse le sentiment global des avis avec analyze_sentiment.
   ```

4. **Question complexe** (RAG en action) :

   ```
   Quels sont les problèmes récurrents mentionnés dans les avis négatifs (note ≤ 2) ?

   (Claude va appeler search_reviews avec query="problèmes récurrents avis négatifs")
   ```

**Résultat attendu** : Claude répond en langage naturel en utilisant les données de votre MCP.

---

#### 4.2 Cas d'usage avancés (10 min)

**Tester des scénarios réalistes** :

**Scénario 1 : Analyse comparative**

```
Compare les avis sur les agences de Paris vs Lyon. Quelle ville a les meilleures notes en moyenne ?
```

**Scénario 2 : Insights métier**

```
Quels sont les 3 thèmes les plus mentionnés dans les avis 5 étoiles ?
Et dans les avis 1-2 étoiles ?
```

**Scénario 3 : Recommandation**

```
Un client cherche une agence professionnelle et réactive à Paris.
Recommande-lui les 3 meilleures agences basées sur les avis.
```

---

#### 4.3 Démo collective (5 min)

**Format** : Montrer votre serveur MCP en action.

**Présenter** :

1. Votre dataset d'avis
2. La base vectorielle ChromaDB
3. Une requête complexe à Claude Code
4. La réponse générée avec données réelles

---

## 📊 Grille d'évaluation (auto-évaluation)

| Critère                                       | Oui ✅ | Non ❌ | Remarque |
| --------------------------------------------- | ------ | ------ | -------- |
| **Dataset** : 50-100 avis générés             |        |        |          |
| **Indexation** : Embeddings créés avec OpenAI |        |        |          |
| **ChromaDB** : Base vectorielle fonctionnelle |        |        |          |
| **MCP Server** : 3 tools implémentés          |        |        |          |
| **Config** : Claude Code connecté au serveur  |        |        |          |
| **Test** : Recherche sémantique fonctionne    |        |        |          |
| **RAG** : Questions complexes répondues       |        |        |          |

---

## 🎁 Bonus (si temps disponible)

### Bonus 1 : Filtres avancés

Ajouter des paramètres de filtrage :

```python
@server.tool()
async def search_reviews(
    query: str,
    limit: int = 5,
    min_rating: int = None,
    max_rating: int = None,
    prestation_type: str = None
) -> str:
    # Implémenter les filtres avec ChromaDB where clause
    ...
```

---

### Bonus 2 : Cache des embeddings

Éviter de régénérer l'embedding de la même query :

```python
import hashlib
import pickle

embedding_cache = {}

def get_cached_embedding(text: str):
    cache_key = hashlib.md5(text.encode()).hexdigest()

    if cache_key in embedding_cache:
        return embedding_cache[cache_key]

    response = client_openai.embeddings.create(
        model="text-embedding-3-small",
        input=text
    )
    embedding = response.data[0].embedding
    embedding_cache[cache_key] = embedding

    return embedding
```

---

### Bonus 3 : Métriques de coût

Tracker les appels API OpenAI :

```python
import time

metrics = {
    "total_queries": 0,
    "total_tokens": 0,
    "total_cost_usd": 0
}

@server.tool()
async def get_metrics() -> str:
    """Retourne les métriques d'utilisation du serveur MCP"""
    return json.dumps(metrics, indent=2)
```

---

### Bonus 4 : Multi-collection

Créer plusieurs collections (avis, documentation interne, tickets JIRA) :

```python
collections = {
    "reviews": client_chroma.get_collection("immodvisor_reviews"),
    "docs": client_chroma.get_collection("internal_docs"),
}

@server.tool()
async def search_all(query: str) -> str:
    """Recherche dans toutes les collections"""
    results = {}
    for name, collection in collections.items():
        results[name] = collection.query(...)
    return json.dumps(results)
```

---

## 💡 Points clés à retenir

### MCP (Model Context Protocol)

- Protocole standardisé pour connecter outils externes aux LLMs
- Architecture : Client (Claude) ↔ Server (Python/Node) ↔ Data
- Tools = fonctions exposées au LLM (comme des APIs)

### RAG (Retrieval Augmented Generation)

- Permet d'accéder à des données privées/récentes
- Pipeline : Query → Embedding → Recherche vectorielle → Génération
- Économise des tokens (seulement top-k résultats dans le contexte)

### Embeddings

- Représentation vectorielle du texte
- Textes similaires = vecteurs proches (similarité cosinus)
- OpenAI text-embedding-3-small : $0.02 par 1M tokens

### ChromaDB

- Base de données vectorielle simple et efficace
- Stockage local (pas besoin de serveur)
- Recherche par similarité cosinus

---

## 🎓 Cas d'usage réels chez Immodvisor

### Court terme

- ✅ **RAG sur docs internes** : Indexer la documentation Symfony, API Platform, guidelines
- ✅ **Recherche dans les tickets JIRA** : "Trouve les bugs récurrents sur le module de paiement"
- ✅ **Analyse d'avis** : Détecter les tendances, problèmes récurrents

### Moyen terme

- ✅ **Agent de support client** : Répondre aux questions basées sur FAQ + historique
- ✅ **Code review assistant** : Indexer les bonnes pratiques de la codebase
- ✅ **Onboarding automatisé** : Nouveau dev → Questions sur le projet → Réponses depuis docs indexées

---

## 📚 Ressources

### Documentation

- [Model Context Protocol](https://modelcontextprotocol.io/)
- [ChromaDB Documentation](https://docs.trychroma.com/)
- [OpenAI Embeddings API](https://platform.openai.com/docs/guides/embeddings)

### Tutoriels

- [Building a RAG System with ChromaDB](https://docs.trychroma.com/guides)
- [OpenAI Cookbook: Question Answering](https://cookbook.openai.com/)

### Alternatives à ChromaDB

- **Pinecone** : Vector database cloud (payant)
- **Weaviate** : Open-source, self-hosted
- **Qdrant** : Rust-based, performant
- **PostgreSQL + pgvector** : Extension SQL pour vecteurs

---

**Session suivante** : [Finalisation de la charte d'utilisation](../charte/guidelines-vibe-coding.md)
