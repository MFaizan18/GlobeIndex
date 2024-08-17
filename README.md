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

**7.2) Fetching Exchange Rate Data**

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
The script then moves on to handle currency exchange rates for indices that are not traded in USD, a crucial step for standardizing all data into a common currency (USD). The historical exchange rate data is stored in a dictionary called `exchange_rates`.

To ensure comprehensive coverage, the period for fetching this data is set to 2200 days. Although the script is configured to use a maximum of 2000 days of index data, this extra buffer of 200 days ensures that we have enough exchange rate data, even if some dates are missing or incomplete. In cases where data is missing for certain days, the script later uses a method called ffill (forward fill) to carry forward the most recent available exchange rate, ensuring that there are no gaps in the data. This approach guarantees accurate and consistent conversion of all indices into USD, which is essential for reliable global financial analysis.

**7.3) Converting Non-USD Prices to USD**

```python
# Convert non-USD prices to USD
    USD_Convdata = {}
    for index, currency in indices.items():
        if currency != 'USD':
            exchange_rate = exchange_rates[currency]
            # Ensure the index of exchange_rate is in datetime.date format
            exchange_rate.index = pd.to_datetime(exchange_rate.index).date
            # Forward-fill missing exchange rates
            exchange_rate = exchange_rate.ffill()
            converted_data = adj_close_data[index].copy()
            for date in converted_data.index:
                date_only = date.date()
                if date_only in exchange_rate.index:
                    rate = exchange_rate.loc[date_only]
                    converted_data.loc[date] /= rate
                else:
                    print(f"No exchange rate data for {currency} on {date_only}, using the most recent available rate.")
                    # Use the most recent available rate
                    rate = exchange_rate.loc[:date_only].iloc[-1]
                    converted_data.loc[date] /= rate
            USD_Convdata[index] = converted_data
        else:
            USD_Convdata[index] = adj_close_data[index]
```
Continuing from the previous explanation, the script next handles the crucial task of converting all non-USD denominated indices into USD. This step ensures that all financial data is standardized, allowing for accurate comparison across global indices.

The script creates a new dictionary, `USD_Convdata`, to store the converted index data. For each index that is not already in USD, the corresponding exchange rate data is retrieved from the exchange_rates dictionary. The script then makes sure the exchange rate dates are correctly formatted and uses forward-filling (`ffill`) to fill in any missing exchange rates, ensuring there are no gaps in the data.

The conversion process involves iterating over each date in the adjusted close prices for the index. For each date, the script checks if there is a corresponding exchange rate available. If the exchange rate is present, the index price is divided by this rate to convert it into USD. If the exchange rate for a particular date is missing, the script uses the most recent available rate, ensuring that the conversion process is robust even in the face of incomplete data.

Finally, the converted data is stored in the USD_Convdata dictionary. For indices already in USD, the data is directly copied over without conversion. This comprehensive conversion process ensures that all index data is consistently expressed in USD, enabling reliable and meaningful global financial analysis.

## 8) Normalization

Next, the script proceeds to normalize the data using robust statistical methods. It calculates the median and interquartile range (IQR) for each index and then applies robust scaling to ensure that the data is standardized, making it less sensitive to outliers

```python
# Calculate median and IQR for each index
    medians_iqrs = {}
    for index, data in USD_Convdata.items():
        median = data.median()
        q1 = data.quantile(0.25)
        q3 = data.quantile(0.75)
        iqr = q3 - q1
        medians_iqrs[index] = (median, iqr)

    # Apply robust scaling
    scaled_data = {}
    for index, data in USD_Convdata.items():
        median, iqr = medians_iqrs[index]
        scaled_data[index] = (data - median) / iqr
```
In this section, the script performs statistical analysis and scaling on the USD-converted index data to normalize it and prepare it for further analysis. First, it calculates the median and the Interquartile Range (IQR) for each index. The median represents the central tendency of the data, while the IQR, calculated as the difference between the first quartile (Q1) and the third quartile (Q3), measures the spread of the middle 50% of the data. These values are stored in the `medians_iqrs` dictionary for each index.

