# Faits stylisés 

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
