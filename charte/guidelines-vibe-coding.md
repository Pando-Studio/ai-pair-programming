# Charte d'utilisation de l'IA générative - Immodvisor

**Version** : 1.0 (Draft - à finaliser pendant la formation)  
**Date** : 8 octobre 2025  
**Équipe** : Développeurs Immodvisor

---

## 🎯 Objectif de cette charte

Cette charte définit les **règles d'utilisation de l'IA générative** (Claude Code, GitHub Copilot, etc.) pour le développement chez Immodvisor.

**Pourquoi ?**

- ✅ Garantir la **qualité et la fiabilité** du code généré
- ✅ Protéger la **sécurité et la confidentialité** des données
- ✅ Harmoniser les **pratiques** au sein de l'équipe
- ✅ Maximiser la **productivité** tout en minimisant les risques

**Public** : Tous les développeurs, lead developers, CTO

---

## 📜 Principes directeurs

### 1. L'IA est un outil d'assistance, pas un remplacement

- ✅ L'IA **accélère** les développeurs compétents
- ❌ L'IA **ne remplace pas** la réflexion architecturale et la review humaine
- ✅ Le développeur reste **responsable** du code mergé

### 2. Qualité et tests non négociables

- ✅ **Tests obligatoires** avant toute implémentation (TDD)
- ✅ **Analyse statique** (PHPStan niveau 9, Psalm) sur tout code généré
- ✅ **Review humaine** systématique

### 3. Sécurité et confidentialité prioritaires

- ❌ **Jamais** de secrets (clés API, tokens, mots de passe) dans les prompts
- ❌ **Jamais** de données clients identifiables
- ✅ Utiliser uniquement des **outils approuvés** par la DSI

### 4. Amélioration continue

- ✅ Partager les **prompts efficaces** avec l'équipe
- ✅ Documenter les **blocages** et solutions
- ✅ Mesurer et ajuster

---

## 🛠️ 1. Outils autorisés

### Outils approuvés ✅

| Outil                    | Usage autorisé   | Compte                   | Remarques                       |
| ------------------------ | ---------------- | ------------------------ | ------------------------------- |
| **Claude Code**          | ✅ Oui           | Professionnel (fourni)   | Outil principal de la formation |
| **GitHub Copilot**       | ⚠️ À valider DSI | Professionnel uniquement | Si subscription entreprise      |
| **JetBrains AI**         | ⚠️ En test       | Professionnel            | Intégré PhpStorm                |
| **ChatGPT / Claude web** | ⚠️ Limité        | Perso ou pro             | **Pas de code sensible**        |
| **Gemini**               | ⚠️ Limité        | Google Workspace         | Via terminal uniquement         |

### Outils interdits ❌

| Outil                             | Raison                                      |
| --------------------------------- | ------------------------------------------- |
| **Outils gratuits non approuvés** | Pas de garantie de confidentialité          |
| **Auto-run de code**              | Risque sécurité (exécution sans validation) |
| **Outils sans trace d'audit**     | Impossible de tracer les usages             |

**📝 À compléter pendant la formation** : Liste finale validée par l'équipe

---

## 🔒 2. Sécurité et gouvernance

### 2.1 Données interdites dans les prompts

**❌ JAMAIS envoyer à l'IA** :

- Clés API, tokens, secrets (`.env`, credentials)
- Données clients identifiables :
  - Emails réels
  - Noms/prénoms de clients
  - Adresses réelles
  - Numéros de téléphone
  - Informations bancaires
- Code contenant des secrets en dur
- Logs de production avec données sensibles

**✅ Acceptable** :

- Code source sans secrets (logique métier, architecture)
- Données anonymisées ou fictives
- Specs fonctionnelles sans données réelles
- Erreurs techniques sans contexte client

---

### 2.2 Checklist avant chaque prompt

**Avant d'envoyer un prompt, vérifier** :

- [ ] Pas de secrets ou credentials
- [ ] Pas de données clients identifiables
- [ ] Code sanitized (anonymisé si nécessaire)
- [ ] Contexte métier non confidentiel

**En cas de doute** → Demander au Lead Dev ou CTO

---

### 2.3 Gestion des secrets

**Règles** :

1. **Toujours utiliser `.env`** pour les secrets
2. **Ajouter `.env` au `.gitignore`**
3. **Utiliser des placeholders** dans les prompts :

```markdown
# ❌ MAUVAIS PROMPT

Voici mon code :
$apiKey = "sk-proj-abc123..."

# ✅ BON PROMPT

Voici mon code :
$apiKey = $\_ENV['OPENAI_API_KEY'];
```

