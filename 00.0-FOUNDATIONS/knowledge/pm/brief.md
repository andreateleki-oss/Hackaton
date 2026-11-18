# Brief produit — Application de suivi de plantes d'intérieur

> Statut : VALIDE
> Date : 2026-07-03
> Source UXR : knowledge/uxr/outputs/

## Le probleme

Le brief utilisateur identifie trois problèmes centraux : suivre l'hydratation des plantes, identifier les maladies, vérifier l'état de santé. Ces trois problèmes sont validés par la donnée UXR :

- **Sur-arrosage comme erreur récurrente** : 13/16 interviewés (synthese.md, thème 1) — "Mes clients tuent leurs plantes par excès d'amour — trop d'arrosage, toujours."
- **Difficulté d'identification des maladies** : 11/16 interviewés (synthese.md, thème 2) — "Je vois des taches sur les feuilles et je ne sais jamais si c'est un champignon, un manque de nutriments ou une brûlure."
- **Besoin d'apprendre à observer** : 13/16 interviewés (synthese.md, thème 10) — "Observer chaque jour. C'est comme ça qu'on apprend à lire une plante."

Ces trois problèmes mappent directement sur les JTBD critiques F1, F2 et F6.

## Pour qui

### Personas prioritaires pour v1

**Persona prioritaire : Léa (débutante)**

Justification :
- 5/16 interviewés correspondent à ce profil (Lucie, Hugo, Romain, Thomas, Charlotte)
- Les trois JTBD choisis (hydratation, diagnostic, observation) sont critiques pour ce segment
- C'est le segment qui abandonne massivement les apps existantes (10/16 — synthese.md, thème 3) car trop complexes
- Fort potentiel de différenciation sur la simplicité radicale (synthese.md, thème 8)

**Persona secondaire : Sophie (passionnée)**

Justification :
- 4/16 interviewés (Sophie, Claire, Amandine, Isabelle)
- Recherche d'expertise fiable (synthese.md, thème 2) — "Je paierais facilement 20€/an pour du vrai diagnostic"
- Dimension communautaire forte (9/16 — JTBD-S1)
- Disposition à payer pour de la valeur (synthese.md, thème 12)

**NON COUVERT EN V1 : Jean (collectionneur)**

Raison : besoins trop spécifiques (données taxonomiques, API vers bases botaniques, granularité par sous-espèce) incompatibles avec un MVP mobile-first pour débutants/intermédiaires.

## JTBD couverts

| JTBD | Couvert par le brief | Commentaire |
|------|---------------------|-------------|
| **JTBD-F1** : Savoir quand arroser sans tuer ma plante | Oui | Brief mentionne "suivre l'hydratation" |
| **JTBD-F2** : Identifier ce qui ne va pas avant qu'il soit trop tard | Oui | Brief mentionne "identifier les maladies" |
| **JTBD-F6** : Apprendre à observer mes plantes | Oui | Brief mentionne "vérifier l'état de santé" |
| **JTBD-F3** : Partir en vacances sans tuer mes plantes | **NON** | 14/16 interviewés — hors scope v1 (confirmé) |
| **JTBD-F4** : Choisir une plante compatible avec mon logement | **NON** | 8/16 interviewés — hors scope v1 |
| **JTBD-E1** : Me sentir responsable sans être jugé | **NON** | 9/16 interviewés — dimension émotionnelle absente |
| **JTBD-S1** : Appartenir à une communauté | **NON** | 9/16 interviewés — hors scope v1 |

Le brief couvre volontairement 3 JTBD sur 6 pour v1. JTBD-F3 (vacances), bien que mentionné par 14/16 utilisateurs, est explicitement hors scope v1.

## Cible plateforme

