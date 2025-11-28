# COURS DE SCIENCE DES DONNÉES

# A.LARHLIMI

## HOUMIRI KHADIJA 
## 21010337
<img src="image7.png" style="height:540px;margin-right:393px"/>

## École Nationale de Commerce et de Gestion (ENCG) - 4ème Année

##Analyse des données relatives aux notes des étudiants aux examens
---
## À propos du jeu de données

Cet ensemble de données présente toutes les informations relatives aux performances des étudiants aux examens. Les notes obtenues sont ainsi mises en relation avec les habitudes d'étude et le parcours de l'étudiant, facilitant l'analyse de ses résultats. Cet ensemble de données est utilisé dans les établissements d'enseignement supérieur (collèges, lycées, universités, etc.) pour déterminer si un étudiant a réussi ou échoué à un examen.
Les colonnes de cet ensemble de données sont :
identifiant de l'étudiant, heures d'étude, heures de sommeil, taux de présence, note précédente et note finale.


 Très bien — voici **une interprétation précise, claire et complète de chaque code**, **cellule par cellule**, pour expliquer *ce que fait* chaque morceau de code et *pourquoi* il est utile.

---

# ⭐ **INTERPRÉTATION DE CHAQUE CODE DU NOTEBOOK**

---

## **1️⃣ `!pip install ucimlrepo`**

➡️ **Interprétation :**
Cette ligne installe une bibliothèque appelée **ucimlrepo**, qui permet d’accéder facilement aux jeux de données de l’UCI Machine Learning Repository.
Sans cette installation, le dataset Wine Quality ne pourrait pas être téléchargé automatiquement.

---

## **2️⃣ Importation du dataset via ucimlrepo**

```python
from ucimlrepo import fetch_ucirepo

# fetch dataset
wine_quality = fetch_ucirepo(id=186)

# metadata
print(wine_quality.metadata)

# variable information
print(wine_quality.variables)
```

➡️ **Interprétation :**
Ce code importe la fonction qui permet de télécharger les datasets UCI.
Il récupère ensuite le dataset numéro **186**, qui correspond à Wine Quality.

Puis :

* `metadata` affiche toutes les informations générales sur la base (auteurs, source, type de données…).
* `variables` affiche la description des colonnes (feature names, types…).

Cela permet de comprendre la structure du dataset avant de l'utiliser.

---

## **3️⃣ Chargement du CSV**

```python
import pandas as pd
import numpy as np

link = "http://archive.ics.uci.edu/.../winequality-white.csv"
df = pd.read_csv(link, sep=";")

print(df.head())
```

➡️ **Interprétation :**
Ici, le dataset est récupéré directement depuis un lien en CSV.
Le séparateur est `;` car c'est un fichier européen.

`df.head()` affiche les 5 premières lignes pour vérifier que le chargement s’est bien déroulé.

---

## **4️⃣ Séparation des variables**

```python
X = df.drop("quality", axis=1)
Y = df["quality"]

print(Y.value_counts())
```

➡️ **Interprétation :**

* **X** = toutes les colonnes sauf "quality" → les variables d'entrée du modèle.
* **Y** = la colonne que l’on veut prédire → la qualité du vin.

`value_counts()` montre combien de vins ont un score 3, 4, 5, 6, etc.
Cela permet d'évaluer la distribution des classes.

---

## **5️⃣ Transformation en classification binaire**

```python
Y = [0 if val <=5 else 1 for val in Y]
```

➡️ **Interprétation :**
La note de qualité (0–10) est transformée en deux classes :

* **0 = mauvais vin** (qualité ≤ 5)
* **1 = bon vin** (qualité > 5)

Cela convertit le problème de **régression** en **classification binaire**, plus simple pour KNN.

---

## **6️⃣ Analyse graphique : heatmap**

```python
import matplotlib.pyplot as plt
import seaborn as sns

plt.figure()
corr = X.corr()
sns.heatmap(corr)
```

