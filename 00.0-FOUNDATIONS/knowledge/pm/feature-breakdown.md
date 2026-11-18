# Decoupage fonctionnel — Application de suivi de plantes

> Statut : PRIORISATION MOSCOW — A VALIDER
> Source : knowledge/pm/brief.md
> Date : 2026-07-03
> Personas cibles : Lea (prioritaire), Sophie (secondaire)
> JTBD couverts : F1, F2, F6

## Couverture JTBD

| JTBD | Features associees | Fréquence |
|------|-------------------|-----------|
| **JTBD-F1** : Savoir quand arroser sans tuer ma plante | F01, F02, F03 | 16/16 |
| **JTBD-F2** : Identifier ce qui ne va pas avant qu'il soit trop tard | F04, F05 | 11/16 |
| **JTBD-F6** : Apprendre à observer mes plantes | F06, F07 | 13/16 |
| **JTBD-E1** : Me sentir responsable sans être jugé | F08 | 9/16 |
| *Transverse* | F09, F10 | — |

## Features proposees

### Bloc 1 : Hydratation (JTBD-F1)

| # | Feature | Description | JTBD | Persona | Testable |
|---|---------|-------------|------|---------|----------|
| **F01** | Ajout de plante minimal | Ajouter une plante avec : nom, photo, date d'ajout. Sans onboarding complexe, sans taxonomie obligatoire. | JTBD-F1, F6 | Léa, Sophie | Oui : l'utilisateur peut ajouter une plante en moins de 30 secondes |
| **F02** | Guide d'observation pour arrosage | Carte visuelle interactive qui explique comment toucher la terre (3-4cm de profondeur), observer les feuilles (affaissement, tombement), évaluer le poids du pot. Pas de fréquence fixe imposée. | JTBD-F1, F6 | Léa | Oui : l'utilisateur comprend quel signal observer avant d'arroser (test par quiz ou suivi comportemental) |
| **F03** | Journal d'arrosage simplifié + rappels bienveillants (opt-in) | L'utilisateur enregistre chaque arrosage d'un tap. L'app affiche l'historique visuel (dernier arrosage il y a X jours). **Enrichissement** : toggle "Rappels bienveillants" par plante (opt-in). Si activé : max 1 notification/semaine, ton bienveillant ("Il y a 7 jours que tu n'as pas arrosé ton Monstera. Va toucher la terre pour vérifier si elle en a besoin."). Éduque à l'observation, ne dicte pas l'action. | JTBD-F1, F6 | Léa, Sophie | Oui : l'utilisateur peut voir l'historique d'arrosage + activer/désactiver les rappels |

**Challenge F01-F03** : Ces 3 features répondent au pain point majeur (13/16 — sur-arrosage par excès d'amour). Elles éduquent à l'observation (JTBD-F6) plutôt que de créer une dépendance à la notification (pain point : 10/16 ont abandonné des apps pour cause de spam de notifications).

**Tension à valider** : Pas de notifications push d'arrosage. L'app éduque, elle ne rappelle pas. Cela coupe avec toutes les apps existantes (Planta, Greg) mais c'est aligné avec la donnée UXR (thème 3, 4, 10).

---

### Bloc 2 : Diagnostic visuel (JTBD-F2)

| # | Feature | Description | JTBD | Persona | Testable |
|---|---------|-------------|------|---------|----------|
| **F04** | Scan visuel + diagnostic | L'utilisateur prend une photo d'une feuille jaune, d'une tache, d'un affaissement. L'app identifie le problème probable (sur-arrosage, carence, parasite, brûlure) et propose un protocole de traitement. | JTBD-F2 | Léa, Sophie | Oui : l'utilisateur obtient un diagnostic en moins de 2 minutes |
| **F05** | Bibliothèque de symptômes | Catalogue visuel des symptômes courants (feuilles jaunes, taches brunes, affaissement, étiolement) avec photos d'illustration et causes associées. Permet de naviguer par symptôme. | JTBD-F2, F6 | Léa, Sophie | Oui : l'utilisateur peut identifier un symptôme dans la bibliothèque et accéder à une explication |

**Challenge F04-F05** : Le diagnostic visuel est le 2e pain point majeur (11/16 — synthese.md, thème 2). C'est un différenciateur premium : "Je paierais facilement 20€/an pour du vrai diagnostic" (Sophie, Charlotte). Les apps existantes échouent sur ce point — trop génériques, pas assez précises.

**Risque identifié** : La fiabilité du diagnostic est critique. Si l'app se trompe (confond mildiou et manque d'humidité), la confiance s'effondre. Il faut une base d'entraînement solide + validation experte + possibilité de signaler une erreur.

