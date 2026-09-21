# Gabarit d'ADR (Architecture Decision Record)

Un ADR enregistre **qu'**une décision a été prise, et **pourquoi**. Sa valeur est là : le code garde le *quoi*, il ne garde jamais le *pourquoi*.

Les ADR vivent dans `docs/adr/`, un fichier par décision : `NNNN-nom-court.md`. Crée le dossier au premier ADR seulement. Pour numéroter, prends le plus grand numéro existant et incrémente.

---

## Quand en écrire un

Les trois conditions doivent être vraies **en même temps** :

1. **Difficile à inverser** : revenir dessus coûte cher.
2. **Surprenant sans contexte** : un lecteur futur se demandera pourquoi.
3. **Vrai arbitrage** : il existait des alternatives réelles, et l'une a été choisie pour des raisons précises.

Sinon, pas d'ADR : une décision facile à inverser sera inversée, et une décision évidente n'a rien à consigner.

---

## Gabarit

```md
# ADR-NNNN : <la décision en quelques mots>

## Contexte & Problème

<Le besoin métier ou technique qui force un choix. Deux à quatre phrases.>

## Décision retenue

<La techno, le pattern ou la règle retenus, et ce que ça implique concrètement.>

## Alternatives rejetées & Raisons

- **<alternative>** : <pourquoi elle a été écartée>
- **<alternative>** : <pourquoi elle a été écartée>

<Au moins une vraie alternative. Si aucune n'existait, ce n'est pas un ADR.>

## Conséquences

- <ce que la décision simplifie ou rend possible>
- <la contrainte ou la dette qu'elle induit>
```

Ces quatre sections sont le format attendu pour une décision structurante. Mais **un ADR peut tenir en un paragraphe** : l'essentiel est de consigner *qu'*une décision a été prise et *pourquoi*, pas de remplir des rubriques.

---

## Qui écrit l'ADR

Le **junior** rédige, le **Lead** challenge. L'ADR s'écrit **au moment de la décision**, jamais rétroactivement : c'est le moment où le raisonnement est encore disponible, et c'est ce qui oblige à le formuler.

Un ADR accepté ne se modifie pas. S'il est dépassé, écris-en un nouveau qui le remplace, et note la filiation dans son contexte.
