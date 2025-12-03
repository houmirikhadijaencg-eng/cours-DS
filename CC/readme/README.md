# COURS DE SCIENCE DES DONNÉES

# A.LARHLIMI

## HOUMIRI khadija

<img src="image7.png" style="height:540px;margin-right:393px"/>

## École Nationale de Commerce et de Gestion (ENCG) - 4ème Année

--- 
# PARTIE 1 : Présentation de donnée de jeux 
# **1. Sélection du Dataset**

Pour ce projet, nous avons choisi le dataset **Finance Data**, disponible sur la plateforme **Kaggle** et publié par l’auteur *nitindatta*. Il s’agit d’un ensemble de données issu d’un **questionnaire Google Forms**, collecté durant la période de confinement.
Ce dataset a été sélectionné car il porte sur des **comportements réels d’investisseurs**, propose des **variables catégorielles et numériques variées**, et il permet de traiter une problématique de **classification supervisée**, contrairement aux datasets trop classiques comme Titanic ou Iris.

Ce choix garantit ainsi un jeu de données :

* pertinent pour de l’analyse comportementale,
* adapté à des techniques de Machine Learning,
* suffisamment riche pour construire un modèle prédictif.

---

# **2. Définition de la Problématique**

L’objectif principal est d’étudier :

### **« Quels facteurs personnels et comportementaux influencent la décision d’investir ? »**

Dans cette perspective, la variable cible choisie est généralement :
**“Do you invest in Investment Avenues?”** → Oui / Non

Ainsi, la problématique se formule comme une **tâche de classification binaire** :

* **1** : L’individu investit
* **0** : L’individu n’investit pas

Cette formulation permet d’appliquer divers modèles supervisés tels que :

* Logistic Regression
* Random Forest
* SVM
* KNN
* Gradient Boosting, etc.

L’objectif est donc d’établir un modèle capable de **prédire la probabilité qu’un individu investisse**, à partir de ses caractéristiques démographiques et comportementales.

---

# **3. Dictionnaire des Données (Metadata)**

Le dataset contient différentes variables issues d’un formulaire d’enquête. Voici la description synthétique :

### **3.1. Taille et Structure**

* Nombre d’observations : environ **500 à 600 entrées** (selon les versions)
* Format : fichier CSV
* Type d’étude : enquête déclarative (self-reported survey)
* Type de tâches possibles : classification, analyse descriptive, clustering

### **3.2. Types de Variables**

* **Variables catégorielles** : genre, préférences, opinions, choix d’investissement
* **Variables ordinales** : niveaux d’importance, niveau de risque accepté
* **Variables numériques** : âge, income si présent
* **Cible (Target)** : binaire (Oui / Non)

### **3.3. Description des principales colonnes**

| Variable                                               | Type             | Signification                                                             |
| ------------------------------------------------------ | ---------------- | ------------------------------------------------------------------------- |
| **GENDER**                                             | Catégorielle     | Indique le genre du répondant (Male / Female).                            |
| **AGE**                                                | Numérique        | Âge du participant.                                                       |
| **Do you invest in Investment Avenues?**               | Binaire (Target) | Réponse indiquant si la personne investit.                                |
| **What do you think are the best investment avenues?** | Catégorielle     | Opinion du participant sur les produits financiers les plus intéressants. |
| **Risk appetite / Risk behaviour**                     | Ordinale         | Indique le niveau de tolérance au risque.                                 |
| **Reasons for investing**                              | Catégorielle     | Motivations principales (revenus, sécurité, retraite, etc.).              |
| **Investment horizon**                                 | Ordinale         | Durée prévue des investissements.                                         |

### **3.4. Identification de la Target**

La variable cible retenue pour la modélisation est :
👉 **“Do you invest in Investment Avenues?”**

Cette variable répond directement à l’objectif du projet : prédire la probabilité qu’un individu investisse.

---

# **Conclusion**

Le dataset Finance Data permet de traiter une problématique pertinente sur le comportement d’investissement des individus. Son mélange de variables démographiques, catégorielles et ordinales constitue une base solide pour réaliser une analyse statistique complète ainsi qu’une modélisation de classification binaire. Grâce à ce dataset, il devient possible d’identifier les facteurs influençant le choix d’investir et d’entraîner des modèles prédictifs performants.

