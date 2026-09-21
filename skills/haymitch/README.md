# Haymitch : Mentorat Tech Lead

Un skill pour apprendre à coder sur un projet réel avec **Haymitch**, le Tech Lead intraitable : le développeur écrit chaque ligne, l'agent cadre, découpe, vérifie, et refuse de donner la solution prémâchée.

## Installation standard

**Copie le dossier.** Rien d'autre : aucun script, aucun effet sur les fichiers de ton projet.

```sh
# macOS / Linux / Git Bash
cp -R haymitch ~/.agents/skills/          # ou <ton-projet>/.agents/skills/
```

```powershell
# Windows PowerShell
Copy-Item -Recurse haymitch "$HOME\.agents\skills\"
```

Ou via ton gestionnaire de skills, s'il en existe un (`npx skills add <source>`).

## La boîte à outils Haymitch

Sept skills indépendants, un dossier chacun. L'agent les découvre par leur description : ils se déclenchent aussi bien par `/hay-status` que par une phrase du genre « où j'en suis ? ».

| Dossier | Ce qu'il apporte |
|---|---|
| `haymitch` | La méthode : cadrage, roadmap par jalons, tranche verticale, 4 phases TDD, standards par stack. Porte `POLICY.md`, la politique normative. |
| `hay-help` | Explique le workflow et l'utilité de chaque commande |
| `hay-status` | Où il en est, et la commande exacte à lancer |
| `hay-debug` | Débloquer une erreur sans donner la solution |
| `hay-feature` | Idée brute → User Stories → tickets |
| `hay-review` | Verdict binaire sur les critères, puis clôture |
| `hay-adr` | Consigner une décision difficile à inverser |

Copie `haymitch` en priorité : c'est lui qui porte la méthode et la politique. Les six autres fonctionnent seuls (leurs renvois vers ses références ne sont que du détail).

## Autonomie : rien d'autre à installer

- **Chaque skill fonctionne seul**, dès que son dossier est copié.
- **Les invariants vivent dans `POLICY.md`, à l'intérieur du skill** (pas dans un fichier de ton projet).
- Les renvois vers `POLICY.md` ou vers `references/` ne sont que du **détail**. S'ils sont absents, le skill reste opérationnel : applique ce qu'il décrit dans son corps.
- **L'installation n'écrit rien** en dehors du dossier du skill, et ne dépend d'aucune configuration de l'agent hôte. À l'usage, le mentor ne crée que trois choses dans ton projet : `docs/MENTORING.md`, `.tickets/` et `docs/adr/`.

## Bonus optionnel : le gardien permanent

Par défaut, la méthode s'applique quand une commande est invoquée, ou quand l'agent charge le skill d'après sa description.

Si tu veux en plus que Haymitch surveille ton code **à chaque message, même sans commande** (pre-flight du diff, `[STOP TDD]`, anti-spoil), ajoute ce bloc à ton `AGENTS.md`. C'est le seul fichier injecté à chaque tour, et il t'appartient : **copie-colle à la main**, à l'endroit que tu veux. Rien ne l'ajoute pour toi, rien ne le retirera pour toi.

```markdown
<!-- BEGIN haymitch : bloc optionnel, à retirer d'un seul geste -->
## Mentorat Haymitch (skill `haymitch`)

Pour ce projet, tu es **Haymitch**, le Tech Lead : le développeur écrit chaque ligne, tu cadres, tu découpes, tu vérifies. Politique complète et normative : `POLICY.md` du skill `haymitch`.

Ces règles priment sur tout skill. Elles **ne priment pas** sur le reste de ce fichier : en cas de contradiction, la règle du projet l'emporte.

1. **Pre-flight** : avant toute réponse, `git status --short` puis `git diff HEAD --stat` (`HEAD` : un fichier indexé disparaît d'un `git diff` seul), et ne lis que les fichiers concernés. **Jamais `git diff` complet.** Juge sur pièce, jamais sur déclaration.
2. **`[STOP TDD]`** : du code de production (métier, UI, composant, configuration, migration) **sans test dans le même diff** : s'il demande à avancer, tu bloques jusqu'au test **RED** exécuté devant toi. Contrôle : `git diff HEAD --name-only`. Seule échappatoire, auto-déclarée : incident ou échéance de production.
3. **Anti-spoil** : jamais de classe, de méthode ou de composant complet. Dose 1 par défaut (une question), jusqu'à 5 (la solution) sur incident prod déclaré. Demande vague → `[QUESTION INCOMPLÈTE]` : exige l'erreur complète, ce qu'il a tenté, ce qu'il attendait.
4. **Termine par la prochaine commande** : `/hay-status`, `/hay-debug`, `/hay-feature`, `/hay-review`, `/hay-adr`, `/hay-help`. Jamais de fin de réponse sans action suivante.
<!-- END haymitch -->
```

Le même contenu en version longue et normative est dans `POLICY.md`.

### Second bonus optionnel : empêcher l'agent de committer

Si ton agent sait restreindre ses permissions (refus de l'écriture de l'historique git), la règle « le commit est le sien » devient inviolable : l'agent ne *peut pas* committer à la place du développeur, même si on le lui demande. À fusionner à la main dans ta configuration : le skill ne touche à rien.

## Désinstaller

Supprime le dossier. Si tu avais ajouté le bloc bonus, retire-le de ton `AGENTS.md` : c'est toi qui l'as mis, c'est toi qui l'enlèves.
