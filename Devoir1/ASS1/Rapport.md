                Hasnae Akhrais


<img src="Hasnae.jfif" style="height:464px;margin-right:432px"/>

**Date du rapport :** 12 novembre 2025
**Source :** UCI Machine Learning Repository — *Mushroom*. ([archive.ics.uci.edu][1])



## 1. Résumé Exécutif

Ce rapport adapte la structure de votre précédent rapport (Default of Credit Card Clients) au dataset **Mushroom** (Agaricus / Lepiota). Ce jeu de données décrit des échantillons de champignons en termes de caractéristiques physiques et vise la classification **edible / poisonous**. Il contient **8 124 instances** et **22 features (catégorielles)** plus la variable cible. Le dataset contient quelques valeurs manquantes (marquées `?`) — principalement pour `stalk-root`. ([archive.ics.uci.edu][1])

**Points clés :**

* 8 124 instances (observations). ([archive.ics.uci.edu][1])
* 22 variables explicatives catégorielles (+ 1 target). ([archive.ics.uci.edu][1])
* Variable cible binaire : `edible` = `e`, `poisonous` = `p`. ([archive.ics.uci.edu][1])
* Données issues de l’Audubon Society Field Guide (données publiées / donnation : 1987). ([archive.ics.uci.edu][1])



## 2. Contexte et Objectifs

### 2.1 Objectif de la Recherche

