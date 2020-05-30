# ETL Project - U.S. Historical Stock Prices Data

![sql.png](stock.jpg)

## Project Overview 
Identify a dataset and perform ETL on the data

## Team Members

* [Catie Clark](https://github.com/csidneyclark)
* [Jacob Clifton](https://github.com/cliftjc1)
* [Masita Mohamad](https://github.com/masitamohamad)

## Project Methodology 
### Step 1: **Extract**

1. Identify data sources
2. Read the data 
3. Identify rows, columns, and fields to be extracted from the sources

* [Kaggle](https://www.kaggle.com/tsaustin/us-historical-stock-prices-with-earnings-data/data)

Input files:
1. dividends_latest.csv
2. earnings_latest.csv
3. stock_prices_latest.csv

### Step 2: **Transform**

Cleansing and aggregation to prepare data for analysis
* Grouped by date and symbol
* Created new column for year only
* Dropped null values
* Aggregate Statistics: Calculated minimum low, maximum high, and average differential of stock prices

### Step 3: **Load**

Write the data into a SQL database for storage
SQLAlchemy
* Created combined symbol/year column to use as primary key for each table
* Created classes: Dividends, Earnings, Prices
* Defined columns within each class corresponding to previous dataframes
* Established database connection using create_engine function
* Pushed the tables and queried server using a Session object

Output file:
1. stonks.sqlite

#### Modules Required

pandas==0.25.1
SQLAlchemy==1.3.9
