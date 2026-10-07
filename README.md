# Stock Market Prediction

A machine learning project that collects historical stock-market data and uses it to analyze and predict stock prices.

The project uses **Python**, **yfinance**, **Pandas**, **NumPy**, **Matplotlib**, and machine-learning techniques to work with historical market data.

> **Disclaimer:** This project is for educational and experimental purposes only. Stock-market predictions are inherently uncertain and should not be considered financial advice.

---

## Features

- Fetch historical stock-market data using `yfinance`
- Select different stocks using their ticker symbols
- Analyze historical price movements
- Clean and preprocess financial data
- Visualize stock prices
- Create features for machine-learning models
- Train a prediction model
- Evaluate model performance
- Generate predicted stock prices

---

## Tech Stack

| Technology | Purpose |
|---|---|
| Python | Core programming language |
| yfinance | Fetch stock-market data |
| Pandas | Data manipulation and analysis |
| NumPy | Numerical computation |
| Matplotlib | Data visualization |
| Scikit-learn | Machine learning |
| Jupyter Notebook | Development and experimentation |

---

## How It Works

The project follows a basic machine-learning pipeline:

```text
        Stock Symbol
             │
             ▼
       Yahoo Finance
             │
             ▼
         yfinance
             │
             ▼
    Historical Stock Data
             │
             ▼
      Data Preprocessing
             │
             ▼
       Feature Creation
             │
             ▼
     Machine Learning Model
             │
             ▼
       Model Evaluation
             │
             ▼
       Price Prediction
```

---

## Data Source

