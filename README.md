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








