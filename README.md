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
<em>Extract data from data sources</em>

* Identify data sources: [Kaggle](https://www.kaggle.com/tsaustin/us-historical-stock-prices-with-earnings-data/data)
* Read the data using Pandas
* Identify rows, columns, and fields to be extracted from the sources

Input files:
1. **dividends_latest.csv**: Dividend data for each stock with dividend date
2. **earnings_latest.csv**: Earnings data for each stock with date and estimated & reported EPS
3. **stock_prices_latest.csv**: Daily stock price data 
---
### Step 2: **Transform**

<em>Clean and aggregate to prepare data for analysis</em>
* Created new column for year only using datetime module

```python
# Example:
dividends_df['date'] = pd.to_datetime(dividends_df['date'])
dividends_df['year'] = pd.DatetimeIndex(dividends_df['date']).year
```

* Dropped null values
* Grouped by date and symbol
* Aggregate Statistics: Calculated minimum low, maximum high, and average differential of stock prices

```python
# Example:
g_prices_df = prices_df.groupby(['symbol', 'year']).agg({'low':'min','high':'max','differential':'mean'})
```

#### Dependencies
* Pandas
  * Dataframe functions
* Datetime
  * Date formatting
---
### Step 3: **Load**

<em>Write the data into a SQL database for storage using SQLAlchemy</em>
* Created combined symbol/year column to use as primary key for each table

```python
# Example:
_dividends_df['symbol_year'] = g_dividends_df['symbol'].astype(str) + g_dividends_df['year'].astype(str)
```

* Created classes: Dividends, Earnings, Prices
* Defined columns within each class corresponding to previous dataframes

```python
# Example:
class Dividends(Base):
    __tablename__ = 'dividends'
    symbol_year = Column(String(20),primary_key=True)
    symbol = Column(String(10))
    year = Column(String(4))
    dividend_mean = Column(Integer)
    dividend_min = Column(Integer)
    dividend_max = Column(Integer)
    dividend_sum = Column(Integer)
```

* Established database connection using create_engine function
```python
# Example:
engine = create_engine("sqlite:///stonks.sqlite")
conn = engine.connect()
```

* Pushed the tables and queried server using a Session object
```python
# Example:
from sqlalchemy.orm import Session
session = Session(bind=engine)
g_dividends_df.to_sql("dividends",engine,if_exists='replace')
```

#### Dependencies
* SQLAlchemy

#### Output file:
1. stonks.sqlite
