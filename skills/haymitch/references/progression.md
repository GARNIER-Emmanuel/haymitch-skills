# État de Progression : `docs/MENTORING.md`

L'état vit dans le projet de l'étudiant, pas dans le skill. C'est lui qui traverse les sessions : grâce à lui le mentor reprend à la phase exacte, et l'étudiant garde la trace des raisons derrière ses choix.

Chemin par défaut : `docs/MENTORING.md`, à la racine du projet.

---

## Format

```markdown
# Mentorat : <nom du projet>

## Intention métier & vision
<le problème résolu, dans les mots de l'étudiant, et pour qui (2 à 4 phrases)>

## Roadmap & jalons
<3 à 6 jalons, une capacité démontrable par ligne, sans date ni estimation.
Un seul jalon porte le marqueur « en cours ». Lien unidirectionnel : ici les
numéros de tickets, jamais leur contenu.>
- [x] **J1 : <capacité>** (walking skeleton), tickets 01 → 02
- [ ] **J2 : <capacité>** 👈 en cours, tickets 03 → 05
- [ ] **J3 : <capacité>** (à découper)

## Ticket en cours
- **Fichier** : `.tickets/NN-nom-court.md`
- **Phase TDD** : <1 à 4> (<nom de la phase>)
- **Signal attendu** : <ce qu'il doit montrer pour valider cette phase>

## Phases TDD du ticket en cours
- [ ] 1. Contrat (DTO Record + Validation)
- [ ] 2. Test d'abord : RED (le test échoue, et le RED a été montré)
- [ ] 3. Implémentation minimale : GREEN
- [ ] 4. Refactorisation & Robustesse

## Tickets
- [ ] 01-nom-court
- [ ] 02-nom-court (bloqué par 01)

## Décisions prises
- <AAAA-MM-JJ> <décision> : <la raison, ou le renvoi vers un ADR de `docs/adr/`>
```

---

## Règles de mise à jour

- **En début de session** : lis le fichier avant toute question. Un cadrage déjà consigné ne se redemande pas, et le ticket en cours te dit où reprendre.
- **S'il est absent** : premier échange. Tu crées le fichier, tu remplis l'intention et la vision depuis les 3 questions de cadrage, tu proposes la roadmap (cf. [vertical-slice-workflow.md](./vertical-slice-workflow.md) Phase 0) ; tu lui fais générer les tickets dans `.tickets/` (cf. [ticket-template.md](./ticket-template.md)), puis tu vérifies les fichiers produits. C'est ton fichier à toi : lui ne rédige que les tickets.
- **À chaque clôture de jalon** : coche le jalon, déplace le marqueur « en cours » sur le suivant, puis découpe son premier ticket.
- **La roadmap se révise** : un jalon mal placé se corrige, et tu dis pourquoi. La réviser n'est pas un échec, c'est le travail.
- **Ce qui ne va jamais dans la roadmap** : le contenu des tickets, les dates, les estimations et le raisonnement (un séquençage difficile à inverser est un ADR, cf. [ADR-FORMAT.md](./ADR-FORMAT.md)).
- **Compatibilité** : un `MENTORING.md` existant sans section roadmap ne bloque rien, et ne justifie pas de reposer le cadrage : propose de la compléter à la prochaine clôture de jalon.
- **À chaque phase franchie** : coche-la, avance la phase courante, et réécris le **signal attendu** pour qu'il porte sur la phase suivante. La phase 2 ne se coche que si le RED a été montré : un test écrit après le code ne la valide pas.
- **À chaque ticket terminé** : coche son entrée dans la liste, puis ouvre le ticket dont tous les prérequis sont satisfaits.
- **À chaque décision** : ajoute une ligne datée. Si elle franchit les trois conditions de [ADR-FORMAT.md](./ADR-FORMAT.md), c'est un ADR : écris-le dans `docs/adr/` et fais pointer la ligne dessus, plutôt que d'y recopier le raisonnement.

---

## Pourquoi les décisions sont datées

Un étudiant qui relit son projet trois mois plus tard ne se demande pas *quoi* il a codé : le code est là. Il se demande *pourquoi* ce type, cette bibliothèque, ce découpage. Le journal des décisions répond à cette question, et il impose au passage la justification au moment du choix, c'est-à-dire au moment précis où le mentor doit la demander.

Ce journal reste un **index** : une ligne par décision. Les décisions lourdes ont en plus leur ADR dans `docs/adr/`, où vit le raisonnement complet. L'index dit *quand* et *quoi* ; l'ADR dit *pourquoi en détail*, et au détriment de quoi.
