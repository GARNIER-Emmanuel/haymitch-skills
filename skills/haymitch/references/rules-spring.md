# Standards de Code : Java 21 & Spring Boot 3+

Applicable dès qu'un fichier `.java` ou un fichier de build Maven/Gradle est concerné.

---

## 1. Modèle & DTOs
- **Java Records** obligatoires pour tous les DTOs (requêtes, réponses, événements).
- **Zéro fuite d'entité JPA** dans la couche Web (ne jamais exposer `@Entity` dans un `@RestController`).
- **Lombok avec précaution** : Interdire `@Data` ou `@ToString` sur les entités JPA avec relations bidirectionnelles (`StackOverflowError` garanti lors de l'appel à `hashCode`/`toString`). Préférer `@Getter`, `@Setter`, et constructeur explicite.

---

## 2. Couche Service & Injection
- **Injection par constructeur uniquement** : Rejeter formellement `@Autowired` sur les attributs (field injection). Impact : impossibilité de tester unitairement sans instancier le contexte Spring, et violation de l'immuabilité.
- **Gestion stricte des transactions** :
  - `@Transactional(readOnly = true)` au niveau classe pour sécuriser la lecture.
  - `@Transactional` explicite sur les méthodes qui modifient l'état.
  - Pas d'appels HTTP distants bloquants ou de traitements lourds à l'intérieur d'une transaction active (blocage des connexions du pool HikariCP).

---

## 3. Couche Contrôleur & API REST
- Contrôleurs ultra-légers : aucune règle métier, aucune requête SQL/Repository directe.
- Validation automatique obligatoire : `@Valid` sur tout corps de requête.
- Statuts HTTP sémantiques : `201 Created` (avec header Location ou body), `200 OK`, `204 No Content`, `400 Bad Request`, `404 Not Found`.
- Collections paginées : une liste exposée sans pagination est un incident en attente.

---

## 4. Gestion des Erreurs
- Pas de `try/catch` vide ou de `e.printStackTrace()`.
- Utilisation de `@RestControllerAdvice` avec gestion des exceptions spécifiques.
- Format standard : RFC 9457 `ProblemDetail` (ou DTO d'erreur standardisé avec timestamp, status, error, message).
- **Ne jamais exposer de stacktrace interne au client HTTP** (risque de sécurité).

---

## 5. Requêtage BDD & Performances
- Attention au **problème N+1** : repérer les relations `@ManyToOne` ou `@OneToMany` chargées en boucle dans les requêtes.
- Suggérer `@EntityGraph` ou `JOIN FETCH` quand un cas N+1 potentiel est identifié.
- Index sur les colonnes filtrées et sur les clés étrangères dès qu'une requête les utilise.

---

## 6. Tests & CLI TDD
- Test d'intégration d'API avec `MockMvc` ou `Testcontainers` ; test unitaire sans contexte Spring pour une règle métier isolée.
- Nommer le test par le comportement attendu (`shouldReturn201WhenSlotIsValid`).
- Commande CLI ciblée à faire exécuter au junior :
  - Maven : `./mvnw test -Dtest=NomDuTest`
  - Gradle : `./gradlew test --tests NomDuTest`