Stock-market data is retrieved using the [`yfinance`](https://github.com/ranaroussi/yfinance) Python library.

Example:

```python
import yfinance as yf

data = yf.download("AAPL", start="2020-01-01", end="2026-01-01")

print(data)
```

The downloaded data can contain:

- Open price
- High price
- Low price
- Closing price
- Adjusted closing price
- Trading volume

---

## Installation

### 1. Clone the repository

```bash
git clone https://github.com/parthib-ui/Stock-prediction.git
```

Move into the project directory:

```bash
cd Stock-prediction
```

### 2. Create a virtual environment

Windows:

```bash
python -m venv venv
```

Activate it:

```bash
venv\Scripts\activate
```

Linux/macOS:

```bash
python3 -m venv venv
source venv/bin/activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

If a `requirements.txt` file has not been created yet, install the main libraries:

```bash
pip install yfinance pandas numpy matplotlib scikit-learn
```

---

## Example Usage

A basic example of downloading stock data:

```python
import yfinance as yf

ticker = "AAPL"

data = yf.download(
    ticker,
    start="2020-01-01",
    end="2026-01-01"
)

print(data.head())
```

---

## Understanding the Stock Data

A typical dataset looks like:

```text
Date        Open    High    Low     Close   Volume
2025-01-02  230.0   234.0   228.0   232.0   45M
2025-01-03  232.0   236.0   231.0   235.0   38M
...
```

### Open

The price at which the stock started trading during the selected period.

### High

The highest price reached during the selected period.

### Low

The lowest price reached during the selected period.

### Close

The price at which the stock ended trading during the selected period.

### Volume

The number of shares traded during the selected period.

---

## Data Preprocessing

Before training a machine-learning model, the raw financial data needs to be prepared.

Typical preprocessing steps include:

1. Removing unnecessary columns
2. Handling missing values
3. Sorting data by date
4. Selecting relevant features
5. Creating additional indicators/features
6. Splitting the dataset into training and testing data

Example:

```python
data = data.dropna()

data = data.sort_index()
```

---

## Feature Engineering

Machine-learning models generally work better when useful features are created from the raw data.

Possible features include:

- Previous day's closing price
- Moving averages
- Daily returns
- Trading volume
- Price difference
- High-low difference
- Rolling statistics

For example:

```python
data["MA20"] = data["Close"].rolling(20).mean()
data["MA50"] = data["Close"].rolling(50).mean()
```

Where:

- `MA20` = 20-day moving average
- `MA50` = 50-day moving average

---

## Machine Learning

The processed data can then be used to train a machine-learning model.

A typical workflow is:

```text
Historical Data
       ↓
Feature Engineering
       ↓
Train/Test Split
       ↓
Model Training
       ↓
Prediction
       ↓
Evaluation
```

Depending on the implementation, possible models include:

- Linear Regression
- Random Forest
- Decision Tree
- Support Vector Regression
- XGBoost
- LSTM / Neural Networks

---

## Model Evaluation

The model should be evaluated using data that it has not seen during training.

Common regression metrics include:

### Mean Absolute Error

```text
MAE = average(|actual - predicted|)
```

Lower MAE generally indicates better performance.

### Mean Squared Error

```text
MSE = average((actual - predicted)²)
```

### Root Mean Squared Error

```text
RMSE = √MSE
```

RMSE gives more weight to larger prediction errors.

---

## Visualization

The project can visualize historical and predicted prices using Matplotlib.

Example:

```python
import matplotlib.pyplot as plt

plt.figure(figsize=(12, 6))

plt.plot(data["Close"], label="Actual Price")

plt.xlabel("Date")
plt.ylabel("Price")
plt.title("Stock Price")

plt.legend()
plt.show()
```

A prediction graph can be used to compare:

```text
Actual Price
     vs
Predicted Price
```

---

## Project Structure

A possible project structure is:

```text
Stock-prediction/
│
├── data/
│   └── stock_data.csv
│
├── notebooks/
│   └── stock_prediction.ipynb
│
├── src/
│   ├── data_collection.py
│   ├── preprocessing.py
│   ├── features.py
│   ├── model.py
│   └── prediction.py
│
├── requirements.txt
├── README.md
└── .gitignore
```

The exact structure may change as the project develops.

---

## Example Stock Symbols

You can change the ticker symbol depending on the market and company.

### US Stocks

```text
AAPL  - Apple
MSFT  - Microsoft
GOOGL - Alphabet
AMZN  - Amazon
TSLA  - Tesla
NVDA  - NVIDIA
```

### Indian Stocks

Yahoo Finance generally uses `.NS` for many stocks listed on NSE.

Examples:

```text
RELIANCE.NS
TCS.NS
INFY.NS
HDFCBANK.NS
SBIN.NS
ICICIBANK.NS
```

Example:

```python
data = yf.download("RELIANCE.NS", period="5y")
```

---

## Historical vs Real-Time Data

This project primarily uses **historical market data** for machine-learning training.

For example:

```python
yf.download("AAPL", period="5y")
```

downloads historical data.

`yfinance` also provides WebSocket functionality for streaming market data, but downloading historical data and receiving a continuous real-time stream are different use cases.

For a machine-learning prediction project, historical data is generally the starting point.

---

## Limitations

Stock prediction is a difficult machine-learning problem.

The model cannot reliably predict the future simply because it performs well on historical data.

Stock prices are affected by many factors, including:

- Company announcements
- Earnings reports
- Economic conditions
- Interest rates
- Inflation
- Government policies
- Global events
- Investor sentiment
- Market psychology
- Unexpected news

Historical price patterns alone cannot capture all of these factors.

Another major risk is **overfitting**, where a model performs well on historical data but performs poorly on unseen data.

---

## Future Improvements

Possible improvements for this project include:

- Add more technical indicators
- Add multiple stocks
- Compare different ML algorithms
- Implement LSTM neural networks
- Add hyperparameter tuning
- Build a Streamlit dashboard
- Add interactive stock charts
- Add real-time market-data streaming
- Add news sentiment analysis
- Combine technical and fundamental indicators
- Compare predicted vs actual prices
- Deploy the application as a web service

---

## Learning Objectives

This project is intended to provide practical experience with:

- Python
- Data collection
- Financial datasets
- Pandas
- NumPy
- Data visualization
- Feature engineering
- Machine learning
- Regression
- Model evaluation
- Time-series data
- Git and GitHub

---

## Disclaimer

This project is **not financial advice**.

Predictions generated by machine-learning models can be inaccurate and should not be used as the sole basis for investment or trading decisions.

The project is intended for **educational and research purposes only**.

---

## Author

**Parthib Ghosh**

GitHub: [@Subhayu004](https://github.com/parthib-ui)

---

## License

This project is intended for educational purposes.

If you decide to publish it under a specific open-source license, add the corresponding `LICENSE` file to the repository.