Next, the script applies robust scaling to the data. Robust scaling is particularly useful when dealing with data that contains outliers, as it uses the median and IQR rather than the mean and standard deviation, making it less sensitive to extreme values. For each index, the script subtracts the median from each data point and then divides the result by the IQR. The scaled data is stored in the scaled_data dictionary. This process standardizes the data, ensuring that all indices are on a comparable scale, which is crucial for subsequent analysis and visualization.

## 9) Setting up the Timezone

To ensure consistency across all indices, the script converts the timestamps of the scaled data to a common timezone. Financial data from different markets often comes with timestamps in various local timezones, which can lead to discrepancies when analyzing or comparing the data.

```python
def convert_timezone(data, to_timezone='America/New_York'):
    try:
        data.index = data.index.tz_localize('UTC').tz_convert(to_timezone)
    except TypeError:
        data.index = data.index.tz_convert(to_timezone)
    return data

# Converting to a common timezone 
for index in scaled_data:
    scaled_data[index] = convert_timezone(scaled_data[index])

```
The script defines a function, convert_timezone, which standardizes the timezone of the data to `America/New_York` (Eastern Time). This function first attempts to localize the index to UTC if it is not already timezone-aware, and then converts it to the specified target timezone. If the data is already timezone-aware, the function directly converts it to the desired timezone without re-localizing it. This conversion is applied to all indices in the scaled_data dictionary, ensuring that all data points are aligned to the same timezone. This step is critical for accurate temporal analysis and comparison across different global indices.

## 10) Combined Dataset

In this step, the script combines the scaled and timezone-aligned data from all indices into a single, unified dataset. This combined dataset is crucial for performing further analysis or visualizations on the aggregated data.

```python
def create_combined_dataset(adj_close_data, interval):
    # Create a unified time range across all dates
    all_dates = pd.date_range(
        start=min(min(data.index.date) for data in adj_close_data.values()),
        end=max(max(data.index.date) for data in adj_close_data.values()),
        freq='B'
    )

    if interval in ['1d', '5d']:
        # Create a DataFrame for all dates
        combined_data = pd.DataFrame(index=all_dates)

        # For each index, align and fill the data
        for idx, data in adj_close_data.items():
            data = data.reset_index()

            # Handle different cases of index column names
            date_col = 'Date' if 'Date' in data.columns else data.columns[0]
            data[date_col] = pd.to_datetime(data[date_col]).dt.date  # Ensure 'Date' is datetime
            data.set_index(date_col, inplace=True)

            daily_data = data.reindex(combined_data.index, fill_value=float('nan'))
            combined_data[idx] = daily_data['Adj Close']  # Adding Adjusted Close prices

        combined_data.index = pd.to_datetime(combined_data.index)
        combined_data.index.name = 'Datetime'
    else:
        # Create a MultiIndex DataFrame for all dates and times
        time_range = pd.date_range(start='00:00', end='23:59', freq=interval).time
        index = pd.MultiIndex.from_product([all_dates, time_range], names=['Date', 'Time'])
        combined_data = pd.DataFrame(index=index)

        # For each index, align and fill the data
        for idx, data in adj_close_data.items():
            data = data.reset_index()

            # Handle different cases of index column names
            datetime_col = 'Datetime' if 'Datetime' in data.columns else data.columns[0]
            data['Date'] = pd.to_datetime(data[datetime_col]).dt.date  # Extract the date
            data['Time'] = pd.to_datetime(data[datetime_col]).dt.floor(interval).dt.time  # Align to specified intervals

            data.set_index(['Date', 'Time'], inplace=True)

            daily_data = data.reindex(combined_data.index, fill_value=float('nan'))
            combined_data[idx] = daily_data['Adj Close']  # Adding Adjusted Close prices

        combined_data.index = combined_data.index.to_frame().apply(lambda row: pd.Timestamp.combine(row['Date'], row['Time']), axis=1)
        combined_data.index = combined_data.index.tz_localize('America/New_York')
        combined_data.index.name = 'Datetime'

    # Remove rows with all NaN values
    combined_data.dropna(how='all', inplace=True)
    
    return combined_data

# Combine the scaled data into a single dataset
combined_data = create_combined_dataset(scaled_data, interval_converted)
```
The `reate_combined_dataset` function is designed to handle this task by first creating a unified time range that spans the entire period covered by the data. The time range is based on business days ('B' frequency) to align with typical market trading days.