4. **Scanner le code** avant commit :

   ```bash
   # Installer gitleaks (scanner de secrets)
   brew install gitleaks

   # Scanner avant commit
   gitleaks detect --source . --verbose
   ```

---

### 2.4 RGPD et confidentialité

**Principes** :

- ✅ Données envoyées à l'IA = **traitées hors UE** (selon outil)
- ✅ Utiliser des **comptes entreprise** avec DPA (Data Processing Agreement)
- ❌ **Pas de données personnelles** sans anonymisation

**📝 À compléter** : Validation DSI sur les outils et DPA signés

---

## 💻 3. Standards de code et bonnes pratiques

### 3.1 Guidelines Symfony / API Platform

**Conventions à respecter** :

1. **Architecture** : Controller → Service → Repository
2. **Typage strict** : PHP 8.2+ avec type hints obligatoires
3. **PSR-12** : Standards de codage PHP
4. **Doctrine** : Annotations pour entités
5. **API Platform** : Resource attributes sur entités
6. **Validation** : Symfony Validator (annotations)

**Exemple de prompt type** :

```markdown
## Contexte

Symfony 6.4 + API Platform 3.2 + Doctrine ORM

Architecture :

- Controller : Pas de logique métier, délégation au Service
- Service : Logique métier
- Repository : Requêtes base de données

## Tâche

Crée un service ReviewService avec une méthode createReview()

## Contraintes

- PHP 8.2 strict typing
- Injection de dépendances (constructeur)
- Validation via Symfony Validator
- Exceptions métier custom (ReviewAlreadyExistsException)
- Respecter PSR-12
- Pas de logique dans le Controller
```

---

### 3.2 Règles métier Immodvisor

**Contraintes spécifiques** :

- **Avis** : Un utilisateur (email) = 1 avis max par agence
- **Notes** : Obligatoire de 1 à 5 étoiles
- **Commentaires** : Min 10 caractères, max 1000
- **Modération** : Statut draft → published → archived

**📝 À compléter** : Autres règles métier critiques à documenter

---

### 3.3 Tests obligatoires

**Règle** : ⛔ **Aucun code en production sans tests**

**Types de tests requis** :

1. **Tests fonctionnels** (API) :

   - Cas nominal (201, 200)
   - Cas d'erreur (400, 404, 409)
   - Validation des schémas OpenAPI

2. **Tests unitaires** (Services) :

   - Logique métier
   - Cas limites
   - Gestion d'erreurs

3. **Couverture** : Minimum 80%

**Prompt type pour générer les tests** :

```markdown
Génère les tests PHPUnit pour cet endpoint POST /api/reviews.

Tests à couvrir :

- Cas nominal (201)
- Validation échouée (400) : rating invalide, comment trop court, email invalide
- Duplicata (409) : avis déjà existant
- Agence inexistante (404)

Format : Given-When-Then (commentaires)
Utilise ApiTestCase et RefreshDatabaseTrait
```

---

### 3.4 Analyse statique (SAST)

**Outils obligatoires** :

| Outil            | Niveau             | Commande                      |
| ---------------- | ------------------ | ----------------------------- |
| **PHPStan**      | Niveau 9 (strict)  | `vendor/bin/phpstan analyse`  |
| **Psalm**        | Strict (optionnel) | `vendor/bin/psalm`            |
| **PHP CS Fixer** | PSR-12             | `vendor/bin/php-cs-fixer fix` |

**Workflow** :

1. L'IA génère le code
2. Lancer PHPStan → Si erreurs, demander à l'IA de corriger
3. Lancer les tests → Si RED, ajuster
4. Lancer PHP CS Fixer → Formater automatiquement

**Prompt pour corriger PHPStan** :

```markdown
PHPStan niveau 9 a détecté les erreurs suivantes :

[coller les erreurs]

Corrige ces erreurs en respectant le typage strict PHP 8.2.
```

---

## 📋 4. Prompts types et cas d'usage

### 4.1 Structure de prompt efficace

**Template recommandé** :

```markdown
## Contexte

[Stack technique : Symfony 6.4, API Platform, PHP 8.2, etc.]
[Architecture : Controller → Service → Repository]

## Tâche

[Description claire de ce que l'IA doit faire]

## Contraintes

- [Standards de code : PSR-12, typage strict]
- [Règles métier spécifiques]
- [Architecture à respecter]
- [Librairies/patterns à utiliser]

## Exemples (optionnel)

[Exemples de code existant pour guider le style]

## Questions

As-tu besoin de clarifications sur [X, Y, Z] avant de générer le code ?
```

