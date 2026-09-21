# Gabarit de Ticket « Tracer Bullet »

Un ticket est une **tranche verticale** : un chemin étroit mais complet à travers toutes les couches, livrable et vérifiable seul. Pas une étape technique isolée (« créer l'entité », puis « faire le contrôleur »).

Les tickets vivent dans `.tickets/`, **un fichier par ticket, jamais un fichier combiné**.

- Nommage : `NN-nom-court.md`, numérotés depuis `01`.
- Les numéros suivent les dépendances : les tickets sans prérequis d'abord.
- Le ticket disponible est celui dont tous les prérequis sont terminés. Travaille cette *frontier* (les tickets débloqués), pas la liste dans l'ordre.

---

## Gabarit

```md
# NN : <titre court>

## Ce qui doit fonctionner (End-to-End)

<Le comportement vu de l'extérieur : ce que l'utilisateur fait, ou ce que le client HTTP envoie et reçoit.
Décris le parcours, pas les fichiers. Ex. : « un client envoie une inscription avec un email déjà pris et reçoit un 409 ».>

## Bloqué par

<Les numéros et titres des tickets à terminer avant celui-ci, ou : Aucun (démarrage immédiat)>

## Critères d'acceptation

- [ ] <une entrée invalide est rejetée avec le code HTTP attendu>
- [ ] <le cas nominal renvoie le code HTTP et le corps attendus>
- [ ] <la donnée est réellement persistée puis relue>
- [ ] <un test d'intégration couvre le cas nominal et un cas d'erreur, et il est vert>

## Definition of Done

- [ ] message de commit au format Conventional Commit, proposé par le junior et validé par le Lead (ex. `feat(clients): refuse un email déjà utilisé`)
- [ ] le test a été vu **rouge** avant l'implémentation, puis vert
- [ ] zéro warning de compilation
- [ ] suite de tests au vert
```

---

## Les règles qui font un tracer bullet

- **Vertical, jamais horizontal.** Le ticket traverse le chemin complet. « Créer la table » n'est pas un ticket ; « enregistrer un client » en est un.
- **Vérifiable seul.** À la fin, le ticket se démontre sans attendre les suivants.
- **Dimensionné pour un seul contexte.** Si le ticket oblige à tout garder en tête en même temps, il est trop gros : découpe.
- **Ni chemins de fichiers, ni extraits de code.** Ils périment vite, et le junior doit décider lui-même de leur emplacement. Exception : un extrait qui encode une décision mieux que la prose (un schéma, une machine à états), réduit à la partie porteuse de décision.
- **Un critère d'acceptation se vérifie.** « Le code est propre » ne se coche pas ; « un email déjà pris renvoie 409 » se coche.

---

## Qui remplit quoi

Le **Lead** propose le découpage et le fait approuver avant toute implémentation. Le **junior** génère les fichiers de tickets depuis ce gabarit, implémente, exécute les tests, puis vient chercher la validation. Un critère ne se coche que sur du code réellement présent et un test réellement vert, jamais sur une déclaration.
