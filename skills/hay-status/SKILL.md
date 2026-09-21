---
name: hay-status
description: "Haymitch Status — Fait le point sur la session de mentorat : ticket en cours, phase TDD atteinte, ce qui bloque, et la commande CLI exacte à exécuter. Utiliser quand le développeur demande où il en est, ce qu'il reste à faire, ou par quoi continuer."
---

# /hay-status — Où il en est, et la commande suivante

> **Autonome** : cette commande fonctionne seule, copiée dans `.agents/skills/` — sans `AGENTS.md` et sans autre skill. Ses renvois à `POLICY.md` ou aux `references/` ne sont que du **détail** ; s'ils sont absents, applique ce qui suit.

La commande la plus invoquée de la boîte à outils, donc la plus courte : **cinq lignes maximum, puis une commande à copier-coller**. Jamais de paragraphe, jamais son diff rediffusé — il l'a écrit, il le connaît.

---

## Procédure

1. Lis `docs/MENTORING.md` : **l'état** — le jalon marqué « en cours » dans la roadmap, et le ticket en cours. Pas le journal des décisions en entier.
2. `git status --short` puis `git diff HEAD --stat` — jamais `git diff` complet (`POLICY.md` §1).
3. Ouvre le fichier du ticket en cours dans `.tickets/`.

---

## Format de sortie

```
Jalon 2/4 · Ticket 03/07 — refus-email-deja-utilise
Phase 2/4 — Test d'abord (RED)
Fait    : contrat (Record + @Email) figé et validé
Bloque  : le test ne compile pas — ce n'est pas encore un RED
Action  : ./mvnw test -Dtest=ClientServiceTest#shouldRejectDuplicateEmail
```

S'il n'y a pas de ticket en cours : l'intention en une phrase, puis `/hay-feature`.

---

## Règles

- **Une seule** commande à la fin, celle de la phase en cours, exécutable telle quelle. Jamais une liste d'options — c'est à toi de savoir où il en est.
- Une phase ne se coche que si tu l'as **vue** franchie. La phase 2 (RED) ne se coche que sur un échec montré : un test écrit après le code ne la valide pas.
- Signale un écart TDD (`POLICY.md` §2) **en une ligne**, pas en dissertation : ce n'est pas le sujet de `/hay-status`.
- Reste factuel. `/hay-status` est un instrument de bord, pas une évaluation : les verdicts se rendent dans `/hay-review`.
- Si la commande à venir échoue une deuxième fois d'affilée, la prochaine action est `/hay-debug`, pas de relancer.
