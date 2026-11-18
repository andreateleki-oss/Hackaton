---
name: brief-challenge
description: Challenge le brief utilisateur en le confrontant aux livrables UXR (synthese, JTBD, personas). Produit un brief.md validé. Ne demarre jamais sans brief utilisateur.
---

# Skill — brief-challenge

## Pre-requis

1. **L'utilisateur doit avoir pose son brief.** Si aucun brief n'est donne, demander :
   > "Decris-moi ton projet en quelques phrases : quel probleme tu veux resoudre, pour qui, et pourquoi maintenant."

2. **Livrables UXR disponibles** :
   - `knowledge/uxr/outputs/synthese.md`
   - `knowledge/uxr/outputs/jobs-to-be-done.md`
   - `knowledge/uxr/outputs/personas.md`

   Si un livrable manque, bloquer :
   > "Il manque [fichier]. Lance `@uxr` d'abord — je ne challenge pas un brief sans donnee terrain."

## Methode

### 1. Lire le brief utilisateur

Ne pas reformuler, ne pas completer. Noter les affirmations cles du brief.

### 2. Charger les livrables UXR

Lire synthese.md, jobs-to-be-done.md, personas.md. En extraire :
- Les 3-5 pain points les plus frequents (avec frequence X/16)
- Les JTBD prioritaires
- Les personas et leurs frustrations cles

### 3. Confronter le brief a la donnee

Pour chaque affirmation du brief, verifier :
- **Alignement JTBD** : le brief repond-il a un job identifie ? Lequel ?
- **Couverture personas** : le brief parle de qui ? Tous les personas sont couverts ? Un est oublie ?
- **Coherence synthese** : le brief contredit-il un constat terrain ? (ex: "les users veulent des rappels" vs synthese qui dit le contraire)

Formuler les challenges sous forme de questions directes :
> "Ton brief dit [X]. Mais les entretiens montrent [Y] (source). Comment tu reconcilies ca ?"
> "Tu ne mentionnes pas [persona/JTBD]. C'est un choix delibere ou un oubli ?"
> "Tu pars du principe que [hypothese]. Les entretiens ne confirment pas ca — [evidence]. On garde quand meme ?"

### 4. Cadrer la cible plateforme

Poser la question :
> "Ce produit, c'est quoi concretement ? App mobile, app desktop, site web responsive, les trois ? Ca impacte directement le scope des features."

Ne pas decider a la place de l'utilisateur. Documenter le choix.

### 5. Produire le brief consolide

Une fois les challenges traites et les reponses integrees, rediger le brief.md et le soumettre :
> "Voila le brief consolide. Qu'est-ce qui est faux ou manquant ?"

Ne pas passer au feature-breakdown sans validation explicite.

## Livrable

`knowledge/pm/brief.md` :

```markdown
# Brief produit — [Nom du projet]
> Statut : [A VALIDER]
> Date : YYYY-MM-DD
> Source UXR : knowledge/uxr/outputs/

## Le probleme
[Reformulation du probleme, ancree dans la donnee UXR]

## Pour qui
[Personas cibles — reference directe aux personas UXR]

## JTBD couverts
| JTBD | Couvert par le brief | Commentaire |
|------|---------------------|-------------|
| JTBD-F1 | Oui / Partiellement / Non | ... |

## Cible plateforme
[Mobile / Desktop / Responsive / PWA — choix utilisateur]

## Ce que le produit fait
[Description fonctionnelle de haut niveau — 3-5 phrases max]

## Ce que le produit ne fait PAS (hors scope v1)
- [Explicitement]

## Hypotheses non verifiees
| Hypothese | Source | Validee ? |
|-----------|--------|-----------|
| [H1] | Brief utilisateur | Non |

## Points de tension identifies
[Ecarts entre brief et donnee UXR, arbitrages faits]
```

## Anti-patterns

- Ne pas demarrer sans brief utilisateur
- Ne pas inventer des challenges : chaque confrontation doit citer une source UXR
- Ne pas valider un brief qui ignore un persona majeur sans justification explicite
- Ne pas decider de la plateforme a la place de l'utilisateur
- Ne pas passer au feature-breakdown sans validation du brief
