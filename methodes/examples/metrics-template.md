# Template de Métriques PACT-R

## Vue d'ensemble

Ce document fournit des templates pour tracker toutes les métriques importantes tout au long du cycle PACT-R.

**Organisation des métriques** :

```
project/
├── metrics/
│   ├── sprint-N/
│   │   ├── feature-moderation-reviews.md
│   │   ├── task-001-api-spec.md
│   │   ├── task-002-tests-acceptance.md
│   │   └── sprint-summary.md
│   ├── sprint-N+1/
│   └── global-metrics.md
```

---

## 1. Template par tâche

**Fichier** : `metrics/sprint-N/task-XXX-[nom-tache].md`

```markdown
# Tâche #XXX : [Nom de la tâche]

**Feature** : [Nom feature parent]
**Sprint** : N
**Date** : YYYY-MM-DD
**Assigné à** : [Nom développeur / IA-assisted]
**Status** : ⏳ En cours / ✅ Terminée / ❌ Bloquée

---

## Contexte

**Objectif** : [Description courte de l'objectif de la tâche]

**Critères d'acceptation** :
- [ ] Critère 1
- [ ] Critère 2
- [ ] Critère 3

**Dépendances** :
- Tâche #XXX (bloquante)
- Tâche #YYY (dépendante)

---

## Estimations initiales

| Métrique | Estimation | Réel | Écart |
|----------|------------|------|-------|
| **Temps total** | 4h | ... | ... |
| - PLAN | 0h | ... | ... |
| - ASSERT | 1h | ... | ... |
| - CODE | 2h | ... | ... |
| - TEST | 1h | ... | ... |
| **Tokens estimés** | 15,000 | ... | ... |
| **Coût estimé** | $0.09 | ... | ... |

---

## Métriques par phase

### Phase ASSERT (Tests RED)

**Début** : YYYY-MM-DD HH:MM
**Fin** : YYYY-MM-DD HH:MM
**Durée** : XXmin

| Métrique | Valeur |
|----------|--------|
| **Tests d'acceptation écrits** | X |
| **Tests unitaires écrits** | X |
| **Tests de contrat écrits** | X |
| **Tokens utilisés** | X |
| **Coût** | $X.XX |
| **Tous tests FAIL (RED)** | ✅ Oui / ❌ Non |

**Problèmes rencontrés** :
- ...

---

### Phase CODE (Implémentation GREEN)

**Début** : YYYY-MM-DD HH:MM
**Fin** : YYYY-MM-DD HH:MM
**Durée** : XXmin

| Métrique | Valeur |
|----------|--------|
| **Lignes de code ajoutées** | X |
| **Lignes de tests ajoutées** | X |
| **Ratio code/tests** | 1:X |
| **Tokens utilisés** | X |
| **Coût** | $X.XX |
| **Tous tests PASS (GREEN)** | ✅ Oui / ❌ Non |

**Fichiers créés/modifiés** :
- `src/Service/ReviewModerationService.php` (+125 lignes)
- `tests/Unit/Service/ReviewModerationServiceTest.php` (+230 lignes)
- ...

**Problèmes rencontrés** :
- ...

---

### Phase TEST (Refactor BLUE)

**Début** : YYYY-MM-DD HH:MM
**Fin** : YYYY-MM-DD HH:MM
**Durée** : XXmin

| Métrique | Valeur | Cible | Status |
|----------|--------|-------|--------|
| **Couverture code** | XX% | > 80% | ✅/❌ |
| **MSI (Mutation Score)** | XX% | > 80% | ✅/❌ |
| **Covered MSI** | XX% | > 90% | ✅/❌ |
| **PHPStan level** | X | 8 | ✅/❌ |
| **Complexité cyclomatique** | X.X | < 5 | ✅/❌ |
| **Tests PBT ajoutés** | X | - | - |
| **Tokens utilisés** | X | - | - |
| **Coût** | $X.XX | - | - |

**Refactorings appliqués** :
- Extraction méthode privée `validateModerator()`
- Introduction Value Object `ReviewStatusTransition`
- ...

**Mutations tuées** : XX/YY (ZZ%)

**Problèmes détectés** :
- ...

---

## Métriques finales

### Temps total

| Phase | Temps estimé | Temps réel | Écart |
|-------|--------------|------------|-------|
| PLAN | 0h | 0h | - |
| ASSERT | 1h | 55min | -5min ✅ |
| CODE | 2h | 2h15 | +15min ⚠️ |
| TEST | 1h | 50min | -10min ✅ |
| **TOTAL** | **4h** | **4h00** | **0min ✅** |

### Coût IA

| Phase | Tokens | Coût estimé | Coût réel | Écart |
|-------|--------|-------------|-----------|-------|
| ASSERT | 5,000 | $0.03 | $0.035 | +$0.005 |
| CODE | 8,000 | $0.05 | $0.048 | -$0.002 ✅ |
| TEST | 2,000 | $0.01 | $0.012 | +$0.002 |
| **TOTAL** | **15,000** | **$0.09** | **$0.095** | **+$0.005 ✅** |

**Note** : Tarification basée sur modèle X à $Y/1M tokens

### Qualité

| Métrique | Valeur | Cible | Status |
|----------|--------|-------|--------|
| Tests écrits | 12 | - | - |
| Couverture | 92% | > 80% | ✅ |
| MSI | 85% | > 80% | ✅ |
| Complexité | 3.2 | < 5 | ✅ |
| PHPStan | Level 8 | 8 | ✅ |

---

## Résultat

- **Status** : ✅ Terminée / ⚠️ Partiellement / ❌ Échec
- **Critères acceptation** : X/Y validés
- **Déployée en preview** : ✅ Oui / ❌ Non
- **URL preview** : https://pr-XX.staging.example.com

**Bugs détectés** :
- Aucun ✅

**Dette technique ajoutée** :
- Aucune ✅

**Dette technique retirée** :
- ...

---

## Learnings

**Ce qui a bien fonctionné** :
- ...

**Ce qui a moins bien fonctionné** :
- ...

**Améliorations pour prochaines tâches** :
- ...
```

