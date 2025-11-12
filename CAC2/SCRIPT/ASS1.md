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

# Présentation de la base "Seoul Bike Sharing Demand"

## Description principale
Ce dataset contient le nombre de vélos en libre-service loués par heure dans la ville de Séoul, avec des données météorologiques associées ainsi que des informations sur les jours fériés.[4]

## Objectif
Son but principal est la **prédiction du nombre de vélos loués** à chaque heure de la journée, ce qui facilite la gestion et la disponibilité des vélos pour répondre à la demande.[4]

## Caractéristiques clés
- **Type de problème** : Régression, c’est-à-dire prédire une valeur numérique (nombre de vélos loués).[4]
- **Nombre d’instances** : 8 760 (correspondant à une année entière, 365 jours x 24 heures).[4]
- **Nombre de variables** : 13 principales, y compris des données temporelles, météorologiques et autres facteurs contextuels qui influencent la demande.[4]

## Variables principales
| Variable                     | Rôle        | Type                          | Description                                              |
|------------------------------|------------|------------------------------|----------------------------------------------------------|
| Date                         | Feature    | Date                          | La date exacte de mesure                                 |
| Rented Bike Count            | Target     | Integer                       | Nombre de vélos loués durant cette heure               |
| Hour                         | Feature    | Integer (0-23)                | Heure de la journée                                      |
| Temperature                  | Feature    | Continu (°C)                   | Température extérieure                                   |
| Humidity                     | Feature    | Integer (%)                   | Humidité relative                                        |
| Wind speed                   | Feature    | Continu (m/s)                   | Vitesse du vent                                         |
| Visibility                   | Feature    | Integer (10m)                   | Visibilité (en multiples de 10 mètres)                |
| Dew point temperature        | Feature    | Continu (°C)                   | Température du point de rosée                            |
| Solar Radiation              | Feature    | Continu (MJ/m2)                | Radiation solaire                                       |
| Rainfall                     | Feature    | Integer (mm)                   | Précipitations en millimètres                          |
| Snowfall                     | Feature    | Integer (cm)                   | Chute de neige (cm)                                      |
| Seasons                      | Feature    | Categorical (hiver, printemps, été, automne) | Saison de l’année                        |
| Holiday                      | Feature    | Binary                        | Indique si c’est un jour férié                          |

## Particularités
- Pas de valeurs manquantes.
- Le dataset est riche pour modéliser la demande en vélos en fonction des conditions météo, de la saison, du jour de la semaine ou d’événements spéciaux.[4]

## Formats et fichiers disponibles
- Principalement un fichier CSV nommé `SeoulBikeData.csv` d’environ 590 Ko.[4]

## Utilisation typique
Ce dataset est adapté pour **l’apprentissage supervisé par la régression**, notamment pour modéliser et prévoir la demande horaire de vélos dans un contexte urbain intelligent.

***

# Ressources complémentaires
Le dataset est accessible gratuitement, sous licence Creative Commons Attribution 4.0 International (CC BY 4.0), ce qui permet de le partager, de le modifier en donnant crédit à l’auteur.[4]

**Code Python - Statistiques descriptives :**

```python
from ucimlrepo import fetch_ucirepo 
  
# fetch dataset 
seoul_bike_sharing_demand = fetch_ucirepo(id=560) 
  
# data (as pandas dataframes) 
X = seoul_bike_sharing_demand.data.features 
y = seoul_bike_sharing_demand.data.targets 
  
# metadata 
print(seoul_bike_sharing_demand.metadata) 
  
# variable information 
print(seoul_bike_sharing_demand.variables)
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Combine features (X) and target (y) into a single DataFrame
df = pd.concat([X, y], axis=1)

# Convert 'Date' column to datetime objects
df['Date'] = pd.to_datetime(df['Date'], format='%d/%m/%Y')

# Create a 'datetime' column by combining 'Date' and 'Hour'
df['datetime'] = df.apply(lambda row: row['Date'] + pd.Timedelta(hours=row['Hour']), axis=1)

# Display the first few rows of the combined DataFrame
print("Combined DataFrame head:")
display(df.head())



