# COURS DE SCIENCE DES DONNÉES
# A.LARHLIMI

## HOUMIRI Khadija 
## École Nationale de Commerce et de Gestion (ENCG) - 4ème Année

---
Objectif du code
Ce code permet de :

Installer le package ucimlrepo.

Télécharger le jeu de données via son identifiant.

Séparer les variables explicatives (features) et la variable cible (targets).

Afficher les métadonnées et informations sur les variables du jeu de données.​

Explication ligne par ligne
python
from ucimlrepo import fetch_ucirepo
Cette ligne importe la fonction fetch_ucirepo depuis le package ucimlrepo, qui sert à télécharger des jeux de données du dépôt UCI ML.​

python
pip install ucimlrepo
C’est une commande shell qui installe le package ucimlrepo nécessaire pour le reste du code.​

python
# fetch dataset
seoul_bike_sharing_demand = fetch_ucirepo(id=560)
Cette ligne télécharge le jeu de données "Seoul Bike Sharing Demand" (identifiant 560) et le stocke dans la variable seoul_bike_sharing_demand. Cette variable contient :

Les données sous forme de dataframes (features, targets, etc.).

Les métadonnées sur le jeu de données.

Une description des variables.​

python
# data (as pandas dataframes)
X = seoul_bike_sharing_demand.data.features
y = seoul_bike_sharing_demand.data.targets
X contient les variables explicatives (features) du jeu de données sous forme de dataframe Pandas.

y contient la ou les variable(s) cible(s) (targets) du jeu de données sous forme de dataframe Pandas. Cela permet ensuite d’entraîner des modèles de machine learning, par exemple en régression ou classification.​

python
# metadata
print(seoul_bike_sharing_demand.metadata)
Affiche les métadonnées du jeu de données (description, nombre d'instances, caractéristiques, source, type, etc.) pour que tu puisses comprendre le contenu et la structure globale du dataset.​

python
# variable information
print(seoul_bike_sharing_demand.variables)
Affiche les informations sur chaque variable : nom, rôle (feature, cible, ID...), type (numérique, catégoriel), description, unités et s’il y a des valeurs manquantes.​

Structure de l’objet retourné
L’objet retourné par fetch_ucirepo contient :

data : dictionnaire de dataframes (features, targets, ids, original).

metadata : métadonnées du dataset (nom, type, nombre d’instances, résumé…).

variables : tableau synthétique sur chaque variable (nom, rôle, type, description…).​

Exemple d’utilisation :
Élément	Utilisation dans le code	Description
.data.features	X = ...	Variables explicatives (données indépendantes)​
.data.targets	y = ...	Variables cibles (à prédire)​
.metadata	print(...)	Description générale du dataset​
.variables	print(...)	Informations détaillées sur les variables​
Cas d’application
Ce code est utile dans tous les travaux de traitement de données et machine learning, pour :

Explorer les informations du jeu de données.

Préparer les dataframes pour modélisation.

Comprendre rapidement la structure des variables et les métadonnées sans devoir aller manuellement sur le site UCI.​

Remarque pratique
Assure-toi d’avoir bien installé le package avec pip install ucimlrepo avant d’utiliser l’import et que tu disposes de Python et Pandas sur ton environnement.
