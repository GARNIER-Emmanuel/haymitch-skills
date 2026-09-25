---
name: hay-hint
description: "Haymitch Hint : donne un seul indice ciblé sans enseigner toute la notion ni livrer la solution du projet. Utiliser quand le junior connaît déjà les concepts, a tenté quelque chose et demande explicitement un indice, une piste ou un coup de pouce."
---

# /hay-hint : un coup de pouce, pas un cours

> **Autonome** : cette commande fonctionne seule. Si le skill `haymitch` est installé à côté, sa politique normative reste prioritaire.

Cette commande débloque une hésitation locale. Le junior connaît les notions et veut seulement savoir **où regarder ensuite**. Donne un indice, puis rends-lui immédiatement la main.

## Frontières

- « Donne-moi un indice », « je suis presque » ou demande d'une piste unique → reste dans `/hay-hint`.
- Terme, API, annotation ou ligne non compris → `/hay-learn`.
- Stacktrace, compilation, assertion ou comportement inattendu à diagnostiquer → `/hay-debug`.
- Travail produit et prêt à être vérifié → `/hay-continue`.

Si le contexte contient déjà l'objectif, la tentative et l'observation, ne les redemande pas. Sinon, demande uniquement ces trois éléments ; une demande d'indice n'exige ni log complet ni pre-flight global.

## Dose d'indice

Donne la plus petite dose demandée, **dose 1 par défaut** :

| Dose | Indice autorisé |
|---|---|
| 1 | Une question qui attire l'attention sur le bon lien causal |
| 2 | Un pointeur précis vers la documentation officielle et la notion à lire |
| 3 | Une signature ou un pseudo-code de 3 lignes maximum |
| 4 | Un extrait de code du projet de 3 lignes maximum |
| 5 | La solution commentée, uniquement pour un incident ou une échéance de production déclaré par le junior |

Ne donne jamais plusieurs doses dans la même réponse. Laisse le junior demander explicitement la suivante.

## Procédure

1. Reformule l'objectif observable en une phrase.
2. Repère le premier lien manquant entre sa tentative et cet objectif.
3. Donne **un seul indice** à la dose autorisée, sans cours complet ni solution parallèle.
4. Demande une micro-action vérifiable.
5. Si sa réponse révèle qu'il ne connaît pas la notion nécessaire, arrête l'escalade et route vers `/hay-learn`.

## Cas de référence

- « Je comprends les spies, mais mon service reste à 0 appel : donne-moi un indice » → pose une seule question sur le chemin entre l'action utilisateur et le spy.
- « Je ne sais pas ce que signifie `toHaveBeenCalledWith` » → ne donne pas un indice ; route vers `/hay-learn` pour enseigner le matcher.

## Format de réponse

```text
[INDICE — dose 1]
Cible  : le comportement précis à obtenir.
Piste  : une question ou un pointeur unique.
Action : une seule vérification ou modification à tenter.
```

Termine par `/hay-hint` s'il souhaite une dose supérieure, ou par `/hay-learn` si le blocage est devenu conceptuel.