Ce rapport fournit ainsi une présentation complète des données, de la problématique, et des métadonnées nécessaires pour une analyse structurée et conforme aux attentes académiques.
👩‍💻 Interprétation du Code et des Résultats du Notebook Jupyter
Le notebook effectue une analyse exploratoire de données (EDA) sur un jeu de données financier (apparemment des données d'enquête sur l'investissement) et tente ensuite de construire des modèles d'apprentissage automatique (Machine Learning) pour prédire des variables cibles.
________________________________________
1. Préparation et Chargement des Données
Cellule(s)	Code/Action	Interprétation des Résultats
[1]	Téléchargement du jeu de données Kaggle nitindatta/finance-data.	Le jeu de données a été téléchargé et extrait avec succès. Le chemin d'accès aux fichiers est affiché.
[2]	Importation des bibliothèques Python nécessaires (numpy, pandas, seaborn, matplotlib, glob, os, warnings).	Préparation de l'environnement pour l'analyse et la visualisation de données.
[5]	Listing des fichiers (AA.csv, BB.csv) dans le répertoire d'entrée spécifié.	Confirme la présence des deux fichiers CSV qui seront utilisés pour charger les données.
[7]	Chargement des fichiers AA.csv dans Original_data et BB.csv dans Finance_data en tant que DataFrames pandas.	Les deux jeux de données ont été chargés en mémoire.
[8]	Affichage des 5 premières lignes de Original_data.	Révèle les colonnes brutes de l'enquête, qui ont de très longs noms (ex. What do you think are the best options for investing your money? (Rank in order of preference) [Mutual Funds]).
[9]	Affichage des 5 premières et 5 dernières lignes de Finance_data.	Montre que le DataFrame Finance_data est une version nettoyée ou transformée d' Original_data, avec des noms de colonnes plus courts et plus lisibles (Mutual_Funds, Equity_Market, gender, age, etc.). Ce DataFrame est utilisé pour l'analyse et l'apprentissage automatique ultérieurs.
[10], [11]	Vérification des valeurs manquantes (isnull().sum()) dans les deux DataFrames.	Aucune valeur manquante (NaN) n'est trouvée dans aucune des colonnes d' Original_data ou de Finance_data. Les données sont "propres" en termes d'exhaustivité.
[12]	Affichage des informations sur les DataFrames (info()).	Les deux DataFrames ont 40 entrées et 24 colonnes, composées de 8 colonnes int64 (principalement les classements d'investissement) et 16 colonnes object (variables catégorielles comme le genre, la durée, etc.).
[13], [14]	Vérification des lignes dupliquées et de la taille (shape).	Aucune ligne complètement dupliquée n'est trouvée. Les deux jeux de données ont la même taille : (40 lignes, 24 colonnes).
[15]	Comptage des valeurs uniques par colonne (nunique()).	Confirme que le jeu de données est petit (40 observations). Les colonnes numériques de classement ont entre 6 et 7 valeurs uniques, et les variables catégorielles ont entre 2 et 4 valeurs uniques.
[16]	Affichage des types de données (dtypes).	Réitère la structure : 8 colonnes int64 et 16 colonnes object dans les deux jeux de données.
[17], [18]	Séparation des colonnes en types object (category_type) et number (Number_type).	Prépare les données pour l'analyse en fonction du type (visualisation des distributions, corrélations, etc.).
[19]	Affichage des informations sur la mémoire (info(memory_usage='deep')).	Confirme que les DataFrames sont petits, utilisant environ 40.0 KB de mémoire chacun.
[20]	Statistiques descriptives pour les colonnes numériques de Finance_data (describe().T).	Fournit des statistiques clés. L'âge (age) varie de 21 à 35 ans (moyenne de 27.8 ans). Les colonnes de classement (1 = meilleur, 7 = pire) montrent :


* Fonds Mutuels (Mutual_Funds) et PPF (PPF) ont les moyennes les plus faibles (2.55 et 2.025), indiquant qu'ils sont généralement classés comme meilleures options.


* Débentures (Debentures) et Or (Gold) ont les moyennes les plus élevées (5.75 et 5.975), indiquant qu'ils sont généralement classés comme pires options.
[21], [22]	Listage des colonnes numériques et catégorielles.	Confirme la liste des colonnes de chaque type.
________________________________________
2. Visualisation et Analyse Exploratoire (EDA)
Cellule	Code/Action	Interprétation du Graphique et des Résultats
[23]	Histogrammes pour la distribution des classements d'investissement.	Les graphiques montrent la répartition des classements (1 à 7) pour chaque catégorie d'investissement :


* PPF et Fonds Mutuels : Tendance claire vers des classements bas (1-3), confirmant qu'ils sont des options privilégiées.


* Débentures et Or : Tendance claire vers des classements hauts (6-7), confirmant qu'ils sont des options moins préférées.


* Marché Boursier (Equity_Market) et Dépôts Fixes (Fixed_Deposits) : Distribution plus uniforme ou bimodale, suggérant des avis plus partagés.
[24]	Diagramme à barres du taux d'investissement par genre (gender).	Les données sont divisées entre Female et Male. Le graphique montre que le nombre d'hommes et de femmes ayant participé est relativement équilibré (approximativement 20 de chaque).
[25]	Diagramme à barres du nombre de participants par groupe d'âge et par genre.	Le groupe d'âge 23-40 ans est le plus représenté pour les deux genres. Le groupe 41+ ans est absent de l'échantillon. Il y a plus de participants dans le groupe 23-40 ans que dans le groupe 10-22 ans pour les deux genres.
[26]	Diagramme à barres de la distribution de la durée d'investissement (Duration).	La majorité des investisseurs préfèrent une durée de "1-3 years" (1-3 ans) ou "3-5 years" (3-5 ans). L'investissement de "Less than 1 year" (Moins d'un an) est la moins courante.
[27]	Diagramme à barres de la distribution des facteurs influençant l'investissement (Factor).	Le facteur "Risk" (Risque) est le plus fréquemment cité, suivi par "Returns" (Rendements), et le facteur "Safety" (Sécurité) est le moins cité.
[28]	Diagramme à barres du nombre d'investisseurs masculins par âge (filtré par Investment_Avenues == 'Yes').	Montre la répartition par âge des investisseurs masculins actifs. Les hommes dans la vingtaine et la trentaine sont les plus nombreux (pics à 24, 27, 30 ans).
[29]	Graphique linéaire du nombre d'investisseuses féminines par âge (filtré par Investment_Avenues == 'Yes').	Montre la répartition par âge des investisseuses féminines actives. Les pics sont visibles autour de 23, 24, 30, et 34 ans, similaire aux hommes mais avec une distribution légèrement différente.
[30]	Diagramme circulaire des sources d'information utilisées par les investisseurs (filtré par Investment_Avenues == 'Yes').	La source d'information la plus populaire est "Financial Consultants" (35.1%), suivie de près par "Internet" (32.4%). Les "Newspapers and Magazines" et la "Television" sont les moins utilisées.
[31], [32]	Matrice de corrélation et carte de chaleur pour les colonnes numériques.	* Corrélation Age-Classement : L'âge a une faible corrélation positive avec Equity_Market (0.25) et Debentures (0.33), suggérant que les personnes plus âgées pourraient classer ces options légèrement plus haut (ou que l'âge est moins pertinent pour le classement que pour d'autres facteurs).


* Corrélation inverse forte : Debentures vs PPF (-0.51) et Government_Bonds vs Fixed_Deposits (-0.53), indiquant que les personnes qui privilégient l'un ont tendance à déclasser l'autre.
[33], [34]	Comptage et visualisation des investissements des clients qui consultent des "Financial Consultants" (Source == 'Financial Consultants').	Les Débentures et l'Or sont les catégories de classement total le plus élevé (97 chacun), indiquant qu'elles sont les moins préférées parmi les personnes utilisant des consultants financiers (car 1 est le meilleur et 7 le pire). Le PPF (25) est le plus préféré.
________________________________________
3. Modélisation par Apprentissage Automatique (Machine Learning)
Le notebook utilise trois modèles de classification (Logistic Regression, Random Forest, SVM) pour prédire deux variables cibles différentes (Stock_Marktet puis Duration) après avoir encodé toutes les variables catégorielles avec LabelEncoder.
Prédiction de la variable cible : Stock_Marktet
•	Problème : Classification binaire (Yes/No encodé en 1/0).
•	Taille du jeu de test (support) : 8 observations (2 pour la classe 0, 6 pour la classe 1).
•	Résultats bruts ([40]) :
| Modèle | Accuracy | F1-Score (Classe 0) | F1-Score (Classe 1) |
| :--- | :--- | :--- | :--- |
| Logistic Regression | 0.75 | 0.00 | 0.86 |
| Random Forest | 0.75 | 0.00 | 0.86 |
| SVM | 0.75 | 0.00 | 0.86 |
•	Interprétation :
o	L'Accuracy de 0.75 peut sembler élevée, mais la classe 0 est complètement ignorée par les modèles (Precision, Recall et F1-Score sont à 0.00).
o	Cela est dû à un déséquilibre important des classes dans le jeu de test (seulement 2 cas de classe 0). Les modèles prédisent simplement la classe majoritaire (classe 1) pour obtenir une accuracy de 6/8 = 0.75.
o	Conclusion : Ces résultats ne sont pas fiables et le modèle n'a pas appris à distinguer la classe 0.
Prédiction de la variable cible : Duration
•	Problème : Classification multi-classes (4 classes possibles de durée d'investissement).
•	Résultats bruts ([56]) :
| Modèle | Accuracy | Moyenne CV Accuracy |
| :--- | :--- | :--- |
| Logistic Regression | 0.625 | 0.675 |
| Random Forest | 0.875 | 0.650 |
| SVM | 0.375 | 0.350 |
•	Résultats GridSearch (Optimisation des Hyperparamètres) ([61]) :
o	Logistic Regression: Meilleure CV Score de 0.619
o	SVM: Meilleure CV Score de 0.590
o	Random Forest: Meilleure CV Score de 0.595
•	Évaluation du meilleur modèle Random Forest optimisé ([62]) :
o	L'Accuracy sur le jeu de test est 0.875.
•	Interprétation :
o	Le Random Forest présente la meilleure performance sur le jeu de test non vu (0.875) et a également une bonne performance en validation croisée (CV) par rapport aux autres modèles.
o	Le ConvergenceWarning pour la Regression Logistique et la faible Accuracy du SVM indiquent que ces modèles pourraient avoir des difficultés avec les données non normalisées ou la petite taille du jeu de données.
o	Le modèle Random Forest optimisé est le meilleur prédicteur pour la variable Duration dans cet ensemble de données.
