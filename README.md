# GlobeIndex

Welcome to the Global Index project! This tool is designed to provide a comprehensive overview of global financial markets by aggregating and analyzing data from various stock indices around the world.

## 1) What exactly is Globe Index?
Globe Index is a sophisticated market analysis tool that fetches historical data from a wide range of global indices and calculates a weighted global index. By applying advanced scaling and smoothing techniques, Globe Index delivers a clear and accurate representation of global market trends.

## 2) Key Features

**2.1) Global Coverage:** Includes data from major indices across the USA, Europe, Asia, and other regions, ensuring a truly global perspective.

**2.2) Unified Currency Reference:** Uses USD as the reference point for currency conversion, ensuring a consistent and comparable view of global markets.

**2.3) Timezone Adjustments:** Adjusts all data to a common timezone, providing a unified timeline for analysis.

**2.4) Customizable Data Intervals:** Supports various data intervals including 5 minutes, 15 minutes, 30 minutes, 60 minutes, daily, and 5-day intervals, allowing for flexible analysis.

**2.5) Robust Data Processing:** Applies median and interquartile range (IQR) scaling to normalize data, ensuring that outliers do not skew the analysis.

**2.6) Interactive Visualization:** Visualizes the scaled and smoothed global index with customizable date ranges and intervals, providing an intuitive and interactive experience.

## 3) Why Use Globe Index?
Globe Index is designed for anyone who needs a comprehensive view of global financial markets. Whether you're tracking market performance, conducting financial research, or making investment decisions, Globe Index provides the tools and insights you need to stay informed.

## 4) Indices Included
Globe Index includes data from a variety of global indices such as:

**4.1) USA:** S&P 500 (^GSPC, ^SPX), NASDAQ Composite (^IXIC), Dow Jones Industrial Average (^DJI), iShares MSCI Emerging Markets ETF (EEM), iShares MSCI ACWI ETF (ACWI), iShares 7-10 Year Treasury Bond ETF (IEF), iShares 20+ Year Treasury Bond ETF (TLT)

**4.2) Europe:** DAX Performance Index (^GDAXI, Germany), CAC 40 Index (^FCHI, France), EURO STOXX 50 Index (^STOXX50E)

**4.3) Asia:** Shanghai Composite Index (000001.SS, China), Hang Seng Index (^HSI, Hong Kong), S&P/ASX 200 Index (^AXJO, Australia), S&P NSE Sensex Index (^NSEI, India), Nikkei 225 Index (^N225, Japan)

**4.4) Other Regions:** S&P/TSX Composite Index (^GSPTSE, Canada), FTSE 100 Index (^FTSE, UK), Swiss Market Index (^SSMI, Switzerland), Singapore Exchange (S68.SI, Singapore Dollar)

**4.5) Commodities:** Invesco DB Commodity Tracking ETF (DBC, USA)

The indices above cover most of the main markets in the world, and we continually add more to the list to ensure comprehensive global coverage.

## 5) How to Run the Project
Follow these steps to run the project:

**5.1) Clone the Repository**
Clone the repository to your local machine using the following command:
```bash
git clone https://github.com/MFaizan18/globe-index.git
```
**5.2) Navigate to the Project Directory**
```bash 
cd globe-index
```
**5.3) Install the Required Packages**
```bash 
pip install -r requirements.txt
```
**5.4) Run the Script**
```bash
python main.py
```
## 6) Detailed Code Breakdown
**6.1)** Let's start by importimg the necessary libraries
```python
import yfinance as yf
import pandas as pd
import matplotlib.pyplot as plt
import matplotlib.dates as mdates
```
**6.2)** Define Indices and Their Respective Currencies
The `indices` dictionary defines various global financial indices and their respective trading currencies. This setup allows the program to fetch and process data for these indices accurately. Here is the dictionary:
```python
indices = {
    '^GSPC': 'USD',   # S&P 500 (USA)
    '^SPX': 'USD',    # S&P 500 (USA)
    '^IXIC': 'USD',   # NASDAQ Composite (USA)
    '^DJI': 'USD',    # Dow Jones Industrial Average (USA)
    'EEM': 'USD',     # iShares MSCI Emerging Markets ETF (USA)
    'ACWI': 'USD',    # iShares MSCI ACWI ETF (USA)
    'IEF': 'USD',     # iShares 7-10 Year Treasury Bond ETF (USA)
    'TLT': 'USD',     # iShares 20+ Year Treasury Bond ETF (USA)
    '^GDAXI': 'EUR',  # DAX Performance Index (Germany)
    '^FCHI': 'EUR',   # CAC 40 Index (France)
    '000001.SS': 'CNY',  # Shanghai Composite Index (China)
    '^HSI': 'HKD',    # Hang Seng Index (Hong Kong)
    '^AXJO': 'AUD',   # S&P/ASX 200 Index (Australia)
    '^NSEI': 'INR',   # S&P NSE Sensex Index (India)
    '^GSPTSE': 'CAD',  # S&P/TSX Composite Index (Canada)
    '^STOXX50E': 'EUR', # EURO STOXX 50 Index (Europe)
    'DX-Y.NYB': 'USD', # US Dollar Index (USA)
    'DBC': 'USD',      # Invesco DB Commodity Tracking ETF (USA)
    '^FTSE': 'GBP',    # FTSE 100 Index (UK)
    '^N225': 'JPY',    # Nikkei 225 Index (Japan)
    '^SSMI': 'CHF',    # Swiss Market Index (Switzerland)
    'S68.SI': 'SGD',   # Singapore Exchange (Singapore Dollar)
}
```
**6.3)** Define Weights for Each Index
The `weights` dictionary assigns a specific weight to each index. These weights are used to calculate a weighted global index, ensuring that more significant indices have a proportionally larger impact on the overall index. Here is the dictionary:
```python
weights = {
    '^GSPC': 0.2849341505160153,
    '^SPX': 0.2849341505160153,
    '^IXIC': 0.13904406766236627,
    '^DJI': 0.06733580635221512,
    'EEM': 0.00013660798561437334,
    'ACWI': 0.00012873756669008846,
    'IEF': 5.5655105250300244e-05,
    'TLT': 7.770477096674917e-05,
    '^GDAXI': 0.009494473622946843,
    '^FCHI': 0.0162405469866196,
    '000001.SS': 0.04434918600192275,
    '^HSI': 0.016865183409181892,
    '^AXJO': 0.00974432819197176,
    '^NSEI': 0.019988365521993356,
    '^GSPTSE': 0.015615910564057308,
    '^STOXX50E': 0.029982548282990032,
    'DBC': 1.4366637718932724e-05,
    '^FTSE': 0.021862274789680232,
    '^N225': 0.02685936617017857,
    '^SSMI': 0.011868092028683554,
    'S68.SI': 0.00046847731692171925
}
```
These weights are determined based on the relative importance and market capitalization of each index, ensuring a balanced and representative global index.
## Data Acquisition











