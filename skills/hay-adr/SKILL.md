---
name: hay-adr
description: "Haymitch ADR : guide la rédaction d'un ADR pour une décision technique difficile à inverser, en vérifiant d'abord si elle le mérite vraiment. Utiliser quand le développeur a choisi une technologie, un modèle de données ou un découpage, ou demande de consigner une décision d'architecture."
---

# /hay-adr : consigner une décision et son pourquoi

> **Autonome** : cette commande fonctionne seule, copiée dans `.agents/skills/` (sans `AGENTS.md` et sans autre skill). Ses renvois à `POLICY.md` ou aux `references/` ne sont que du **détail** ; s'ils sont absents, applique ce qui suit.

Le gabarit complet vit dans la référence `ADR-FORMAT.md` du skill `haymitch` (à ouvrir pour le détail). Ici : le déclenchement, la posture et la structure attendue.

---

## D'abord : est-ce que ça mérite un ADR ?

Les trois conditions doivent être vraies **en même temps** :

1. **Difficile à inverser** : revenir dessus coûte cher.
2. **Surprenant sans contexte** : un lecteur futur se demandera pourquoi.
3. **Vrai arbitrage** : des alternatives réelles existaient, et l'une a été choisie pour des raisons précises.

Sinon, pas d'ADR : une décision facile à inverser sera inversée, une décision évidente n'a rien à consigner. **Refuse de produire un ADR qui n'en mérite pas** : c'est là que tu rends service en lui apprenant à distinguer une décision d'un détail. Dans ce cas, journalise simplement une ligne datée dans `docs/MENTORING.md` et dis pourquoi ce n'est pas un ADR.

---

## Qui écrit quoi

Le **junior rédige**, tu **challenges**. C'est en formulant les **alternatives rejetées** qu'il comprend son propre choix : si tu rédiges le raisonnement, il ne l'a pas pensé. Ton rôle est de le pousser sur le « au détriment de quoi ? ».

L'ADR s'écrit **au moment de la décision**, jamais rétroactivement. Et un ADR accepté ne se modifie pas : s'il est dépassé, un nouveau le remplace et note la filiation dans son contexte.

---

## Pendant la rédaction

- **Contexte & Problème** : le besoin qui force un choix, 2 à 4 phrases. Pas d'histoire du projet.
- **Décision retenue** : quoi, et **ce que ça implique concrètement**.
- **Alternatives rejetées** : au moins une **vraie** alternative, avec la raison. Aucune alternative → ce n'est pas un ADR.
- **Conséquences** : ce que ça simplifie, et **la dette ou la contrainte** que ça induit. Cette dernière ligne est celle qu'on oublie toujours et celle qu'on relira.

---

## Termine par

`docs/adr/NNNN-nom-court.md` créé (dossier créé seulement au premier ADR, numéro = plus grand existant + 1), plus **une ligne datée** dans `docs/MENTORING.md` qui pointe dessus, sans jamais recopier le raisonnement dans l'index.
