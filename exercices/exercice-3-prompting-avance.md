# Exercice 3 : Maîtrise du prompting avancé

**Durée** : 1h30  
**Format** : Semi-ouvert avec cas d'usage réels  
**Binômes** : Recommandés pour partage d'expérience

---

## 🎯 Objectifs pédagogiques

À la fin de cet exercice, vous saurez :

- ✅ Structurer des prompts efficaces selon le contexte
- ✅ Appliquer les techniques de prompting avancées  
- ✅ Adapter votre style de prompting selon l'objectif
- ✅ Mesurer et optimiser l'efficacité de vos prompts
- ✅ Créer une bibliothèque de prompts réutilisables

---

## 📖 Contexte

En tant que développeur utilisant l'IA, la qualité de vos prompts détermine directement :
- 🎯 **Précision** du code généré
- ⏱️ **Vitesse** de développement  
- 💰 **Coût** en tokens
- 🔄 **Nombre d'itérations** nécessaires

Cet exercice vous fait pratiquer les techniques de prompting sur des cas réels d'Immodvisor.

---

## 🚀 Déroulé de l'exercice

### Checkpoint 1 : Prompting structuré (30 min)

#### 1.1 Analyser des prompts inefficaces (10 min)

**Tâche** : Identifier les problèmes dans ces prompts réels.

**Exemple de prompt faible** :
```
Crée une fonction PHP pour calculer la moyenne des avis
```

**Problèmes à identifier** :
- Manque de contexte
- Pas de contraintes techniques
- Ambiguïtés multiples
- Pas d'exemples

---

#### 1.2 Refactorer avec la structure PACT-R (20 min)

**Tâche** : Transformer le prompt précédent avec cette structure :

```markdown
## Contexte

[Décrire le projet, stack, architecture]

## Tâche  

[Objectif précis et critères d'acceptation]

## Contraintes

[Standards, architecture, limitations]

## Exemples (optionnel)

[Code existant pour guider le style]

## Questions

[Inviter l'IA à clarifier si nécessaire]
```

**Prompt refactorisé attendu** :

```markdown
## Contexte

Je développe l'API d'avis Immodvisor avec Symfony 6.4 + API Platform.
Architecture : Controller → Service → Repository.
Base de données : PostgreSQL avec entité Review (rating: int 1-5).

## Tâche

Crée une méthode `calculateAverageRating(string $agencyId): float` qui :

- Récupère tous les avis d'une agence
- Calcule la moyenne des notes (rating)
- Retourne 0.0 si aucun avis
- Arrondit à 2 décimales

## Contraintes

- PHP 8.2 strict typing
- Utilise Doctrine pour les requêtes
- Gestion d'erreur si agence inexistante
- Performance : optimiser pour >10k avis
- Tests unitaires requis

## Exemples

Voici une méthode similaire existante :
[coller exemple de ReviewRepository::findByAgency()]

## Questions

As-tu besoin de voir l'entité Review ou d'autres détails ?
```

**Livrable** : Prompt refactorisé pour votre cas d'usage

---

### Checkpoint 2 : Techniques avancées (30 min)

#### 2.1 Chain-of-thought prompting (10 min)

**Tâche** : Utiliser le raisonnement étape par étape.

**Scénario** : Optimiser une requête SQL lente.

**Prompt chain-of-thought** :
```markdown
Analyse cette requête SQL qui est lente (>2s pour 50k avis) :

```sql
SELECT * FROM reviews WHERE agency_id = '123' ORDER BY created_at DESC;
```

Avant de proposer des optimisations, explique ton raisonnement :

1. **Analyse** : Quels sont les goulots d'étranglement probables ?
2. **Hypothèses** : Quels index manquent probablement ?
3. **Stratégie** : Dans quel ordre appliquer les optimisations ?
4. **Validation** : Comment mesurer l'amélioration ?

Ensuite, propose les optimisations concrètes.
```

**Testez** avec Claude Code et comparez avec un prompt direct.

---

#### 2.2 Few-shot learning (10 min)

**Tâche** : Guider l'IA avec des exemples.

**Scénario** : Générer des validations Symfony cohérentes.

**Prompt few-shot** :
```markdown
Voici 2 exemples de validation Symfony dans notre codebase :

**Exemple 1 - AgencyDto :**
```php
#[Assert\NotBlank(message: 'Le nom de l\'agence est obligatoire')]
#[Assert\Length(
    min: 2, 
    max: 100, 
    minMessage: 'Le nom doit contenir au moins {{ limit }} caractères',
    maxMessage: 'Le nom ne peut dépasser {{ limit }} caractères'
)]
private string $name;
```

**Exemple 2 - UserDto :**
```php
#[Assert\NotBlank]
#[Assert\Email(message: 'L\'email {{ value }} n\'est pas valide')]
private string $email;
```

Génère les validations pour ReviewDto en suivant le même style :
- rating : entier entre 1 et 5
- comment : texte entre 10 et 1000 caractères
- authorEmail : email valide
```

---

#### 2.3 Contraintes négatives (10 min)

**Tâche** : Préciser ce qu'on NE veut PAS.

**Scénario** : Refactoring d'un contrôleur trop chargé.

