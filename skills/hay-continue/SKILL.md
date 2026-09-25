---
name: hay-continue
description: "Haymitch Continue : vérifie les ajouts du développeur contre la preuve attendue de la phase TDD courante, met à jour l'avancement uniquement si la preuve est suffisante, puis donne une seule prochaine action. Utiliser quand le développeur demande de vérifier ce qu'il vient de faire, de valider une étape, de poursuivre le ticket ou de passer à la phase suivante."
---

# /hay-continue : valider une phase et avancer

> **Autonome** : cette commande fonctionne seule. Si le skill `haymitch` est installé à côté, sa politique normative reste prioritaire.

Cette commande est le **sas entre deux phases TDD**. Elle contrôle une preuve ciblée, avance l'état si elle est recevable, puis donne une action. Elle ne remplace ni le tableau de bord `/hay-status`, ni la revue finale `/hay-review`.

## Frontières

- **Besoin d'orientation sans nouvel ajout** → `/hay-status`.
- **Ajout effectué, phase à valider** → reste dans `/hay-continue`.
- **Erreur ou test incompris** → `/hay-debug`.
- **Notion non comprise ou « je ne sais pas faire »** → `/hay-learn`.
- **Phase 4 terminée, ticket à clore** → `/hay-review`.

## Inspection minimale

1. Lis seulement dans `docs/MENTORING.md` le ticket courant, la phase TDD et le signal attendu.
2. Ouvre le fichier `.tickets/NN-....md` correspondant.
3. Exécute `git status --short`, `git diff HEAD --stat` et `git diff HEAD --name-only`.
4. Ouvre uniquement les fichiers modifiés nécessaires à la preuve. Jamais de diff brut complet.
5. Utilise la sortie de test fournie par le junior. Ne relance pas ses tests à sa place.

Si l'état ou le ticket manque, n'invente pas une phase : dirige vers `/hay-feature` ou `/hay-status`.

## Portes de validation

| Phase | Preuve minimale |
|---|---|
| 1. Contrat | Entrées, sorties et comportements observables définis ; le ticket reste compréhensible sans lire l'implémentation. |
| 2. RED | Test ciblé exécuté et échec causé par le comportement absent, pas par une compilation cassée. |
| 3. GREEN | Même test ciblé vu vert ; aucun comportement supplémentaire non demandé. |
| 4. Refactorisation | Tests ciblés et suite pertinente vus verts ; critères d'acceptation démontrés. |

La présence d'un fichier ne constitue jamais une preuve. Une déclaration « c'est fait » non plus.

## Décision et mise à jour

### Preuve suffisante

1. Commence par `[PHASE VALIDÉE]`.
2. Résume la preuve en une phrase.
3. Coche la phase franchie dans `docs/MENTORING.md` et renseigne la phase suivante avec son signal attendu.
4. Ne coche pas le ticket terminé : la clôture appartient à `/hay-review` après validation du commit.
5. Donne une seule prochaine action, réalisable immédiatement.

Après validation de la phase 4, il n'existe pas de phase 5 : marque la phase terminée et route vers `/hay-review` pour les critères, le commit réel et la clôture.

### Preuve insuffisante

1. Commence par `[PHASE NON VALIDÉE]`.
2. N'actualise aucun état.
3. Nomme la preuve manquante ou la première divergence observable.
4. Donne une seule action corrective. Route vers `/hay-debug` ou `/hay-learn` si nécessaire.

## Format de sortie

```text
[PHASE VALIDÉE] Phase 2 — RED
Preuve   : ClientApiTest échoue parce que l'endpoint attendu est absent.
Avance   : phase 3 — implémentation minimale.
Objectif : faire passer uniquement ce test, sans anticiper le cas d'erreur.
Action   : écris le minimum nécessaire, puis relance la même commande ciblée.
```

Maximum cinq lignes après le verdict. N'explique la commande CLI que si elle apparaît pour la première fois ou si le junior le demande.
