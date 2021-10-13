# basic_VaR
Building a basic VaR model in Python.

Following along with a video from the YouTube channel Financial Programming with Ritvik.
Link to channel: [HERE](https://www.youtube.com/channel/UCyMifqUrSntvvrrGMaVPkrw)
Link to video: [HERE](https://youtu.be/hdEp8A90RdM)

# Steps to the VaR Model

## Create a portfolio
* Create two arrays - one with stock tickers and the other with their respective weights.
* Get the closing price (or the Adjusted Close) for each stock over a given time period. We use the yfinance API to get this information. (`df`)

## Perform all the basic calculations.
* Calculate the daily percentage change. (` returns = df.pct_change()`)
* Calculate the covariance matrix. (`cov_matrix = returns.cov()`)
* Calculate the daily average returns of each stock over the time period. (`avg_returns = returns.mean()`)
* Sum the number of observations. (`returns.count()[0]`)

## Construct the Normal Distribution Curve and Calculate VaR
Using the scipy.stats library. We will need to get the porfolio mean and standard deviation to do this.
`@` = NumPy's two dimensional array dot product

* Calculate the portfolio mean (`port_mean = avg_returns @ weights`)
* Calculate the portfolio standard deviation (`port_std = np.sqrt(weights.T @ cov_matrix @ weights)`)
* Set a confidence level (0.05)
* Calculate VaR using the percent point function. (`VaR = norm.ppf(0.05, port_mean, port_std)`)

## Calculate VaR over 5 Days
`VaR * np.sqrt(5)`