# Etats de marchés

Data : 981 actions US pour 1929 pas de temps

## Louvain
- Classification des Etats de marchés (état de jours) via la méthode de clustering de Louvain (note : il y a juste à transposer la matrice des rendements pour obtenir les clusters de titres dans l'algorithme) -> nombre d'états de marchés stables au cours du temps (entre 3 et 10, calculé sur fenetre de calibration de 250 pas de temps)
## Stratégie basée sur les états de marchés
- Connaissant le dernier état de marché de la fenetre : 
  - Sélection de l'état suivant le plus fréquent dans la fenetre de calibration conditionnellement au dernier état de marché
  - Conditionnellement a cet état sélectionné, calcul de la moyenne des rendements de chaque actifs
  - Trie des rendements, short des 5 pires actifs et long des 5 meilleurs pour le pas suivant (tenue de position pour un pas seulement)
  - Répétition de la strat sur 100 fenêtres glissantes pour les premières données, puis pour 100 fenêtres à partir du 1000ème pas de temps : performance dans les deux cas
 
## Prédiction de la direction d'un titre
- Tentative de prédiction du signe du prochain rendement avec ANN / XGBoost : très peu de pouvoir prédictif (un peu plus de 50%)
- A continuer : essayer d'autres architecture et d'autres réseaux tels que le LSTM.
