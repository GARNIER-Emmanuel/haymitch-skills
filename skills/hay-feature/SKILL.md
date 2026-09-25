---
name: hay-feature
description: "Haymitch Feature : transforme une idée brute en roadmap de 3 à 6 jalons, puis en 1 à 3 User Stories et en tickets tracer-bullet dans .tickets/, et interdit toute autre fonctionnalité jusqu'à ce que celle-ci soit finie de bout en bout. Utiliser quand le développeur décrit une fonctionnalité à construire, une idée à cadrer, une roadmap à définir, ou demande de découper du travail en tickets."
---

# /hay-feature : d'une idée brute à des tickets

> **Autonome** : cette commande fonctionne seule, copiée dans `.agents/skills/` (sans `AGENTS.md` et sans autre skill). Ses renvois à `POLICY.md` ou aux `references/` ne sont que du **détail** ; s'ils sont absents, applique ce qui suit.

Un seul parcours en deux temps, jamais l'un sans l'autre : cadrer, puis découper. Les gabarits complets vivent dans les références `vertical-slice-workflow.md` et `ticket-template.md` du skill `haymitch` (à ouvrir pour le détail). Ce qui suit suffit pour découper.

---

## Temps 1 : Cadrer (3 questions, pas une de plus)

1. **L'intention métier** : en une phrase, quel problème le projet résout-il ?
2. **Le premier cas d'usage** : quelle est la toute première action qu'un utilisateur doit pouvoir faire ?
3. **Le contrat de données** : quelles informations entrent, et que doit renvoyer le système ?

Puis **tu proposes la roadmap : 3 à 6 jalons**, une **capacité démontrable** par ligne, sans date ni estimation, ordonnés par dépendances. Le jalon 1 est un **walking skeleton**, jamais « socle technique + auth ». Il valide l'ordre ou le corrige : **l'ordre technique est ton expertise, la priorité métier est son droit.**

Il n'a pas besoin d'un cahier des charges. Il a besoin d'une tranche. Sors **1 à 3 User Stories**, puis **interdis toute autre fonctionnalité** : on réalise celle-ci de bout en bout avant d'en ouvrir une autre (**lister les jalons n'autorise pas à les ouvrir**).

---

## Temps 2 : Découper en tickets tracer-bullet

- **Tu proposes le découpage, il génère les fichiers** dans `.tickets/`, un fichier par ticket (jamais un fichier combiné), selon le gabarit. Tu vérifies les fichiers produits.
- Le nombre de tickets est une conséquence du parcours, jamais une cible. Les **1 à 3** du cadrage désignent les User Stories, pas les tickets : trois tickets peuvent suffire comme en exiger davantage.
- Un ticket est une **tranche verticale** : un chemin étroit mais **complet** à travers toutes les couches, livrable et vérifiable seul. « Créer la table » n'est pas un ticket ; « enregistrer un client » en est un.
- Numérote depuis `01`, **par dépendances** : les tickets sans prérequis d'abord, et chaque ticket déclare ce qui le bloque.
- Deux à quatre critères d'acceptation **vérifiables** : « un email déjà pris renvoie 409 » se coche, « le code est propre » ne se coche pas.
- Redécoupe si le ticket porte plusieurs comportements démontrables, dépasse quatre critères indépendants ou ne tient plus dans une boucle TDD que le junior peut garder en tête.
- **Ni chemins de fichiers, ni extraits de code** dans un ticket : ils périment, et c'est à lui de décider de leur emplacement. Exception : l'extrait qui encode une décision mieux que la prose.
- **Fais approuver le découpage avant la moindre implémentation.** C'est le moment le moins cher pour corriger une erreur de conception.

---

## Consigner, puis lancer

1. Reporte le cadrage, la vision, la roadmap et la liste des tickets dans `docs/MENTORING.md` (`references/progression.md` du skill `haymitch`) : sans cette trace, la session suivante redémarrera le cadrage à zéro.
2. Termine par **le premier ticket dont tous les prérequis sont terminés**, son contenu en une phrase, et l'action immédiate : le contrat à écrire (phase 1), ou `/hay-status` s'il veut d'abord s'orienter.

---

## Un cadrage déjà consigné ne se redemande pas

Si `docs/MENTORING.md` contient déjà le cadrage et une liste de tickets, tu ne reposes pas les 3 questions : tu reprends à la phase exacte, et tu pointes vers `/hay-status`. S'il n'y a **pas de roadmap** dans un fichier existant, tu ne reposes rien non plus : tu proposes la roadmap à la prochaine clôture de jalon.
