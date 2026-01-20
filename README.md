# GenAI Stock Analyzer & Portfolio Optimization

This project combines AI-assisted prompts with financial data analysis using Python libraries to compute KPIs, visualize stock performance, and perform portfolio optimization. It demonstrates how to integrate LLMs, yfinance, and portfolio optimization techniques for research or investment analysis.

## 1. Libraries and Functions

### Core Python Libraries

- **numpy** – numerical operations and vectorized calculations
- **pandas** – data manipulation and tabular storage
- **matplotlib** – visualization of KPIs and stock performance
- **scipy.optimize** – optimization routines for Modern Portfolio Theory (MPT)

### Financial Libraries

- **yfinance** – fetches historical stock and crypto prices
- **PyPortfolioOpt** – advanced portfolio optimization models including Black-Litterman
- **risk_models** and **expected_returns** – used for sample covariance and mean historical return computation

### AI Integration

- **langchain_groq** – connects to the Groq LLM for generating prompts, explanations, and code snippets

**Prompt Functions:**
- `output(prompt)` – sends a prompt to the LLM and displays the output
- `extract_assets(asset_name)` – extracts stock tickers from names like "Apple (AAPL)" → "AAPL"

## 2. Inputs: Keys and Assets

### API Keys

The project requires API keys to access AI models:
- **Groq:** `groq_api_key`
- (Optional for other models: OpenAI, Google Gemini, OpenRouter.ai)

### Assets

The analysis is performed on the following assets:
```python
assets = [
    "Apple (AAPL)",
    "Amazon (AMZN)",
    "Bitcoin (BTC-USD)",
    "Alphabet (GOOGL)",
    "Meta (META)",
    "Microsoft (MSFT)",
    "Nvidia (NVDA)",
    "S&P 500 index (SPY)",
    "Tesla (TSLA)"
]
```

### Analysis Period

- **Start Year:** 2024
- **End Year:** 2025

The tickers are extracted for fetching historical data via yfinance.

## 3. Output: Data Visualization, KPIs, and Portfolio

### 3.1 Data Visualization

Historical stock prices (Close and Adjusted Close) are downloaded and displayed.

Visualizations include:
- **Relative Strength Index (RSI)** – momentum indicator; overbought above 70, oversold below 30
- **Bollinger Bands** – volatility indicator with 20-day moving average and ±2 standard deviation bands
- **MACD (Moving Average Convergence Divergence)** – trend indicator calculated from 12- and 26-day EMAs

### 3.2 Key Performance Indicators (KPIs)

KPIs are calculated and stored in a dictionary for each asset:
```python
kpi_store[ticker] = {
    "RSI_14": <latest RSI>,
    "Bollinger": {"MA20": ..., "Upper": ..., "Lower": ...},
    "MACD": {"MACD": ..., "Signal": ...},
    "PE_Ratio": <trailing P/E>,
    "Beta": <5Y monthly Beta>
}
```

These KPIs allow comparison of assets' momentum, volatility, trend, valuation, and risk.

### 3.3 Portfolio Optimization

**Modern Portfolio Theory (MPT):**
- Maximizes portfolio Sharpe ratio with risk-free rate (0.04 by default)
- Generates optimized weights for each asset

**Alternative Portfolio Optimization:**
- Explored with LLM prompts for methods beyond MPT

**Black-Litterman Model:**
- Incorporates investor views (e.g., Microsoft outperforming Google by 5%)
- Calculates implied returns and covariances
- Generates optimized portfolio weights using `EfficientFrontier` from PyPortfolioOpt

Optimized portfolio weights are stored in dictionary format:
```python
weights_dict = { "AAPL": 0.12, "AMZN": 0.15, ... }
```

## 4. Usage Guide

### Step 1: Install Required Libraries
```bash
pip install yfinance matplotlib pandas numpy scipy PyPortfolioOpt langchain-groq
```

### Step 2: Set API Keys
```python
groq_api_key = "YOUR_GROQ_API_KEY"
```

### Step 3: Define Assets and Analysis Period
```python
assets = ["Apple (AAPL)", "Amazon (AMZN)", "Bitcoin (BTC-USD)", ...]
start_year = 2024
end_year = 2025
```

### Step 4: Fetch Historical Data
```python
import yfinance as yf

tickers = [extract_assets(asset) for asset in assets]
data = yf.download(tickers, start='2024-01-01', end='2025-12-31', auto_adjust=True)['Close']
```

### Step 5: Compute KPIs
```python
# Compute RSI, Bollinger Bands, MACD, P/E Ratio, Beta for each asset
# Store in a dictionary `kpi_store`
```

### Step 6: Visualize KPIs

Use the plotting functions provided:
- `plot_rsi(ticker)`
- `plot_bollinger_bands(ticker)`
- `plot_macd(ticker)`

### Step 7: Portfolio Optimization

**Modern Portfolio Theory (MPT):**
```python
# Use `scipy.optimize.minimize` to maximize Sharpe ratio
# Returns weights_dict
```

**Black-Litterman Model:**
```python
# Use PyPortfolioOpt BlackLittermanModel
# Define views and market capitalization
# Optimize portfolio
```

### Step 8: Interpret Results

- KPI visualizations help assess momentum, volatility, trend, and valuation
- Portfolio weights help determine capital allocation across assets

---
