<h1 align='center'> Market States </h1>
  
[<h1 align='center'>![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Gruz77/Physics-of-Markets/blob/main/Market_States/Market_States.ipynb)</h1>

Data: 981 US stocks for 1929 time steps

## Louvain
- Classification of market states (state of days) via the Louvain clustering method (note: there is just to transpose the matrix of returns to obtain the clusters of securities in the algorithm) -> number of stable market states over time (between 3 and 10, calculated on a calibration window of 250 time steps)
## Strategy based on market states
- Knowing the last market state of the window : 
  - Selection of the next most frequent state in the calibration window conditional on the last market state
  - Conditional on this selected state, calculation of the average of the returns of each asset
  - Sort returns, short the 5 worst assets and long the 5 best for the next step (hold position for one step only)
  - Repeat the strategy over 100 sliding windows for the first data, then for 100 windows from the 1000th time step: performance in both cases
