# Exercices pratiques - Formation AI Pair Programming

Ce dossier contient les 2 exercices pratiques de la formation (2h chacun).

---

## 🏋️ Exercices

### Exercice 1 : API de gestion d'avis avec PACT-R (2h)

**Fichier** : [exercice-1-api-avis-pact-r.md](exercice-1-api-avis-pact-r.md)

**Objectifs** :

- Appliquer la méthodologie PACT-R complète
- Créer des spécifications techniques (ERD, OpenAPI)
- Écrire des tests avant le code (TDD strict)
- Utiliser Claude Code pour générer du code conforme
- Mesurer les métriques (tokens, temps, qualité)

**Stack** : PHP 8.2 + Symfony 6.4 + API Platform 3.2 + PHPUnit

**Checkpoints** :

1. PLAN (30min) : Specs + découpage
2. ASSERT + CODE (1h) : Tests RED → Code GREEN
3. TEST (30min) : Refactoring + PHPStan
4. REVIEW (10min) : Démo + retours

---

### Exercice 2 : Serveur MCP + RAG pour base d'avis (2h)

**Fichier** : [exercice-2-serveur-mcp-rag.md](exercice-2-serveur-mcp-rag.md)

**Objectifs** :

- Comprendre et utiliser le Model Context Protocol (MCP)
- Générer des embeddings avec l'API OpenAI
- Stocker et interroger une base vectorielle (ChromaDB)
- Créer un serveur MCP exposant des tools
- Connecter Claude Code au serveur MCP

**Stack** : Python ou Node.js + ChromaDB + OpenAI API

**Checkpoints** :

1. Dataset (30min) : Génération + indexation
2. Indexation (45min) : Embeddings + ChromaDB
3. MCP Server (45min) : 3 tools + config Claude Code
4. Tests (30min) : Requêtes sémantiques + démo

---

## 📋 Format des exercices

- **Semi-ouverts** : Instructions claires mais liberté d'implémentation
- **Checkpoints** : Points de validation réguliers
- **Prompts suggérés** : Templates pour guider l'utilisation de l'IA
- **Bonus** : Extensions pour les plus rapides
- **Auto-évaluation** : Grilles de critères

---

## 🎯 Prérequis techniques

### Pour l'exercice 1

```bash
# Vérifier les versions
php --version  # >= 8.2
composer --version
symfony version  # >= 5.x

# Créer le projet Symfony
symfony new exercice-1-api-avis --version=6.4
cd exercice-1-api-avis

# Installer les dépendances
composer require api-platform orm
composer require --dev phpunit phpstan
```

### Pour l'exercice 2

**Option Python** :

```bash
python3 --version  # >= 3.9
pip install chromadb openai python-dotenv mcp
```

**Option Node.js** :

```bash
node --version  # >= 18.x
npm install chromadb openai dotenv @modelcontextprotocol/sdk
```

---

## 💡 Conseils pour réussir

### Exercice 1

- ✅ Commencer simple (juste POST pour le MVP)
- ✅ Copier-coller les specs complètes dans les prompts
- ✅ Ne pas sauter la phase PLAN
- ✅ Écrire les tests AVANT le code

### Exercice 2

- ✅ Générer un dataset diversifié (notes variées)
- ✅ Tester la recherche vectorielle avant de créer le serveur MCP
- ✅ Utiliser des chemins absolus dans la config MCP
- ✅ Redémarrer Claude Code après modif de config

---

## 📊 Livrables attendus

### Exercice 1

- [ ] `docs/openapi.yaml` - Spécifications API
- [ ] `docs/erd.md` - Modèle de données
- [ ] `tests/Functional/Api/ReviewApiTest.php` - Tests fonctionnels
- [ ] `src/Entity/Review.php` - Entité Review
- [ ] `metrics.md` - Métriques collectées

### Exercice 2

- [ ] `data/reviews-dataset.json` - Dataset de 50-100 avis
- [ ] `scripts/index_reviews.py` - Script d'indexation
- [ ] `mcp-server/server.py` - Serveur MCP avec 3 tools
- [ ] `.cursor/mcp.json` - Configuration MCP
- [ ] Démo : Requête sémantique fonctionnelle

---

## 🎁 Bonus (si temps disponible)

### Exercice 1

- Implémenter GET /api/reviews/{id}
- Mutation testing avec Infection
- Générer la documentation Swagger

### Exercice 2

- Filtres avancés (min_rating, max_rating)
- Cache des embeddings
- Multi-collection (avis + docs internes)

---

## 📚 Ressources

### Exercice 1

- [API Platform Documentation](https://api-platform.com/docs/)
- [Symfony Validation](https://symfony.com/doc/current/reference/constraints.html)
- [PHPStan](https://phpstan.org/)

### Exercice 2

- [Model Context Protocol](https://modelcontextprotocol.io/)
- [ChromaDB Documentation](https://docs.trychroma.com/)
- [OpenAI Embeddings API](https://platform.openai.com/docs/guides/embeddings)

---

## 🤝 Support

**Pendant la formation** :

- Demander au formateur
- S'entraider entre participants
- Consulter Claude Code (il a accès à cette doc !)

**Après la formation** :

- Canal Slack/Teams dédié
- Retours d'expérience partagés
- Amélioration continue de la charte

---

**Bon courage et bon coding avec l'IA ! 🚀**