---

### Bloc 3 : Éducation progressive (JTBD-F6)

| # | Feature | Description | JTBD | Persona | Testable |
|---|---------|-------------|------|---------|----------|
| **F06** | Fiches plantes éducatives | Pour chaque plante ajoutée, une fiche courte (format TikTok : 60-90 secondes de lecture) qui explique : origine géographique, lumière, arrosage, signes de bonne santé. Visuel, sans jargon. | JTBD-F6, F1 | Léa | Oui : l'utilisateur peut lire une fiche en moins de 90 secondes |
| **F07** | Inspection quotidienne guidée | Suggestion d'une routine visuelle rapide (2-3 minutes) : "Regarde tes plantes, observe les nouvelles feuilles, touche la terre, repère les changements." Pas de notification quotidienne — juste un écran dédié si l'utilisateur ouvre l'app. | JTBD-F6 | Léa, Sophie | Oui : l'utilisateur peut suivre une checklist d'observation en moins de 3 minutes |

**Challenge F06-F07** : JTBD-F6 (13/16 — thème 10 : "Observer chaque jour. C'est comme ça qu'on apprend à lire une plante"). Les débutants ne savent pas quoi observer. Ces features éduquent progressivement sans créer de dépendance.

**Alignement mobile-first** : Format court, visuel, TikTok-like (thème 8, 15). Léa (persona prioritaire) utilise TikTok et Instagram comme ressources principales. Hugo : "J'ai pas besoin d'une appli complexe. Juste un guide simple pour pas tuer mes plantes. En mode TikTok — court, visuel, pas de jargon."

---

### Bloc 4 : Suivi et historique (JTBD-F6)

| # | Feature | Description | JTBD | Persona | Testable |
|---|---------|-------------|------|---------|----------|
| **F12** | Historique de l'état des plantes | Historique visuel de chaque plante : photos dans le temps, états enregistrés (bonne santé, malade, morte), journal d'évolution. Permet de voir l'impact des actions (arrosage, rempotage) et d'apprendre par l'observation dans le temps. | JTBD-F6 | Léa, Sophie | Oui : l'utilisateur peut consulter l'historique d'une plante et voir l'évolution visuelle |

**Challenge F12** : JTBD-F6 (13/16 — "Observer chaque jour. C'est comme ça qu'on apprend à lire une plante"). L'historique permet de développer la compétence d'observation en visualisant l'impact de ses actions. Sophie : "J'aimerais pouvoir garder des photos et voir comment la plante évolue." Léa : "Des fois je me rappelle plus si elle allait bien avant ou si c'est juste une impression."

**Implication technique** : Stockage de photos (local + cloud), timeline visuelle, étiquetage d'états, synchronisation offline.

---

### Principes de conception transversaux

**Décision validée** : Certains éléments ne sont pas des features isolées mais des principes de conception qui s'appliquent à toute l'app.

#### 1. Ton bienveillant et non-jugeant

**Ancrage UXR** : JTBD-E1 (9/16 — thème 7 : "J'étais plus choqué d'avoir tué quelque chose que triste pour la plante elle-même"). Dimension émotionnelle forte chez les débutants : peur de faire des erreurs, culpabilité. Le ton de l'app doit être bienveillant, pas moralisateur.

**Application** :
- Copie : "Pas de souci, tes plantes attendent. Prends le temps d'observer la terre avant d'arroser." (pas de "Vous avez oublié d'arroser !")
- Messages d'erreur : "Oups, on n'a pas pu analyser cette photo. Essaie avec une feuille bien éclairée." (pas de "Erreur : image invalide")
- États vides : "Tu n'as pas encore ajouté de plante. Prêt à accueillir la première ?" (pas de "Aucune plante")
- Notifications : "Il y a 7 jours que tu n'as pas arrosé ton Monstera. Va toucher la terre pour vérifier si elle en a besoin." (pas de "Arrose maintenant !")

