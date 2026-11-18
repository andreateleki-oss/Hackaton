---
name: user-stories
description: Genere des User Stories depuis les features priorisees. Chaque US est exploitable par design ET dev. Force les edge cases. Ne genere jamais uniquement le happy path.
---

# Skill — user-stories

## Pre-requis

- `knowledge/pm/feature-breakdown.md` valide avec priorisation MoSCoW
- `knowledge/uxr/outputs/personas.md` disponible

Generer les US uniquement pour les features Must et Should.
Les Could et Won't n'ont pas de US en v1.

## Format impose

```markdown
### US-XXX [TYPE] — [Titre court]

**Feature source :** F0X — [nom]
**Status :** Backlog
**Type :** Design / Tech / Product
**Persona :** [Nom du persona — comportement cle]
**JTBD :** JTBD-FX

En tant que [persona comportemental]
Je veux [action concrete]
Afin de [benefice mesurable]

**Criteres d'acceptation**

Scenario: Happy path
  Given [contexte initial]
  When [action utilisateur]
  Then [resultat observable]

Scenario: Cas vide / premier usage
  Given [aucune donnee]
  When [...]
  Then [...]

Scenario: Erreur
  Given [...]
  When [action qui echoue]
  Then [message d'erreur clair]

**Depend de :** [US-XXX si applicable]
```

## Regle absolue

**Toujours generer au moins 3 scenarios : happy path + cas vide + erreur.**

Si l'utilisateur dit "juste le happy path" :
> "Le happy path c'est 20% de l'usage reel. Les cas d'erreur et les cas limites c'est la que l'experience se joue. On garde les 3 ?"

## Ce que les US doivent permettre

Les US sont le contrat entre PM, design et dev :
- **Pour le design** : le persona, le contexte, le resultat attendu, les etats (vide, erreur, succes) — tout ce qu'il faut pour concevoir les ecrans
- **Pour le dev** : les criteres d'acceptation en Gherkin, les edge cases, la complexite, les dependances — tout ce qu'il faut pour implementer et tester

Le PM ne decide pas du design ni de la stack. Il fournit la matiere pour que chacun puisse travailler.

## Livrable

`knowledge/pm/user-stories.md` :

```markdown
# User Stories — [Projet]
> Statut : [A VALIDER]
> Source : knowledge/pm/feature-breakdown.md
> Date : YYYY-MM-DD
> Scope : Must + Should uniquement

## Vue d'ensemble
| US | Type | Feature | Status | Persona | JTBD |
|----|------|---------|--------|---------|------|
| US-001 | Design | F01 | Backlog | Lea | JTBD-F1 |

## Stories detaillees
[US au format ci-dessus]

## Matrice de couverture
| Persona | US associees |
|---------|-------------|
| Lea | US-001, US-003 |

## Points d'attention pour le design
- [etats particuliers, contraintes UX identifiees dans les entretiens]

## Points d'attention pour le dev
- [dependances entre US, contraintes techniques identifiees]
```

## Anti-patterns
- Ne pas generer de US pour les Could et Won't
- Ne pas ecrire de US sans persona precis
- Ne pas accepter des criteres non verifiables ("l'utilisateur est satisfait")
- Ne pas faire une US qui couvre plusieurs comportements distincts
- Ne pas decider du design (wireframes, composants) ni de la stack technique
- Toujours lier a un JTBD et a un insight UXR si disponible
