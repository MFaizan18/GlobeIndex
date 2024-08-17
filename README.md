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
**6.2) Define Indices and Their Respective Currencies**

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
**6.3) Define Weights for Each Index**

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

## 7) Data Acquisition
**7.1) Fetching Adj Close Data**

This part of the code uses the `yfinance` library to fetch historical data for each index defined in the indices dictionary. The data is then stored in the `adj_close_data` dictionary for further processing.
```python
adj_close_data = {}

for index, timezone in indices.items():
    data = yf.download(index, period=period, interval=interval)
    data.dropna(how="any", inplace=True)
    
    if data.empty:
        print(f"No data for {index}")
        continue
    adj_close_data[index] = data['Adj Close']
```
The `period` and `interval` for fetching the data are obtained from user input, as shown in the code below.

```python
allowed_intervals = ['5m', '15m', '30m', '60m', '1d', '5d']
    interval_mapping = {
        '5m': ('5T', 50),
        '15m': ('15T', 25),
        '30m': ('30T', 25),
        '60m': ('60T', 20),
        '1d': ('1D', 15),
        '5d': ('5D', 10),
    }
    
    while True:
        interval = input(f"Enter the interval {allowed_intervals}: ")
        if interval not in allowed_intervals:
            print("Invalid interval. Please select from the allowed intervals.")
            continue
        
        period = input("Enter the period in days (e.g., '7d', '365d', '40d'): ")
        if not period.endswith('d') or not period[:-1].isdigit():
            print("Invalid period format. Please enter the period in days (e.g., '7d').")
            continue
        
        days = int(period.replace('d', ''))
        if days > 2000:
            print("The maximum number of days allowed is 2000. Please enter a valid period.")
            continue
```
The script prompts the user to enter a time interval and a period for fetching the data. The allowed intervals are `['5m', '15m', '30m', '60m', '1d', '5d']` representing different time frames (e.g., 5 minutes, 15 minutes, 1 day, etc.)

The user is also asked to input the period, which defines how many days of historical data to retrieve (e.g., '7d' for 7 days). The script checks that the period is in the correct format and doesn't exceed 2000 days.

The script is configured with a maximum period of 2000 days, which is more than 5 years of data. However, it's important to note that for shorter intervals (like minutes), data availability is limited to a much shorter period—in this case, typically up to 60 days. These limitations apply specifically to minute-based intervals. For daily intervals, data can be retrieved for several years without issue. For more detailed information on these limitations, you can refer to the Yahoo Finance page.

The `interval_mapping` dictionary is a key part of the script that defines how different time intervals are handled. Each entry in the dictionary maps a user-selected interval (like '5m' for 5 minutes) to a tuple containing two important elements:

Frequency Code (e.g., '5T', '1D'):

The first element in each tuple is a frequency code that is used for time-based operations within the script.
The code is designed to be compatible with the pandas library's time-related functions, particularly when generating a range of times using `pd.date_range()`.

For example:
`5T` corresponds to a 5-minute frequency.
`1D` corresponds to a 1-day frequency.

This frequency code is used later in the script to create a time range that matches the selected interval, allowing the data to be properly aligned and processed according to the user's selection.

Smoothing Factor (e.g., 50, 25):

The second element in each tuple is a smoothing factor, which is used in calculations like the Exponential Moving Average (EMA).
The smoothing factor controls the sensitivity of the EMA to changes in data. A higher value results in more smoothing, meaning that the EMA will react more slowly to recent changes in data, while a lower value makes the EMA more responsive.

In this context:
For the `5m` interval, the smoothing factor is 50.
For the `1d` interval, the smoothing factor is 15.

This factor is later applied in the script when calculating the EMA to smooth out the data and highlight trends over the selected interval.

**7.1) Fetching Exchange Rate Data**

In this section of the code, we handle the currency exchange rates for indices that are traded in currencies other than USD. Since our goal is to create a global index that can be compared on a common basis, it is essential to account for these exchange rates. The exchange rates are stored in the `exchange_rates` dictionary.

```python
exchange_rates = {}

for index, currency in indices.items():
    if currency != 'USD':
        exchange_rate_data = yf.download(f'{currency}=X', period='2200d', interval='1d')
        
        if exchange_rate_data.empty:
            print(f"No data for {index}")
            continue
        exchange_rates[currency] = exchange_rate_data['Adj Close']
```















