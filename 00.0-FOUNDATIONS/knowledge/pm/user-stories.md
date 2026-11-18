# User Stories — Application de suivi de plantes

> Statut : A VALIDER
> Source : knowledge/pm/feature-breakdown.md
> Date : 2026-07-06
> Scope : Must + Should uniquement (7 features sur 10)
> Decoupage : granulaire avec separation Design / Tech — une US par comportement distinct

## Vue d'ensemble

| US | Type | Feature | Status | Persona | JTBD |
|----|------|---------|--------|---------|------|
| US-000 | Tech | Scaffolding — Setup technique | Backlog | Lea, Sophie | Transverse |
| US-001 | Design | F01 — Ajout de plante | Backlog | Lea | JTBD-F1, F6 |
| US-002 | Tech | F01 — Ajout de plante | Backlog | Lea | JTBD-F1, F6 |
| US-003 | Design | F02 — Guide d'observation pour arrosage | Backlog | Lea | JTBD-F1, F6 |
| US-004 | Tech | F02 — Guide d'observation pour arrosage | Backlog | Lea | JTBD-F1, F6 |
| US-005 | Design | F06 — Fiches plantes educatives | Backlog | Lea | JTBD-F6, F1 |
| US-006 | Tech | F06 — Base de fiches plantes embarquee | Backlog | Lea | JTBD-F6, F1 |
| US-007 | Tech | F06 — Identification automatique via API | Backlog | Lea | JTBD-F6, F1 |
| US-008 | Design | F09 — Onboarding | Backlog | Lea | Transverse |
| US-009 | Tech | F09 — Onboarding | Backlog | Lea | Transverse |
| US-010 | Design | F03 — Journal d'arrosage + historique visuel | Backlog | Lea, Sophie | JTBD-F1, F6 |
| US-011 | Design | F03 — Rappels bienveillants (opt-in) | Backlog | Lea, Sophie | JTBD-F1, F6 |
| US-012 | Tech | F03 — Journal d'arrosage + rappels | Backlog | Lea, Sophie | JTBD-F1, F6 |
| US-013 | Design | F04 — Ecran de scan et etats | Backlog | Lea, Sophie | JTBD-F2 |
| US-014 | Design | F04 — Resultat diagnostic et feedback | Backlog | Lea, Sophie | JTBD-F2 |
| US-015 | Tech | F04 — Compression et envoi photo | Backlog | Lea, Sophie | JTBD-F2 |
| US-016 | Tech | F04 — Integration API diagnostic | Backlog | Lea, Sophie | JTBD-F2 |
| US-017 | Tech | F04 — Gestion erreurs et fallback offline | Backlog | Lea, Sophie | JTBD-F2 |
| US-019 | Tech | F10 — Stockage local et service workers | Backlog | Lea, Sophie | Transverse |
| US-020 | Tech | F10 — Detection connexion et sync auto | Backlog | Lea, Sophie | Transverse |
| US-021 | Tech | F10 — Synchronisation en background | Backlog | Lea, Sophie | Transverse |
| US-022 | Design | F10 — Etats degrades offline | Backlog | Lea, Sophie | Transverse |

**Total** : 22 User Stories (1 Scaffolding + 9 Must + 12 Should)
- **Design** : 8 US
- **Tech** : 14 US

---

## Stories detaillees

---

## Scaffolding

### US-000 [Tech] — Setup technique du projet

**Feature source :** Scaffolding — Setup technique
**Status :** Backlog
**Type :** Tech
**Persona :** Lea, Sophie — utilisatrices en mobilite
**JTBD :** Transverse (prerequis a toutes les US Tech)

En tant que developpeur
Je veux initialiser le projet technique (repo, stack, CI, structure de dossiers, linting, tests)
Afin que toutes les US Tech puissent etre implementees sur une base solide et coherente

**Criteres d'acceptation**

Scenario : Happy path — Projet initialise et deployable
  Given je cree le projet technique
  When le setup est termine
  Then le repo est initialise avec la structure de dossiers (src/, public/, tests/)
  And la stack est configuree : framework front (React/Vue/Svelte), bundler, TypeScript
  And le linting et le formatage sont configures (ESLint, Prettier)
  And un pipeline CI basique est en place (lint + tests + build)
  And le projet se deploie en environnement de dev (staging)
  And un README.md explique comment lancer le projet en local

Scenario : PWA — Manifest et service worker de base
  Given le projet cible une PWA
  When je configure le manifest et le service worker
  Then un manifest.json est cree avec le nom de l'app, les icones et la couleur du theme
  And un service worker de base est enregistre (cache du shell applicatif)
  And l'app est installable sur mobile (prompt "Ajouter a l'ecran d'accueil")
  And le mode offline affiche au minimum le shell applicatif

Scenario : Base de donnees locale — Schema initial
  Given je configure le stockage local
  When je cree le schema initial
  Then IndexedDB (ou SQLite) est configure avec les tables : plants, waterings, settings
  And les migrations sont gerees (versioning du schema)
  And un jeu de donnees de test est disponible pour le dev

**Edge cases a couvrir**
- Navigateur sans support service worker : fallback online-only avec detection
- Navigateur sans support IndexedDB : fallback localStorage avec avertissement (fonctionnalites limitees)
- Environnement de dev vs. production : variables d'environnement separees
- Hot reload en dev : service worker ne bloque pas le hot reload
- Tests : framework de tests configure (Vitest/Jest) avec au moins 1 test passant

**Depend de :** Aucune (US fondatrice)

---

## F01 — Ajout de plante (Must)

### US-001 [Design] — Concevoir l'ecran d'ajout de plante

**Feature source :** F01 — Ajout de plante
**Status :** Backlog
**Type :** Design
**Persona :** Lea, la debutante qui ne veut pas tuer ses plantes — arrose de facon irreguliere, utilise TikTok/Instagram comme ressources principales, n'a aucune connaissance prealable en jardinage
**JTBD :** JTBD-F1 (Savoir quand arroser sans tuer ma plante), JTBD-F6 (Apprendre a observer mes plantes)

En tant que designer
Je veux concevoir un ecran d'ajout de plante epure avec 3 champs maximum (nom, photo, bouton confirmer)
Afin que Lea puisse ajouter sa premiere plante en moins de 30 secondes sans se sentir perdue ou jugee

**Criteres d'acceptation**