The function then checks the interval to determine how to structure the combined dataset:

**10.1) For Daily or Longer Intervals ('1d', '5d'):**

The function creates a DataFrame indexed by all the business days in the unified time range. For each index, the data is realigned to this common timeline. Missing dates are filled with NaN to ensure that each index aligns correctly with the unified time frame. The adjusted close prices are then added to this combined DataFrame.

**10.2) For Shorter Intervals (e.g., Minute Intervals):**

The function creates a MultiIndex DataFrame that includes both dates and specific times of the day. This setup accommodates more granular data. Each index’s data is then aligned to both the date and time, filling any gaps with NaN values. The combined dataset is then indexed by timestamps localized to the `America/New_York` timezone.

Finally, the function removes any rows that are entirely NaN (indicating no available data for any index at those times), ensuring that the final combined dataset is clean and ready for analysis. This combined dataset, stored in the combined_data variable, is the foundation for all subsequent analysis, providing a comprehensive and consistent view of all the indices over time.

## 11) Calculating the Global Index

After combining and scaling the data, the script proceeds to calculate a global index that represents the aggregated performance of all the indices in the dataset. This global index is a weighted average of the individual indices, where each index's influence is determined by its predefined weight, based on the market capitalization of each index. The dictionary containing these weights, which reflect the relative market cap of each index, has already been explained earlier.

``` python
def calculate_global_index(combined_data, weights):
    # Explicitly specify dtype to avoid the warning
    global_index = pd.Series(index=combined_data.index, dtype='float64')
    
    for timestamp in combined_data.index:
        weighted_sum = 0
        weight_sum = 0
        for index, weight in weights.items():
            if index in combined_data.columns and not pd.isna(combined_data.loc[timestamp, index]):
                weighted_sum += combined_data.loc[timestamp, index] * weight
                weight_sum += weight
        
        if weight_sum != 0:
            global_index[timestamp] = weighted_sum / weight_sum
        else:
            global_index[timestamp] = None
    
    # Drop any rows where the global index is NaN
    global_index.dropna(inplace=True)
    
    return global_index

# Call the function to calculate the global index
global_index = calculate_global_index(combined_data, weights)
```

The calculate_global_index function performs this task by first creating an empty global_index series, explicitly set to a `float64` data type to ensure numerical precision. The function then iterates over each timestamp in the combined dataset. For each timestamp, it calculates a weighted sum of the adjusted close prices for all indices that have data available at that specific time.

The weighted sum is computed by multiplying each index's adjusted close price by its corresponding weight, reflecting its market cap significance. The function also tracks the sum of weights to ensure proper averaging. If the sum of weights is non-zero (indicating that valid data was available for at least one index), the global index value for that timestamp is calculated as the weighted average. If no valid data is available for that timestamp, the global index value is set to None.

Finally, the function removes any timestamps where the global index value is NaN, ensuring that the resulting global index series is clean and ready for analysis. This global index, stored in the `global_index variable`, represents the overall performance of the combined indices, weighted according to their significance in the global financial landscape, as determined by their market capitalizations.

## 12)  Adjusting and Smoothing the Global Index

Once the global index is calculated, the script performs additional steps to prepare the data for further analysis or visualization. This involves ensuring that all values in the global index are positive and then applying smoothing to reduce noise and highlight trends.

