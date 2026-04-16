# Plan de normalisation et d'identification

## 1. Entités prioritaires

| Type d'entité | Pourquoi est-il prioritaire ?             | Identifiant actuel | Stratégie proposée  |
| ------------- | ----------------------------------------- | ------------------ | ------------------- |
| Etablissement | c'est le sujet du dataset                 | record_id          | construire des URI  |
| Ville         | localiser chaque etablissement            | city               | Normaliser les noms |
| site web      | identifier le site unique de chaque ecole | site web           |                     |

## 2. Champs à normaliser

| Champ            | Problème observé                        | Règle de normalisation proposée                      | Impact attendu |
| ---------------- | --------------------------------------- | ---------------------------------------------------- | -------------- |
| institution_name | absence d'accent                        | restaurer les accents via UTF-8 correcte             |                |
| main_filed       | deux langue anglais et francais         | Aligner sur la classification ISCED-F 2013           |                |
| city             | des faute(marakesh au lieu de marakech) | normaliser sur la liste officiel des villes du maroc |                |

## 3. Stratégie d'identifiants

| Entité cible  | Base de construction envisagée | Risque                                   | Recommandation                   |
| ------------- | ------------------------------ | ---------------------------------------- | -------------------------------- |
| etablissement |                                |                                          |                                  |
| Ville         | short_name en miniscul+ ville  | deux ecole avec meme nom dans meme ville | ajouter un identifiant apres(-1) |
|               |                                |                                          |                                  |

## 4. Risques et limites

- Quels champs sont trop faibles pour servir d'identifiant ?
  country → valeur constante "Morocco", ne différencie rien
  portal_hint → valeur identique pour toutes les lignes, inutile
- Quelles collisions ou ambiguïtés sont possibles ?
  short_name deux ecole avec meme nom peut exister dans la meme ville(ENSA)
  Le nom de ville "Marrakesh" vs "Marrakech" peut creer deux entites distinctes dans un graphe si non normalise
- Quelles informations supplémentaires seraient nécessaires ?
  Plus de coordonnes GPS pour localiser mieux le lieu d'une ecole
