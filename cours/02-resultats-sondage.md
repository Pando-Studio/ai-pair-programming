# Résultats du sondage interne Immodvisor

**Durée** : 15 minutes  
**Format** : Présentation des insights clés

---

## 🎯 Contexte

**Sondage réalisé** : 7-8 octobre 2025  
**Participants** : 7 développeurs sur 9 (taux de réponse : 78%)  
**Objectif** : Évaluer le niveau de maturité de l'équipe sur l'IA générative et identifier les besoins spécifiques

---

## 👥 Profil de l'équipe

### Expérience et rôles

| Poste              | Nombre | Expérience moyenne  |
| ------------------ | ------ | ------------------- |
| **Développeur**    | 4      | 9,25 ans (5-17 ans) |
| **Lead Developer** | 1      | 15 ans              |
| **CTO**            | 1      | 17 ans              |
| **Product Owner**  | 1      | 5 ans               |

**📊 Insight** : Équipe **très expérimentée** (moyenne 11,4 ans) → Attentes élevées sur qualité et pragmatisme

---

### Stack technique

**Languages & Frameworks** :

- ✅ **PHP** (7/7) - 100% de l'équipe
- ✅ **Symfony** (6/7) - 86%
- ✅ **API Platform** (6/7) - 86%
- ✅ **JavaScript** (4/7) - 57%
- Angular, React Native, SQL (minoritaires)

**IDE principal** :

- ✅ **PhpStorm** : 6/7 (86%)
- VS Code : 1/7

**Outils quotidiens** :

- **Jira** : 100% (gestion de projet)
- **Slack** : 100% (communication)
- **GitLab** : 86% (versionning)
- **Postman/Bruno** : 86% (tests API)

**🎯 Conclusion** : Stack homogène **PHP/Symfony/API Platform** + PhpStorm → Formation très ciblée possible

---

## 🤖 Maturité IA : État des lieux

### Outils IA déjà utilisés

#### IDE/Plugins IA

| Outil            | Utilisateurs | Fréquence | Satisfaction       |
| ---------------- | ------------ | --------- | ------------------ |
| **Aucun**        | 4/7 (57%)    | -         | -                  |
| **JetBrains AI** | 2/7          | En test   | "Limité"           |
| **Cursor**       | 1/7          | Gratuit   | "Trop limité"      |
| **Mammouth AI**  | 1/7          | Régulier  | Positif (Claude 4) |

**📊 Insight** : **Majorité (57%) n'utilise AUCUN outil IA dans l'IDE** → Gros potentiel d'adoption

---

#### APIs/Services IA utilisés

| Service      | Utilisateurs | Usage                                      |
| ------------ | ------------ | ------------------------------------------ |
| **OpenAI**   | 4/7 (57%)    | Recherche, questions techniques            |
| **Gemini**   | 3/7 (43%)    | Terminal, recherche (via Google Workspace) |
| **Claude**   | 2/7 (29%)    | Tests perso                                |
| **Langfuse** | 2/7 (29%)    | Observabilité (formation précédente)       |

**📊 Insight** : Usage principalement **en dehors de l'IDE**, pour recherche/questions → Pas encore de "vibe coding" intégré

---

### Niveau d'utilisation pour coder

**Question : "Utilisez-vous régulièrement de l'IAG pour vous aider à coder ?"**

- ✅ **Oui** : 1/7 (14%) - Le PO !
- ❌ **Non** : 6/7 (86%)

**Comment l'utilisent-ils ?** (pour le 1 qui l'utilise)

- "Décrire une intention métier puis laisser l'IA proposer une implémentation"
- "Questions techniques / à la place de StackOverflow" (CTO en test)

**📊 Insight MAJEUR** : **86% n'utilisent PAS l'IA pour coder** → Énorme marge de progression

---

## 🎓 Niveau de connaissance (auto-évaluation /10)

### Concepts fondamentaux

| Concept                                        | Moyenne | Min-Max | Niveau global   |
| ---------------------------------------------- | ------- | ------- | --------------- |
| **Bases LLM** (tokens, température, contexte)  | **6,0** | 4-8     | Intermédiaire   |
| **Prompting** (rôles, contraintes, itérations) | **5,6** | 3-8     | Intermédiaire   |
| **Tool/MCP/Agents**                            | **3,4** | 1-6     | **Faible**      |
| **Embeddings & recherche sémantique**          | **1,9** | 0-3     | **Très faible** |
| **RAG** (indexation, chunking)                 | **1,7** | 0-3     | **Très faible** |
| **Évaluation/qualité** (tests)                 | **3,4** | 1-5     | **Faible**      |
| **Sécurité & conformité**                      | **3,9** | 2-5     | **Faible**      |
| **Intégration IA avec PHP**                    | **2,7** | 0-5     | **Très faible** |

**📊 Insights** :

