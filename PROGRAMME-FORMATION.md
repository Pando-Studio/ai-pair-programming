# Programme de formation : AI Pair Programming & Vibe Coding

## 🎯 Informations générales

**Durée** : 7 heures  
**Public** : développeurs  
**Niveau** : Débutant à intermédiaire en IA générative  
**Format** : Présentiel avec exercices pratiques semi-ouverts  
**Prérequis techniques** :

- Claude Code installé
- Clés API OpenAI fournies
- PHP 8.x + Symfony + Composer
- Git, IDE (PhpStorm recommandé)

---

## 📋 Objectifs pédagogiques

À l'issue de cette formation, les participants seront capables de :

1. **Comprendre** les concepts fondamentaux de l'IA générative pour le code (LLM, tokens, prompting, MCP, RAG)
2. **Appliquer** méthodologie de ai pair programming, pour développer avec l'IA
3. **Créer** une API complète avec tests en utilisant l'assistance IA
4. **Construire** un serveur MCP connecté à une base vectorielle
5. **Définir** une charte d'utilisation et des guidelines adaptées à leur contexte

---

## 🕐 Déroulé détaillé (7h)

### \*\*Session 1 : Contexte & Fondamentaux

#### 9h00-9h15 : Accueil & Tour de table (15min)

- Présentation formateur et participants
- Attentes et objectifs individuels
- Logistique de la journée

#### 9h15-9h35 : État des lieux du marché (20min)

📖 **Support** : [`cours/01-introduction.md`](cours/01-introduction.md)

**Contenu** :

- Historique du ai pair programming (vibe coding) (de GitHub Copilot à Claude Code/Cursor)
- Chiffres clés vérifiés (adoption, productivité, emploi)
- Tendances du métier de développeur
- Mythes vs réalité (fiabilité, sécurité, impact environnemental)

**Format** : Présentation interactive avec discussions

#### 9h35-9h50 : Résultats du sondage interne (15min)

📖 **Support** : [`cours/02-resultats-sondage.md`](cours/02-resultats-sondage.md)

**Contenu** :

- Analyse des réponses
- Niveau de maturité de l'équipe
- Besoins et attentes spécifiques
- Préoccupations principales (qualité, sécurité, complexité)

**Format** : Présentation des insights clés

#### 9h50-10h00 : Concepts fondamentaux (10min)

📖 **Support** : [`cours/04-concepts-fondamentaux.md`](cours/04-concepts-fondamentaux.md)

**Contenu rapide** :

- LLM, tokens, température, contexte
- Prompting efficace (rôles, contraintes, itérations)
- MCP (Model Context Protocol)
- RAG (Retrieval Augmented Generation)
- Embeddings et recherche sémantique

**Format** : Présentation synthétique (approfondissement durant les exercices)

---

### **🔟 Pause (10min) - 10h00-10h10**

---

### **Session 2 : Méthodes & Charte (1h) - 10h10-11h10**

#### 10h10-10h40 : Méthodologies de vibe coding (30min)

📖 **Support** : [`cours/03-methodologies-vibe-coding.md`](cours/03-methodologies-vibe-coding.md)

**Contenu** :

- **Origine** : Plan-Act-Review-Repeat (Andrej Karpathy, 2025)
- **PACT-R** : Extension avec Assert et Test (Plan, Assert, Code, Test, Review)
- Philosophie : specs d'abord, puis TDD avec IA
- API-First + Test-Driven Development
- Workflows selon inputs (Greenfield, JIRA, Figma, etc.)
- Garde-fous anti-over-engineering (YAGNI, Monolith-First)
- Démonstration courte avec Claude Code

**Ressources** : [`ressources/historique.md`](cours/ressources/historique.md) pour l'historique complet

**Format** : Présentation + démo live (5min)

#### 10h40-11h10 : Atelier : Construction de la charte d'utilisation (30min)

📖 **Support** : [`charte/guidelines-vibe-coding.md`](charte/guidelines-vibe-coding.md)

**Activité collaborative** :

