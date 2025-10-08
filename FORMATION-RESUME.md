# Formation AI Pair Programming - Résumé exécutif

**Formateur** : Yacine Arhalaiss  
**Public** : 9 développeurs Immodvisor  
**Durée** : 7 heures  
**Date prévue** : [À définir]

---

## ✅ Statut de préparation

### Contenus créés

| Élément                  | Statut                    | Fichier                                                              |
| ------------------------ | ------------------------- | -------------------------------------------------------------------- |
| **Programme détaillé**   | ✅ Complet                | [PROGRAMME-FORMATION.md](PROGRAMME-FORMATION.md)                     |
| **Contenus théoriques**  | ✅ Complets (4 modules)   | [cours/](cours/)                                                     |
| **Exercices pratiques**  | ✅ Complets (2 exercices) | [exercices/](exercices/)                                             |
| **Charte d'utilisation** | ✅ Template prêt          | [charte/guidelines-vibe-coding.md](charte/guidelines-vibe-coding.md) |

---

## 📚 Structure du repository

```
ai-pair-programming/
├── PROGRAMME-FORMATION.md         # Programme détaillé 7h
├── FORMATION-RESUME.md             # Ce fichier (résumé exécutif)
│
├── cours/                          # Contenus théoriques (1h10)
│   ├── README.md
│   ├── 01-introduction.md          # 20min - Historique, chiffres, tendances
│   ├── 02-resultats-sondage.md     # 15min - Analyse équipe Immodvisor
│   ├── 03-methodologies-vibe-coding.md  # 30min - PACT-R + démo
│   └── 04-concepts-fondamentaux.md # 10min - LLM, MCP, RAG
│
├── exercices/                      # Exercices pratiques (4h)
│   ├── README.md
│   ├── exercice-1-api-avis-pact-r.md      # 2h - API avec PACT-R
│   └── exercice-2-serveur-mcp-rag.md      # 2h - MCP + RAG
│
├── charte/                         # Charte & guidelines (1h fil rouge)
│   ├── README.md
│   └── guidelines-vibe-coding.md   # Template à compléter
│
├── examples/                       # Exemples PACT-R détaillés
│   ├── plan-phase.md
│   ├── coding-phase.md
│   ├── test-phase.md
│   ├── review-phase.md
│   └── metrics-template.md
│
├── README.md                       # Méthodologie PACT-R complète
├── input-plan-workflow.md          # Workflows PLAN selon inputs
├── Constat métier de développeur, IAG.md   # Ressource source
├── data Gen AI in Code.md          # Chiffres clés vérifiés
└── Formation IAG & automation...csv # Questionnaire (7 réponses)
```

---

## 🎯 Vue d'ensemble de la formation

### Session 1 : Contexte & Fondamentaux (1h) - 9h00-10h00

| Timing     | Contenu                           | Support                                                          |
| ---------- | --------------------------------- | ---------------------------------------------------------------- |
| 9h00-9h15  | Accueil & Tour de table           | -                                                                |
| 9h15-9h35  | **Historique & marché** (20min)   | [01-introduction.md](cours/01-introduction.md)                   |
| 9h35-9h50  | **Résultats sondage** (15min)     | [02-resultats-sondage.md](cours/02-resultats-sondage.md)         |
| 9h50-10h00 | **Concepts fondamentaux** (10min) | [04-concepts-fondamentaux.md](cours/04-concepts-fondamentaux.md) |

**Insights clés du sondage** :

- 86% n'utilisent PAS l'IA pour coder actuellement
- 100% préoccupés par la qualité
- 71% préoccupés par la sécurité
- Top priorité : Génération/maintenance de tests (86%)

---

### Session 2 : Méthodes & Charte (1h) - 10h10-11h10

| Timing      | Contenu                           | Support                                                                  |
| ----------- | --------------------------------- | ------------------------------------------------------------------------ |
| 10h10-10h40 | **Méthodologies PACT-R** (30min)  | [03-methodologies-vibe-coding.md](cours/03-methodologies-vibe-coding.md) |
| 10h40-11h10 | **Atelier : Charte v0.1** (30min) | [guidelines-vibe-coding.md](charte/guidelines-vibe-coding.md)            |

**Démo live** : Créer un endpoint simple avec Claude Code (PLAN → ASSERT → CODE → TEST)

---

### Session 3 : Exercice 1 - API Avis PACT-R (2h) - 11h10-13h10

| Checkpoint           | Durée | Contenu                                            |
| -------------------- | ----- | -------------------------------------------------- |
| **1. PLAN**          | 30min | Générer dataset + Specs (ERD, OpenAPI) + Découpage |
| **2. ASSERT + CODE** | 1h    | Tests RED → Code GREEN avec Claude Code            |
| **3. TEST (BLUE)**   | 30min | Refactoring + PHPStan niveau 9                     |
| **4. REVIEW**        | 10min | Démo + Retours d'expérience                        |