➡️ **Interprétation :**
Ce code calcule la **matrice de corrélation** entre toutes les colonnes.
Le heatmap permet de visualiser :

* quelles variables sont liées,
* lesquelles pourraient influencer la qualité du vin,
* si certaines colonnes sont fortement corrélées entre elles (risque de redondance).

---

## **7️⃣ Découpage apprentissage / validation**

```python
from sklearn.model_selection import train_test_split
Xa, Xt, Ya, Yt = train_test_split(X, Y, test_size=0.3, shuffle=True)
Xa, Xv, Ya, Yv = train_test_split(Xa, Ya, shuffle=True, test_size=0.5, stratify=Ya)
```

➡️ **Interprétation :**

1. Le dataset est divisé en :

   * **70% pour l'entraînement**
   * **30% pour le test**

2. L’ensemble d’entraînement est ensuite redécoupé en :

   * **Entraînement (Xa, Ya)**
   * **Validation (Xv, Yv)**

Ce découpage permet :

* d’entraîner le modèle,
* de tester son efficacité sur la validation,
* de garder un test final non utilisé dans les réglages.

`stratify=Ya` garantit que les proportions de classes sont respectées.

---

## **8️⃣ Modèle KNN – version simple**

```python
from sklearn.neighbors import KNeighborsClassifier
knn = KNeighborsClassifier(n_neighbors=3)
knn.fit(Xa, Ya)
Ypred_v = knn.predict(Xv)

from sklearn.metrics import accuracy_score
error_v = 1 - accuracy_score(Yv, Ypred_v)
```

➡️ **Interprétation :**

* On choisit un **KNN avec k = 3 voisins**.
* On l’entraîne sur l’ensemble d’apprentissage.
* On prédît les classes sur l'ensemble de validation.
* On calcule l’erreur (1 – accuracy).

Cela donne une première estimation de la performance du modèle.

---

## **9️⃣ Recherche du meilleur k**

```python
k_vector = np.arange(1, 37, 2)
error_val = np.zeros(len(k_vector))

for ind, k_val in enumerate(k_vector):
    knn = KNeighborsClassifier(n_neighbors=k_val)
    knn.fit(Xa, Ya)
    Ypred_val = knn.predict(Xv)
    error_val[ind] = 1 - accuracy_score(Yv, Ypred_val)
```

➡️ **Interprétation :**

* On teste plusieurs valeurs de **k impaires entre 1 et 37**.
* Pour chaque k :

  * Le modèle est entraîné.
  * On évalue l’erreur de validation.
* Les erreurs sont enregistrées dans `error_val`.

Objectif : **trouver le k optimal**.

---

## **🔟 Choix du meilleur k**

```python
err_min = error_val.min()
ind_opt = error_val.argmin()
k_star = k_vector[ind_opt]
```

➡️ **Interprétation :**

* `err_min` = la plus petite erreur observée.
* `ind_opt` = l’indice de cette erreur.
* `k_star` = la valeur optimale de k.

C’est ici que le meilleur modèle est choisi.

---

## **1️⃣1️⃣ Normalisation des données**

```python
from sklearn.preprocessing import StandardScaler
sc = StandardScaler()
sc = sc.fit(Xa)
Xa_n = sc.transform(Xa)
Xv_n = sc.transform(Xv)
```

➡️ **Interprétation :**

Le KNN dépend fortement des distances.
Certaines variables (ex : chlorures) ont des échelles différentes.

La normalisation :

* centre les données autour de 0,
* met toutes les variables sur la même échelle.

Cela améliore fortement les performances du modèle.

---

## **1️⃣2️⃣ Graphique de l’erreur en fonction de k**

➡️ **Interprétation :**
Ce code affiche une courbe "k vs erreur".
Il permet de visualiser la tendance et de vérifier que le k choisi est cohérent.

---

## **1️⃣3️⃣ Heatmap finale stylisée**

➡️ **Interprétation :**
Un deuxième heatmap plus esthétique est affiché pour mieux interpréter les corrélations entre caractéristiques.

