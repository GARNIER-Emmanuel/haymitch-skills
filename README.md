# 🏹 Haymitch Skills Suite

> *« Here's some advice: stay alive in production. »*

Un assistant IA classique vous pond trois cents lignes de code d'un coup. Le résultat tourne, mais vous n'avez rien appris. Vous ne savez pas pourquoi ce choix de transaction s'impose, ni pourquoi ce test a échoué.

Haymitch renverse la table : vous écrivez chaque ligne dans votre IDE, l'agent prend le rôle du Tech Lead. Il cadre le besoin, découpe les tranches de code, audite vos diffs et refuse catégoriquement de coder à votre place.

Stacks supportées : Java 21 & Spring Boot 3+, Angular 17+, React 18+. TDD rigoureux, du premier cadrage au commit validé.

[![Licence : MIT](https://img.shields.io/badge/licence-MIT-green.svg)](LICENSE)
[![Agent Skills](https://img.shields.io/badge/Agent%20Skills-compatible-4B5563.svg)](https://agentskills.io)
[![Skills](https://img.shields.io/badge/skills-9-blue.svg)](#les-9-commandes)

---

## Ce qui se passe dans votre terminal

```text
Vous      /hay-feature je veux que les clients s'inscrivent avec leur email

Haymitch  Trois questions, pas une de plus :
          1. En une phrase, quel problème cela résout-il ?
          2. Quelle est la première action utilisateur ?
          3. Quelles données entrent et que doit renvoyer le système ?

Vous      [vous répondez aux trois questions]

Haymitch  Cadrage noté dans docs/MENTORING.md. Découpage proposé :
          01-enregistrer-un-client, 02-refuser-un-email-deja-utilise.
          Valide ou ajuste : c'est le moment le moins cher pour changer d'avis.
          Ensuite : on attaque le contrat.

Vous      [ClientController.java codé avec la validation, sans test]

Haymitch  [STOP TDD] : ClientController.java modifié, aucun test dans le diff.
          Une seule action possible : écris le test qui échoue et montre-le-moi.
          /hay-learn t'aidera si tu ne comprends pas ce que ce RED doit prouver. 🏹

Vous      /hay-learn je ne comprends pas ce que mon test rouge doit vérifier

Haymitch  Le RED doit échouer parce que le comportement métier manque, pas parce
          que le test est cassé. Si POST /clients n'existe pas encore, quel statut
          ton test doit-il observer maintenant, et lequel attend-il à la fin ?

Vous      [écrit ClientApiTest, l'exécute et montre : attendu 201, obtenu 404]
          /hay-continue

Haymitch  [PHASE VALIDÉE] Phase 2 — RED
          Preuve   : ClientApiTest atteint POST /clients et échoue sur le 404 observé.
          Avance   : phase 3 — implémentation minimale.
          Objectif : faire passer uniquement ce cas nominal.
          Action   : écris le minimum nécessaire, puis relance ce test ciblé.
```

---

## Trois règles intransigeantes

| Règle | Ce qu'elle impose sur le terrain |
|---|---|
| **Pre-flight ciblé** | L'agent regarde le diff réel (`git status --short`, `git diff HEAD --stat`) avant toute réponse qui dépend du projet. Une question théorique ne recharge pas inutilement le dépôt. |
| **`[STOP TDD]`** | Du code de prod modifié sans test rouge dans le même diff ? L'agent bloque. Vous écrivez le test d'abord, ou vous ne passez pas. |
| **Anti-spoil** | Jamais de composant ni de classe complète parachutée. L'aide commence à la dose 1 : une question ciblée pour vous mettre sur la piste. |

Seule exception acceptée : un incident de production ou une urgence critique que vous déclarez vous-même.

---

## Installation en 30 secondes

```bash
# Dans votre projet : installe la suite pour vos agents détectés
npx skills add GARNIER-Emmanuel/haymitch-skills

# En global sur votre machine
npx skills add GARNIER-Emmanuel/haymitch-skills -g

# Vérifier ce qui sera installé sans toucher à rien
npx skills add GARNIER-Emmanuel/haymitch-skills --list
```

Le CLI détecte automatiquement vos outils (`.agents/skills/`, `.claude/skills/`, etc.). Si vous préférez cloner à la main :

```bash
git clone https://github.com/GARNIER-Emmanuel/haymitch-skills.git
cp -R haymitch-skills/skills/* ~/.agents/skills/     # ou <votre-projet>/.agents/skills/
```

**Prérequis** : un agent compatible avec la spécification [Agent Skills](https://agentskills.io). Aucun runtime, aucun script externe, aucun binaire caché : uniquement du Markdown clair. Un dépôt `git` est vivement conseillé. Si votre projet n'en a pas, l'initialiser sera votre premier ticket.

> **Astuce** : les commandes `/hay-...` fonctionnent via leur description. Vous pouvez taper `/hay-status` ou simplement demander « où en est-on ? ».

---

## Les 9 commandes

| Commande | Quand la lancer | Ce qu'elle fait |
|---|---|---|
| **`/haymitch`** | Au lancement ou pour cadrer la stack | Porte la méthode, les invariants et les règles d'architecture. |
| **`/hay-feature`** | Devant une idée brute | Pose 3 questions, bâtit une roadmap de 3 à 6 jalons et découpe en tickets. |
| **`/hay-status`** | Pour reprendre le fil | Affiche en 6 lignes maximum votre jalon, votre phase, le pourquoi et la prochaine commande CLI. |
| **`/hay-continue`** | Après avoir terminé une étape | Vérifie la preuve de la phase TDD, avance l'état si elle est suffisante et donne une seule action. |
| **`/hay-debug`** | Bloqué sur un test rouge ou une exception | Décode la cause racine et pose la question qui débloque, sans donner la solution. |
| **`/hay-learn`** | Une notion ou une ligne reste incomprise | Explique progressivement, ligne par ligne si nécessaire, puis rend une micro-action au junior. |
| **`/hay-review`** | Ticket terminé | Rend un verdict binaire, fait créer le commit au junior, le vérifie, puis clôt le ticket. |
| **`/hay-adr`** | Choix technique lourd | Guide la rédaction d'une décision d'architecture, et refuse ce qui n'en mérite pas. |
| **`/hay-help`** | Hésitation sur la marche à suivre | Explique la suite des opérations et oriente vers le bon outil. |

Chaque skill est **autonome**. Installez `/haymitch` en premier : il contient le socle méthodologique complet.

---

## Le flux de travail au quotidien

1. **Cadrer** : une idée floue devient une roadmap de 3 à 6 jalons orientés valeur métier (jamais de jalons horizontaux comme « socle technique »). On traite une tranche à la fois.
2. **Découper** : des tickets *tracer-bullet* qui traversent toutes les couches du système, de l'entrée HTTP jusqu'à la base de données.
3. **Implémenter** : boucle TDD en 4 temps stricts : **contrat → test rouge → code minimal pour passer au vert → refactorisation**. `/hay-continue` contrôle la preuve entre deux phases.
4. **Prouver** : chaque critère d'acceptation se vérifie sur un test qui tourne et réussit devant l'agent.
5. **Clore** : vous proposez puis créez un commit Conventional Commit. Le mentor vérifie le commit, écrit l'état de reprise, puis recommande un nouveau fil avec `/hay-status`.
6. **Consigner** : un choix d'architecture difficile à inverser part aussitôt dans un ADR, pendant que le contexte est encore chaud.

---

## Les traces laissées dans votre projet

| Emplacement | Qui l'écrit | Ce qu'on y trouve |
|---|---|---|
| `docs/MENTORING.md` | l'agent | Un bloc `État courant` compact, la vision, la roadmap et l'index des décisions. |
| `.tickets/NN-nom.md` | vous | Un fichier par ticket, découpé depuis le gabarit et coché sur preuves. |
| `docs/adr/NNNN-nom.md` | vous | Les choix structurants avec leurs alternatives écartées et leurs conséquences. |

Rien d'autre ne pollue votre projet. Le reste vit exclusivement dans les skills.

---

## Bonus 1 : surveillance ciblée dans AGENTS.md

Par défaut, Haymitch intervient quand vous l'appelez. Si vous voulez qu'il garde un œil sur votre code dès qu'une réponse dépend de l'état du projet (pre-flight, blocage TDD, contrôle du diff), ajoutez ce bloc dans l'`AGENTS.md` de votre projet :

```markdown
<!-- BEGIN haymitch : bloc optionnel, à retirer d'un seul geste -->
## Mentorat Haymitch (skill `haymitch`)

Tu es **Haymitch** : le junior code, tu cadres et vérifies. `POLICY.md` du skill fait foi ; les règles du projet restent prioritaires.

1. Réponse dépendante du projet : `git status --short`, `git diff HEAD --stat`, bloc `État courant`, ticket et fichiers utiles. Jamais de diff complet.
2. Production sans test associé : `[STOP TDD]` jusqu'au RED ciblé montré. Exception uniquement pour un incident ou délai prod déclaré.
3. Anti-spoil : dose 1 par défaut. Question vague : objectif, tentative, commande, extrait causal ≤ 40 lignes, résultat attendu.
4. Termine par une seule commande : `/hay-status`, `/hay-continue`, `/hay-debug`, `/hay-learn`, `/hay-feature`, `/hay-review`, `/hay-adr` ou `/hay-help`.
<!-- END haymitch -->
```

---

## Bonus 2 : interdire les commits automatiques

Votre agent supporte la restriction de droits ? Retirez-lui la permission de modifier l'historique git. Ainsi, l'agent ne pourra physiquement jamais committer à votre place. La responsabilité du commit reste entre vos mains.

---

## Frugalité et consommation de tokens

Chaque skill fonctionne comme un aiguilleur : le `SKILL.md` reste court et ne charge ses fichiers de références que si la situation l'exige. Ordres de grandeur indicatifs du texte brut (le tokenizer de l'agent peut varier) :

| Contexte chargé | Tokens consommés |
|---|---|
| Catalogue des 9 descriptions (permanent) | ~400 |
| Commande `/hay-status` | ~600 |
| Commandes `/hay-adr`, `/hay-debug`, `/hay-learn` | ~650 à 850 |
| Commandes `/hay-feature`, `/hay-continue`, `/hay-review` | ~850 à 1 100 |
| Commande `/hay-help` | ~400 |
| `/haymitch` seul | ~1 400 |

Quatre gardes-fous protègent le contexte : aucun diff intégral, extraits de logs limités à 40 lignes, références chargées à la demande et nouveau fil après chaque ticket clôturé.

---

## Compatibilité

La suite s'adapte à plus de 75 agents via la commande [`skills`](https://skills.sh) :

| Environnement | Dossier projet | Dossier global |
|---|---|---|
| Antigravity, Cursor, Codex, Gemini CLI, Copilot, Warp, Zed, Cline... | `.agents/skills/` | `~/.agents/skills/` |
| Claude Code | `.claude/skills/` | `~/.claude/skills/` |

---

## Questions fréquentes

**Mon agent ne voit pas les skills.**  
Vérifiez la présence du fichier `SKILL.md` et de son frontmatter YAML (`name` et `description`). La commande `npx skills list` confirme ce qui est actif.

**Une commande ne répond pas.**  
Les descriptions sont en français. Utilisez des requêtes en français ou tapez le nom du skill (`/hay-status`).

**Haymitch n'intervient pas spontanément.**  
Comportement normal : il attend vos commandes. Pour une surveillance continue à chaque message, intégrez le bloc du bonus 1 dans votre `AGENTS.md`.

---

## Participer

Une suggestion ou un retour d'expérience ? Ouvrez une [issue](https://github.com/GARNIER-Emmanuel/haymitch-skills/issues). Précisez votre stack, votre agent et le comportement observé. Une règle clé : `POLICY.md` est la source de vérité unique. Les autres fichiers pointent vers lui pour éviter toute redondance.

---

## Licence

[MIT](LICENSE) © 2026 Emmanuel GARNIER BOIDUN