---

### 4.2 Cas d'usage : Génération de tests

**Prompt** :

```markdown
## Contexte

Symfony 6.4 + API Platform 3.2

Voici la spec OpenAPI de mon endpoint :
[coller spec OpenAPI]

## Tâche

Génère les tests PHPUnit fonctionnels pour cet endpoint.

## Contraintes

- Utilise ApiPlatform\Symfony\Bundle\Test\ApiTestCase
- Format Given-When-Then
- Couvrir : cas nominal, validation échouée, cas limites
- Tester la conformité au schéma OpenAPI

Génère le fichier tests/Functional/Api/XxxApiTest.php
```

---

### 4.3 Cas d'usage : Refactoring

**Prompt** :

```markdown
## Contexte

Voici mon code actuel :
[coller le code]

## Tâche

Refactore ce code en suivant SOLID et PSR-12.

## Contraintes

- Extraire les responsabilités si violation de SRP
- Améliorer la lisibilité (noms de variables, méthodes)
- Ajouter type hints manquants
- NE PAS casser les tests existants
- NE PAS ajouter de fonctionnalités

Relance les tests après refactoring.
```

---

### 4.4 Cas d'usage : Génération d'entité Doctrine

**Prompt** :

```markdown
## Contexte

Symfony 6.4 + Doctrine ORM + API Platform 3.2

## Tâche

Crée une entité Review avec les champs suivants :

- id (UUID, PK)
- agencyId (UUID, FK vers Agency)
- rating (int, 1-5)
- comment (text, min 10 max 1000 caractères)
- authorEmail (string, email valide)
- authorName (string)
- createdAt, updatedAt (auto)

## Contraintes

- Annotations Doctrine
- Symfony Validator (Assert)
- API Platform Resource
- Constraint unique : (agencyId, authorEmail)
- Générer le Repository correspondant
```

---

### 4.5 Bibliothèque de prompts

**📝 À compléter pendant et après la formation** :

| Cas d'usage                      | Prompt type                         | Lien |
| -------------------------------- | ----------------------------------- | ---- |
| Générer un endpoint API Platform | [Template](prompts/api-endpoint.md) | TODO |
| Créer un service métier          | [Template](prompts/service.md)      | TODO |
| Générer des tests                | [Template](prompts/tests.md)        | TODO |
| Refactoring SOLID                | [Template](prompts/refactor.md)     | TODO |
| Analyser une erreur              | [Template](prompts/debug.md)        | TODO |

---

## ✅ 5. Workflow de validation

### 5.1 Avant de commiter du code généré par IA

**Checklist obligatoire** :

