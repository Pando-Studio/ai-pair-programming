# Concepts fondamentaux : LLM, MCP, RAG

**Format** : Présentation rapide, approfondissement durant les exercices

---

## 🎯 Objectif

Comprendre les concepts essentiels pour travailler efficacement avec l'IA générative :

- LLM, tokens, température, contexte
- Prompting efficace
- Model Context Protocol (MCP)
- RAG (Retrieval Augmented Generation)
- Embeddings et recherche sémantique

---

## 🧠 LLM : Large Language Models

### Qu'est-ce qu'un LLM ?

**Définition** : Modèle de machine learning entraîné sur d'immenses quantités de texte pour prédire la suite la plus probable.

**Modèles populaires (2025)** :

| Modèle                            | Taille contexte | Forces                                   | Cas d'usage dev             |
| --------------------------------- | --------------- | ---------------------------------------- | --------------------------- |
| **GPT-4o** (OpenAI)               | 128k tokens     | Polyvalent, rapide                       | Code général, debugging     |
| **Claude 3.5 Sonnet** (Anthropic) | 200k tokens     | Excellent en code, suit les instructions | Refactoring, architecture   |
| **Gemini 1.5 Pro** (Google)       | 2M tokens       | Contexte énorme                          | Analyse de codebase entière |
| **o1** (OpenAI)                   | 128k tokens     | Raisonnement profond                     | Problèmes complexes         |

---

### Tokens : L'unité de mesure

**Qu'est-ce qu'un token ?**

