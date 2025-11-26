# COURS DE SCIENCE DES DONNÉES
# A.LARHLIMI

## HOUMIRI Khadija 
## École Nationale de Commerce et de Gestion (ENCG) - 4ème Année

---
# COURS DE SCIENCE DES DONNÉES
# A.LARHLIMI

## HOUMIRI Khadija 
## École Nationale de Commerce et de Gestion (ENCG) - 4ème Année

---
La base de données à laquelle tu fais référence, **"Seoul Bike Sharing Demand" (dataset 560)**, est un ensemble de données fourni par l'UCI Machine Learning Repository. Voici une synthèse claire et concise pour que tu comprennes bien son contenu et ses objectifs :

***

Voici une **présentation détaillée** du lien que tu as envoyé — le jeu de données Wine Quality hébergé sur UCI Machine Learning Repository. ([archive.ics.uci.edu][1])

---

## 🍷 Qu’est-ce que le dataset « Wine Quality »

* Le dataset Wine Quality regroupe deux jeux de données distincts, l’un pour des vins rouges, l’autre pour des vins blancs — des échantillons de vins « Vinho Verde » du nord du Portugal. ([archive.ics.uci.edu][1])
* L’objectif principal : **modéliser la qualité du vin** à partir de tests physico-chimiques (variables d’entrée) pour prédire ou expliquer la qualité perçue (variable de sortie). ([archive.ics.uci.edu][1])
* Ce dataset est souvent utilisé dans des contextes d’**apprentissage automatique** pour des tâches de **régression** (prédire la note de qualité) ou de **classification** (qualifier un vin comme « bon / médiocre », etc.). ([uci-ics-mlr-prod.aws.uci.edu][2])

---

## 📊 Contenu du dataset — variables & structure

Chaque échantillon (chaque vin) est décrit par un ensemble de **caractéristiques physico-chimiques** (entrée) et une **note de qualité** (sortie). ([archive.ics.uci.edu][1])

### Variables explicatives (features) — 11 caractéristiques

| Variable             | Description / rôle                                                                        |
| -------------------- | ----------------------------------------------------------------------------------------- |
| fixed_acidity        | Acidité fixe (acidité totale non volatile) ([archive.ics.uci.edu][1])                     |
| volatile_acidity     | Acidité volatile (acides volatils) ([archive.ics.uci.edu][1])                             |
| citric_acid          | Acidité citrique ([archive.ics.uci.edu][1])                                               |
| residual_sugar       | Sucre résiduel (quantité de sucres restants) ([archive.ics.uci.edu][1])                   |
| chlorides            | Taux de chlorures ([archive.ics.uci.edu][1])                                              |
| free_sulfur_dioxide  | Dioxyde de soufre libre (libre SO₂) ([archive.ics.uci.edu][1])                            |
| total_sulfur_dioxide | Dioxyde de soufre total (libre + combiné) ([archive.ics.uci.edu][1])                      |
| density              | Densité du vin ([archive.ics.uci.edu][1])                                                 |
| pH                   | pH du vin (acidité/ alcalinité) ([archive.ics.uci.edu][1])                                |
| sulphates            | Sulfates (composés chimiques influençant goût et conservation) ([archive.ics.uci.edu][1]) |
| alcohol              | Taux d’alcool (en pourcentage) ([archive.ics.uci.edu][1])                                 |

### Variable cible (target) — qualité

* `quality`: une note (score) généralement entre 0 et 10 attribuée au vin selon des **critiques d’experts** (goûteurs), qui jugent des aspects sensoriels (goût, arôme, équilibre, etc.). ([archive.ics.uci.edu][1])
* Le dataset ne contient **pas** d’informations sur le type de raisin, la marque du vin, le prix ou le millésime — uniquement des données chimiques + la note sensorielle. ([archive.ics.uci.edu][1])

### Taille & format

* Environ **4 898 instances** (échantillons) au total. ([archive.ics.uci.edu][1])
* Données numériques continues pour les variables d’entrée. ([archive.ics.uci.edu][1])
* Pas de valeurs manquantes (dataset « clean »). ([archive.ics.uci.edu][1])

---

## 🎓 Usage & intérêt

Pourquoi ce dataset est populaire :

* Il permet d’explorer l’influence des caractéristiques chimiques d’un vin sur la qualité perçue — utile en œnologie, data science, apprentissage machine.
* Il est simple, bien documenté et assez réaliste pour constituer un **bon cas d’étude** (régression ou classification).
* Il sert de **référence pour expérimenter** des techniques de pré-traitement (normalisation, sélection de variables), modélisation (régression, kNN, forêts aléatoires, etc.), évaluation de performance.
* Permet aussi d’analyser la **corrélation entre variables chimiques** et qualité, d’identifier les variables les plus importantes, etc.

---

## 📚 Informations & provenance

* Créé par Paulo Cortez, A. Cerdeira, F. Almeida, Telmo Matos & J. Reis, en 2009. ([archive.ics.uci.edu][1])
* DOI associé : 10.24432/C56S3T. ([archive.ics.uci.edu][1])
* Licence : Creative Commons Attribution 4.0 International (CC BY 4.0) — utilisation libre avec attribution. ([archive.ics.uci.edu][1])

---

## 🧠 Possibilités d’exploitation typiques

Voici quelques exemples de ce qu’on peut faire avec ce dataset :

