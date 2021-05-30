<h1 align='center'> Stylized Facts </h1>

[<h1 align='center'>![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/googlecolab/colabtools/blob/master/notebooks/colab-github-demo.ipynb)</h1>

Stylized facts are statistical regularities of market behaviour.

- Data :  
  - Daily data: AAPL and SPY (S&P500 tracker) via yfinance
  - Intraday data: AAPLE and SPY for 09-02-2012 and 10-02-2012 - minute scale from 9am to 4pm (US time) (file not provided in repo)
 
## Empirical analysis of returns/log returns 
- Evidence of non-normality: qq-plot, fat-tail identification with ECDF in scale log-log and scale linear-log
- Autocorrelation: very slow decay of the autocorrelation of |r|: evidence of a power law

## Measures of volatility:
- Quadratic variations
- Garman-Klass estimator

## Estimates of the number of jumps
- Proof of a power law of the number of jumps