- [ ] **Tests écrits d'abord** (TDD)
- [ ] **Tests GREEN** ✅ (`php bin/phpunit`)
- [ ] **PHPStan niveau 9** ✅ (`vendor/bin/phpstan analyse`)
- [ ] **Pas de secrets** dans le code
- [ ] **Review du code** (comprendre ce que l'IA a fait)
- [ ] **Conformité aux guidelines** Symfony/API Platform
- [ ] **Commit message** explicite (mention IA si pertinent)

---

### 5.2 Processus de review

**Règles** :

1. **Auto-review** : Relire le code généré, comprendre chaque ligne
2. **Pair review** : Au moins 1 autre dev review le code
3. **Focus review sur** :
   - Sécurité (injections SQL, XSS, secrets)
   - Logique métier correcte
   - Performance (pas de N+1 queries)
   - Conformité architecture

**Template de PR** :

```markdown
## Description

[Description de la feature/fix]

## Code généré par IA

- [ ] Oui (Claude Code / Copilot / Autre)
- [ ] Non

## Checklist

- [ ] Tests GREEN ✅
- [ ] PHPStan niveau 9 ✅
- [ ] Pas de secrets
- [ ] Code reviewé et compris
- [ ] Conformité guidelines
```

---

### 5.3 CI/CD (Intégration Continue)

**Pipeline GitLab CI obligatoire** :

```yaml
# .gitlab-ci.yml
stages:
  - test
  - quality

phpunit:
  stage: test
  script:
    - composer install
    - php bin/phpunit --coverage-text
  coverage: '/^\s*Lines:\s*\d+.\d+\%/'

phpstan:
  stage: quality
  script:
    - composer install
    - vendor/bin/phpstan analyse --level=9
  allow_failure: false

security:
  stage: quality
  script:
    - composer audit
    - gitleaks detect
  allow_failure: false
```

**Règle** : ❌ **Pas de merge si pipeline RED**

---

## 📊 6. Métriques et amélioration continue

### 6.1 Métriques à tracker

**Par tâche/feature** :

| Métrique             | Comment mesurer    | Objectif         |
| -------------------- | ------------------ | ---------------- |
| **Temps de dev**     | Time tracking      | Vélocité x1.5-2x |
| **Tokens utilisés**  | Logs Claude Code   | Budget par tâche |
| **Coût IA**          | Facturation API    | ROI > 3x         |
| **Couverture tests** | PHPUnit --coverage | > 80%            |
| **Bugs post-deploy** | Monitoring Sentry  | < 1%             |

---

### 6.2 Partage d'apprentissages

**Rituels d'équipe** :

1. **Weekly retro IA** (15min) :

   - Prompts qui ont bien marché
   - Blocages rencontrés
   - Mise à jour de la charte

2. **Bibliothèque de prompts** :

   - Partager les prompts efficaces dans un repo dédié
   - Catégoriser par cas d'usage

3. **Formation continue** :
   - Veille sur les nouveaux outils (Claude, Copilot, etc.)
   - Partage de ressources (articles, vidéos)

---

## 🚀 7. Adoption progressive

### Phase 1 : Expérimentation (Semaine 1-2)

**Objectif** : Se familiariser avec les outils

- ✅ Installer Claude Code sur tous les postes
- ✅ Tester sur petites tâches (génération tests, refactoring simple)
- ✅ Partager les retours d'expérience

**Critères de succès** :

- 100% de l'équipe a testé au moins 1 outil IA
- Au moins 5 prompts types créés

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

---

### Phase 3 : Généralisation (Mois 2+)

**Objectif** : Intégrer dans le workflow quotidien

- ✅ Utiliser IA sur tous les nouveaux projets
- ✅ Optimiser les prompts et workflows
- ✅ Former les nouveaux arrivants

**Critères de succès** :

- 80% des features utilisent IA
- Vélocité mesurée > 1.5x
- NPS équipe > 8/10

---

## 📝 Annexes

### Annexe A : Glossaire

| Terme         | Définition                                            |
| ------------- | ----------------------------------------------------- |
| **LLM**       | Large Language Model (GPT-4, Claude, Gemini)          |
| **MCP**       | Model Context Protocol (connexion outils externes)    |
| **RAG**       | Retrieval Augmented Generation (recherche sémantique) |
| **TDD**       | Test-Driven Development (tests avant code)            |
| **SAST**      | Static Application Security Testing (PHPStan, Psalm)  |
| **Embedding** | Représentation vectorielle d'un texte                 |

---

### Annexe B : Ressources

**Documentation officielle** :

- [Claude Code Documentation](https://docs.anthropic.com/claude/docs)
- [GitHub Copilot Best Practices](https://docs.github.com/en/copilot/getting-started-with-github-copilot)
- [PACT-R Methodology](../README.md)

**Sécurité** :

- [Cursor IDE Security Best Practices](https://www.backslash.security/blog/cursor-ide-security-best-practices)
- [GitLeaks - Scanner de secrets](https://github.com/gitleaks/gitleaks)

---

### Annexe C : Template de retour d'expérience

````markdown
## Retour d'expérience : [Nom de la tâche]

### Contexte

- **Tâche** : [Description]
- **Outil IA utilisé** : Claude Code / Copilot / Autre
- **Durée** : Xh

### Ce qui a bien marché ✅

- [Prompt efficace / Génération rapide / etc.]

### Ce qui a bloqué ❌

- [Prompt flou / IA ne comprend pas / etc.]

### Prompts réutilisables

```markdown
[coller les prompts qui ont fonctionné]
```
````

### Apprentissages

- [Leçons tirées]
- [Ajustements à faire dans la charte]

```

---

## ✍️ Signatures et validation

**Charte élaborée par** : Équipe dev Immodvisor
**Date de création** : 8 octobre 2025
**Prochaine révision** : [À définir - suggéré : 1 mois après adoption]

**Validation** :
- [ ] Lead Developers
- [ ] CTO
- [ ] DSI (pour aspects sécurité/gouvernance)

---

**Cette charte est un document vivant. N'hésitez pas à proposer des améliorations !** 🚀

**📝 À compléter pendant la formation** :
- Section 1 : Finaliser la liste des outils autorisés
- Section 3.2 : Ajouter les règles métier spécifiques Immodvisor
- Section 4.5 : Créer la bibliothèque de prompts types
- Section 6 : Définir les métriques précises à tracker
- Annexe C : Tester le template de retour d'expérience

```