```python
# Determine the minimum value in the global index
min_value = global_index.min()

# Apply a positive offset to ensure all values are positive
offset = abs(min_value) + 1  # Adding 1 to ensure the smallest value is slightly positive
adjusted_global_index = global_index + offset

# Apply Exponential Moving Average (EMA) for smoothing
smoothed_global_index = adjusted_global_index.ewm(span=ema_span, adjust=False).mean()

# Convert smoothed data back to a pandas Series with the same index
smoothed_global_index = pd.Series(smoothed_global_index, index=adjusted_global_index.index)
```
Since we applied robust scaling using the median and interquartile range (IQR), it's expected that the global index might include negative values. To address this, the script adds a positive offset, calculated as the absolute value of the minimum index value plus 1. This ensures that all values in the `adjusted_global_index` are positive without altering their relative dependencies.

Once the offset is applied, the script smooths the global index using an Exponential Moving Average (EMA). This smoothing reduces noise and highlights longer-term trends. Finally, the smoothed data is converted back into a pandas Series with the same index as the adjusted global index, resulting in a `smoothed_global_index` that is ready for further analysis or visualization

## 13) Benchmarking and Rescaling the Global Index

To finalize the global index, the script benchmarks and rescales it to ensure that its values resemble those of a real-world financial index. This is crucial because, after scaling and smoothing, the values of the index might be abstract and not directly comparable to actual market indices.

```python
# Choose a Benchmark
benchmark_index = 'ACWI'

# Calculate the Average Value of Your Smoothed Global Index
reference_period_start = smoothed_global_index.index.min()
reference_period_end = smoothed_global_index.index.max()
global_index_avg = smoothed_global_index.loc[reference_period_start:reference_period_end].mean()

# Calculate the Average Value of the Benchmark Index
benchmark_data = adj_close_data[benchmark_index]
benchmark_avg = benchmark_data.loc[reference_period_start:reference_period_end].mean()

# Determine the Scaling Factor
scaling_factor = benchmark_avg / global_index_avg

# Apply the Scaling Factor to Rescale Your Smoothed Global Index
scaled_smoothed_global_index = smoothed_global_index * scaling_factor
```

The script starts by selecting a benchmark index, in this case, the ACWI (All Country World Index). The ACWI is an ETF that represents a broad global market exposure, making it an ideal reference for rescaling the global index to resemble a realistic financial index.

The script then calculates the average value of the smoothed global index over its entire period, as well as the average value of the ACWI benchmark index over the same period. By comparing these two averages, the script determines a scaling factor.

This scaling factor is then applied to the smoothed global index to rescale it, ensuring that its values are expressed in points, similar to actual market indices. Without this step, the global index values would not resemble the price levels typically associated with financial indices, making them less intuitive and practical for real-world analysis.

## 14) visualization

To visualize the final global index, the script plots a graph showing how the index has evolved over time. This plot provides a clear and intuitive view of the global market trends captured by the index.

```python
To visualize the final global index, the script plots a graph showing how the index has evolved over time. This # Plotting
plt.figure(figsize=(14, 8))
plt.title(f'Global Market Overview ({period}, Interval: {interval}, EMA: {ema_span})', fontsize=16)
plt.xlabel('Date', fontsize=14)
plt.ylabel('Global Index Value', fontsize=14)

plt.plot(scaled_smoothed_global_index.index, scaled_smoothed_global_index, label='Global Index', color='blue', linewidth=0.8)

plt.legend(loc='upper left', fontsize=12)
locator = mdates.AutoDateLocator(minticks=10, maxticks=20)
formatter = mdates.ConciseDateFormatter(locator)
plt.gca().xaxis.set_major_locator(locator)
plt.gca().xaxis.set_major_formatter(formatter)
plt.xticks(rotation=45)
plt.grid(True, which='both', linestyle='--', linewidth=0.5)
plt.tight_layout()
plt.show()
plot provides a clear and intuitive view of the global market trends captured by the index.
```
To demonstrate the effectiveness of the global index calculation and visualization, I’ve included three screenshots that show the results for different periods and intervals:

**14.1) Period = '60d', Interval = '30m':**

This screenshot captures the global index over a short-term period of 60 days with 30-minute intervals, providing a detailed view of intraday market movements.




























