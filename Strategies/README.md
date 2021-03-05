# Stratégies 

Une stratégie peut être vue comme un diagnostic, c'est un outil de mesure, une réduction de l'information disponible sur les marchés, dont le but est d'extraire du signal et de l'augmenter par rapport au bruit. En soit, une stratégie doit être vue comme un titre (on peut considérer un portefeuille de stratégies).

On note que dans notre cas, pour notre signal noté x, il est très important de décaler le pas temporel au temps suivant pour l'utiliser au temps t+1 (il ne faut pas inclure le rendement futur lorsqu'on utilise un signal sur le passé). 

On a donc :
g_t = x_t * r_(t+1)
Avec g la valeur de la stratégie, x notre signal, et r le rendement (on utilise toujours des logs-rendements).

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
