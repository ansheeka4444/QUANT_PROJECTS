# Order Book Imbalance Analysis and Short-Horizon Trading Strategy Backtesting

## Project Overview
This project analyzes cryptocurrency Level-2 order book snapshots to understand market microstructure and evaluate short-horizon trading signals.

It uses order book depth, bid-ask spread, mid-price, microprice, and Order Book Imbalance (OBI) to identify potential buying and selling signals. A 30-second forward-return framework is used to evaluate these signals through a simplified backtesting approach.

## Objectives
- Analyze Level-2 order book data.
- Calculate Order Book Imbalance (OBI).
- Understand bid-ask spread and market depth.
- Calculate mid-price and microprice.
- Generate BUY, SELL, and NEUTRAL signals.
- Evaluate 30-second forward price movements.
- Measure trading performance and risk.
- Store analytical results using SQLite.

## Dataset
**Source:** Kaggle – Cryptocurrency Order Book Dataset

Dataset link: https://www.kaggle.com/datasets/polyorderbooks/polymarket-crypto-5min-orderbooks

The dataset contains order book snapshots with fields such as:
- Market and token identifiers
- Bid and ask prices
- Bid and ask sizes
- Best bid and best ask
- Snapshot timestamps
- Time remaining until market close

## Technologies Used
- Python
- Jupyter Notebook
- Pandas and NumPy
- Matplotlib
- SQLite
- PyArrow

## Key Features

### 1. Data Cleaning
- Handled missing and invalid values.
- Processed nested order book arrays.
- Removed duplicate snapshots.
- Filtered invalid and crossed order books.

### 2. Feature Engineering
- Mid-Price
- Bid-Ask Spread
- Relative Spread
- Order Book Imbalance (OBI)
- Microprice
- Top-five-level market depth

### 3. Signal Generation
The strategy uses OBI thresholds:

- OBI above +0.15: BUY signal
- OBI below -0.15: SELL signal
- Otherwise: NEUTRAL signal

### 4. Forward Return Analysis
The project matches future order book snapshots approximately 30 seconds after each observation to evaluate short-term price movement.

### 5. Backtesting and Performance Evaluation
The strategy evaluates:
- Total trades
- Win rate
- Gross and net PnL
- Average PnL
- Profit factor
- Maximum drawdown
- BUY versus SELL performance
- Threshold sensitivity
- Non-overlapping trade performance
- Transaction-cost sensitivity

### 6. SQL Analysis
SQLite is used to store and query:
- Order book analysis
- Trading results
- Cost sensitivity
- BUY/SELL performance
- Non-overlapping trades
- Threshold analysis

## Project Outputs
The notebook generates:

- `project1_output.csv`
- `project1_trades.csv`
- `threshold_cost_analysis.csv`
- `buy_sell_analysis.csv`
- `non_overlapping_trades.csv`
- `obi_threshold_analysis.csv`
- `hft_project1.db`

## How to Run

1. Install the required libraries:

   ```bash
   pip install pandas numpy matplotlib pyarrow
   ```

2. Download the dataset from Kaggle.

3. Place the dataset file (`btc.parquet`) in the project directory.

4. Open the Jupyter Notebook.

5. Run the notebook cells sequentially.

## Important Limitations
This is an educational research and backtesting project, not a production-ready HFT trading system.

The current simulation assumes execution at displayed best bid/ask prices and does not fully model queue priority, partial fills, exchange latency, market impact, or live transaction costs.

Threshold selection is based on historical observations and requires out-of-sample and walk-forward validation before any real-world application.

## Learning Outcomes
- Practical understanding of order book dynamics.
- Experience with Level-2 market data.
- Feature engineering using Python.
- Short-horizon signal evaluation.
- Backtesting and risk metric calculation.
- SQL-based financial data analysis.

# Algorithmic Trading Strategy Backtesting and Performance Evaluation

## Project Overview

This project implements a Python-based algorithmic trading backtesting framework to evaluate a Moving Average (MA) Crossover strategy across five major Indian NSE-listed stocks.

