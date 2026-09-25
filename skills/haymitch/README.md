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

Neuf skills indépendants, un dossier chacun. L'agent les découvre par leur description : ils se déclenchent aussi bien par `/hay-status` que par une phrase du genre « où j'en suis ? ».

| Dossier | Ce qu'il apporte |
|---|---|
| `haymitch` | La méthode : cadrage, roadmap par jalons, tranche verticale, 4 phases TDD, standards par stack. Porte `POLICY.md`, la politique normative. |
| `hay-help` | Explique le workflow et l'utilité de chaque commande |
| `hay-status` | Où il en est, et la commande exacte à lancer |
| `hay-continue` | Vérifier la preuve d'une phase TDD et avancer l'état |
| `hay-debug` | Débloquer une erreur sans donner la solution |
| `hay-learn` | Comprendre une notion ou du code, avec une progression pédagogique |
| `hay-feature` | Idée brute → User Stories → tickets |
| `hay-review` | Verdict binaire sur les critères, puis clôture |
| `hay-adr` | Consigner une décision difficile à inverser |

Copie `haymitch` en priorité : c'est lui qui porte la méthode et la politique. Les huit autres fonctionnent seuls (leurs renvois vers ses références ne sont que du détail).

## Autonomie : rien d'autre à installer

- **Chaque skill fonctionne seul**, dès que son dossier est copié.
- **Les invariants vivent dans `POLICY.md`, à l'intérieur du skill** (pas dans un fichier de ton projet).
- Les renvois vers `POLICY.md` ou vers `references/` ne sont que du **détail**. S'ils sont absents, le skill reste opérationnel : applique ce qu'il décrit dans son corps.
- **L'installation n'écrit rien** en dehors du dossier du skill, et ne dépend d'aucune configuration de l'agent hôte. À l'usage, le mentor ne crée que trois choses dans ton projet : `docs/MENTORING.md`, `.tickets/` et `docs/adr/`.
- **Après chaque ticket**, l'état écrit permet de repartir dans un nouveau fil avec `/hay-status`, sans transporter l'ancien historique.

## Bonus optionnel : le gardien permanent

Par défaut, la méthode s'applique quand une commande est invoquée, ou quand l'agent charge le skill d'après sa description.

Si tu veux que Haymitch surveille les demandes qui dépendent du projet, ajoute ce bloc compact à ton `AGENTS.md`. Il est injecté à chaque tour : garde-le court.

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

Le même contenu en version longue et normative est dans `POLICY.md`.

### Second bonus optionnel : empêcher l'agent de committer

Si ton agent sait restreindre ses permissions (refus de l'écriture de l'historique git), la règle « le commit est le sien » devient inviolable : l'agent ne *peut pas* committer à la place du développeur, même si on le lui demande. À fusionner à la main dans ta configuration : le skill ne touche à rien.

## Désinstaller

Supprime le dossier. Si tu avais ajouté le bloc bonus, retire-le de ton `AGENTS.md` : c'est toi qui l'as mis, c'est toi qui l'enlèves.