---

## 2. Template par feature

**Fichier** : `metrics/sprint-N/feature-[nom-feature].md`

```markdown
# Feature : [Nom de la feature]

**Sprint** : N
**Dates** : YYYY-MM-DD → YYYY-MM-DD
**Équipe** : [Noms]
**Status** : ⏳ En cours / ✅ Déployée / ❌ Annulée

---

## Vue d'ensemble

**Objectif métier** : [Description courte]

**User stories** :
- En tant que [rôle], je veux [action] afin de [bénéfice]
- ...

**Slices planifiées** : X
**Slices terminées** : Y / X

---

## Métriques globales feature

### Développement

| Métrique | Valeur | Budget | Status |
|----------|--------|--------|--------|
| **Temps total dev** | XXh | XXh | ✅/⚠️/❌ |
| - Phase PLAN (1.1 + 1.2) | Xh | Xh | ... |
| - Phase ASSERT | Xh | Xh | ... |
| - Phase CODE | Xh | Xh | ... |
| - Phase TEST | Xh | Xh | ... |
| - Phase REVIEW | Xh | Xh | ... |
| **Tokens totaux** | XXX,XXX | XXX,XXX | ✅/⚠️/❌ |
| **Coût IA total** | $X.XX | $X.XX | ✅/⚠️/❌ |
| **Vélocité** | X slices/semaine | X | ✅/⚠️/❌ |

### Qualité

| Métrique | Valeur | Cible | Status |
|----------|--------|-------|--------|
| **Tests unitaires** | XX | - | - |
| **Tests acceptation** | XX | - | - |
| **Couverture globale** | XX% | > 80% | ✅/❌ |
| **MSI global** | XX% | > 80% | ✅/❌ |
| **Complexité moyenne** | X.X | < 5 | ✅/❌ |
| **PHPStan** | Level X | 8 | ✅/❌ |

### CI/CD

| Métrique | Valeur | Cible | Status |
|----------|--------|-------|--------|
| **Temps build moyen** | Xmin | < 10min | ✅/❌ |
| **Builds réussis** | XX/YY | > 80% | ✅/❌ |
| **Preview deployments** | XX | XX | ✅ |

---

## Découpage et progression

| Slice | Tâches | Status | Temps | Coût | Bugs |
|-------|--------|--------|-------|------|------|
| 1. Soumission review | 5 | ✅ | 12h | $0.45 | 0 |
| 2. Approbation | 7 | ✅ | 8h | $0.38 | 1 |
| 3. Rejet avec raison | 6 | ✅ | 6h | $0.32 | 0 |
| 4. Modération en masse | 8 | ⏳ | ... | ... | ... |
| **TOTAL** | **26** | **3/4** | **26h** | **$1.15** | **1** |

---

## Phase REVIEW

### Démo

**Date** : YYYY-MM-DD
**Participants** : [Liste]
**Durée** : XXmin

**Scénarios démontrés** :
- ✅ Scénario 1
- ✅ Scénario 2
- ...

**Feedback stakeholders** :
- **Positif** : ...
- **Améliorations** : ...

**Décision** : ✅ Validé / ⚠️ Itération / ❌ Rejet

---

### Tests utilisateurs

**Date** : YYYY-MM-DD
**Profils** : 5 utilisateurs (détails...)

**SUS Score** : XX/100 (cible > 70)

| Testeur | Profil | SUS Score |
|---------|--------|-----------|
| 1 | Expert | XX |
| 2 | Nouveau | XX |
| 3 | Power user | XX |
| 4 | Occasionnel | XX |
| 5 | Manager | XX |
| **MOYENNE** | - | **XX** |

**Problèmes détectés** :
- **Critiques** : X
- **Majeurs** : X
- **Mineurs** : X

**Actions correctives** :
1. ...
2. ...

---

### Métriques usage (post-production)

**Période** : J+1 à J+7 après déploiement
**Date déploiement** : YYYY-MM-DD

#### Adoption

| Métrique | Valeur | Cible | Status |
|----------|--------|-------|--------|
| Utilisateurs actifs | XX/YY | > 80% | ✅/❌ |
| Temps adoption | J+X | < J+7 | ✅/❌ |
| Utilisation quotidienne | XX% | > 70% | ✅/❌ |

#### Efficacité

| Métrique | Avant | Après | Gain | Cible |
|----------|-------|-------|------|-------|
| Temps moyen/action | Xmin | Ys | XX% | > 50% |
| Actions/jour | XX | YY | xZ | xW |
| Taux erreur | XX% | YY% | XX% | < 1% |

#### Satisfaction

| Métrique | Valeur | Cible | Status |
|----------|--------|-------|--------|
| NPS | X.X/10 | > 8 | ✅/❌ |
| Feedback positif | XX% | > 80% | ✅/❌ |
| Demandes support | X | < 5 | ✅/❌ |

#### Qualité production

| Métrique | Valeur | Cible | Status |
|----------|--------|-------|--------|
| Bugs critiques | X | 0 | ✅/❌ |
| Bugs mineurs | X | < 3 | ✅/❌ |
| Hotfix | X | 0 | ✅/❌ |
| Taux erreur prod | X.XX% | < 1% | ✅/❌ |
| Downtime | Xmin | 0 | ✅/❌ |

---

## ROI (Return on Investment)

### Coûts

| Poste | Montant |
|-------|---------|
| Temps dev (XXh x XX€/h) | X,XXX€ |
| Coût IA | $X.XX (~X€) |
| Infrastructure/Outils | XX€ |
| **TOTAL** | **X,XXX€** |

### Bénéfices

| Métrique | Valeur |
|----------|--------|
| Économies/jour | XX€ |
| Économies/mois (20j) | X,XXX€ |
| Break-even | X.X jours |
| **ROI mensuel** | **XX%** |
| **ROI annuel** | **XX%** |

---

## Décision finale

- [ ] ✅ Feature déployée en production
- [ ] ⚠️ Itération requise
- [ ] ❌ Feature abandonnée

**Justification** : ...

**Prochaines étapes** :
1. ...
2. ...

---

## Learnings

**Succès** :
- ...

**Challenges** :
- ...

**Améliorations process** :
- ...
```