**Support** : [exercice-1-api-avis-pact-r.md](exercices/exercice-1-api-avis-pact-r.md)

---

### Session 4 : Exercice 2 - MCP + RAG (2h) - 14h10-16h10

| Checkpoint          | Durée | Contenu                                                 |
| ------------------- | ----- | ------------------------------------------------------- |
| **1. Dataset**      | 30min | Générer 50-100 avis + Installer dépendances             |
| **2. Indexation**   | 45min | Embeddings OpenAI + ChromaDB + Test recherche           |
| **3. MCP Server**   | 45min | 3 tools (search, stats, sentiment) + Config Claude Code |
| **4. Tests & Démo** | 30min | Requêtes sémantiques + Démo collective                  |

**Support** : [exercice-2-serveur-mcp-rag.md](exercices/exercice-2-serveur-mcp-rag.md)

---

### Session 5 : Finalisation & Retours (1h) - 16h20-17h20

| Timing      | Contenu                                                                     |
| ----------- | --------------------------------------------------------------------------- |
| 16h20-16h50 | **Complétion charte** (30min) : Prompts validés, règles sécu, workflow      |
| 16h50-17h10 | **Démos & Partages** (20min) : 2-3 participants montrent leurs réalisations |
| 17h10-17h20 | **Conclusion & Next steps** (10min) : Plan d'adoption progressif            |

---

## 🎓 Points clés de la formation

### Messages à faire passer

1. **L'IA accélère SI cadrage strict**

   - Specs claires + Tests d'abord + Review outillée = Gains réels
   - Sans cadre = Perte de temps + Risques sécu

2. **PACT-R = Méthodologie éprouvée**

   - Investir en PLAN pour accélérer ensuite
   - TDD strict (RED → GREEN → BLUE)
   - Métriques continues

3. **Sécurité et qualité non négociables**

   - Jamais de secrets dans les prompts
   - PHPStan niveau 9 obligatoire
   - Review humaine systématique

4. **Adoption progressive**
   - Start small : tâches simples bien cadrées
   - Measure : métriques (temps, qualité, coût)
   - Adapt : ajuster selon retours terrain

---

## 📊 Métriques de succès de la formation

### Pendant la formation

- [ ] 100% des participants ont testé Claude Code
- [ ] Au moins 5 prompts types validés
- [ ] Charte v1.0 consensuelle
- [ ] 2 exercices complétés (au moins MVP)

### Après la formation (2 semaines)

- [ ] 80% de l'équipe utilise l'IA au moins 1x/semaine
- [ ] Charte appliquée et ajustée selon retours
- [ ] Premiers gains mesurés (vélocité, qualité)
- [ ] Bibliothèque de prompts alimentée

---

## 🛠️ Prérequis techniques à valider AVANT la formation

### Installations obligatoires

- [ ] **Claude Code** installé sur tous les postes (9/9)
- [ ] **Clés API OpenAI** distribuées à tous (9/9)
- [ ] **PHP 8.2+** + **Symfony** + **Composer** (vérifier versions)
- [ ] **Python 3.9+** OU **Node.js 18+** (pour exercice 2)
- [ ] **Git** configuré
- [ ] Ce repository cloné localement

### Environnement de dev

- [ ] Serveur local fonctionnel (Symfony CLI ou Docker)
- [ ] Base de données (SQLite ou PostgreSQL)
- [ ] Connexion internet stable (appels API OpenAI)
- [ ] Droits d'installation (confirmé par 6/7 dans le sondage)

### Matériel

- [ ] Projecteur/écran pour présentations
- [ ] Paper board ou tableau pour atelier charte
- [ ] Post-its (pour brainstorming collaboratif)

---

## 📋 Checklist formateur J-1

### Préparation contenus

- [ ] Convertir les MD en slides (Marp, reveal.js, ou Google Slides)
- [ ] Préparer la démo live (exercice simple PACT-R)
- [ ] Tester les 2 exercices en conditions réelles
- [ ] Vérifier que les prompts suggérés fonctionnent

### Préparation logistique

- [ ] Confirmer les horaires avec les participants
- [ ] Vérifier la salle et le matériel (projecteur, wifi)
- [ ] Préparer les clés API OpenAI (9 clés)
- [ ] Envoyer le lien du repo en avance

### Matériel pédagogique

- [ ] Imprimer la charte (1 exemplaire par participant)
- [ ] Préparer des templates de retour d'expérience
- [ ] Post-its et feutres pour atelier collaboratif

---

## 🎯 Livrables post-formation

