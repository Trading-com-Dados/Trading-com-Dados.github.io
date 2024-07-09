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
## Machine Learning
This library has a few machine learning models that you can use in your daily activities, both supervised and unsupervised.

```python
from tradingcomdados import unsupervised_learning as ul

ul.clustering_pipeline()
```

## Alternative Data
You can obtain alternative data from the Brazilian stock exchange (B3) and Nasdaq using this module. Here, our goal is to facilitate data acquisition from sources such as CVM and others.

Examples:
* Updated composition of indexes, such as IBOV, IFIX but also S&P 500
* Economy sectors of companies listed in the Brazilian stock exchange


```python
from tradingcomdados import alternative_data as ad

# General function
ad.index_composition()

# Obtaining composition of IBOV
ad.index_composition('ibov')

# Obtaining sectors of Brazilian companies listed on B3
ad.get_sectors('B3')

# Obtaing sectors of companies listed on NASDAQ
ad.get_sectors('NASDAQ')

# Obtaining sector classification of a particular company listed on B3
ad.get_sectors('B3','PETR3') 

# Obtaining sector classification of a particular company listed on NASDAQ
ad.get_sectors('NASDAQ', 'AAPL')

# Obtaining multiple companies sector classification
ad.get_sectors('NASDAQ', 'AAPL','META')
ad.get_sectors('B3', 'VALE3', 'MGLU3', 'PETR4')

```


## Funds Data
Fetches data of investment funds from the Brazilian Securities and Exchange Commission (CVM)


```python
from tradingcomdados import funds_data as fd

# Fetching daily data containing information such as quote value, number of investors, and net asset value (NAV)
# You have to specify start and end dates, in the YYYY-MM-DD format.
fd.get_funds_data(start = '2024-01-01', end = '2024-02-01')

# You can either leave it empty or specify a CNPJ
fd.get_funds_data('07.593.972/0001-86', start = '2024-01-01', end = '2024-02-01')


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
