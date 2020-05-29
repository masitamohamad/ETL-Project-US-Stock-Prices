# ETL Project - U.S. Historical Stock Prices Data

![sql.png](stock.jpg)

## Project Overview 
Identify a dataset and perform ETL on the data

## Team Members

* Catie Clark
* Jacob Clifton
* Masita Mohamad

## Step 1: **Extract**

Identify data sources and rows, columns, and fields to be extracted from those sources
* Kaggle link: https://www.kaggle.com/tsaustin/us-historical-stock-prices-with-earnings-data/data

Raw Data
1. dividends_latest.csv
2. earnings_latest.csv
3. stock_prices_latest.csv

## Step 2: **Transform**
Cleansing and aggregation to prepare data for analysis
* Grouped by date and symbol
* Created new column for year only
* Dropped null values
* Aggregate Statistics: Calculated minimum low, maximum high, and average differential of stock prices

## Step 3: **Load**
SQLAlchemy
Created combined symbol/year column to use as primary key