The framework uses historical stock market data to generate trading signals, simulate trade execution, account for transaction costs and slippage, and evaluate strategy performance against a Buy-and-Hold benchmark.

It also incorporates chronological training and testing datasets to examine out-of-sample performance.

## Objectives

- Develop a rule-based algorithmic trading strategy.
- Analyze historical stock market data.
- Generate trading signals using technical indicators.
- Simulate next-day order execution.
- Account for transaction costs and slippage.
- Evaluate risk-adjusted trading performance.
- Compare strategy returns with a benchmark.
- Store and analyze results using SQL.

## Technologies Used

| Technology | Purpose |
|---|---|
| Python | Strategy development |
| Pandas | Data manipulation |
| NumPy | Numerical calculations |
| Matplotlib | Data visualization |
| yfinance | Historical market data |
| SQLite | Database management |
| Jupyter Notebook | Development and analysis |

## Stocks Analyzed

The framework analyzes the following NSE-listed stocks:

- Reliance Industries (RELIANCE.NS)
- Tata Consultancy Services (TCS.NS)
- Infosys (INFY.NS)
- HDFC Bank (HDFCBANK.NS)
- ICICI Bank (ICICIBANK.NS)

Historical daily OHLCV data is downloaded using Yahoo Finance through the yfinance library.

## Methodology

### 1. Data Collection and Preprocessing

- Download historical OHLCV data.
- Handle missing and invalid values.
- Remove duplicate timestamps.
- Validate stock prices.
- Organize data chronologically.

### 2. Technical Indicator Calculation

The strategy uses:

- Simple Moving Average (SMA 20)
- Simple Moving Average (SMA 50)
- Exponential Moving Average (EMA 20)

### 3. Trading Signal Generation

A moving-average crossover strategy generates trading signals.

- BUY: 20-day SMA is above 50-day SMA.
- SELL: 20-day SMA moves below or becomes equal to 50-day SMA.
- HOLD: No position change is required.

Signals are generated using closing-price information and executed at the next available trading day's opening price.

### 4. Backtesting

The framework simulates historical trading activity using:

- Long-only positions.
- Next-day opening-price execution.
- Position-change detection.
- Transaction-cost modeling.
- Slippage assumptions.
- Strategy return calculation.

### 5. Train-Test Evaluation

The historical dataset is divided chronologically:

- Training data: 70%
- Testing data: 30%

Moving averages are calculated using historical observations before the split so that the testing period retains the required indicator warm-up history.

The strategy is evaluated separately on training and testing periods.

### 6. Performance Evaluation

The framework calculates:

- Total Return
- Compound Annual Growth Rate (CAGR)
- Sharpe Ratio
- Maximum Drawdown
- Annualized Volatility
- Win Rate
- Profit Factor
- Average Trade Return

Strategy performance is compared against a Buy-and-Hold benchmark.

## SQL Database Integration

SQLite stores the backtesting results and trade information.

Database tables include:

- `multi_ticker_results`
- `trade_log`
- `trade_metrics`
- Individual stock backtesting tables

SQL queries are used to:

1. Rank stocks by testing-period Sharpe ratio.
2. Summarize winning and losing trades.
3. Compare trade performance across stocks.

## Visualizations

The project generates:

- Multi-stock strategy equity curves.
- Strategy vs Buy-and-Hold comparisons.
- Training vs testing Sharpe ratio charts.
- Portfolio drawdown comparisons.

## Project Outputs

The notebook exports:

- `multi_ticker_results.csv`
- `trade_log.csv`
- `trade_metrics.csv`
- Individual stock backtesting CSV files.
- `algorithmic_trading.db`

## How to Run

1. Install Python and Jupyter Notebook.
2. Install the required libraries:

   ```bash
   pip install pandas numpy matplotlib yfinance
   ```

3. Open the Jupyter Notebook.
4. Run the notebook cells sequentially.
5. Ensure internet connectivity for historical data downloads.
6. Review the generated metrics, charts, SQL outputs, and CSV files.

## Limitations

