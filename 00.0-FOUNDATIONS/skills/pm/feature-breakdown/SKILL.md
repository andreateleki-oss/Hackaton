---
name: feature-breakdown
description: Propose 10 features max depuis le brief valide. Chaque feature est challengee avec l'utilisateur avant validation. Ne demarre jamais sans brief.md valide.
---

# Skill — feature-breakdown

## Pre-requis

```bash
# brief valide
grep "Statut" knowledge/pm/brief.md
# doit retourner "Valide"
```

Si absent ou non valide :
> "Le brief n'est pas valide. On ne decoupe pas de features sans brief."

## Methode

### 1. Extraire la matiere

Depuis brief.md, lire :
- Les JTBD couverts
- Les personas cibles
- Le scope declare (ce que le produit fait / ne fait pas)
- La cible plateforme

Depuis les livrables UXR :
- Les pain points les plus frequents
- Les workarounds actuels des utilisateurs

### 2. Proposer 10 features maximum

Chaque feature doit :
- Repondre a au moins un JTBD identifie
- Etre livrable seule (pas de dependance circulaire)
- Avoir une valeur observable pour l'utilisateur
- Etre testable (on peut dire "ca marche" ou "ca marche pas")

Format :

| # | Feature | JTBD | Persona | Testable ? |
|---|---------|------|---------|------------|
| F01 | ... | JTBD-FX | Persona X | Oui : [critere] |

Pourquoi 10 max : au-dela, on n'a pas priorise, on a liste. Un bon PM coupe.

### 3. Challenger chaque feature avec l'utilisateur

Pour chaque feature, poser :
> "F0X — [nom]. Ca repond a [JTBD]. Tu confirmes que c'est dans le scope v1 ?"

Signaler les tensions :
- Features qui ne repondent a aucun JTBD : pourquoi les garder ?
- JTBD non couverts par aucune feature : oubli volontaire ?
- Features trop larges : peut-on decouper ?

### 4. Valider le decoupage

Afficher le tableau final et demander :
> "10 features, [X] JTBD couverts sur [Y]. Qu'est-ce qui manque ? Qu'est-ce qu'on enleve ?"

Ne pas passer a MoSCoW sans validation.

## Livrable

`knowledge/pm/feature-breakdown.md` :

```markdown
# Decoupage fonctionnel — [Projet]
> Statut : [A VALIDER]
> Source : knowledge/pm/brief.md
> Date : YYYY-MM-DD

## Couverture JTBD
| JTBD | Features associees |
|------|-------------------|
| JTBD-F1 | F01, F03 |
| JTBD-F2 | F02 |

## Features proposees

| # | Feature | Description | JTBD | Persona | Testable |
|---|---------|-------------|------|---------|----------|
| F01 | ... | ... | JTBD-FX | ... | Oui : [critere] |

## JTBD non couverts
| JTBD | Raison |
|------|--------|
| JTBD-FX | Hors scope v1 — [justification] |

## [A DECIDER]
- [points ouverts]
```

## Anti-patterns

- Ne pas depasser 10 features — si on a 15, on n'a pas priorise
- Ne pas proposer de features sans lien avec un JTBD
- Ne pas accepter "tout le module X" comme une feature
- Ne pas passer a MoSCoW sans validation du decoupage
- Ne pas inventer des features que le brief n'implique pas
