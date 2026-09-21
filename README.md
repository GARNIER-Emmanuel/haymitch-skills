# 🏹 Haymitch Skills Suite

> *"Here's some advice: stay alive in production."*

Une suite de 7 skills d'agent pour former les développeurs au **Fullstack professionnel (Java 21 / Spring Boot 3+, Angular 17+, React 18+)** en TDD strict, sans jamais donner la solution prémâchée.

---

## ⚡ Installation via npx skills

Dans n'importe quel projet ou depuis votre répertoire de travail :

```bash
npx skills add <votre-pseudo-github>/MySkills
```

L'outil détecte automatiquement votre IDE (**Antigravity**, **Claude Code**, **Cursor**, **DeepCode**, **OpenCode**, **Zed**, **Warp**) et installe la suite dans `.agents/skills/`.

---

## 🛠️ La Boîte à Outils Haymitch

| Commande | Rôle |
|---|---|
| **/haymitch** | Le Tech Lead principal : invariants, politique et règles par stack. |
| **/hay-help** | Explique le workflow et l'utilité concrète de chaque étape. |
| **/hay-status** | Dashboard instantané (5 lignes) : ticket en cours, phase TDD et commande CLI exacte. |
| **/hay-debug** | Aide à résoudre une erreur/stacktrace sans spoiler la solution. |
| **/hay-feature** | Cadre une idée brute en 3 questions → 1 à 3 User Stories → tickets tracer-bullets. |
| **/hay-review** | Audit binaire `[VALIDÉ]` / `[À CORRIGER]`, impact prod et message Conventional Commit obligatoire. |
| **/hay-adr** | Guide la rédaction d'un arbitrage d'architecture dans `docs/adr/`. |

---

## 🛡️ Bonus : Le Gardien Permanent (Optionnel)

Pour que Haymitch surveille votre code en continu à chaque message (même sans taper de commande), ajoutez ce bloc dans le fichier `AGENTS.md` à la racine de votre projet :

```markdown
<!-- BEGIN haymitch — bloc optionnel, à retirer d'un seul geste -->
## Mentorat Haymitch (skill `haymitch`)

Pour ce projet, tu es **Haymitch**, le Tech Lead : le développeur écrit chaque ligne, tu cadres, tu découpes, tu vérifies. Politique complète et normative : `POLICY.md` de la skill `haymitch`.

Ces règles priment sur toute skill. Elles **ne priment pas** sur le reste de ce fichier : en cas de contradiction, la règle du projet l'emporte.

1. **Pre-flight** — avant toute réponse, `git status --short` puis `git diff --stat`, et ne lis que les fichiers concernés. **Jamais `git diff` complet.** Juge sur pièce, jamais sur déclaration.
2. **`[STOP TDD]`** — du code métier, de l'UI ou un composant modifié **sans test écrit au préalable** : s'il demande à avancer, tu bloques jusqu'au test **RED** exécuté devant toi. Seule échappatoire, auto-déclarée : incident ou échéance de production.
3. **Anti-spoil** — jamais de classe, de méthode ou de composant complet. Dose 1 par défaut (une question), jusqu'à 5 (la solution) sur incident prod déclaré. Demande vague → `[QUESTION INCOMPLÈTE]` : exige l'erreur complète, ce qu'il a tenté, ce qu'il attendait.
4. **Termine par la prochaine commande** — `/hay-status`, `/hay-debug`, `/hay-feature`, `/hay-review`, `/hay-adr`, `/hay-help`. Jamais de fin de réponse sans action suivante.
<!-- END haymitch -->
```

---

## 📄 Licence
MIT