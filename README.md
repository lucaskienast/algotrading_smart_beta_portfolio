# Algotrading Smart Beta ETF Portfolio
This is a smart beta algotrading strategy written in Python aiming to track an index while achieving higher risk adjusted returns. It works as follows:
- load market data
- filter stocks for high dollar volume
- create `dataframe` for close prices and volume of remaining stocks
- get stock index portfolio weights
- compute daily returns across all stocks
- compute cumulative stock index returns
- compute covariance of stock index returns
- $Minimize \left [ \sigma^2_p + \lambda \sqrt{\sum_{1}^{m}(weight_i - indexWeight_i)^2} \right  ]$ where $m$ is the number of stocks in the portfolio, and $\lambda$ is a scaling factor that you can choose to prioritize b/w portfolio variance and distance to index weights
- Define objective function as $\mathbf{x^T} \mathbf{P} \mathbf{x} + \lambda \left \| \mathbf{x} - \mathbf{index} \right \|_2$
- set constraints (no shorting or leveraging)
- get optimal weights for _Smart Beta ETF_ by running optimization with `cvxpy`
- compute daily returns and cumulative returns of _Smart Beta ETF_ weighted portfolio
- compute annualized tracking error $$ TE = \sqrt{252} * SampleStdev(r_p - r_b) $$
- rebalance portfolio every `shift_size` number of days and looking back `chunk_size` number of days since optimal weights will not stay optimal forever
- compute portfolio turnover to measure cost of rebalancing portfolio with $ AnnualizedTurnover =\frac{SumTotalTurnover}{NumberOfRebalanceEvents} * NumberofRebalanceEventsPerYear $
