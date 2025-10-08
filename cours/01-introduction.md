# Introduction : Vibe Coding & IA Générative pour le développement

**Format** : Présentation interactive

---

## 🎯 Objectifs

- Comprendre l'évolution du développement assisté par IA
- Connaître les chiffres clés vérifiés (adoption, productivité, emploi)
- Distinguer les mythes de la réalité
- Se situer dans les tendances du marché

---

## 📜 Historique du Vibe Coding

> 📖 **Pour un historique détaillé** : Voir [`ressources/historique.md`](ressources/historique.md) qui détaille l'origine du vibe coding, la méthodologie Plan-Act-Review-Repeat d'Andrej Karpathy, et les travaux d'Anthropic.

### Ligne du temps

**2021 : GitHub Copilot**

- Premier assistant IA grand public pour le code
- Basé sur OpenAI Codex (dérivé de GPT-3)
- Autocomplétion contextuelle dans l'éditeur
- Révolution : passage de "search Stack Overflow" à "ask AI"

**2022-2023 : Explosion des outils**

- **ChatGPT** (nov 2022) : Démocratisation de l'IA conversationnelle
- **Codeium, Tabnine, Replit Ghostwriter** : Alternatives à Copilot
- **Amazon CodeWhisperer** : Entrée des géants cloud

**2024 : Ère des coding agents**

- **Cursor** : IDE repensé pour l'IA (fork de VS Code)
- **Claude Code** : Agent IA capable de modifier plusieurs fichiers
- **GitHub Copilot Workspace** : De l'autocomplétion à la génération de features complètes
- **v0, Bolt, Lovable** : Générateurs d'applications complètes

**2025 : Vibe Coding devient mainstream**

- **25% des startups YC** avec ~95% de code généré par IA
- **Microsoft, Google, Robinhood** : 20-50% du code interne généré par IA
- Passage de "tool" à "pair programmer"

### Qu'est-ce que le "Vibe Coding" ?

**Définition** :  
AI Pair Programming
Développer en décrivant l'**intention** plutôt qu'en écrivant ligne par ligne. L'IA génère le code, le développeur valide, guide, et raffine.