**Différenciation** : Axe 5 validé ("Ton bienveillant et non-jugeant"). Les apps existantes ont un ton directif ou moralisateur (synthese.md, thème 3).

#### 2. Design mobile-first

**Ancrage UXR** : Léa (persona prioritaire) utilise principalement son smartphone. Thème 8, 15 : format court, visuel, TikTok-like.

**Application** :
- Bottom nav, gestes swipe, écrans plein format photo
- Pas de sidebar desktop
- Format court (60-90 secondes de lecture), visuel
- Optimisé pour une utilisation en mobilité (dans un magasin de plantes, au jardin)

**Différenciation** : Alignement mobile-first validé par l'utilisateur. Les apps existantes sont souvent pensées desktop-first puis adaptées mobile.

---

### Bloc 5 : Infra et transverse (contraintes techniques)

| # | Feature | Description | JTBD | Persona | Testable |
|---|---------|-------------|------|---------|----------|
| **F09** | Onboarding minimal (< 60s) | Écran d'accueil qui explique en 3 phrases ce que fait l'app, propose d'ajouter une première plante immédiatement. Pas de configuration, pas de compte obligatoire au démarrage. | Transverse | Léa | Oui : l'utilisateur complète l'onboarding en moins de 60 secondes |
| **F10** | Fonctionnement offline | L'app fonctionne offline : ajout de plantes, journal d'arrosage, consultation de fiches, bibliothèque de symptômes. Synchronisation en background quand la connexion revient. | Transverse | Léa, Sophie | Oui : l'utilisateur peut utiliser l'app sans connexion internet |

