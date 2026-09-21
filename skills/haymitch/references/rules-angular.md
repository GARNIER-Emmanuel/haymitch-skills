# Standards de Code : Angular (17 - 19+)

Applicable dès qu'un fichier Angular (`.component.ts`, `.service.ts`, `angular.json`) est concerné.

---

## 1. Architecture des Composants (Modern Angular)
- **Standalone Components uniquement** : Tout composant, directive ou pipe doit être `standalone: true`. Rejeter formellement les `NgModule` (obsolètes).
- **Stratégie de détection de changement** : `ChangeDetectionStrategy.OnPush` obligatoire sur tous les composants pour des performances optimales et l'anticipation du Zoneless.
- **Nouvelle syntaxe du Control Flow** : Utiliser impérativement le control flow natif (`@if`, `@for`, `@switch`) au lieu des anciennes directives structurelles (`*ngIf`, `*ngFor`).
- **Encapsulation par Feature** : Regrouper le composant, son template `.html`, ses styles `.css` et son fichier de test `.spec.ts` dans le même dossier de feature.

---

## 2. Gestion de l'État & Réactivité (Signals)
- **Signals natifs prioritaires** : Préférer les **Signals** (`signal()`, `computed()`) pour l'état local et la synchronisation de l'UI.
- **RxJS avec parcimonie** : Réserver RxJS aux opérations asynchrones complexes (debounce, requêtes HTTP annulables, websocket). Convertir les Observables en Signals via `toSignal()` dans le composant.
- **Pas de souscription manuelle non nettoyée** : Rejeter tout `.subscribe()` dans un composant sans désinscription automatique (`takeUntilDestroyed()`). Préférer le pipe `async` ou les Signals.

---

## 3. Injection de Dépendances
- **Utiliser `inject()`** au lieu de l'injection lourde par constructeur :
  ```typescript
  private readonly clientService = inject(ClientService);
  ```
- Services injectés en `providedIn: 'root'` pour les singletons globaux, ou fournis au niveau du composant de feature pour un cycle de vie restreint.

---

## 4. Formulaires & Validation
- Utiliser les **Reactive Forms fortement typés** (`FormGroup`, `FormControl` typés).
- Pas de `any` dans les formulaires.
- Validation explicite à l'écran (messages d'erreurs clairs basés sur les erreurs du validateur).

---

## 5. TypeScript & Sécurité
- Mode `strict: true` exigé.
- **Interdiction formelle du type `any`** : Exiger des `interface` ou `type` précis pour chaque modèle de données.
- Ne jamais injecter de HTML brut avec `[innerHTML]` sans passer par `DomSanitizer` (risque XSS).

---

## 6. Tests & CLI TDD
- Écrire le test unitaire du composant ou du service **AVANT** le code d'implémentation (TDD).
- Commande CLI ciblée à faire exécuter au junior :
  ```bash
  ng test --include="src/app/features/clients/**/*.spec.ts"
  ```
