# Projet — Équipe d'agents produit

Ce dépôt héberge une équipe d'agents spécialisés (UXR, PM, design, dev, tracking).
Chaque agent est défini dans `.claude/agents/`. La connaissance partagée vit dans
`knowledge/`, les compétences réutilisables dans `skills/`.

## Structure

```
.claude/agents/        définitions des agents
knowledge/uxr/         entretiens bruts + livrables UXR
knowledge/pm/          matière PM
knowledge/design/      matière design
skills/                compétences réutilisables par domaine
```

## Agents disponibles

| Agent | Rôle | Statut |
|-------|------|--------|
| `agent-uxr` | Analyse les entretiens, les synthétise, construit des personas | ✅ Opérationnel |
| `agent-pm` | Challenge le brief, découpe en features, priorise MoSCoW, produit des user stories | ✅ Opérationnel |
| `agent-design` | (à définir) | ⏸ Squelette |
| `agent-dev` | (à définir) | ⏸ Squelette |
| `agent-tracking` | (à définir) | ⏸ Squelette |
| `agent-suivi` | Produit un état des lieux du projet au lancement | ✅ Opérationnel |

## Avancement pipeline

| Étape | Statut | Livrables |
|-------|--------|-----------|
| UXR | ✅ Terminé | `knowledge/uxr/outputs/` : grille-analyse, synthese, personas, jobs-to-be-done, personas.html |
| PM | ✅ Terminé | `knowledge/pm/` : brief.md, feature-breakdown.md, user-stories.md |
| Design | ⏸ À lancer | `knowledge/design/` vide — agent à définir |
| Dev | ⏸ Bloqué | Attend les livrables design |

## Gardes-fous permanents

- ❌ Lancer `@pm` sans livrables UXR validés (`knowledge/uxr/outputs/synthese.md`)
- ❌ Lancer `@design` sans livrables PM validés (`knowledge/pm/user-stories.md`)
- ❌ Lancer `@dev` sans livrables UXR et PM validés
- ❌ Générer du code sans features priorisées dans le backlog
- ❌ Synthétiser des interviews sans critères validés dans `grille-analyse.md`
- ❌ Inventer des décisions non documentées dans les livrables
- ✅ UXR → PM → Design → Dev : l'ordre ne se négocie pas
- ✅ Une question avant toute exécution
- ✅ Tout output IA est validé par le designer avant d'être considéré comme vrai
