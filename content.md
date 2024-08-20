# tradingcomdados library


## Introduction
*Trading com Dados Library for quantitative finance*

The library consists of a collection of methods that can be used in order to help Data Scientists, Quantitative Analysts and data professionals during the development of quantitative finance applications. One of the main objectives of the library is to provide methods to connect to Trading com dados' data provider services.

## Library Motivation and Description
Trading com dados is an Edtech that provides educational content for people who want to know quantitative finance and in order to obtain that knowlegde, we need quality data, thus this library and our API service was created to solve that.

# How to install
```python 
pip install tradingcomdados
```

# How to use


## Alternative Data
You can obtain alternative data from the Brazilian stock exchange (B3) and major U.S. stock exchanges such as NASDAQ, AMEX, and NYSE using this module. The goal is to facilitate data acquisition from sources like CVM, NASDAQ, B3, and others.

**Features:**
- Updated Brazilian index compositions, such as IBOV, IFIX, IBRA, IDIV, SMLL, and BDRX.
- Updated S&P 500 index composition.
- Economic sector classifications for companies listed on the Brazilian stock exchange and major U.S. stock exchanges.
- Active symbols of equities listed on B3 (stocks and BDRs) or investment funds such as Brazilian real estate investment funds (FII) and investment funds in agro-industrial productive chains (FIAGRO).
- Historical cryptocurrency data from Binance.

**Example Usage:**

```python
from tradingcomdados import alternative_data as ad

# Obtaining the index composition:
ad.index_composition('ibov')
ad.index_composition('sp500')

# Returns the entire DataFrame from B3. You can also pass a list of desired symbols to get their composition:
ad.index_composition('ibov', assets=['RRRP3', 'ABEV3'])
ad.index_composition('sp500', assets=['MMM', 'AAPL'])

# You can use the parameter `mode` to return a list of the index composition symbols:
ad.index_composition('ibov', mode = 'list')
ad.index_composition('sp500', mode = 'list')

# Obtaining economic and sector classifications for companies listed on NASDAQ, NYSE, AMEX, or the Brazilian stock exchange (B3):
ad.get_sectors('B3')
ad.get_sectors('NASDAQ')

# Obtaining sector classification for specific companies listed on B3:
ad.get_sectors(stock_exchange='B3', symbols=['VALE3', 'PETR4'])

# Note: The function supports language options only for B3 data ('pt' for Portuguese; default is 'eng'):
ad.get_sectors(stock_exchange='B3', symbols=['VALE3', 'PETR4'], B3_language='pt')

# Obtaining sector classification for specific companies listed on major U.S. stock exchanges:
ad.get_sectors(stock_exchange='AMEX', symbols=['ZOM', 'AAMC'])
ad.get_sectors(stock_exchange='NASDAQ', symbols=['AAPL', 'META', 'TSLA', 'MSFT'])

# Obtaining a DataFrame of active symbols for a specific asset class listed on the Brazilian stock exchange (B3):
ad.get_symbols('STOCK')
ad.get_symbols('FII')
ad.get_symbols('BDR')

# You can use the parameter `mode` to return a list of symbols. Defaults to 'df' (DataFrame):
ad.get_symbols('BDR', mode='list')

# Retrieving historical cryptocurrency data from Binance: 
ad.get_histdata_binance('BTCUSDT', '5m', '2024-01-01', '2024-03-01')

```


## Funds Data
Fetches data of investment funds from the Brazilian Securities and Exchange Commission (CVM)

**Features:**


**Example Usage:**

```python
from tradingcomdados import funds_data as fd

# Fetching daily data containing information such as quote value, number of investors, and net asset value (NAV)

# You can either leave it empty or specify a CNPJ
fd.get_fund_data()

# When specifying a CNPJ, you have to specify start and end dates, in the YYYY-MM-DD format.
fd.get_fund_data(cnpj = '07.593.972/0001-86', start = '2024-07-01', end = '2024-07-10')


# Fetch the registration data of investment funds
fd.get_funds_info()

# You can either leave it empty or specify a CNPJ
fd.get_funds_info('07.593.972/0001-86')



```

# HUB Features
Using our library, you can access data from Trading com Dados HUB as long as you have a valid API key.
If you are interested about purchasing HUB, contact our team.

## Access to HUB data can be made through data_provider module.
```python
from tradingcomdados import data_provider as dp

# Obtain price information for different types of assets, such as stocks, treasury, indexes, etc.
dp.get_data()

```
### Indexes
For example, in order to obtain daily quotes for brazilian indexes, you must specify the following parameters:

type: 'index'

request_type: 'historical_data_index'

index: desired index. Supported indexes: AGFS, BDRX, GPTW, IBOV, IBRA, IBXL, IBXX, ICO2, ICON, IDIV, IEEX
IFIL, IFIX, IFNC, IGCT, IGCX, IGNM, IMAT, IMOB, INDX, ISEE, ITAG, IVBX, MLCX, SMLL, UTIL

start_date: format yyyy-mm-dd

end_date: format yyyy-mm-dd

api_key: valid api key from Trading com Dados HUB

**An example, for IBOV:**
```python
ibov = dp.get_data('index',
            'historical_data_index',
            'IBOV',
            '2022-01-01',
            '2022-01-10',
            api_key = 'api_key')
```

Other functions
```python
dp.get_data_tickers()

dp.get_data_report()

dp.get_data_report_tickers()

dp.get_data_indicator()

#Get historical data for indicators from API using standard parameters for the chosen ticker.
dp.get_data_indicator_hist()

#Get data from API using standard parameters for the chosen ticker.
dp.get_data_accounting()
```