---

## 3. Template sprint summary

**Fichier** : `metrics/sprint-N/sprint-summary.md`

```markdown
# Sprint N - Summary

**Dates** : YYYY-MM-DD → YYYY-MM-DD
**Équipe** : [Noms]
**Sprint Goal** : [Objectif principal]

---

## Features développées

| Feature | Slices | Status | Temps | Coût | Déployée |
|---------|--------|--------|-------|------|----------|
| Modération reviews | 4/4 | ✅ | 28h | $1.47 | ✅ |
| Notifications email | 2/3 | ⏳ | 12h | $0.65 | ❌ |
| **TOTAL** | **6/7** | - | **40h** | **$2.12** | **1/2** |

---

## Métriques sprint

### Vélocité

| Métrique | Valeur | Sprint précédent | Évolution |
|----------|--------|------------------|-----------|
| **Slices terminées** | 6 | 5 | +20% ✅ |
| **Story points** | 21 | 18 | +17% ✅ |
| **Temps dev total** | 40h | 42h | -5% ✅ |
| **Tokens utilisés** | 195K | 220K | -11% ✅ |
| **Coût IA** | $2.12 | $2.35 | -10% ✅ |

### Qualité

| Métrique | Valeur | Cible | Tendance |
|----------|--------|-------|----------|
| **Couverture moyenne** | 86% | > 80% | ↗️ +3% |
| **MSI moyen** | 83% | > 80% | ↗️ +2% |
| **Bugs sprint** | 2 | < 5 | ✅ |
| **Bugs prod** | 0 | 0 | ✅ |
| **Dette technique** | -5 items | < 0 | ✅ |

### CI/CD

| Métrique | Valeur | Cible | Tendance |
|----------|--------|-------|----------|
| **Temps build moyen** | 4m30s | < 10min | ↘️ -30s |
| **Builds réussis** | 92% | > 80% | ↗️ +5% |
| **Déploiements** | 12 | - | = |

---

## Phase REVIEW sprint

### Démos

- ✅ Feature Modération reviews : Validée (SUS 79)
- ⏳ Feature Notifications : En cours

### Tests utilisateurs

| Feature | Testeurs | SUS Score | Problèmes |
|---------|----------|-----------|-----------|
| Modération reviews | 5 | 79 | 1 majeur, 2 mineurs |

### Métriques usage

**Features en production** : 1

| Feature | Adoption | NPS | ROI |
|---------|----------|-----|-----|
| Modération reviews | 90% | 9.2 | 328%/mois |

---

## Rétrospective

### ✅ Ce qui a bien fonctionné

1. **TDD strict** : 0 bug en production grâce aux tests exhaustifs
2. **Property-Based Testing** : Détection de 3 edge cases non anticipés
3. **Démos hebdo** : Feedback rapide, ajustements mineurs uniquement
4. **Preview environments** : Tests utilisateurs sur vraies données

### ⚠️ Ce qui a moins bien fonctionné

1. **Estimations** : Feature Notifications sous-estimée de 30%
2. **Mutation testing** : Ralentit CI sur gros changesets (> 500 lignes)
3. **Communication** : 2 blocages par manque de sync Product Owner

### 🔄 Actions d'amélioration Sprint N+1

1. **Estimations** : Ajouter buffer 20% sur nouvelles features
2. **CI** : Paralléliser mutation testing par module
3. **Communication** : Daily standup async sur Slack

---

## Métriques cumulatives projet

### Développement (depuis début projet)

| Métrique | Sprint N | Cumul | Moyenne/sprint |
|----------|----------|-------|----------------|
| Temps dev | 40h | 180h | 36h |
| Coût IA | $2.12 | $9.50 | $1.90 |
| Features déployées | 1 | 5 | 1 |

### Qualité (depuis début projet)

| Métrique | Valeur | Évolution |
|----------|--------|-----------|
| Couverture moyenne | 86% | ↗️ +8% vs Sprint 1 |
| MSI moyen | 83% | ↗️ +13% vs Sprint 1 |
| Bugs production total | 3 | ↘️ -2 vs Sprint 1 |
| Dette technique | 12 items | ↘️ -18 vs Sprint 1 |

---

## Budget et ROI projet

### Coûts (cumul projet)

| Poste | Montant |
|-------|---------|
| Temps dev (180h x 60€/h) | 10,800€ |
| Coût IA | $9.50 (~9€) |
| Infrastructure | 150€ |
| **TOTAL** | **10,959€** |

### Bénéfices (5 features en prod)

| Feature | ROI mensuel |
|---------|-------------|
| Modération reviews | 328% |
| Dashboard analytics | 215% |
| Bulk export | 180% |
| Auto-tagging | 95% |
| Search filters | 125% |
| **MOYENNE** | **189%** |

**ROI global projet** : ~190%/mois

---

## Planification Sprint N+1

**Objectif** : Finaliser feature Notifications + Démarrer Contestations

**Slices planifiées** : 8
**Temps estimé** : 42h
**Budget IA** : $2.50

**Priorités** :
1. P0 : Terminer Notifications (slice 3/3)
2. P1 : Contestations (slices 1-2)
3. P2 : Améliorations UX (backlog)
```