Analyser les caractéristiques morphologiques des champignons pour construire des modèles de classification robustes (détecter les champignons *poisonous* vs *edible*). Ce dataset est fréquemment utilisé comme benchmark pour tester des algorithmes de classification (SVM, Random Forest, XGBoost, réseaux de neurones, méthodes d'ensemble, etc.). ([archive.ics.uci.edu][1])

### 2.2 Applications pratiques

* Démonstrations pédagogiques pour l’apprentissage supervisé.
* Évaluation de pipelines de prétraitement pour features catégorielles (one-hot, target encoding, embeddings).
* Études sur l’impact des valeurs manquantes et des codages non-ordonnés.



## 3. Caractéristiques du Dataset

### 3.1 Informations Générales

| Caractéristique        | Détail                                                                                   |
| ---------------------- | ---------------------------------------------------------------------------------------- |
| **Type de dataset**    | Multivarié                                                                               |
| **Domaine**            | Biologie / Écologie                                                                      |
| **Tâche**              | Classification binaire                                                                   |
| **Type de features**   | Catégorielles (lettres codées)                                                           |
| **Nombre d'instances** | 8 124. ([archive.ics.uci.edu][1])                                                        |
| **Nombre de features** | 22 (plus la cible). ([archive.ics.uci.edu][1])                                           |
| **Valeurs manquantes** | Oui (caractère `?` pour certaines lignes — ex. `stalk-root`). ([archive.ics.uci.edu][1]) |
| **Licence**            | Creative Commons Attribution 4.0 (CC BY 4.0). ([archive.ics.uci.edu][1])                 |
| **DOI (citation)**     | 10.24432/C5959T. ([archive.ics.uci.edu][1])                                              |



## 4. Description des Variables

**Variable cible**

* `class` / `poisonous` : `e` = edible, `p` = poisonous. ([archive.ics.uci.edu][1])

**Exemples de features (noms et codes) :**
(cap-shape, cap-surface, cap-color, bruises, odor, gill-attachment, gill-spacing, gill-size, gill-color, stalk-shape, stalk-root, stalk-surface-above-ring, stalk-surface-below-ring, stalk-color-above-ring, stalk-color-below-ring, veil-type, veil-color, ring-number, ring-type, spore-print-color, population, habitat). Les modalités de chaque variable sont codées par des lettres (par ex. cap-shape: `b`,`c`,`x`,`f`, ...). ([archive.ics.uci.edu][1])

> Remarque : `stalk-root` contient des `?` (valeurs manquantes) — à traiter lors du prétraitement (remplacement, catégorie ‘missing’, imputation, suppression selon stratégie).


## 5. Résultats Principaux (attendus / suggestions d’analyse)

> Ici je fournis des résultats attendus et un plan d’analyse – je n’exécute pas le code pour vous sauf si vous le demandez.

1. **Exploration**

   * Répartition cible (`edible` vs `poisonous`) — dataset souvent équilibré mais vérifier le ratio exact.
   * Vérifier distribution des modalités par feature (ex. `odor` est un fort prédicteur). ([archive.ics.uci.edu][1])

2. **Prétraitement**

   * Gérer `?` dans `stalk-root` (catégorie `missing` ou imputation).
   * Encodage des variables catégorielles : one-hot (pour arbres), target-encoding ou embeddings (pour réseaux).
   * Aucun besoin de normalisation (features catégorielles).

3. **Modélisation**

   * Baselines : Logistic Regression (après one-hot), Decision Tree, Random Forest.
   * Modèles performants souvent : Random Forest, XGBoost, LightGBM — très bons sur données catégorielles encodées.
   * Évaluer métriques : accuracy, precision, recall, F1, AUC. Pour ce dataset, `odor` et `spore-print-color` sont usuellent très discriminants. ([archive.ics.uci.edu][1])

4. **Interprétabilité**

   * Feature importance (arbres), SHAP values pour comprendre l’impact des modalités (ex. certaines odeurs indiquent fortement le caractère *poisonous*).



## 6. Code Python — Chargement et EDA rapide

```python
import pandas as pd
import matplotlib.pyplot as plt

# URL direct depuis UCI
url = "https://archive.ics.uci.edu/ml/machine-learning-databases/agaricus-lepiota/agaricus-lepiota.data"

# Colonnes (cible + 22 features)
cols = [
 "class","cap-shape","cap-surface","cap-color","bruises","odor",
 "gill-attachment","gill-spacing","gill-size","gill-color",
 "stalk-shape","stalk-root","stalk-surface-above-ring","stalk-surface-below-ring",
 "stalk-color-above-ring","stalk-color-below-ring","veil-type","veil-color",
 "ring-number","ring-type","spore-print-color","population","habitat"
]

df = pd.read_csv(url, header=None, names=cols)
print("Shape:", df.shape)
print(df['class'].value_counts(normalize=True))

# Traiter les '?' comme valeur manquante
df['stalk-root'] = df['stalk-root'].replace('?', pd.NA)

# Exemples d'EDA
print(df.isna().sum())  # compter les valeurs manquantes
print(df['odor'].value_counts())

# Visualisation simple
df['class'].value_counts().plot(kind='bar')
plt.title("Répartition edible vs poisonous")
plt.xlabel("Classe")
plt.ylabel("Nombre d'observations")
plt.show()
```



## 7. Accès aux Données & Citation

* Téléchargement direct des fichiers (données, .names, README) disponible sur la page UCI (fichiers `agaricus-lepiota.data`, `agaricus-lepiota.names`). ([archive.ics.uci.edu][1])
* Importation via `ucimlrepo` (exemple) : `mushroom = fetch_ucirepo(id=73)`. ([archive.ics.uci.edu][1])
* **Citation recommandée :** *Mushroom [Dataset]. (1981). UCI Machine Learning Repository. [https://doi.org/10.24432/C5959T](https://doi.org/10.24432/C5959T).* ([archive.ics.uci.edu][1])



## 8. Publications & Réutilisations

Ce dataset a été largement cité et utilisé (plusieurs dizaines d’articles, études et travaux de cours) pour tester des méthodes de classification et d’ensemble. Il existe des travaux récents utilisant des méthodes d’ensemble et d’apprentissage profond adaptés à des données catégorielles. ([archive.ics.uci.edu][1])



## 9. Recommandations

### 9.1 Pour les praticiens / étudiants

* Commencez par nettoyer `stalk-root` et encodez toutes les variables.
* Tester des modèles d’ensemble (Random Forest, XGBoost) comme baseline rapide.
* Expérimenter l’encodage (one-hot vs target-encoding) et mesurer l’impact sur overfitting.

### 9.2 Pour les chercheurs

* Étudier embeddings catégoriels / architectures hybrides pour capturer interactions complexes entre modalités.
* Investiguer robustesse à la distribution (si de nouveaux habitats ou espèces sont inclus).



## 10. Limitations & Considérations Éthiques

* Données tirées d’un guide de terrain (Audubon) — échantillons limités aux espèces présentes dans la référence. Généralisation limitée. ([archive.ics.uci.edu][1])
* Usage pédagogique et de recherche : **ne pas** utiliser comme conseil réel de consommation de champignons — risque pour la vie humaine. Toujours rappeler la mise en garde du dataset (aucune règle simple pour déterminer l’éditabilité des champignons).



## 11. Annexes — Ressources utiles

* Page UCI (description + téléchargement) — source principale. ([archive.ics.uci.edu][1])
* Fichiers : `agaricus-lepiota.data`, `agaricus-lepiota.names`, README (disponibles sur la page UCI). ([archive.ics.uci.edu][1])




[1]: https://archive.ics.uci.edu/dataset/73/mushroom "UCI Machine Learning Repository"
