# Fiche d'analyse du jeu de données

## Identification

- **Groupe** :group
- **Date** :09/04/2026
- **Nom du jeu de données** : higher_education_sample
- **Source / producteur** :portail data.gov.ma
- **URL de la source** :https://data.gov.ma
- **Domaine métier** : Enseignement supérieur public au Maroc

## Description générale

- **Objectif du jeu de données** : Represente les ecoles qui se trouve dans le maroc son nom short data de creation et leur site
- **Format(s) disponible(s)** :csv
- **Langue(s)** :Francais, Anglais
- **Licence** : non indiquer dans le fichier
- **Fréquence de mise à jour** : non indiquer
- **Unité d'observation** :
- **Granularité des enregistrements** :fine, chaque ligne= etablissement unique

## Structure du jeu de données

| Champ / colonne | Signification | Exemple de valeur | Observation |
| record_id | numero de ligne| 2 | il augmente de facon croissante = compteur |
|institution_name | nom de l'ecole| Ecole national de l'informatique et analyse de systeme|ENSIAS|Pas d'accent
| short_name | abriviation de nom de l'ecole |ENSIAS | |
|city|ville ou l'ecole se trouve| Rabat | |
|country|pay ou l'ecole se trouve|Morocco|tout les lignes avec meme country morocco
|website|site web de l'ecole| https://www.ensias.um5.ac.ma|
|institution_type|type de l'institution|public school|
|main_field|champs principal|computer science
|year_created| annee de creation de l'ecole| 1992
|portal_hint|source de data| data.gov.ma| tjrs la meme valeur dans tout les lignes

## Évaluation "Open Data"

| Critère                | Observation                       | Score / 5 |
| ---------------------- | --------------------------------- | --------- |
| Accessibilité          | data se forme csv bien organiser  | 4/5       |
| Réutilisabilité        | il ya de colonne avec meme valeur | 3/5       |
| Documentation          |                                   |           |
| Format exploitable     | csv                               | 4/5       |
| Présence d'une licence | pas indiquer dans le fichier      | 3/4       |

## Évaluation "Linked Data readiness"

| Point observé                                      | Oui / Non / Partiel | Commentaire                                |
| -------------------------------------------------- | ------------------- | ------------------------------------------ |
| Identifiants stables pour les enregistrements      | non                 |                                            |
| Entités clairement distinguables                   | Partiel             |                                            |
| Valeurs normalisées                                | partiel             | il ya ligne non normaliser                 |
| Informations géographiques exploitables            | oui                 | presence de ville de chaquee etablissement |
| Possibilité de lien vers des référentiels externes | oui                 | il existe dans table de lien externe       |
| Présence de clés candidates plausibles             | partiel             | short_name + city                          |
| Présence de codes ou nomenclatures réutilisables   | Non                 |                                            |

## Maturité "5 étoiles"

| Niveau                                             | Atteint ? | Justification                     |
| -------------------------------------------------- | --------- | --------------------------------- |
| 1 étoile : données disponibles sur le Web          | oui       | Publie sur data.gov.ma            |
| 2 étoiles : données structurées                    | oui       | se forme csv                      |
| 3 étoiles : format non propriétaire                | oui       | csv format ouvert                 |
| 4 étoiles : usage d'URI pour identifier les choses | Non       | Aucun URI present dans le fichier |
| 5 étoiles : liens vers d'autres données            | Non       | Aucun liaison externe             |

## Clés candidates et identifiants

| Objet ou entité cible | Champ(s) candidat(s) | Fiabilité | Limites                                       | Recommandation |
| --------------------- | -------------------- | --------- | --------------------------------------------- | -------------- |
| Etablissement         | short_name           | Moyenne   | Deux etablissement peut avoir meme briviation |                |
| ville                 | city                 | Moyenne   |                                               |                |
| Pays                  | country              | Moyenne   | tjrs le meme = Morocco                        |                |

## Normalisation préalable nécessaire

| Champ | Problème observé     | Impact pour le LOD     | Action recommandée                          |
| ----- | -------------------- | ---------------------- | ------------------------------------------- |
| Ville | faute d'horthographe | va contenir des fautes | Normaliser sur des donnes de ville du maroc |
|       |                      |                        |                                             |
|       |                      |                        |                                             |

## Qualité des données

- **Forces observées** :Structure simple et lisible, presence de site web officiel verifiable
- **Faiblesses observées** :il ya des fautes d'horthographe, langue mixte(Anglais et Francais)
- **Ambiguïtés ou doublons potentiels** :des colonne avec meme valeu
- **Champs manquants pour une meilleure interconnexion** :autre coordonne pour specifier le lieu exacte dans la ville
- **Risque principal pour une future mise en relation** : faute d'horthographe apparait sur les villes

## Conclusion courte

En `8 à 12` lignes, expliquez si ce jeu de données constitue une bonne base pour une future publication en données ouvertes liées, à quelles conditions, et quelles actions techniques devraient être menées en priorité.

Ce jeu de donnes constitue une base solide mais necessite encore des verification et des changement, le point fort de cette data c'est qu'il est ce forme csv bien structurer, il atteint 3 etoile sur 5 mais au fond de ces donnes il n'ya pas des lien et des URI vers des donnes externe aussi cette data necessite une normalisation du vocabulaire de quelque champs comme name_field,instituer_type , corriger les erreurs d'horthographe concernant les noms des villes , localiser mieux le lieu de chaque etablissement aussi construire des URI , ajouter des identifients pour eviter les redoublent pour les colonnes avec meme noms. en corrigent et verifient ca on peut bien sur construire une bonne base pour une future publication en donnes ouverte liees.