---

## 4. Template métriques globales projet

**Fichier** : `metrics/global-metrics.md`

```markdown
# Métriques Globales Projet

**Projet** : [Nom]
**Début** : YYYY-MM-DD
**Sprints réalisés** : N
**Status** : ⏳ En cours / ✅ Terminé

---

## Statistiques générales

### Développement

| Métrique | Valeur |
|----------|--------|
| **Temps total dev** | XXXh |
| **Features déployées** | XX |
| **Slices terminées** | XXX |
| **Tâches complétées** | XXX |
| **Lignes de code** | XX,XXX |
| **Lignes de tests** | XX,XXX |
| **Ratio code/tests** | 1:X.X |

### Coûts IA

| Métrique | Valeur |
|----------|--------|
| **Tokens totaux** | X,XXX,XXX |
| **Coût total** | $XX.XX |
| **Coût moyen/sprint** | $X.XX |
| **Coût moyen/feature** | $X.XX |
| **Coût moyen/tâche** | $X.XX |

### Qualité

| Métrique | Valeur actuelle | Meilleur | Pire |
|----------|-----------------|----------|------|
| **Couverture** | XX% | XX% | XX% |
| **MSI** | XX% | XX% | XX% |
| **Complexité moyenne** | X.X | X.X | X.X |
| **Bugs production total** | XX | - | - |
| **Dette technique** | XX items | XX | XX |

---

## Évolution par sprint

### Vélocité

| Sprint | Slices | Temps (h) | Tokens | Coût | Features déployées |
|--------|--------|-----------|--------|------|--------------------|
| 1 | 3 | 38 | 180K | $1.85 | 0 |
| 2 | 4 | 36 | 200K | $2.10 | 1 |
| 3 | 5 | 42 | 220K | $2.35 | 1 |
| 4 | 5 | 40 | 195K | $2.12 | 1 |
| 5 | 6 | ... | ... | ... | ... |

**Tendances** :
- Vélocité : ↗️ +100% (3 → 6 slices/sprint)
- Temps : → Stable (~40h/sprint)
- Coût : ↘️ -10% (optimisation prompts)

### Qualité

| Sprint | Couverture | MSI | Bugs prod | Dette tech |
|--------|------------|-----|-----------|------------|
| 1 | 78% | 70% | 2 | 30 items |
| 2 | 82% | 75% | 1 | 25 items |
| 3 | 84% | 80% | 0 | 18 items |
| 4 | 86% | 83% | 0 | 12 items |
| 5 | ... | ... | ... | ... |

**Tendances** :
- Qualité : ↗️ Amélioration continue
- Bugs : ↘️ Réduction 100% depuis Sprint 3
- Dette : ↘️ -60% depuis début

---

## ROI global

### Investissement total

| Poste | Montant |
|-------|---------|
| Temps dev (XXXh x XX€/h) | XX,XXX€ |
| Coût IA | $XX.XX (~XX€) |
| Infrastructure | XX€ |
| Formation/Setup | XX€ |
| **TOTAL** | **XX,XXX€** |

### Retours (features en production)

| Feature | Économies/mois | ROI mensuel |
|---------|----------------|-------------|
| Feature 1 | X,XXX€ | XX% |
| Feature 2 | X,XXX€ | XX% |
| ... | ... | ... |
| **TOTAL** | **XX,XXX€** | **XXX%** |

**Break-even projet** : X.X mois
**ROI annuel estimé** : XXX%

---

## Comparaison avant/après PACT-R

### Sans PACT-R (estimations)

| Métrique | Valeur estimée |
|----------|----------------|
| Temps dev features | XXXh (+XX%) |
| Bugs production | XX (+XX%) |
| Couverture tests | XX% (-XX%) |
| Dette technique | XX items (+XX%) |
| Time-to-market | XX semaines (+XX%) |

### Avec PACT-R (réel)

| Métrique | Valeur | Gain |
|----------|--------|------|
| Temps dev | XXXh | ✅ -XX% |
| Bugs prod | XX | ✅ -XX% |
| Couverture | XX% | ✅ +XX% |
| Dette tech | XX items | ✅ -XX% |
| Time-to-market | XX semaines | ✅ -XX% |

---

## Top insights

### 🏆 Succès majeurs

1. **0 bugs critiques** en production depuis Sprint 3
2. **ROI moyen 189%** sur features déployées
3. **Vélocité doublée** en 4 sprints
4. **Dette technique réduite de 60%**

### 📈 Métriques clés

- **Couverture tests** : 86% (cible > 80%)
- **MSI** : 83% (cible > 80%)
- **Satisfaction users** : NPS 8.8/10 (cible > 8)
- **Adoption features** : 85% moyenne (cible > 80%)

### 🎯 Optimisations identifiées

1. **Prompts IA** : Itérations réduisent coût de 10%
2. **Mutation testing** : Parallélisation réduit temps CI de 30%
3. **Preview envs** : Tests users sur vraies données = -40% bugs

---

## Prochaines étapes

1. ...
2. ...
3. ...
```

