# Standards Généraux & Hygiène de Code (Toutes Stacks)

Applicable que le code soit en Java, Angular ou React.

---

## 1. Screaming Architecture & Organisation
- **Rejeter formellement le découpage horizontal par couches techniques** (les dossiers fourre-tout `controllers/`, `services/`, `components/`, `reducers/` à la racine).
- **L'arborescence doit crier le domaine métier** et le cas d'usage (ex: `consultations/prise_rdv/`, `clients/creation/`).
- Regrouper les éléments d'une même fonctionnalité ensemble.
- Limiter la portée : ce qui n'a pas besoin d'être exporté ou public hors de la feature doit rester privé ou package-private.

---

## 2. Règle TDD Stricte (Red → Green → Refactor)
- **Le test s'écrit TOUJOURS avant l'implémentation.** Le déclenchement du `[STOP TDD]` et son échappatoire vivent dans `POLICY.md` §2 : ne les redéfinis pas ici.
- Un test valide teste le comportement observable depuis l'extérieur (contrat d'API ou interaction utilisateur), jamais les détails d'implémentation internes ou les méthodes privées.
- Un test qui n'asserte rien n'est pas un test.
- Un test qui ne compile pas n'est pas un RED : c'est une erreur de test, et la corriger fait partie de la phase 2.

---

## 3. Sécurité & Secrets
- **Zéro secret dans le dépôt** : ni token, ni mot de passe, ni clé API (même en commentaire).
- Tout secret doit être injecté par variables d'environnement (`.env.example` versionné, `.env` dans `.gitignore`).
- Entrées validées systématiquement à la frontière du système (serveur et client).

---

## 4. Git & Clôture de Ticket
- Commits atomiques rédigés au format **Conventional Commits** :
  - `feat(scope): ...`
  - `fix(scope): ...`
  - `refactor(scope): ...`
  - `test(scope): ...`
- **Exigence avant clôture** : le junior formule le message, crée lui-même le commit, puis le Lead vérifie `git log -1 --oneline` et `git status --short` avant de cocher le ticket dans `docs/MENTORING.md`.
- Un commit atomique par ticket vert est la valeur par défaut. Ne committe ni ne pousse une phase RED. Le push intervient sur une branche de travail après un ticket vert ou en fin de session, seulement si un remote existe.
- Zéro code mort, zéro code commenté dans le dépôt.
