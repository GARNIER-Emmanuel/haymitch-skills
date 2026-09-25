---
name: hay-help
description: "Haymitch Help : choisit la bonne commande et explique ce qu'elle débloque. Utiliser quand le junior demande comment démarrer, quoi faire maintenant ou à quoi sert une commande Haymitch."
---

# /hay-help : choisir le bon parcours

> **Autonome** : cette commande fonctionne seule. Charge uniquement l'état nécessaire au routage.

Haymitch suit une boucle : cadrer → découper verticalement → contrat → RED → GREEN → refactor → revue → commit. N'explique que l'étape utile maintenant.

## Routage

| Situation | Commande |
|---|---|
| Nouvelle idée, roadmap ou tickets | `/hay-feature` |
| Reprise de session, position inconnue | `/hay-status` |
| Contrat, RED, GREEN ou refactor produit | `/hay-continue` |
| Stacktrace, compilation, assertion ou bug dont la cause est inconnue | `/hay-debug` |
| Notion connue, tentative faite, besoin d'une seule piste | `/hay-hint` |
| Notion, API, annotation ou ligne incomprise, même dans un test en échec | `/hay-learn` |
| Phase 4 terminée, ticket à clore | `/hay-review` |
| Décision difficile à inverser | `/hay-adr` |

Pour « que faire maintenant ? », lis seulement le bloc `État courant` de `docs/MENTORING.md`, réponds en une phrase et donne une commande. Ne charge ni le diff ni les références de stack pour expliquer le catalogue.

## Réponse

1. Nomme une seule commande.
2. Explique en une phrase ce qu'elle débloque.
3. Donne l'action immédiate attendue.

Demande au junior de formuler en trois phrases : objectif, tentative, observation. Devant une erreur concrète dont la cause est inconnue, route vers `/hay-debug`. S'il connaît les notions et demande seulement où regarder, route vers `/hay-hint`. Devant « je ne sais pas faire » parce qu'une notion manque, route vers `/hay-learn`.

Si aucune commande ne convient, dis-le au lieu de forcer un mauvais parcours.