Scenario : Happy path — Ecran d'ajout optimise pour le premier usage
  Given je concois l'ecran d'ajout de premiere plante
  When je structure les elements visuels
  Then l'ecran contient exactement 3 elements : 1 champ texte "Donne-lui un petit nom", 1 bouton "Ajouter une photo", 1 bouton principal "Ajouter ma plante"
  And le champ nom est autofocus au chargement de l'ecran
  And le bouton "Ajouter ma plante" est desactive (grayed out) tant que le nom n'est pas renseigne
  And le ton de tous les microcopy est bienveillant ("Donne-lui un petit nom", "Ajoute une photo si tu veux")
  And aucun champ taxonomique (espece, famille) n'est visible
  And la hierarchie visuelle guide vers le champ nom en premier

Scenario : Etat vide — Collection sans plante
  Given je concois l'etat vide de la collection
  When l'utilisateur ouvre l'app pour la premiere fois et n'a aucune plante
  Then l'ecran affiche une illustration accueillante (silhouette de plante bienveillante, pas triste)
  And un message rassurant : "Tu n'as pas encore ajoute de plante. Pret·e a accueillir la premiere ?"
  And un CTA principal bien visible : "Ajouter ma premiere plante"
  And le CTA occupe au moins 20% de la hauteur de l'ecran (tactile large)

Scenario : Erreur — Tentative d'ajout sans nom
  Given je concois le feedback d'erreur
  When l'utilisateur tente de valider sans avoir saisi de nom
  Then le bouton "Ajouter ma plante" reste desactive (pas de clic possible)
  And un message bienveillant apparait sous le champ nom : "Donne-lui un petit nom pour la retrouver facilement."
  And le message d'erreur n'utilise jamais les mots "erreur", "invalide", "obligatoire"
  And le champ nom est mis en evidence (focus visuel doux, pas de rouge agressif)

**Edge cases a couvrir**
- Etat vide (aucune plante) : illustration accueillante + CTA principal bien visible
- Ajout sans photo : image par defaut (silhouette de plante bienveillante) + suggestion douce "Tu pourras ajouter une photo plus tard"
- Nom trop long (> 50 caracteres) : troncature avec "..." dans la liste de collection
- Capture photo en faible luminosite : l'app accepte, suggere de reprendre une photo en meilleure lumiere plus tard
- Micro-interaction apres ajout reussi : feedback visuel immediat (animation douce, message "Bienvenue dans ta jungle !")
- Geste de retour arriere (swipe ou bouton) : si formulaire rempli, confirmation douce "Veux-tu vraiment quitter sans ajouter ta plante ?"

**Depend de :** Aucune

---

### US-002 [Tech] — Implementer le stockage local et la synchronisation d'ajout de plante

**Feature source :** F01 — Ajout de plante
**Status :** Backlog
**Type :** Tech
**Persona :** Lea, la debutante qui ne veut pas tuer ses plantes
**JTBD :** JTBD-F1, JTBD-F6

En tant que developpeur
Je veux implementer le stockage local des plantes avec synchronisation cloud en background
Afin que l'utilisateur puisse ajouter des plantes meme offline et les retrouver sur tous ses appareils

**Criteres d'acceptation**

Scenario : Happy path — Ajout de plante avec sauvegarde locale
  Given l'utilisateur a saisi un nom ("Mon monstera") et pris une photo
  When il clique sur "Ajouter ma plante"
  Then la plante est sauvegardee en local avec les champs : id (UUID), nom, photo (blob ou path), date_ajout, date_modification
  And la photo est compressee avant stockage (max 1 Mo, qualite 80%, resolution max 1920x1080)
  And la plante apparait immediatement dans la liste de collection (affichage optimiste)

Scenario : Ajout sans photo
  Given l'utilisateur ne prend pas de photo
  When il clique sur "Ajouter ma plante" avec seulement un nom
  Then la plante est sauvegardee avec une image par defaut
  And l'utilisateur peut ajouter une photo plus tard depuis la fiche plante

Scenario : Erreur — Echec de compression de photo
  Given l'utilisateur ajoute une photo de tres grande taille (> 10 Mo, 4K)
  When l'app tente de compresser la photo et echoue (timeout, erreur memoire)
  Then l'app affiche un message bienveillant : "Oups, cette photo est trop lourde. Essaie avec une photo plus petite."
  And l'utilisateur peut reprendre une photo ou annuler l'ajout
  And aucune plante n'est creee en base locale (transaction rollback)

**Edge cases a couvrir**
- Photo tres lourde (> 10 Mo, 4K) : compression avant stockage, gestion d'erreur si compression echoue
- Nom trop long (> 50 caracteres) : accepte en base, tronque a l'affichage
- Stockage local plein : message d'erreur clair, suggestion de liberer de l'espace
- Utilisateur quitte le flow d'ajout avant de confirmer : sauvegarde en brouillon
- Reprise du brouillon au retour : si brouillon existe, proposer de reprendre

**Depend de :** US-000, US-019

---

## F02 — Guide d'observation pour arrosage (Must)

### US-003 [Design] — Concevoir la carte visuelle interactive d'observation

**Feature source :** F02 — Guide d'observation pour arrosage
**Status :** Backlog
**Type :** Design
**Persona :** Lea, la debutante qui ne veut pas tuer ses plantes — ne sait pas quoi observer, arrose "au feeling"
**JTBD :** JTBD-F1 (Savoir quand arroser sans tuer ma plante), JTBD-F6 (Apprendre a observer mes plantes)

En tant que designer
Je veux concevoir une carte visuelle interactive avec 3 zones cliquables (terre, feuilles, pot) qui explique les gestes d'observation
Afin que Lea apprenne a observer sa plante avant d'arroser plutot que de suivre une frequence fixe

**Criteres d'acceptation**

Scenario : Happy path — Exploration des 3 zones d'observation
  Given je concois la carte visuelle d'une plante en pot
  When je structure les zones interactives
  Then la carte montre une illustration de plante avec 3 zones cliquables : terre (main qui touche), feuilles (oeil qui observe), pot (balance qui pese)
  And chaque zone s'ouvre sur un detail explicatif court (< 60 secondes de lecture)
  And le contenu utilise un langage simple, sans jargon botanique
  And des pictogrammes guident visuellement (main, oeil, balance)

Scenario : Premier usage — Decouverte guidee
  Given l'utilisateur n'a jamais vu le guide d'observation
  When il accede au guide pour la premiere fois
  Then un overlay leger pointe vers la premiere zone ("Commence par toucher la terre")
  And l'overlay disparait apres interaction ou apres 5 secondes
  And le guide ne bloque jamais l'interaction

