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
