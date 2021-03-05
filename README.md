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

Une stratégie peut être vue comme un diagnostic, c'est un outil de mesure, une réduction de l'information disponible sur les marchés, dont le but est d'extraire du signal et de l'augmenter par rapport au bruit. En soit, une stratégie doit être vue comme un titre (on peut considérer un portefeuille de stratégies).

On note que dans notre cas, pour notre signal noté ![img](http://www.sciweavers.org/tex2img.php?eq=x_t&bc=White&fc=Black&im=jpg&fs=12&ff=arev&edit=0), il est très important de décaler le pas temporel au temps suivant pour l'utiliser au temps t+1 (il ne faut pas inclure le rendement futur lorsqu'on utilise un signal sur le passé). 

On a donc :
![img](http://www.sciweavers.org/tex2img.php?eq=g_t%20%3D%20x_tr_%7Bt%2B1%7D&bc=White&fc=Black&im=jpg&fs=12&ff=arev&edit=0)
Avec ![img](http://www.sciweavers.org/tex2img.php?eq=g&bc=White&fc=Black&im=jpg&fs=12&ff=arev&edit=0) la valeur de la stratégie, ![img](http://www.sciweavers.org/tex2img.php?eq=x%20%5Cin%20%5C%7B-1%2C0%2C1%5C%7D&bc=White&fc=Black&im=jpg&fs=12&ff=arev&edit=0) notre signal, et ![img](http://www.sciweavers.org/tex2img.php?eq=r&bc=White&fc=Black&im=jpg&fs=12&ff=arev&edit=0) le rendement (on utilise toujours des logs-rendements).

Nous allons travailler sur des stratégies très classiques de trend-following puis mean-reverting, sur différentes périodes afin de montrer qu'elles ne sont pas du tout stationnaires, et qu'il faut savoir être adaptatif aux niveaux des portefeuilles de stratégies pour pouvoir générer de la performance. (Une stratégie qui marche aujourd'hui ne marchera très probablement plus demain). 

Puis on s'intéressera à une approche Deep Learning, et une première approche de donnée alternatives.

- Trend Folowing (croisement de moyennes mobiles)
  - Grille de performances sur les paramètres de la strat (longueur des MB) entière et sur deux périodes -> preuve de non stationnarité de la stratégie
- Mean-Reverting 
  - Grille de performances sur les paramètres de la strat entière et sur deux périodes -> preuve de non stationnarité de la stratégie
- Utilisation d'un LSTM pour la prédiction et la prise de décision (à développer)
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
