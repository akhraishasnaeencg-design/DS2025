# Rapport sur le jeu de données Mushroom (UCI)

## Description générale

Le jeu de données Mushroom comprend des descriptions de 8124 échantillons hypothétiques issus de 23 espèces de champignons à lamelles, appartenant aux familles Agaricus et Lepiota. Chaque exemple correspond à un champignon identifié comme **comestible (edible)** ou **vénéneux (poisonous)**. Les champignons dont l'edibilité est inconnue ont été regroupés avec la classe « vénéneux ». Il s'agit donc d'un problème de classification binaire.

## Caractéristiques principales

- **Nombre d'exemples (instances)** : 8124
- **Nombre de variables (attributs)** : 22 caractéristiques observables pour chaque champignon
- **Type de données** : toutes les variables sont catégorielles
- **Tâche d'analyse** : classification binaire (prédire comestible ou vénéneux)


## Description des variables

Le dataset contient 22 attributs qui décrivent les caractéristiques physiques du champignon, par exemple :


| Nom de la variable | Description | Modalités codées |
| :-- | :-- | :-- |
| cap-shape | Forme du chapeau | bell=b, conical=c, convex=x, flat=f, knobbed=k, sunken=s |
| cap-surface | Surface du chapeau | fibrous=f, grooves=g, scaly=y, smooth=s |
| cap-color | Couleur du chapeau | brown=n, buff=b, cinnamon=c, gray=g, green=r, pink=p, purple=u, red=e, white=w, yellow=y |
| bruises | Présence de meurtrissures | bruises=t, no=f |
| odor | Odeur | almond=a, anise=l, creosote=c, fishy=y, foul=f, musty=m, none=n, pungent=p, spicy=s |
| gill-attachment | Attache des lamelles | attached=a, descending=d, free=f, notched=n |
| gill-spacing | Espacement des lamelles | close=c, crowded=w, distant=d |
| gill-size | Taille des lamelles | broad=b, narrow=n |
| gill-color | Couleur des lamelles | black=k, brown=n, buff=b, chocolate=h, gray=g, green=r, orange=o, pink=p, purple=u, red=e, white=w, yellow=y |
| stalk-shape | Forme du pied | enlarging=e, tapering=t |
| stalk-root | Type de racine du pied (valeurs manquantes possibles) | bulbous=b, club=c, cup=u, equal=e, rhizomorphs=z, rooted=r, missing=? |
| veil-type | Type de voile | partial=p, universal=u |
| ring-number | Nombre d'anneaux | none=n, one=o, two=t |
| spore-print-color | Couleur de la sporée | black=k, brown=n, buff=b, chocolate=h, green=r, orange=o, purple=u, white=w, yellow=y |
| habitat | Habitat naturel | grasses=g, leaves=l, meadows=m, paths=p, urban=u, waste=w, woods=d |

## Classe cible

- **poisonous** : variable cible catégorielle (binaire)
    - edible = e (comestible)
    - poisonous = p (vénéneux)


## Particularités

- Il existe des valeurs manquantes dans la variable stalk-root.
- Les données sont extraites de guides naturalistes, simulant des caractéristiques physiques réelles.
- Le jeu ne contient pas de données numériques, tout est sous forme d'attributs catégoriels codés.


## Usage

Ce jeu de données est utilisé principalement en apprentissage automatique pour expérimenter des algorithmes de classification supervisée. Il permet d'identifier facilement des modèles capables de prédire la toxicité ou la comestibilité des champignons à partir d'observations visuelles.

## Licence et provenance

- Licence : Creative Commons Attribution 4.0 International (CC BY 4.0)
- Source : UCI Machine Learning Repository, Dataset ID 73
- Date d'ajout : 1987


## Références et documents

- Fichiers originaux : agaricus-lepiota.data, agaricus-lepiota.names, README, etc.
- Articles scientifiques référencés utilisant ce dataset
- DOI : 10.24432/C5959T

***

Ce rapport synthétise les informations indispensables pour comprendre et exploiter ce jeu de données Mushroom, qui est un classique pour la classification en biologie. Il est adapté pour des applications pédagogiques ou de recherche en machine learning sur des données catégorielles.[^1][^2][^5]
<span style="display:none">[^3][^4][^6][^7][^8][^9]</span>

<div align="center">⁂</div>

[^1]: https://archive.ics.uci.edu/dataset/73/mushroom

[^2]: https://archive.ics.uci.edu/ml/datasets/mushroom

[^3]: https://greenlake.co.uk/pages/dataset_MUSH.html

[^4]: https://archive.ics.uci.edu/dataset/848/secondary+mushroom+dataset

[^5]: https://search.r-project.org/CRAN/refmans/arulesCBA/html/Mushroom.html

[^6]: https://www.scikit-yb.org/en/latest/api/datasets/mushroom.html

[^7]: https://www.kaggle.com/datasets/uciml/mushroom-classification

[^8]: https://www.scribd.com/document/698313979/02-Mushroom-Machine-Learning-Repository

[^9]: https://rpubs.com/soumya2g/CUNY-Coursework-UCI_Mashroom_Data_Analysis