- Présentation du template de charte
- Discussion collective sur les 5 dimensions :
  1. **Standards de code** (PSR-12, conventions Symfony)
  2. **Sécurité & RGPD** (secrets, données sensibles)
  3. **Prompts types** (cas d'usage courants)
  4. **Gouvernance** (outils autorisés, validation)
  5. **Workflow de review** (tests obligatoires, CI/CD)
- Chaque participant note ses besoins/contraintes
- Mise en commun et priorisation des règles

**Livrable** : Draft v1 de la charte (à compléter en fil rouge)

---

### **Session 3 : Exercice 1 - API Avis avec PACT-R (2h) - 11h10-13h10**

#### 11h10-11h25 : Présentation de l'exercice (15min)

📖 **Support** : [`exercices/exercice-1-api-avis-pact-r.md`](exercices/exercice-1-api-avis-pact-r.md)

**Contexte métier** :
Créer une API de gestion d'avis simplifiée pour Immodvisor en suivant strictement la méthode PACT-R.

**Objectifs** :

- Phase PLAN : Spécifications (User Flows, ERD, OpenAPI)
- Phase ASSERT : Écrire les tests d'abord (RED)
- Phase CODE : Implémentation minimale avec IA (GREEN)
- Phase TEST : Refactoring et amélioration (BLUE)
- Phase REVIEW : Démo et métriques

**Stack technique** :

- Symfony 6+ avec API Platform
- PHPUnit pour les tests
- Claude Code comme assistant IA

**Format** : Semi-ouvert avec checkpoints

#### 11h25-13h10 : Réalisation de l'exercice (1h45)

**Checkpoint 1 (30min) : Phase PLAN**

- Générer le jeu de données (faux avis avec IA)
- Créer les spécifications (User Flows, ERD, OpenAPI)
- Découper en tâches (2-4h max)

**Checkpoint 2 (30min) : Phase ASSERT + CODE**

- Écrire les tests unitaires d'abord (RED)
- Demander à l'IA de générer l'implémentation
- Passer au GREEN

**Checkpoint 3 (30min) : Phase TEST + REVIEW**

- Refactoring avec l'IA
- Lancer PHPStan/Psalm
- Démo rapide de sa feature

**Checkpoint 4 (15min) : Retours d'expérience**

- Qu'est-ce qui a fonctionné ?
- Qu'est-ce qui a bloqué ?
- Premiers apprentissages pour la charte

---

### **🍽️ Pause déjeuner (1h) - 13h10-14h10**

---

### **Session 4 : Exercice 2 - Serveur MCP + RAG (2h) - 14h10-16h10**

#### 14h10-14h25 : Présentation de l'exercice (15min)

📖 **Support** : [`exercices/exercice-2-serveur-mcp-rag.md`](exercices/exercice-2-serveur-mcp-rag.md)

**Contexte** :
Créer un serveur MCP (Model Context Protocol) qui expose une base de données vectorielle d'avis Immodvisor pour enrichir le contexte de Claude Code.

**Objectifs** :

- Comprendre le protocole MCP
- Générer des embeddings d'avis avec OpenAI
- Stocker dans une base vectorielle (ChromaDB ou SQLite avec extension)
- Exposer via MCP pour interrogation sémantique
- Tester l'intégration avec Claude Code

**Use case** :
Permettre à l'IA de rechercher des avis similaires, analyser des tendances, ou générer des insights métier en interrogeant la base vectorielle.

**Format** : Semi-ouvert avec checkpoints

#### 14h25-16h10 : Réalisation de l'exercice (1h45)

**Checkpoint 1 (30min) : Génération du dataset**

- Utiliser l'IA pour générer 50-100 faux avis réalistes
- Format JSON avec : id, note, commentaire, date, agence, auteur

**Checkpoint 2 (45min) : Création des embeddings**

- Utiliser l'API OpenAI Embeddings
- Stocker dans ChromaDB ou SQLite avec extension vectorielle
- Indexer les avis

**Checkpoint 3 (30min) : Serveur MCP**

- Créer le serveur MCP (Node.js ou Python)
- Exposer les opérations :
  - `search_avis` : Recherche sémantique
  - `get_stats` : Statistiques sur les avis
  - `analyze_sentiment` : Analyse de sentiment global
- Configurer Claude Code pour utiliser le serveur

**Checkpoint 4 (10min) : Test & démo**

- Interroger le serveur MCP depuis Claude Code
- Exemples de requêtes sémantiques
- Discussion sur les cas d'usage possibles

---

### **🔟 Pause (10min) - 16h10-16h20**

---

### **Session 5 : Finalisation charte & Retours (1h) - 16h20-17h20**

#### 16h20-16h50 : Complétion de la charte (30min)

**Activité collaborative** :

- Retour sur les apprentissages des 2 exercices
- Complétion de la charte avec :
  - **Prompts validés** pour cas d'usage Symfony/API Platform
  - **Règles de sécurité** spécifiques (secrets, données clients)
  - **Workflow de validation** (review, tests, métriques)
  - **Outils autorisés** et gouvernance
  - **Guidelines de code** (standards Symfony, PSR-12)

**Livrable** : Charte v1.0 finalisée et consensuelle

#### 16h50-17h10 : Démos & Partages (20min)

**Format** : Tour de table rapide

- 2-3 participants montrent leur réalisation (API ou MCP)
- Partage des difficultés et solutions trouvées
- Discussion sur les prompts qui ont bien fonctionné

#### 17h10-17h20 : Conclusion & Prochaines étapes (10min)

**Synthèse** :

- Récapitulatif des concepts clés
- Ressources pour aller plus loin
- Plan d'adoption progressif chez Immodvisor :
  - Semaine 1 : Tester sur petites tâches
  - Semaine 2-4 : Premiers projets PACT-R
  - Mois 2+ : Optimisation continue

**Q&A finale**

---

## 📚 Supports et ressources

### Documentation de référence (dossier `cours/ressources/`)

1. [`historique.md`](cours/ressources/historique.md) - Origine du vibe coding, Plan-Act-Review-Repeat, personnalités clés
2. [`data.md`](cours/ressources/data.md) - Chiffres clés vérifiés avec sources et URLs
3. [`constat.md`](cours/ressources/constat.md) - Analyse du marché et tendances

### Contenus théoriques (dossier `cours/`)

1. [`01-introduction.md`](cours/01-introduction.md) - Historique, chiffres, tendances
2. [`02-resultats-sondage.md`](cours/02-resultats-sondage.md) - Analyse du sondage interne
3. [`03-methodologies-vibe-coding.md`](cours/03-methodologies-vibe-coding.md) - PACT-R et méthodes
4. [`04-concepts-fondamentaux.md`](cours/04-concepts-fondamentaux.md) - LLM, MCP, RAG, etc.

### Exercices pratiques (dossier `exercices/`)

1. [`exercice-1-api-avis-pact-r.md`](exercices/exercice-1-api-avis-pact-r.md) - API avec PACT-R (2h)
2. [`exercice-2-serveur-mcp-rag.md`](exercices/exercice-2-serveur-mcp-rag.md) - MCP + RAG (2h)

### Charte & Guidelines (dossier `charte/`)

1. [`guidelines-vibe-coding.md`](charte/guidelines-vibe-coding.md) - Template à compléter en fil rouge

### Références

- [README.md - Méthodologie PACT-R](README.md)
- [input-plan-workflow.md - Workflows PLAN](input-plan-workflow.md)
- Exemples détaillés dans `examples/`

---

## 🎓 Critères de réussite

### Pour les participants

- [ ] Comprendre la méthodologie PACT-R et savoir quand l'appliquer
- [ ] Avoir créé une API complète avec tests guidés par l'IA
- [ ] Avoir construit et testé un serveur MCP fonctionnel
- [ ] Contribuer à la charte d'utilisation de l'équipe
- [ ] Identifier 3-5 cas d'usage concrets pour leur travail quotidien

### Pour l'équipe Immodvisor

- [ ] Charte d'utilisation consensuelle et applicable
- [ ] Premiers exemples de code généré avec IA + tests
- [ ] Compréhension partagée des bonnes pratiques
- [ ] Plan d'adoption progressif défini
- [ ] Base de connaissance (ce repo) pour onboarding futurs devs

---

## 🛠️ Matériel nécessaire

### Avant la formation

- [ ] Installer Claude Code sur tous les postes
- [ ] Distribuer les clés API OpenAI
- [ ] Vérifier PHP 8.x + Symfony + Composer installés
- [ ] Cloner ce repository sur tous les postes
- [ ] Préparer environnement de dev (serveur local, DB)

### Pendant la formation

- [ ] Projecteur/écran pour les présentations
- [ ] Connexion internet stable (appels API)
- [ ] Paper board ou tableau pour collaboration sur charte
- [ ] Post-its pour atelier collaboratif

### Après la formation

- [ ] Partager le repository mis à jour avec charte finalisée
- [ ] Envoyer les slides et supports en PDF
- [ ] Créer un canal Slack/Teams dédié pour questions/partage
- [ ] Planifier un point de suivi à 2 semaines

---

## 📊 Évaluation post-formation

### Questionnaire de satisfaction (5min)

- Clarté des concepts (1-5)
- Pertinence des exercices (1-5)
- Utilité pour le travail quotidien (1-5)
- Qualité de l'animation (1-5)
- Recommanderiez-vous cette formation ? (NPS 0-10)

### Suivi à 2 semaines

- Combien de fois avez-vous utilisé l'IA pour coder ?
- Quels cas d'usage ont le mieux fonctionné ?
- Quels blocages avez-vous rencontrés ?
- La charte est-elle appliquée ? Doit-elle être ajustée ?

---

## 🚀 Prochaines étapes suggérées

### Court terme (1 mois)

1. Appliquer PACT-R sur une petite feature réelle
2. Créer un serveur MCP pour docs internes Immodvisor
3. Affiner la charte selon retours terrain

### Moyen terme (3 mois)

1. Généraliser l'usage sur nouveaux projets
2. Mesurer les gains (vélocité, qualité, satisfaction)
3. Former les nouveaux arrivants avec ce repo

### Long terme (6+ mois)

1. Contribuer à la méthodologie PACT-R (retours d'expérience)
2. Construire une bibliothèque de prompts réutilisables
3. Automatiser davantage (agents de review, génération de tests)

---

**Bon courage et bon coding avec l'IA ! 🤖💻**
