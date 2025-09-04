# MOBIGIS_trafic_analysis
Analyse (en R et Python) des 18 stations de comptage vélo à Bruxelles (2024) pour comprendre les profils d’usage et prédire le traffic. Résultats explorés dans un dashboard Power BI. ACP · Clustering · OLS · XGBoost · Power BI
Accès à la base de données

Pour des raisons de confidentialité, les identifiants de connexion à la base de données ne sont pas inclus dans ce dépôt public. Vous pouvez me contacter à olivier.lebert@hotmail.com pour obtenir les informations d'accès si vous voulez éxécuter le fichier qmd. 
Le script vous demandera ensuite le mot de passe via une invite sécurisée (getPass()) et ne le stockera pas.

# Résultats clés

ACP sur profils horaires (centré-réduit) → axe 1 : profils à pics vs lisses ; axe 2 : semaine vs week-end. 
HCPC + k-means → 2 clusters : un groupe “forte fréquentation/pics fin de journée”. 
OLS (Count puis log1p(Count)) : lecture interprétable R² ≈ 0.52 avant transformation de la cible, ensuite R² = 0.71 (mais hétéroscédasticité → limite gaussienne encore présentes bien que partiellement corrigées). 
XGBoost : nette hausse de performance prédictive – test set : R² ≈ 0,85, MAE ≈ 20, MSE ≈ 1 543,9, Poisson dev. ≈ 11,1. 
Power Bi : 
  Page 1 : Nuage de points + slicers permettent d'évaluer visuellement la performance du modèle en fonction de la station, de la date et de l'heure. 
  Page 2 : Graphique en ligne confrontant les prédictions à la réalité + Heatmap WAPE % par jour × heure pour repérer les créneaux les plus difficiles (tôt le matin, en particulier le week-end).

En bref, les effets station, horaire et calendrier dominent, la météo reste pertinente mais a une incidence plus limitée (la pluie a une influence négative, à l'inverse de l'ensoleillement).

# Fichiers joints 
Rapport interactif (quarto qui nécessite le code à demander par mail) : Analyse_bike.qmd 
Rapport PDF : Rapport_bike.pdf 
Slides PowerPoint PDF : Bruxelles_mobilité.pdf 
Dashboard Power BI (+ csv) : 
  prêt à l’emploi = powerbi/bike_dashboard.pbix 
  template (demande le CSV) = powerbi/bike_dashboard.pbit + data/bike.csv

# Packages nécessaires
## Les packages R suivants seront installés automatiquement au premier lancement :
    RMariaDB
    getPass
    DBI
    dplyr
    lubridate
    tidyr
    factoextra
    FactoMineR
    tibble
    ggplot2
    reticulate
    quarto

## En Python (via l’environnement reticulate) :
    pandas
    numpy
    matplotlib
    seaborn
    xgboost
    scikit-learn
    statsmodels
