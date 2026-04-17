# Rapport hors séance - TP1

## Page de garde

- **Module** : Linked Open Data
- **TP** : TP1 - Introduction aux données ouvertes liées
- **Groupe** :group
- **Étudiants** :Debar Fatima, Mohamed Vall Aichetou
- **Date** :09/04/2026

## Consigne

Ce rapport est à remettre **avant la prochaine séance**. Il constitue une **étude distincte** du travail réalisé pendant le TP1 en classe et prépare directement le TP2.

## 1. Introduction

Dans ce TP, nous avons étudié un jeu de données publié sur data.gov.ma 
contenant 21 établissements d'enseignement supérieur marocains. 
Le dataset est au format CSV et contient des informations comme le nom, 
la ville, le type et le domaine de chaque établissement.
Les entités retenues pour le travail hors séance sont : 
Établissement, Ville et Pays.
Le problème principal est l'absence d'identifiants stables et de liens 
vers des référentiels externes.

## 2. Types d'entités étudiés

Présentez :

- les `2 à 3` types d'entités retenus pour le travail hors séance
  les entites qu'on a retenu: etablissement, city et siteWeb
- les raisons de ce choix:

- les champs ou indices disponibles pour les apparier à des référentiels externes

## 3. Benchmark des référentiels externes

## 3. Benchmark des référentiels externes

- **Couverture** : Wikidata couvre les établissements connus 
  mondialement mais pas tous les établissements marocains. 
  GeoNames couvre toutes les villes du Maroc.

- **Précision apparente** : Wikidata est le plus précis car il 
  distingue université, école d'ingénieurs et faculté. 
  GeoNames est précis uniquement pour la géographie.

- **Qualité des identifiants** : Wikidata utilise des Q-identifiants 
  stables (ex: Q3578202 pour ENSIAS, Q1028 pour Morocco). 
  GeoNames utilise des codes numériques stables 
  (ex: 2553604 pour Casablanca).

- **Richesse sémantique** : Wikidata est le plus riche avec logo, 
  coordonnées, effectifs. GeoNames donne coordonnées GPS et 
  code pays.

- **Facilité d'utilisation pour un futur alignement** : GeoNames 
  est le plus facile car le nom de la ville suffit. Wikidata 
  nécessite le nom complet de l'établissement.

## 4. Cas d'appariement manuel

- **Entité locale** : ENSIAS
  - Référentiel cible : Wikidata
  - Indices utilisés : institution_name + city = Rabat
  - Niveau de confiance : Élevé
  - Ambiguïté éventuelle : aucune
  - Décision finale : Accepté → Q3578202

- **Entité locale** : Université Mohammed V
  - Référentiel cible : Wikidata
  - Indices utilisés : institution_name + short_name = UM5
  - Niveau de confiance : Élevé
  - Ambiguïté éventuelle : aucune
  - Décision finale : Accepté → Q1360237

- **Entité locale** : Casablanca
  - Référentiel cible : GeoNames
  - Indices utilisés : city + country = Morocco
  - Niveau de confiance : Élevé
  - Ambiguïté éventuelle : aucune
  - Décision finale : Accepté → 2553604

- **Entité locale** : Rabat
  - Référentiel cible : GeoNames
  - Indices utilisés : city + country = Morocco
  - Niveau de confiance : Élevé
  - Ambiguïté éventuelle : aucune
  - Décision finale : Accepté → à vérifier sur GeoNames

## 5. Plan de normalisation et d'identification

Expliquez :

- quelles valeurs doivent être normalisées
  institution_name, main_field, city
- quelles règles doivent être appliquées avant un futur travail RDF
  Restaurer les accents via UTF-8, Aligner sur classification ISCED-F 2013, normaliser sur des liste de ville du maroc
- quelles entités devraient recevoir un identifiant stable
  Pour les établissements, construire un slug URI de la forme : short_name + city
  Pour les villes, aligner directement sur ce qui est dans la liste des villes du maroc.
- comment ces identifiants pourraient être construits conceptuellement

## 6. Analyse des risques

- **Risques de faux appariement** : 
  Le sigle ENSA existe pour plusieurs écoles dans différentes 
  villes du Maroc, ce qui peut créer une confusion lors de 
  l'appariement avec Wikidata.

- **Cas de désambiguïsation** : 
  Le short_name "UAE" désigne à la fois Abdelmalek Essaadi 
  University et les Émirats Arabes Unis. Il faut toujours 
  combiner avec le champ city pour désambiguïser.

- **Limites des référentiels choisis** : 
  Wikidata ne contient pas tous les établissements marocains, 
  certaines petites écoles n'ont pas de page. DBpedia dépend 
  de l'existence d'une page Wikipedia.

- **Informations manquantes dans le dataset** : 
  Absence de coordonnées GPS, pas de code officiel des 
  établissements, pas de licence explicite, pas d'identifiant 
  ISCED pour les domaines disciplinaires.

## 7. Difficultés rencontrées

- **Absence ou faiblesse des identifiants** : 
  Le champ record_id est un simple compteur séquentiel, 
  il ne peut pas servir d'identifiant stable universel. 
  Le short_name n'est pas toujours unique (ex: ENSA).

- **Qualité insuffisante de certaines valeurs** : 
  Les noms des établissements sont sans accents ce qui 
  complique la recherche dans Wikidata et DBpedia. 
  Les noms de villes ont des variantes orthographiques 
  (Marrakesh vs Marrakech).

- **Limites de couverture des référentiels** : 
  Certains établissements comme les petites écoles 
  spécialisées n'ont pas de page dans Wikidata ni DBpedia.

- **Difficultés de désambiguïsation** : 
  Le sigle UAE peut désigner l'université marocaine ou 
  les Émirats Arabes Unis. Sans contexte supplémentaire 
  comme la ville ou le pays, l'appariement devient risqué.

## 8. Conclusion

Concluez sur la valeur de cette étude préparatoire et sur la manière dont elle facilite la séance suivante.

## Annexes éventuelles

Vous pouvez ajouter si nécessaire :

- une capture du jeu de données source
- un schéma conceptuel
- un tableau complémentaire de liens externes