* **Classification** : par exemple, transformer la note quality en « bon / moyen / mauvais » et construire un classifieur.
* **Régression** : prédire la note de qualité telle quelle (score 0–10) à partir des caractéristiques chimiques.
* **Analyse exploratoire** : corrélations, visualisations (boxplots, scatterplots) pour identifier les variables influentes.
* **Sélection de variables / ingénierie de features** : déterminer quelles caractéristiques chimiques sont réellement pertinentes.
* **Prétraitements + normalisation** pour améliorer les performances des modèles sensibles aux échelles.

---
Voici une **description claire, précise et structurée de chaque partie** de votre fichier **TP_ml.ipynb**, cellule par cellule, en suivant exactement l’ordre du notebook.

---

# ✅ **DESCRIPTION DÉTAILLÉE DE CHAQUE PARTIE DU FICHIER *TP_ml.ipynb***

---

## **🟦 Partie 1 — Installation de la bibliothèque**

### 🔢 Cellule :

```markdown
Install the ucimlrepo package
```

Vous indiquez que vous allez installer une bibliothèque nécessaire pour charger le dataset depuis UCI.

### 🔢 Cellule :

```python
!pip install ucimlrepo
```

Cette cellule installe **ucimlrepo**, une bibliothèque permettant d’accéder facilement aux jeux de données de l’UCI Machine Learning Repository.

---

## **🟦 Partie 2 — Importation du dataset Wine Quality**

### 🔢 Cellule :

```markdown
Import the dataset
```

### 🔢 Cellule :

```python
from ucimlrepo import fetch_ucirepo
...
print(wine_quality.variables)
```

Cette partie :

* charge le dataset **Wine Quality** depuis UCI (via son ID),
* affiche des informations sur les variables (caractéristiques chimiques du vin).

---

## **🟦 Partie 3 — Chargement manuel du dataset**

### 🔢 Cellule :

```markdown
chargement des données et l'affichage de leur résumé
```

### 🔢 Cellule :

```python
df = pd.read_csv(link)
df.describe()
df.info()
df.head()
```

Ici :

* vous chargez le fichier CSV via un lien Internet,
* vous affichez :

  * un résumé statistique (`describe()`),
  * les types et tailles des colonnes (`info()`),
  * les premières lignes (`head()`).

Objectif : **exploration initiale des données**.

---

## **🟦 Partie 4 — Séparation des données et préparation des variables**

### 🔢 Cellule :

```python
X = df.drop("quality", axis=1)
Y = df["quality"]
print(Y.value_counts())
```

Cette cellule :

* sépare les données explicatives (**X**) de la cible (**Y**),
* regarde combien d’échantillons existent pour chaque note de qualité.

---

## **🟦 Partie 5 — Transformation de la cible en classification binaire**

### 🔢 Cellule :

```python
Y = [0 if val <= 5 else 1 for val in Y]
```

Transformation du problème initial (prédire une note entre 0 et 10) en un problème **binaire** :

* 0 = vin de mauvaise qualité (≤5)
* 1 = vin de bonne qualité (≥6)

Très utile pour l’apprentissage supervisé.

---

## **🟦 Partie 6 — Séparation apprentissage / validation**

### 🔢 Cellule :

```python
Xa, Xv, Ya, Yv = ... (train_test_split)
```

(Ici le code est partiellement visible mais on comprend la logique.)

Objectif :

* créer un ensemble pour entraîner le modèle (**train**),
* et un autre pour l’évaluer (**validation**).

---

## **🟦 Partie 7 — Test du modèle kNN pour plusieurs valeurs de k**

### 🔢 Cellule :

```python
k_vector = np.arange(1, 37, 2)
...
clf = KNeighborsClassifier(n_neighbors=k)
clf.fit(Xa, Ya)
...
```

Dans cette section :

* vous testez différentes valeurs de **k** (1, 3, 5, …, 35),
* pour chaque k :

  * vous entraînez le classifieur kNN,
  * vous calculez le **taux d’erreur** sur l’ensemble de validation.

Objectif : **trouver le meilleur k**.

---

## **🟦 Partie 8 — Sélection du meilleur k**

### 🔢 Cellule :

```python
err_min, ind_opt = ...
k_star = k_vector[ind_opt]
```

Cette cellule :

* trouve l’erreur minimale,
* récupère la position du k optimal,
* détermine la meilleure valeur de k.

---

## **🟦 Partie 9 — Normalisation des données**

### 🔢 Cellule :

```python
from sklearn.preprocessing import StandardScaler
Xa_n = sc.transform(Xa)
Xv_n = sc.transform(Xv)
```

La normalisation :

* met toutes les variables sur la même échelle (moyenne 0, écart-type 1),
* est indispensable pour kNN (qui utilise les distances).

Objectif :
➡️ Vérifier si la normalisation **améliore les résultats**.

---

## **🟦 Partie 10 — Visualisation de l’erreur en fonction de k**

### 🔢 Cellule :

```python
plt.plot(k_vector, error_val)
plt.plot(k_star, err_min, 'ro')
```

Cette cellule :

* dessine la courbe des erreurs pour les différents k,
* marque en rouge le **k optimal**.

Objectif : **visualiser graphiquement le meilleur modèle**.

---

## **🟦 Partie 11 — Matrice de corrélation**

### 🔢 Cellule :

```python
sns.heatmap(df.corr(), ...)
```

Cette partie :

* génère une **heatmap** (carte de chaleur),
* montre la corrélation entre les variables chimiques du vin.

Objectif : comprendre quelles variables influencent la qualité (alcool, acidité volatile, etc.)

---



