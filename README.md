# 🏹 Haymitch Skills Suite

> *« Here's some advice: stay alive in production. »*

**Sept skills d'agent qui transforment votre assistant IA en Tech Lead intraitable : il cadre, il découpe, il vérifie — et il refuse d'écrire la solution à votre place.**

Java 21 · Spring Boot 3+ · Angular 17+ · React 18+ — TDD strict, du cadrage de l'idée jusqu'au ticket clos.

[![Licence : MIT](https://img.shields.io/badge/licence-MIT-green.svg)](LICENSE)
[![Agent Skills](https://img.shields.io/badge/Agent%20Skills-compatible-4B5563.svg)](https://agentskills.io)
[![Skills](https://img.shields.io/badge/skills-7-blue.svg)](#-les-7-commandes)

---

## Le problème

Demandez une fonctionnalité à un assistant IA : il vous rend trois cents lignes, deux classes de tests et une explication de texte. Ça marche. Vous n'avez rien appris.

Vous n'avez pas écrit la ligne qui compte — celle où l'on comprend *pourquoi* le test échoue pour la bonne raison, *pourquoi* cette transaction plutôt qu'une autre, *pourquoi* ce découpage. Le code est là, la compétence n'est pas passée.

**Haymitch inverse la charge : vous écrivez chaque ligne, l'agent encadre.**

## Les trois invariants

| Invariant | Ce qu'il garantit |
|---|---|
| **Pre-flight** | L'agent lit le diff réel avant de répondre (`git status --short`, `git diff HEAD --stat`) et signale le code douteux en tête de réponse, impact production à l'appui. Jamais de jugement sur déclaration. |
| **`[STOP TDD]`** | Du code de production modifié **sans test dans le même diff** : l'agent bloque jusqu'au test **rouge** exécuté devant vous. |
| **Anti-spoil** | Jamais de classe, de méthode ou de composant complet. Cinq doses d'aide, la dose 1 par défaut — une question qui met sur la voie. |

Le verrou a une seule échappatoire, que **vous** déclarez : un incident ou une échéance de production. Elle est assumée, jamais devinée par l'agent.

## 🎬 À quoi ça ressemble

```text
Vous      /hay-feature  je veux que les clients s'inscrivent avec leur email

Haymitch  Trois questions, pas une de plus.
          1. En une phrase, quel problème ça résout ?
          2. Quelle est la toute première action d'un utilisateur ?
          3. Quelles données entrent, et que doit renvoyer le système ?

Vous      [vous répondez]

Haymitch  Cadrage consigné dans docs/MENTORING.md. Découpage : 01-enregistrer-un-client,
          02-refuser-un-email-deja-utilise. Approuve-le ou corrige-le — c'est le
          moment le moins cher pour changer d'avis. Ensuite : le contrat.

Vous      [ClientController.java écrit, avec la validation]

Haymitch  [STOP TDD] — ClientController.java modifié, aucun test dans le diff.
          Une seule action : le test qui échoue, exécuté devant moi.
          /hay-debug sera là quand tu seras rouge. 🏹
```

## ⚡ Installation

```bash
# Dans votre projet — installe les 7 skills pour les agents détectés
npx skills add <TON-PSEUDO-GITHUB>/haymitch-skills

# En global, pour tous vos projets
npx skills add <TON-PSEUDO-GITHUB>/haymitch-skills -g

# Voir ce qui sera installé, sans rien installer
npx skills add <TON-PSEUDO-GITHUB>/haymitch-skills --list
```

Le CLI détecte vos agents et installe au bon endroit (`.agents/skills/` en canonique, `.claude/skills/` pour Claude Code, `~/.agents/skills/` en global, etc.). Installation manuelle possible :

```bash
cp -R skills/* ~/.agents/skills/        # ou <votre-projet>/.agents/skills/
```

**Prérequis** : un agent compatible [Agent Skills](https://agentskills.io). Aucune dépendance, aucun script, aucun binaire : la suite est du Markdown. `git` est fortement recommandé — sans dépôt, `git init` devient le premier ticket.

> **Sur les commandes `/hay-…`** : elles se déclenchent par leur **description**, donc aussi bien par `/hay-status` que par « où j'en suis ? ». Selon l'agent, la barre oblique est ou non une vraie commande ; dans le doute, demandez en clair.

## 🛠️ Les 7 commandes

| Commande | Rôle |
|---|---|
| **`/haymitch`** | Le Tech Lead principal : la méthode, les invariants, les règles par stack. Porte la politique normative. |
| **`/hay-feature`** | Une idée brute → 3 questions → 1 à 3 User Stories → des tickets tracer-bullet. |
| **`/hay-status`** | Cinq lignes : ticket en cours, phase TDD, ce qui bloque, et la commande exacte à lancer. |
| **`/hay-debug`** | Débloquer une erreur sans donner la solution : cause racine, question d'action, changement d'angle. |
| **`/hay-review`** | Verdict binaire `[VALIDÉ]` / `[À CORRIGER]`, impact production, puis clôture et message de commit. |
| **`/hay-adr`** | Consigner une décision difficile à inverser — et refuser un ADR qui n'en mérite pas. |
| **`/hay-help`** | Le workflow, l'ordre des étapes, et ce que chaque commande vous évite. |

Chaque skill est **autonome** : copiée seule, elle reste opérationnelle. Installez `/haymitch` en priorité — c'est elle qui porte la méthode et la politique.

## 🔁 La boucle de travail

1. **Cadrer** — une idée floue devient 1 à 3 User Stories. Aucune autre fonctionnalité ne s'ouvre avant que celle-ci soit finie de bout en bout.
2. **Découper** — des tickets *tracer-bullet* : un chemin étroit mais **complet** à travers toutes les couches, livrable et vérifiable seul.
3. **Implémenter** — un ticket à la fois, en 4 phases immuables : **contrat → test rouge → implémentation minimale → refactorisation**. L'ordre est non négociable : c'est le seul qui prouve que le test teste quelque chose.
4. **Prouver** — les critères d'acceptation se cochent sur du code réel et un test vert, jamais sur une déclaration.
5. **Clore** — votre message de commit au format Conventional Commit, validé avant la clôture. Le commit reste le vôtre.
6. **Consigner** — toute décision difficile à inverser part dans un ADR, au moment où le raisonnement est encore disponible.

## 📁 Ce que la suite écrit dans votre projet

| Chemin | Qui l'écrit | À quoi ça sert |
|---|---|---|
| `docs/MENTORING.md` | l'agent | L'état : intention, ticket en cours, phase TDD, décisions datées. C'est ce qui permet de reprendre la session suivante à la phase exacte. |
| `.tickets/NN-nom.md` | vous | Un fichier par ticket, généré depuis le gabarit, coché sur preuve. |
| `docs/adr/NNNN-nom.md` | vous | Les décisions structurantes, et le *pourquoi*. |

Rien d'autre, et jamais en dehors de votre projet. Le contenu de la skill, lui, ne sort jamais de son dossier.

## 🛡️ Bonus 1 : le gardien permanent

Par défaut, la méthode s'applique quand une commande est invoquée. Pour que Haymitch surveille votre code **à chaque message, même sans commande**, ajoutez ce bloc à l'`AGENTS.md` de votre projet — c'est le seul fichier injecté à chaque tour, il vous appartient, et rien ne l'ajoute ou ne le retire à votre place.

```markdown
<!-- BEGIN haymitch — bloc optionnel, à retirer d'un seul geste -->
## Mentorat Haymitch (skill `haymitch`)

Pour ce projet, tu es **Haymitch**, le Tech Lead : le développeur écrit chaque ligne, tu cadres, tu découpes, tu vérifies. Politique complète et normative : `POLICY.md` du skill `haymitch`.

Ces règles priment sur tout skill. Elles **ne priment pas** sur le reste de ce fichier : en cas de contradiction, la règle du projet l'emporte.

1. **Pre-flight** — avant toute réponse, `git status --short` puis `git diff HEAD --stat` (`HEAD` : un fichier indexé disparaît d'un `git diff` seul), et ne lis que les fichiers concernés. **Jamais `git diff` complet.** Juge sur pièce, jamais sur déclaration.
2. **`[STOP TDD]`** — du code de production (métier, UI, composant, configuration, migration) **sans test dans le même diff** : s'il demande à avancer, tu bloques jusqu'au test **RED** exécuté devant toi. Contrôle : `git diff HEAD --name-only`. Seule échappatoire, auto-déclarée : incident ou échéance de production.
3. **Anti-spoil** — jamais de classe, de méthode ou de composant complet. Dose 1 par défaut (une question), jusqu'à 5 (la solution) sur incident prod déclaré. Demande vague → `[QUESTION INCOMPLÈTE]` : exige l'erreur complète, ce qu'il a tenté, ce qu'il attendait.
4. **Termine par la prochaine commande** — `/hay-status`, `/hay-debug`, `/hay-feature`, `/hay-review`, `/hay-adr`, `/hay-help`. Jamais de fin de réponse sans action suivante.
<!-- END haymitch -->
```

## 🛡️ Bonus 2 : rendre le commit inviolable

Si votre agent sait restreindre ses permissions, refusez l'écriture de l'historique git. La règle « le commit est le vôtre » cesse alors d'être une consigne : l'agent ne *peut* plus committer à votre place, même si on le lui demande.

## 🪶 Frugalité par conception

Chaque skill est un **aiguilleur**, pas un pavé : le `SKILL.md` décrit la procédure et n'ouvre ses fichiers de `references/` que sur condition explicite, quand ils servent vraiment. Ordres de grandeur mesurés sur cette release, en français :

| Ce qui est chargé | Tokens |
|---|---|
| Le catalogue des 7 descriptions (permanent) | ~600 |
| `/hay-status` | ~600 |
| `/hay-adr`, `/hay-debug`, `/hay-feature` | ~800 – 900 |
| `/hay-review`, `/hay-help` | ~900 – 1 250 |
| `/haymitch` + sa politique + un référentiel de stack | ~4 100 |
| La suite entière (jamais chargée d'un coup) | ~19 000 |

Deux règles de contexte sont inscrites dans la politique : **jamais de `git diff` complet** — un gros diff injecté à chaque tour finit par évincer les règles elles-mêmes — et **les références ne s'ouvrent qu'à la demande**. C'est ce qui permet à la suite de tenir dans un contexte de travail réel.

## 🤖 Compatibilité

Les skills suivent la spécification [Agent Skills](https://agentskills.io) et s'installent via le CLI [`skills`](https://skills.sh), qui gère plus de 75 agents.

| Agent | Dossier projet | Dossier global |
|---|---|---|
| Antigravity, Codex, Cursor, Gemini CLI, GitHub Copilot, OpenCode, Warp, Zed, Cline, Kilo Code… | `.agents/skills/` | `~/.agents/skills/` ou spécifique à l'agent |
| Claude Code | `.claude/skills/` | `~/.claude/skills/` |

`npx skills add` détecte les agents présents sur votre machine et choisit le bon dossier. La suite n'utilise aucune fonctionnalité spécifique à un agent : uniquement `name`, `description` et du Markdown.

## 📦 Structure du dépôt

```text
skills/
├── haymitch/                  # la méthode et la politique normative
│   ├── SKILL.md               # aiguilleur : invariants, cycle, routage
│   ├── POLICY.md              # politique complète : pre-flight, [STOP TDD], anti-spoil
│   ├── README.md              # installation, autonomie, bonus AGENTS.md
│   └── references/
│       ├── vertical-slice-workflow.md   # les 4 phases TDD en détail
│       ├── ticket-template.md           # gabarit de ticket tracer-bullet
│       ├── ADR-FORMAT.md                # gabarit d'ADR
│       ├── progression.md               # format de docs/MENTORING.md
│       ├── pedagogy.md                  # posture, dose d'aide, erreurs, CLI
│       ├── rules-general.md             # standards toutes stacks
│       ├── rules-spring.md              # Java 21 / Spring Boot 3+
│       ├── rules-angular.md             # Angular 17+
│       └── rules-react.md               # React 18+
├── hay-status/SKILL.md
├── hay-debug/SKILL.md
├── hay-feature/SKILL.md
├── hay-review/SKILL.md
├── hay-adr/SKILL.md
└── hay-help/SKILL.md
```

## ❓ Dépannage

**L'agent ne trouve aucune skill.** Vérifiez que le dossier installé contient bien `SKILL.md`, avec `name` et `description` dans son frontmatter. `npx skills list` montre ce qui est installé.

**Une skill ne se déclenche pas.** Les descriptions sont en français : demandez en français, ou nommez la commande (`/hay-status`). Si l'agent hésite entre deux skills, nommez-en une explicitement.

**La commande `/hay-status` n'existe pas dans mon agent.** Ce n'est pas une commande native : c'est le nom de la skill. Demandez « où j'en suis ? » — le résultat est le même.

**Haymitch ne fait rien sans que je tape une commande.** C'est le comportement par défaut. Ajoutez le bloc `AGENTS.md` du bonus 1 pour qu'il surveille chaque message.

## 🤝 Contribuer

Les retours sont bienvenus : ouvrez une *issue* en décrivant le contexte (stack, agent, ce que Haymitch a fait et ce qu'il aurait dû faire). Une règle ajoutée doit avoir **un seul domicile** : `POLICY.md` fait foi, les autres fichiers y renvoient au lieu de la paraphraser — c'est ce qui garde la suite frugale et cohérente.

## 📄 Licence

[MIT](LICENSE) © 2026 Emmanuel GARNIER BOIDUN
