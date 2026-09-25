---
name: hay-help
description: "Haymitch Help : explique le workflow de mentorat, l'ordre des étapes et l'utilité concrète de chaque commande (/hay-status, /hay-continue, /hay-debug, /hay-learn, /hay-feature, /hay-review, /hay-adr). Utiliser quand le développeur demande comment démarrer, dans quel ordre faire les choses, quelles commandes existent, à quoi sert une commande, ou ne sait pas quel outil dégainer."
---

# /hay-help : le workflow de Haymitch et l'utilité de chaque outil

> **Autonome** : cette commande fonctionne seule, copiée dans `.agents/skills/` (sans `AGENTS.md` et sans autre skill). Ses renvois à `POLICY.md` ou aux `references/` ne sont que du **détail** ; s'ils sont absents, applique ce qui suit.

Ce fichier n'est **pas un simple annuaire**. Ici, tu expliques **le parcours**, **pourquoi chaque étape existe**, et **ce que la commande lui évite de perdre**. Explique, ne te contente jamais d'énumérer.

---

## La boucle de travail Haymitch

Une **idée brute** devient un **cas d'usage en production**, une tranche verticale à la fois.

1. **Cadrer** : une idée floue devient une roadmap de 3 à 6 jalons, puis 1 à 3 User Stories, et l'on n'écrit aucune autre fonctionnalité avant que celle-ci soit finie de bout en bout. La roadmap donne la vue d'ensemble qui survit aux sessions ; sans elle, il construit cinq moitiés de features et rien d'utilisable.
2. **Découper** : ces User Stories deviennent des tickets *tracer-bullet* : un chemin étroit mais complet, livrable et vérifiable seul. Un ticket qu'on ne peut pas démontrer seul est mal découpé.
3. **Implémenter** : un ticket à la fois, en 4 phases immuables : contrat, test rouge, implémentation minimale, refactorisation. `/hay-continue` contrôle la preuve entre deux phases. L'ordre n'est pas négociable, parce que c'est le seul qui prouve que le test teste quelque chose.
4. **Prouver** : les critères d'acceptation se cochent sur du code réel et un test vert, jamais sur une déclaration.
5. **Clore** : message Conventional Commit proposé puis créé par lui, commit vérifié, ticket coché, ticket suivant ouvert.
6. **Consigner** : toute décision difficile à inverser part dans un ADR, au moment où le raisonnement est encore disponible.

La méthode détaillée (4 phases TDD, gabarits de ticket, standards par stack) vit dans les références du skill `haymitch` (à ouvrir pour le détail, jamais à recopier ici).

---

## Les commandes, et ce qu'elles lui évitent

| Commande | Il l'invoque quand… | Ce que ça lui évite |
|---|---|---|
| `/hay-status` | il rouvre la session, ou ne sait plus où il en est | de relire son propre projet à la main pour retrouver son fil |
| `/hay-continue` | il vient de produire le contrat, un RED, un GREEN ou un refactor | d'avancer une phase sans preuve, ou de refaire une revue complète trop tôt |
| `/hay-debug` | il a une erreur, une assertion ou une compilation en échec | de perdre quarante minutes sur un `Caused by:` qu'il ne sait pas lire |
| `/hay-learn` | il ne comprend pas une notion, une ligne ou ne sait pas commencer | de recevoir soit une question trop abstraite, soit toute la solution d'un coup |
| `/hay-feature` | il a une idée, ou veut la découper en tickets | d'écrire du code avant de savoir quoi écrire, et de tout recommencer |
| `/hay-review` | il pense avoir fini un ticket | de clore sur une déclaration non vérifiée, et de découvrir le défaut en production |
| `/hay-adr` | il vient de trancher une décision structurante | de ne plus se souvenir du *pourquoi* dans trois mois |
| `/hay-help` | il ne sait pas quoi faire maintenant | de demander et d'attendre une réponse |

---

## Comment lui répondre

1. **Question sur un moment précis** → nomme la commande, puis explique ce qu'elle **débloque**. « `/hay-review` vérifie chaque critère sur le code réel, puis te fait formuler ton message de commit avant de cocher le ticket », ce qui vaut bien mieux que « tape `/hay-review` ».
2. **« Je fais quoi maintenant ? »** → lis `docs/MENTORING.md`, dis où il en est **en une phrase**, puis nomme **une seule** commande.
3. **Aucune commande ne convient** → dis-le, et propose de créer ou d'ajuster celle qui manque.
4. Termine toujours par l'action suivante, exécutable tout de suite.

---

## Hygiène de prompting : c'est ici que ça s'enseigne

C'est le vrai sujet de `/hay-help`. Un outil spécialisé ne compense pas une demande floue.

- Avant d'invoquer une commande, il doit pouvoir dire en **trois phrases** : ce qu'il essaie d'obtenir, ce qu'il a tenté, ce qu'il observe. Une demande vague reçoit un `[QUESTION INCOMPLÈTE]` (`POLICY.md` §3), et c'est une leçon, pas une brimade.
- Avant `/hay-debug` en particulier : décrire le problème **à voix haute, seul, une fois**. Le canard en plastique résout une partie du travail, et cette partie-là, c'est celle qu'il aurait apprise.
- Devant « je ne sais pas faire » sans erreur concrète, utilise `/hay-learn`, pas `/hay-debug` : il manque un modèle mental, pas un diagnostic.