Scenario : Contenu d'une zone — Detail "Toucher la terre"
  Given l'utilisateur clique sur la zone "terre"
  When le detail s'affiche
  Then l'explication montre : "Enfonce ton doigt a 3-4 cm. Si c'est sec, ta plante a probablement soif. Si c'est humide, attends encore."
  And une illustration ou video courte (15-30s) accompagne l'explication
  And un bouton "Compris !" ferme le detail

**Edge cases a couvrir**
- Plante sans pot (bouture dans l'eau) : adaptation du guide (zone "eau" remplace "terre")
- Ecran petit (< 320px) : zones restent cliquables, pas de chevauchement
- Utilisateur daltonien : ne pas s'appuyer uniquement sur la couleur pour les zones
- Geste swipe entre les zones pour navigation fluide
- Retour a la carte depuis un detail : geste swipe ou bouton retour

**Depend de :** US-001

---

### US-004 [Tech] — Implementer le contenu statique du guide d'observation

**Feature source :** F02 — Guide d'observation pour arrosage
**Status :** Backlog
**Type :** Tech
**Persona :** Lea, la debutante qui ne veut pas tuer ses plantes
**JTBD :** JTBD-F1, JTBD-F6

En tant que developpeur
Je veux implementer le guide d'observation avec contenu statique embarque (3 zones, textes, illustrations)
Afin que l'utilisateur puisse consulter le guide meme offline et apprendre les gestes d'observation

**Criteres d'acceptation**

Scenario : Happy path — Affichage du guide avec zones interactives
  Given l'utilisateur ouvre le guide d'observation depuis une fiche plante
  When le guide se charge
  Then les 3 zones (terre, feuilles, pot) sont affichees et cliquables
  And le contenu est charge depuis le stockage local (pas de requete reseau)
  And le temps de chargement est < 500ms

Scenario : Etat vide — Aucune plante ajoutee
  Given l'utilisateur n'a pas encore ajoute de plante
  When il tente d'acceder au guide d'observation
  Then l'app redirige vers l'ecran d'ajout de plante avec un message : "Ajoute ta premiere plante pour decouvrir le guide d'observation"

Scenario : Erreur — Contenu corrompu
  Given le contenu statique du guide est corrompu en local
  When le guide tente de se charger
  Then l'app affiche un message : "Le guide n'a pas pu se charger. Verifie ta connexion pour le retelecharger."
  And un bouton "Reessayer" tente de retelecharger le contenu

**Edge cases a couvrir**
- Contenu statique corrompu : detection d'integrite, retelechargement si connexion disponible
- Animations desactivees (mode economie d'energie) : fallback sur images statiques
- Lecteur d'ecran : textes alternatifs pour chaque zone et illustration
- Navigation clavier : toutes les zones accessibles au tab

**Depend de :** US-000, US-003

---

## F06 — Fiches plantes educatives (Must)

### US-005 [Design] — Concevoir les fiches plantes courtes et visuelles

**Feature source :** F06 — Fiches plantes educatives
**Status :** Backlog
**Type :** Design
**Persona :** Lea, la debutante qui ne veut pas tuer ses plantes — utilise TikTok/Instagram comme ressources principales, format court et visuel
**JTBD :** JTBD-F6 (Apprendre a observer mes plantes), JTBD-F1 (Savoir quand arroser)

En tant que designer
Je veux concevoir des fiches plantes au format court (60-90 secondes de lecture), visuelles et sans jargon
Afin que Lea comprenne les besoins de sa plante sans effort et developpe sa competence d'observation

**Criteres d'acceptation**

Scenario : Happy path — Fiche plante complete
  Given je concois une fiche pour une plante identifiee (ex: Monstera deliciosa)
  When je structure le contenu
  Then la fiche contient 4 sections : origine, lumiere, arrosage, signes de bonne sante
  And chaque section est lisible en 15-20 secondes max
  And le ton est bienveillant et pedagogique ("Ta Monstera vient des forets tropicales. Elle aime la lumiere indirecte.")
  And des icones visuelles accompagnent chaque section (soleil, goutte, coeur)
  And aucun terme botanique n'est utilise sans explication simple

Scenario : Plante non identifiee
  Given la plante n'a pas ete identifiee automatiquement
  When l'utilisateur consulte la fiche
  Then l'app affiche des conseils generiques d'observation ("Observe la terre, les feuilles, la lumiere")
  And propose d'identifier la plante via photo (lien vers identification)

Scenario : Contenu trop long
  Given un redacteur propose un texte de fiche > 200 mots
  When le texte depasse la limite
  Then le design impose une troncature a 200 mots avec un "En savoir plus" optionnel
  And le contenu principal reste lisible en 90 secondes

**Edge cases a couvrir**
- Plante non identifiee : conseils generiques + suggestion d'identification
- Plante rare sans fiche : message "On ne connait pas encore cette plante. Aide-nous a l'ajouter !"
- Mode sombre : contraste suffisant pour les icones et illustrations
- Accessibilite : textes alternatifs pour toutes les illustrations

**Depend de :** Aucune

---

### US-006 [Tech] — Implementer la base de fiches plantes embarquee

**Feature source :** F06 — Base de fiches plantes embarquee
**Status :** Backlog
**Type :** Tech
**Persona :** Lea, la debutante qui ne veut pas tuer ses plantes
**JTBD :** JTBD-F6, JTBD-F1

En tant que developpeur
Je veux implementer une base de fiches plantes embarquee (JSON/SQLite) avec les 50 plantes les plus courantes
Afin que l'utilisateur puisse consulter les fiches meme offline

**Criteres d'acceptation**

Scenario : Happy path — Consultation d'une fiche plante
  Given l'utilisateur a ajoute une plante identifiee comme "Monstera deliciosa"
  When il ouvre la fiche de sa plante
  Then la fiche s'affiche avec les 4 sections (origine, lumiere, arrosage, signes de bonne sante)
  And le contenu est charge depuis le stockage local
  And le temps de chargement est < 300ms

Scenario : Plante absente de la base
  Given l'utilisateur a ajoute une plante non presente dans la base embarquee
  When il ouvre la fiche
  Then l'app affiche un message : "On ne connait pas encore cette plante."
  And propose des conseils generiques d'observation
  And si connexion disponible, cherche la fiche sur le serveur

Scenario : Mise a jour de la base
  Given une nouvelle version de la base de fiches est disponible sur le serveur
  When l'app detecte la mise a jour (au lancement ou en background)
  Then la base locale est mise a jour silencieusement
  And l'utilisateur n'est pas interrompu

**Edge cases a couvrir**
- Base corrompue : reinitialisation depuis le bundle de l'app
- Espace disque insuffisant : avertissement sans bloquer l'usage
- Recherche par nom commun ET nom latin : correspondance floue (fuzzy matching)
- Mise a jour partielle interrompue : rollback a la version precedente

**Depend de :** US-000, US-019

---

### US-007 [Tech] — Implementer l'identification automatique via API

**Feature source :** F06 — Identification automatique via API
**Status :** Backlog
**Type :** Tech
**Persona :** Lea, la debutante qui ne veut pas tuer ses plantes
**JTBD :** JTBD-F6, JTBD-F1

En tant que developpeur
Je veux implementer l'identification automatique de plante par photo via une API externe (PlantNet ou similaire)
Afin que Lea puisse identifier sa plante sans connaitre son nom et acceder a la bonne fiche educative

**Criteres d'acceptation**

Scenario : Happy path — Identification reussie
  Given l'utilisateur prend une photo de sa plante
  When l'API retourne un resultat avec confiance > 70%
  Then l'app affiche le nom de la plante identifiee avec le score de confiance
  And propose de lier cette identification a la fiche plante
  And l'utilisateur peut confirmer ou corriger

Scenario : Identification incertaine
  Given l'API retourne un resultat avec confiance < 70%
  When l'app affiche le resultat
  Then l'app propose les 3 resultats les plus probables
  And l'utilisateur choisit le bon ou selectionne "Aucun de ces choix"
  And si "Aucun", la plante reste non identifiee avec conseils generiques

Scenario : Erreur — Pas de connexion
  Given l'utilisateur n'a pas de connexion internet
  When il tente d'identifier une plante par photo
  Then l'app affiche : "L'identification a besoin d'internet. Ta photo est sauvegardee, on identifiera ta plante des que la connexion reviendra."
  And la photo est stockee localement avec un flag "pending_identification"

**Edge cases a couvrir**
- Photo floue ou trop sombre : message "Essaie avec une photo plus nette et bien eclairee"
- Photo qui n'est pas une plante : message "On n'a pas reussi a trouver de plante sur cette photo"
- API indisponible (timeout, erreur serveur) : retry automatique (3 tentatives, backoff exponentiel)
- Rate limiting API : file d'attente locale, traitement differe
- Identification offline differee : sync automatique au retour de connexion

**Depend de :** US-000, US-006

---

## F09 — Onboarding (Must)

### US-008 [Design] — Concevoir l'onboarding ultra-court (< 60s)

**Feature source :** F09 — Onboarding
**Status :** Backlog
**Type :** Design
**Persona :** Lea, la debutante qui ne veut pas tuer ses plantes — 10/16 utilisateurs ont abandonne des apps a cause d'onboardings trop longs
**JTBD :** Transverse

En tant que designer
Je veux concevoir un onboarding en 3 ecrans maximum completable en moins de 60 secondes
Afin que Lea commence a utiliser l'app immediatement sans se sentir submergee par des configurations

**Criteres d'acceptation**

Scenario : Happy path — Onboarding en 3 ecrans
  Given l'utilisateur ouvre l'app pour la premiere fois
  When l'onboarding se lance
  Then l'ecran 1 explique en 1 phrase ce que fait l'app ("Apprends a observer tes plantes pour ne plus les tuer")
  And l'ecran 2 propose d'ajouter sa premiere plante (nom + photo optionnelle)
  And l'ecran 3 affiche la collection avec la plante ajoutee et un message de bienvenue
  And l'onboarding est completable en < 60 secondes
  And aucun compte n'est requis pour commencer

Scenario : Skip de l'onboarding
  Given l'utilisateur ne veut pas suivre l'onboarding
  When il clique sur "Passer" (visible sur chaque ecran)
  Then l'app le redirige directement vers l'ecran de collection (etat vide)
  And l'onboarding ne se relance jamais

Scenario : Premiere plante ajoutee pendant l'onboarding
  Given l'utilisateur ajoute une plante a l'ecran 2
  When il termine l'onboarding
  Then la plante apparait dans sa collection
  And un message de bienvenue s'affiche : "Bienvenue dans ta jungle !"

**Edge cases a couvrir**
- Utilisateur qui ferme l'app pendant l'onboarding : reprend a l'ecran ou il s'est arrete
- Retour arriere : possible entre les ecrans, pas de perte de donnees
- Accessibilite : navigation au clavier/lecteur d'ecran, contrastes suffisants
- Langue : textes courts, facilement traduisibles

**Depend de :** Aucune

---

### US-009 [Tech] — Implementer l'onboarding avec tracking et persistance

**Feature source :** F09 — Onboarding
**Status :** Backlog
**Type :** Tech
**Persona :** Lea, la debutante qui ne veut pas tuer ses plantes
**JTBD :** Transverse

En tant que developpeur
Je veux implementer le flow d'onboarding avec persistance d'etat et tracking de completion
Afin que l'onboarding ne se relance jamais apres completion et qu'on mesure le taux de completion

**Criteres d'acceptation**

Scenario : Happy path — Completion de l'onboarding
  Given l'utilisateur complete les 3 ecrans de l'onboarding
  When il arrive sur l'ecran de collection
  Then un flag "onboarding_completed: true" est sauvegarde en local
  And l'onboarding ne se relance plus jamais
  And un evenement analytics "onboarding_completed" est envoye avec le temps de completion

Scenario : Skip de l'onboarding
  Given l'utilisateur clique "Passer" a l'ecran 1 ou 2
  When il arrive sur la collection
  Then le flag "onboarding_skipped: true" est sauvegarde avec le numero de l'ecran de skip
  And un evenement analytics "onboarding_skipped" est envoye avec l'ecran de sortie
  And l'onboarding ne se relance plus

Scenario : Erreur — App fermee pendant l'onboarding
  Given l'utilisateur ferme l'app a l'ecran 2
  When il reouvre l'app
  Then l'onboarding reprend a l'ecran 2 (etat persiste)
  And les donnees saisies a l'ecran 2 (nom de plante) sont conservees

**Edge cases a couvrir**
- Reinstallation de l'app : l'onboarding se relance (donnees locales perdues)
- Migration de version : si le format d'onboarding change, ne pas relancer pour les utilisateurs existants
- Tracking offline : evenements analytics mis en file d'attente et envoyes au retour de connexion

**Depend de :** US-000

---

## F03 — Journal d'arrosage simplifie + rappels bienveillants (Should)

### US-010 [Design] — Concevoir l'historique visuel d'arrosage

**Feature source :** F03 — Journal d'arrosage simplifie
**Status :** Backlog
**Type :** Design
**Persona :** Lea, la debutante qui ne veut pas tuer ses plantes — arrose de facon irreguliere, a peur d'oublier
**JTBD :** JTBD-F1 (Savoir quand arroser sans tuer ma plante), JTBD-F6 (Apprendre a observer)

En tant que designer
Je veux concevoir un historique visuel d'arrosage avec un bouton "J'ai arrose" en un tap
Afin que Lea puisse voir en un coup d'oeil quand elle a arrose pour la derniere fois et se rassurer

**Criteres d'acceptation**

Scenario : Happy path — Enregistrement d'un arrosage
  Given je concois l'interaction d'enregistrement d'arrosage
  When l'utilisateur ouvre la fiche d'une plante
  Then un bouton "J'ai arrose" est visible et accessible en un tap
  And apres le tap, une animation douce confirme l'enregistrement (goutte d'eau, checkmark)
  And l'historique affiche "Dernier arrosage : aujourd'hui"

Scenario : Historique visuel — Timeline
  Given l'utilisateur a enregistre plusieurs arrosages
  When il consulte l'historique
  Then une timeline visuelle montre les arrosages passes (points sur une frise)
  And l'intervalle entre chaque arrosage est visible ("il y a 3 jours", "il y a 10 jours")
  And pas de jugement : aucun code couleur rouge/vert, juste de l'information

Scenario : Etat vide — Aucun arrosage enregistre
  Given l'utilisateur n'a jamais enregistre d'arrosage pour cette plante
  When il consulte la fiche plante
  Then un message bienveillant s'affiche : "Tu n'as pas encore enregistre d'arrosage. Appuie quand tu arroses !"
  And le bouton "J'ai arrose" est bien visible

**Edge cases a couvrir**
- Double tap accidentel : debounce de 2 secondes, possibilite d'annuler dans les 5 secondes
- Arrosage enregistre par erreur : bouton "Annuler" disponible pendant 5 secondes apres le tap
- Historique tres long (> 100 arrosages) : pagination ou scroll infini
- Plusieurs plantes arrosees en meme temps : bouton "Arroser toutes" depuis la collection

**Depend de :** US-001

---

### US-011 [Design] — Concevoir le systeme de rappels bienveillants (opt-in)

**Feature source :** F03 — Rappels bienveillants (opt-in)
**Status :** Backlog
**Type :** Design
**Persona :** Lea, la debutante qui a peur d'oublier — Sophie, la passionnee qui a une routine structuree
**JTBD :** JTBD-F1 (Savoir quand arroser), JTBD-F6 (Apprendre a observer)

En tant que designer
Je veux concevoir un systeme de rappels bienveillants opt-in (max 1/semaine par plante, ton educatif)
Afin que Lea soit guidee vers l'observation sans etre spammee ni dependante des notifications

**Criteres d'acceptation**

Scenario : Happy path — Activation des rappels
  Given l'utilisateur consulte la fiche d'une plante
  When il active le toggle "Rappels bienveillants"
  Then un message explique : "Tu recevras max 1 rappel par semaine pour cette plante. On t'invitera a observer, pas a arroser."
  And le toggle est clairement opt-in (desactive par defaut)
  And la frequence max est affichee (1/semaine)

Scenario : Notification recue — Ton educatif
  Given les rappels sont actives pour "Mon Monstera"
  When 7 jours se sont ecoules depuis le dernier arrosage
  Then la notification dit : "Il y a 7 jours que tu n'as pas arrose ton Monstera. Va toucher la terre pour verifier si elle en a besoin."
  And la notification ne dit jamais "Arrose maintenant !" ni "Tu as oublie !"
  And le ton est bienveillant et educatif

Scenario : Desactivation des rappels
  Given l'utilisateur veut desactiver les rappels
  When il desactive le toggle
  Then les rappels s'arretent immediatement
  And un message confirme : "C'est note, plus de rappels pour cette plante."

**Edge cases a couvrir**
- Permissions de notification refusees par l'OS : message explicatif + lien vers les reglages
- Trop de plantes avec rappels actifs (> 10) : regrouper les notifications en une seule ("3 de tes plantes attendent une petite visite")
- Arrosage enregistre juste avant un rappel : annuler le rappel prevu
- Mode "Ne pas deranger" : respecter les plages horaires de l'OS

**Depend de :** US-010

---

### US-012 [Tech] — Implementer l'enregistrement d'arrosage et les notifications push opt-in

**Feature source :** F03 — Journal d'arrosage + rappels
**Status :** Backlog
**Type :** Tech
**Persona :** Lea, Sophie
**JTBD :** JTBD-F1, JTBD-F6

En tant que developpeur
Je veux implementer l'enregistrement d'arrosage en un tap avec stockage local et notifications push opt-in
Afin que l'utilisateur puisse suivre ses arrosages et recevoir des rappels bienveillants s'il le souhaite

**Criteres d'acceptation**

Scenario : Happy path — Enregistrement d'arrosage
  Given l'utilisateur appuie sur "J'ai arrose" sur la fiche d'une plante
  When l'evenement est enregistre
  Then un enregistrement est cree en local : plant_id, timestamp, type="watering"
  And l'historique est mis a jour immediatement (affichage optimiste)
  And si rappels actifs, le prochain rappel est recalcule (dernier arrosage + 7 jours)

Scenario : Notifications push opt-in
  Given l'utilisateur active les rappels pour une plante
  When 7 jours se sont ecoules depuis le dernier arrosage
  Then une notification push est envoyee avec le message bienveillant
  And la notification est limitee a max 1 par plante par semaine
  And si plus de 3 plantes doivent etre rappelees le meme jour, regrouper en une seule notification

Scenario : Erreur — Permission de notification refusee
  Given l'utilisateur active les rappels mais l'OS refuse les permissions
  When l'app detecte le refus
  Then un message explique comment activer les notifications dans les reglages
  And le toggle reste desactive visuellement
  And aucune notification n'est planifiee

**Edge cases a couvrir**
- Annulation d'arrosage (undo) : suppression de l'enregistrement dans les 5 secondes
- Arrosage multiple le meme jour : accepte, affiche tous les enregistrements
- Changement de fuseau horaire : recalcul des rappels
- Synchronisation des arrosages entre appareils : resolution par timestamp (last write wins)

**Depend de :** US-000, US-010, US-019

---

## F04 — Scan visuel + diagnostic (Should)

### US-013 [Design] — Concevoir l'ecran de scan et etats

**Feature source :** F04 — Scan visuel + diagnostic
**Status :** Backlog
**Type :** Design
**Persona :** Lea, la debutante inquiete — Sophie, la passionnee qui veut identifier les problemes tot
**JTBD :** JTBD-F2 (Identifier ce qui ne va pas avant qu'il soit trop tard)

En tant que designer
Je veux concevoir l'ecran de prise de photo pour diagnostic avec les differents etats (chargement, resultat, erreur)
Afin que l'utilisateur sache exactement quoi photographier et comprenne le resultat

**Criteres d'acceptation**

Scenario : Happy path — Prise de photo guidee
  Given l'utilisateur ouvre le scan diagnostic
  When l'ecran de capture s'affiche
  Then un guide visuel montre quoi cadrer ("Cadre la feuille qui t'inquiete, bien eclairee")
  And un bouton de capture est bien visible et large (tactile)
  And apres la capture, un ecran de chargement anime s'affiche ("Analyse en cours...")

Scenario : Etat de chargement — Analyse en cours
  Given l'utilisateur a pris une photo
  When l'analyse est en cours
  Then une animation apaisante s'affiche (pas de spinner stressant)
  And un message rassurant : "On regarde ca de pres..."
  And un temps estime est affiche si disponible

Scenario : Erreur — Photo inutilisable
  Given l'utilisateur a pris une photo floue ou trop sombre
  When l'API ne peut pas analyser
  Then un message bienveillant : "On n'arrive pas a bien voir. Essaie avec plus de lumiere et en te rapprochant de la feuille."
  And l'utilisateur peut reprendre une photo immediatement
  And la photo ratee n'est pas sauvegardee

**Edge cases a couvrir**
- Camera non disponible (permissions refusees) : explication + lien vers les reglages
- Photo depuis la galerie (au lieu de la camera) : supporter les deux modes
- Ecran de chargement trop long (> 10s) : message "Ca prend un peu plus de temps que prevu..."
- Plusieurs photos pour un meme diagnostic : galerie de selection

**Depend de :** Aucune

---

### US-014 [Design] — Concevoir le resultat diagnostic et feedback utilisateur

**Feature source :** F04 — Resultat diagnostic et feedback
**Status :** Backlog
**Type :** Design
**Persona :** Lea, la debutante inquiete — Sophie, la passionnee qui veut des protocoles precis
**JTBD :** JTBD-F2 (Identifier ce qui ne va pas avant qu'il soit trop tard)

En tant que designer
Je veux concevoir l'ecran de resultat diagnostic avec le probleme identifie, le niveau de confiance et le protocole de traitement
Afin que l'utilisateur comprenne ce qui ne va pas et sache quoi faire concretement

**Criteres d'acceptation**

Scenario : Happy path — Diagnostic avec haute confiance
  Given l'API retourne un diagnostic avec confiance > 80%
  When l'ecran de resultat s'affiche
  Then le probleme identifie est affiche clairement (ex: "Sur-arrosage probable")
  And une explication courte en langage simple (pas de jargon)
  And un protocole de traitement en etapes numerotees ("1. Laisse secher la terre. 2. Espace les arrosages. 3. Observe dans 5 jours.")
  And un bouton "Ce diagnostic est-il utile ?" (feedback)

Scenario : Diagnostic incertain — Confiance < 60%
  Given l'API retourne un diagnostic avec confiance < 60%
  When l'ecran de resultat s'affiche
  Then l'app affiche : "On n'est pas surs a 100%. Voici les possibilites les plus probables :"
  And les 2-3 diagnostics possibles sont listes avec leur probabilite
  And l'utilisateur peut choisir celui qui lui semble le plus juste

Scenario : Plante en bonne sante
  Given l'API ne detecte aucun probleme
  When l'ecran de resultat s'affiche
  Then un message positif : "Ta plante a l'air en pleine forme ! Continue comme ca."
  And des conseils preventifs sont proposes

**Edge cases a couvrir**
- Diagnostic contradictoire : afficher les deux avec explication
- Probleme grave (parasite, maladie avancee) : ton rassurant mais action urgente suggeree
- Historique des diagnostics : pouvoir revoir les anciens diagnostics d'une plante
- Feedback utilisateur negatif : proposer de reprendre une photo ou de signaler une erreur

**Depend de :** US-013

---

### US-015 [Tech] — Implementer la compression et l'envoi photo

**Feature source :** F04 — Compression et envoi photo
**Status :** Backlog
**Type :** Tech
**Persona :** Lea, Sophie
**JTBD :** JTBD-F2

En tant que developpeur
Je veux implementer la capture photo, compression et envoi vers l'API de diagnostic
Afin que l'analyse soit rapide meme avec une connexion lente

**Criteres d'acceptation**

Scenario : Happy path — Capture et envoi
  Given l'utilisateur prend une photo pour diagnostic
  When la photo est capturee
  Then la photo est compressee (max 500 Ko, qualite 85%, resolution max 1280x960)
  And la photo est envoyee a l'API de diagnostic via HTTPS
  And un indicateur de progression s'affiche pendant l'envoi

Scenario : Connexion lente — Upload long
  Given l'utilisateur est en 3G ou connexion faible
  When l'envoi prend plus de 5 secondes
  Then un message s'affiche : "La connexion est un peu lente, on continue l'envoi..."
  And l'envoi continue en background si l'utilisateur quitte l'ecran
  And une notification locale informe quand le resultat est pret

Scenario : Erreur — Pas de connexion
  Given l'utilisateur n'a pas de connexion internet
  When il tente d'envoyer la photo
  Then l'app sauvegarde la photo localement avec un flag "pending_diagnosis"
  And affiche : "Pas de connexion. Ta photo est sauvegardee, on lancera l'analyse des que la connexion reviendra."

**Edge cases a couvrir**
- Photo depuis la galerie : supporter les formats JPEG, PNG, HEIC
- Compression echouee : fallback sur la photo originale si < 2 Mo
- Envoi interrompu : retry automatique (3 tentatives, backoff exponentiel)
- Quota API depasse : message "On a atteint la limite d'analyses pour aujourd'hui. Reessaie demain."

**Depend de :** US-000, US-013

---

### US-016 [Tech] — Implementer l'integration API diagnostic

**Feature source :** F04 — Integration API diagnostic
**Status :** Backlog
**Type :** Tech
**Persona :** Lea, Sophie
**JTBD :** JTBD-F2

En tant que developpeur
Je veux implementer l'integration avec l'API de diagnostic visuel (analyse de photo, retour de resultats structures)
Afin que l'utilisateur recoive un diagnostic fiable avec un protocole de traitement

**Criteres d'acceptation**

Scenario : Happy path — Diagnostic reussi
  Given l'API recoit une photo valide
  When l'API retourne un resultat
  Then l'app parse la reponse : probleme identifie, score de confiance, protocole de traitement
  And le resultat est sauvegarde en local (historique des diagnostics par plante)
  And le resultat est affiche a l'utilisateur selon le design (US-014)

Scenario : API indisponible — Timeout
  Given l'API ne repond pas dans les 15 secondes
  When le timeout est atteint
  Then l'app affiche : "Le diagnostic prend trop de temps. Verifie ta connexion et reessaie."
  And la photo est conservee localement pour retry
  And un bouton "Reessayer" est propose

Scenario : Erreur API — Reponse invalide
  Given l'API retourne une reponse malformee ou un code d'erreur
  When l'app parse la reponse
  Then l'app affiche : "Oups, quelque chose n'a pas fonctionne. Reessaie dans quelques minutes."
  And l'erreur est loguee pour monitoring
  And la photo est conservee pour retry

**Edge cases a couvrir**
- Reponse API avec plusieurs diagnostics possibles : afficher les top 3 tries par confiance
- Mise a jour de l'API (changement de format) : versioning de l'integration, fallback gracieux
- Cache des resultats : ne pas re-analyser la meme photo si resultat recent (< 1h)
- Rate limiting : file d'attente locale, traitement differe

**Depend de :** US-000, US-015

---

### US-017 [Tech] — Implementer la gestion des erreurs et fallback offline

**Feature source :** F04 — Gestion erreurs et fallback offline
**Status :** Backlog
**Type :** Tech
**Persona :** Lea, Sophie
**JTBD :** JTBD-F2

En tant que developpeur
Je veux implementer une gestion d'erreurs robuste et un mode degrade offline pour le diagnostic
Afin que l'utilisateur ne soit jamais bloque et comprenne toujours ce qui se passe

**Criteres d'acceptation**

Scenario : Happy path — Mode degrade offline
  Given l'utilisateur n'a pas de connexion
  When il tente un diagnostic
  Then l'app sauvegarde la photo et affiche : "Diagnostic en attente de connexion. En attendant, voici des conseils d'observation generaux."
  And des conseils generiques sont affiches (issus de la base locale)
  And des que la connexion revient, le diagnostic est lance automatiquement

Scenario : Erreurs reseau intermittentes
  Given la connexion est instable
  When un envoi echoue
  Then l'app retente automatiquement (3 tentatives, backoff exponentiel : 1s, 2s, 4s)
  And apres 3 echecs, l'app passe en mode degrade (sauvegarde locale + retry ulterieur)
  And l'utilisateur est informe : "On reessaiera automatiquement plus tard."

Scenario : Erreur critique — Crash de l'analyse
  Given une erreur inattendue survient pendant l'analyse
  When l'app detecte le crash
  Then l'app ne crash pas (catch global)
  And un message s'affiche : "Quelque chose s'est mal passe. Ta photo est sauvegardee, reessaie plus tard."
  And l'erreur est loguee pour monitoring

**Edge cases a couvrir**
- File d'attente de diagnostics offline : traitement FIFO au retour de connexion
- Notification quand un diagnostic offline est pret : notification locale
- Nettoyage des photos en attente (> 30 jours) : suppression avec avertissement
- Espace disque critique : prioriser les diagnostics en attente

**Depend de :** US-000, US-015, US-016

---

## F10 — Fonctionnement offline (Should)

### US-019 [Tech] — Implementer le stockage local et les service workers

**Feature source :** F10 — Stockage local et service workers
**Status :** Backlog
**Type :** Tech
**Persona :** Lea, Sophie — utilisatrices en mobilite (magasin de plantes, jardin, transports)
**JTBD :** Transverse

En tant que developpeur
Je veux implementer le stockage local (IndexedDB/SQLite) et les service workers pour le cache offline
Afin que l'app fonctionne sans connexion internet pour les operations de base

**Criteres d'acceptation**

Scenario : Happy path — App utilisable offline
  Given l'utilisateur a deja utilise l'app en ligne au moins une fois
  When il perd la connexion internet
  Then l'app reste fonctionnelle : consultation de la collection, ajout de plante, consultation des fiches, enregistrement d'arrosage
  And les donnees sont sauvegardees en local
  And un indicateur discret montre "Mode hors ligne"

Scenario : Premier lancement sans connexion
  Given l'utilisateur installe l'app (PWA) et n'a pas de connexion
  When il ouvre l'app pour la premiere fois
  Then l'app charge le shell applicatif et les ressources embarquees
  And les fiches plantes de base (top 50) sont disponibles
  And les fonctions necessitant une API (identification, diagnostic) affichent un etat degrade

Scenario : Erreur — Stockage local plein
  Given le stockage local est plein
  When l'utilisateur tente de sauvegarder des donnees
  Then l'app affiche : "L'espace de stockage est plein. Libere de l'espace pour continuer."
  And les donnees existantes ne sont pas corrompues
  And les operations de lecture restent fonctionnelles

**Edge cases a couvrir**
- Quota IndexedDB depasse : nettoyage des caches non essentiels en priorite
- Service worker non supporte (navigateur ancien) : fallback online-only avec avertissement
- Mise a jour du service worker : activation silencieuse au prochain lancement
- Corruption de la base IndexedDB : detection et reinitialisation depuis le serveur

**Depend de :** US-000

---

### US-020 [Tech] — Implementer la detection de connexion et la synchronisation automatique

**Feature source :** F10 — Detection connexion et sync auto
**Status :** Backlog
**Type :** Tech
**Persona :** Lea, Sophie
**JTBD :** Transverse

En tant que developpeur
Je veux implementer la detection de connexion et la synchronisation automatique des donnees en attente
Afin que les donnees creees offline soient synchronisees des que la connexion revient

**Criteres d'acceptation**

Scenario : Happy path — Retour de connexion
  Given l'utilisateur a cree des donnees offline (plantes, arrosages)
  When la connexion internet revient
  Then l'app detecte le retour de connexion automatiquement
  And les donnees en attente sont synchronisees en background (pas de blocage UI)
  And un indicateur discret montre "Synchronisation en cours..."
  And une fois termine : "Tout est a jour"

Scenario : Connexion intermittente
  Given la connexion est instable (Wi-Fi faible, metro)
  When l'app detecte des coupures frequentes
  Then l'app ne tente pas de synchroniser a chaque micro-reconnexion
  And un debounce de 5 secondes est applique avant de lancer la sync
  And les operations de sync echouees sont remises en file d'attente

Scenario : Erreur — Sync echouee
  Given la synchronisation echoue (erreur serveur, timeout)
  When l'app detecte l'echec
  Then les donnees restent en local et marquees "pending_sync"
  And l'app retente automatiquement (backoff exponentiel : 30s, 1m, 5m)
  And apres 5 echecs consecutifs, un message discret : "La synchronisation ne fonctionne pas. Tes donnees sont en securite en local."

**Edge cases a couvrir**
- Passage Wi-Fi vers 4G : ne pas relancer la sync si deja en cours
- Mode avion active : ne pas tenter de synchroniser
- Donnees conflictuelles (meme plante modifiee sur 2 appareils) : last write wins par timestamp
- Volume important a synchroniser : pagination et priorisation (plantes > arrosages > diagnostics)

**Depend de :** US-000, US-019

---

### US-021 [Tech] — Implementer la synchronisation en background avec gestion des conflits

**Feature source :** F10 — Synchronisation en background
**Status :** Backlog
**Type :** Tech
**Persona :** Lea, Sophie
**JTBD :** Transverse

En tant que developpeur
Je veux implementer la synchronisation en background via Background Sync API avec resolution de conflits
Afin que les donnees soient synchronisees meme si l'app est fermee

**Criteres d'acceptation**

Scenario : Happy path — Sync en background
  Given l'utilisateur a des donnees en attente de sync
  When l'app est fermee et la connexion revient
  Then le service worker detecte le retour de connexion
  And les donnees en attente sont synchronisees en background
  And une notification locale informe : "Tes donnees ont ete synchronisees"

Scenario : Conflit de donnees — Meme plante modifiee sur 2 appareils
  Given la meme plante a ete modifiee offline sur 2 appareils
  When les deux appareils se synchronisent
  Then la strategie "last write wins" est appliquee (comparaison des timestamps)
  And la version avec le timestamp le plus recent est conservee
  And la version perdante est archivee (pas supprimee) pour recuperation manuelle

Scenario : Erreur — Background Sync non supporte
  Given le navigateur ne supporte pas Background Sync API
  When l'utilisateur ferme l'app avec des donnees en attente
  Then les donnees sont synchronisees au prochain lancement de l'app
  And un message informe : "Certaines donnees n'ont pas encore ete synchronisees."

**Edge cases a couvrir**
- Suppression d'une plante offline sur un appareil et modification sur un autre : garder la modification
- Sync partielle interrompue : reprise la ou elle s'est arretee
- Batterie faible : ne pas lancer de sync en background si batterie < 15%
- Taille des donnees > 10 Mo : compression avant envoi

**Depend de :** US-000, US-019, US-020

---

### US-022 [Design] — Concevoir les etats degrades offline

**Feature source :** F10 — Etats degrades offline
**Status :** Backlog
**Type :** Design
**Persona :** Lea, la debutante qui ne comprend pas les erreurs techniques — Sophie, la passionnee en mobilite
**JTBD :** Transverse

En tant que designer
Je veux concevoir les etats degrades de l'app quand certaines fonctionnalites ne sont pas disponibles offline
Afin que l'utilisateur comprenne ce qui marche et ce qui ne marche pas sans etre frustre

**Criteres d'acceptation**

Scenario : Happy path — Indicateur offline discret
  Given l'utilisateur perd la connexion
  When l'app passe en mode offline
  Then un indicateur discret apparait (barre fine en haut, pas de popup bloquant)
  And le message est rassurant : "Mode hors ligne — tes donnees sont en securite"
  And les fonctionnalites disponibles restent pleinement accessibles

Scenario : Fonctionnalite indisponible — Diagnostic offline
  Given l'utilisateur tente un diagnostic sans connexion
  When l'ecran de diagnostic s'affiche
  Then un message clair : "Le diagnostic a besoin d'internet. Ta photo sera analysee des que la connexion reviendra."
  And un bouton "Prendre la photo quand meme" est propose (sauvegarde locale)
  And des conseils d'observation generaux sont proposes en attendant

Scenario : Retour de connexion — Transition fluide
  Given l'utilisateur retrouve la connexion
  When l'app detecte le retour
  Then l'indicateur offline disparait avec une animation douce
  And un message ephemere : "Connexion retrouvee ! Synchronisation en cours..."
  And les fonctionnalites redeviennent disponibles progressivement

**Edge cases a couvrir**
- Connexion tres lente (< 100 kbps) : traiter comme offline pour les operations lourdes
- Offline prolonge (> 24h) : pas de message alarmiste, juste "Tes donnees sont en securite en local"
- Premiere utilisation offline : experience minimale mais fonctionnelle
- Transition rapide online/offline (metro) : pas de clignotement de l'indicateur (debounce 3s)

**Depend de :** US-019

---

## Matrice de couverture

| Persona | US associees |
|---------|-------------|
| Lea | US-000 a US-022 (toutes) |
| Sophie | US-010 a US-022 |

## Points d'attention pour le design
- Ton bienveillant et non-jugeant sur TOUS les ecrans (principe transversal JTBD-E1)
- Mobile-first : bottom nav, gestes swipe, format court et visuel
- Etats vides accueillants (jamais de "Aucun resultat" sec)
- Messages d'erreur sans les mots "erreur", "invalide", "obligatoire"
- Accessibilite : contrastes, lecteur d'ecran, navigation clavier

## Points d'attention pour le dev
- Architecture offline-first : stockage local prioritaire, sync en background
- Setup technique (US-000) est prerequis a toutes les US Tech
- Dependances : US-019 (stockage local) est prerequis pour US-002, US-006, US-012, US-020, US-021
- API externes : identification (PlantNet), diagnostic (a definir) — gestion des etats degrades critique
- Compression photo : max 1 Mo pour stockage, max 500 Ko pour envoi API
- Notifications push : opt-in explicite, max 1/semaine/plante, regroupement si > 3 plantes