---

## 5. Outils de tracking recommandés

### Tracking automatique

```markdown
## Outils pour automatiser le tracking métriques

### Tokens et Coûts IA
- **Langfuse** : https://langfuse.com (open-source LLM observability)
- **Helicone** : https://helicone.ai (tracking OpenAI/Anthropic)
- **Custom logging** : Wrapper API pour logger tokens

### Temps de développement
- **Toggl Track** : https://toggl.com
- **Clockify** : https://clockify.me (gratuit)
- **WakaTime** : https://wakatime.com (temps IDE)

### Qualité code
- **PHPUnit** : Couverture intégrée
- **Infection** : MSI dans output JSON
- **PHPStan** : Baseline + CI integration
- **SonarQube** : Dashboard qualité global

### CI/CD
- **GitHub Actions metrics** : Temps build dans logs
- **Grafana** : Visualisation métriques CI/CD

### Usage (post-prod)
- **Plausible Analytics** : Privacy-friendly
- **Matomo** : Open-source alternative Google Analytics
- **PostHog** : Product analytics + feature flags
```

---

## Checklist tracking métriques

### Par tâche
- [ ] Estimations initiales documentées
- [ ] Temps par phase tracké (ASSERT, CODE, TEST)
- [ ] Tokens/coût enregistrés
- [ ] Qualité mesurée (couverture, MSI)
- [ ] Learnings capturés

### Par feature
- [ ] Métriques globales calculées
- [ ] Tests utilisateurs réalisés (SUS Score)
- [ ] Métriques usage collectées (post-prod)
- [ ] ROI calculé
- [ ] Décision documentée

### Par sprint
- [ ] Vélocité mesurée
- [ ] Comparaison sprint précédent
- [ ] Rétrospective réalisée
- [ ] Actions d'amélioration définies

### Projet global
- [ ] Métriques cumulatives à jour
- [ ] Tendances analysées
- [ ] ROI global calculé
- [ ] Insights partagés avec équipe