- ✅ **Bonnes bases théoriques** (LLM, prompting) grâce aux usages perso
- ❌ **Concepts avancés très faibles** (MCP, RAG, embeddings)
- ❌ **Intégration PHP quasi inexistante** → C'est précisément notre objectif !

---

## 😊 Attitude générale face à l'IA

**Question : "Quelle est votre attitude générale ?" (1-10)**

| Note     | Signification     | Réponses |
| -------- | ----------------- | -------- |
| **0**    | Très sceptique    | 1/7      |
| **4**    | Prudent           | 3/7      |
| **7**    | Optimiste modéré  | 2/7      |
| **9-10** | Très enthousiaste | 1/7      |

**Moyenne** : **5,1/10** → Attitude **prudente mais ouverte**

**📊 Insight** : Équipe **pragmatique** et **exigeante** → Besoin de preuves concrètes, pas de hype

---

## 🎯 Attentes et priorités (choix multiples)

### Top priorités de l'équipe

| Priorité                                                    | Mentions | %       |
| ----------------------------------------------------------- | -------- | ------- |
| **Générer/maintenir des tests**                             | 6/7      | **86%** |
| **Intégrations PHP (Symfony/API Platform)**                 | 5/7      | **71%** |
| **Vibe coding productif (guidelines, stratégies, prompts)** | 2/7      | 29%     |
| **RAG sur docs internes**                                   | 2/7      | 29%     |
| **Agents/outillage/MCP (CLI/terminal/automation)**          | 2/7      | 29%     |
| **Sécurité/gouvernance (RGPD, secrets)**                    | 2/7      | 29%     |
| **Évaluation des outputs (tests dorés, assertions)**        | 1/7      | 14%     |
| **Conception de modèles et base de données & SQL**          | 1/7      | 14%     |

**📊 Insights clés** :

1. **#1 : Tests** (86%) → Douleur majeure, doit être au cœur de la formation
2. **#2 : Intégration PHP/Symfony** (71%) → Besoin de cas pratiques concrets
3. Intérêt pour **RAG, MCP, Agents** (29%) → Minoritaire mais stratégique

**🎯 Conséquence pour la formation** :

- Exercice 1 DOIT inclure génération de tests
- Exercice 2 MCP/RAG répond à l'intérêt avancé
- Fil rouge charte doit couvrir Symfony/API Platform

---

## 💡 Cas pratiques souhaités

### Demandes exprimées

**Génération automatique de tests** :

> "Génération auto de test des APIs à partir de la doc OpenAPI" (CTO)

**Agents de qualité** :

> "Agent de code review sur les pre hook git avant de pouvoir merge une branch" (CTO)

**MCP pour clients** :

> "Mise en place d'un serveur MCP pour nos clients" (CTO)

**RAG sur règles fonctionnelles** :

> "Un agent qui va répondre aux règles fonctionnelles qu'il a pu étudier. Exemple : quel est le déclencheur des envois des emails d'avis publiés ?" (PO)

**Analyse UX automatique** :

> "De l'aide pour améliorer notre interface espace client (UX), qu'une IA puisse accéder/naviguer et proposer des axes d'amélioration UX" (PO)

**Génération de release notes** :

> "L'IA pourrait générer des notes de version Confluence automatiquement sur une base de tickets JIRA" (PO)

**Tests unitaires automatiques** :

> "Création de tests unitaires automatiques via agent. Vérifier la qualité de code une fois poussé sur Gitlab." (Dev)

**Refactorisation** :

> "Analyse du respect de bonnes pratiques et propositions de refactorisation (séparation du code métier de la logique)" (Lead Dev)

**📊 Insight** : Demandes **très concrètes et opérationnelles** → Équipe sait ce qu'elle veut !

---

## 😰 Préoccupations principales

### Top préoccupations (choix multiples)

