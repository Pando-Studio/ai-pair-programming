# Méthodologies de vibe coding

**Format** : Présentation + démo live

---

## 🎯 Objectifs

- Comprendre l'origine de PACT-R depuis Plan-Act-Review-Repeat
- Maîtriser la méthodologie PACT-R
- Savoir quand et comment l'appliquer
- Découvrir les workflows selon vos inputs
- Maîtriser les garde-fous anti-over-engineering

---

## 🔄 PACT-R : Plan, Assert, Code, Test, Review

### Vue d'ensemble

**PACT-R** est une méthodologie de développement logiciel conçue pour maximiser qualité et vélocité avec l'IA.

```
PLAN → ASSERT → CODE → TEST → REVIEW
  ↑                                ↓
  └────────────────────────────────┘
         (Itérations rapides)
```

### Origine : Plan-Act-Review-Repeat

**PACT-R** s'inspire et étend la méthodologie **Plan-Act-Review-Repeat** popularisée par **Andrej Karpathy** (cofondateur d'OpenAI) en février 2025. Cette approche cyclique originale comprenait 4 phases :

1. **Plan** : Définir l'intention en langage naturel
2. **Act** : L'IA génère le code
3. **Review** : Tester et valider ce qui a été produit
4. **Repeat** : Itérer sans nécessairement retoucher le code manuellement