**Origine** : Le terme a été inventé et popularisé en février 2025 par **Andrej Karpathy** (cofondateur d'OpenAI, ancien responsable IA chez Tesla) à travers un post viral sur X (ex-Twitter). Il a formalisé la méthodologie **Plan-Act-Review-Repeat** comme approche cyclique pour le développement assisté par IA. ([SoftyFlow](https://www.softyflow.io/vibe-coding/), [O'clock](https://oclock.io/le-vibe-coding-cest-quoi))

> 📖 **Détails historiques** : Voir [`ressources/historique.md`](ressources/historique.md)

**Caractéristiques** :

- Specs/intention d'abord, code ensuite
- Itérations rapides avec l'IA
- Focus sur la validation et les tests
- Moins de "boilerplate", plus de logique métier

---

## 📊 Chiffres clés

### Adoption massive et récente

| Métrique                | Chiffre                                     | Source                | Année     |
| ----------------------- | ------------------------------------------- | --------------------- | --------- |
| **Devs utilisant l'IA** | **84%** utilisent ou planifient d'utiliser  | Stack Overflow Survey | 2025      |
| **Usage quotidien**     | **51%** des pros utilisent **chaque jour**  | Stack Overflow Survey | 2025      |
| **Microsoft**           | **20-30%** du code interne généré par IA    | Satya Nadella         | 2025      |
| **Google**              | **>25-30%** du nouveau code assisté par IA  | Sundar Pichai         | 2024-2025 |
| **Robinhood**           | **~50%** du nouveau code généré par IA      | CEO Robinhood         | 2025      |
| **YC Startups**         | **25%** avec **~95%** de code généré par IA | Jared Friedman        | 2025      |

**📖 Sources complètes avec URLs** : Voir [`ressources/data.md`](ressources/data.md)

---

### Productivité : mythes vs réalité

#### ✅ Ce qui fonctionne (gains mesurés)

| Contexte                        | Gain                   | Étude                       | Remarque                               |
| ------------------------------- | ---------------------- | --------------------------- | -------------------------------------- |
| **Tâche simple bien spécifiée** | **+55,8%** de vitesse  | GitHub/Microsoft RCT (2023) | Tâche JS isolée                        |
| **Environnement contrôlé**      | **+10 à +15%** de gain | Bain Tech Report (2025)     | Mais **adoption faible** en entreprise |
| **Génération de tests**         | Significatif           | Retours terrain             | Accélération forte                     |
| **Boilerplate/migrations**      | Très efficace          | Retours terrain             | CRUD, glue code                        |

#### ❌ Ce qui NE fonctionne PAS (ralentissements observés)

| Contexte                               | Impact                           | Étude                 | Remarque                      |
| -------------------------------------- | -------------------------------- | --------------------- | ----------------------------- |
| **Devs expérimentés, repos complexes** | **+19% de temps** (plus lents !) | METR RCT (juil. 2025) | Repos réels, issues complexes |
| **Tâches floues/mal spécifiées**       | Perte de temps                   | Retours terrain       | Itérations inutiles           |
| **Algorithmes critiques**              | Contre-productif                 | Retours terrain       | Nécessite expertise humaine   |

**🎯 Conclusion honnête** :  
L'IA accélère **si et seulement si** :

- Le problème est **bien cadré** (specs claires)
- Les **tests sont en place**
- La **review est outillée** (SAST, linters)

Sans ces garde-fous, l'IA **ralentit et fragilise**.

---

### Emploi et marché

#### Court terme (0-12 mois) : Ralentissement

| Métrique                    | Chiffre                  | Source                         | Remarque              |
| --------------------------- | ------------------------ | ------------------------------ | --------------------- |
| **Offres tech USA**         | **-36%** vs début 2020   | Indeed Hiring Lab (juil. 2025) | Gel embauches         |
| **Jeunes devs (22-25 ans)** | **~-20%** vs pic 2022    | Stanford (août 2025)           | "Software developers" |
| **Métiers exposés à l'IA**  | **-13%** pour les jeunes | Stanford (août 2025)           | Tâches automatisables |

#### Moyen/long terme (1-10 ans) : Évolution, pas disparition

| Projection                 | Chiffre                               | Source                           | Remarque                          |
| -------------------------- | ------------------------------------- | -------------------------------- | --------------------------------- |
| **Software developers/QA** | **+15%** d'emplois projetés 2024-2034 | Bureau of Labor Statistics (USA) | Le marché reste porteur           |
| **Computer programmers**   | **-6%** projeté                       | BLS                              | Tâches "boilerplate" automatisées |

**🎯 Interprétation** :

- Les **tâches juniors répétitives** sont les plus automatisables
- Les **profils outillés** (architecture, qualité, CI/CD, sécurité) sont valorisés
- Le métier évolue : moins de "coder ligne par ligne", plus de "superviser, intégrer, valider"

---

## 🔍 Mythes vs Réalité

### Mythe 1 : "Le code IA est peu fiable"

**Réalité** :  
✅ **Vrai SANS garde-fous** (tests, SAST, review)  
✅ **Faux AVEC process rigoureux** (PACT-R, TDD, linters)

**Solution** :

- **Tests d'abord** (TDD obligatoire)
- **SAST strict** (PHPStan niveau 9, Psalm)
- **Review humaine** systématique
- **CI/CD avec métriques** (couverture >80%)

---

### Mythe 2 : "Ça va me faire perdre du temps"

**Réalité** :  
✅ **Vrai** au début (courbe d'apprentissage) et sur tâches floues  
✅ **Faux** une fois maîtrisé, sur tâches bien cadrées

**Solution** :

- **Structurer** : prompt clair, tests d'abord, micro-itérations
- **Identifier les bons cas d'usage** :
  - ✅ Glue code, CRUD, migrations
  - ✅ Génération de tests
  - ✅ Documentation
  - ❌ Algorithmes critiques
  - ❌ Optimisations performance

---

### Mythe 3 : "C'est dangereux pour la sécurité"

**Réalité** :  
✅ **Vrai** si on colle du code sans contrôle  
✅ **Plusieurs études** montrent une augmentation des vulnérabilités sans cadrage

**Solution** :

- **Politiques d'outil strictes** :
  - Pas d'auto-run de code
  - Liste blanche d'outils autorisés
- **Scans systématiques** :
  - `composer audit` en CI
  - SAST (PHPStan, Psalm, Snyk)
- **Review humaine** obligatoire
- **Charte de sécurité** (voir session 2)

**📖 Source** : [backslash.security - Cursor IDE Security Best Practices](https://www.backslash.security/blog/cursor-ide-security-best-practices)

---

### Mythe 4 : "C'est mauvais pour le climat"

**Réalité** :  
✅ **Dépend du modèle et de l'usage**  
✅ **L'écart est immense** entre petits modèles et LLMs lourds (jusqu'à ×62 000 sur certaines tâches)

**Ordres de grandeur** :

- Mistral Large-2 : **~1,14 g CO₂e** par prompt de 400 tokens
- Équivalent : **~45 ml d'eau** par prompt

**Solution** :

- **Mesurer** : Software Carbon Intensity (SCI), CodeCarbon
- **Choisir des modèles plus légers** quand suffisant
- **Planifier** : lancer jobs lourds quand intensité carbone faible (Electricity Maps API)
- **Optimiser** : caching, réutilisation de contexte

**📖 Sources** :

- [AI Energy Score (Hugging Face)](https://huggingface.github.io/AIEnergyScore/)
- [Mistral Sustainability Tracker](https://www.itpro.com/technology/artificial-intelligence/mistrals-new-sustainability-tracker-tool-shows-the-impact-ai-has-on-the-environment-and-it-makes-for-sober-reading)

---

## 🎓 Tendances du métier de développeur

### Ce qui change

| Avant (2020)                   | Maintenant (2025)                           | Compétences clés             |
| ------------------------------ | ------------------------------------------- | ---------------------------- |
| Écrire du code ligne par ligne | Décrire l'intention, valider le code généré | **Prompting efficace**       |
| Chercher sur Stack Overflow    | Demander à l'IA, puis vérifier              | **Esprit critique**          |
| Tests manuels ou après coup    | Tests d'abord (TDD obligatoire)             | **TDD strict**               |
| Review de code humain seul     | Review humaine + outils IA                  | **Maîtrise des outils SAST** |
| Focus : écrire du code         | Focus : architecture, qualité, sécurité     | **Vision globale**           |

### Compétences valorisées en 2025

1. **Architecture et design** : Découpage modulaire, API-First, SOLID
2. **Tests et qualité** : TDD, PBT, mutation testing, couverture >80%
3. **Sécurité** : SAST, supply chain, RGPD, secrets management
4. **CI/CD et DevOps** : Pipelines, observabilité, métriques
5. **Prompting efficace** : Savoir guider l'IA pour obtenir du bon code
6. **Product ops IA** : Intégrer l'IA dans les produits (MCP, RAG, agents)

### Nouveaux rôles émergents

- **AI Toolsmith** : Spécialiste de l'outillage IA pour équipes dev
- **DevSecOps orienté IA** : Sécurisation des workflows avec IA
- **Test Design Engineer** : Conception de stratégies de tests automatisés
- **AI Governance Lead** : Définition des politiques d'usage IA

---

## 💡 Points clés à retenir

1. **L'IA est un outil, pas un remplacement**

   - Elle accélère les bons développeurs
   - Elle ralentit si mal utilisée

2. **Le cadre est essentiel**

   - Specs claires + Tests d'abord + Review outillée = Gains réels
   - Sans cadre = Perte de temps + Risques sécu

3. **Le métier évolue**

   - Moins de "coder", plus de "concevoir et valider"
   - Les compétences valorisées changent

4. **Adopter progressivement**
   - Start small : tâches simples bien cadrées
   - Measure : métriques (temps, qualité, coût)
   - Adapt : ajuster selon retours terrain

---

## 📚 Ressources pour aller plus loin

### Documentation interne

- **Chiffres et sources vérifiées** : [`ressources/data.md`](ressources/data.md) - Toutes les sources avec URLs
- **Historique du vibe coding** : [`ressources/historique.md`](ressources/historique.md) - Origines, Plan-Act-Review-Repeat, personnalités clés
- **Constat et contexte** : [`ressources/constat.md`](ressources/constat.md) - Analyse du marché et tendances

### Chiffres et études

- [Stack Overflow Developer Survey 2025](https://survey.stackoverflow.co/2025/ai)
- [METR Study: AI and Experienced Developers (2025)](https://metr.org/blog/2025-07-10-early-2025-ai-experienced-os-dev-study/)
- [Bain Tech Report 2025: GenAI in Software Development](https://www.bain.com/insights/from-pilots-to-payoff-generative-ai-in-software-development-technology-report-2025/)
- [Stanford: Impact of AI on Young Developers (2025)](https://digitaleconomy.stanford.edu/wp-content/uploads/2025/08/Canaries_BrynjolfssonChandarChen.pdf)

### Sécurité et bonnes pratiques

- [GitHub Copilot Best Practices](https://docs.github.com/en/copilot/get-started/best-practices)
- [Cursor IDE Security Best Practices (Backslash Security)](https://www.backslash.security/blog/cursor-ide-security-best-practices)
- [WIRED: Vibe Coding is the New Open Source](https://www.wired.com/story/vibe-coding-is-the-new-open-source)

### Impact environnemental

- [AI Energy Score (Hugging Face)](https://huggingface.github.io/AIEnergyScore/)
- [Software Carbon Intensity (Green Software Foundation)](https://sci.greensoftware.foundation/)
- [CodeCarbon: Measure emissions of code execution](https://github.com/mlco2/codecarbon)

---

**Prochain module** : [Résultats du sondage interne](02-resultats-sondage.md)
