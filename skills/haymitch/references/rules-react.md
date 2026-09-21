# Standards de Code : React (18 - 19+)

Applicable dès qu'un fichier React (`.tsx`, `.jsx`, ou composant React) est concerné.

---

## 1. Architecture des Composants & Responsabilité Unique
- **Composants Fonctionnels uniquement** : Aucun composant classe n'est toléré.
- **Séparation Stricte (Présentation vs Logique)** :
  - Le composant d'UI ne gère QUE le rendu visuel et les événements utilisateurs directs.
  - La logique métier, la gestion des états complexes et les appels API doivent être isolés dans des **Custom Hooks** dédiés (ex: `useCreateClient()`).
- **Petits composants composables** : Rejeter les composants "monolithes" de plus de 150 lignes. Découper en sous-composants réutilisables.

---

## 2. Gestion de l'État & Immuabilité
- **Immuabilité absolue** : Interdiction totale de muter un état directement (`state.push(...)`, `state.x = y`). Toujours utiliser les fonctions de mise à jour d'état ou le pattern de déstructuration (`[...prev, newItem]`, `{ ...prev, key: val }`).
- **Éviter le sur-stockage dans `useState`** : Si une valeur peut être calculée à partir des props ou d'un état existant, ne pas créer un état supplémentaire (calcul direct ou `useMemo` si lourd).
- **Règles des Hooks** :
  - Pas d'appels conditionnels aux hooks (`if (...) { useEffect(...) }`).
  - Tableaux de dépendances d'`useEffect`, `useCallback` et `useMemo` exhaustifs et surveillés (interdiction de tricher avec eslint-disable sans justification ADR).

---

## 3. Typage TypeScript Strict
- Typage explicite des `Props` de chaque composant via une `interface` ou un `type` dédié.
- Éviter `React.FC` désuet ; préférer le typage direct des props :
  ```typescript
  interface ClientCardProps {
    readonly id: string;
    readonly name: string;
    readonly onSelect: (id: string) => void;
  }

  export function ClientCard({ id, name, onSelect }: ClientCardProps) { ... }
  ```
- **Zéro `any`** : Modéliser les réponses API et les événements précisément.

---

## 4. Gestion des Formulaires & Validation
- Préférer les formulaires non contrôlés ou les bibliothèques éprouvées (**React Hook Form** ou **TanStack Form**) associées à un schéma de validation (**Zod**).
- Validation précoce et messages d'erreur accessibles.

---

## 5. Tests & CLI TDD
- Utiliser **React Testing Library** + **Vitest** (ou Jest).
- **Règle d'or de RTL** : Tester le comportement tel que l'utilisateur le perçoit (`screen.getByRole('button', { name: /valider/i })`), ne jamais tester les états internes ou les props.
- Écrire le test d'interaction utilisateur **AVANT** le composant (TDD).
- Commande CLI ciblée à faire exécuter au junior :
  ```bash
  npm test -- src/features/clients/ClientCard.test.tsx
  ```