**Prompt avec contraintes négatives** :
```markdown
Refactorise ce contrôleur Symfony :

[coller le code du contrôleur]

## Ce que tu DOIS faire :
- ✅ Extraire la logique métier dans un Service
- ✅ Valider les DTOs d'entrée
- ✅ Respecter Single Responsibility Principle

## Ce que tu NE dois PAS faire :
- ❌ Pas de logique métier dans le Controller
- ❌ Pas de requêtes Doctrine directes dans le Controller  
- ❌ Pas de new Exception() (utiliser les exceptions du Service)
- ❌ Pas de transformation manuelle (utiliser Serializer)
- ❌ Pas de validation inline (utiliser Validator)
```

---

### Checkpoint 3 : Cas d'usage métier (30 min)

#### 3.1 Debugging assisté par IA (15 min)

**Scénario** : Une API retourne 500 sans message clair.

**Prompt de debugging** :
```markdown
J'ai une erreur 500 sur POST /api/reviews mais les logs sont peu clairs.

## Symptômes
- Code d'erreur : 500 Internal Server Error
- Logs Symfony : "An exception occurred"  
- Reproduction : 100% sur les avis avec rating = 0

## Code concerné
[coller ReviewController::create() et ReviewService::createReview()]

## Tests
Les tests passent, mais en conditions réelles ça plante.

## Environnement  
- PHP 8.2, Symfony 6.4, PostgreSQL 14
- En dev ça marche, en staging ça plante

## Tâche
Aide-moi à diagnostiquer étape par étape :

1. **Hypothèses** : Quelles sont les causes probables ?
2. **Debug** : Quels logs/variables inspecter ?  
3. **Fix** : Quelles corrections apporter ?
4. **Prevention** : Comment éviter ce type d'erreur ?
```

---

#### 3.2 Revue de code avec IA (15 min)

**Prompt de code review** :
```markdown
Fais une revue critique de cette Pull Request.

## Contexte
Feature : Ajout de filtres sur l'API des avis
Reviewer habituel : indisponible
Deadline : demain

## Code à reviewer
[coller le code de la PR]

## Critères de review

**Sécurité** :
- Injection SQL, XSS, validation des entrées

**Performance** :  
- Requêtes N+1, index manquants, pagination

**Architecture** :
- Respect SOLID, séparation des responsabilités

**Tests** :
- Couverture, cas limites, tests d'intégration

**Standards** :
- PSR-12, naming, documentation

## Format attendu
Pour chaque fichier :
1. ✅ Points positifs
2. ⚠️ Points d'amélioration  
3. ❌ Blockers (si applicable)
4. 📝 Suggestions concrètes
```

---

## 📊 Grille d'évaluation

| Technique                    | Testé ✅ | Efficace ⚡ | Réutilisable 🔄 |
|------------------------------|----------|-------------|------------------|
| **Structure contexte-tâche** |          |             |                  |
| **Chain-of-thought**         |          |             |                  |
| **Few-shot examples**        |          |             |                  |
| **Contraintes négatives**    |          |             |                  |
| **Debugging assisté**        |          |             |                  |
| **Code review IA**           |          |             |                  |

---

## 🎁 Bonus : Bibliothèque de prompts

### Créer vos templates réutilisables

**Tâche** : Documenter vos meilleurs prompts.

**Template de prompt** :
```markdown
# [NOM_DU_PROMPT]

**Usage** : [Quand utiliser ce prompt]
**Tokens moyens** : [Estimation coût]
**Efficacité** : [Note sur 5]

## Template
```
[Votre prompt avec placeholders {{VARIABLE}}]
```

## Exemple d'utilisation
[Cas concret d'application]

## Variantes
- Version courte : [prompt simplifié]
- Version experte : [prompt détaillé]
```

**Livrables** :
- `prompts/api-generation.md`
- `prompts/debugging.md`  
- `prompts/code-review.md`
- `prompts/testing.md`

---

## 💡 Conseils pour optimiser vos prompts

### ✅ Bonnes pratiques

1. **Commencer spécifique, puis généraliser**
   - Premier prompt très détaillé
   - Versions simplifiées ensuite

2. **Mesurer l'efficacité**
   - Compter les itérations nécessaires
   - Tracker les tokens utilisés
   - Noter la qualité du résultat

3. **Itérer et améliorer**
   - Garder un historique des versions
   - A/B tester différentes formulations
   - Documenter ce qui marche/ne marche pas

### ❌ Pièges à éviter

- Prompts trop longs (>2000 tokens)
- Instructions contradictoires
- Exemples incohérents  
- Manque de validation du résultat

---

## 📚 Ressources

### Documentation
- [Anthropic Prompt Engineering Guide](https://docs.anthropic.com/en/docs/prompt-engineering)
- [OpenAI Prompt Engineering](https://help.openai.com/en/articles/6654000-best-practices-for-prompt-engineering-with-openai-api)

### Outils
- [PromptBase](https://promptbase.com/) - Marketplace de prompts
- [LangSmith](https://smith.langchain.com/) - Testing et monitoring de prompts

---

**Prochain exercice** : [Exercice 4 - Refactoring de code legacy avec IA](exercice-4-refactoring-legacy.md)