- Uses daily market data rather than tick-level or Level-2 order book data.
- Assumes simplified execution at the next trading day's opening price.
- Transaction costs and slippage are modeled using fixed assumptions.
- Does not simulate actual exchange latency, queue priority, partial fills, or market impact.
- Historical backtesting does not guarantee future trading performance.

## Future Enhancements

- Implement intraday and tick-level backtesting.
- Integrate Level-2 order book data.
- Explore momentum and mean-reversion strategies.
- Implement walk-forward validation.
- Add parameter optimization using training data.
- Incorporate realistic execution and market-impact models.

## Conclusion

This project demonstrates the development of a multi-stock algorithmic trading backtesting framework using Python and SQL. It combines historical data analysis, technical indicators, trading simulation, transaction-cost modeling, risk metrics, and benchmark comparison to evaluate quantitative trading strategies.

# Statistical Arbitrage and Pairs Trading Strategy Backtester

## Project Overview

This project implements a Python-based statistical arbitrage research and backtesting system using historical stock market data.

It analyzes the relationship between two stocks, estimates their hedge ratio, identifies potential mean-reversion opportunities, and evaluates a pairs-trading strategy using historical price movements.

The project uses RELIANCE.NS and ONGC.NS as the selected stock pair.

## Objectives

- Analyze relationships between stock prices.
- Test cointegration between selected stocks.
- Estimate hedge ratios using OLS regression.
- Calculate spread and Z-scores.
- Estimate mean-reversion half-life using an Ornstein-Uhlenbeck (OU) model.
- Generate long-spread and short-spread trading signals.
- Evaluate strategy performance on training and testing datasets.

## Technologies Used

- Python
- Pandas
- NumPy
- Matplotlib
- Statsmodels
- YFinance
- SQLite
- Jupyter Notebook

## Methodology

### 1. Data Collection and Preprocessing
- Fetch historical stock prices using Yahoo Finance.
- Align stock prices based on trading dates.
- Handle missing values and prepare the dataset.

### 2. Statistical Analysis
- Calculate correlation between the selected stocks.
- Perform the Engle-Granger cointegration test.
- Estimate the hedge ratio using OLS regression.

### 3. Mean-Reversion Analysis
- Calculate the price spread using the estimated hedge ratio.
- Estimate mean-reversion speed and half-life using the OU approach.
- Calculate rolling Z-scores to identify spread deviations.

### 4. Trading Signal Generation
- Generate a short-spread signal when Z-score reaches the upper threshold.
- Generate a long-spread signal when Z-score reaches the lower threshold.
- Exit positions when the spread moves back towards its mean.
- Apply a stop-loss threshold to manage adverse movements.

### 5. Backtesting and Performance Evaluation
- Use chronological training and testing datasets.
- Simulate trading positions with a one-day execution lag.
- Include simplified transaction costs.
- Evaluate total return, CAGR, Sharpe ratio and maximum drawdown.
- Maintain individual trade records.

## Database and Outputs

The project creates an SQLite database named `pairs_trading.db` containing:

- `stock_prices`
- `pair_signals`
- `trade_log`

Generated output files:

- `stock_prices.csv`
- `pair_signals.csv`
- `performance_metrics.csv`
- `trade_log.csv`

Visualizations:

- Spread and Z-score analysis
- Portfolio performance
- Strategy drawdown

## Key Findings

- Observed strong correlation between RELIANCE and ONGC.
- The Engle-Granger cointegration test did not pass the 5% significance threshold.
- Training and testing performance showed different results.
- Out-of-sample results highlighted the importance of statistical validation and strategy generalization.

## Limitations

- Uses daily historical price data rather than tick-level data.
- Tests only one stock pair.
- Uses a fixed hedge ratio.
- Transaction costs are simplified.
- Does not simulate order-book execution, queue position, partial fills or market latency.

## Conclusion

This project demonstrates the application of statistical modelling, quantitative research, and backtesting techniques in financial markets. It also highlights why correlation alone is insufficient to establish a reliable pairs-trading relationship and why out-of-sample validation is important.

**Note:** This is an educational quantitative research and backtesting project, not a production-ready trading system or a recommendation to trade.