([Level96](https://www.level96.co/blog/vibe-coding-definition), [Ada Tech School](https://blog.adatechschool.fr/vibe-coding-guide-complet-2025/))

**PACT-R enrichit cette approche** en y ajoutant :

- Meilleure plannification : Création de specifications exhaustives
- La phase **ASSERT** (tests d'abord, TDD strict) pour garantir la fiabilité

> 📖 **Historique complet** : Voir [`ressources/historique.md`](../ressources/historique.md) qui détaille Plan-Act-Review-Repeat, son origine et les personnalités associées au vibe coding

### Philosophie clé

> **Investir en amont (PLAN) pour accélérer ensuite**

- **Specs exhaustives d'abord** → Moins d'ambiguïté pour l'IA
- **Tests avant code (TDD strict)** → Fiabilité garantie
- **API-First** → Le contrat est la source de vérité
- **Itérations courtes** → Feedback rapide
- **Métriques continues** → Piloter les améliorations

---

## 1️⃣ Phase PLAN : Spécifications exhaustives + découpage

### Pourquoi investir en amont ?

**Sans specs claires** :

- ❌ L'IA génère du code qui ne répond pas au besoin
- ❌ Multiples itérations inutiles (perte de temps)
- ❌ Bugs difficiles à détecter
- ❌ Architecture incohérente

**Avec specs exhaustives** :

- ✅ L'IA comprend mieux ce qu'il faut faire
- ✅ Code cohérent dès la première génération
- ✅ Tests faciles à écrire
- ✅ Architecture solide

### 1.1 Spécifications techniques complètes

**Livrables obligatoires** :

1. **User Flows** : Parcours utilisateurs (nominal, erreurs, limites)
2. **Diagrammes de séquence** : Interactions entre composants
3. **Modèle de données** : ERD complet (types, contraintes, relations)
4. **Spécifications API** : Contrats OpenAPI exhaustifs

**Exemple concret (API d'avis)** :

```yaml
# openapi.yaml
/api/reviews:
  post:
    summary: Créer un avis
    requestBody:
      required: true
      content:
        application/json:
          schema:
            type: object
            required: [agencyId, rating, comment, authorEmail]
            properties:
              agencyId:
                type: string
                format: uuid
              rating:
                type: integer
                minimum: 1
                maximum: 5
              comment:
                type: string
                minLength: 10
                maxLength: 1000
              authorEmail:
                type: string
                format: email
    responses:
      201:
        description: Avis créé
        content:
          application/json:
            schema:
              $ref: "#/components/schemas/Review"
      400:
        description: Validation échouée
      409:
        description: Avis déjà existant pour cet utilisateur
```

**💡 Astuce** : Plus la spec est détaillée, meilleur sera le code généré par l'IA

---

### 1.2 Découpage et priorisation modulaire

**Principes** :

- ✅ Tâches de **2-4h maximum**
- ✅ **Indépendantes** et testables
- ✅ **Vertical slices** (end-to-end) plutôt que layers
- ✅ **TDD-Ready** : Critères d'acceptation testables

**Méthodes de priorisation** :

| Méthode                | Quand l'utiliser                           |
| ---------------------- | ------------------------------------------ |
| **MoSCoW**             | Feature complète à découper                |
| **Value vs Effort**    | Backlog de plusieurs features              |
| **Tracer Bullets**     | Besoin de démo rapide end-to-end           |
| **User Story Mapping** | Produit avec parcours utilisateur complexe |

**Exemple de découpage (API d'avis)** :

```markdown
## Epic : API de gestion d'avis

### Must Have (MVP)

- [ ] POST /api/reviews - Créer un avis (2h)
- [ ] GET /api/reviews/{id} - Lire un avis (1h)
- [ ] GET /api/reviews?agencyId=X - Lister les avis d'une agence (2h)

### Should Have

- [ ] PUT /api/reviews/{id} - Modifier son avis (2h)
- [ ] DELETE /api/reviews/{id} - Supprimer son avis (1h)
- [ ] GET /api/reviews/stats - Statistiques d'avis (3h)

### Could Have

- [ ] Modération des avis
- [ ] Réponse de l'agence
- [ ] Système de signalement
```

---

### 🗺️ Workflows PLAN selon vos inputs

**PACT-R s'adapte à votre situation de départ** :

| Vous avez              | Workflow recommandé         | Durée  | Exemple                                      |
| ---------------------- | --------------------------- | ------ | -------------------------------------------- |
| **Tickets JIRA**       | MCP → Analyse → Specs       | 1-2j   | Récupérer tickets Linear, analyser, enrichir |
| **Maquettes Figma**    | MCP Figma → Specs           | 1-2j   | Extraire composants, user flows, DTOs        |
| **Cahier des charges** | Analyse CDC → Specs         | 2-3j   | Extraire exigences, créer ERD/OpenAPI        |
| **API existante**      | Analyse OpenAPI → Extension | 0.5-1j | Respecter conventions, étendre cohérent      |
| **Code legacy**        | Reverse engineering → Specs | 3-4j   | Documenter existant, spécifier changements   |
| **Rien (greenfield)**  | Discovery → Specs           | 3-5j   | User research, maquettes, specs              |

**📖 Détails complets** : Voir [`input-plan-workflow.md`](../methodes/input-plan-workflow.md)

---

## 2️⃣ Phase ASSERT : Tests d'abord (RED)

### Règle d'or TDD

> ⛔ **Aucune ligne de code de production sans test RED d'abord**

### Types de tests à écrire

**1. Tests d'acceptation (ATDD/BDD)** :

```php
// tests/Feature/CreateReviewTest.php
/** @test */
public function it_creates_a_review_for_an_agency(): void
{
    // Given
    $agency = Agency::factory()->create();

    // When
    $response = $this->postJson('/api/reviews', [
        'agencyId' => $agency->id,
        'rating' => 5,
        'comment' => 'Excellent service, très professionnel',
        'authorEmail' => 'client@example.com',
    ]);

    // Then
    $response->assertStatus(201);
    $this->assertDatabaseHas('reviews', [
        'agency_id' => $agency->id,
        'rating' => 5,
    ]);
}
```

**2. Tests unitaires (cas nominal + erreurs + limites)** :

```php
/** @test */
public function it_rejects_review_with_invalid_rating(): void
{
    $response = $this->postJson('/api/reviews', [
        'agencyId' => $this->agency->id,
        'rating' => 6, // Invalid: max is 5
        'comment' => 'Test',
        'authorEmail' => 'test@example.com',
    ]);

    $response->assertStatus(400);
    $response->assertJsonValidationErrors(['rating']);
}
```

**3. Tests de contrat (conformité OpenAPI)** :

```php
/** @test */
public function review_response_matches_openapi_schema(): void
{
    $review = Review::factory()->create();

    $response = $this->getJson("/api/reviews/{$review->id}");

    $response->assertStatus(200);
    $response->assertJsonStructure([
        'id',
        'agencyId',
        'rating',
        'comment',
        'authorEmail',
        'createdAt',
        'updatedAt',
    ]);
}
```

### Workflow avec IA

**Prompt efficace pour générer les tests** :

```markdown
## Contexte

Je développe une API de gestion d'avis avec Symfony + API Platform.

## Spec OpenAPI

[coller la spec de l'endpoint POST /api/reviews]

## Tâche

Génère les tests PHPUnit pour cet endpoint, en suivant ces règles :

- Format ATDD (Given-When-Then)
- Cas nominal
- Cas d'erreur (validation, duplicata, etc.)
- Cas limites (champs min/max)
- Conformité au schéma OpenAPI

## Contraintes

- Utiliser les factories Laravel/Symfony
- Nommer les tests explicitement : it_creates_a_review_for_an_agency
- Couvrir TOUS les codes HTTP (201, 400, 409)
```

---

## 3️⃣ Phase CODE : Implémentation minimale (GREEN)

### Objectif

> Écrire le code **le plus simple** qui fait passer les tests

### Approche API-First + TDD

**Workflow** :

1. Les tests sont RED ❌
2. Demander à l'IA de générer l'implémentation minimale
3. Lancer les tests → GREEN ✅
4. Ne PAS ajouter de fonctionnalités non testées

### Vibe Coding avec IA : Bonnes pratiques

**⚠️ Avant de commencer** :

1. **Fournir le contexte complet** :

   - ✅ Spécifications de la tâche
   - ✅ Fichier `GUIDELINES.md` (si existant)
   - ✅ Tests RED déjà écrits
   - ✅ Contraintes techniques (versions PHP, Symfony, etc.)

2. **Encourager l'IA à poser des questions** :

   > "Avant de générer le code, as-tu besoin de clarifications sur les specs, les règles métier, ou l'architecture ?"

3. **Itérer avec l'IA** :
   - Commencer par le code minimal (GREEN)
   - Valider l'approche
   - Raffiner si nécessaire

**Exemple de prompt efficace** :

```markdown
## Contexte

Tâche : Implémenter l'endpoint POST /api/reviews

**Specs OpenAPI** :
[coller la spec complète]

**Tests RED** :
[coller les tests qui échouent]

**Guidelines** :

- PHP 8.2 + Symfony 6.4 + API Platform 3.2
- Architecture : Controller → Service → Repository
- Validation via Symfony Validator
- Pas de logique métier dans le Controller

## Questions

Avant de générer le code, as-tu besoin de clarifications sur :

- Les règles métier (ex: peut-on modifier un avis ?)
- Les contraintes de validation ?
- L'architecture à respecter ?

Pose-moi toutes les questions nécessaires avant de générer le code.
```

### Contraintes CODE

- ✅ Pas de sur-engineering (YAGNI)
- ✅ Pas de fonctionnalités non testées
- ✅ Typage strict (PHPStan niveau 9)
- ✅ Respect des standards PSR-12
- ✅ Injection de dépendances systématique

---

## 4️⃣ Phase TEST : Refactoring et amélioration (BLUE)

### Objectif

> Améliorer le code sans casser les tests

### Activités

**1. Refactoring** :

- Amélioration lisibilité
- Extraction de méthodes
- Respect SOLID

**2. Property-Based Testing (PBT)** :

- Tester des invariants plutôt que des cas spécifiques
- Exemple : "Un avis créé doit toujours avoir un rating entre 1 et 5"

**3. Mutation Testing** :

- Vérifier la robustesse des tests
- Objectif : MSI (Mutation Score Index) > 80%

**4. Analyse statique** :

- PHPStan niveau 9
- Psalm niveau strict
- Couverture de code > 80%

### Workflow avec IA

**Prompt pour refactoring** :

```markdown
## Contexte

Voici le code qui fait passer les tests :

[coller le code GREEN]

## Tâche

Refactore ce code en suivant ces règles :

- Extraire les responsabilités selon SOLID
- Améliorer la lisibilité
- Ajouter des type hints stricts
- Supprimer les duplications

## Contraintes

- NE PAS casser les tests existants
- NE PAS ajouter de fonctionnalités
- Respecter les guidelines Symfony
```

---

## 5️⃣ Phase REVIEW : Validation et métriques

### Objectif

> Valider la valeur métier et collecter des données pour piloter les itérations

### Activités

**1. Démo courte (15-30min)** :

- Feature end-to-end fonctionnelle
- Cas nominal + cas d'erreur
- Environnement de preview

**2. Tests utilisateurs légers (5 users)** :

- Protocole Nielsen Norman Group
- Questionnaire SUS (System Usability Scale)

**3. Métriques Build-Measure-Learn** :

#### Métriques techniques

| Métrique             | Cible            | Outil                        |
| -------------------- | ---------------- | ---------------------------- |
| **Tokens utilisés**  | Budget par tâche | Logs IA                      |
| **Coût total**       | ROI > 3x         | Facturation API              |
| **Temps de dev**     | Vélocité x1.5-2x | Time tracking                |
| **Couverture tests** | > 80%            | PHPUnit --coverage           |
| **MSI**              | > 80%            | Infection (mutation testing) |
| **Temps CI/CD**      | < 10 min         | GitLab CI                    |

#### Métriques usage

| Métrique          | Cible              | Outil               |
| ----------------- | ------------------ | ------------------- |
| **Adoption**      | > 80% en 1 semaine | Analytics           |
| **NPS**           | > 8/10             | Survey              |
| **Taux d'erreur** | < 1%               | Monitoring (Sentry) |

### Décision

```
Métriques OK ?
├─ Techniques KO → Refactor/Optimisation → Nouvelle itération
├─ Usage KO → Ajuster specs/UX → Retour PLAN 1.1
└─ Tout OK → ✅ Merge Production
```

---

## 🛡️ Garde-fous anti-over-engineering

### Principe YAGNI (You Aren't Gonna Need It)

> N'implémente que ce qui est dans les specs et testé

| ❌ Over-engineering          | ✅ YAGNI                                    |
| ---------------------------- | ------------------------------------------- |
| Système de cache "au cas où" | Implémenter quand métriques montrent besoin |
| Message queue pour 100 req/j | Solution simple, migrer si scaling justifié |
| Microservices dès le début   | Monolithe modulaire, extraire si nécessaire |
| Design patterns complexes    | Commencer simple, refactorer si besoin      |

### Monolith-First / Modular Monolith

**Principe** : Démarrer avec un monolithe bien structuré

**Quand extraire en services ?**

- ✅ Scaling indépendant nécessaire
- ✅ Équipes multiples sur domaines séparés
- ✅ Besoin de déploiements indépendants

**Sinon** : Garder le monolithe modulaire (bounded contexts clairs)

---

## 📊 Démonstration live (5 min)

### Scénario : Créer un endpoint simple avec Claude Code

**Étapes** :

1. **PLAN** : Ouvrir `openapi.yaml`, montrer la spec
2. **ASSERT** : Demander à Claude de générer les tests
3. **CODE** : Demander l'implémentation minimale
4. **TEST** : Lancer PHPUnit → GREEN ✅
5. **REVIEW** : Montrer la couverture de code

**Prompt utilisé** :

```markdown
Crée un endpoint GET /api/reviews/{id} en Symfony + API Platform.

Specs :

- Retourne un avis par son ID
- 200 si trouvé
- 404 si non trouvé
- Conformité OpenAPI (voir openapi.yaml)

Génère d'abord les tests PHPUnit, puis l'implémentation minimale.
```

---

## 💡 Points clés à retenir

### PACT-R en 5 principes

1. **Specs exhaustives** : Investir en amont pour accélérer ensuite
2. **Test-First, Always** : RED → GREEN → BLUE obligatoire
3. **API-First** : Le contrat est la source de vérité
4. **Itérer rapidement** : Tâches courtes (2-4h), feedback constant
5. **YAGNI by default** : Pas d'implémentation sans preuve

### Quand appliquer PACT-R ?

| Contexte                          | Appliquer PACT-R ?      | Raison                                |
| --------------------------------- | ----------------------- | ------------------------------------- |
| **Nouvelle feature bien définie** | ✅ Oui, complet         | Maximise qualité et vélocité          |
| **Feature exploratoire**          | ⚠️ Oui, mais PLAN léger | Discovery Track en parallèle          |
| **Bug fix simple**                | ❌ Non                  | Overkill, juste écrire le test        |
| **Spike technique**               | ❌ Non                  | Timeboxer, apprendre, jeter           |
| **Refactoring**                   | ⚠️ Partiel              | Tests d'abord, pas de nouvelles specs |

### Erreurs à éviter

❌ **Sauter la phase PLAN** → Code incohérent, multiples itérations  
❌ **Écrire le code avant les tests** → Perte du bénéfice TDD  
❌ **Sur-engineer dès le début** → Complexité inutile  
❌ **Ignorer les métriques** → Pas de feedback pour améliorer  
❌ **Appliquer PACT-R rigidement** → Processus paralysant

---

## 🎓 Checklist rapide PACT-R

### Avant de démarrer une feature

- [ ] Specs complètes (User Flows, ERD, OpenAPI)
- [ ] Découpage en tâches < 4h
- [ ] Critères d'acceptation testables définis
- [ ] Estimation tokens/coût par tâche

### Pendant le développement

- [ ] Tests RED écrits avant code
- [ ] Code minimal pour GREEN
- [ ] Refactor pour BLUE
- [ ] Métriques trackées par tâche

### Avant de merger

- [ ] Couverture > 80%
- [ ] MSI > 80% (si mutation testing activé)
- [ ] PHPStan niveau 9 passé
- [ ] Démo réalisée
- [ ] Métriques usage positives (si applicable)

---

## 📚 Ressources

### Documentation interne

- **Historique du vibe coding** : [`ressources/historique.md`](ressources/historique.md) - Plan-Act-Review-Repeat et origines de PACT-R
- **Chiffres et sources vérifiées** : [`ressources/data.md`](ressources/data.md) - Sources avec URLs sur l'adoption et la productivité
- **Constat et contexte** : [`ressources/constat.md`](ressources/constat.md) - Analyse du marché

### Méthodologies et exemples

- **Méthodologie complète** : [pact-r.md](../methodes/pact-r.md)
- **Workflows PLAN détaillés** : [input-plan-workflow.md](../methodes/input-plan-workflow.md)
- **Exemples** : [`plan-phase.md`](../methodes/examples/plan-phase.md), [`coding-phase.md`](../methodes/examples/coding-phase.md), etc.

### Liens externes clés

- [Level96 - Vibe Coding Definition](https://www.level96.co/blog/vibe-coding-definition)
- [Ada Tech School - Guide complet 2025](https://blog.adatechschool.fr/vibe-coding-guide-complet-2025/)
- [Cloudflare - AI Vibe Coding](https://www.cloudflare.com/fr-fr/learning/ai/ai-vibe-coding/)

---

**Prochain module** : [Concepts fondamentaux (LLM, MCP, RAG)](04-concepts-fondamentaux.md)