### Immédiats (fin de journée)

1. **Charte v1.0 finalisée** : Validée collectivement
2. **Code des exercices** : Partagé sur GitLab/GitHub
3. **Bibliothèque de prompts** : 5-10 prompts validés
4. **Métriques initiales** : Temps, tokens, qualité

### À 2 semaines

1. **Retours d'expérience** : Questionnaire de satisfaction
2. **Ajustements charte** : Selon retours terrain
3. **Premiers gains mesurés** : Vélocité, qualité
4. **Plan d'adoption** : Roadmap 3 mois

### À 1 mois

1. **Formation nouveaux arrivants** : Utilisation de ce repo
2. **Optimisation workflows** : Amélioration continue
3. **Extension MCP** : Autres cas d'usage (docs internes, JIRA)

---

## 🚀 Roadmap d'adoption (après la formation)

### Phase 1 : Expérimentation (Semaine 1-2)

**Objectif** : Se familiariser avec les outils

- ✅ Tester sur petites tâches (génération tests, refactoring simple)
- ✅ Partager les retours en retro IA hebdomadaire
- ✅ Alimenter la bibliothèque de prompts

**Critères de succès** :

- 100% de l'équipe a testé au moins 1 outil IA
- Au moins 5 prompts types validés

---

### Phase 2 : Premiers projets (Semaine 3-4)

**Objectif** : Appliquer PACT-R sur feature réelle

- ✅ Choisir 1-2 features moyennes (2-3 jours)
- ✅ Appliquer strictement PACT-R
- ✅ Mesurer les métriques
- ✅ Ajuster la charte selon retours

**Critères de succès** :

- Feature livrée avec qualité >= baseline
- Métriques collectées et analysées
- Charte ajustée v1.1

---

### Phase 3 : Généralisation (Mois 2+)

**Objectif** : Intégrer dans le workflow quotidien

- ✅ Utiliser IA sur tous les nouveaux projets
- ✅ Optimiser les prompts et workflows
- ✅ Former les nouveaux arrivants avec ce repo

**Critères de succès** :

- 80% des features utilisent IA
- Vélocité mesurée > 1.5x
- NPS équipe > 8/10

---

## 💡 Conseils pour la journée

### Pour maximiser l'engagement

- ✅ Poser des questions régulièrement (sonder l'équipe)
- ✅ Adapter le rythme selon les retours
- ✅ Valoriser les contributions (prompts, idées)
- ✅ Rester pragmatique (pas de hype, que du concret)

### Pour gérer le timing

- ✅ Checkpoints stricts sur les exercices
- ✅ Préparer des bonus pour les plus rapides
- ✅ Avoir des exemples de code prêts si blocage

### Pour maximiser l'apprentissage

- ✅ Démos live plutôt que slides statiques
- ✅ Encourager l'entraide entre participants
- ✅ Documenter les prompts efficaces en temps réel

---

## 📞 Contacts et support

### Pendant la formation

- **Formateur** : Yacine Arhalaiss
- **Support technique** : Claude Code (il a accès à cette doc !)

### Après la formation

- **Canal Slack/Teams** : [À créer]
- **Repository GitLab** : [À définir]
- **Retros IA hebdomadaires** : Vendredi 15h (suggéré)

---

## 📚 Ressources complémentaires

### Pour approfondir

- [README.md](README.md) - Méthodologie PACT-R complète
- [input-plan-workflow.md](input-plan-workflow.md) - Workflows PLAN détaillés
- [examples/](examples/) - Exemples PACT-R étape par étape

### Sources de données

- [Constat métier de développeur, IAG.md](Constat%20métier%20de%20développeur,%20IAG.md) - Analyse du métier
- [data Gen AI in Code.md](data%20Gen%20AI%20in%20Code.md) - Chiffres clés vérifiés
- [CSV questionnaire](Formation%20IAG%20&%20automation%20-%20Dev_Votre%20expérience,%20vos%20besoins,%20vos%20idées_Submissions_2025-10-08.csv) - Sondage équipe

---

## ✅ Checklist finale avant la formation

### J-7

- [ ] Confirmer la date avec les participants
- [ ] Valider la salle et le matériel
- [ ] Envoyer le lien du repo pour pré-lecture
- [ ] Préparer les clés API OpenAI

### J-1

- [ ] Tester tous les exercices
- [ ] Vérifier les installations (Claude Code, PHP, etc.)
- [ ] Préparer la démo live
- [ ] Imprimer la charte

### J-Day

- [ ] Arriver 15min en avance
- [ ] Tester le projecteur et la connexion internet
- [ ] Distribuer les clés API
- [ ] Let's go ! 🚀

---

**Bonne formation et bon coding avec l'IA ! 🎓💻**