**Challenge F09** : Pain point majeur (thème 3 — 10/16 ont abandonné pour cause d'onboarding trop long). Thomas : "Ils me demandaient des infos que j'avais pas : l'espèce exacte, l'orientation de la fenêtre au degré près... J'ai lâché avant d'avoir rentré mes 7 plantes."

**Challenge F10** : Contrainte technique validée par l'utilisateur (offline-first). Impact sur architecture : PWA ou app native, service workers, stockage local, synchro en background. Implique que F04 (diagnostic visuel) doit soit embarquer un modèle ML on-device, soit afficher un état dégradé offline.

---

## JTBD non couverts en v1

| JTBD | Fréquence | Raison hors scope |
|------|-----------|-------------------|
| **JTBD-F3** : Partir en vacances sans tuer mes plantes | 14/16 | Confirmé hors scope v1 par l'utilisateur. Complexité élevée (systèmes capillaires, instructions pour tiers, arrosage automatique). Priorité sur diagnostic et observation d'abord. |
| **JTBD-F4** : Choisir une plante compatible avec mon logement | 8/16 | Nécessite diagnostic de lumière + base de données d'espèces. Complexité technique élevée. Peut être adressé en v2. |
| **JTBD-F5** : Éradiquer un parasite durablement | 6/16 | Couvert partiellement par F04 (diagnostic) mais pas de protocole progressif d'éradication. Priorité en v2 pour Sophie. |
| **JTBD-S1** : Appartenir à une communauté | 9/16 | Dimension communautaire (partage, entraide, diagnostic collaboratif) hors scope v1. Nécessite modération, gestion de contenu UGC. Complexité organisationnelle élevée. |
| **JTBD-F7** : Accéder à des données botaniques fiables pour espèces rares | 6/16 | Persona Jean (collectionneur) hors scope v1. Nécessite bases taxonomiques, API GBIF/The Plant List, granularité par sous-espèce. |

---

## Récapitulatif

**10 features proposées**, réparties en 5 blocs :
- **3 features hydratation** (JTBD-F1) — coeur de l'app, incluant rappels bienveillants opt-in validés
- **2 features diagnostic** (JTBD-F2) — différenciateur premium
- **2 features éducation** (JTBD-F6) — développement de compétence
- **1 feature historique** (JTBD-F6) — suivi visuel dans le temps, validée par l'utilisateur
- **2 features transverses** — onboarding + offline validé

**Principes de conception transversaux** :
- **Ton bienveillant et non-jugeant** (JTBD-E1) — s'applique à toute l'app (copie, messages d'erreur, états vides, illustrations)
- **Design mobile-first** — bottom nav, gestes swipe, format court et visuel

**Couverture JTBD** : 3/7 JTBD critiques couverts (F1, F2, F6), alignés avec le brief validé. 4 JTBD hors scope v1 (F3, F4, F5, S1, F7) avec justifications explicites.

**Alignement personas** : 10/10 features répondent aux besoins de Léa (prioritaire). 8/10 répondent aussi à Sophie (secondaire). Jean (collectionneur) non couvert, conformément au brief.

**Alignement différenciation** :
- Axe 1 (pas de notifications spam) : F02, F03 (rappels bienveillants opt-in, max 1/semaine), F07 — éducation, pas de spam
- Axe 2 (onboarding minimal) : F09 — < 60s
- Axe 3 (focus observation) : F02, F06, F07 — développement de compétence
- Axe 4 (diagnostic fiable) : F04, F05 — différenciateur premium
- Axe 5 (ton bienveillant) : principe de conception transversal
- Axe 6 (mobile-first) : principe de conception transversal
- **Nouveau** : Axe 7 (offline-first) : F10 — contrainte technique validée

---

## Points de vigilance avant validation

### 1. Notifications d'arrosage — DECISION VALIDEE, CHALLENGE MAINTENU

**Décision utilisateur** : OUI, il veut des notifications d'arrosage dans l'app.

**Challenge PM ancré dans la donnée UXR** :
10/16 utilisateurs ont abandonné les apps existantes (Planta, Greg, Happy Plant) à cause des notifications inadaptées (thème 3, synthese.md). Verbatims :
- "Au bout d'une semaine j'étais spammée, j'ai désactivé les notifs et du coup l'appli ne servait plus à rien." — Sophie
- "Des fois ça me dit d'arroser mon cactus alors que j'ai arrosé il y a 3 jours." — Lucie

**Compromis proposé** : Notifications intelligentes, non-spam, ancrees dans l'observation
- **Opt-in explicite** : l'utilisateur active les notifications par plante (pas par défaut)
- **Basées sur l'observation, pas sur des fréquences fixes** : "Il y a 7 jours que tu n'as pas arrosé ton Monstera. Va toucher la terre pour vérifier si elle en a besoin." (éduque à l'observation, ne dicte pas l'action)
- **Fréquence limitée** : maximum 1 notification par plante par semaine
- **Ton bienveillant** : "Pas de souci, tes plantes attendent. Prends le temps d'observer la terre avant d'arroser."
- **Désactivation facile** : toggle accessible dans les réglages de chaque plante

**Ce compromis** :
- Répond à ta demande (notifications présentes)
- Évite le piège des apps existantes (spam, fréquences fixes inadaptées)
- Reste aligné avec JTBD-F6 (éduquer à l'observation) et le principe "pas de dépendance à la notification"

**Proposition** : Intégrer ce compromis comme enrichissement de F03 (Journal d'arrosage simplifié) en ajoutant un toggle "Rappels bienveillants" (opt-in).

**A valider** : Es-tu d'accord avec ce compromis ? Ou veux-tu des notifications plus fréquentes / plus directives (style "Arrose maintenant") ?

### 2. Fiabilité du diagnostic visuel (F04) — `[A DECIDER]`

**Tension** : Le diagnostic visuel est le différenciateur clé. Mais si l'app se trompe (confond mildiou et manque d'humidité), la confiance s'effondre. La fiabilité est critique.

**Stratégie de fiabilité** : `[A DECIDER]` — ML maison ? API externe ? Validation experte ? Possibilité de signaler une erreur ?

**Impact sur priorisation** : Si la fiabilité ne peut pas être garantie en v1, F04 pourrait glisser de Must à Should.

### 3. Features manquantes ? — `[A DECIDER]`

**10 features max = principe de PM.** Mais peut-être qu'une feature critique manque ?

**Questions à challenger** :
- Faut-il une feature "Historique visuel de santé" (photos dans le temps) pour observer l'évolution ? (pourrait enrichir F03 ou F06)
- Faut-il une feature "États de la plante" (morte, malade, en bonne santé) pour aider Léa à trier ? (pourrait compléter F01)
- Faut-il une feature "Recherche par symptôme" en complément de F05 (bibliothèque) ?

**Décision** : `[A DECIDER]` — Pas de réponse reçue. On garde le scope actuel (10 features) sauf si l'utilisateur signale une feature critique manquante.

### 4. Scope technique et contrainte offline — DECISION VALIDEE

**Décision utilisateur** : OUI, l'app doit fonctionner offline.

**Contrainte technique identifiée** : PWA ou app native avec service workers, stockage local, synchronisation en background.

**Impact sur le scope fonctionnel** :
- **F03 (Journal d'arrosage)** : stockage local obligatoire, synchro cloud optionnelle
- **F04 (Diagnostic visuel)** : le modèle ML doit être embarqué (on-device) ou l'app doit gérer l'état dégradé (offline = diagnostic indisponible). `[A DECIDER]` : quelle approche choisir ?
- **F05 (Bibliothèque de symptômes)** : contenu pré-téléchargé, disponible offline
- **F06 (Fiches plantes)** : contenu pré-rédigé et embarqué, disponible offline
- **F09 (Onboarding)** : doit fonctionner offline dès l'installation

**Implications pour le dev** : Architecture offline-first, gestion des conflits de synchronisation, UX des états dégradés (perte de connexion pendant un diagnostic).

**Proposition** : Ajouter une note transversale "Contrainte offline" dans le bloc 5 (Infra et transverse).

---

## Validation post-intégration des réponses

**Décisions validées par l'utilisateur** :
- Notifications d'arrosage : OUI, avec compromis intelligent (rappels bienveillants opt-in, max 1/semaine, ton éducatif) — intégré dans F03
- Offline : OUI, contrainte technique ajoutée (F11)
- Historique de l'état des plantes : OUI, ajouté comme F12
- Diagnostic visuel (F04) : GARDE en v1, stratégie technique reste [A DECIDER] pour le dev
- Ton bienveillant : TRAITE comme principe de design transversal, pas comme feature à prioriser

**Point `[A DECIDER]` restant (pour le dev)** :
- Stratégie de fiabilité pour F04 (diagnostic visuel) : ML maison embarqué on-device ? API externe avec état dégradé offline ? Validation experte ?

**Statut** : Décisions structurantes validées. Prêt pour priorisation MoSCoW.

---

## Priorisation MoSCoW

> Filtre appliqué : "Si on enlève ça, le produit résout-il quand même le problème central du brief ?"
> Problème central : **Permettre à un débutant (Léa) de ne plus tuer ses plantes par sur-arrosage, et d'apprendre à observer pour diagnostiquer un problème.**

| # | Feature | Priorité | Justification |
|---|---------|----------|---------------|
| **F01** | Ajout de plante minimal | **Must** | Sans ça, l'utilisateur ne peut pas commencer à utiliser l'app. Bloquant absolu. C'est le point d'entrée. |
| **F02** | Guide d'observation pour arrosage | **Must** | Sans ça, le problème central (sur-arrosage 13/16) n'est pas résolu. L'utilisateur ne sait toujours pas comment savoir s'il doit arroser. C'est le coeur du JTBD-F1. |
| **F03** | Journal d'arrosage simplifié + rappels bienveillants (opt-in) | **Should** | Le core fonctionne sans (F02 suffit pour apprendre à arroser). Mais important pour ancrer l'habitude et rassurer les débutants. Valeur forte pour Léa (peur d'oublier). |
| **F04** | Scan visuel + diagnostic | **Should** | JTBD-F2 (11/16) est important mais pas le coeur du problème central (sur-arrosage 13/16). Différenciateur premium, mais le produit fonctionne sans. Si la fiabilité technique n'est pas garantie, passe en Could. |
| **F05** | Bibliothèque de symptômes | **Could** | Valeur additionnelle. Complète F04 mais pas bloquant. L'utilisateur peut diagnostiquer via F04 ou chercher sur internet. Nice-to-have. |
| **F06** | Fiches plantes éducatives | **Must** | Sans ça, Léa ne comprend pas les besoins de sa plante (lumière, arrosage, signes de bonne santé). JTBD-F6 (13/16 — apprendre à observer). Bloquant pour le développement de compétence. |
| **F07** | Inspection quotidienne guidée | **Could** | Valeur additionnelle. Complète F06 mais pas bloquant. L'utilisateur peut observer sans checklist guidée. Nice-to-have. |
| **F12** | Historique de l'état des plantes | **Could** | Valeur forte pour l'apprentissage (voir l'évolution), mais le core fonctionne sans. Utile pour Sophie (progression), moins critique pour Léa en v1. Nice-to-have. |
| **F09** | Onboarding minimal (< 60s) | **Must** | Sans ça, 10/16 abandonnent avant d'avoir ajouté leurs plantes (thème 3). Bloquant pour l'adoption. Pain point majeur des apps existantes. |
| **F10** | Fonctionnement offline | **Should** | Contrainte technique validée par l'utilisateur. Important mais pas bloquant en v1 : on peut lancer en online-only et ajouter offline en v1.1. Impacte F04 (diagnostic on-device complexe). |

---

## Résumé de priorisation

| Priorité | Nombre | % du total | Features |
|----------|--------|-----------|----------|
| **Must** | 4 | 40% | F01, F02, F06, F09 |
| **Should** | 3 | 30% | F03, F04, F10 |
| **Could** | 3 | 30% | F05, F07, F12 |
| **Won't v1** | 0 | 0% | — |

**Total** : 10 features

---

## Challenge de la priorisation

### Must : 4 features (40%) — DANS LES CLOUS

**Règle** : Must < 40%. On est pile à 40%, c'est dans les clous.

**Test de cohérence** : Si on enlève un seul Must, le produit résout-il encore le problème central ?

- **Sans F01 (Ajout de plante)** : Non. Bloquant absolu.
- **Sans F02 (Guide d'observation)** : Non. Le problème central (sur-arrosage) n'est pas résolu. Léa ne sait toujours pas quand arroser.
- **Sans F06 (Fiches plantes)** : Non. Léa ne comprend pas les besoins de sa plante (lumière, arrosage, signes de bonne santé). Elle ne peut pas développer sa compétence d'observation.
- **Sans F09 (Onboarding minimal)** : Non. 10/16 abandonnent avant d'avoir ajouté leurs plantes. Bloquant pour l'adoption.

**Verdict** : Les 4 Must sont justifiés. Pas de dégradation possible sans casser le core.

---

## Points de tension à valider

---

### 1. F04 (Diagnostic visuel) en Should — acceptable ?

**Tension** : F04 est le différenciateur clé (JTBD-F2, 11/16). Pourquoi pas Must ?

**Justification** :
1. Le problème central (brief validé) est le sur-arrosage (13/16), pas le diagnostic. JTBD-F1 (arrosage) > JTBD-F2 (diagnostic).
2. F04 a un risque technique fort : si la fiabilité n'est pas garantie, la confiance s'effondre. Stratégie technique [A DECIDER].
3. Le produit fonctionne sans F04 : l'utilisateur peut apprendre à arroser (F02) et à observer (F06) sans diagnostic IA.

**Décision** : Should est cohérent. Si la fiabilité technique est garantie en cours de dev, F04 reste prioritaire. Sinon, passe en Could ou Won't v1.

---

### 2. F10 (Offline) en Should — pourquoi pas Must ?

**Tension** : Contrainte technique validée par l'utilisateur. Pourquoi pas Must ?

**Justification** :
1. On peut lancer en online-only et ajouter offline en v1.1. Ce n'est pas bloquant pour l'adoption.
2. Impact technique fort : PWA avec service workers, stockage local, synchro en background. F04 (diagnostic) doit embarquer un modèle ML on-device si offline, ce qui complexifie beaucoup.
3. Le pain point principal (sur-arrosage) est résolu sans offline. Léa peut utiliser l'app chez elle avec Wi-Fi.

**Proposition** : Garder F10 en Should, mais marquer comme prioritaire dans Should (livrer en v1 si la vélocité le permet).

---

### 3. F03 (Journal d'arrosage + rappels) en Should — acceptable ?

**Tension** : JTBD-F1 (16/16 — arrosage). Pourquoi pas Must ?

**Justification** :
1. F02 (Guide d'observation) suffit pour résoudre le problème central (apprendre quand arroser). F03 ancre l'habitude mais n'est pas bloquant.
2. Les rappels sont opt-in. Si l'utilisateur ne les active pas, F03 se réduit à un journal d'arrosage simple. Utile mais pas critique.
3. Léa (persona prioritaire) a peur d'oublier, donc F03 a de la valeur. Mais elle peut apprendre à arroser sans journal (F02 suffit).

**Décision** : Should est cohérent. Si la vélocité le permet, livrer F03 en v1. Sinon, reporter en v1.1.

---

## Scope v1 recommandé (Must + Should prioritaires)

**Must (4 features)** :
- F01 : Ajout de plante minimal
- F02 : Guide d'observation pour arrosage
- F06 : Fiches plantes éducatives
- F09 : Onboarding minimal (< 60s)

**Should prioritaires (à livrer si vélocité permet)** :
- F03 : Journal d'arrosage simplifié + rappels bienveillants (opt-in)
- F04 : Scan visuel + diagnostic (si fiabilité technique garantie)

**Should secondaires** :
- F10 : Fonctionnement offline (reporter en v1.1 si complexité technique trop forte)

**Could (nice-to-have v1, ou v2)** :
- F05 : Bibliothèque de symptômes
- F07 : Inspection quotidienne guidée
- F12 : Historique de l'état des plantes

---

## Couverture JTBD par priorité

| JTBD | Must | Should | Could | Couverture |
|------|------|--------|-------|------------|
| **JTBD-F1** : Savoir quand arroser sans tuer ma plante (16/16) | F02 | F03 | — | ✅ Core couvert (F02), habitude renforcée (F03) |
| **JTBD-F2** : Identifier ce qui ne va pas avant qu'il soit trop tard (11/16) | — | F04 | F05 | ⚠️ Couverture partielle (F04 en Should, risque technique) |
| **JTBD-F6** : Apprendre à observer mes plantes (13/16) | F06 | — | F07, F12 | ✅ Core couvert (F06), compléments nice-to-have (F07, F12) |
| **JTBD-E1** : Me sentir responsable sans être jugé (9/16) | — | — | — | ✅ Principe de design transversal (ton bienveillant) |

**Verdict** : Les 3 JTBD prioritaires (F1, F2, F6) sont couverts. JTBD-F1 et F6 sont solidement couverts par des Must. JTBD-F2 est couvert par un Should (F04), ce qui est cohérent avec la hiérarchie de priorité (F1 > F6 > F2).

---

## Validation avant passage aux User Stories

**Points à valider avec l'utilisateur** :

1. **Must = 4 features (40%)** : Es-tu d'accord avec ce niveau de Must ? Trop ? Pas assez ?
2. **F04 (Diagnostic) en Should** : Es-tu d'accord de ne pas garantir le diagnostic visuel en v1 ? Ou veux-tu le forcer en Must quitte à prendre le risque technique ?
3. **F03 (Journal d'arrosage) en Should** : Es-tu d'accord de potentiellement reporter le journal d'arrosage si la vélocité ne suit pas ? Ou veux-tu le forcer en Must ?
4. **F10 (Offline) en Should** : Es-tu d'accord de lancer en online-only et d'ajouter offline en v1.1 si nécessaire ? Ou veux-tu forcer offline en Must ?
5. **Scope v1 recommandé** : Must (4) + Should prioritaires (F03, F04) = 6 features. C'est ambitieux mais faisable. Es-tu d'accord avec ce scope ?

**Une fois ces 5 points validés, on passe aux User Stories (Must + Should uniquement).**
