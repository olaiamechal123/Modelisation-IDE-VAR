# Modélisation économétrique des déterminants macroéconomiques des IDE au France : approche VAR

## Contexte  
Ce projet vise à modéliser les déterminants macroéconomiques des Investissements Directs Étrangers (IDE) à travers l’estimation d’un modèle Vector Autoregressive (VAR). Il cherche à analyser les dynamiques des flux d’IDE en réponse aux principales variables macroéconomiques, afin d’identifier les facteurs exerçant l’impact le plus significatif, positif ou négatif.

## Objectifs

Examen des corrélations entre les flux d’IDE et leurs déterminants macroéconomiques potentiels.

Analyse prédictive et dynamique des relations entre les IDE et ces déterminants à l’aide du cadre VAR (impulse responses, décomposition de la variance, causalité au sens de Granger, etc.).

## Outils et technologies utilisés

### Python
- **Collecte des données** : `requests`, `BeautifulSoup`  
- **Traitement et nettoyage des données** : `pandas`  
- **Visualisation statistique et exploratoire** : `matplotlib`, `seaborn`

### R
- **Analyse exploratoire et visualisation** :
  - `ggplot2` → boxplots (détection des outliers) 
  - `corrplot` → matrice de corrélation entre IDE et variables macroéconomiques  
- **Traitement des séries chronologiques** : `tseries`  
- **Modélisation économétrique** : `vars` 

## collection de données

Les données ont été collectées à partir du site https://donnees.banquemondiale.org. Nous avons utilisé la technique de web scraping avec la bibliothèque BeautifulSoup afin d’extraire automatiquement le fichier Excel

## Traitement des données

Premièrement, on définit la variable **IDE** qui représente un investissement durable réalisé par un acteur économique (entreprise, individu) d’un pays dans une entreprise située dans un autre pays.

Ensuite, on définit les déterminants macroéconomiques de l’IDE :

- **Taille du marché** : représente le revenu total maximal qu’une entreprise peut générer sur un marché donné.  
- **Croissance économique** : l’augmentation durable de la production de biens et services d’un pays sur une période donnée.  
- **Ouverture commerciale** : le degré d’intégration d’une économie nationale avec le reste du monde, caractérisé par de faibles barrières (tarifs douaniers, quotas) aux échanges de biens et services, permettant aux acteurs économiques de commercer librement avec l’étranger, contrairement à une économie fermée.  
- **Inflation** : hausse générale et durable des prix des biens et services.  
- **Taux de change réel** : désigne la valeur relative d’une monnaie par rapport à une autre.  
- **Salaire moyen** : la moyenne arithmétique de tous les salaires d’une population donnée, calculée en additionnant tous les salaires et en divisant par le nombre total de salariés.

Après la définition des variables, on passe maintenant aux étapes pour préparer le dataset final :

On utilise **pandas** pour :  
- extraire à partir des fichiers Excel les déterminants ainsi que l’IDE, avec une colonne pour les années ;  
- fusionner ces déterminants avec l’IDE en utilisant la colonne « Année » dans un DataFrame ;  
- détecter les types de données et les transformer en type numérique ;  
- détecter les valeurs manquantes et les traiter par la méthode de la moyenne et la méthode forward fill ;
-  enfin, stocker ce DataFrame dans un fichier Excel.
  
  Ces étapes sont réalisées dans le fichier [Data_Preparation](https://github.com/olaiamechal123/Modelisation-IDE-VAR/blob/main/Data_Preparation.ipynb).
## Modelisation

Dans cette partie, les étapes suivantes ont été réalisées :

1. **Détection graphique des valeurs aberrantes**  
   Visualisation  pour identifier et analyser les outliers.

2. **Analyse de corrélation**  
   Étude des corrélations entre les déterminants macroéconomiques et les flux d’**IDE** .

3. **Transformation en série temporelle**  
   Conversion du dataset en objets de type série chronologique avec le package `tseries` (R).

4. **Test de stationnarité**  
   Application du test **ADF**  sur chaque variable pour vérifier la stationnarité.

5. **Différenciation**  
   Différenciation d’ordre 1 des variables non stationnaires afin de les rendre stationnaires.

6. **Choix du nombre de retards (lags)**  
   Détermination du nombre optimal de retards via les critères d’information BIC.

7. **Standardisation des variables**  
   Centrage et réduction (standardisation) des séries pour la modélisation VAR.

8. **Estimation du modèle VAR**  
   Estimation du modèle Vector Autoregressive avec le package `vars` (R).

9. **Validation du modèle**  
   - Test de stabilité   
   - Test d’autocorrélation des résidus  
   - Test de normalité des résidus 

 Ces étapes sont réalisées dans le notebook [Modelisation](https://github.com/olaiamechal123/Modelisation-IDE-VAR/blob/main/Modelisation/Notebook.Rmd).