**Webapp mobile-first** (confirmé par l'utilisateur)

Justification :
- Alignement avec le comportement du persona prioritaire Léa (TikTok, Instagram, formats courts)
- 6/16 utilisateurs < 30 ans privilégient les formats courts et visuels sur mobile (synthese.md, thème 15)
- "J'ai pas besoin d'une appli complexe. Juste un guide simple pour pas tuer mes plantes. En mode TikTok — court, visuel, pas de jargon." (Hugo, entretien_Hugo_L.docx)
- Cohérence avec le principe de simplicité radicale (synthese.md, thème 8)

## Ce que le produit fait

Une webapp qui aide les utilisateurs débutants et intermédiaires à :

1. **Comprendre quand arroser leurs plantes** sans suivre une fréquence fixe arbitraire, en apprenant à lire les signaux réels de la plante (toucher la terre, observer les feuilles).
2. **Diagnostiquer visuellement les problèmes** (maladies, parasites, carences) avant qu'il ne soit trop tard, avec identification fiable et protocoles de traitement.
3. **Développer leur capacité d'observation** pour devenir autonomes progressivement et ne plus dépendre d'un système externe.

Le produit **éduque à l'observation** plutôt que de remplacer l'observation par des automatismes. Il **accompagne le développement de compétence** plutôt que de créer une dépendance à la notification.

## Ce que le produit ne fait PAS (hors scope v1)

- **Pas de notifications push d'arrosage automatiques** (synthese.md, thème 3 — 10/16 ont abandonné des apps à cause de ça)
- **Pas de données taxonomiques pour collectionneurs** (segment Jean non couvert en v1)
- **Pas de gestion de vacances** [A DECIDER — voir JTBD-F3]
- **Pas de fonctionnalité communautaire** [A DECIDER — voir JTBD-S1]
- **Pas d'aide au choix de plante avant achat** [A DECIDER — voir JTBD-F4]
- **Pas de mode jardin extérieur** (segment jardiniers anciens non couvert)
- **Pas d'app mobile native** (webapp mobile-first responsive)

## Hypotheses non verifiees

| Hypothèse | Source | Validée par UXR ? | Commentaire |
|-----------|--------|-------------------|-------------|
| Les utilisateurs veulent une webapp mobile-first | Brief utilisateur | **OUI** | Aligné avec donnée UXR (segment jeune débutant utilise mobile/TikTok) |
| Les utilisateurs veulent prioritairement suivre l'hydratation | Brief utilisateur | **OUI** | JTBD-F1 = 16/16 interviewés |
| Les utilisateurs veulent identifier les maladies | Brief utilisateur | **OUI** | JTBD-F2 = 11/16 interviewés |
| Les utilisateurs veulent vérifier l'état de santé | Brief utilisateur | **OUI** | JTBD-F6 = 13/16 interviewés |
| Les 3 JTBD choisis suffisent pour une v1 viable | Brief utilisateur | **OUI** | JTBD-F3 (vacances) hors scope v1 par choix |

## Différenciation vs apps existantes

Axes de différenciation validés (vs Planta, Greg, Happy Plant, Bloomify) :

1. **Pas de notifications spam** (pain point majeur — 10/16 ont abandonné pour cette raison)
2. **Onboarding minimal** (synthese.md, thème 8 — "Je voudrais juste un truc qui me dise quand faire quoi, sans que j'aie à tout configurer")
3. **Focus sur l'éducation à l'observation** plutôt que dépendance à l'app (synthese.md, thème 10)
4. **Diagnostic visuel fiable** comme différenciateur premium (synthese.md, thème 12 — disposition à payer pour de l'expertise)
5. **Ton bienveillant et non-jugeant** (synthese.md, thème 8 — "j'ai besoin qu'on me guide sans me juger si je rate")

## Criteres de reussite

**Critères fonctionnels :**
- L'utilisateur peut diagnostiquer un problème (feuilles jaunes, taches) en moins de 2 minutes
- L'utilisateur comprend quand arroser sans compter les jours (observation de la terre, signaux de la plante)
- L'utilisateur complète l'onboarding en moins de 60 secondes

**Critères de rétention :**
- Pas d'abandon pour cause de notifications spam (taux de désactivation notifs < 10%)
- Retour hebdomadaire sans dépendance quotidienne (engagement != dépendance)

**Critères émotionnels :**
- L'utilisateur se sent accompagné, pas jugé (ton bienveillant)
- L'utilisateur ressent une progression de compétence (JTBD-E2)

## Prochaines etapes

1. **Lancer le feature-breakdown** — découper en 10 features max basées sur les JTBD validés F1, F2, F6
