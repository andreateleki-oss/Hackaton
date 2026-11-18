---
name: moscow-prioritization
description: Priorise les features en MoSCoW. Force la justification de chaque Must. Refuse un backlog avec plus de 40% de Must.
---

# Skill — moscow-prioritization

## Pre-requis

`knowledge/pm/feature-breakdown.md` valide.

## Le filtre Must

Pour chaque feature, poser mentalement :
> "Si on enleve ca, le produit resout-il quand meme le probleme central du brief ?"

- **Must** — Non. Sans ca, le probleme n'est pas resolu.
- **Should** — Partiellement. Le core fonctionne mais c'est important.
- **Could** — Oui. Nice-to-have, valeur additionnelle.
- **Won't (v1)** — Explicitement exclu de cette version.

## Regle de sanity check

Si Must > 40% du backlog, refuser et dire :
> "Il y a [X]% de Must. C'est trop — ca veut dire qu'on n'a pas vraiment priorise.
>  On reprend. Pour chaque Must, je vais te demander : sans ca, le produit ne resout pas le probleme ?"

Passer chaque Must en revue avec l'utilisateur.

## Question a poser pour chaque Must contestable

> "Si tu lances le produit sans cette feature, est-ce que l'utilisateur peut quand meme [resoudre son probleme principal] ?"

Si la reponse est "oui mais c'est moins bien", c'est un Should.

## Livrable

Enrichir `knowledge/pm/feature-breakdown.md` avec la section priorisation :

```markdown
## Priorisation MoSCoW

| # | Feature | Priorite | Justification |
|---|---------|----------|---------------|
| F01 | ... | Must | Sans ca, [probleme central] n'est pas resolu |
| F02 | ... | Should | Important mais le core fonctionne sans |
| F03 | ... | Could | Valeur additionnelle |
| F04 | ... | Won't v1 | Reporte — [raison explicite] |

## Resume
Must : X (X%) — Should : X — Could : X — Won't : X
```

## Anti-patterns

- Ne pas tout mettre en Must
- Ne pas justifier un Must sans reference au probleme central du brief
- Ne pas mettre en Won't sans raison explicite
- Ne pas passer aux user stories sans validation de la priorisation
