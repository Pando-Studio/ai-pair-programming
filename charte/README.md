# Charte d'utilisation de l'IA - Immodvisor

Ce dossier contient la charte d'utilisation de l'IA générative pour le développement chez Immodvisor.

---

## 📋 Document principal

**[guidelines-vibe-coding.md](guidelines-vibe-coding.md)**

Cette charte définit :

1. **Outils autorisés** : Claude Code, Copilot, etc.
2. **Sécurité et gouvernance** : Secrets, RGPD, données sensibles
3. **Standards de code** : Symfony, PSR-12, architecture
4. **Prompts types** : Templates réutilisables
5. **Workflow de validation** : Tests, PHPStan, review
6. **Métriques** : Suivi de productivité et qualité
7. **Adoption progressive** : Roadmap sur 2 mois

---

## 🎯 Objectif

**Garantir** :

- ✅ Qualité et fiabilité du code généré
- ✅ Sécurité et confidentialité des données
- ✅ Harmonisation des pratiques
- ✅ Productivité maximale avec risques minimisés

---

## 🔄 Statut

**Version actuelle** : 1.0 (Draft)

**📝 À compléter pendant la formation** :

- Section 1 : Finaliser la liste des outils autorisés
- Section 3.2 : Ajouter les règles métier spécifiques Immodvisor
- Section 4.5 : Créer la bibliothèque de prompts types
- Section 6 : Définir les métriques précises à tracker

**Prochaines étapes** :

1. ✅ Élaboration collaborative pendant la formation (8 oct 2025)
2. ⏳ Test sur 2 semaines (9-22 oct 2025)
3. ⏳ Ajustements selon retours terrain (23 oct 2025)
4. ⏳ Validation finale par Lead Devs + CTO + DSI
5. ⏳ Déploiement officiel

---

## 🛠️ Structure de la charte

```
1. Outils autorisés
   ├─ Approuvés (Claude Code, etc.)
   └─ Interdits (auto-run, outils non sécurisés)

2. Sécurité et gouvernance
   ├─ Données interdites (secrets, données clients)
   ├─ Checklist avant prompts
   ├─ Gestion des secrets
   └─ RGPD et confidentialité

3. Standards de code
   ├─ Guidelines Symfony / API Platform
   ├─ Règles métier Immodvisor
   ├─ Tests obligatoires (TDD)
   └─ Analyse statique (PHPStan niveau 9)

4. Prompts types
   ├─ Structure efficace
   ├─ Cas d'usage courants
   └─ Bibliothèque de prompts

5. Workflow de validation
   ├─ Checklist avant commit
   ├─ Processus de review
   └─ CI/CD (pipeline GitLab)

6. Métriques et amélioration
   ├─ Métriques à tracker
   └─ Partage d'apprentissages

7. Adoption progressive
   ├─ Phase 1 : Expérimentation (S1-2)
   ├─ Phase 2 : Premiers projets (S3-4)
   └─ Phase 3 : Généralisation (M2+)
```

---

## 💡 Utilisation

### Pour les développeurs

1. **Lire la charte** avant d'utiliser l'IA
2. **Respecter les règles** de sécurité et qualité
3. **Utiliser les prompts types** de la bibliothèque
4. **Partager les retours** d'expérience

### Pour les leads

1. **Faire respecter la charte** lors des reviews
2. **Collecter les métriques** de productivité
3. **Animer les retros IA** hebdomadaires
4. **Mettre à jour la charte** selon les besoins

### Pour le CTO / DSI

1. **Valider les outils autorisés**
2. **Auditer la sécurité** des pratiques
3. **Suivre les métriques** globales
4. **Ajuster la gouvernance** si nécessaire

---

## 📚 Compléments

### Bibliothèque de prompts (à créer)

```
charte/
└── prompts/
    ├── api-endpoint.md (générer un endpoint API Platform)
    ├── service.md (créer un service métier)
    ├── tests.md (générer des tests PHPUnit)
    ├── refactor.md (refactoring SOLID)
    └── debug.md (analyser une erreur)
```

**📝 TODO** : Créer ces templates pendant/après la formation

---

### Templates de retour d'expérience

Voir **Annexe C** de la charte pour le template de feedback.

**Usage** : Après chaque tâche avec IA, documenter :

- Ce qui a bien marché
- Ce qui a bloqué
- Prompts réutilisables
- Apprentissages

---

## 🔗 Ressources liées

- **Programme de formation** : [../PROGRAMME-FORMATION.md](../PROGRAMME-FORMATION.md)
- **Méthodologie PACT-R** : [../README.md](../README.md)
- **Exercices pratiques** : [../exercices/](../exercices/)
- **Constat métier** : [../Constat métier de développeur, IAG.md](../Constat%20métier%20de%20développeur,%20IAG.md)

---

## ✍️ Contribution

Cette charte est un **document vivant**.

**Pour proposer une amélioration** :

1. Créer une issue ou MR
2. Discuter en retro IA hebdomadaire
3. Valider avec les leads
4. Mettre à jour la charte

**Fréquence de révision** : Mensuelle (1er mois), puis trimestrielle

---

**La charte évolue avec l'équipe. Votre feedback est essentiel ! 🚀**