| Préoccupation                                             | Mentions | %        |
| --------------------------------------------------------- | -------- | -------- |
| **Qualité et fiabilité des résultats** (risque d'erreurs) | 7/7      | **100%** |
| **Confidentialité et sécurité des données** (RGPD)        | 5/7      | **71%**  |
| **Complexité de mise en place et de maintenance**         | 3/7      | 43%      |
| **Risque de remplacement d'emplois**                      | 1/7      | 14%      |
| **Impact écologique et sociologique**                     | 1/7      | 14%      |

**📊 Insights** :

1. **100% préoccupés par la qualité** → Tests et validation OBLIGATOIRES dans la formation
2. **71% préoccupés par la sécurité** → Charte doit inclure RGPD, secrets, gouvernance
3. **43% craignent la complexité** → Formation doit montrer que c'est simple et progressif
4. **Peu de peur du chômage** (14%) → Équipe mature et confiante

**🎯 Réponses à apporter** :

- Démontrer que **tests + SAST = fiabilité** (exercice 1)
- Définir **règles de sécurité claires** (charte)
- Prouver que **c'est simple** avec cas pratiques concrets

---

## 🚀 Niveau de préparation (auto-évaluation /10)

| Note    | Signification       | Réponses  |
| ------- | ------------------- | --------- |
| **3-4** | Peu préparé         | 3/7 (43%) |
| **5**   | Moyennement préparé | 1/7 (14%) |
| **7**   | Bien préparé        | 2/7 (29%) |
| **9**   | Très préparé        | 1/7 (14%) |

**Moyenne** : **5,4/10** → Niveau **moyen**, besoin de montée en compétences

**📊 Insight** : Équipe **consciente de ses lacunes** et **volontaire pour apprendre**

---

## 🛠️ Prérequis techniques

### Outils IA déjà installés

| Réponse                                                              | Nombre | %   |
| -------------------------------------------------------------------- | ------ | --- |
| **Non**                                                              | 4/7    | 57% |
| **Oui** (Cursor gratuit, JetBrains AI, Mammouth AI, Gemini terminal) | 3/7    | 43% |

**📊 Insight** : **Majorité n'a RIEN installé** → Installation Claude Code nécessaire avant la formation

---

### Droits d'installation

| Réponse        | Nombre |
| -------------- | ------ |
| **Oui**        | 6/7    |
| **Non**        | 1/7    |
| **Je suppose** | 1/7    |

**✅ OK** : Pas de blocage technique pour installation

---

### Comptes/Clés API disponibles

**Comptes professionnels** :

- **Gemini** (via Google Workspace) : 2/7
- **OpenAI** : 2/7

**Comptes personnels** :

- **ChatGPT** : Quelques-uns
- **Claude** : Quelques-uns

**Clés API** :

- **OpenAI** : 2/7 ont une clé dispo
- **Gemini** : 1/7

**📊 Insight** : **Fourniture de clés API OpenAI obligatoire** pour la formation

---

### Contraintes techniques

- **Aucune contrainte** : 6/7
- **VPN/proxy** : "À voir avec DSI" (1/7)

**✅ OK** : Pas de blocage majeur identifié

---

## 🎯 Synthèse : Portrait-robot de l'équipe

### Forces

✅ **Équipe senior** (moyenne 11,4 ans d'expérience)  
✅ **Stack homogène** (PHP/Symfony/API Platform)  
✅ **Bonnes bases théoriques** LLM/Prompting  
✅ **Pragmatiques et exigeants** (attitude prudente mais ouverte)  
✅ **Besoins clairement identifiés** (tests, intégrations PHP)  
✅ **Pas de blocage technique** (droits installation, accès internet)

### Points de vigilance

⚠️ **86% n'utilisent PAS l'IA pour coder** actuellement  
⚠️ **Concepts avancés très faibles** (MCP, RAG, embeddings)  
⚠️ **100% préoccupés par la qualité** → Besoin de preuves  
⚠️ **71% préoccupés par la sécurité** → Charte obligatoire  
⚠️ **Peu de confiance sans validation** → Démo concrète nécessaire

### Opportunités

🚀 **Majorité sans outil IA** → Énorme marge de progression  
🚀 **Forte demande de tests automatisés** → Quick win possible  
🚀 **Intérêt pour MCP/RAG** → Cas d'usage différenciant  
🚀 **Équipe volontaire** → Formation bien accueillie

---

## 📋 Implications pour la formation

### Ce qu'il FAUT absolument faire

1. **Prouver la fiabilité avec tests** → Exercice 1 DOIT inclure TDD strict
2. **Montrer des cas concrets PHP/Symfony** → Pas de théorie abstraite
3. **Définir la charte de sécurité** → Répondre à la préoccupation #1
4. **Rester pragmatique** → Pas de hype, que du concret
5. **Installer Claude Code avant la formation** → 57% n'ont rien actuellement

### Ce qu'il faut ÉVITER

❌ Trop de théorie (équipe senior)  
❌ Exemples hors contexte PHP/Symfony  
❌ Promesses sans preuves (équipe sceptique)  
❌ Complexité inutile (43% craignent la complexité)  
❌ Ignorer les questions de sécurité (71% préoccupés)

---

## 💬 Citations marquantes

> "Je n'utilise jamais de plugin IA intégré à un IDE. Mais les récentes MAJ de PhpStorm intègrent de la suggestion de code qui ressemble un peu à de l'IA."  
> — Dev, 17 ans d'expérience

> "L'objectif pour moi est de pouvoir créer divers agents pour des traitements isolés."  
> — Dev, 5-6 ans d'expérience

> "Contrainte de budget"  
> — Dev concernant l'adoption d'outils IA payants

> "Que ce soit clair ce qu'on a le droit de faire ou pas, et avec quelle IA"  
> — PO sur la gouvernance

**📊 Insight** : Équipe **consciente du potentiel** mais **prudente** sur coûts, gouvernance et fiabilité

---

**Prochain module** : [Méthodologies de vibe coding](03-methodologies-vibe-coding.md)