- Morceau de texte (mot, partie de mot, caractère)
- **~4 caractères = 1 token** (en moyenne, pour l'anglais)
- **~3 caractères = 1 token** (pour le code)

**Exemples** :

```
"Hello world" = 2 tokens
"function calculateTotal()" = 5 tokens
"$this->reviewRepository->findByAgencyId($agencyId)" = ~12 tokens
```

**Pourquoi c'est important ?**

- 💰 **Coût** : Facturation par token (input + output)
- ⏱️ **Latence** : Plus de tokens = réponse plus lente
- 🧠 **Limite de contexte** : Max 128k-2M tokens selon modèle

**Tarifs indicatifs (2025)** :

| Modèle            | Input (par 1M tokens) | Output (par 1M tokens) |
| ----------------- | --------------------- | ---------------------- |
| GPT-4o            | $2.50                 | $10.00                 |
| Claude 3.5 Sonnet | $3.00                 | $15.00                 |
| Gemini 1.5 Pro    | $1.25                 | $5.00                  |

---

### Température : Contrôler la créativité

**Définition** : Paramètre qui contrôle l'aléatoire des réponses (0 à 2)

| Température   | Comportement             | Quand l'utiliser                                      |
| ------------- | ------------------------ | ----------------------------------------------------- |
| **0 - 0.2**   | Déterministe, prévisible | **Code production**, génération de tests, refactoring |
| **0.5 - 0.7** | Équilibré                | Brainstorming, suggestions d'architecture             |
| **0.8 - 1.5** | Créatif, varié           | Noms de variables, documentation, idées               |

**💡 Recommandation pour le code** : **Température 0** → Reproductibilité maximale

---

### Contexte : La fenêtre de mémoire

**Contexte** = Tout ce que l'IA "voit" :

- Votre prompt
- L'historique de conversation
- Les fichiers ouverts (dans IDE IA)
- Les résultats de tool calls (MCP)

**Limite de contexte** :

- GPT-4o : 128k tokens ≈ 300 pages
- Claude 3.5 Sonnet : 200k tokens ≈ 500 pages
- Gemini 1.5 Pro : 2M tokens ≈ 5000 pages

**Problème** : Une fois le contexte dépassé, l'IA "oublie" le début

**Solutions** :

- Résumer les parties anciennes
- Utiliser RAG pour récupérer seulement l'info pertinente
- Découper en conversations plus courtes

---

## 💬 Prompting efficace

### Anatomie d'un bon prompt

**Structure recommandée** :

```markdown
## Contexte

[Décrire le contexte du projet, la stack technique, les contraintes]

## Tâche

[Décrire clairement ce que l'IA doit faire]

## Contraintes

[Lister les règles à respecter : standards de code, architecture, librairies]

## Exemples (optionnel)

[Montrer des exemples de code existant pour guider le style]

## Questions

[Inviter l'IA à poser des questions si besoin de clarifications]
```

**Exemple concret** :

```markdown
## Contexte

Je développe une API de gestion d'avis avec Symfony 6.4 + API Platform 3.2.
Architecture : Controller → Service → Repository.

## Tâche

Crée un service ReviewService avec une méthode createReview() qui :

- Valide les données (rating 1-5, comment min 10 caractères)
- Vérifie qu'un avis n'existe pas déjà pour cet utilisateur et cette agence
- Persiste l'avis en base de données
- Retourne le DTO ReviewDto

## Contraintes

- PHP 8.2 strict typing
- Utilise Symfony Validator
- Lance ReviewAlreadyExistsException si duplicata
- Lance ValidationException si validation échoue
- Pas de logique dans le Controller

## Questions

As-tu besoin de voir le schéma de base de données ou les DTOs existants ?
```

---

### Techniques de prompting avancées

**1. Role prompting** (définir un rôle)

```markdown
Tu es un développeur senior PHP/Symfony avec 10 ans d'expérience.
Tu suis strictement les principes SOLID et les PSR-12.
```

**2. Chain-of-thought** (demander le raisonnement)

```markdown
Avant de générer le code, explique ton approche :

1. Quelle architecture vas-tu utiliser ?
2. Quels patterns vas-tu appliquer ?
3. Quels cas d'erreur dois-tu gérer ?

Ensuite, génère le code.
```

**3. Few-shot examples** (donner des exemples)

```markdown
Voici un exemple de service existant dans notre codebase :

[coller un exemple de bon code]

Génère un service similaire pour les avis, en suivant le même style.
```

**4. Contraintes négatives** (dire ce qu'on NE veut PAS)

```markdown
## Ce que tu NE dois PAS faire :

- ❌ Pas de code dans le Controller
- ❌ Pas de requêtes SQL brutes
- ❌ Pas de foreach si on peut utiliser une méthode de Collection
- ❌ Pas de commentaires évidents
```

**5. Itérations guidées**

```markdown
Étape 1 : Propose la signature de la méthode avec type hints
→ [validation par le dev]

Étape 2 : Génère l'implémentation
→ [validation par le dev]

Étape 3 : Ajoute la gestion d'erreurs
```

---

## 🔌 MCP : Model Context Protocol

### Qu'est-ce que MCP ?

**MCP** = Protocole standardisé pour connecter des **outils externes** aux LLMs.

**Analogie** : MCP est aux LLMs ce que les APIs REST sont aux applications web.

**Cas d'usage** :

- Accéder à des bases de données
- Lire/écrire des fichiers
- Appeler des APIs externes
- Récupérer des données depuis JIRA, Figma, Slack, etc.
- Exécuter des commandes système

---

### Architecture MCP

```
┌─────────────┐
│   Claude    │
│   (LLM)     │
└──────┬──────┘
       │
       │ MCP Protocol
       │
┌──────┴──────┐
│ MCP Server  │
│  (Node.js   │
│   ou Python)│
└──────┬──────┘
       │
       ├─── Database (SQLite, PostgreSQL, etc.)
       ├─── APIs (JIRA, Figma, GitHub, etc.)
       ├─── Filesystem
       └─── Other tools
```

**Composants** :

- **MCP Server** : Expose des "resources" et des "tools"
- **LLM Client** : Appelle les tools du serveur
- **Protocol** : JSON-RPC standardisé

---

### Exemple : Serveur MCP pour avis

**Ce que vous allez construire dans l'exercice 2** :

```json
{
  "mcpServers": {
    "reviews-db": {
      "command": "node",
      "args": ["./mcp-server/index.js"],
      "tools": [
        {
          "name": "search_reviews",
          "description": "Recherche sémantique dans les avis",
          "parameters": {
            "query": "string",
            "limit": "number"
          }
        },
        {
          "name": "get_stats",
          "description": "Statistiques sur les avis",
          "parameters": {
            "agencyId": "string (optional)"
          }
        }
      ]
    }
  }
}
```

**Workflow** :

1. Vous demandez à Claude : "Quels sont les avis positifs sur l'agence X ?"
2. Claude appelle le tool `search_reviews` via MCP
3. Le serveur MCP interroge la base vectorielle
4. Les résultats remontent à Claude
5. Claude vous répond en langage naturel

---

## 🔍 RAG : Retrieval Augmented Generation

### Problème à résoudre

**Sans RAG** :

- ❌ L'IA ne connaît que ce qu'elle a vu pendant son entraînement
- ❌ Pas d'accès aux données privées (votre codebase, vos docs internes)
- ❌ Limite de contexte (128k-2M tokens max)

**Avec RAG** :

- ✅ L'IA peut accéder à des données externes
- ✅ Seulement les infos pertinentes sont récupérées (économie de tokens)
- ✅ Données à jour (pas besoin de réentraîner le modèle)

---

### Architecture RAG

```
┌──────────────┐
│   Question   │
│  utilisateur │
└──────┬───────┘
       │
       │ 1. Embedding de la question
       ▼
┌──────────────┐
│ Embedding    │
│   Model      │
│ (OpenAI Ada) │
└──────┬───────┘
       │
       │ 2. Recherche sémantique
       ▼
┌──────────────┐
│   Vector     │
│   Database   │
│ (ChromaDB,   │
│  Pinecone)   │
└──────┬───────┘
       │
       │ 3. Documents pertinents
       ▼
┌──────────────┐
│     LLM      │
│  (GPT-4o,    │
│   Claude)    │
└──────┬───────┘
       │
       │ 4. Réponse générée
       ▼
┌──────────────┐
│   Réponse    │
│ à l'user     │
└──────────────┘
```

**Étapes RAG** :

1. **Indexation** (fait une fois) :

   - Découper les documents en chunks (morceaux)
   - Générer des embeddings pour chaque chunk
   - Stocker dans une base vectorielle

2. **Récupération** (à chaque question) :

   - Transformer la question en embedding
   - Rechercher les chunks les plus similaires (similarité cosinus)
   - Récupérer les top-k chunks (ex: top 5)

3. **Génération** :
   - Injecter les chunks pertinents dans le prompt
   - Le LLM génère la réponse en se basant sur ces chunks

---

### Embeddings : Représentation vectorielle

**Qu'est-ce qu'un embedding ?**

- Représentation numérique d'un texte
- Vecteur de dimensions (ex: 1536 dimensions pour OpenAI Ada)
- Textes similaires → vecteurs proches

**Exemple** :

```python
# Texte
text1 = "L'agence était très professionnelle"
text2 = "Service de qualité, très pro"
text3 = "Le café était bon"

# Embeddings (vecteurs simplifiés à 3 dimensions pour l'exemple)
embedding1 = [0.8, 0.9, 0.1]  # Pro, qualité, non-café
embedding2 = [0.85, 0.88, 0.05]  # Très proche de text1
embedding3 = [0.1, 0.2, 0.95]  # Très différent (parle de café)

# Similarité cosinus
sim(text1, text2) = 0.98  # Très similaire !
sim(text1, text3) = 0.23  # Peu similaire
```

**Modèles d'embeddings populaires** :

| Modèle                            | Dimensions | Coût (par 1M tokens) | Cas d'usage         |
| --------------------------------- | ---------- | -------------------- | ------------------- |
| **OpenAI text-embedding-3-small** | 1536       | $0.02                | Général, économique |
| **OpenAI text-embedding-3-large** | 3072       | $0.13                | Haute précision     |
| **Cohere embed-multilingual**     | 1024       | $0.10                | Multilingue         |

---

### Chunking : Découper intelligemment

**Pourquoi chunker ?**

- Embeddings limités à ~8000 tokens par chunk
- Chunks trop longs = perte de précision sémantique
- Chunks trop courts = perte de contexte

**Stratégies de chunking** :

| Stratégie          | Taille           | Quand l'utiliser                           |
| ------------------ | ---------------- | ------------------------------------------ |
| **Fixed-size**     | 500 tokens       | Documents homogènes (docs techniques)      |
| **Sentence-based** | Phrases entières | Texte naturel (articles, avis)             |
| **Semantic**       | Variable         | Découpage par section/paragraphe logique   |
| **Code-aware**     | Variable         | Code source (découper par fonction/classe) |

**Exemple chunking d'avis** :

```python
# Avis original (trop long pour un seul embedding)
review = """
L'agence Immodvisor Paris 15 m'a accompagné pour l'achat de mon appartement.
Le conseiller était très professionnel et à l'écoute.
Le processus a été rapide, seulement 2 mois entre la première visite et la signature.
Cependant, quelques documents manquaient au dossier initial, ce qui a causé un léger retard.
Dans l'ensemble, je recommande vivement cette agence.
Note: 4/5
"""

# Chunking par phrase logique
chunks = [
    "L'agence Immodvisor Paris 15 m'a accompagné pour l'achat de mon appartement. Le conseiller était très professionnel et à l'écoute.",
    "Le processus a été rapide, seulement 2 mois entre la première visite et la signature.",
    "Cependant, quelques documents manquaient au dossier initial, ce qui a causé un léger retard.",
    "Dans l'ensemble, je recommande vivement cette agence. Note: 4/5"
]
```

---

## 🛠️ Mise en pratique dans les exercices

### Exercice 1 : API Avis avec PACT-R

**Concepts appliqués** :

- ✅ **LLM** : Utiliser Claude Code pour générer code et tests
- ✅ **Tokens** : Optimiser les prompts pour économiser des tokens
- ✅ **Température** : 0 pour génération de code déterministe
- ✅ **Prompting** : Structurer les demandes pour obtenir du bon code

---

### Exercice 2 : Serveur MCP + RAG

**Concepts appliqués** :

- ✅ **MCP** : Créer un serveur MCP exposant des tools
- ✅ **RAG** : Indexer des avis, récupérer les plus pertinents
- ✅ **Embeddings** : Générer avec OpenAI API
- ✅ **Chunking** : Découper les avis pour indexation

**Architecture complète** :

```
Claude Code (client MCP)
    ↓
MCP Server (Node.js/Python)
    ↓
ChromaDB (base vectorielle)
    ↓
Embeddings OpenAI
    ↓
Avis Immodvisor (données)
```

---

## 💡 Points clés à retenir

### LLM & Tokens

- Les LLMs prédisent la suite la plus probable
- Tokens = unité de mesure (4 car ≈ 1 token)
- Température 0 pour code déterministe
- Contexte limité (128k-2M tokens selon modèle)

### Prompting efficace

- Structurer : Contexte → Tâche → Contraintes → Questions
- Role prompting : Définir le rôle de l'IA
- Few-shot : Donner des exemples de bon code
- Itérations guidées : Valider étape par étape

### MCP

- Protocole pour connecter outils externes aux LLMs
- Architecture : LLM Client ↔ MCP Server ↔ Data/APIs
- Permet d'accéder à des données privées
- Exercice 2 = construire un serveur MCP

### RAG

- Retrieval Augmented Generation
- Permet d'accéder à des données non connues du LLM
- Architecture : Question → Embedding → Recherche vectorielle → Génération
- Chunks + Embeddings + Similarité = Récupération pertinente

---

## 📚 Ressources pour approfondir

### Documentation officielle

- [OpenAI API Reference](https://platform.openai.com/docs/api-reference)
- [Anthropic Claude Docs](https://docs.anthropic.com/)
- [Model Context Protocol](https://modelcontextprotocol.io/)

### Outils et frameworks

- [LangChain](https://www.langchain.com/) - Framework pour applications LLM
- [Langfuse](https://langfuse.com/) - Observabilité LLM (traces, métriques)
- [ChromaDB](https://www.trychroma.com/) - Base de données vectorielle
- [Pinecone](https://www.pinecone.io/) - Vector database as a service

### Tutoriels

- [OpenAI Cookbook](https://cookbook.openai.com/) - Recettes pratiques
- [Anthropic Prompt Engineering Guide](https://docs.anthropic.com/en/docs/prompt-engineering)

---

**Prochaine session** : [Atelier : Construction de la charte d'utilisation](../charte/guidelines-vibe-coding.md)
