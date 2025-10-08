# **1\) Fiabilité du code généré : mythe vs réalité \+ mode d’emploi**

**Ce que disent les données (contradictoires mais utiles)**

* Adoption élevée mais confiance limitée : **51 %** des pros utilisent des outils IA **au quotidien** et **84 %** les utilisent/planifient de le faire, mais **46 %** déclarent **ne pas faire confiance** à l’exactitude par défaut. ([survey.stackoverflow.co](https://survey.stackoverflow.co/2025/ai?utm_source=chatgpt.com))

* Gains possibles sur tâches simples : un RCT GitHub a montré **\+55,8 %** de vitesse sur une tâche JS bien spécifiée. ([arXiv](https://arxiv.org/abs/2302.06590?utm_source=chatgpt.com))

* Effet parfois négatif sur tâches réalistes et exigeantes : un RCT (METR, 2025\) sur des devs expérimentés a trouvé **\+19 % de temps** avec IA (plus lents) sur des issues “vraies vie” de gros repos. ([metr.org](https://metr.org/blog/2025-07-10-early-2025-ai-experienced-os-dev-study/))

* Sécurité : plusieurs études montrent que l’assistance IA **peut augmenter** la probabilité d’introduire des vulnérabilités si elle n’est pas cadrée. ([arXiv](https://arxiv.org/abs/2211.03622?utm_source=chatgpt.com))

* Dans l’écosystème startup : Y Combinator (W25) indique qu’**≈ 25 %** des startups ont **\~95 %** de code généré par IA — ce qui impose des process de revue/test béton. ([TechCrunch](https://techcrunch.com/2025/03/06/a-quarter-of-startups-in-ycs-current-cohort-have-codebases-that-are-almost-entirely-ai-generated/?utm_source=chatgpt.com))

* Côté sécu/supply chain, la presse spécialisée rappelle les **risques du “vibe coding” non gouverné** (variabilité d’output, traçabilité faible, gouvernance outillée rare). ([WIRED](https://www.wired.com/story/vibe-coding-is-the-new-open-source))

**Conclusion honnête à donner aux équipes**  
 L’IA peut accélérer **si et seulement si** le travail est **bien cadré** (problème clair, tests et règles établies, relecture outillée). Sans cela, elle **ralentit** et **fragilise** la sécurité.

**Mode d’emploi concret (PHP) pour en tirer du bon, sans se brûler :**

* **Spécifier avant de générer** : décrire l’intention, les contraintes d’API, les erreurs à gérer, les perfs attendues. (Bonnes pratiques de GitHub Copilot : prompt clair, décomposer, donner le contexte de fichiers). ([GitHub Docs](https://docs.github.com/en/copilot/get-started/best-practices?utm_source=chatgpt.com))

* **Test-first ou test-guided** : demander d’abord les **tests PHPUnit** puis l’implémentation ; exécuter et itérer jusqu’au vert. ([phpunit.de](https://phpunit.de/index.html?utm_source=chatgpt.com))

* **Revue systématique \+ SAST** : passer **PHPStan**/**Psalm** au niveau strict, refuser tout code non typé ; faire tourner **composer audit** en CI. ([phpstan.org](https://phpstan.org/?utm_source=chatgpt.com))

* **Refactoring outillé** : utiliser **Rector** pour standardiser/moderniser les patches générés (noms, signatures, idiomes PHP 8.x), puis retester. ([getrector.com](https://getrector.com/?utm_source=chatgpt.com))

* **Politiques d’outil IA** : suivre les best practices officielles (Copilot) et **désactiver tout “auto-run” risqué** dans les IDE agentiques (Cursor) ; l’agent propose, **jamais n’exécute** sans validation humaine. ([GitHub Docs](https://docs.github.com/en/copilot/get-started/best-practices?utm_source=chatgpt.com))

# **2\) Environnement & énergie : faits, ordres de grandeur et outils**

**Ce qu’on sait (et ce qu’on ne sait pas encore)**

* L’empreinte **varie énormément selon les modèles et l’usage** ; une initiative ouverte **AI Energy Score** compare l’efficacité énergétique entre modèles. ([huggingface.github.io](https://huggingface.github.io/AIEnergyScore/?utm_source=chatgpt.com))

* Étude Mistral (outil d’audit LCA) : pour **Large-2**, \~**1,14 g CO₂e** et **45 ml d’eau** **par prompt de 400 tokens** (ordre de grandeur utile pour sensibiliser). ([IT Pro](https://www.itpro.com/technology/artificial-intelligence/mistrals-new-sustainability-tracker-tool-shows-the-impact-ai-has-on-the-environment-and-it-makes-for-sober-reading?utm_source=chatgpt.com))

* Les estimations “grand public” restent incertaines ; l’**écart d’énergie** entre petits modèles et LLMs généralistes est **immense** (jusqu’à **× 62 000** sur certaines tâches), d’où l’intérêt de **choisir la bonne taille de modèle**. ([Financial Times](https://www.ft.com/content/ea513c7b-9808-47c3-8396-1a542bfc6d4f?utm_source=chatgpt.com))

**Boîte à outils pratico-pratique (dev & ops)**

* **Mesurer**

  * **SCI** (Software Carbon Intensity), devenu **ISO** : cadre standard pour mesurer l’intensité carbone d’un service logiciel. ([sci.greensoftware.foundation](https://sci.greensoftware.foundation/?utm_source=chatgpt.com))

  * **CodeCarbon** pour estimer l’énergie/CO₂ de jobs (CPU/GPU/RAM) locaux/CI. (NB : utile pour comparer, mais méthodes à manier avec précaution). ([GitHub](https://github.com/mlco2/codecarbon?utm_source=chatgpt.com))

  * **Electricity Maps API** pour piloter les jobs quand l’intensité carbone du réseau est basse (régionalisation, batchs planifiés). ([portal.electricitymaps.com](https://portal.electricitymaps.com/docs/getting-started?utm_source=chatgpt.com))

* **Réduire/optimiser**

  * Préférer des **modèles plus petits** pour la doc/génération simple ; réserver les LLMs lourds aux cas complexes. ([Financial Times](https://www.ft.com/content/ea513c7b-9808-47c3-8396-1a542bfc6d4f?utm_source=chatgpt.com))

  * Outiller le **front** avec **GreenFrame** (mesure de l’empreinte d’une page/app) et **ecoCode** (règles “green” dans SonarQube). ([GreenFrame](https://greenframe.io/?utm_source=chatgpt.com))

  * Côté cloud, exploiter les **dashboards carbone** natifs : **Google Cloud Carbon Footprint**, **AWS CCFT**, **Azure Emissions Impact Dashboard**. ([Google Cloud](https://cloud.google.com/carbon-footprint?utm_source=chatgpt.com))

# **3\) Marché & métier : quoi dire sans dramatiser**

**Court terme (0–12 mois)**

* **Gel des embauches tech** par rapport à 2020 : **–36 %** de postes tech aux USA (Indeed Hiring Lab, juillet 2025). Les entreprises privilégient des profils plus expérimentés. ([Indeed Hiring Lab Japan](https://www.hiringlab.org/2025/07/30/the-us-tech-hiring-freeze-continues/?utm_source=chatgpt.com))

* **Jeunes devs** : l’emploi des **22–25 ans** en “software developer” est **≈ –20 %** vs pic fin 2022 (analyse Stanford sur données ADP, août 2025). ([Stanford Digital Economy Lab](https://digitaleconomy.stanford.edu/wp-content/uploads/2025/08/Canaries_BrynjolfssonChandarChen.pdf?utm_source=chatgpt.com))

**Moyen terme (1–3 ans)**

* Le marché reste **porteur globalement** (BLS : **\+15 %** projetés 2024–2034 pour “software developers/QA/testers”), mais le contenu du travail change : supervision, intégration, sécurité, product-ops IA. ([Bureau of Labor Statistics](https://www.bls.gov/ooh/computer-and-information-technology/software-developers.htm?utm_source=chatgpt.com))

**Long terme (3–10 ans)**

* L’IA **augmente** surtout les **profils outillés** : architecture, qualité, CI/CD, sécurité ; les tâches juniors “boilerplate” sont **les plus automatisables**. (Voir aussi débats presse/think tanks : AI \= facteur parmi d’autres, pas l’unique cause du ralentissement). ([Barron's](https://www.barrons.com/articles/ai-artificial-intelligence-job-market-economy-3a2d9c9c?utm_source=chatgpt.com))

# **4\) Script de réponses aux objections (pour animer la journée)**

* **“Le code IA est peu fiable.”**  
   → Vrai **sans** garde-fous. Avec **tests \+ SAST \+ revues**, on transforme l’IA en **générateur d’implémentations candidates** qui passent vos exigences (tests, style, perf). **On ne remplace pas la relecture** — on l’outille. ([arXiv](https://arxiv.org/abs/2302.06590?utm_source=chatgpt.com))

* **“Ça va me faire perdre du temps.”**  
   → Possible au début (courbe d’apprentissage) et sur des tâches floues. On **structure** : prompt clair, **tests d’abord**, micro-itérations ; l’IA excelle sur **glue code**, docs, migrations répétitives (Rector), génération de tests. ([GitHub Docs](https://docs.github.com/en/copilot/get-started/best-practices?utm_source=chatgpt.com))

* **“C’est dangereux pour la sécu.”**  
   → Oui si on colle du code sans contrôle. **Politiques d’outil** (pas d’auto-run, liste blanche stricte), **composer audit**, scan SAST, et **revue humaine** restent non-négociables. ([backslash.security](https://www.backslash.security/blog/cursor-ide-security-best-practices?utm_source=chatgpt.com))

* **“C’est mauvais pour le climat.”**  
   → Ça **dépend du modèle et de l’usage**. Mesurer (SCI/CodeCarbon), **choisir des modèles plus légers** quand c’est suffisant et **planifier** sur des créneaux/regions à faible intensité carbone. ([Financial Times](https://www.ft.com/content/ea513c7b-9808-47c3-8396-1a542bfc6d4f?utm_source=chatgpt.com))

# **5\) Proposition de programme — 1 journée (7h)**

**Matin (3h30) — “Cadres & preuves”**

1. **Panorama chiffré & vocabulaire** (30’) — adoption, confiance, qualité/sécu, marché. ([survey.stackoverflow.co](https://survey.stackoverflow.co/2025/ai?utm_source=chatgpt.com))

2. **Atelier 1 – Test-first avec l’IA (PHP)** (75’)

   * Écrire tests **PHPUnit** pour une feature donnée, **ensuite** demander l’implémentation à l’IA, faire passer au vert. ([phpunit.de](https://phpunit.de/index.html?utm_source=chatgpt.com))

3. **Atelier 2 – Durcir la qualité** (60’)

   * **PHPStan/Psalm** niveau strict \+ **composer audit** \+ **Rector** sur le patch IA ; pipeline CI minimal. ([phpstan.org](https://phpstan.org/?utm_source=chatgpt.com))

4. **Rituels de revue “vibe coding”** (45’) — modèles de PR, checklists sécurité, conventions de prompts. ([GitHub Docs](https://docs.github.com/en/copilot/get-started/best-practices?utm_source=chatgpt.com))

**Après-midi (3h30) — “Sobriété & futur du métier”**  
 5\. **Mesurer l’empreinte et l’optimiser** (60’)

* Démo **SCI**, **CodeCarbon** (comparatif simple), **GreenFrame** (front), **Electricity Maps** pour planifier. ([sci.greensoftware.foundation](https://sci.greensoftware.foundation/?utm_source=chatgpt.com))

6. **Atelier 3 – Cartographier vos cas d’usage** (60’)

   * Sélectionner où l’IA **aide vraiment** (scaffold, test gen, migrations, doc) vs où **elle nuit** (algos critiques, perf, sécu).

7. **Carrières & organisation** (30’)

   * Rôles qui montent : **AI Toolsmith**, **DevSecOps** orienté IA, **test design** et **observabilité** ; panorama marché (court/moyen/long terme). ([Indeed Hiring Lab Japan](https://www.hiringlab.org/2025/07/30/the-us-tech-hiring-freeze-continues/?utm_source=chatgpt.com))

8. **Atelier 4 – Votre “charte IA” d’équipe** (60’)

   * Choix d’outils, secrets/données, interdits (auto-run), seuils de couverture, “Definition of Done” IA, gouvernance sécurité. ([backslash.security](https://www.backslash.security/blog/cursor-ide-security-best-practices?utm_source=chatgpt.com))

---

Si tu veux, je te génère le **support de formation** (slides \+ fiches atelier \+ checklists CI) et un **README “Charte IA PHP”** adapté à ta stack. Dis-moi pour quels frameworks (Laravel/Symfony/raw PHP) et IDE (VS Code/Cursor/PhpStorm) tu veux des pas-à-pas.

* [WIRED](https://www.wired.com/story/vibe-coding-is-the-new-open-source)  
* [IT Pro](https://www.itpro.com/technology/artificial-intelligence/mistrals-new-sustainability-tracker-tool-shows-the-impact-ai-has-on-the-environment-and-it-makes-for-sober-reading?utm_source=chatgpt.com)  
* [Financial Times](https://www.ft.com/content/ea513c7b-9808-47c3-8396-1a542bfc6d4f?utm_source=chatgpt.com)  
* [theverge.com](https://www.theverge.com/news/669339/github-ai-coding-agent-fix-bugs?utm_source=chatgpt.com)  
* [Barron's](https://www.barrons.com/articles/ai-artificial-intelligence-job-market-economy-3a2d9c9c?utm_source=chatgpt.com)

