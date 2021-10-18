<h1 align='center'> Strategies </h1>

[<h1 align='center'>![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Gruz77/Physics-of-Markets/blob/main/Strategies/Strategies.ipynb)</h1>

A strategy can be seen as a diagnostic, a measurement tool, a reduction of the information available on the markets, whose aim is to extract signal and increase it with respect to the noise. In other words, a strategy must be seen as a security (we can consider a portfolio of strategies).

Avoid look-ahead bias: we note that in our case, for our signal noted x, it is very important to shift the time step to the next time to use it at time t+1 (we must not include the future return when using a signal on the past). 

Thus, we have :
<br>
<p style="text-align:center">g<sub>t</sub> = x<sub>t-1</sub>*r<sub>t</sub></p>

With :
- g the value of the strategy
- x our signal
- r the return (we always use log returns).

We are going to work on very classical trend-following and mean-reverting strategies, over different periods, in order to show that they are not at all stationary, and that we need to know how to be adaptive at the level of the strategy portfolios in order to generate performance. (A strategy that works today will probably not work tomorrow). 

Then we will look at a Deep Learning approach, and a first approach of "alternative" data.

## Trend Following (really basic: crossing moving averages)
- Performance grid on the parameters of the entire strategy (length of the MBs) and over two periods -> proof of non-stationarity of the strategy

## Mean-Reverting 
- Performance grid on the parameters of the entire strat and over two periods -> proof of non-stationarity of the strategy

## Original strategies using Google Trend : 
- Example Netflix
  - Retrieve the "interest_over_time" score of "Netflix" via *pytrends* and long the Netflix asset if score > a certain threshold (very discretionary)
  - Possibility that streaming/tech sites are linked to Google searches -> interesting alternative Google Trend data
  - Performance grid on threshold parameter
- Crisis portfolio
  - build up a portfolio that is likely to fall sharply in times of health or economic crisis
  - monitoring of the interest scores of the words "crash", "crisis", "virus" -> short assets according to their categories
  - Proof of signal significance -> performance for "virus" during covid for example 
  - Very discretionary -> to be used in "defensive" strategies
