# Benchmark des référentiels externes

## Identification

- **Groupe** : Groupe-03
- **Jeu de données étudié** : higher_education_sample.csv
- **Types d'entités retenus** : Établissement, Ville, Pays

## 1. Référentiels comparés

| Référentiel | URL | Types d'entités couverts | Intérêt potentiel | Limites observées |
| --- | --- | --- | --- | --- |
| Wikidata | https://www.wikidata.org | Établissements, Villes, Pays | Identifiants stables, données enrichies | Pas tous les établissements marocains présents |
| GeoNames | https://www.geonames.org | Villes, Pays | URI géographiques stables, coordonnées GPS | Pas d'info sur les établissements |
| DBpedia | https://dbpedia.org | Établissements, Domaines | Lié à Wikipedia, riche sémantiquement | Données parfois incomplètes ou obsolètes |

## 2. Critères de comparaison

- **Couverture** : Wikidata et DBpedia couvrent les établissements 
  connus mondialement mais pas tous les établissements marocains. 
  GeoNames couvre bien toutes les villes du Maroc.

- **Qualité des identifiants** : Wikidata utilise des Q-identifiants 
  stables (ex: Q1028 pour le Maroc). GeoNames utilise des codes 
  numériques stables. DBpedia utilise des URI basées sur Wikipedia.

- **Précision sémantique** : Wikidata est le plus précis car il 
  distingue université, école d'ingénieurs, faculté. DBpedia est 
  moins précis. GeoNames est précis uniquement pour la géographie.

- **Facilité d'appariement** : GeoNames est le plus facile car le 
  nom de la ville suffit. Wikidata nécessite le nom complet de 
  l'établissement. DBpedia dépend de l'existence d'une page Wikipedia.

- **Richesse des informations disponibles** : Wikidata est le plus 
  riche avec logo, coordonnées, effectifs. GeoNames donne coordonnées 
  GPS et code pays. DBpedia donne les informations de Wikipedia.

## 3. Cas d'appariement manuel

Documentez au moins `6` cas.

| Entité locale | Type | Référentiel cible | Correspondance candidate | Indices utilisés | Niveau de confiance | Décision |
| --- | --- | --- | --- | --- | --- | --- |
| ENSIAS | Établissement | Wikidata | Q3578202 | institution_name + city = Rabat | Élevé | Accepté |
| Université Mohammed V | Établissement | Wikidata | Q1360237 | institution_name + short_name = UM5 | Élevé | Accepté |
| Cadi Ayyad University | Établissement | DBpedia | dbr:Cadi_Ayyad_University | institution_name + city = Marrakesh | Moyen | Accepté |
| Rabat | Ville | GeoNames | 2538475 | city + country = Morocco | Élevé | Accepté |
| Casablanca | Ville | GeoNames | 2553604 | city + country = Morocco | Élevé | Accepté |
| Morocco | Pays | Wikidata | Q1028 | country = Morocco | Très élevé | Accepté |

## 4. Synthèse

- **Quel référentiel paraît le plus utile pour chaque type d'entité ?**
  - Établissement → Wikidata : identifiants stables et données enrichies
  - Ville → GeoNames : coordonnées GPS et URI stables pour toutes 
    les villes marocaines
  - Pays → Wikidata : code Q1028 pour Morocco, très fiable

- **Quels cas restent ambigus ?**
  - Le sigle ENSA existe pour plusieurs écoles dans différentes villes
  - Cadi Ayyad University peut être confondue avec d'autres universités 
    si on utilise seulement le nom court

- **Quels champs du dataset aident le plus à l'appariement ?**
  - institution_name → pour chercher dans Wikidata et DBpedia
  - city + country → pour chercher dans GeoNames
  - website → identifiant unique et stable pour chaque établissement