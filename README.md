# Physics-of-markets

Repo regroupant plusieurs projets liés à la dynamique des marchés.

## Faits stylisés 

Les faits stylisés sont des régularités statistiques du comportement des marchés.

- Data :  
  - Données journalières : AAPL et SPY (tracker S&P500) via yfinance
  - Données intraday : AAPLE et SPY pour 09-02-2012 et 10-02-2012 - échelle minutes de 9h à 16h (heures US) (fichier non fourni dans le repo)
- Analyse empirique des rendements/log-rendements : 
  - Preuves de non-normalité : qq-plot, identification de queues grasses avec la ECDF en scale log-log et scale linear-log
  - Autocorrélation : décroissance très lente de l'autocorrélation de |r| : preuve d'une loi de puissance
- Mesures de volatilité:
  - Variations quadratiques
  - Estimateur de Garman-Klass
- Estimations du nombre de sauts

## Stratégies 

Dans cette partie on travaille sur des stratégies très classiques de trend-following puis mean-reverting, sur différentes périodes afin de montrer qu'elles ne sont pas du tout stationnaires, et qu'il faut savoir être adaptatif aux niveaux des portefeuilles de stratégies pour pouvoir générer de la performance dans tous les cas. 
Puis on s'intéressera ç une approche Deep Learning, et une première approche de donnée alternatives.

- Trend Folowing (croisement de moyennes mobiles)
  - Grille de performances sur les paramètres de la strat (longueur des MB) entière et sur deux périodes -> preuve de non stationnarité de la stratégie
- Mean-Reverting 
  - Grille de performances sur les paramètres de la strat entière et sur deux périodes -> preuve de non stationnarité de la stratégie
- Utilisation d'un LSTM pour la préditcion et la prise de décision
- Google Trend : Exemple Netflix
  - Récupération du score "interest_over_time" de "Netflix" via *pytrends* et long de l'actif Netflix si score > à un certain seuil (très discrétionnaire)
  - Possibilité que les sites streaming/tech soient liés aux recherches Google -> donnée alternative Google Trend intéressante
  - Grille de performance sur le paramètre de seuil
- Google Trend : Crise
  - consituer un portefeuille suceptible de baisser fortement en temps de crise sanitaire ou économique
  - suveillance des scores d'intérêt des mots "krach", "crisis", "virus" -> short des actifs en fonction de leur catégories
  - Preuve de la significativité du signal -> performance pour "virus" lors du covid par exemple 
  - Très discrétionnaire -> a utiliser en stratégies "défensives"

## Etats de marchés

Data : 981 actions US pour 1929 pas de temps

- Classification des Etats de marchés (état de jours) via la méthode de clustering de Louvain (note : il y a juste à transposer la matrice des rendements pour obtenir les clusters de titres dans l'algorithme) -> nombre d'états de marchés stables au cours du temps (entre 3 et 10, calculé sur fenetre de calibration de 250 pas de temps)
- Stratégie basée sur les états de marchés :
  - Connaissant le dernier état de marché de la fenetre : 
    - Sélection de l'état suivant le plus fréquent dans la fenetre de calibration conditionnellement au dernier état de marché
    - Conditionnellement a cet état sélectionné, calcul de la moyenne des rendements de chaque actifs
    - Trie des rendements, short des 5 pires actifs et long des 5 meilleurs pour le pas suivant (tenue de position pour un pas seulement)
    - Répétition de la strat sur 100 fenêtres glissantes pour les premières données, puis pour 100 fenêtres à partir du 1000ème pas de temps : performance dans les deux cas
- Prédiction de la direction d'un titre :
  - Tentative de prédiction du signe du prochain rendement avec ANN / XGBoost : très peu de pouvoir prédictif (un peu plus de 50%)
  - A continuer : essayer d'autres architecture et d'autres réseaux tels que le LSTM.

## Modèle d'agents

- Jeu de la minorité grand canonique
  - Modèle d'agents de spéculateurs et producteurs (fournisseurs de prévisibilité)
  - Etude de la dynamique de la prévisibilité en fonction de l'évolution des paramètres du modèle (exemple : trop de spéculateurs pour pas assez de producteurs -> absence de prévisibilité -> explosion des fluctuations car ils apprennent du bruit -> herding)
- Gains et impacts de marché 
  - Etude du gain moyen des producteurs et spéculation en fonction de l'évolution des deux parties
  - Etude de la différence entre gain réel et espéré d'un agent entré en cours de jeu
