---
header:
  overlay_image: /assets/images/covid/miguel.jpg
  caption: "Photo credit: [**miguel-Ã¡-padriÃ**](https://pexels.com)"
permalink: /portfolio/Covid_19/
date: 2020-05-25
toc: true
toc_label: "Contents"
---

# 2019 Corona Virus Exploratory Data Analysis

## Data Source
>Max Roser, Hannah Ritchie, Esteban Ortiz-Ospina and Joe Hasell (2020) - "Coronavirus Disease (COVID-19) – Statistics and Research". Published [online](https://ourworldindata.org/coronavirus) at OurWorldInData.org.




```python
from IPython.core.interactiveshell import InteractiveShell
InteractiveShell.ast_node_interactivity = "all"
```


```python
# Increase width display within the notebook
from IPython.core.display import display, HTML
display(HTML("<style>.container {width:90% !important;}</style>"))
```


<style>.container {width:90% !important;}</style>



```python
# Load Pandas into Pythoimport pandas as pd
from matplotlib import pyplot as plt
import pandas as pd
import io
import numpy as np
import requests
%matplotlib inline
```


```python
# Enable diplay of more rows and columns
pd.set_option('display.max_rows', 5000)
pd.set_option('display.max_columns', 500)
pd.set_option('display.width', 1000)
```


```python
# Read data into a DataFrame
url="https://covid.ourworldindata.org/data/owid-covid-data.csv"
s=requests.get(url).content
data = pd.read_csv(io.StringIO(s.decode('utf-8')))
```


```python
import qgrid
qgrid_widget = qgrid.show_grid(data.head(20), show_toolbar=True)
qgrid_widget
```


    QgridWidget(grid_options={'fullWidthRows': True, 'syncColumnCellResize': True, 'forceFitColumns': True, 'defau…



```python
# A preview of the data set

data.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>iso_code</th>
      <th>location</th>
      <th>date</th>
      <th>total_cases</th>
      <th>new_cases</th>
      <th>total_deaths</th>
      <th>new_deaths</th>
      <th>total_cases_per_million</th>
      <th>new_cases_per_million</th>
      <th>total_deaths_per_million</th>
      <th>new_deaths_per_million</th>
      <th>total_tests</th>
      <th>new_tests</th>
      <th>total_tests_per_thousand</th>
      <th>new_tests_per_thousand</th>
      <th>new_tests_smoothed</th>
      <th>new_tests_smoothed_per_thousand</th>
      <th>tests_units</th>
      <th>stringency_index</th>
      <th>population</th>
      <th>population_density</th>
      <th>median_age</th>
      <th>aged_65_older</th>
      <th>aged_70_older</th>
      <th>gdp_per_capita</th>
      <th>extreme_poverty</th>
      <th>cvd_death_rate</th>
      <th>diabetes_prevalence</th>
      <th>female_smokers</th>
      <th>male_smokers</th>
      <th>handwashing_facilities</th>
      <th>hospital_beds_per_100k</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>ABW</td>
      <td>Aruba</td>
      <td>2020-03-13</td>
      <td>2</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>18.733</td>
      <td>18.733</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.00</td>
      <td>106766.0</td>
      <td>584.8</td>
      <td>41.2</td>
      <td>13.085</td>
      <td>7.452</td>
      <td>35973.781</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>11.62</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>ABW</td>
      <td>Aruba</td>
      <td>2020-03-20</td>
      <td>4</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>37.465</td>
      <td>18.733</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>30.56</td>
      <td>106766.0</td>
      <td>584.8</td>
      <td>41.2</td>
      <td>13.085</td>
      <td>7.452</td>
      <td>35973.781</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>11.62</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>ABW</td>
      <td>Aruba</td>
      <td>2020-03-24</td>
      <td>12</td>
      <td>8</td>
      <td>0</td>
      <td>0</td>
      <td>112.395</td>
      <td>74.930</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>41.67</td>
      <td>106766.0</td>
      <td>584.8</td>
      <td>41.2</td>
      <td>13.085</td>
      <td>7.452</td>
      <td>35973.781</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>11.62</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>ABW</td>
      <td>Aruba</td>
      <td>2020-03-25</td>
      <td>17</td>
      <td>5</td>
      <td>0</td>
      <td>0</td>
      <td>159.227</td>
      <td>46.831</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>41.67</td>
      <td>106766.0</td>
      <td>584.8</td>
      <td>41.2</td>
      <td>13.085</td>
      <td>7.452</td>
      <td>35973.781</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>11.62</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>ABW</td>
      <td>Aruba</td>
      <td>2020-03-26</td>
      <td>19</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>177.959</td>
      <td>18.733</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>41.67</td>
      <td>106766.0</td>
      <td>584.8</td>
      <td>41.2</td>
      <td>13.085</td>
      <td>7.452</td>
      <td>35973.781</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>11.62</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Type of data
type(data)
```




    pandas.core.frame.DataFrame




```python
# The first 5 rows
data.head(5)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>iso_code</th>
      <th>location</th>
      <th>date</th>
      <th>total_cases</th>
      <th>new_cases</th>
      <th>total_deaths</th>
      <th>new_deaths</th>
      <th>total_cases_per_million</th>
      <th>new_cases_per_million</th>
      <th>total_deaths_per_million</th>
      <th>new_deaths_per_million</th>
      <th>total_tests</th>
      <th>new_tests</th>
      <th>total_tests_per_thousand</th>
      <th>new_tests_per_thousand</th>
      <th>new_tests_smoothed</th>
      <th>new_tests_smoothed_per_thousand</th>
      <th>tests_units</th>
      <th>stringency_index</th>
      <th>population</th>
      <th>population_density</th>
      <th>median_age</th>
      <th>aged_65_older</th>
      <th>aged_70_older</th>
      <th>gdp_per_capita</th>
      <th>extreme_poverty</th>
      <th>cvd_death_rate</th>
      <th>diabetes_prevalence</th>
      <th>female_smokers</th>
      <th>male_smokers</th>
      <th>handwashing_facilities</th>
      <th>hospital_beds_per_100k</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>ABW</td>
      <td>Aruba</td>
      <td>2020-03-13</td>
      <td>2</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>18.733</td>
      <td>18.733</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.00</td>
      <td>106766.0</td>
      <td>584.8</td>
      <td>41.2</td>
      <td>13.085</td>
      <td>7.452</td>
      <td>35973.781</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>11.62</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>ABW</td>
      <td>Aruba</td>
      <td>2020-03-20</td>
      <td>4</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>37.465</td>
      <td>18.733</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>30.56</td>
      <td>106766.0</td>
      <td>584.8</td>
      <td>41.2</td>
      <td>13.085</td>
      <td>7.452</td>
      <td>35973.781</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>11.62</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>ABW</td>
      <td>Aruba</td>
      <td>2020-03-24</td>
      <td>12</td>
      <td>8</td>
      <td>0</td>
      <td>0</td>
      <td>112.395</td>
      <td>74.930</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>41.67</td>
      <td>106766.0</td>
      <td>584.8</td>
      <td>41.2</td>
      <td>13.085</td>
      <td>7.452</td>
      <td>35973.781</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>11.62</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>ABW</td>
      <td>Aruba</td>
      <td>2020-03-25</td>
      <td>17</td>
      <td>5</td>
      <td>0</td>
      <td>0</td>
      <td>159.227</td>
      <td>46.831</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>41.67</td>
      <td>106766.0</td>
      <td>584.8</td>
      <td>41.2</td>
      <td>13.085</td>
      <td>7.452</td>
      <td>35973.781</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>11.62</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>ABW</td>
      <td>Aruba</td>
      <td>2020-03-26</td>
      <td>19</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>177.959</td>
      <td>18.733</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>41.67</td>
      <td>106766.0</td>
      <td>584.8</td>
      <td>41.2</td>
      <td>13.085</td>
      <td>7.452</td>
      <td>35973.781</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>11.62</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
# The last 10 Rows
data.tail(5)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>iso_code</th>
      <th>location</th>
      <th>date</th>
      <th>total_cases</th>
      <th>new_cases</th>
      <th>total_deaths</th>
      <th>new_deaths</th>
      <th>total_cases_per_million</th>
      <th>new_cases_per_million</th>
      <th>total_deaths_per_million</th>
      <th>new_deaths_per_million</th>
      <th>total_tests</th>
      <th>new_tests</th>
      <th>total_tests_per_thousand</th>
      <th>new_tests_per_thousand</th>
      <th>new_tests_smoothed</th>
      <th>new_tests_smoothed_per_thousand</th>
      <th>tests_units</th>
      <th>stringency_index</th>
      <th>population</th>
      <th>population_density</th>
      <th>median_age</th>
      <th>aged_65_older</th>
      <th>aged_70_older</th>
      <th>gdp_per_capita</th>
      <th>extreme_poverty</th>
      <th>cvd_death_rate</th>
      <th>diabetes_prevalence</th>
      <th>female_smokers</th>
      <th>male_smokers</th>
      <th>handwashing_facilities</th>
      <th>hospital_beds_per_100k</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>19913</th>
      <td>NaN</td>
      <td>International</td>
      <td>2020-02-28</td>
      <td>705</td>
      <td>0</td>
      <td>4</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>19914</th>
      <td>NaN</td>
      <td>International</td>
      <td>2020-02-29</td>
      <td>705</td>
      <td>0</td>
      <td>6</td>
      <td>2</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>19915</th>
      <td>NaN</td>
      <td>International</td>
      <td>2020-03-01</td>
      <td>705</td>
      <td>0</td>
      <td>6</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>19916</th>
      <td>NaN</td>
      <td>International</td>
      <td>2020-03-02</td>
      <td>705</td>
      <td>0</td>
      <td>6</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>19917</th>
      <td>NaN</td>
      <td>International</td>
      <td>2020-03-10</td>
      <td>696</td>
      <td>-9</td>
      <td>7</td>
      <td>1</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



## Concise Summary (Including memory usage)


```python
data.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 19918 entries, 0 to 19917
    Data columns (total 32 columns):
     #   Column                           Non-Null Count  Dtype  
    ---  ------                           --------------  -----  
     0   iso_code                         19854 non-null  object
     1   location                         19918 non-null  object
     2   date                             19918 non-null  object
     3   total_cases                      19918 non-null  int64  
     4   new_cases                        19918 non-null  int64  
     5   total_deaths                     19918 non-null  int64  
     6   new_deaths                       19918 non-null  int64  
     7   total_cases_per_million          19541 non-null  float64
     8   new_cases_per_million            19541 non-null  float64
     9   total_deaths_per_million         19541 non-null  float64
     10  new_deaths_per_million           19541 non-null  float64
     11  total_tests                      5287 non-null   float64
     12  new_tests                        4699 non-null   float64
     13  total_tests_per_thousand         5287 non-null   float64
     14  new_tests_per_thousand           4699 non-null   float64
     15  new_tests_smoothed               5785 non-null   float64
     16  new_tests_smoothed_per_thousand  5785 non-null   float64
     17  tests_units                      6384 non-null   object
     18  stringency_index                 15553 non-null  float64
     19  population                       19854 non-null  float64
     20  population_density               19044 non-null  float64
     21  median_age                       18127 non-null  float64
     22  aged_65_older                    17884 non-null  float64
     23  aged_70_older                    18036 non-null  float64
     24  gdp_per_capita                   17880 non-null  float64
     25  extreme_poverty                  11861 non-null  float64
     26  cvd_death_rate                   18053 non-null  float64
     27  diabetes_prevalence              18710 non-null  float64
     28  female_smokers                   14728 non-null  float64
     29  male_smokers                     14570 non-null  float64
     30  handwashing_facilities           7858 non-null   float64
     31  hospital_beds_per_100k           16668 non-null  float64
    dtypes: float64(24), int64(4), object(4)
    memory usage: 4.9+ MB



```python
# Row labels
data.index
```




    RangeIndex(start=0, stop=19918, step=1)




```python
# Columns names
data.columns
```




    Index(['iso_code', 'location', 'date', 'total_cases', 'new_cases', 'total_deaths', 'new_deaths', 'total_cases_per_million', 'new_cases_per_million', 'total_deaths_per_million', 'new_deaths_per_million', 'total_tests', 'new_tests', 'total_tests_per_thousand', 'new_tests_per_thousand', 'new_tests_smoothed', 'new_tests_smoothed_per_thousand', 'tests_units', 'stringency_index', 'population', 'population_density', 'median_age', 'aged_65_older', 'aged_70_older', 'gdp_per_capita', 'extreme_poverty', 'cvd_death_rate', 'diabetes_prevalence', 'female_smokers', 'male_smokers', 'handwashing_facilities', 'hospital_beds_per_100k'], dtype='object')




```python
# Data types of each column
data.dtypes
```




    iso_code                            object
    location                            object
    date                                object
    total_cases                          int64
    new_cases                            int64
    total_deaths                         int64
    new_deaths                           int64
    total_cases_per_million            float64
    new_cases_per_million              float64
    total_deaths_per_million           float64
    new_deaths_per_million             float64
    total_tests                        float64
    new_tests                          float64
    total_tests_per_thousand           float64
    new_tests_per_thousand             float64
    new_tests_smoothed                 float64
    new_tests_smoothed_per_thousand    float64
    tests_units                         object
    stringency_index                   float64
    population                         float64
    population_density                 float64
    median_age                         float64
    aged_65_older                      float64
    aged_70_older                      float64
    gdp_per_capita                     float64
    extreme_poverty                    float64
    cvd_death_rate                     float64
    diabetes_prevalence                float64
    female_smokers                     float64
    male_smokers                       float64
    handwashing_facilities             float64
    hospital_beds_per_100k             float64
    dtype: object




```python
# Number of rows and columns
data.shape
```




    (19918, 32)



## A quick Summary of the data


```python
data.describe()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>total_cases</th>
      <th>new_cases</th>
      <th>total_deaths</th>
      <th>new_deaths</th>
      <th>total_cases_per_million</th>
      <th>new_cases_per_million</th>
      <th>total_deaths_per_million</th>
      <th>new_deaths_per_million</th>
      <th>total_tests</th>
      <th>new_tests</th>
      <th>total_tests_per_thousand</th>
      <th>new_tests_per_thousand</th>
      <th>new_tests_smoothed</th>
      <th>new_tests_smoothed_per_thousand</th>
      <th>stringency_index</th>
      <th>population</th>
      <th>population_density</th>
      <th>median_age</th>
      <th>aged_65_older</th>
      <th>aged_70_older</th>
      <th>gdp_per_capita</th>
      <th>extreme_poverty</th>
      <th>cvd_death_rate</th>
      <th>diabetes_prevalence</th>
      <th>female_smokers</th>
      <th>male_smokers</th>
      <th>handwashing_facilities</th>
      <th>hospital_beds_per_100k</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>1.991800e+04</td>
      <td>19918.000000</td>
      <td>19918.000000</td>
      <td>19918.000000</td>
      <td>19541.000000</td>
      <td>19541.000000</td>
      <td>19541.000000</td>
      <td>19541.000000</td>
      <td>5.287000e+03</td>
      <td>4699.000000</td>
      <td>5287.000000</td>
      <td>4699.000000</td>
      <td>5785.000000</td>
      <td>5785.000000</td>
      <td>15553.000000</td>
      <td>1.985400e+04</td>
      <td>19044.000000</td>
      <td>18127.000000</td>
      <td>17884.000000</td>
      <td>18036.000000</td>
      <td>17880.000000</td>
      <td>11861.000000</td>
      <td>18053.000000</td>
      <td>18710.000000</td>
      <td>14728.000000</td>
      <td>14570.000000</td>
      <td>7858.000000</td>
      <td>16668.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>1.825575e+04</td>
      <td>548.200221</td>
      <td>1208.974445</td>
      <td>34.741842</td>
      <td>514.986474</td>
      <td>13.363489</td>
      <td>22.563373</td>
      <td>0.577226</td>
      <td>2.554069e+05</td>
      <td>10382.310917</td>
      <td>11.451028</td>
      <td>0.392042</td>
      <td>9237.185480</td>
      <td>0.360112</td>
      <td>54.937178</td>
      <td>1.084762e+08</td>
      <td>426.420258</td>
      <td>32.399288</td>
      <td>9.900006</td>
      <td>6.306530</td>
      <td>23265.794951</td>
      <td>10.084057</td>
      <td>244.987944</td>
      <td>8.007348</td>
      <td>11.335812</td>
      <td>32.638729</td>
      <td>55.441215</td>
      <td>3.233602</td>
    </tr>
    <tr>
      <th>std</th>
      <td>1.878006e+05</td>
      <td>4902.813015</td>
      <td>12778.144590</td>
      <td>332.606374</td>
      <td>1489.373662</td>
      <td>63.480914</td>
      <td>93.657352</td>
      <td>3.580049</td>
      <td>9.184020e+05</td>
      <td>34434.815120</td>
      <td>21.143161</td>
      <td>0.609683</td>
      <td>29252.528275</td>
      <td>0.530204</td>
      <td>34.315395</td>
      <td>6.887964e+08</td>
      <td>1846.878197</td>
      <td>8.950361</td>
      <td>6.474540</td>
      <td>4.448331</td>
      <td>21389.479793</td>
      <td>17.499983</td>
      <td>119.084066</td>
      <td>4.023691</td>
      <td>10.573281</td>
      <td>13.198517</td>
      <td>30.905088</td>
      <td>2.613157</td>
    </tr>
    <tr>
      <th>min</th>
      <td>0.000000e+00</td>
      <td>-2461.000000</td>
      <td>0.000000</td>
      <td>-1918.000000</td>
      <td>0.000000</td>
      <td>-265.189000</td>
      <td>0.000000</td>
      <td>-41.023000</td>
      <td>1.000000e+00</td>
      <td>1.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>8.090000e+02</td>
      <td>0.137000</td>
      <td>15.100000</td>
      <td>1.144000</td>
      <td>0.526000</td>
      <td>661.240000</td>
      <td>0.100000</td>
      <td>79.370000</td>
      <td>0.990000</td>
      <td>0.100000</td>
      <td>7.700000</td>
      <td>1.188000</td>
      <td>0.100000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>6.000000e+00</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.702000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>8.505500e+03</td>
      <td>555.000000</td>
      <td>0.364500</td>
      <td>0.029000</td>
      <td>652.000000</td>
      <td>0.031000</td>
      <td>19.440000</td>
      <td>2.225728e+06</td>
      <td>42.368000</td>
      <td>25.300000</td>
      <td>4.029000</td>
      <td>2.361000</td>
      <td>6570.102000</td>
      <td>0.500000</td>
      <td>145.183000</td>
      <td>5.310000</td>
      <td>1.900000</td>
      <td>21.400000</td>
      <td>24.640000</td>
      <td>1.400000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>9.000000e+01</td>
      <td>2.000000</td>
      <td>1.000000</td>
      <td>0.000000</td>
      <td>29.465000</td>
      <td>0.254000</td>
      <td>0.201000</td>
      <td>0.000000</td>
      <td>4.445800e+04</td>
      <td>1955.000000</td>
      <td>2.551000</td>
      <td>0.151000</td>
      <td>2131.000000</td>
      <td>0.154000</td>
      <td>68.520000</td>
      <td>9.660350e+06</td>
      <td>93.105000</td>
      <td>32.400000</td>
      <td>7.775000</td>
      <td>5.021000</td>
      <td>15847.419000</td>
      <td>1.500000</td>
      <td>233.070000</td>
      <td>7.110000</td>
      <td>7.000000</td>
      <td>31.400000</td>
      <td>59.607000</td>
      <td>2.600000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>1.201750e+03</td>
      <td>45.000000</td>
      <td>26.000000</td>
      <td>1.000000</td>
      <td>261.054000</td>
      <td>5.925000</td>
      <td>4.850000</td>
      <td>0.056000</td>
      <td>1.612825e+05</td>
      <td>6363.500000</td>
      <td>13.573000</td>
      <td>0.543000</td>
      <td>5983.000000</td>
      <td>0.502000</td>
      <td>83.330000</td>
      <td>3.691056e+07</td>
      <td>227.322000</td>
      <td>40.900000</td>
      <td>15.322000</td>
      <td>9.842000</td>
      <td>35938.374000</td>
      <td>10.000000</td>
      <td>311.110000</td>
      <td>10.080000</td>
      <td>20.000000</td>
      <td>40.800000</td>
      <td>84.169000</td>
      <td>4.280000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>5.459526e+06</td>
      <td>107909.000000</td>
      <td>345994.000000</td>
      <td>10520.000000</td>
      <td>19624.020000</td>
      <td>4944.376000</td>
      <td>1237.551000</td>
      <td>200.040000</td>
      <td>1.416369e+07</td>
      <td>416546.000000</td>
      <td>172.316000</td>
      <td>7.285000</td>
      <td>389611.000000</td>
      <td>4.993000</td>
      <td>100.000000</td>
      <td>7.794799e+09</td>
      <td>19347.500000</td>
      <td>48.200000</td>
      <td>27.049000</td>
      <td>18.493000</td>
      <td>116935.600000</td>
      <td>77.600000</td>
      <td>724.417000</td>
      <td>23.360000</td>
      <td>44.000000</td>
      <td>78.100000</td>
      <td>98.999000</td>
      <td>13.800000</td>
    </tr>
  </tbody>
</table>
</div>




```python
data.describe(include=['object'])
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>iso_code</th>
      <th>location</th>
      <th>date</th>
      <th>tests_units</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>19854</td>
      <td>19918</td>
      <td>19918</td>
      <td>6384</td>
    </tr>
    <tr>
      <th>unique</th>
      <td>211</td>
      <td>212</td>
      <td>148</td>
      <td>5</td>
    </tr>
    <tr>
      <th>top</th>
      <td>CZE</td>
      <td>France</td>
      <td>2020-05-16</td>
      <td>tests performed</td>
    </tr>
    <tr>
      <th>freq</th>
      <td>148</td>
      <td>148</td>
      <td>211</td>
      <td>2520</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Describe all Columns
data.describe(include='all')
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>iso_code</th>
      <th>location</th>
      <th>date</th>
      <th>total_cases</th>
      <th>new_cases</th>
      <th>total_deaths</th>
      <th>new_deaths</th>
      <th>total_cases_per_million</th>
      <th>new_cases_per_million</th>
      <th>total_deaths_per_million</th>
      <th>new_deaths_per_million</th>
      <th>total_tests</th>
      <th>new_tests</th>
      <th>total_tests_per_thousand</th>
      <th>new_tests_per_thousand</th>
      <th>new_tests_smoothed</th>
      <th>new_tests_smoothed_per_thousand</th>
      <th>tests_units</th>
      <th>stringency_index</th>
      <th>population</th>
      <th>population_density</th>
      <th>median_age</th>
      <th>aged_65_older</th>
      <th>aged_70_older</th>
      <th>gdp_per_capita</th>
      <th>extreme_poverty</th>
      <th>cvd_death_rate</th>
      <th>diabetes_prevalence</th>
      <th>female_smokers</th>
      <th>male_smokers</th>
      <th>handwashing_facilities</th>
      <th>hospital_beds_per_100k</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>19854</td>
      <td>19918</td>
      <td>19918</td>
      <td>1.991800e+04</td>
      <td>19918.000000</td>
      <td>19918.000000</td>
      <td>19918.000000</td>
      <td>19541.000000</td>
      <td>19541.000000</td>
      <td>19541.000000</td>
      <td>19541.000000</td>
      <td>5.287000e+03</td>
      <td>4699.000000</td>
      <td>5287.000000</td>
      <td>4699.000000</td>
      <td>5785.000000</td>
      <td>5785.000000</td>
      <td>6384</td>
      <td>15553.000000</td>
      <td>1.985400e+04</td>
      <td>19044.000000</td>
      <td>18127.000000</td>
      <td>17884.000000</td>
      <td>18036.000000</td>
      <td>17880.000000</td>
      <td>11861.000000</td>
      <td>18053.000000</td>
      <td>18710.000000</td>
      <td>14728.000000</td>
      <td>14570.000000</td>
      <td>7858.000000</td>
      <td>16668.000000</td>
    </tr>
    <tr>
      <th>unique</th>
      <td>211</td>
      <td>212</td>
      <td>148</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>5</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>top</th>
      <td>CZE</td>
      <td>France</td>
      <td>2020-05-16</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>tests performed</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>freq</th>
      <td>148</td>
      <td>148</td>
      <td>211</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2520</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.825575e+04</td>
      <td>548.200221</td>
      <td>1208.974445</td>
      <td>34.741842</td>
      <td>514.986474</td>
      <td>13.363489</td>
      <td>22.563373</td>
      <td>0.577226</td>
      <td>2.554069e+05</td>
      <td>10382.310917</td>
      <td>11.451028</td>
      <td>0.392042</td>
      <td>9237.185480</td>
      <td>0.360112</td>
      <td>NaN</td>
      <td>54.937178</td>
      <td>1.084762e+08</td>
      <td>426.420258</td>
      <td>32.399288</td>
      <td>9.900006</td>
      <td>6.306530</td>
      <td>23265.794951</td>
      <td>10.084057</td>
      <td>244.987944</td>
      <td>8.007348</td>
      <td>11.335812</td>
      <td>32.638729</td>
      <td>55.441215</td>
      <td>3.233602</td>
    </tr>
    <tr>
      <th>std</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.878006e+05</td>
      <td>4902.813015</td>
      <td>12778.144590</td>
      <td>332.606374</td>
      <td>1489.373662</td>
      <td>63.480914</td>
      <td>93.657352</td>
      <td>3.580049</td>
      <td>9.184020e+05</td>
      <td>34434.815120</td>
      <td>21.143161</td>
      <td>0.609683</td>
      <td>29252.528275</td>
      <td>0.530204</td>
      <td>NaN</td>
      <td>34.315395</td>
      <td>6.887964e+08</td>
      <td>1846.878197</td>
      <td>8.950361</td>
      <td>6.474540</td>
      <td>4.448331</td>
      <td>21389.479793</td>
      <td>17.499983</td>
      <td>119.084066</td>
      <td>4.023691</td>
      <td>10.573281</td>
      <td>13.198517</td>
      <td>30.905088</td>
      <td>2.613157</td>
    </tr>
    <tr>
      <th>min</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.000000e+00</td>
      <td>-2461.000000</td>
      <td>0.000000</td>
      <td>-1918.000000</td>
      <td>0.000000</td>
      <td>-265.189000</td>
      <td>0.000000</td>
      <td>-41.023000</td>
      <td>1.000000e+00</td>
      <td>1.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>NaN</td>
      <td>0.000000</td>
      <td>8.090000e+02</td>
      <td>0.137000</td>
      <td>15.100000</td>
      <td>1.144000</td>
      <td>0.526000</td>
      <td>661.240000</td>
      <td>0.100000</td>
      <td>79.370000</td>
      <td>0.990000</td>
      <td>0.100000</td>
      <td>7.700000</td>
      <td>1.188000</td>
      <td>0.100000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>6.000000e+00</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.702000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>8.505500e+03</td>
      <td>555.000000</td>
      <td>0.364500</td>
      <td>0.029000</td>
      <td>652.000000</td>
      <td>0.031000</td>
      <td>NaN</td>
      <td>19.440000</td>
      <td>2.225728e+06</td>
      <td>42.368000</td>
      <td>25.300000</td>
      <td>4.029000</td>
      <td>2.361000</td>
      <td>6570.102000</td>
      <td>0.500000</td>
      <td>145.183000</td>
      <td>5.310000</td>
      <td>1.900000</td>
      <td>21.400000</td>
      <td>24.640000</td>
      <td>1.400000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>9.000000e+01</td>
      <td>2.000000</td>
      <td>1.000000</td>
      <td>0.000000</td>
      <td>29.465000</td>
      <td>0.254000</td>
      <td>0.201000</td>
      <td>0.000000</td>
      <td>4.445800e+04</td>
      <td>1955.000000</td>
      <td>2.551000</td>
      <td>0.151000</td>
      <td>2131.000000</td>
      <td>0.154000</td>
      <td>NaN</td>
      <td>68.520000</td>
      <td>9.660350e+06</td>
      <td>93.105000</td>
      <td>32.400000</td>
      <td>7.775000</td>
      <td>5.021000</td>
      <td>15847.419000</td>
      <td>1.500000</td>
      <td>233.070000</td>
      <td>7.110000</td>
      <td>7.000000</td>
      <td>31.400000</td>
      <td>59.607000</td>
      <td>2.600000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.201750e+03</td>
      <td>45.000000</td>
      <td>26.000000</td>
      <td>1.000000</td>
      <td>261.054000</td>
      <td>5.925000</td>
      <td>4.850000</td>
      <td>0.056000</td>
      <td>1.612825e+05</td>
      <td>6363.500000</td>
      <td>13.573000</td>
      <td>0.543000</td>
      <td>5983.000000</td>
      <td>0.502000</td>
      <td>NaN</td>
      <td>83.330000</td>
      <td>3.691056e+07</td>
      <td>227.322000</td>
      <td>40.900000</td>
      <td>15.322000</td>
      <td>9.842000</td>
      <td>35938.374000</td>
      <td>10.000000</td>
      <td>311.110000</td>
      <td>10.080000</td>
      <td>20.000000</td>
      <td>40.800000</td>
      <td>84.169000</td>
      <td>4.280000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>5.459526e+06</td>
      <td>107909.000000</td>
      <td>345994.000000</td>
      <td>10520.000000</td>
      <td>19624.020000</td>
      <td>4944.376000</td>
      <td>1237.551000</td>
      <td>200.040000</td>
      <td>1.416369e+07</td>
      <td>416546.000000</td>
      <td>172.316000</td>
      <td>7.285000</td>
      <td>389611.000000</td>
      <td>4.993000</td>
      <td>NaN</td>
      <td>100.000000</td>
      <td>7.794799e+09</td>
      <td>19347.500000</td>
      <td>48.200000</td>
      <td>27.049000</td>
      <td>18.493000</td>
      <td>116935.600000</td>
      <td>77.600000</td>
      <td>724.417000</td>
      <td>23.360000</td>
      <td>44.000000</td>
      <td>78.100000</td>
      <td>98.999000</td>
      <td>13.800000</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Describe a single column
data['total_deaths_per_million'].describe()
```




    count    19541.000000
    mean        22.563373
    std         93.657352
    min          0.000000
    25%          0.000000
    50%          0.201000
    75%          4.850000
    max       1237.551000
    Name: total_deaths_per_million, dtype: float64



## Count the number of occurances of each value


```python
# A frequency distribution of the total deaths per million
data['total_deaths_per_million'].value_counts().head(10)
```




    0.000     8313
    15.216      67
    0.414       67
    2.286       61
    6.094       61
    0.084       58
    0.061       55
    1.705       55
    0.352       55
    0.425       55
    Name: total_deaths_per_million, dtype: int64




```python
# Data collection frequency per location
data['location'].value_counts().sort_index().head()
```




    Afghanistan    138
    Albania         79
    Algeria        143
    Andorra         74
    Angola          66
    Name: location, dtype: int64




```python
# Data collection frequency per country
data['location'].value_counts().plot(kind='bar', figsize=(200,6));
```


![png](assets/images/covid/output_26_0.png)


# Using simple operator comparison on columns to extract relevant or drop irrelevant information
## **Filtering and Sorting**


```python
data1 = data
```


```python
# Using a series of boleans
country_zero = data1['total_deaths_per_million'] > 0
```


```python
country_zero
```




    0        False
    1        False
    2        False
    3        False
    4        False
             ...  
    19913    False
    19914    False
    19915    False
    19916    False
    19917    False
    Name: total_deaths_per_million, Length: 19918, dtype: bool




```python
# Countries that have registered deaths due to covid 19
data2 = data1[country_zero]
```


```python
# Current Total deaths per million  deu to covid 19 in ascending order
data3 = data2.sort_values('total_deaths_per_million',ascending=False)
```


```python
data3
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>iso_code</th>
      <th>location</th>
      <th>date</th>
      <th>total_cases</th>
      <th>new_cases</th>
      <th>total_deaths</th>
      <th>new_deaths</th>
      <th>total_cases_per_million</th>
      <th>new_cases_per_million</th>
      <th>total_deaths_per_million</th>
      <th>new_deaths_per_million</th>
      <th>total_tests</th>
      <th>new_tests</th>
      <th>total_tests_per_thousand</th>
      <th>new_tests_per_thousand</th>
      <th>new_tests_smoothed</th>
      <th>new_tests_smoothed_per_thousand</th>
      <th>tests_units</th>
      <th>stringency_index</th>
      <th>population</th>
      <th>population_density</th>
      <th>median_age</th>
      <th>aged_65_older</th>
      <th>aged_70_older</th>
      <th>gdp_per_capita</th>
      <th>extreme_poverty</th>
      <th>cvd_death_rate</th>
      <th>diabetes_prevalence</th>
      <th>female_smokers</th>
      <th>male_smokers</th>
      <th>handwashing_facilities</th>
      <th>hospital_beds_per_100k</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>16627</th>
      <td>SMR</td>
      <td>San Marino</td>
      <td>2020-05-24</td>
      <td>665</td>
      <td>4</td>
      <td>42</td>
      <td>1</td>
      <td>19594.555</td>
      <td>117.862</td>
      <td>1237.551</td>
      <td>29.465</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>3.393800e+04</td>
      <td>556.667</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>56861.470</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>5.64</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>3.80</td>
    </tr>
    <tr>
      <th>16628</th>
      <td>SMR</td>
      <td>San Marino</td>
      <td>2020-05-25</td>
      <td>665</td>
      <td>0</td>
      <td>42</td>
      <td>0</td>
      <td>19594.555</td>
      <td>0.000</td>
      <td>1237.551</td>
      <td>0.000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>3.393800e+04</td>
      <td>556.667</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>56861.470</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>5.64</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>3.80</td>
    </tr>
    <tr>
      <th>16629</th>
      <td>SMR</td>
      <td>San Marino</td>
      <td>2020-05-26</td>
      <td>666</td>
      <td>1</td>
      <td>42</td>
      <td>0</td>
      <td>19624.020</td>
      <td>29.465</td>
      <td>1237.551</td>
      <td>0.000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>3.393800e+04</td>
      <td>556.667</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>56861.470</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>5.64</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>3.80</td>
    </tr>
    <tr>
      <th>16615</th>
      <td>SMR</td>
      <td>San Marino</td>
      <td>2020-05-12</td>
      <td>628</td>
      <td>0</td>
      <td>41</td>
      <td>0</td>
      <td>18504.331</td>
      <td>0.000</td>
      <td>1208.085</td>
      <td>0.000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>66.67</td>
      <td>3.393800e+04</td>
      <td>556.667</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>56861.470</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>5.64</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>3.80</td>
    </tr>
    <tr>
      <th>16624</th>
      <td>SMR</td>
      <td>San Marino</td>
      <td>2020-05-21</td>
      <td>656</td>
      <td>1</td>
      <td>41</td>
      <td>0</td>
      <td>19329.365</td>
      <td>29.465</td>
      <td>1208.085</td>
      <td>0.000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>66.67</td>
      <td>3.393800e+04</td>
      <td>556.667</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>56861.470</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>5.64</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>3.80</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>3451</th>
      <td>CHN</td>
      <td>China</td>
      <td>2020-01-11</td>
      <td>59</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0.041</td>
      <td>0.000</td>
      <td>0.001</td>
      <td>0.001</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2.78</td>
      <td>1.439324e+09</td>
      <td>147.674</td>
      <td>38.7</td>
      <td>10.641</td>
      <td>5.929</td>
      <td>15308.712</td>
      <td>0.7</td>
      <td>261.899</td>
      <td>9.74</td>
      <td>1.9</td>
      <td>48.4</td>
      <td>NaN</td>
      <td>4.34</td>
    </tr>
    <tr>
      <th>3452</th>
      <td>CHN</td>
      <td>China</td>
      <td>2020-01-12</td>
      <td>59</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0.041</td>
      <td>0.000</td>
      <td>0.001</td>
      <td>0.000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2.78</td>
      <td>1.439324e+09</td>
      <td>147.674</td>
      <td>38.7</td>
      <td>10.641</td>
      <td>5.929</td>
      <td>15308.712</td>
      <td>0.7</td>
      <td>261.899</td>
      <td>9.74</td>
      <td>1.9</td>
      <td>48.4</td>
      <td>NaN</td>
      <td>4.34</td>
    </tr>
    <tr>
      <th>3453</th>
      <td>CHN</td>
      <td>China</td>
      <td>2020-01-13</td>
      <td>59</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0.041</td>
      <td>0.000</td>
      <td>0.001</td>
      <td>0.000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2.78</td>
      <td>1.439324e+09</td>
      <td>147.674</td>
      <td>38.7</td>
      <td>10.641</td>
      <td>5.929</td>
      <td>15308.712</td>
      <td>0.7</td>
      <td>261.899</td>
      <td>9.74</td>
      <td>1.9</td>
      <td>48.4</td>
      <td>NaN</td>
      <td>4.34</td>
    </tr>
    <tr>
      <th>3454</th>
      <td>CHN</td>
      <td>China</td>
      <td>2020-01-14</td>
      <td>59</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0.041</td>
      <td>0.000</td>
      <td>0.001</td>
      <td>0.000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2.78</td>
      <td>1.439324e+09</td>
      <td>147.674</td>
      <td>38.7</td>
      <td>10.641</td>
      <td>5.929</td>
      <td>15308.712</td>
      <td>0.7</td>
      <td>261.899</td>
      <td>9.74</td>
      <td>1.9</td>
      <td>48.4</td>
      <td>NaN</td>
      <td>4.34</td>
    </tr>
    <tr>
      <th>3455</th>
      <td>CHN</td>
      <td>China</td>
      <td>2020-01-15</td>
      <td>59</td>
      <td>0</td>
      <td>2</td>
      <td>1</td>
      <td>0.041</td>
      <td>0.000</td>
      <td>0.001</td>
      <td>0.001</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>8.33</td>
      <td>1.439324e+09</td>
      <td>147.674</td>
      <td>38.7</td>
      <td>10.641</td>
      <td>5.929</td>
      <td>15308.712</td>
      <td>0.7</td>
      <td>261.899</td>
      <td>9.74</td>
      <td>1.9</td>
      <td>48.4</td>
      <td>NaN</td>
      <td>4.34</td>
    </tr>
  </tbody>
</table>
<p>11228 rows × 32 columns</p>
</div>



> San Marino has the highest death density, China has the  this is in terms of the total deaths per a million people



```python
# Total deaths per million  deu to covid 19 in descending order
data4 = data2.sort_values('total_deaths_per_million',ascending=True)
data4
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>iso_code</th>
      <th>location</th>
      <th>date</th>
      <th>total_cases</th>
      <th>new_cases</th>
      <th>total_deaths</th>
      <th>new_deaths</th>
      <th>total_cases_per_million</th>
      <th>new_cases_per_million</th>
      <th>total_deaths_per_million</th>
      <th>new_deaths_per_million</th>
      <th>total_tests</th>
      <th>new_tests</th>
      <th>total_tests_per_thousand</th>
      <th>new_tests_per_thousand</th>
      <th>new_tests_smoothed</th>
      <th>new_tests_smoothed_per_thousand</th>
      <th>tests_units</th>
      <th>stringency_index</th>
      <th>population</th>
      <th>population_density</th>
      <th>median_age</th>
      <th>aged_65_older</th>
      <th>aged_70_older</th>
      <th>gdp_per_capita</th>
      <th>extreme_poverty</th>
      <th>cvd_death_rate</th>
      <th>diabetes_prevalence</th>
      <th>female_smokers</th>
      <th>male_smokers</th>
      <th>handwashing_facilities</th>
      <th>hospital_beds_per_100k</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>8635</th>
      <td>IND</td>
      <td>India</td>
      <td>2020-03-16</td>
      <td>93</td>
      <td>3</td>
      <td>2</td>
      <td>0</td>
      <td>0.067</td>
      <td>0.002</td>
      <td>0.001</td>
      <td>0.000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>samples tested</td>
      <td>48.15</td>
      <td>1.380004e+09</td>
      <td>450.419</td>
      <td>28.2</td>
      <td>5.989</td>
      <td>3.414</td>
      <td>6426.674</td>
      <td>21.2</td>
      <td>282.280</td>
      <td>10.39</td>
      <td>1.9</td>
      <td>20.6</td>
      <td>59.55</td>
      <td>0.53</td>
    </tr>
    <tr>
      <th>8633</th>
      <td>IND</td>
      <td>India</td>
      <td>2020-03-14</td>
      <td>83</td>
      <td>8</td>
      <td>2</td>
      <td>1</td>
      <td>0.060</td>
      <td>0.006</td>
      <td>0.001</td>
      <td>0.001</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>samples tested</td>
      <td>36.11</td>
      <td>1.380004e+09</td>
      <td>450.419</td>
      <td>28.2</td>
      <td>5.989</td>
      <td>3.414</td>
      <td>6426.674</td>
      <td>21.2</td>
      <td>282.280</td>
      <td>10.39</td>
      <td>1.9</td>
      <td>20.6</td>
      <td>59.55</td>
      <td>0.53</td>
    </tr>
    <tr>
      <th>8632</th>
      <td>IND</td>
      <td>India</td>
      <td>2020-03-13</td>
      <td>75</td>
      <td>2</td>
      <td>1</td>
      <td>1</td>
      <td>0.054</td>
      <td>0.001</td>
      <td>0.001</td>
      <td>0.001</td>
      <td>6500.0</td>
      <td>NaN</td>
      <td>0.005</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>samples tested</td>
      <td>33.33</td>
      <td>1.380004e+09</td>
      <td>450.419</td>
      <td>28.2</td>
      <td>5.989</td>
      <td>3.414</td>
      <td>6426.674</td>
      <td>21.2</td>
      <td>282.280</td>
      <td>10.39</td>
      <td>1.9</td>
      <td>20.6</td>
      <td>59.55</td>
      <td>0.53</td>
    </tr>
    <tr>
      <th>3458</th>
      <td>CHN</td>
      <td>China</td>
      <td>2020-01-18</td>
      <td>80</td>
      <td>17</td>
      <td>2</td>
      <td>0</td>
      <td>0.056</td>
      <td>0.012</td>
      <td>0.001</td>
      <td>0.000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>8.33</td>
      <td>1.439324e+09</td>
      <td>147.674</td>
      <td>38.7</td>
      <td>10.641</td>
      <td>5.929</td>
      <td>15308.712</td>
      <td>0.7</td>
      <td>261.899</td>
      <td>9.74</td>
      <td>1.9</td>
      <td>48.4</td>
      <td>NaN</td>
      <td>4.34</td>
    </tr>
    <tr>
      <th>3457</th>
      <td>CHN</td>
      <td>China</td>
      <td>2020-01-17</td>
      <td>63</td>
      <td>4</td>
      <td>2</td>
      <td>0</td>
      <td>0.044</td>
      <td>0.003</td>
      <td>0.001</td>
      <td>0.000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>8.33</td>
      <td>1.439324e+09</td>
      <td>147.674</td>
      <td>38.7</td>
      <td>10.641</td>
      <td>5.929</td>
      <td>15308.712</td>
      <td>0.7</td>
      <td>261.899</td>
      <td>9.74</td>
      <td>1.9</td>
      <td>48.4</td>
      <td>NaN</td>
      <td>4.34</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>16610</th>
      <td>SMR</td>
      <td>San Marino</td>
      <td>2020-05-07</td>
      <td>608</td>
      <td>19</td>
      <td>41</td>
      <td>0</td>
      <td>17915.022</td>
      <td>559.844</td>
      <td>1208.085</td>
      <td>0.000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>66.67</td>
      <td>3.393800e+04</td>
      <td>556.667</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>56861.470</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>5.64</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>3.80</td>
    </tr>
    <tr>
      <th>16615</th>
      <td>SMR</td>
      <td>San Marino</td>
      <td>2020-05-12</td>
      <td>628</td>
      <td>0</td>
      <td>41</td>
      <td>0</td>
      <td>18504.331</td>
      <td>0.000</td>
      <td>1208.085</td>
      <td>0.000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>66.67</td>
      <td>3.393800e+04</td>
      <td>556.667</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>56861.470</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>5.64</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>3.80</td>
    </tr>
    <tr>
      <th>16628</th>
      <td>SMR</td>
      <td>San Marino</td>
      <td>2020-05-25</td>
      <td>665</td>
      <td>0</td>
      <td>42</td>
      <td>0</td>
      <td>19594.555</td>
      <td>0.000</td>
      <td>1237.551</td>
      <td>0.000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>3.393800e+04</td>
      <td>556.667</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>56861.470</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>5.64</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>3.80</td>
    </tr>
    <tr>
      <th>16629</th>
      <td>SMR</td>
      <td>San Marino</td>
      <td>2020-05-26</td>
      <td>666</td>
      <td>1</td>
      <td>42</td>
      <td>0</td>
      <td>19624.020</td>
      <td>29.465</td>
      <td>1237.551</td>
      <td>0.000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>3.393800e+04</td>
      <td>556.667</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>56861.470</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>5.64</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>3.80</td>
    </tr>
    <tr>
      <th>16627</th>
      <td>SMR</td>
      <td>San Marino</td>
      <td>2020-05-24</td>
      <td>665</td>
      <td>4</td>
      <td>42</td>
      <td>1</td>
      <td>19594.555</td>
      <td>117.862</td>
      <td>1237.551</td>
      <td>29.465</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>3.393800e+04</td>
      <td>556.667</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>56861.470</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>5.64</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>3.80</td>
    </tr>
  </tbody>
</table>
<p>11228 rows × 32 columns</p>
</div>



<a id="columns"></a>

## Manipulation on  `DataFrame` columns.


```python
data.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>iso_code</th>
      <th>location</th>
      <th>date</th>
      <th>total_cases</th>
      <th>new_cases</th>
      <th>total_deaths</th>
      <th>new_deaths</th>
      <th>total_cases_per_million</th>
      <th>new_cases_per_million</th>
      <th>total_deaths_per_million</th>
      <th>new_deaths_per_million</th>
      <th>total_tests</th>
      <th>new_tests</th>
      <th>total_tests_per_thousand</th>
      <th>new_tests_per_thousand</th>
      <th>new_tests_smoothed</th>
      <th>new_tests_smoothed_per_thousand</th>
      <th>tests_units</th>
      <th>stringency_index</th>
      <th>population</th>
      <th>population_density</th>
      <th>median_age</th>
      <th>aged_65_older</th>
      <th>aged_70_older</th>
      <th>gdp_per_capita</th>
      <th>extreme_poverty</th>
      <th>cvd_death_rate</th>
      <th>diabetes_prevalence</th>
      <th>female_smokers</th>
      <th>male_smokers</th>
      <th>handwashing_facilities</th>
      <th>hospital_beds_per_100k</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>ABW</td>
      <td>Aruba</td>
      <td>2020-03-13</td>
      <td>2</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>18.733</td>
      <td>18.733</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.00</td>
      <td>106766.0</td>
      <td>584.8</td>
      <td>41.2</td>
      <td>13.085</td>
      <td>7.452</td>
      <td>35973.781</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>11.62</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>ABW</td>
      <td>Aruba</td>
      <td>2020-03-20</td>
      <td>4</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>37.465</td>
      <td>18.733</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>30.56</td>
      <td>106766.0</td>
      <td>584.8</td>
      <td>41.2</td>
      <td>13.085</td>
      <td>7.452</td>
      <td>35973.781</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>11.62</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>ABW</td>
      <td>Aruba</td>
      <td>2020-03-24</td>
      <td>12</td>
      <td>8</td>
      <td>0</td>
      <td>0</td>
      <td>112.395</td>
      <td>74.930</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>41.67</td>
      <td>106766.0</td>
      <td>584.8</td>
      <td>41.2</td>
      <td>13.085</td>
      <td>7.452</td>
      <td>35973.781</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>11.62</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>ABW</td>
      <td>Aruba</td>
      <td>2020-03-25</td>
      <td>17</td>
      <td>5</td>
      <td>0</td>
      <td>0</td>
      <td>159.227</td>
      <td>46.831</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>41.67</td>
      <td>106766.0</td>
      <td>584.8</td>
      <td>41.2</td>
      <td>13.085</td>
      <td>7.452</td>
      <td>35973.781</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>11.62</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>ABW</td>
      <td>Aruba</td>
      <td>2020-03-26</td>
      <td>19</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>177.959</td>
      <td>18.733</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>41.67</td>
      <td>106766.0</td>
      <td>584.8</td>
      <td>41.2</td>
      <td>13.085</td>
      <td>7.452</td>
      <td>35973.781</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>11.62</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



### DataFrame sorted  in terms of the total tests values in ascending order


```python
# Sort the DataFrame in terms of the total tests values in ascending order
data.sort_values('total_tests', ascending=False)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>iso_code</th>
      <th>location</th>
      <th>date</th>
      <th>total_cases</th>
      <th>new_cases</th>
      <th>total_deaths</th>
      <th>new_deaths</th>
      <th>total_cases_per_million</th>
      <th>new_cases_per_million</th>
      <th>total_deaths_per_million</th>
      <th>new_deaths_per_million</th>
      <th>total_tests</th>
      <th>new_tests</th>
      <th>total_tests_per_thousand</th>
      <th>new_tests_per_thousand</th>
      <th>new_tests_smoothed</th>
      <th>new_tests_smoothed_per_thousand</th>
      <th>tests_units</th>
      <th>stringency_index</th>
      <th>population</th>
      <th>population_density</th>
      <th>median_age</th>
      <th>aged_65_older</th>
      <th>aged_70_older</th>
      <th>gdp_per_capita</th>
      <th>extreme_poverty</th>
      <th>cvd_death_rate</th>
      <th>diabetes_prevalence</th>
      <th>female_smokers</th>
      <th>male_smokers</th>
      <th>handwashing_facilities</th>
      <th>hospital_beds_per_100k</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>18784</th>
      <td>USA</td>
      <td>United States</td>
      <td>2020-05-24</td>
      <td>1622670</td>
      <td>21236</td>
      <td>97087</td>
      <td>1080</td>
      <td>4902.287</td>
      <td>64.157</td>
      <td>293.312</td>
      <td>3.263</td>
      <td>14163694.0</td>
      <td>378908.0</td>
      <td>42.790</td>
      <td>1.145</td>
      <td>386196.0</td>
      <td>1.167</td>
      <td>inconsistent units (COVID Tracking Project)</td>
      <td>NaN</td>
      <td>331002647.0</td>
      <td>35.608</td>
      <td>38.3</td>
      <td>15.413</td>
      <td>9.732</td>
      <td>54225.446</td>
      <td>1.2</td>
      <td>151.089</td>
      <td>10.79</td>
      <td>19.1</td>
      <td>24.6</td>
      <td>NaN</td>
      <td>2.77</td>
    </tr>
    <tr>
      <th>18783</th>
      <td>USA</td>
      <td>United States</td>
      <td>2020-05-23</td>
      <td>1601434</td>
      <td>24147</td>
      <td>96007</td>
      <td>1305</td>
      <td>4838.130</td>
      <td>72.951</td>
      <td>290.049</td>
      <td>3.943</td>
      <td>13784786.0</td>
      <td>365728.0</td>
      <td>41.646</td>
      <td>1.105</td>
      <td>389611.0</td>
      <td>1.177</td>
      <td>inconsistent units (COVID Tracking Project)</td>
      <td>NaN</td>
      <td>331002647.0</td>
      <td>35.608</td>
      <td>38.3</td>
      <td>15.413</td>
      <td>9.732</td>
      <td>54225.446</td>
      <td>1.2</td>
      <td>151.089</td>
      <td>10.79</td>
      <td>19.1</td>
      <td>24.6</td>
      <td>NaN</td>
      <td>2.77</td>
    </tr>
    <tr>
      <th>18782</th>
      <td>USA</td>
      <td>United States</td>
      <td>2020-05-22</td>
      <td>1577287</td>
      <td>25434</td>
      <td>94702</td>
      <td>1263</td>
      <td>4765.179</td>
      <td>76.839</td>
      <td>286.106</td>
      <td>3.816</td>
      <td>13419058.0</td>
      <td>394296.0</td>
      <td>40.541</td>
      <td>1.191</td>
      <td>387783.0</td>
      <td>1.172</td>
      <td>inconsistent units (COVID Tracking Project)</td>
      <td>NaN</td>
      <td>331002647.0</td>
      <td>35.608</td>
      <td>38.3</td>
      <td>15.413</td>
      <td>9.732</td>
      <td>54225.446</td>
      <td>1.2</td>
      <td>151.089</td>
      <td>10.79</td>
      <td>19.1</td>
      <td>24.6</td>
      <td>NaN</td>
      <td>2.77</td>
    </tr>
    <tr>
      <th>18781</th>
      <td>USA</td>
      <td>United States</td>
      <td>2020-05-21</td>
      <td>1551853</td>
      <td>23285</td>
      <td>93439</td>
      <td>1518</td>
      <td>4688.340</td>
      <td>70.347</td>
      <td>282.291</td>
      <td>4.586</td>
      <td>13024762.0</td>
      <td>416546.0</td>
      <td>39.349</td>
      <td>1.258</td>
      <td>383304.0</td>
      <td>1.158</td>
      <td>inconsistent units (COVID Tracking Project)</td>
      <td>NaN</td>
      <td>331002647.0</td>
      <td>35.608</td>
      <td>38.3</td>
      <td>15.413</td>
      <td>9.732</td>
      <td>54225.446</td>
      <td>1.2</td>
      <td>151.089</td>
      <td>10.79</td>
      <td>19.1</td>
      <td>24.6</td>
      <td>NaN</td>
      <td>2.77</td>
    </tr>
    <tr>
      <th>18780</th>
      <td>USA</td>
      <td>United States</td>
      <td>2020-05-20</td>
      <td>1528568</td>
      <td>19970</td>
      <td>91921</td>
      <td>1568</td>
      <td>4617.993</td>
      <td>60.332</td>
      <td>277.705</td>
      <td>4.737</td>
      <td>12608216.0</td>
      <td>405404.0</td>
      <td>38.091</td>
      <td>1.225</td>
      <td>377619.0</td>
      <td>1.141</td>
      <td>inconsistent units (COVID Tracking Project)</td>
      <td>72.69</td>
      <td>331002647.0</td>
      <td>35.608</td>
      <td>38.3</td>
      <td>15.413</td>
      <td>9.732</td>
      <td>54225.446</td>
      <td>1.2</td>
      <td>151.089</td>
      <td>10.79</td>
      <td>19.1</td>
      <td>24.6</td>
      <td>NaN</td>
      <td>2.77</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>19913</th>
      <td>NaN</td>
      <td>International</td>
      <td>2020-02-28</td>
      <td>705</td>
      <td>0</td>
      <td>4</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>19914</th>
      <td>NaN</td>
      <td>International</td>
      <td>2020-02-29</td>
      <td>705</td>
      <td>0</td>
      <td>6</td>
      <td>2</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>19915</th>
      <td>NaN</td>
      <td>International</td>
      <td>2020-03-01</td>
      <td>705</td>
      <td>0</td>
      <td>6</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>19916</th>
      <td>NaN</td>
      <td>International</td>
      <td>2020-03-02</td>
      <td>705</td>
      <td>0</td>
      <td>6</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>19917</th>
      <td>NaN</td>
      <td>International</td>
      <td>2020-03-10</td>
      <td>696</td>
      <td>-9</td>
      <td>7</td>
      <td>1</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>19918 rows × 32 columns</p>
</div>




```python
data.sort_values('total_tests', ascending=True)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>iso_code</th>
      <th>location</th>
      <th>date</th>
      <th>total_cases</th>
      <th>new_cases</th>
      <th>total_deaths</th>
      <th>new_deaths</th>
      <th>total_cases_per_million</th>
      <th>new_cases_per_million</th>
      <th>total_deaths_per_million</th>
      <th>new_deaths_per_million</th>
      <th>total_tests</th>
      <th>new_tests</th>
      <th>total_tests_per_thousand</th>
      <th>new_tests_per_thousand</th>
      <th>new_tests_smoothed</th>
      <th>new_tests_smoothed_per_thousand</th>
      <th>tests_units</th>
      <th>stringency_index</th>
      <th>population</th>
      <th>population_density</th>
      <th>median_age</th>
      <th>aged_65_older</th>
      <th>aged_70_older</th>
      <th>gdp_per_capita</th>
      <th>extreme_poverty</th>
      <th>cvd_death_rate</th>
      <th>diabetes_prevalence</th>
      <th>female_smokers</th>
      <th>male_smokers</th>
      <th>handwashing_facilities</th>
      <th>hospital_beds_per_100k</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>16124</th>
      <td>SEN</td>
      <td>Senegal</td>
      <td>2020-03-02</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>tests performed</td>
      <td>0.00</td>
      <td>16743930.0</td>
      <td>82.328</td>
      <td>18.7</td>
      <td>3.008</td>
      <td>1.796</td>
      <td>2470.580</td>
      <td>38.0</td>
      <td>241.219</td>
      <td>2.42</td>
      <td>0.4</td>
      <td>16.6</td>
      <td>20.859</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>15228</th>
      <td>PRY</td>
      <td>Paraguay</td>
      <td>2020-03-07</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>samples tested</td>
      <td>5.56</td>
      <td>7132530.0</td>
      <td>17.144</td>
      <td>26.5</td>
      <td>6.378</td>
      <td>3.833</td>
      <td>8827.010</td>
      <td>1.7</td>
      <td>199.128</td>
      <td>8.27</td>
      <td>5.0</td>
      <td>21.6</td>
      <td>79.602</td>
      <td>1.30</td>
    </tr>
    <tr>
      <th>3233</th>
      <td>CHE</td>
      <td>Switzerland</td>
      <td>2020-01-24</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0.000</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>tests performed</td>
      <td>0.00</td>
      <td>8654618.0</td>
      <td>214.243</td>
      <td>43.1</td>
      <td>18.436</td>
      <td>12.644</td>
      <td>57410.166</td>
      <td>NaN</td>
      <td>99.739</td>
      <td>5.59</td>
      <td>22.6</td>
      <td>28.9</td>
      <td>NaN</td>
      <td>4.53</td>
    </tr>
    <tr>
      <th>14071</th>
      <td>NPL</td>
      <td>Nepal</td>
      <td>2020-01-28</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0.034</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>3.0</td>
      <td>NaN</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>people tested</td>
      <td>13.89</td>
      <td>29136808.0</td>
      <td>204.430</td>
      <td>25.0</td>
      <td>5.809</td>
      <td>3.212</td>
      <td>2442.804</td>
      <td>15.0</td>
      <td>260.797</td>
      <td>7.26</td>
      <td>9.5</td>
      <td>37.8</td>
      <td>47.782</td>
      <td>0.30</td>
    </tr>
    <tr>
      <th>16125</th>
      <td>SEN</td>
      <td>Senegal</td>
      <td>2020-03-03</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0.060</td>
      <td>0.06</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>3.0</td>
      <td>2.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>tests performed</td>
      <td>0.00</td>
      <td>16743930.0</td>
      <td>82.328</td>
      <td>18.7</td>
      <td>3.008</td>
      <td>1.796</td>
      <td>2470.580</td>
      <td>38.0</td>
      <td>241.219</td>
      <td>2.42</td>
      <td>0.4</td>
      <td>16.6</td>
      <td>20.859</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>19913</th>
      <td>NaN</td>
      <td>International</td>
      <td>2020-02-28</td>
      <td>705</td>
      <td>0</td>
      <td>4</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>19914</th>
      <td>NaN</td>
      <td>International</td>
      <td>2020-02-29</td>
      <td>705</td>
      <td>0</td>
      <td>6</td>
      <td>2</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>19915</th>
      <td>NaN</td>
      <td>International</td>
      <td>2020-03-01</td>
      <td>705</td>
      <td>0</td>
      <td>6</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>19916</th>
      <td>NaN</td>
      <td>International</td>
      <td>2020-03-02</td>
      <td>705</td>
      <td>0</td>
      <td>6</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>19917</th>
      <td>NaN</td>
      <td>International</td>
      <td>2020-03-10</td>
      <td>696</td>
      <td>-9</td>
      <td>7</td>
      <td>1</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>19918 rows × 32 columns</p>
</div>



> ### * United States has recorded the highest number of tests,Senegal has the least as of May 22 2020

# Correlation between columns


```python
data
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>iso_code</th>
      <th>location</th>
      <th>date</th>
      <th>total_cases</th>
      <th>new_cases</th>
      <th>total_deaths</th>
      <th>new_deaths</th>
      <th>total_cases_per_million</th>
      <th>new_cases_per_million</th>
      <th>total_deaths_per_million</th>
      <th>new_deaths_per_million</th>
      <th>total_tests</th>
      <th>new_tests</th>
      <th>total_tests_per_thousand</th>
      <th>new_tests_per_thousand</th>
      <th>new_tests_smoothed</th>
      <th>new_tests_smoothed_per_thousand</th>
      <th>tests_units</th>
      <th>stringency_index</th>
      <th>population</th>
      <th>population_density</th>
      <th>median_age</th>
      <th>aged_65_older</th>
      <th>aged_70_older</th>
      <th>gdp_per_capita</th>
      <th>extreme_poverty</th>
      <th>cvd_death_rate</th>
      <th>diabetes_prevalence</th>
      <th>female_smokers</th>
      <th>male_smokers</th>
      <th>handwashing_facilities</th>
      <th>hospital_beds_per_100k</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>ABW</td>
      <td>Aruba</td>
      <td>2020-03-13</td>
      <td>2</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>18.733</td>
      <td>18.733</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.00</td>
      <td>106766.0</td>
      <td>584.8</td>
      <td>41.2</td>
      <td>13.085</td>
      <td>7.452</td>
      <td>35973.781</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>11.62</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>ABW</td>
      <td>Aruba</td>
      <td>2020-03-20</td>
      <td>4</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>37.465</td>
      <td>18.733</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>30.56</td>
      <td>106766.0</td>
      <td>584.8</td>
      <td>41.2</td>
      <td>13.085</td>
      <td>7.452</td>
      <td>35973.781</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>11.62</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>ABW</td>
      <td>Aruba</td>
      <td>2020-03-24</td>
      <td>12</td>
      <td>8</td>
      <td>0</td>
      <td>0</td>
      <td>112.395</td>
      <td>74.930</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>41.67</td>
      <td>106766.0</td>
      <td>584.8</td>
      <td>41.2</td>
      <td>13.085</td>
      <td>7.452</td>
      <td>35973.781</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>11.62</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>ABW</td>
      <td>Aruba</td>
      <td>2020-03-25</td>
      <td>17</td>
      <td>5</td>
      <td>0</td>
      <td>0</td>
      <td>159.227</td>
      <td>46.831</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>41.67</td>
      <td>106766.0</td>
      <td>584.8</td>
      <td>41.2</td>
      <td>13.085</td>
      <td>7.452</td>
      <td>35973.781</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>11.62</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>ABW</td>
      <td>Aruba</td>
      <td>2020-03-26</td>
      <td>19</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>177.959</td>
      <td>18.733</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>41.67</td>
      <td>106766.0</td>
      <td>584.8</td>
      <td>41.2</td>
      <td>13.085</td>
      <td>7.452</td>
      <td>35973.781</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>11.62</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>19913</th>
      <td>NaN</td>
      <td>International</td>
      <td>2020-02-28</td>
      <td>705</td>
      <td>0</td>
      <td>4</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>19914</th>
      <td>NaN</td>
      <td>International</td>
      <td>2020-02-29</td>
      <td>705</td>
      <td>0</td>
      <td>6</td>
      <td>2</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>19915</th>
      <td>NaN</td>
      <td>International</td>
      <td>2020-03-01</td>
      <td>705</td>
      <td>0</td>
      <td>6</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>19916</th>
      <td>NaN</td>
      <td>International</td>
      <td>2020-03-02</td>
      <td>705</td>
      <td>0</td>
      <td>6</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>19917</th>
      <td>NaN</td>
      <td>International</td>
      <td>2020-03-10</td>
      <td>696</td>
      <td>-9</td>
      <td>7</td>
      <td>1</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>19918 rows × 32 columns</p>
</div>




```python
# Is there a corelation between total cases and tatal deaths

data.plot(kind='scatter', x='extreme_poverty', y='total_deaths_per_million');
```


![png](assets/images/covid/output_44_0.png)



```python
# Count the number of missing values in a specific column
null_count = data.total_tests.isnull()
```


```python
null_count
```




    0        True
    1        True
    2        True
    3        True
    4        True
             ...
    19913    True
    19914    True
    19915    True
    19916    True
    19917    True
    Name: total_tests, Length: 19918, dtype: bool




```python
# Show missing content in total_tests only
data[null_count]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>iso_code</th>
      <th>location</th>
      <th>date</th>
      <th>total_cases</th>
      <th>new_cases</th>
      <th>total_deaths</th>
      <th>new_deaths</th>
      <th>total_cases_per_million</th>
      <th>new_cases_per_million</th>
      <th>total_deaths_per_million</th>
      <th>new_deaths_per_million</th>
      <th>total_tests</th>
      <th>new_tests</th>
      <th>total_tests_per_thousand</th>
      <th>new_tests_per_thousand</th>
      <th>new_tests_smoothed</th>
      <th>new_tests_smoothed_per_thousand</th>
      <th>tests_units</th>
      <th>stringency_index</th>
      <th>population</th>
      <th>population_density</th>
      <th>median_age</th>
      <th>aged_65_older</th>
      <th>aged_70_older</th>
      <th>gdp_per_capita</th>
      <th>extreme_poverty</th>
      <th>cvd_death_rate</th>
      <th>diabetes_prevalence</th>
      <th>female_smokers</th>
      <th>male_smokers</th>
      <th>handwashing_facilities</th>
      <th>hospital_beds_per_100k</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>ABW</td>
      <td>Aruba</td>
      <td>2020-03-13</td>
      <td>2</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>18.733</td>
      <td>18.733</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.00</td>
      <td>106766.0</td>
      <td>584.8</td>
      <td>41.2</td>
      <td>13.085</td>
      <td>7.452</td>
      <td>35973.781</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>11.62</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>ABW</td>
      <td>Aruba</td>
      <td>2020-03-20</td>
      <td>4</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>37.465</td>
      <td>18.733</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>30.56</td>
      <td>106766.0</td>
      <td>584.8</td>
      <td>41.2</td>
      <td>13.085</td>
      <td>7.452</td>
      <td>35973.781</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>11.62</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>ABW</td>
      <td>Aruba</td>
      <td>2020-03-24</td>
      <td>12</td>
      <td>8</td>
      <td>0</td>
      <td>0</td>
      <td>112.395</td>
      <td>74.930</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>41.67</td>
      <td>106766.0</td>
      <td>584.8</td>
      <td>41.2</td>
      <td>13.085</td>
      <td>7.452</td>
      <td>35973.781</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>11.62</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>ABW</td>
      <td>Aruba</td>
      <td>2020-03-25</td>
      <td>17</td>
      <td>5</td>
      <td>0</td>
      <td>0</td>
      <td>159.227</td>
      <td>46.831</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>41.67</td>
      <td>106766.0</td>
      <td>584.8</td>
      <td>41.2</td>
      <td>13.085</td>
      <td>7.452</td>
      <td>35973.781</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>11.62</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>ABW</td>
      <td>Aruba</td>
      <td>2020-03-26</td>
      <td>19</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>177.959</td>
      <td>18.733</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>41.67</td>
      <td>106766.0</td>
      <td>584.8</td>
      <td>41.2</td>
      <td>13.085</td>
      <td>7.452</td>
      <td>35973.781</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>11.62</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>19913</th>
      <td>NaN</td>
      <td>International</td>
      <td>2020-02-28</td>
      <td>705</td>
      <td>0</td>
      <td>4</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>19914</th>
      <td>NaN</td>
      <td>International</td>
      <td>2020-02-29</td>
      <td>705</td>
      <td>0</td>
      <td>6</td>
      <td>2</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>19915</th>
      <td>NaN</td>
      <td>International</td>
      <td>2020-03-01</td>
      <td>705</td>
      <td>0</td>
      <td>6</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>19916</th>
      <td>NaN</td>
      <td>International</td>
      <td>2020-03-02</td>
      <td>705</td>
      <td>0</td>
      <td>6</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>19917</th>
      <td>NaN</td>
      <td>International</td>
      <td>2020-03-10</td>
      <td>696</td>
      <td>-9</td>
      <td>7</td>
      <td>1</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>14631 rows × 32 columns</p>
</div>




```python
data[null_count].shape
```




    (14631, 32)




```python
notnull_count = data.total_tests.notnull()
```


```python
notnull_count
```




    0        False
    1        False
    2        False
    3        False
    4        False
             ...  
    19913    False
    19914    False
    19915    False
    19916    False
    19917    False
    Name: total_tests, Length: 19918, dtype: bool




```python
# Only show non Missing total_tests
data[notnull_count]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>iso_code</th>
      <th>location</th>
      <th>date</th>
      <th>total_cases</th>
      <th>new_cases</th>
      <th>total_deaths</th>
      <th>new_deaths</th>
      <th>total_cases_per_million</th>
      <th>new_cases_per_million</th>
      <th>total_deaths_per_million</th>
      <th>new_deaths_per_million</th>
      <th>total_tests</th>
      <th>new_tests</th>
      <th>total_tests_per_thousand</th>
      <th>new_tests_per_thousand</th>
      <th>new_tests_smoothed</th>
      <th>new_tests_smoothed_per_thousand</th>
      <th>tests_units</th>
      <th>stringency_index</th>
      <th>population</th>
      <th>population_density</th>
      <th>median_age</th>
      <th>aged_65_older</th>
      <th>aged_70_older</th>
      <th>gdp_per_capita</th>
      <th>extreme_poverty</th>
      <th>cvd_death_rate</th>
      <th>diabetes_prevalence</th>
      <th>female_smokers</th>
      <th>male_smokers</th>
      <th>handwashing_facilities</th>
      <th>hospital_beds_per_100k</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>657</th>
      <td>ARG</td>
      <td>Argentina</td>
      <td>2020-04-08</td>
      <td>1715</td>
      <td>87</td>
      <td>60</td>
      <td>7</td>
      <td>37.946</td>
      <td>1.925</td>
      <td>1.328</td>
      <td>0.155</td>
      <td>13330.0</td>
      <td>NaN</td>
      <td>0.295</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>tests performed</td>
      <td>100.0</td>
      <td>45195777.0</td>
      <td>16.177</td>
      <td>31.9</td>
      <td>11.198</td>
      <td>7.441</td>
      <td>18933.907</td>
      <td>0.6</td>
      <td>191.032</td>
      <td>5.50</td>
      <td>16.2</td>
      <td>27.7</td>
      <td>NaN</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>658</th>
      <td>ARG</td>
      <td>Argentina</td>
      <td>2020-04-09</td>
      <td>1795</td>
      <td>80</td>
      <td>65</td>
      <td>5</td>
      <td>39.716</td>
      <td>1.770</td>
      <td>1.438</td>
      <td>0.111</td>
      <td>14850.0</td>
      <td>1520.0</td>
      <td>0.329</td>
      <td>0.034</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>tests performed</td>
      <td>100.0</td>
      <td>45195777.0</td>
      <td>16.177</td>
      <td>31.9</td>
      <td>11.198</td>
      <td>7.441</td>
      <td>18933.907</td>
      <td>0.6</td>
      <td>191.032</td>
      <td>5.50</td>
      <td>16.2</td>
      <td>27.7</td>
      <td>NaN</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>659</th>
      <td>ARG</td>
      <td>Argentina</td>
      <td>2020-04-10</td>
      <td>1894</td>
      <td>99</td>
      <td>79</td>
      <td>14</td>
      <td>41.907</td>
      <td>2.190</td>
      <td>1.748</td>
      <td>0.310</td>
      <td>16379.0</td>
      <td>1529.0</td>
      <td>0.362</td>
      <td>0.034</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>tests performed</td>
      <td>100.0</td>
      <td>45195777.0</td>
      <td>16.177</td>
      <td>31.9</td>
      <td>11.198</td>
      <td>7.441</td>
      <td>18933.907</td>
      <td>0.6</td>
      <td>191.032</td>
      <td>5.50</td>
      <td>16.2</td>
      <td>27.7</td>
      <td>NaN</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>660</th>
      <td>ARG</td>
      <td>Argentina</td>
      <td>2020-04-11</td>
      <td>1975</td>
      <td>81</td>
      <td>82</td>
      <td>3</td>
      <td>43.699</td>
      <td>1.792</td>
      <td>1.814</td>
      <td>0.066</td>
      <td>18027.0</td>
      <td>1648.0</td>
      <td>0.399</td>
      <td>0.036</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>tests performed</td>
      <td>100.0</td>
      <td>45195777.0</td>
      <td>16.177</td>
      <td>31.9</td>
      <td>11.198</td>
      <td>7.441</td>
      <td>18933.907</td>
      <td>0.6</td>
      <td>191.032</td>
      <td>5.50</td>
      <td>16.2</td>
      <td>27.7</td>
      <td>NaN</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>662</th>
      <td>ARG</td>
      <td>Argentina</td>
      <td>2020-04-13</td>
      <td>2203</td>
      <td>66</td>
      <td>95</td>
      <td>6</td>
      <td>48.743</td>
      <td>1.460</td>
      <td>2.102</td>
      <td>0.133</td>
      <td>19758.0</td>
      <td>NaN</td>
      <td>0.437</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>tests performed</td>
      <td>100.0</td>
      <td>45195777.0</td>
      <td>16.177</td>
      <td>31.9</td>
      <td>11.198</td>
      <td>7.441</td>
      <td>18933.907</td>
      <td>0.6</td>
      <td>191.032</td>
      <td>5.50</td>
      <td>16.2</td>
      <td>27.7</td>
      <td>NaN</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>19699</th>
      <td>ZWE</td>
      <td>Zimbabwe</td>
      <td>2020-05-20</td>
      <td>46</td>
      <td>0</td>
      <td>4</td>
      <td>0</td>
      <td>3.095</td>
      <td>0.000</td>
      <td>0.269</td>
      <td>0.000</td>
      <td>14618.0</td>
      <td>443.0</td>
      <td>0.984</td>
      <td>0.030</td>
      <td>490.0</td>
      <td>0.033</td>
      <td>tests performed</td>
      <td>NaN</td>
      <td>14862927.0</td>
      <td>42.729</td>
      <td>19.6</td>
      <td>2.822</td>
      <td>1.882</td>
      <td>1899.775</td>
      <td>21.4</td>
      <td>307.846</td>
      <td>1.82</td>
      <td>1.6</td>
      <td>30.7</td>
      <td>36.791</td>
      <td>1.7</td>
    </tr>
    <tr>
      <th>19700</th>
      <td>ZWE</td>
      <td>Zimbabwe</td>
      <td>2020-05-21</td>
      <td>48</td>
      <td>2</td>
      <td>4</td>
      <td>0</td>
      <td>3.230</td>
      <td>0.135</td>
      <td>0.269</td>
      <td>0.000</td>
      <td>15084.0</td>
      <td>466.0</td>
      <td>1.015</td>
      <td>0.031</td>
      <td>541.0</td>
      <td>0.036</td>
      <td>tests performed</td>
      <td>NaN</td>
      <td>14862927.0</td>
      <td>42.729</td>
      <td>19.6</td>
      <td>2.822</td>
      <td>1.882</td>
      <td>1899.775</td>
      <td>21.4</td>
      <td>307.846</td>
      <td>1.82</td>
      <td>1.6</td>
      <td>30.7</td>
      <td>36.791</td>
      <td>1.7</td>
    </tr>
    <tr>
      <th>19701</th>
      <td>ZWE</td>
      <td>Zimbabwe</td>
      <td>2020-05-22</td>
      <td>51</td>
      <td>3</td>
      <td>4</td>
      <td>0</td>
      <td>3.431</td>
      <td>0.202</td>
      <td>0.269</td>
      <td>0.000</td>
      <td>15194.0</td>
      <td>110.0</td>
      <td>1.022</td>
      <td>0.007</td>
      <td>542.0</td>
      <td>0.036</td>
      <td>tests performed</td>
      <td>NaN</td>
      <td>14862927.0</td>
      <td>42.729</td>
      <td>19.6</td>
      <td>2.822</td>
      <td>1.882</td>
      <td>1899.775</td>
      <td>21.4</td>
      <td>307.846</td>
      <td>1.82</td>
      <td>1.6</td>
      <td>30.7</td>
      <td>36.791</td>
      <td>1.7</td>
    </tr>
    <tr>
      <th>19702</th>
      <td>ZWE</td>
      <td>Zimbabwe</td>
      <td>2020-05-23</td>
      <td>56</td>
      <td>5</td>
      <td>4</td>
      <td>0</td>
      <td>3.768</td>
      <td>0.336</td>
      <td>0.269</td>
      <td>0.000</td>
      <td>15336.0</td>
      <td>142.0</td>
      <td>1.032</td>
      <td>0.010</td>
      <td>437.0</td>
      <td>0.029</td>
      <td>tests performed</td>
      <td>NaN</td>
      <td>14862927.0</td>
      <td>42.729</td>
      <td>19.6</td>
      <td>2.822</td>
      <td>1.882</td>
      <td>1899.775</td>
      <td>21.4</td>
      <td>307.846</td>
      <td>1.82</td>
      <td>1.6</td>
      <td>30.7</td>
      <td>36.791</td>
      <td>1.7</td>
    </tr>
    <tr>
      <th>19703</th>
      <td>ZWE</td>
      <td>Zimbabwe</td>
      <td>2020-05-24</td>
      <td>56</td>
      <td>0</td>
      <td>4</td>
      <td>0</td>
      <td>3.768</td>
      <td>0.000</td>
      <td>0.269</td>
      <td>0.000</td>
      <td>15555.0</td>
      <td>219.0</td>
      <td>1.047</td>
      <td>0.015</td>
      <td>427.0</td>
      <td>0.029</td>
      <td>tests performed</td>
      <td>NaN</td>
      <td>14862927.0</td>
      <td>42.729</td>
      <td>19.6</td>
      <td>2.822</td>
      <td>1.882</td>
      <td>1899.775</td>
      <td>21.4</td>
      <td>307.846</td>
      <td>1.82</td>
      <td>1.6</td>
      <td>30.7</td>
      <td>36.791</td>
      <td>1.7</td>
    </tr>
  </tbody>
</table>
<p>5287 rows × 32 columns</p>
</div>




```python
data[notnull_count].shape
```




    (5287, 32)




```python
data.shape
```




    (19918, 32)



### Percentage of the missing values in total tests column


```python
# Most of the values in total_tests are missing
#Percentage of the missing values total
(14421/19708)*100
```




    73.17333062715649



## A count of the missing values in each column and a visual of the same


```python
# A count of the missing values in each column and a visual of the same
print(data.isnull().sum())
data.isnull().sum().plot(kind='bar', figsize=(25,6));
```

    iso_code                              64
    location                               0
    date                                   0
    total_cases                            0
    new_cases                              0
    total_deaths                           0
    new_deaths                             0
    total_cases_per_million              377
    new_cases_per_million                377
    total_deaths_per_million             377
    new_deaths_per_million               377
    total_tests                        14631
    new_tests                          15219
    total_tests_per_thousand           14631
    new_tests_per_thousand             15219
    new_tests_smoothed                 14133
    new_tests_smoothed_per_thousand    14133
    tests_units                        13534
    stringency_index                    4365
    population                            64
    population_density                   874
    median_age                          1791
    aged_65_older                       2034
    aged_70_older                       1882
    gdp_per_capita                      2038
    extreme_poverty                     8057
    cvd_death_rate                      1865
    diabetes_prevalence                 1208
    female_smokers                      5190
    male_smokers                        5348
    handwashing_facilities             12060
    hospital_beds_per_100k              3250
    dtype: int64



![png](assets/images/covid/output_57_1.png)


## Drop columns with most  values missing


```python
# Drop columns with most missing values
data_drop = data.drop(['total_tests', 'new_tests', 'total_tests_per_thousand', 'new_tests_per_thousand', 'new_tests_smoothed', 'new_tests_smoothed_per_thousand', 'tests_units', 'handwashing_facilities'], axis=1)
```


```python
data_drop
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>iso_code</th>
      <th>location</th>
      <th>date</th>
      <th>total_cases</th>
      <th>new_cases</th>
      <th>total_deaths</th>
      <th>new_deaths</th>
      <th>total_cases_per_million</th>
      <th>new_cases_per_million</th>
      <th>total_deaths_per_million</th>
      <th>new_deaths_per_million</th>
      <th>stringency_index</th>
      <th>population</th>
      <th>population_density</th>
      <th>median_age</th>
      <th>aged_65_older</th>
      <th>aged_70_older</th>
      <th>gdp_per_capita</th>
      <th>extreme_poverty</th>
      <th>cvd_death_rate</th>
      <th>diabetes_prevalence</th>
      <th>female_smokers</th>
      <th>male_smokers</th>
      <th>hospital_beds_per_100k</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>ABW</td>
      <td>Aruba</td>
      <td>2020-03-13</td>
      <td>2</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>18.733</td>
      <td>18.733</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>106766.0</td>
      <td>584.8</td>
      <td>41.2</td>
      <td>13.085</td>
      <td>7.452</td>
      <td>35973.781</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>11.62</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>ABW</td>
      <td>Aruba</td>
      <td>2020-03-20</td>
      <td>4</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>37.465</td>
      <td>18.733</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>30.56</td>
      <td>106766.0</td>
      <td>584.8</td>
      <td>41.2</td>
      <td>13.085</td>
      <td>7.452</td>
      <td>35973.781</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>11.62</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>ABW</td>
      <td>Aruba</td>
      <td>2020-03-24</td>
      <td>12</td>
      <td>8</td>
      <td>0</td>
      <td>0</td>
      <td>112.395</td>
      <td>74.930</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>41.67</td>
      <td>106766.0</td>
      <td>584.8</td>
      <td>41.2</td>
      <td>13.085</td>
      <td>7.452</td>
      <td>35973.781</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>11.62</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>ABW</td>
      <td>Aruba</td>
      <td>2020-03-25</td>
      <td>17</td>
      <td>5</td>
      <td>0</td>
      <td>0</td>
      <td>159.227</td>
      <td>46.831</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>41.67</td>
      <td>106766.0</td>
      <td>584.8</td>
      <td>41.2</td>
      <td>13.085</td>
      <td>7.452</td>
      <td>35973.781</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>11.62</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>ABW</td>
      <td>Aruba</td>
      <td>2020-03-26</td>
      <td>19</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>177.959</td>
      <td>18.733</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>41.67</td>
      <td>106766.0</td>
      <td>584.8</td>
      <td>41.2</td>
      <td>13.085</td>
      <td>7.452</td>
      <td>35973.781</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>11.62</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>19913</th>
      <td>NaN</td>
      <td>International</td>
      <td>2020-02-28</td>
      <td>705</td>
      <td>0</td>
      <td>4</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>19914</th>
      <td>NaN</td>
      <td>International</td>
      <td>2020-02-29</td>
      <td>705</td>
      <td>0</td>
      <td>6</td>
      <td>2</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>19915</th>
      <td>NaN</td>
      <td>International</td>
      <td>2020-03-01</td>
      <td>705</td>
      <td>0</td>
      <td>6</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>19916</th>
      <td>NaN</td>
      <td>International</td>
      <td>2020-03-02</td>
      <td>705</td>
      <td>0</td>
      <td>6</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>19917</th>
      <td>NaN</td>
      <td>International</td>
      <td>2020-03-10</td>
      <td>696</td>
      <td>-9</td>
      <td>7</td>
      <td>1</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>19918 rows × 24 columns</p>
</div>



## columns with relatively few missing columns


```python
data_drop.isnull().sum()
```




    iso_code                      64
    location                       0
    date                           0
    total_cases                    0
    new_cases                      0
    total_deaths                   0
    new_deaths                     0
    total_cases_per_million      377
    new_cases_per_million        377
    total_deaths_per_million     377
    new_deaths_per_million       377
    stringency_index            4365
    population                    64
    population_density           874
    median_age                  1791
    aged_65_older               2034
    aged_70_older               1882
    gdp_per_capita              2038
    extreme_poverty             8057
    cvd_death_rate              1865
    diabetes_prevalence         1208
    female_smokers              5190
    male_smokers                5348
    hospital_beds_per_100k      3250
    dtype: int64



## A representation of Maximum values for each  columns


```python
data_drop.groupby('location').max()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>iso_code</th>
      <th>date</th>
      <th>total_cases</th>
      <th>new_cases</th>
      <th>total_deaths</th>
      <th>new_deaths</th>
      <th>total_cases_per_million</th>
      <th>new_cases_per_million</th>
      <th>total_deaths_per_million</th>
      <th>new_deaths_per_million</th>
      <th>stringency_index</th>
      <th>population</th>
      <th>population_density</th>
      <th>median_age</th>
      <th>aged_65_older</th>
      <th>aged_70_older</th>
      <th>gdp_per_capita</th>
      <th>extreme_poverty</th>
      <th>cvd_death_rate</th>
      <th>diabetes_prevalence</th>
      <th>female_smokers</th>
      <th>male_smokers</th>
      <th>hospital_beds_per_100k</th>
    </tr>
    <tr>
      <th>location</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Afghanistan</th>
      <td>AFG</td>
      <td>2020-05-26</td>
      <td>11173</td>
      <td>1063</td>
      <td>219</td>
      <td>32</td>
      <td>287.015</td>
      <td>27.307</td>
      <td>5.626</td>
      <td>0.822</td>
      <td>78.70</td>
      <td>3.892834e+07</td>
      <td>54.422</td>
      <td>18.6</td>
      <td>2.581</td>
      <td>1.337</td>
      <td>1803.987</td>
      <td>NaN</td>
      <td>597.029</td>
      <td>9.59</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.500</td>
    </tr>
    <tr>
      <th>Albania</th>
      <td>ALB</td>
      <td>2020-05-26</td>
      <td>1004</td>
      <td>34</td>
      <td>32</td>
      <td>3</td>
      <td>348.878</td>
      <td>11.815</td>
      <td>11.120</td>
      <td>1.042</td>
      <td>87.96</td>
      <td>2.877800e+06</td>
      <td>104.871</td>
      <td>38.0</td>
      <td>13.188</td>
      <td>8.643</td>
      <td>11803.431</td>
      <td>1.1</td>
      <td>304.195</td>
      <td>10.08</td>
      <td>7.100</td>
      <td>51.200</td>
      <td>2.890</td>
    </tr>
    <tr>
      <th>Algeria</th>
      <td>DZA</td>
      <td>2020-05-26</td>
      <td>8503</td>
      <td>199</td>
      <td>609</td>
      <td>42</td>
      <td>193.906</td>
      <td>4.538</td>
      <td>13.888</td>
      <td>0.958</td>
      <td>89.35</td>
      <td>4.385104e+07</td>
      <td>17.348</td>
      <td>29.1</td>
      <td>6.211</td>
      <td>3.857</td>
      <td>13913.839</td>
      <td>0.5</td>
      <td>278.364</td>
      <td>6.73</td>
      <td>0.700</td>
      <td>30.400</td>
      <td>1.900</td>
    </tr>
    <tr>
      <th>Andorra</th>
      <td>AND</td>
      <td>2020-05-26</td>
      <td>763</td>
      <td>43</td>
      <td>51</td>
      <td>4</td>
      <td>9875.105</td>
      <td>556.526</td>
      <td>660.066</td>
      <td>51.770</td>
      <td>56.48</td>
      <td>7.726500e+04</td>
      <td>163.755</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>109.135</td>
      <td>7.97</td>
      <td>29.000</td>
      <td>37.800</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Angola</th>
      <td>AGO</td>
      <td>2020-05-26</td>
      <td>69</td>
      <td>9</td>
      <td>4</td>
      <td>2</td>
      <td>2.099</td>
      <td>0.274</td>
      <td>0.122</td>
      <td>0.061</td>
      <td>90.74</td>
      <td>3.286627e+07</td>
      <td>23.890</td>
      <td>16.8</td>
      <td>2.405</td>
      <td>1.362</td>
      <td>5819.495</td>
      <td>NaN</td>
      <td>276.045</td>
      <td>3.94</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Anguilla</th>
      <td>AIA</td>
      <td>2020-05-26</td>
      <td>3</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>199.973</td>
      <td>133.316</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>NaN</td>
      <td>1.500200e+04</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Antigua and Barbuda</th>
      <td>ATG</td>
      <td>2020-05-26</td>
      <td>25</td>
      <td>6</td>
      <td>3</td>
      <td>2</td>
      <td>255.290</td>
      <td>61.270</td>
      <td>30.635</td>
      <td>20.423</td>
      <td>NaN</td>
      <td>9.792800e+04</td>
      <td>231.845</td>
      <td>32.1</td>
      <td>6.933</td>
      <td>4.631</td>
      <td>21490.943</td>
      <td>NaN</td>
      <td>191.511</td>
      <td>13.17</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>3.800</td>
    </tr>
    <tr>
      <th>Argentina</th>
      <td>ARG</td>
      <td>2020-05-26</td>
      <td>12615</td>
      <td>723</td>
      <td>467</td>
      <td>24</td>
      <td>279.119</td>
      <td>15.997</td>
      <td>10.333</td>
      <td>0.531</td>
      <td>100.00</td>
      <td>4.519578e+07</td>
      <td>16.177</td>
      <td>31.9</td>
      <td>11.198</td>
      <td>7.441</td>
      <td>18933.907</td>
      <td>0.6</td>
      <td>191.032</td>
      <td>5.50</td>
      <td>16.200</td>
      <td>27.700</td>
      <td>5.000</td>
    </tr>
    <tr>
      <th>Armenia</th>
      <td>ARM</td>
      <td>2020-05-26</td>
      <td>7113</td>
      <td>452</td>
      <td>87</td>
      <td>6</td>
      <td>2400.418</td>
      <td>152.536</td>
      <td>29.360</td>
      <td>2.025</td>
      <td>NaN</td>
      <td>2.963234e+06</td>
      <td>102.931</td>
      <td>35.7</td>
      <td>11.232</td>
      <td>7.571</td>
      <td>8787.580</td>
      <td>1.8</td>
      <td>341.010</td>
      <td>7.11</td>
      <td>1.500</td>
      <td>52.100</td>
      <td>4.200</td>
    </tr>
    <tr>
      <th>Aruba</th>
      <td>ABW</td>
      <td>2020-05-26</td>
      <td>101</td>
      <td>22</td>
      <td>3</td>
      <td>1</td>
      <td>945.994</td>
      <td>206.058</td>
      <td>28.099</td>
      <td>9.366</td>
      <td>86.11</td>
      <td>1.067660e+05</td>
      <td>584.800</td>
      <td>41.2</td>
      <td>13.085</td>
      <td>7.452</td>
      <td>35973.781</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>11.62</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Australia</th>
      <td>AUS</td>
      <td>2020-05-26</td>
      <td>7118</td>
      <td>611</td>
      <td>102</td>
      <td>7</td>
      <td>279.139</td>
      <td>23.961</td>
      <td>4.000</td>
      <td>0.275</td>
      <td>73.15</td>
      <td>2.549988e+07</td>
      <td>3.202</td>
      <td>37.9</td>
      <td>15.504</td>
      <td>10.129</td>
      <td>44648.710</td>
      <td>0.5</td>
      <td>107.791</td>
      <td>5.07</td>
      <td>13.000</td>
      <td>16.500</td>
      <td>3.840</td>
    </tr>
    <tr>
      <th>Austria</th>
      <td>AUT</td>
      <td>2020-05-26</td>
      <td>16459</td>
      <td>1141</td>
      <td>641</td>
      <td>31</td>
      <td>1827.478</td>
      <td>126.688</td>
      <td>71.172</td>
      <td>3.442</td>
      <td>81.48</td>
      <td>9.006400e+06</td>
      <td>106.749</td>
      <td>44.4</td>
      <td>19.202</td>
      <td>13.748</td>
      <td>45436.686</td>
      <td>0.7</td>
      <td>145.183</td>
      <td>6.35</td>
      <td>28.400</td>
      <td>30.900</td>
      <td>7.370</td>
    </tr>
    <tr>
      <th>Azerbaijan</th>
      <td>AZE</td>
      <td>2020-05-26</td>
      <td>4271</td>
      <td>231</td>
      <td>51</td>
      <td>3</td>
      <td>421.237</td>
      <td>22.783</td>
      <td>5.030</td>
      <td>0.296</td>
      <td>91.67</td>
      <td>1.013918e+07</td>
      <td>119.309</td>
      <td>32.4</td>
      <td>6.018</td>
      <td>3.871</td>
      <td>15847.419</td>
      <td>NaN</td>
      <td>559.812</td>
      <td>7.11</td>
      <td>0.300</td>
      <td>42.500</td>
      <td>4.700</td>
    </tr>
    <tr>
      <th>Bahamas</th>
      <td>BHS</td>
      <td>2020-05-26</td>
      <td>100</td>
      <td>6</td>
      <td>11</td>
      <td>2</td>
      <td>254.292</td>
      <td>15.258</td>
      <td>27.972</td>
      <td>5.086</td>
      <td>NaN</td>
      <td>3.932480e+05</td>
      <td>39.497</td>
      <td>34.3</td>
      <td>8.996</td>
      <td>5.200</td>
      <td>27717.847</td>
      <td>NaN</td>
      <td>235.954</td>
      <td>13.17</td>
      <td>3.100</td>
      <td>20.400</td>
      <td>2.900</td>
    </tr>
    <tr>
      <th>Bahrain</th>
      <td>BHR</td>
      <td>2020-05-26</td>
      <td>9171</td>
      <td>388</td>
      <td>14</td>
      <td>2</td>
      <td>5389.687</td>
      <td>228.023</td>
      <td>8.228</td>
      <td>1.175</td>
      <td>81.48</td>
      <td>1.701583e+06</td>
      <td>1935.907</td>
      <td>32.4</td>
      <td>2.372</td>
      <td>1.387</td>
      <td>43290.705</td>
      <td>NaN</td>
      <td>151.689</td>
      <td>16.52</td>
      <td>5.800</td>
      <td>37.600</td>
      <td>2.000</td>
    </tr>
    <tr>
      <th>Bangladesh</th>
      <td>BGD</td>
      <td>2020-05-26</td>
      <td>35585</td>
      <td>1975</td>
      <td>501</td>
      <td>28</td>
      <td>216.073</td>
      <td>11.992</td>
      <td>3.042</td>
      <td>0.170</td>
      <td>93.52</td>
      <td>1.646894e+08</td>
      <td>1265.036</td>
      <td>27.5</td>
      <td>5.098</td>
      <td>3.262</td>
      <td>3523.984</td>
      <td>14.8</td>
      <td>298.003</td>
      <td>8.38</td>
      <td>1.000</td>
      <td>44.700</td>
      <td>0.800</td>
    </tr>
    <tr>
      <th>Barbados</th>
      <td>BRB</td>
      <td>2020-05-26</td>
      <td>92</td>
      <td>11</td>
      <td>7</td>
      <td>1</td>
      <td>320.144</td>
      <td>38.278</td>
      <td>24.359</td>
      <td>3.480</td>
      <td>88.89</td>
      <td>2.873710e+05</td>
      <td>664.463</td>
      <td>39.8</td>
      <td>14.952</td>
      <td>9.473</td>
      <td>16978.068</td>
      <td>NaN</td>
      <td>170.050</td>
      <td>13.57</td>
      <td>1.900</td>
      <td>14.500</td>
      <td>5.800</td>
    </tr>
    <tr>
      <th>Belarus</th>
      <td>BLR</td>
      <td>2020-05-26</td>
      <td>37144</td>
      <td>1485</td>
      <td>204</td>
      <td>7</td>
      <td>3930.864</td>
      <td>157.154</td>
      <td>21.589</td>
      <td>0.741</td>
      <td>19.44</td>
      <td>9.449321e+06</td>
      <td>46.858</td>
      <td>40.3</td>
      <td>14.799</td>
      <td>9.788</td>
      <td>17167.967</td>
      <td>NaN</td>
      <td>443.129</td>
      <td>5.18</td>
      <td>10.500</td>
      <td>46.100</td>
      <td>11.000</td>
    </tr>
    <tr>
      <th>Belgium</th>
      <td>BEL</td>
      <td>2020-05-26</td>
      <td>57342</td>
      <td>2454</td>
      <td>9312</td>
      <td>496</td>
      <td>4947.705</td>
      <td>211.741</td>
      <td>803.478</td>
      <td>42.797</td>
      <td>81.48</td>
      <td>1.158962e+07</td>
      <td>375.564</td>
      <td>41.8</td>
      <td>18.571</td>
      <td>12.849</td>
      <td>42658.576</td>
      <td>0.2</td>
      <td>114.898</td>
      <td>4.29</td>
      <td>25.100</td>
      <td>31.400</td>
      <td>5.640</td>
    </tr>
    <tr>
      <th>Belize</th>
      <td>BLZ</td>
      <td>2020-05-26</td>
      <td>18</td>
      <td>4</td>
      <td>2</td>
      <td>1</td>
      <td>45.269</td>
      <td>10.060</td>
      <td>5.030</td>
      <td>2.515</td>
      <td>86.11</td>
      <td>3.976210e+05</td>
      <td>16.426</td>
      <td>25.0</td>
      <td>3.853</td>
      <td>2.279</td>
      <td>7824.362</td>
      <td>NaN</td>
      <td>176.957</td>
      <td>17.11</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.300</td>
    </tr>
    <tr>
      <th>Benin</th>
      <td>BEN</td>
      <td>2020-05-26</td>
      <td>339</td>
      <td>102</td>
      <td>3</td>
      <td>1</td>
      <td>27.963</td>
      <td>8.414</td>
      <td>0.247</td>
      <td>0.082</td>
      <td>59.72</td>
      <td>1.212320e+07</td>
      <td>99.110</td>
      <td>18.8</td>
      <td>3.244</td>
      <td>1.942</td>
      <td>2064.236</td>
      <td>49.6</td>
      <td>235.848</td>
      <td>0.99</td>
      <td>0.600</td>
      <td>12.300</td>
      <td>0.500</td>
    </tr>
    <tr>
      <th>Bermuda</th>
      <td>BMU</td>
      <td>2020-05-26</td>
      <td>133</td>
      <td>24</td>
      <td>9</td>
      <td>2</td>
      <td>2135.757</td>
      <td>385.400</td>
      <td>144.525</td>
      <td>32.117</td>
      <td>96.30</td>
      <td>6.227300e+04</td>
      <td>1308.820</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>50669.315</td>
      <td>NaN</td>
      <td>139.547</td>
      <td>13.00</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Bhutan</th>
      <td>BTN</td>
      <td>2020-05-26</td>
      <td>27</td>
      <td>5</td>
      <td>0</td>
      <td>0</td>
      <td>34.992</td>
      <td>6.480</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>74.07</td>
      <td>7.716120e+05</td>
      <td>21.188</td>
      <td>28.6</td>
      <td>4.885</td>
      <td>2.977</td>
      <td>8708.597</td>
      <td>1.5</td>
      <td>217.066</td>
      <td>9.75</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.700</td>
    </tr>
    <tr>
      <th>Bolivia</th>
      <td>BOL</td>
      <td>2020-05-26</td>
      <td>6660</td>
      <td>438</td>
      <td>261</td>
      <td>16</td>
      <td>570.546</td>
      <td>37.522</td>
      <td>22.359</td>
      <td>1.371</td>
      <td>96.30</td>
      <td>1.167303e+07</td>
      <td>10.202</td>
      <td>25.4</td>
      <td>6.704</td>
      <td>4.393</td>
      <td>6885.829</td>
      <td>7.1</td>
      <td>204.299</td>
      <td>6.89</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.100</td>
    </tr>
    <tr>
      <th>Bonaire Sint Eustatius and Saba</th>
      <td>BES</td>
      <td>2020-05-26</td>
      <td>7</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>266.962</td>
      <td>76.275</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>NaN</td>
      <td>2.622100e+04</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Bosnia and Herzegovina</th>
      <td>BIH</td>
      <td>2020-05-26</td>
      <td>2406</td>
      <td>101</td>
      <td>146</td>
      <td>10</td>
      <td>733.354</td>
      <td>30.785</td>
      <td>44.501</td>
      <td>3.048</td>
      <td>92.59</td>
      <td>3.280815e+06</td>
      <td>68.496</td>
      <td>42.5</td>
      <td>16.569</td>
      <td>10.711</td>
      <td>11713.895</td>
      <td>0.2</td>
      <td>329.635</td>
      <td>10.08</td>
      <td>30.200</td>
      <td>47.700</td>
      <td>3.500</td>
    </tr>
    <tr>
      <th>Botswana</th>
      <td>BWA</td>
      <td>2020-05-26</td>
      <td>35</td>
      <td>6</td>
      <td>1</td>
      <td>1</td>
      <td>14.883</td>
      <td>2.551</td>
      <td>0.425</td>
      <td>0.425</td>
      <td>86.11</td>
      <td>2.351625e+06</td>
      <td>4.044</td>
      <td>25.8</td>
      <td>3.941</td>
      <td>2.242</td>
      <td>15807.374</td>
      <td>NaN</td>
      <td>237.372</td>
      <td>4.81</td>
      <td>5.700</td>
      <td>34.400</td>
      <td>1.800</td>
    </tr>
    <tr>
      <th>Brazil</th>
      <td>BRA</td>
      <td>2020-05-26</td>
      <td>374898</td>
      <td>20803</td>
      <td>23473</td>
      <td>1188</td>
      <td>1763.733</td>
      <td>97.869</td>
      <td>110.430</td>
      <td>5.589</td>
      <td>81.02</td>
      <td>2.125594e+08</td>
      <td>25.040</td>
      <td>33.5</td>
      <td>8.552</td>
      <td>5.060</td>
      <td>14103.452</td>
      <td>3.4</td>
      <td>177.961</td>
      <td>8.11</td>
      <td>10.100</td>
      <td>17.900</td>
      <td>2.200</td>
    </tr>
    <tr>
      <th>British Virgin Islands</th>
      <td>VGB</td>
      <td>2020-05-26</td>
      <td>8</td>
      <td>2</td>
      <td>1</td>
      <td>1</td>
      <td>264.577</td>
      <td>66.144</td>
      <td>33.072</td>
      <td>33.072</td>
      <td>NaN</td>
      <td>3.023700e+04</td>
      <td>207.973</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>13.67</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Brunei</th>
      <td>BRN</td>
      <td>2020-05-26</td>
      <td>141</td>
      <td>14</td>
      <td>1</td>
      <td>1</td>
      <td>322.298</td>
      <td>32.001</td>
      <td>2.286</td>
      <td>2.286</td>
      <td>58.33</td>
      <td>4.374830e+05</td>
      <td>81.347</td>
      <td>32.4</td>
      <td>4.591</td>
      <td>2.382</td>
      <td>71809.251</td>
      <td>NaN</td>
      <td>201.285</td>
      <td>12.79</td>
      <td>2.000</td>
      <td>30.900</td>
      <td>2.700</td>
    </tr>
    <tr>
      <th>Bulgaria</th>
      <td>BGR</td>
      <td>2020-05-26</td>
      <td>2433</td>
      <td>91</td>
      <td>130</td>
      <td>6</td>
      <td>350.150</td>
      <td>13.096</td>
      <td>18.709</td>
      <td>0.864</td>
      <td>73.15</td>
      <td>6.948445e+06</td>
      <td>65.180</td>
      <td>44.7</td>
      <td>20.801</td>
      <td>13.272</td>
      <td>18563.307</td>
      <td>1.5</td>
      <td>424.688</td>
      <td>5.81</td>
      <td>30.100</td>
      <td>44.400</td>
      <td>7.454</td>
    </tr>
    <tr>
      <th>Burkina Faso</th>
      <td>BFA</td>
      <td>2020-05-26</td>
      <td>841</td>
      <td>43</td>
      <td>52</td>
      <td>6</td>
      <td>40.233</td>
      <td>2.057</td>
      <td>2.488</td>
      <td>0.287</td>
      <td>89.81</td>
      <td>2.090328e+07</td>
      <td>70.151</td>
      <td>17.6</td>
      <td>2.409</td>
      <td>1.358</td>
      <td>1703.102</td>
      <td>43.7</td>
      <td>269.048</td>
      <td>2.42</td>
      <td>1.600</td>
      <td>23.900</td>
      <td>0.400</td>
    </tr>
    <tr>
      <th>Burundi</th>
      <td>BDI</td>
      <td>2020-05-26</td>
      <td>42</td>
      <td>15</td>
      <td>1</td>
      <td>1</td>
      <td>3.532</td>
      <td>1.261</td>
      <td>0.084</td>
      <td>0.084</td>
      <td>22.22</td>
      <td>1.189078e+07</td>
      <td>423.062</td>
      <td>17.5</td>
      <td>2.562</td>
      <td>1.504</td>
      <td>702.225</td>
      <td>71.7</td>
      <td>293.068</td>
      <td>6.05</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.800</td>
    </tr>
    <tr>
      <th>Cambodia</th>
      <td>KHM</td>
      <td>2020-05-26</td>
      <td>124</td>
      <td>35</td>
      <td>0</td>
      <td>0</td>
      <td>7.417</td>
      <td>2.093</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>NaN</td>
      <td>1.671897e+07</td>
      <td>90.672</td>
      <td>25.6</td>
      <td>4.412</td>
      <td>2.385</td>
      <td>3645.070</td>
      <td>NaN</td>
      <td>270.892</td>
      <td>4.00</td>
      <td>2.000</td>
      <td>33.700</td>
      <td>0.800</td>
    </tr>
    <tr>
      <th>Cameroon</th>
      <td>CMR</td>
      <td>2020-05-26</td>
      <td>5044</td>
      <td>555</td>
      <td>171</td>
      <td>44</td>
      <td>190.011</td>
      <td>20.907</td>
      <td>6.442</td>
      <td>1.658</td>
      <td>71.30</td>
      <td>2.654586e+07</td>
      <td>50.885</td>
      <td>18.8</td>
      <td>3.165</td>
      <td>1.919</td>
      <td>3364.926</td>
      <td>23.8</td>
      <td>244.661</td>
      <td>7.20</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.300</td>
    </tr>
    <tr>
      <th>Canada</th>
      <td>CAN</td>
      <td>2020-05-26</td>
      <td>85700</td>
      <td>2760</td>
      <td>6545</td>
      <td>207</td>
      <td>2270.670</td>
      <td>73.128</td>
      <td>173.414</td>
      <td>5.485</td>
      <td>74.54</td>
      <td>3.774216e+07</td>
      <td>4.037</td>
      <td>41.4</td>
      <td>16.984</td>
      <td>10.797</td>
      <td>44017.591</td>
      <td>0.5</td>
      <td>105.599</td>
      <td>7.37</td>
      <td>12.000</td>
      <td>16.600</td>
      <td>2.500</td>
    </tr>
    <tr>
      <th>Cape Verde</th>
      <td>CPV</td>
      <td>2020-05-26</td>
      <td>390</td>
      <td>44</td>
      <td>3</td>
      <td>1</td>
      <td>701.454</td>
      <td>79.138</td>
      <td>5.396</td>
      <td>1.799</td>
      <td>84.26</td>
      <td>5.559880e+05</td>
      <td>135.580</td>
      <td>25.7</td>
      <td>4.460</td>
      <td>3.437</td>
      <td>6222.554</td>
      <td>NaN</td>
      <td>182.219</td>
      <td>2.42</td>
      <td>2.100</td>
      <td>16.500</td>
      <td>2.100</td>
    </tr>
    <tr>
      <th>Cayman Islands</th>
      <td>CYM</td>
      <td>2020-05-26</td>
      <td>134</td>
      <td>17</td>
      <td>1</td>
      <td>1</td>
      <td>2038.953</td>
      <td>258.673</td>
      <td>15.216</td>
      <td>15.216</td>
      <td>NaN</td>
      <td>6.572000e+04</td>
      <td>256.496</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>49903.029</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>13.22</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Central African Republic</th>
      <td>CAF</td>
      <td>2020-05-26</td>
      <td>652</td>
      <td>80</td>
      <td>1</td>
      <td>1</td>
      <td>134.996</td>
      <td>16.564</td>
      <td>0.207</td>
      <td>0.207</td>
      <td>68.52</td>
      <td>4.829764e+06</td>
      <td>7.479</td>
      <td>18.3</td>
      <td>3.655</td>
      <td>2.251</td>
      <td>661.240</td>
      <td>NaN</td>
      <td>435.727</td>
      <td>6.10</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>Chad</th>
      <td>TCD</td>
      <td>2020-05-26</td>
      <td>687</td>
      <td>83</td>
      <td>61</td>
      <td>10</td>
      <td>41.824</td>
      <td>5.053</td>
      <td>3.714</td>
      <td>0.609</td>
      <td>88.89</td>
      <td>1.642586e+07</td>
      <td>11.833</td>
      <td>16.7</td>
      <td>2.486</td>
      <td>1.446</td>
      <td>1768.153</td>
      <td>38.4</td>
      <td>280.995</td>
      <td>6.10</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Chile</th>
      <td>CHL</td>
      <td>2020-05-26</td>
      <td>73997</td>
      <td>4895</td>
      <td>761</td>
      <td>45</td>
      <td>3870.903</td>
      <td>256.065</td>
      <td>39.809</td>
      <td>2.354</td>
      <td>75.93</td>
      <td>1.911621e+07</td>
      <td>24.282</td>
      <td>35.4</td>
      <td>11.087</td>
      <td>6.938</td>
      <td>22767.037</td>
      <td>1.3</td>
      <td>127.993</td>
      <td>8.46</td>
      <td>34.200</td>
      <td>41.500</td>
      <td>2.110</td>
    </tr>
    <tr>
      <th>China</th>
      <td>CHN</td>
      <td>2020-05-26</td>
      <td>84102</td>
      <td>15141</td>
      <td>4638</td>
      <td>1290</td>
      <td>58.432</td>
      <td>10.520</td>
      <td>3.222</td>
      <td>0.896</td>
      <td>81.94</td>
      <td>1.439324e+09</td>
      <td>147.674</td>
      <td>38.7</td>
      <td>10.641</td>
      <td>5.929</td>
      <td>15308.712</td>
      <td>0.7</td>
      <td>261.899</td>
      <td>9.74</td>
      <td>1.900</td>
      <td>48.400</td>
      <td>4.340</td>
    </tr>
    <tr>
      <th>Colombia</th>
      <td>COL</td>
      <td>2020-05-26</td>
      <td>21981</td>
      <td>1046</td>
      <td>750</td>
      <td>30</td>
      <td>431.992</td>
      <td>20.557</td>
      <td>14.740</td>
      <td>0.590</td>
      <td>90.74</td>
      <td>5.088288e+07</td>
      <td>44.223</td>
      <td>32.2</td>
      <td>7.646</td>
      <td>4.312</td>
      <td>13254.949</td>
      <td>4.5</td>
      <td>124.240</td>
      <td>7.44</td>
      <td>4.700</td>
      <td>13.500</td>
      <td>1.710</td>
    </tr>
    <tr>
      <th>Comoros</th>
      <td>COM</td>
      <td>2020-05-26</td>
      <td>87</td>
      <td>44</td>
      <td>1</td>
      <td>1</td>
      <td>100.047</td>
      <td>50.598</td>
      <td>1.150</td>
      <td>1.150</td>
      <td>NaN</td>
      <td>8.695950e+05</td>
      <td>437.352</td>
      <td>20.4</td>
      <td>2.963</td>
      <td>1.726</td>
      <td>1413.890</td>
      <td>18.1</td>
      <td>261.516</td>
      <td>11.88</td>
      <td>4.400</td>
      <td>23.600</td>
      <td>2.200</td>
    </tr>
    <tr>
      <th>Congo</th>
      <td>COG</td>
      <td>2020-05-26</td>
      <td>531</td>
      <td>50</td>
      <td>17</td>
      <td>4</td>
      <td>96.229</td>
      <td>9.061</td>
      <td>3.081</td>
      <td>0.725</td>
      <td>97.22</td>
      <td>5.518092e+06</td>
      <td>15.405</td>
      <td>19.0</td>
      <td>3.402</td>
      <td>2.063</td>
      <td>4881.406</td>
      <td>37.0</td>
      <td>344.094</td>
      <td>7.20</td>
      <td>1.700</td>
      <td>52.300</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Costa Rica</th>
      <td>CRI</td>
      <td>2020-05-26</td>
      <td>951</td>
      <td>37</td>
      <td>10</td>
      <td>2</td>
      <td>186.686</td>
      <td>7.263</td>
      <td>1.963</td>
      <td>0.393</td>
      <td>84.26</td>
      <td>5.094114e+06</td>
      <td>96.079</td>
      <td>33.6</td>
      <td>9.468</td>
      <td>5.694</td>
      <td>15524.995</td>
      <td>1.3</td>
      <td>137.973</td>
      <td>8.78</td>
      <td>6.400</td>
      <td>17.400</td>
      <td>1.130</td>
    </tr>
    <tr>
      <th>Cote d'Ivoire</th>
      <td>CIV</td>
      <td>2020-05-26</td>
      <td>2423</td>
      <td>127</td>
      <td>30</td>
      <td>3</td>
      <td>91.856</td>
      <td>4.815</td>
      <td>1.137</td>
      <td>0.114</td>
      <td>80.56</td>
      <td>2.637828e+07</td>
      <td>76.399</td>
      <td>18.7</td>
      <td>2.933</td>
      <td>1.582</td>
      <td>3601.006</td>
      <td>28.2</td>
      <td>303.740</td>
      <td>2.42</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Croatia</th>
      <td>HRV</td>
      <td>2020-05-26</td>
      <td>2244</td>
      <td>96</td>
      <td>100</td>
      <td>8</td>
      <td>546.615</td>
      <td>23.385</td>
      <td>24.359</td>
      <td>1.949</td>
      <td>96.30</td>
      <td>4.105268e+06</td>
      <td>73.726</td>
      <td>44.0</td>
      <td>19.724</td>
      <td>13.053</td>
      <td>22669.797</td>
      <td>0.7</td>
      <td>253.782</td>
      <td>5.59</td>
      <td>34.300</td>
      <td>39.900</td>
      <td>5.540</td>
    </tr>
    <tr>
      <th>Cuba</th>
      <td>CUB</td>
      <td>2020-05-26</td>
      <td>1947</td>
      <td>74</td>
      <td>82</td>
      <td>6</td>
      <td>171.896</td>
      <td>6.533</td>
      <td>7.240</td>
      <td>0.530</td>
      <td>100.00</td>
      <td>1.132662e+07</td>
      <td>110.408</td>
      <td>43.1</td>
      <td>14.738</td>
      <td>9.719</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>190.968</td>
      <td>8.27</td>
      <td>17.100</td>
      <td>53.300</td>
      <td>5.200</td>
    </tr>
    <tr>
      <th>Curacao</th>
      <td>CUW</td>
      <td>2020-05-26</td>
      <td>18</td>
      <td>3</td>
      <td>1</td>
      <td>1</td>
      <td>109.689</td>
      <td>18.282</td>
      <td>6.094</td>
      <td>6.094</td>
      <td>NaN</td>
      <td>1.641000e+05</td>
      <td>362.644</td>
      <td>41.7</td>
      <td>16.367</td>
      <td>10.068</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>11.62</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Cyprus</th>
      <td>CYP</td>
      <td>2020-05-26</td>
      <td>937</td>
      <td>58</td>
      <td>17</td>
      <td>3</td>
      <td>1069.758</td>
      <td>66.218</td>
      <td>19.409</td>
      <td>3.425</td>
      <td>94.44</td>
      <td>8.758990e+05</td>
      <td>127.657</td>
      <td>37.3</td>
      <td>13.416</td>
      <td>8.563</td>
      <td>32415.132</td>
      <td>NaN</td>
      <td>141.171</td>
      <td>9.24</td>
      <td>19.600</td>
      <td>52.700</td>
      <td>3.400</td>
    </tr>
    <tr>
      <th>Czech Republic</th>
      <td>CZE</td>
      <td>2020-05-26</td>
      <td>9002</td>
      <td>408</td>
      <td>317</td>
      <td>18</td>
      <td>840.603</td>
      <td>38.099</td>
      <td>29.601</td>
      <td>1.681</td>
      <td>82.41</td>
      <td>1.070898e+07</td>
      <td>137.176</td>
      <td>43.3</td>
      <td>19.027</td>
      <td>11.580</td>
      <td>32605.906</td>
      <td>NaN</td>
      <td>227.485</td>
      <td>6.82</td>
      <td>30.500</td>
      <td>38.300</td>
      <td>6.630</td>
    </tr>
    <tr>
      <th>Democratic Republic of Congo</th>
      <td>COD</td>
      <td>2020-05-26</td>
      <td>2297</td>
      <td>175</td>
      <td>67</td>
      <td>10</td>
      <td>25.647</td>
      <td>1.954</td>
      <td>0.748</td>
      <td>0.112</td>
      <td>80.56</td>
      <td>8.956140e+07</td>
      <td>35.879</td>
      <td>17.0</td>
      <td>3.020</td>
      <td>1.745</td>
      <td>808.133</td>
      <td>77.1</td>
      <td>318.949</td>
      <td>6.10</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Denmark</th>
      <td>DNK</td>
      <td>2020-05-26</td>
      <td>11387</td>
      <td>390</td>
      <td>563</td>
      <td>22</td>
      <td>1965.919</td>
      <td>67.332</td>
      <td>97.200</td>
      <td>3.798</td>
      <td>77.78</td>
      <td>5.792203e+06</td>
      <td>136.520</td>
      <td>42.3</td>
      <td>19.677</td>
      <td>12.325</td>
      <td>46682.515</td>
      <td>0.2</td>
      <td>114.767</td>
      <td>6.41</td>
      <td>19.300</td>
      <td>18.800</td>
      <td>2.500</td>
    </tr>
    <tr>
      <th>Djibouti</th>
      <td>DJI</td>
      <td>2020-05-26</td>
      <td>2468</td>
      <td>310</td>
      <td>14</td>
      <td>4</td>
      <td>2497.971</td>
      <td>313.765</td>
      <td>14.170</td>
      <td>4.049</td>
      <td>100.00</td>
      <td>9.880020e+05</td>
      <td>41.285</td>
      <td>25.4</td>
      <td>4.213</td>
      <td>2.380</td>
      <td>2705.406</td>
      <td>22.5</td>
      <td>258.037</td>
      <td>6.05</td>
      <td>1.700</td>
      <td>24.500</td>
      <td>1.400</td>
    </tr>
    <tr>
      <th>Dominica</th>
      <td>DMA</td>
      <td>2020-05-26</td>
      <td>16</td>
      <td>5</td>
      <td>0</td>
      <td>0</td>
      <td>222.250</td>
      <td>69.453</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>85.19</td>
      <td>7.199100e+04</td>
      <td>98.567</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>9673.367</td>
      <td>NaN</td>
      <td>227.376</td>
      <td>11.62</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>3.800</td>
    </tr>
    <tr>
      <th>Dominican Republic</th>
      <td>DOM</td>
      <td>2020-05-26</td>
      <td>15073</td>
      <td>651</td>
      <td>460</td>
      <td>38</td>
      <td>1389.485</td>
      <td>60.012</td>
      <td>42.405</td>
      <td>3.503</td>
      <td>97.22</td>
      <td>1.084790e+07</td>
      <td>222.873</td>
      <td>27.6</td>
      <td>6.981</td>
      <td>4.419</td>
      <td>14600.861</td>
      <td>1.6</td>
      <td>266.653</td>
      <td>8.20</td>
      <td>8.500</td>
      <td>19.100</td>
      <td>1.600</td>
    </tr>
    <tr>
      <th>Ecuador</th>
      <td>ECU</td>
      <td>2020-05-26</td>
      <td>37355</td>
      <td>11536</td>
      <td>3203</td>
      <td>410</td>
      <td>2117.263</td>
      <td>653.855</td>
      <td>181.544</td>
      <td>23.239</td>
      <td>93.52</td>
      <td>1.764306e+07</td>
      <td>66.939</td>
      <td>28.1</td>
      <td>7.104</td>
      <td>4.458</td>
      <td>10581.936</td>
      <td>3.6</td>
      <td>140.448</td>
      <td>5.55</td>
      <td>2.000</td>
      <td>12.300</td>
      <td>1.500</td>
    </tr>
    <tr>
      <th>Egypt</th>
      <td>EGY</td>
      <td>2020-05-26</td>
      <td>17967</td>
      <td>827</td>
      <td>783</td>
      <td>30</td>
      <td>175.571</td>
      <td>8.081</td>
      <td>7.651</td>
      <td>0.293</td>
      <td>84.26</td>
      <td>1.023344e+08</td>
      <td>97.999</td>
      <td>25.3</td>
      <td>5.159</td>
      <td>2.891</td>
      <td>10550.206</td>
      <td>1.3</td>
      <td>525.432</td>
      <td>17.31</td>
      <td>0.200</td>
      <td>50.100</td>
      <td>1.600</td>
    </tr>
    <tr>
      <th>El Salvador</th>
      <td>SLV</td>
      <td>2020-05-26</td>
      <td>1983</td>
      <td>109</td>
      <td>36</td>
      <td>4</td>
      <td>305.726</td>
      <td>16.805</td>
      <td>5.550</td>
      <td>0.617</td>
      <td>100.00</td>
      <td>6.486201e+06</td>
      <td>307.811</td>
      <td>27.6</td>
      <td>8.273</td>
      <td>5.417</td>
      <td>7292.458</td>
      <td>2.2</td>
      <td>167.295</td>
      <td>8.87</td>
      <td>2.500</td>
      <td>18.800</td>
      <td>1.300</td>
    </tr>
    <tr>
      <th>Equatorial Guinea</th>
      <td>GNQ</td>
      <td>2020-05-26</td>
      <td>1043</td>
      <td>171</td>
      <td>12</td>
      <td>3</td>
      <td>743.415</td>
      <td>121.883</td>
      <td>8.553</td>
      <td>2.138</td>
      <td>NaN</td>
      <td>1.402985e+06</td>
      <td>45.194</td>
      <td>22.4</td>
      <td>2.846</td>
      <td>1.752</td>
      <td>22604.873</td>
      <td>NaN</td>
      <td>202.812</td>
      <td>7.78</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2.100</td>
    </tr>
    <tr>
      <th>Eritrea</th>
      <td>ERI</td>
      <td>2020-05-26</td>
      <td>39</td>
      <td>7</td>
      <td>0</td>
      <td>0</td>
      <td>10.997</td>
      <td>1.974</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>NaN</td>
      <td>3.546427e+06</td>
      <td>44.304</td>
      <td>19.3</td>
      <td>3.607</td>
      <td>2.171</td>
      <td>1510.459</td>
      <td>NaN</td>
      <td>311.110</td>
      <td>6.05</td>
      <td>0.200</td>
      <td>11.400</td>
      <td>0.700</td>
    </tr>
    <tr>
      <th>Estonia</th>
      <td>EST</td>
      <td>2020-05-26</td>
      <td>1824</td>
      <td>134</td>
      <td>65</td>
      <td>6</td>
      <td>1375.007</td>
      <td>101.015</td>
      <td>49.000</td>
      <td>4.523</td>
      <td>80.56</td>
      <td>1.326539e+06</td>
      <td>31.033</td>
      <td>42.7</td>
      <td>19.452</td>
      <td>13.491</td>
      <td>29481.252</td>
      <td>0.5</td>
      <td>255.569</td>
      <td>4.02</td>
      <td>24.500</td>
      <td>39.300</td>
      <td>4.690</td>
    </tr>
    <tr>
      <th>Ethiopia</th>
      <td>ETH</td>
      <td>2020-05-26</td>
      <td>655</td>
      <td>88</td>
      <td>5</td>
      <td>2</td>
      <td>5.697</td>
      <td>0.765</td>
      <td>0.043</td>
      <td>0.017</td>
      <td>73.15</td>
      <td>1.149636e+08</td>
      <td>104.957</td>
      <td>19.8</td>
      <td>3.526</td>
      <td>2.063</td>
      <td>1729.927</td>
      <td>26.7</td>
      <td>182.634</td>
      <td>7.47</td>
      <td>0.400</td>
      <td>8.500</td>
      <td>0.300</td>
    </tr>
    <tr>
      <th>Faeroe Islands</th>
      <td>FRO</td>
      <td>2020-05-26</td>
      <td>187</td>
      <td>72</td>
      <td>0</td>
      <td>0</td>
      <td>3826.870</td>
      <td>1473.447</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>NaN</td>
      <td>4.886500e+04</td>
      <td>35.308</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Falkland Islands</th>
      <td>FLK</td>
      <td>2020-05-26</td>
      <td>13</td>
      <td>6</td>
      <td>0</td>
      <td>0</td>
      <td>3732.415</td>
      <td>1722.653</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>NaN</td>
      <td>3.483000e+03</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Fiji</th>
      <td>FJI</td>
      <td>2020-05-26</td>
      <td>18</td>
      <td>5</td>
      <td>0</td>
      <td>0</td>
      <td>20.079</td>
      <td>5.578</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>NaN</td>
      <td>8.964440e+05</td>
      <td>49.562</td>
      <td>28.6</td>
      <td>6.224</td>
      <td>3.284</td>
      <td>8702.975</td>
      <td>1.4</td>
      <td>412.820</td>
      <td>14.49</td>
      <td>10.200</td>
      <td>34.800</td>
      <td>2.300</td>
    </tr>
    <tr>
      <th>Finland</th>
      <td>FIN</td>
      <td>2020-05-26</td>
      <td>6599</td>
      <td>267</td>
      <td>308</td>
      <td>43</td>
      <td>1191.001</td>
      <td>48.189</td>
      <td>55.588</td>
      <td>7.761</td>
      <td>68.52</td>
      <td>5.540718e+06</td>
      <td>18.136</td>
      <td>42.8</td>
      <td>21.228</td>
      <td>13.264</td>
      <td>40585.721</td>
      <td>NaN</td>
      <td>153.507</td>
      <td>5.76</td>
      <td>18.300</td>
      <td>22.600</td>
      <td>3.280</td>
    </tr>
    <tr>
      <th>France</th>
      <td>FRA</td>
      <td>2020-05-26</td>
      <td>145279</td>
      <td>7578</td>
      <td>28432</td>
      <td>2004</td>
      <td>2225.696</td>
      <td>116.096</td>
      <td>435.583</td>
      <td>30.702</td>
      <td>90.74</td>
      <td>6.527351e+07</td>
      <td>122.578</td>
      <td>42.0</td>
      <td>19.718</td>
      <td>13.079</td>
      <td>38605.671</td>
      <td>NaN</td>
      <td>86.060</td>
      <td>4.77</td>
      <td>30.100</td>
      <td>35.600</td>
      <td>5.980</td>
    </tr>
    <tr>
      <th>French Polynesia</th>
      <td>PYF</td>
      <td>2020-05-26</td>
      <td>89</td>
      <td>29</td>
      <td>0</td>
      <td>0</td>
      <td>316.834</td>
      <td>103.238</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>NaN</td>
      <td>2.809040e+05</td>
      <td>77.324</td>
      <td>32.7</td>
      <td>7.775</td>
      <td>4.593</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>22.63</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Gabon</th>
      <td>GAB</td>
      <td>2020-05-26</td>
      <td>2135</td>
      <td>206</td>
      <td>14</td>
      <td>2</td>
      <td>959.237</td>
      <td>92.554</td>
      <td>6.290</td>
      <td>0.899</td>
      <td>87.04</td>
      <td>2.225728e+06</td>
      <td>7.859</td>
      <td>23.1</td>
      <td>4.450</td>
      <td>2.976</td>
      <td>16562.413</td>
      <td>3.4</td>
      <td>259.967</td>
      <td>7.20</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>6.300</td>
    </tr>
    <tr>
      <th>Gambia</th>
      <td>GMB</td>
      <td>2020-05-26</td>
      <td>25</td>
      <td>5</td>
      <td>1</td>
      <td>1</td>
      <td>10.345</td>
      <td>2.069</td>
      <td>0.414</td>
      <td>0.414</td>
      <td>78.70</td>
      <td>2.416664e+06</td>
      <td>207.566</td>
      <td>17.5</td>
      <td>2.339</td>
      <td>1.417</td>
      <td>1561.767</td>
      <td>10.1</td>
      <td>331.430</td>
      <td>1.91</td>
      <td>0.700</td>
      <td>31.200</td>
      <td>1.100</td>
    </tr>
    <tr>
      <th>Georgia</th>
      <td>GEO</td>
      <td>2020-05-26</td>
      <td>731</td>
      <td>43</td>
      <td>12</td>
      <td>2</td>
      <td>183.246</td>
      <td>10.779</td>
      <td>3.008</td>
      <td>0.501</td>
      <td>100.00</td>
      <td>3.989175e+06</td>
      <td>65.032</td>
      <td>38.7</td>
      <td>14.864</td>
      <td>10.244</td>
      <td>9745.079</td>
      <td>4.2</td>
      <td>496.218</td>
      <td>7.11</td>
      <td>5.300</td>
      <td>55.500</td>
      <td>2.600</td>
    </tr>
    <tr>
      <th>Germany</th>
      <td>DEU</td>
      <td>2020-05-26</td>
      <td>179002</td>
      <td>6294</td>
      <td>8302</td>
      <td>315</td>
      <td>2136.471</td>
      <td>75.122</td>
      <td>99.088</td>
      <td>3.760</td>
      <td>73.15</td>
      <td>8.378394e+07</td>
      <td>237.016</td>
      <td>46.6</td>
      <td>21.453</td>
      <td>15.957</td>
      <td>45229.245</td>
      <td>NaN</td>
      <td>156.139</td>
      <td>8.31</td>
      <td>28.200</td>
      <td>33.100</td>
      <td>8.000</td>
    </tr>
    <tr>
      <th>Ghana</th>
      <td>GHA</td>
      <td>2020-05-26</td>
      <td>6808</td>
      <td>921</td>
      <td>32</td>
      <td>5</td>
      <td>219.097</td>
      <td>29.640</td>
      <td>1.030</td>
      <td>0.161</td>
      <td>86.11</td>
      <td>3.107294e+07</td>
      <td>126.719</td>
      <td>21.1</td>
      <td>3.385</td>
      <td>1.948</td>
      <td>4227.630</td>
      <td>12.0</td>
      <td>298.245</td>
      <td>4.97</td>
      <td>0.300</td>
      <td>7.700</td>
      <td>0.900</td>
    </tr>
    <tr>
      <th>Gibraltar</th>
      <td>GIB</td>
      <td>2020-05-26</td>
      <td>155</td>
      <td>20</td>
      <td>0</td>
      <td>0</td>
      <td>4600.635</td>
      <td>593.630</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>NaN</td>
      <td>3.369100e+04</td>
      <td>3457.100</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Greece</th>
      <td>GRC</td>
      <td>2020-05-26</td>
      <td>2882</td>
      <td>156</td>
      <td>172</td>
      <td>9</td>
      <td>276.502</td>
      <td>14.967</td>
      <td>16.502</td>
      <td>0.863</td>
      <td>84.26</td>
      <td>1.042306e+07</td>
      <td>83.479</td>
      <td>45.3</td>
      <td>20.396</td>
      <td>14.524</td>
      <td>24574.382</td>
      <td>1.5</td>
      <td>175.695</td>
      <td>4.55</td>
      <td>35.300</td>
      <td>52.000</td>
      <td>4.210</td>
    </tr>
    <tr>
      <th>Greenland</th>
      <td>GRL</td>
      <td>2020-05-26</td>
      <td>12</td>
      <td>3</td>
      <td>0</td>
      <td>0</td>
      <td>211.372</td>
      <td>52.843</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>81.48</td>
      <td>5.677200e+04</td>
      <td>0.137</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>199.941</td>
      <td>2.16</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Grenada</th>
      <td>GRD</td>
      <td>2020-05-26</td>
      <td>23</td>
      <td>6</td>
      <td>0</td>
      <td>0</td>
      <td>204.410</td>
      <td>53.324</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>NaN</td>
      <td>1.125190e+05</td>
      <td>317.132</td>
      <td>29.4</td>
      <td>7.304</td>
      <td>5.021</td>
      <td>13593.877</td>
      <td>NaN</td>
      <td>243.964</td>
      <td>10.71</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>3.700</td>
    </tr>
    <tr>
      <th>Guam</th>
      <td>GUM</td>
      <td>2020-05-26</td>
      <td>166</td>
      <td>17</td>
      <td>5</td>
      <td>2</td>
      <td>983.511</td>
      <td>100.721</td>
      <td>29.624</td>
      <td>11.850</td>
      <td>75.93</td>
      <td>1.687830e+05</td>
      <td>304.128</td>
      <td>31.4</td>
      <td>9.551</td>
      <td>5.493</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>310.496</td>
      <td>21.52</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Guatemala</th>
      <td>GTM</td>
      <td>2020-05-26</td>
      <td>3760</td>
      <td>370</td>
      <td>59</td>
      <td>5</td>
      <td>209.873</td>
      <td>20.652</td>
      <td>3.293</td>
      <td>0.279</td>
      <td>96.30</td>
      <td>1.791557e+07</td>
      <td>157.834</td>
      <td>22.9</td>
      <td>4.694</td>
      <td>3.016</td>
      <td>7423.808</td>
      <td>8.7</td>
      <td>155.898</td>
      <td>10.18</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.600</td>
    </tr>
    <tr>
      <th>Guernsey</th>
      <td>GGY</td>
      <td>2020-05-26</td>
      <td>252</td>
      <td>23</td>
      <td>13</td>
      <td>2</td>
      <td>3758.277</td>
      <td>343.017</td>
      <td>193.879</td>
      <td>29.828</td>
      <td>NaN</td>
      <td>6.705200e+04</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Guinea</th>
      <td>GIN</td>
      <td>2020-05-26</td>
      <td>3275</td>
      <td>204</td>
      <td>20</td>
      <td>3</td>
      <td>249.376</td>
      <td>15.534</td>
      <td>1.523</td>
      <td>0.228</td>
      <td>73.15</td>
      <td>1.313279e+07</td>
      <td>51.755</td>
      <td>19.0</td>
      <td>3.135</td>
      <td>1.733</td>
      <td>1998.926</td>
      <td>35.3</td>
      <td>336.717</td>
      <td>2.42</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.300</td>
    </tr>
    <tr>
      <th>Guinea-Bissau</th>
      <td>GNB</td>
      <td>2020-05-26</td>
      <td>1173</td>
      <td>128</td>
      <td>6</td>
      <td>2</td>
      <td>596.037</td>
      <td>65.041</td>
      <td>3.049</td>
      <td>1.016</td>
      <td>NaN</td>
      <td>1.967998e+06</td>
      <td>66.191</td>
      <td>19.4</td>
      <td>3.002</td>
      <td>1.565</td>
      <td>1548.675</td>
      <td>67.1</td>
      <td>382.474</td>
      <td>2.42</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Guyana</th>
      <td>GUY</td>
      <td>2020-05-26</td>
      <td>137</td>
      <td>10</td>
      <td>11</td>
      <td>2</td>
      <td>174.176</td>
      <td>12.714</td>
      <td>13.985</td>
      <td>2.543</td>
      <td>90.74</td>
      <td>7.865590e+05</td>
      <td>3.952</td>
      <td>26.3</td>
      <td>5.305</td>
      <td>2.837</td>
      <td>7435.047</td>
      <td>NaN</td>
      <td>373.159</td>
      <td>11.62</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.600</td>
    </tr>
    <tr>
      <th>Haiti</th>
      <td>HTI</td>
      <td>2020-05-26</td>
      <td>1063</td>
      <td>138</td>
      <td>31</td>
      <td>4</td>
      <td>93.225</td>
      <td>12.103</td>
      <td>2.719</td>
      <td>0.351</td>
      <td>NaN</td>
      <td>1.140253e+07</td>
      <td>398.448</td>
      <td>24.3</td>
      <td>4.800</td>
      <td>2.954</td>
      <td>1653.173</td>
      <td>23.5</td>
      <td>430.548</td>
      <td>6.65</td>
      <td>2.900</td>
      <td>23.100</td>
      <td>0.700</td>
    </tr>
    <tr>
      <th>Honduras</th>
      <td>HND</td>
      <td>2020-05-26</td>
      <td>4189</td>
      <td>273</td>
      <td>182</td>
      <td>12</td>
      <td>422.934</td>
      <td>27.563</td>
      <td>18.375</td>
      <td>1.212</td>
      <td>100.00</td>
      <td>9.904608e+06</td>
      <td>82.805</td>
      <td>24.9</td>
      <td>4.652</td>
      <td>2.883</td>
      <td>4541.795</td>
      <td>16.0</td>
      <td>240.208</td>
      <td>7.21</td>
      <td>2.000</td>
      <td>NaN</td>
      <td>0.700</td>
    </tr>
    <tr>
      <th>Hong Kong</th>
      <td>HKG</td>
      <td>2020-05-19</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>66.67</td>
      <td>7.496988e+06</td>
      <td>7039.714</td>
      <td>44.8</td>
      <td>16.303</td>
      <td>10.158</td>
      <td>56054.920</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>8.33</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Hungary</th>
      <td>HUN</td>
      <td>2020-05-26</td>
      <td>3771</td>
      <td>210</td>
      <td>499</td>
      <td>25</td>
      <td>390.359</td>
      <td>21.738</td>
      <td>51.654</td>
      <td>2.588</td>
      <td>74.07</td>
      <td>9.660350e+06</td>
      <td>108.043</td>
      <td>43.4</td>
      <td>18.577</td>
      <td>11.976</td>
      <td>26777.561</td>
      <td>0.5</td>
      <td>278.296</td>
      <td>7.55</td>
      <td>26.800</td>
      <td>34.800</td>
      <td>7.020</td>
    </tr>
    <tr>
      <th>Iceland</th>
      <td>ISL</td>
      <td>2020-05-26</td>
      <td>1804</td>
      <td>99</td>
      <td>10</td>
      <td>2</td>
      <td>5286.447</td>
      <td>290.110</td>
      <td>29.304</td>
      <td>5.861</td>
      <td>53.70</td>
      <td>3.412500e+05</td>
      <td>3.404</td>
      <td>37.3</td>
      <td>14.431</td>
      <td>9.207</td>
      <td>46482.958</td>
      <td>0.2</td>
      <td>117.992</td>
      <td>5.31</td>
      <td>14.300</td>
      <td>15.200</td>
      <td>2.910</td>
    </tr>
    <tr>
      <th>India</th>
      <td>IND</td>
      <td>2020-05-26</td>
      <td>145380</td>
      <td>6977</td>
      <td>4167</td>
      <td>195</td>
      <td>105.347</td>
      <td>5.056</td>
      <td>3.020</td>
      <td>0.141</td>
      <td>100.00</td>
      <td>1.380004e+09</td>
      <td>450.419</td>
      <td>28.2</td>
      <td>5.989</td>
      <td>3.414</td>
      <td>6426.674</td>
      <td>21.2</td>
      <td>282.280</td>
      <td>10.39</td>
      <td>1.900</td>
      <td>20.600</td>
      <td>0.530</td>
    </tr>
    <tr>
      <th>Indonesia</th>
      <td>IDN</td>
      <td>2020-05-26</td>
      <td>22750</td>
      <td>973</td>
      <td>1391</td>
      <td>60</td>
      <td>83.174</td>
      <td>3.557</td>
      <td>5.085</td>
      <td>0.219</td>
      <td>76.39</td>
      <td>2.735236e+08</td>
      <td>145.725</td>
      <td>29.3</td>
      <td>5.319</td>
      <td>3.053</td>
      <td>11188.744</td>
      <td>5.7</td>
      <td>342.864</td>
      <td>6.32</td>
      <td>2.800</td>
      <td>76.100</td>
      <td>1.040</td>
    </tr>
    <tr>
      <th>International</th>
      <td>NaN</td>
      <td>2020-03-10</td>
      <td>705</td>
      <td>134</td>
      <td>7</td>
      <td>2</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Iran</th>
      <td>IRN</td>
      <td>2020-05-26</td>
      <td>137724</td>
      <td>5275</td>
      <td>7451</td>
      <td>292</td>
      <td>1639.709</td>
      <td>62.803</td>
      <td>88.710</td>
      <td>3.476</td>
      <td>62.04</td>
      <td>8.399295e+07</td>
      <td>49.831</td>
      <td>32.4</td>
      <td>5.440</td>
      <td>3.182</td>
      <td>19082.620</td>
      <td>0.2</td>
      <td>270.308</td>
      <td>9.59</td>
      <td>0.800</td>
      <td>21.100</td>
      <td>1.500</td>
    </tr>
    <tr>
      <th>Iraq</th>
      <td>IRQ</td>
      <td>2020-05-26</td>
      <td>4632</td>
      <td>308</td>
      <td>163</td>
      <td>8</td>
      <td>115.159</td>
      <td>7.657</td>
      <td>4.052</td>
      <td>0.199</td>
      <td>96.30</td>
      <td>4.022250e+07</td>
      <td>88.125</td>
      <td>20.0</td>
      <td>3.186</td>
      <td>1.957</td>
      <td>15663.986</td>
      <td>2.5</td>
      <td>218.612</td>
      <td>8.83</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.400</td>
    </tr>
    <tr>
      <th>Ireland</th>
      <td>IRL</td>
      <td>2020-05-26</td>
      <td>24698</td>
      <td>1169</td>
      <td>1606</td>
      <td>234</td>
      <td>5001.827</td>
      <td>236.745</td>
      <td>325.246</td>
      <td>47.390</td>
      <td>90.74</td>
      <td>4.937796e+06</td>
      <td>69.874</td>
      <td>38.7</td>
      <td>13.928</td>
      <td>8.678</td>
      <td>67335.293</td>
      <td>0.2</td>
      <td>126.459</td>
      <td>3.28</td>
      <td>23.000</td>
      <td>25.700</td>
      <td>2.960</td>
    </tr>
    <tr>
      <th>Isle of Man</th>
      <td>IMN</td>
      <td>2020-05-26</td>
      <td>336</td>
      <td>43</td>
      <td>24</td>
      <td>5</td>
      <td>3951.454</td>
      <td>505.692</td>
      <td>282.247</td>
      <td>58.801</td>
      <td>NaN</td>
      <td>8.503200e+04</td>
      <td>147.872</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Israel</th>
      <td>ISR</td>
      <td>2020-05-26</td>
      <td>16734</td>
      <td>1176</td>
      <td>281</td>
      <td>15</td>
      <td>1933.328</td>
      <td>135.867</td>
      <td>32.465</td>
      <td>1.733</td>
      <td>94.44</td>
      <td>8.655541e+06</td>
      <td>402.606</td>
      <td>30.6</td>
      <td>11.733</td>
      <td>7.359</td>
      <td>33132.320</td>
      <td>0.5</td>
      <td>93.320</td>
      <td>6.74</td>
      <td>15.400</td>
      <td>35.400</td>
      <td>2.990</td>
    </tr>
    <tr>
      <th>Italy</th>
      <td>ITA</td>
      <td>2020-05-26</td>
      <td>230158</td>
      <td>6557</td>
      <td>32877</td>
      <td>971</td>
      <td>3806.666</td>
      <td>108.449</td>
      <td>543.765</td>
      <td>16.060</td>
      <td>93.52</td>
      <td>6.046183e+07</td>
      <td>205.859</td>
      <td>47.9</td>
      <td>23.021</td>
      <td>16.240</td>
      <td>35220.084</td>
      <td>2.0</td>
      <td>113.151</td>
      <td>4.78</td>
      <td>19.800</td>
      <td>27.800</td>
      <td>3.180</td>
    </tr>
    <tr>
      <th>Jamaica</th>
      <td>JAM</td>
      <td>2020-05-26</td>
      <td>556</td>
      <td>45</td>
      <td>9</td>
      <td>2</td>
      <td>187.764</td>
      <td>15.197</td>
      <td>3.039</td>
      <td>0.675</td>
      <td>80.56</td>
      <td>2.961161e+06</td>
      <td>266.879</td>
      <td>31.4</td>
      <td>9.684</td>
      <td>6.390</td>
      <td>8193.571</td>
      <td>NaN</td>
      <td>206.537</td>
      <td>11.28</td>
      <td>5.300</td>
      <td>28.600</td>
      <td>1.700</td>
    </tr>
    <tr>
      <th>Japan</th>
      <td>JPN</td>
      <td>2020-05-26</td>
      <td>16623</td>
      <td>1401</td>
      <td>846</td>
      <td>101</td>
      <td>131.432</td>
      <td>11.077</td>
      <td>6.689</td>
      <td>0.799</td>
      <td>47.22</td>
      <td>1.264765e+08</td>
      <td>347.778</td>
      <td>48.2</td>
      <td>27.049</td>
      <td>18.493</td>
      <td>39002.223</td>
      <td>NaN</td>
      <td>79.370</td>
      <td>5.72</td>
      <td>11.200</td>
      <td>33.700</td>
      <td>13.050</td>
    </tr>
    <tr>
      <th>Jersey</th>
      <td>JEY</td>
      <td>2020-05-26</td>
      <td>307</td>
      <td>37</td>
      <td>29</td>
      <td>4</td>
      <td>3037.409</td>
      <td>366.072</td>
      <td>286.921</td>
      <td>39.575</td>
      <td>NaN</td>
      <td>1.010730e+05</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Jordan</th>
      <td>JOR</td>
      <td>2020-05-26</td>
      <td>711</td>
      <td>40</td>
      <td>9</td>
      <td>4</td>
      <td>69.684</td>
      <td>3.920</td>
      <td>0.882</td>
      <td>0.392</td>
      <td>100.00</td>
      <td>1.020314e+07</td>
      <td>109.285</td>
      <td>23.2</td>
      <td>3.810</td>
      <td>2.361</td>
      <td>8337.490</td>
      <td>0.1</td>
      <td>208.257</td>
      <td>11.75</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.400</td>
    </tr>
    <tr>
      <th>Kazakhstan</th>
      <td>KAZ</td>
      <td>2020-05-26</td>
      <td>8969</td>
      <td>438</td>
      <td>35</td>
      <td>4</td>
      <td>477.666</td>
      <td>23.327</td>
      <td>1.864</td>
      <td>0.213</td>
      <td>89.35</td>
      <td>1.877671e+07</td>
      <td>6.681</td>
      <td>30.6</td>
      <td>6.991</td>
      <td>4.625</td>
      <td>24055.588</td>
      <td>0.1</td>
      <td>466.792</td>
      <td>7.11</td>
      <td>7.000</td>
      <td>43.100</td>
      <td>6.700</td>
    </tr>
    <tr>
      <th>Kenya</th>
      <td>KEN</td>
      <td>2020-05-26</td>
      <td>1286</td>
      <td>80</td>
      <td>52</td>
      <td>5</td>
      <td>23.916</td>
      <td>1.488</td>
      <td>0.967</td>
      <td>0.093</td>
      <td>95.37</td>
      <td>5.377130e+07</td>
      <td>87.324</td>
      <td>20.0</td>
      <td>2.686</td>
      <td>1.528</td>
      <td>2993.028</td>
      <td>36.8</td>
      <td>218.637</td>
      <td>2.92</td>
      <td>1.200</td>
      <td>20.400</td>
      <td>1.400</td>
    </tr>
    <tr>
      <th>Kosovo</th>
      <td>XKX</td>
      <td>2020-05-26</td>
      <td>1038</td>
      <td>88</td>
      <td>30</td>
      <td>4</td>
      <td>537.052</td>
      <td>45.530</td>
      <td>15.522</td>
      <td>2.070</td>
      <td>92.59</td>
      <td>1.932774e+06</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Kuwait</th>
      <td>KWT</td>
      <td>2020-05-26</td>
      <td>21967</td>
      <td>1073</td>
      <td>165</td>
      <td>11</td>
      <td>5143.818</td>
      <td>251.255</td>
      <td>38.637</td>
      <td>2.576</td>
      <td>100.00</td>
      <td>4.270563e+06</td>
      <td>232.128</td>
      <td>33.7</td>
      <td>2.345</td>
      <td>1.114</td>
      <td>65530.537</td>
      <td>NaN</td>
      <td>132.235</td>
      <td>15.84</td>
      <td>2.700</td>
      <td>37.000</td>
      <td>2.000</td>
    </tr>
    <tr>
      <th>Kyrgyzstan</th>
      <td>KGZ</td>
      <td>2020-05-26</td>
      <td>1468</td>
      <td>78</td>
      <td>16</td>
      <td>3</td>
      <td>225.009</td>
      <td>11.956</td>
      <td>2.452</td>
      <td>0.460</td>
      <td>92.13</td>
      <td>6.524191e+06</td>
      <td>32.333</td>
      <td>26.3</td>
      <td>4.489</td>
      <td>2.882</td>
      <td>3393.474</td>
      <td>1.4</td>
      <td>436.362</td>
      <td>7.11</td>
      <td>3.600</td>
      <td>50.500</td>
      <td>4.500</td>
    </tr>
    <tr>
      <th>Laos</th>
      <td>LAO</td>
      <td>2020-05-26</td>
      <td>19</td>
      <td>4</td>
      <td>0</td>
      <td>0</td>
      <td>2.611</td>
      <td>0.550</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>96.30</td>
      <td>7.275556e+06</td>
      <td>29.715</td>
      <td>24.4</td>
      <td>4.029</td>
      <td>2.322</td>
      <td>6397.360</td>
      <td>22.7</td>
      <td>368.111</td>
      <td>4.00</td>
      <td>7.300</td>
      <td>51.200</td>
      <td>1.500</td>
    </tr>
    <tr>
      <th>Latvia</th>
      <td>LVA</td>
      <td>2020-05-26</td>
      <td>1049</td>
      <td>71</td>
      <td>22</td>
      <td>4</td>
      <td>556.144</td>
      <td>37.642</td>
      <td>11.664</td>
      <td>2.121</td>
      <td>NaN</td>
      <td>1.886202e+06</td>
      <td>31.212</td>
      <td>43.9</td>
      <td>19.754</td>
      <td>14.136</td>
      <td>25063.846</td>
      <td>0.7</td>
      <td>350.060</td>
      <td>4.91</td>
      <td>25.600</td>
      <td>51.000</td>
      <td>5.570</td>
    </tr>
    <tr>
      <th>Lebanon</th>
      <td>LBN</td>
      <td>2020-05-26</td>
      <td>1119</td>
      <td>67</td>
      <td>26</td>
      <td>4</td>
      <td>163.945</td>
      <td>9.816</td>
      <td>3.809</td>
      <td>0.586</td>
      <td>85.19</td>
      <td>6.825442e+06</td>
      <td>594.561</td>
      <td>31.1</td>
      <td>8.514</td>
      <td>5.430</td>
      <td>13367.565</td>
      <td>NaN</td>
      <td>266.591</td>
      <td>12.71</td>
      <td>26.900</td>
      <td>40.700</td>
      <td>2.900</td>
    </tr>
    <tr>
      <th>Lesotho</th>
      <td>LSO</td>
      <td>2020-05-26</td>
      <td>2</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0.934</td>
      <td>0.467</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>62.04</td>
      <td>2.142252e+06</td>
      <td>73.562</td>
      <td>22.2</td>
      <td>4.506</td>
      <td>2.647</td>
      <td>2851.153</td>
      <td>59.6</td>
      <td>405.126</td>
      <td>3.94</td>
      <td>0.400</td>
      <td>53.900</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Liberia</th>
      <td>LBR</td>
      <td>2020-05-26</td>
      <td>265</td>
      <td>17</td>
      <td>26</td>
      <td>4</td>
      <td>52.396</td>
      <td>3.361</td>
      <td>5.141</td>
      <td>0.791</td>
      <td>79.63</td>
      <td>5.057677e+06</td>
      <td>49.127</td>
      <td>19.2</td>
      <td>3.057</td>
      <td>1.756</td>
      <td>752.788</td>
      <td>38.6</td>
      <td>272.509</td>
      <td>2.42</td>
      <td>1.500</td>
      <td>18.100</td>
      <td>0.800</td>
    </tr>
    <tr>
      <th>Libya</th>
      <td>LBY</td>
      <td>2020-05-26</td>
      <td>75</td>
      <td>13</td>
      <td>3</td>
      <td>1</td>
      <td>10.915</td>
      <td>1.892</td>
      <td>0.437</td>
      <td>0.146</td>
      <td>100.00</td>
      <td>6.871287e+06</td>
      <td>3.623</td>
      <td>29.0</td>
      <td>4.424</td>
      <td>2.816</td>
      <td>17881.509</td>
      <td>NaN</td>
      <td>341.862</td>
      <td>10.43</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>3.700</td>
    </tr>
    <tr>
      <th>Liechtenstein</th>
      <td>LIE</td>
      <td>2020-05-26</td>
      <td>83</td>
      <td>18</td>
      <td>1</td>
      <td>1</td>
      <td>2176.364</td>
      <td>471.983</td>
      <td>26.221</td>
      <td>26.221</td>
      <td>NaN</td>
      <td>3.813700e+04</td>
      <td>237.012</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>7.77</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2.397</td>
    </tr>
    <tr>
      <th>Lithuania</th>
      <td>LTU</td>
      <td>2020-05-26</td>
      <td>1635</td>
      <td>122</td>
      <td>63</td>
      <td>6</td>
      <td>600.597</td>
      <td>44.815</td>
      <td>23.142</td>
      <td>2.204</td>
      <td>90.74</td>
      <td>2.722291e+06</td>
      <td>45.135</td>
      <td>43.5</td>
      <td>19.002</td>
      <td>13.778</td>
      <td>29524.265</td>
      <td>0.7</td>
      <td>342.989</td>
      <td>3.67</td>
      <td>21.300</td>
      <td>38.000</td>
      <td>6.560</td>
    </tr>
    <tr>
      <th>Luxembourg</th>
      <td>LUX</td>
      <td>2020-05-26</td>
      <td>3993</td>
      <td>234</td>
      <td>110</td>
      <td>8</td>
      <td>6378.839</td>
      <td>373.816</td>
      <td>175.726</td>
      <td>12.780</td>
      <td>79.63</td>
      <td>6.259760e+05</td>
      <td>231.447</td>
      <td>39.7</td>
      <td>14.312</td>
      <td>9.842</td>
      <td>94277.965</td>
      <td>0.2</td>
      <td>128.275</td>
      <td>4.42</td>
      <td>20.900</td>
      <td>26.000</td>
      <td>4.510</td>
    </tr>
    <tr>
      <th>Macedonia</th>
      <td>MKD</td>
      <td>2020-05-26</td>
      <td>1999</td>
      <td>107</td>
      <td>113</td>
      <td>6</td>
      <td>959.499</td>
      <td>51.359</td>
      <td>54.239</td>
      <td>2.880</td>
      <td>NaN</td>
      <td>2.083380e+06</td>
      <td>82.600</td>
      <td>39.1</td>
      <td>13.260</td>
      <td>8.160</td>
      <td>13111.214</td>
      <td>5.0</td>
      <td>322.688</td>
      <td>10.08</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>4.280</td>
    </tr>
    <tr>
      <th>Madagascar</th>
      <td>MDG</td>
      <td>2020-05-26</td>
      <td>542</td>
      <td>79</td>
      <td>2</td>
      <td>1</td>
      <td>19.573</td>
      <td>2.853</td>
      <td>0.072</td>
      <td>0.036</td>
      <td>95.37</td>
      <td>2.769102e+07</td>
      <td>43.951</td>
      <td>19.6</td>
      <td>2.929</td>
      <td>1.686</td>
      <td>1416.440</td>
      <td>77.6</td>
      <td>405.994</td>
      <td>3.94</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.200</td>
    </tr>
    <tr>
      <th>Malawi</th>
      <td>MWI</td>
      <td>2020-05-26</td>
      <td>101</td>
      <td>18</td>
      <td>4</td>
      <td>1</td>
      <td>5.280</td>
      <td>0.941</td>
      <td>0.209</td>
      <td>0.052</td>
      <td>57.41</td>
      <td>1.912996e+07</td>
      <td>197.519</td>
      <td>18.1</td>
      <td>2.979</td>
      <td>1.783</td>
      <td>1095.042</td>
      <td>71.4</td>
      <td>227.349</td>
      <td>3.94</td>
      <td>4.400</td>
      <td>24.700</td>
      <td>1.300</td>
    </tr>
    <tr>
      <th>Malaysia</th>
      <td>MYS</td>
      <td>2020-05-26</td>
      <td>7417</td>
      <td>235</td>
      <td>115</td>
      <td>7</td>
      <td>229.160</td>
      <td>7.261</td>
      <td>3.553</td>
      <td>0.216</td>
      <td>73.15</td>
      <td>3.236600e+07</td>
      <td>96.254</td>
      <td>29.9</td>
      <td>6.293</td>
      <td>3.407</td>
      <td>26808.164</td>
      <td>0.1</td>
      <td>260.942</td>
      <td>16.74</td>
      <td>1.000</td>
      <td>42.400</td>
      <td>1.900</td>
    </tr>
    <tr>
      <th>Maldives</th>
      <td>MDV</td>
      <td>2020-05-26</td>
      <td>1395</td>
      <td>191</td>
      <td>4</td>
      <td>1</td>
      <td>2580.743</td>
      <td>353.349</td>
      <td>7.400</td>
      <td>1.850</td>
      <td>NaN</td>
      <td>5.405420e+05</td>
      <td>1454.433</td>
      <td>30.6</td>
      <td>4.120</td>
      <td>2.875</td>
      <td>15183.616</td>
      <td>NaN</td>
      <td>164.905</td>
      <td>9.19</td>
      <td>2.100</td>
      <td>55.000</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Mali</th>
      <td>MLI</td>
      <td>2020-05-26</td>
      <td>1059</td>
      <td>58</td>
      <td>67</td>
      <td>5</td>
      <td>52.294</td>
      <td>2.864</td>
      <td>3.309</td>
      <td>0.247</td>
      <td>72.22</td>
      <td>2.025083e+07</td>
      <td>15.196</td>
      <td>16.4</td>
      <td>2.519</td>
      <td>1.486</td>
      <td>2014.306</td>
      <td>NaN</td>
      <td>268.024</td>
      <td>2.42</td>
      <td>1.600</td>
      <td>23.000</td>
      <td>0.100</td>
    </tr>
    <tr>
      <th>Malta</th>
      <td>MLT</td>
      <td>2020-05-26</td>
      <td>611</td>
      <td>44</td>
      <td>6</td>
      <td>1</td>
      <td>1383.796</td>
      <td>99.651</td>
      <td>13.589</td>
      <td>2.265</td>
      <td>NaN</td>
      <td>4.415390e+05</td>
      <td>1454.037</td>
      <td>42.4</td>
      <td>19.426</td>
      <td>11.324</td>
      <td>36513.323</td>
      <td>0.2</td>
      <td>168.711</td>
      <td>8.83</td>
      <td>20.900</td>
      <td>30.200</td>
      <td>4.485</td>
    </tr>
    <tr>
      <th>Mauritania</th>
      <td>MRT</td>
      <td>2020-05-26</td>
      <td>237</td>
      <td>54</td>
      <td>6</td>
      <td>1</td>
      <td>50.971</td>
      <td>11.614</td>
      <td>1.290</td>
      <td>0.215</td>
      <td>77.78</td>
      <td>4.649660e+06</td>
      <td>4.289</td>
      <td>20.3</td>
      <td>3.138</td>
      <td>1.792</td>
      <td>3597.633</td>
      <td>6.0</td>
      <td>232.347</td>
      <td>2.42</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Mauritius</th>
      <td>MUS</td>
      <td>2020-05-26</td>
      <td>334</td>
      <td>41</td>
      <td>10</td>
      <td>2</td>
      <td>262.627</td>
      <td>32.239</td>
      <td>7.863</td>
      <td>1.573</td>
      <td>82.41</td>
      <td>1.271767e+06</td>
      <td>622.962</td>
      <td>37.4</td>
      <td>10.945</td>
      <td>5.884</td>
      <td>20292.745</td>
      <td>0.5</td>
      <td>224.644</td>
      <td>22.02</td>
      <td>3.200</td>
      <td>40.700</td>
      <td>3.400</td>
    </tr>
    <tr>
      <th>Mexico</th>
      <td>MEX</td>
      <td>2020-05-26</td>
      <td>71105</td>
      <td>3329</td>
      <td>7633</td>
      <td>479</td>
      <td>551.489</td>
      <td>25.820</td>
      <td>59.201</td>
      <td>3.715</td>
      <td>82.41</td>
      <td>1.289328e+08</td>
      <td>66.444</td>
      <td>29.3</td>
      <td>6.857</td>
      <td>4.321</td>
      <td>17336.469</td>
      <td>2.5</td>
      <td>152.783</td>
      <td>13.06</td>
      <td>6.900</td>
      <td>21.400</td>
      <td>1.380</td>
    </tr>
    <tr>
      <th>Moldova</th>
      <td>MDA</td>
      <td>2020-05-26</td>
      <td>7147</td>
      <td>252</td>
      <td>261</td>
      <td>11</td>
      <td>1771.707</td>
      <td>62.470</td>
      <td>64.701</td>
      <td>2.727</td>
      <td>87.04</td>
      <td>4.033963e+06</td>
      <td>123.655</td>
      <td>37.6</td>
      <td>10.864</td>
      <td>6.955</td>
      <td>5189.972</td>
      <td>0.2</td>
      <td>408.502</td>
      <td>5.72</td>
      <td>5.900</td>
      <td>44.600</td>
      <td>5.800</td>
    </tr>
    <tr>
      <th>Monaco</th>
      <td>MCO</td>
      <td>2020-05-26</td>
      <td>98</td>
      <td>9</td>
      <td>5</td>
      <td>2</td>
      <td>2497.197</td>
      <td>229.334</td>
      <td>127.408</td>
      <td>50.963</td>
      <td>NaN</td>
      <td>3.924400e+04</td>
      <td>19347.500</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>5.46</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>13.800</td>
    </tr>
    <tr>
      <th>Mongolia</th>
      <td>MNG</td>
      <td>2020-05-26</td>
      <td>141</td>
      <td>74</td>
      <td>0</td>
      <td>0</td>
      <td>43.010</td>
      <td>22.573</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>90.74</td>
      <td>3.278292e+06</td>
      <td>1.980</td>
      <td>28.6</td>
      <td>4.031</td>
      <td>2.421</td>
      <td>11840.846</td>
      <td>0.5</td>
      <td>460.043</td>
      <td>4.82</td>
      <td>5.500</td>
      <td>46.500</td>
      <td>7.000</td>
    </tr>
    <tr>
      <th>Montenegro</th>
      <td>MNE</td>
      <td>2020-05-26</td>
      <td>324</td>
      <td>30</td>
      <td>9</td>
      <td>1</td>
      <td>515.873</td>
      <td>47.766</td>
      <td>14.330</td>
      <td>1.592</td>
      <td>NaN</td>
      <td>6.280620e+05</td>
      <td>46.280</td>
      <td>39.1</td>
      <td>14.762</td>
      <td>9.395</td>
      <td>16409.288</td>
      <td>1.0</td>
      <td>387.305</td>
      <td>10.08</td>
      <td>44.000</td>
      <td>47.900</td>
      <td>3.861</td>
    </tr>
    <tr>
      <th>Montserrat</th>
      <td>MSR</td>
      <td>2020-05-26</td>
      <td>11</td>
      <td>4</td>
      <td>1</td>
      <td>1</td>
      <td>2200.440</td>
      <td>800.160</td>
      <td>200.040</td>
      <td>200.040</td>
      <td>NaN</td>
      <td>4.999000e+03</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Morocco</th>
      <td>MAR</td>
      <td>2020-05-26</td>
      <td>7532</td>
      <td>281</td>
      <td>200</td>
      <td>15</td>
      <td>204.061</td>
      <td>7.613</td>
      <td>5.419</td>
      <td>0.406</td>
      <td>90.74</td>
      <td>3.691056e+07</td>
      <td>80.080</td>
      <td>29.6</td>
      <td>6.769</td>
      <td>4.209</td>
      <td>7485.013</td>
      <td>1.0</td>
      <td>419.146</td>
      <td>7.14</td>
      <td>0.800</td>
      <td>47.100</td>
      <td>1.100</td>
    </tr>
    <tr>
      <th>Mozambique</th>
      <td>MOZ</td>
      <td>2020-05-26</td>
      <td>209</td>
      <td>26</td>
      <td>1</td>
      <td>1</td>
      <td>6.687</td>
      <td>0.832</td>
      <td>0.032</td>
      <td>0.032</td>
      <td>56.48</td>
      <td>3.125544e+07</td>
      <td>37.728</td>
      <td>17.7</td>
      <td>3.158</td>
      <td>1.870</td>
      <td>1136.103</td>
      <td>62.9</td>
      <td>329.942</td>
      <td>3.30</td>
      <td>5.100</td>
      <td>29.100</td>
      <td>0.700</td>
    </tr>
    <tr>
      <th>Myanmar</th>
      <td>MMR</td>
      <td>2020-05-26</td>
      <td>203</td>
      <td>21</td>
      <td>6</td>
      <td>2</td>
      <td>3.731</td>
      <td>0.386</td>
      <td>0.110</td>
      <td>0.037</td>
      <td>86.11</td>
      <td>5.440979e+07</td>
      <td>81.721</td>
      <td>29.1</td>
      <td>5.732</td>
      <td>3.120</td>
      <td>5591.597</td>
      <td>6.4</td>
      <td>202.104</td>
      <td>4.61</td>
      <td>6.300</td>
      <td>35.200</td>
      <td>0.900</td>
    </tr>
    <tr>
      <th>Namibia</th>
      <td>NAM</td>
      <td>2020-05-26</td>
      <td>21</td>
      <td>4</td>
      <td>0</td>
      <td>0</td>
      <td>8.265</td>
      <td>1.574</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>73.15</td>
      <td>2.540916e+06</td>
      <td>3.078</td>
      <td>22.0</td>
      <td>3.552</td>
      <td>2.085</td>
      <td>9541.808</td>
      <td>13.4</td>
      <td>243.811</td>
      <td>3.94</td>
      <td>9.700</td>
      <td>34.200</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Nepal</th>
      <td>NPL</td>
      <td>2020-05-26</td>
      <td>682</td>
      <td>83</td>
      <td>4</td>
      <td>1</td>
      <td>23.407</td>
      <td>2.849</td>
      <td>0.137</td>
      <td>0.034</td>
      <td>93.52</td>
      <td>2.913681e+07</td>
      <td>204.430</td>
      <td>25.0</td>
      <td>5.809</td>
      <td>3.212</td>
      <td>2442.804</td>
      <td>15.0</td>
      <td>260.797</td>
      <td>7.26</td>
      <td>9.500</td>
      <td>37.800</td>
      <td>0.300</td>
    </tr>
    <tr>
      <th>Netherlands</th>
      <td>NLD</td>
      <td>2020-05-26</td>
      <td>45445</td>
      <td>1335</td>
      <td>5830</td>
      <td>234</td>
      <td>2652.194</td>
      <td>77.911</td>
      <td>340.242</td>
      <td>13.656</td>
      <td>79.63</td>
      <td>1.713487e+07</td>
      <td>508.544</td>
      <td>43.2</td>
      <td>18.779</td>
      <td>11.881</td>
      <td>48472.545</td>
      <td>NaN</td>
      <td>109.361</td>
      <td>5.29</td>
      <td>24.400</td>
      <td>27.300</td>
      <td>3.320</td>
    </tr>
    <tr>
      <th>New Caledonia</th>
      <td>NCL</td>
      <td>2020-05-26</td>
      <td>18</td>
      <td>5</td>
      <td>0</td>
      <td>0</td>
      <td>63.049</td>
      <td>17.514</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>NaN</td>
      <td>2.854910e+05</td>
      <td>15.342</td>
      <td>33.4</td>
      <td>9.954</td>
      <td>6.489</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>23.36</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>New Zealand</th>
      <td>NZL</td>
      <td>2020-05-26</td>
      <td>1154</td>
      <td>95</td>
      <td>21</td>
      <td>4</td>
      <td>239.308</td>
      <td>19.700</td>
      <td>4.355</td>
      <td>0.829</td>
      <td>96.30</td>
      <td>4.822233e+06</td>
      <td>18.206</td>
      <td>37.9</td>
      <td>15.322</td>
      <td>9.720</td>
      <td>36085.843</td>
      <td>NaN</td>
      <td>128.797</td>
      <td>8.08</td>
      <td>14.800</td>
      <td>17.200</td>
      <td>2.610</td>
    </tr>
    <tr>
      <th>Nicaragua</th>
      <td>NIC</td>
      <td>2020-05-26</td>
      <td>279</td>
      <td>254</td>
      <td>17</td>
      <td>9</td>
      <td>42.116</td>
      <td>38.342</td>
      <td>2.566</td>
      <td>1.359</td>
      <td>16.67</td>
      <td>6.624554e+06</td>
      <td>51.667</td>
      <td>27.3</td>
      <td>5.445</td>
      <td>3.519</td>
      <td>5321.444</td>
      <td>3.2</td>
      <td>137.016</td>
      <td>11.47</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.900</td>
    </tr>
    <tr>
      <th>Niger</th>
      <td>NER</td>
      <td>2020-05-26</td>
      <td>951</td>
      <td>69</td>
      <td>62</td>
      <td>5</td>
      <td>39.287</td>
      <td>2.850</td>
      <td>2.561</td>
      <td>0.207</td>
      <td>64.81</td>
      <td>2.420664e+07</td>
      <td>16.955</td>
      <td>15.1</td>
      <td>2.553</td>
      <td>1.378</td>
      <td>926.000</td>
      <td>44.5</td>
      <td>238.339</td>
      <td>2.42</td>
      <td>0.100</td>
      <td>15.400</td>
      <td>0.300</td>
    </tr>
    <tr>
      <th>Nigeria</th>
      <td>NGA</td>
      <td>2020-05-26</td>
      <td>8068</td>
      <td>386</td>
      <td>233</td>
      <td>17</td>
      <td>39.139</td>
      <td>1.873</td>
      <td>1.130</td>
      <td>0.082</td>
      <td>85.65</td>
      <td>2.061396e+08</td>
      <td>209.588</td>
      <td>18.1</td>
      <td>2.751</td>
      <td>1.447</td>
      <td>5338.454</td>
      <td>NaN</td>
      <td>181.013</td>
      <td>2.42</td>
      <td>0.600</td>
      <td>10.800</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Northern Mariana Islands</th>
      <td>MNP</td>
      <td>2020-05-26</td>
      <td>22</td>
      <td>4</td>
      <td>2</td>
      <td>1</td>
      <td>382.230</td>
      <td>69.496</td>
      <td>34.748</td>
      <td>17.374</td>
      <td>NaN</td>
      <td>5.755700e+04</td>
      <td>119.878</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>194.994</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Norway</th>
      <td>NOR</td>
      <td>2020-05-26</td>
      <td>8352</td>
      <td>425</td>
      <td>235</td>
      <td>13</td>
      <td>1540.606</td>
      <td>78.395</td>
      <td>43.348</td>
      <td>2.398</td>
      <td>75.93</td>
      <td>5.421242e+06</td>
      <td>14.462</td>
      <td>39.7</td>
      <td>16.821</td>
      <td>10.813</td>
      <td>64800.057</td>
      <td>0.2</td>
      <td>114.316</td>
      <td>5.31</td>
      <td>19.600</td>
      <td>20.700</td>
      <td>3.600</td>
    </tr>
    <tr>
      <th>Oman</th>
      <td>OMN</td>
      <td>2020-05-26</td>
      <td>7770</td>
      <td>513</td>
      <td>37</td>
      <td>4</td>
      <td>1521.554</td>
      <td>100.458</td>
      <td>7.245</td>
      <td>0.783</td>
      <td>92.59</td>
      <td>5.106622e+06</td>
      <td>14.980</td>
      <td>30.7</td>
      <td>2.355</td>
      <td>1.530</td>
      <td>37960.709</td>
      <td>NaN</td>
      <td>266.342</td>
      <td>12.61</td>
      <td>0.500</td>
      <td>15.600</td>
      <td>1.600</td>
    </tr>
    <tr>
      <th>Pakistan</th>
      <td>PAK</td>
      <td>2020-05-26</td>
      <td>57705</td>
      <td>2603</td>
      <td>1197</td>
      <td>50</td>
      <td>261.236</td>
      <td>11.784</td>
      <td>5.419</td>
      <td>0.226</td>
      <td>96.30</td>
      <td>2.208923e+08</td>
      <td>255.573</td>
      <td>23.5</td>
      <td>4.495</td>
      <td>2.780</td>
      <td>5034.708</td>
      <td>4.0</td>
      <td>423.031</td>
      <td>8.35</td>
      <td>2.800</td>
      <td>36.700</td>
      <td>0.600</td>
    </tr>
    <tr>
      <th>Palestine</th>
      <td>PSE</td>
      <td>2020-05-26</td>
      <td>602</td>
      <td>153</td>
      <td>5</td>
      <td>2</td>
      <td>118.006</td>
      <td>29.992</td>
      <td>0.980</td>
      <td>0.392</td>
      <td>96.30</td>
      <td>5.101416e+06</td>
      <td>778.202</td>
      <td>20.4</td>
      <td>3.043</td>
      <td>1.726</td>
      <td>4449.898</td>
      <td>1.0</td>
      <td>265.910</td>
      <td>10.59</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Panama</th>
      <td>PAN</td>
      <td>2020-05-26</td>
      <td>11183</td>
      <td>370</td>
      <td>310</td>
      <td>10</td>
      <td>2591.796</td>
      <td>85.752</td>
      <td>71.846</td>
      <td>2.318</td>
      <td>82.41</td>
      <td>4.314768e+06</td>
      <td>55.133</td>
      <td>29.7</td>
      <td>7.918</td>
      <td>5.030</td>
      <td>22267.037</td>
      <td>2.2</td>
      <td>128.346</td>
      <td>8.33</td>
      <td>2.400</td>
      <td>9.900</td>
      <td>2.300</td>
    </tr>
    <tr>
      <th>Papua New Guinea</th>
      <td>PNG</td>
      <td>2020-05-26</td>
      <td>8</td>
      <td>5</td>
      <td>0</td>
      <td>0</td>
      <td>0.894</td>
      <td>0.559</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>80.56</td>
      <td>8.947027e+06</td>
      <td>18.220</td>
      <td>22.6</td>
      <td>3.808</td>
      <td>2.142</td>
      <td>3823.194</td>
      <td>NaN</td>
      <td>561.494</td>
      <td>17.65</td>
      <td>23.500</td>
      <td>48.800</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Paraguay</th>
      <td>PRY</td>
      <td>2020-05-26</td>
      <td>865</td>
      <td>126</td>
      <td>11</td>
      <td>2</td>
      <td>121.275</td>
      <td>17.666</td>
      <td>1.542</td>
      <td>0.280</td>
      <td>94.44</td>
      <td>7.132530e+06</td>
      <td>17.144</td>
      <td>26.5</td>
      <td>6.378</td>
      <td>3.833</td>
      <td>8827.010</td>
      <td>1.7</td>
      <td>199.128</td>
      <td>8.27</td>
      <td>5.000</td>
      <td>21.600</td>
      <td>1.300</td>
    </tr>
    <tr>
      <th>Peru</th>
      <td>PER</td>
      <td>2020-05-26</td>
      <td>123979</td>
      <td>4749</td>
      <td>3629</td>
      <td>173</td>
      <td>3760.147</td>
      <td>144.032</td>
      <td>110.064</td>
      <td>5.247</td>
      <td>100.00</td>
      <td>3.297185e+07</td>
      <td>25.129</td>
      <td>29.1</td>
      <td>7.151</td>
      <td>4.455</td>
      <td>12236.706</td>
      <td>3.5</td>
      <td>85.755</td>
      <td>5.95</td>
      <td>4.800</td>
      <td>NaN</td>
      <td>1.600</td>
    </tr>
    <tr>
      <th>Philippines</th>
      <td>PHL</td>
      <td>2020-05-26</td>
      <td>14319</td>
      <td>666</td>
      <td>873</td>
      <td>50</td>
      <td>130.670</td>
      <td>6.078</td>
      <td>7.967</td>
      <td>0.456</td>
      <td>97.22</td>
      <td>1.095811e+08</td>
      <td>351.873</td>
      <td>25.2</td>
      <td>4.803</td>
      <td>2.661</td>
      <td>7599.188</td>
      <td>NaN</td>
      <td>370.437</td>
      <td>7.07</td>
      <td>7.800</td>
      <td>40.800</td>
      <td>1.000</td>
    </tr>
    <tr>
      <th>Poland</th>
      <td>POL</td>
      <td>2020-05-26</td>
      <td>21631</td>
      <td>595</td>
      <td>1007</td>
      <td>40</td>
      <td>571.544</td>
      <td>15.721</td>
      <td>26.607</td>
      <td>1.057</td>
      <td>83.33</td>
      <td>3.784660e+07</td>
      <td>124.027</td>
      <td>41.8</td>
      <td>16.763</td>
      <td>10.202</td>
      <td>27216.445</td>
      <td>NaN</td>
      <td>227.331</td>
      <td>5.91</td>
      <td>23.300</td>
      <td>33.100</td>
      <td>6.620</td>
    </tr>
    <tr>
      <th>Portugal</th>
      <td>PRT</td>
      <td>2020-05-26</td>
      <td>30788</td>
      <td>1516</td>
      <td>1330</td>
      <td>60</td>
      <td>3019.406</td>
      <td>148.675</td>
      <td>130.434</td>
      <td>5.884</td>
      <td>87.96</td>
      <td>1.019671e+07</td>
      <td>112.371</td>
      <td>46.2</td>
      <td>21.502</td>
      <td>14.924</td>
      <td>27936.896</td>
      <td>0.5</td>
      <td>127.842</td>
      <td>9.85</td>
      <td>16.300</td>
      <td>30.000</td>
      <td>3.390</td>
    </tr>
    <tr>
      <th>Puerto Rico</th>
      <td>PRI</td>
      <td>2020-05-26</td>
      <td>3260</td>
      <td>182</td>
      <td>129</td>
      <td>9</td>
      <td>1139.525</td>
      <td>63.618</td>
      <td>45.092</td>
      <td>3.146</td>
      <td>100.00</td>
      <td>2.860840e+06</td>
      <td>376.232</td>
      <td>38.2</td>
      <td>15.168</td>
      <td>9.829</td>
      <td>35044.670</td>
      <td>NaN</td>
      <td>108.094</td>
      <td>12.90</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Qatar</th>
      <td>QAT</td>
      <td>2020-05-26</td>
      <td>45465</td>
      <td>1830</td>
      <td>26</td>
      <td>3</td>
      <td>15780.650</td>
      <td>635.183</td>
      <td>9.024</td>
      <td>1.041</td>
      <td>89.81</td>
      <td>2.881060e+06</td>
      <td>227.322</td>
      <td>31.9</td>
      <td>1.307</td>
      <td>0.617</td>
      <td>116935.600</td>
      <td>NaN</td>
      <td>176.690</td>
      <td>16.52</td>
      <td>0.800</td>
      <td>26.900</td>
      <td>1.200</td>
    </tr>
    <tr>
      <th>Romania</th>
      <td>ROU</td>
      <td>2020-05-26</td>
      <td>18283</td>
      <td>523</td>
      <td>1197</td>
      <td>42</td>
      <td>950.374</td>
      <td>27.186</td>
      <td>62.222</td>
      <td>2.183</td>
      <td>87.04</td>
      <td>1.923768e+07</td>
      <td>85.129</td>
      <td>43.0</td>
      <td>17.850</td>
      <td>11.690</td>
      <td>23313.199</td>
      <td>5.7</td>
      <td>370.946</td>
      <td>9.74</td>
      <td>22.900</td>
      <td>37.100</td>
      <td>6.892</td>
    </tr>
    <tr>
      <th>Russia</th>
      <td>RUS</td>
      <td>2020-05-26</td>
      <td>353427</td>
      <td>11656</td>
      <td>3633</td>
      <td>153</td>
      <td>2421.820</td>
      <td>79.871</td>
      <td>24.895</td>
      <td>1.048</td>
      <td>87.04</td>
      <td>1.459345e+08</td>
      <td>8.823</td>
      <td>39.6</td>
      <td>14.178</td>
      <td>9.393</td>
      <td>24765.954</td>
      <td>0.1</td>
      <td>431.297</td>
      <td>6.18</td>
      <td>23.400</td>
      <td>58.300</td>
      <td>8.050</td>
    </tr>
    <tr>
      <th>Rwanda</th>
      <td>RWA</td>
      <td>2020-05-26</td>
      <td>336</td>
      <td>22</td>
      <td>0</td>
      <td>0</td>
      <td>25.942</td>
      <td>1.699</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>100.00</td>
      <td>1.295221e+07</td>
      <td>494.869</td>
      <td>20.3</td>
      <td>2.974</td>
      <td>1.642</td>
      <td>1854.211</td>
      <td>56.0</td>
      <td>191.375</td>
      <td>4.28</td>
      <td>4.700</td>
      <td>21.000</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Saint Kitts and Nevis</th>
      <td>KNA</td>
      <td>2020-05-26</td>
      <td>15</td>
      <td>5</td>
      <td>0</td>
      <td>0</td>
      <td>281.997</td>
      <td>93.999</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>NaN</td>
      <td>5.319200e+04</td>
      <td>212.865</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>24654.385</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>12.84</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2.300</td>
    </tr>
    <tr>
      <th>Saint Lucia</th>
      <td>LCA</td>
      <td>2020-05-26</td>
      <td>18</td>
      <td>5</td>
      <td>0</td>
      <td>0</td>
      <td>98.024</td>
      <td>27.229</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>NaN</td>
      <td>1.836290e+05</td>
      <td>293.187</td>
      <td>34.9</td>
      <td>9.721</td>
      <td>6.405</td>
      <td>12951.839</td>
      <td>NaN</td>
      <td>204.620</td>
      <td>11.62</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.300</td>
    </tr>
    <tr>
      <th>Saint Vincent and the Grenadines</th>
      <td>VCT</td>
      <td>2020-05-26</td>
      <td>18</td>
      <td>5</td>
      <td>0</td>
      <td>0</td>
      <td>162.240</td>
      <td>45.067</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>NaN</td>
      <td>1.109470e+05</td>
      <td>281.787</td>
      <td>31.8</td>
      <td>7.724</td>
      <td>4.832</td>
      <td>10727.146</td>
      <td>NaN</td>
      <td>252.675</td>
      <td>11.62</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2.600</td>
    </tr>
    <tr>
      <th>San Marino</th>
      <td>SMR</td>
      <td>2020-05-26</td>
      <td>666</td>
      <td>36</td>
      <td>42</td>
      <td>6</td>
      <td>19624.020</td>
      <td>1060.758</td>
      <td>1237.551</td>
      <td>176.793</td>
      <td>92.59</td>
      <td>3.393800e+04</td>
      <td>556.667</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>56861.470</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>5.64</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>3.800</td>
    </tr>
    <tr>
      <th>Sao Tome and Principe</th>
      <td>STP</td>
      <td>2020-05-26</td>
      <td>299</td>
      <td>156</td>
      <td>11</td>
      <td>2</td>
      <td>1364.294</td>
      <td>711.805</td>
      <td>50.191</td>
      <td>9.126</td>
      <td>NaN</td>
      <td>2.191610e+05</td>
      <td>212.841</td>
      <td>18.7</td>
      <td>2.886</td>
      <td>2.162</td>
      <td>3052.714</td>
      <td>32.3</td>
      <td>270.113</td>
      <td>2.42</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2.900</td>
    </tr>
    <tr>
      <th>Saudi Arabia</th>
      <td>SAU</td>
      <td>2020-05-26</td>
      <td>74795</td>
      <td>2840</td>
      <td>399</td>
      <td>15</td>
      <td>2148.426</td>
      <td>81.577</td>
      <td>11.461</td>
      <td>0.431</td>
      <td>94.44</td>
      <td>3.481387e+07</td>
      <td>15.322</td>
      <td>31.9</td>
      <td>3.295</td>
      <td>1.845</td>
      <td>49045.411</td>
      <td>NaN</td>
      <td>259.538</td>
      <td>17.72</td>
      <td>1.800</td>
      <td>25.400</td>
      <td>2.700</td>
    </tr>
    <tr>
      <th>Senegal</th>
      <td>SEN</td>
      <td>2020-05-26</td>
      <td>3130</td>
      <td>177</td>
      <td>36</td>
      <td>4</td>
      <td>186.933</td>
      <td>10.571</td>
      <td>2.150</td>
      <td>0.239</td>
      <td>66.67</td>
      <td>1.674393e+07</td>
      <td>82.328</td>
      <td>18.7</td>
      <td>3.008</td>
      <td>1.796</td>
      <td>2470.580</td>
      <td>38.0</td>
      <td>241.219</td>
      <td>2.42</td>
      <td>0.400</td>
      <td>16.600</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Serbia</th>
      <td>SRB</td>
      <td>2020-05-26</td>
      <td>11193</td>
      <td>445</td>
      <td>239</td>
      <td>10</td>
      <td>1644.918</td>
      <td>65.397</td>
      <td>35.123</td>
      <td>1.470</td>
      <td>100.00</td>
      <td>6.804596e+06</td>
      <td>80.291</td>
      <td>41.2</td>
      <td>17.366</td>
      <td>NaN</td>
      <td>14048.881</td>
      <td>NaN</td>
      <td>439.415</td>
      <td>10.08</td>
      <td>37.700</td>
      <td>40.200</td>
      <td>5.609</td>
    </tr>
    <tr>
      <th>Seychelles</th>
      <td>SYC</td>
      <td>2020-05-26</td>
      <td>11</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>111.857</td>
      <td>20.338</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>93.52</td>
      <td>9.834000e+04</td>
      <td>208.354</td>
      <td>36.2</td>
      <td>8.606</td>
      <td>5.586</td>
      <td>26382.287</td>
      <td>1.1</td>
      <td>242.648</td>
      <td>10.55</td>
      <td>7.100</td>
      <td>35.700</td>
      <td>3.600</td>
    </tr>
    <tr>
      <th>Sierra Leone</th>
      <td>SLE</td>
      <td>2020-05-26</td>
      <td>735</td>
      <td>86</td>
      <td>42</td>
      <td>5</td>
      <td>92.140</td>
      <td>10.781</td>
      <td>5.265</td>
      <td>0.627</td>
      <td>94.44</td>
      <td>7.976985e+06</td>
      <td>104.700</td>
      <td>19.1</td>
      <td>2.538</td>
      <td>1.285</td>
      <td>1390.300</td>
      <td>52.2</td>
      <td>325.721</td>
      <td>2.42</td>
      <td>8.800</td>
      <td>41.300</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Singapore</th>
      <td>SGP</td>
      <td>2020-05-26</td>
      <td>31960</td>
      <td>1426</td>
      <td>23</td>
      <td>2</td>
      <td>5462.928</td>
      <td>243.746</td>
      <td>3.931</td>
      <td>0.342</td>
      <td>85.19</td>
      <td>5.850343e+06</td>
      <td>7915.731</td>
      <td>42.4</td>
      <td>12.922</td>
      <td>7.049</td>
      <td>85535.383</td>
      <td>NaN</td>
      <td>92.243</td>
      <td>10.99</td>
      <td>5.200</td>
      <td>28.300</td>
      <td>2.400</td>
    </tr>
    <tr>
      <th>Sint Maarten (Dutch part)</th>
      <td>SXM</td>
      <td>2020-05-26</td>
      <td>77</td>
      <td>15</td>
      <td>15</td>
      <td>4</td>
      <td>1795.625</td>
      <td>349.797</td>
      <td>349.797</td>
      <td>93.279</td>
      <td>NaN</td>
      <td>4.288200e+04</td>
      <td>1209.088</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>36327.232</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Slovakia</th>
      <td>SVK</td>
      <td>2020-05-26</td>
      <td>1511</td>
      <td>114</td>
      <td>28</td>
      <td>4</td>
      <td>276.758</td>
      <td>20.880</td>
      <td>5.129</td>
      <td>0.733</td>
      <td>87.04</td>
      <td>5.459643e+06</td>
      <td>113.128</td>
      <td>41.2</td>
      <td>15.070</td>
      <td>9.167</td>
      <td>30155.152</td>
      <td>0.7</td>
      <td>287.959</td>
      <td>7.29</td>
      <td>23.100</td>
      <td>37.700</td>
      <td>5.820</td>
    </tr>
    <tr>
      <th>Slovenia</th>
      <td>SVN</td>
      <td>2020-05-26</td>
      <td>1469</td>
      <td>59</td>
      <td>106</td>
      <td>6</td>
      <td>706.613</td>
      <td>28.380</td>
      <td>50.988</td>
      <td>2.886</td>
      <td>89.81</td>
      <td>2.078932e+06</td>
      <td>102.619</td>
      <td>44.5</td>
      <td>19.062</td>
      <td>12.930</td>
      <td>31400.840</td>
      <td>NaN</td>
      <td>153.493</td>
      <td>7.25</td>
      <td>20.100</td>
      <td>25.000</td>
      <td>4.500</td>
    </tr>
    <tr>
      <th>Somalia</th>
      <td>SOM</td>
      <td>2020-05-26</td>
      <td>1689</td>
      <td>95</td>
      <td>66</td>
      <td>6</td>
      <td>106.272</td>
      <td>5.977</td>
      <td>4.153</td>
      <td>0.378</td>
      <td>56.48</td>
      <td>1.589322e+07</td>
      <td>23.500</td>
      <td>16.8</td>
      <td>2.731</td>
      <td>1.496</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>365.769</td>
      <td>6.05</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.900</td>
    </tr>
    <tr>
      <th>South Africa</th>
      <td>ZAF</td>
      <td>2020-05-26</td>
      <td>23615</td>
      <td>1240</td>
      <td>481</td>
      <td>52</td>
      <td>398.171</td>
      <td>20.908</td>
      <td>8.110</td>
      <td>0.877</td>
      <td>87.96</td>
      <td>5.930869e+07</td>
      <td>46.754</td>
      <td>27.3</td>
      <td>5.344</td>
      <td>3.053</td>
      <td>12294.876</td>
      <td>18.9</td>
      <td>200.380</td>
      <td>5.52</td>
      <td>8.100</td>
      <td>33.200</td>
      <td>2.320</td>
    </tr>
    <tr>
      <th>South Korea</th>
      <td>KOR</td>
      <td>2020-05-26</td>
      <td>11225</td>
      <td>909</td>
      <td>269</td>
      <td>9</td>
      <td>218.942</td>
      <td>17.730</td>
      <td>5.247</td>
      <td>0.176</td>
      <td>82.41</td>
      <td>5.126918e+07</td>
      <td>527.967</td>
      <td>43.4</td>
      <td>13.914</td>
      <td>8.622</td>
      <td>35938.374</td>
      <td>0.2</td>
      <td>85.998</td>
      <td>6.80</td>
      <td>6.200</td>
      <td>40.900</td>
      <td>12.270</td>
    </tr>
    <tr>
      <th>South Sudan</th>
      <td>SSD</td>
      <td>2020-05-26</td>
      <td>655</td>
      <td>224</td>
      <td>8</td>
      <td>3</td>
      <td>58.515</td>
      <td>20.011</td>
      <td>0.715</td>
      <td>0.268</td>
      <td>96.30</td>
      <td>1.119373e+07</td>
      <td>NaN</td>
      <td>19.2</td>
      <td>3.441</td>
      <td>2.032</td>
      <td>1569.888</td>
      <td>NaN</td>
      <td>280.775</td>
      <td>10.43</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Spain</th>
      <td>ESP</td>
      <td>2020-05-25</td>
      <td>235772</td>
      <td>9181</td>
      <td>28752</td>
      <td>950</td>
      <td>5042.735</td>
      <td>196.365</td>
      <td>614.953</td>
      <td>20.319</td>
      <td>85.19</td>
      <td>4.675478e+07</td>
      <td>93.105</td>
      <td>45.5</td>
      <td>19.436</td>
      <td>13.799</td>
      <td>34272.360</td>
      <td>1.0</td>
      <td>99.403</td>
      <td>7.17</td>
      <td>27.400</td>
      <td>31.400</td>
      <td>2.970</td>
    </tr>
    <tr>
      <th>Sri Lanka</th>
      <td>LKA</td>
      <td>2020-05-26</td>
      <td>1182</td>
      <td>65</td>
      <td>10</td>
      <td>1</td>
      <td>55.199</td>
      <td>3.036</td>
      <td>0.467</td>
      <td>0.047</td>
      <td>100.00</td>
      <td>2.141325e+07</td>
      <td>341.955</td>
      <td>34.1</td>
      <td>10.069</td>
      <td>5.331</td>
      <td>11669.077</td>
      <td>0.7</td>
      <td>197.093</td>
      <td>10.68</td>
      <td>0.300</td>
      <td>27.000</td>
      <td>3.600</td>
    </tr>
    <tr>
      <th>Sudan</th>
      <td>SDN</td>
      <td>2020-05-26</td>
      <td>3826</td>
      <td>410</td>
      <td>165</td>
      <td>19</td>
      <td>87.253</td>
      <td>9.350</td>
      <td>3.763</td>
      <td>0.433</td>
      <td>85.19</td>
      <td>4.384927e+07</td>
      <td>23.258</td>
      <td>19.7</td>
      <td>3.548</td>
      <td>2.034</td>
      <td>4466.507</td>
      <td>NaN</td>
      <td>431.388</td>
      <td>15.67</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.800</td>
    </tr>
    <tr>
      <th>Suriname</th>
      <td>SUR</td>
      <td>2020-05-26</td>
      <td>11</td>
      <td>4</td>
      <td>1</td>
      <td>1</td>
      <td>18.751</td>
      <td>6.819</td>
      <td>1.705</td>
      <td>1.705</td>
      <td>82.41</td>
      <td>5.866340e+05</td>
      <td>3.612</td>
      <td>29.6</td>
      <td>6.933</td>
      <td>4.229</td>
      <td>13767.119</td>
      <td>NaN</td>
      <td>258.314</td>
      <td>12.54</td>
      <td>7.400</td>
      <td>42.900</td>
      <td>3.100</td>
    </tr>
    <tr>
      <th>Swaziland</th>
      <td>SWZ</td>
      <td>2020-05-26</td>
      <td>256</td>
      <td>30</td>
      <td>2</td>
      <td>1</td>
      <td>220.658</td>
      <td>25.858</td>
      <td>1.724</td>
      <td>0.862</td>
      <td>82.41</td>
      <td>1.160164e+06</td>
      <td>79.492</td>
      <td>21.5</td>
      <td>3.163</td>
      <td>1.845</td>
      <td>7738.975</td>
      <td>NaN</td>
      <td>333.436</td>
      <td>3.94</td>
      <td>1.700</td>
      <td>16.500</td>
      <td>2.100</td>
    </tr>
    <tr>
      <th>Sweden</th>
      <td>SWE</td>
      <td>2020-05-26</td>
      <td>33843</td>
      <td>812</td>
      <td>4029</td>
      <td>185</td>
      <td>3351.034</td>
      <td>80.402</td>
      <td>398.940</td>
      <td>18.318</td>
      <td>40.74</td>
      <td>1.009927e+07</td>
      <td>24.718</td>
      <td>41.0</td>
      <td>19.985</td>
      <td>13.433</td>
      <td>46949.283</td>
      <td>0.5</td>
      <td>133.982</td>
      <td>4.79</td>
      <td>18.800</td>
      <td>18.900</td>
      <td>2.220</td>
    </tr>
    <tr>
      <th>Switzerland</th>
      <td>CHE</td>
      <td>2020-05-26</td>
      <td>30663</td>
      <td>1390</td>
      <td>1641</td>
      <td>78</td>
      <td>3542.964</td>
      <td>160.608</td>
      <td>189.610</td>
      <td>9.013</td>
      <td>76.85</td>
      <td>8.654618e+06</td>
      <td>214.243</td>
      <td>43.1</td>
      <td>18.436</td>
      <td>12.644</td>
      <td>57410.166</td>
      <td>NaN</td>
      <td>99.739</td>
      <td>5.59</td>
      <td>22.600</td>
      <td>28.900</td>
      <td>4.530</td>
    </tr>
    <tr>
      <th>Syria</th>
      <td>SYR</td>
      <td>2020-05-26</td>
      <td>106</td>
      <td>20</td>
      <td>4</td>
      <td>1</td>
      <td>6.057</td>
      <td>1.143</td>
      <td>0.229</td>
      <td>0.057</td>
      <td>83.33</td>
      <td>1.750066e+07</td>
      <td>NaN</td>
      <td>21.7</td>
      <td>NaN</td>
      <td>2.577</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>376.264</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.500</td>
    </tr>
    <tr>
      <th>Taiwan</th>
      <td>TWN</td>
      <td>2020-05-26</td>
      <td>441</td>
      <td>31</td>
      <td>7</td>
      <td>3</td>
      <td>18.516</td>
      <td>1.302</td>
      <td>0.294</td>
      <td>0.126</td>
      <td>30.56</td>
      <td>2.381678e+07</td>
      <td>NaN</td>
      <td>42.2</td>
      <td>NaN</td>
      <td>8.353</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>103.957</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Tajikistan</th>
      <td>TJK</td>
      <td>2020-05-26</td>
      <td>3100</td>
      <td>362</td>
      <td>46</td>
      <td>8</td>
      <td>325.028</td>
      <td>37.955</td>
      <td>4.823</td>
      <td>0.839</td>
      <td>NaN</td>
      <td>9.537642e+06</td>
      <td>64.281</td>
      <td>23.3</td>
      <td>3.466</td>
      <td>2.155</td>
      <td>2896.913</td>
      <td>4.8</td>
      <td>427.698</td>
      <td>7.11</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>4.800</td>
    </tr>
    <tr>
      <th>Tanzania</th>
      <td>TZA</td>
      <td>2020-05-26</td>
      <td>509</td>
      <td>174</td>
      <td>21</td>
      <td>6</td>
      <td>8.521</td>
      <td>2.913</td>
      <td>0.352</td>
      <td>0.100</td>
      <td>50.00</td>
      <td>5.973421e+07</td>
      <td>64.699</td>
      <td>17.7</td>
      <td>3.108</td>
      <td>1.874</td>
      <td>2683.304</td>
      <td>49.1</td>
      <td>217.288</td>
      <td>5.75</td>
      <td>3.300</td>
      <td>26.700</td>
      <td>0.700</td>
    </tr>
    <tr>
      <th>Thailand</th>
      <td>THA</td>
      <td>2020-05-26</td>
      <td>3042</td>
      <td>263</td>
      <td>57</td>
      <td>4</td>
      <td>43.582</td>
      <td>3.768</td>
      <td>0.817</td>
      <td>0.057</td>
      <td>82.41</td>
      <td>6.979998e+07</td>
      <td>135.132</td>
      <td>40.1</td>
      <td>11.373</td>
      <td>6.890</td>
      <td>16277.671</td>
      <td>0.1</td>
      <td>109.861</td>
      <td>7.04</td>
      <td>1.900</td>
      <td>38.800</td>
      <td>2.100</td>
    </tr>
    <tr>
      <th>Timor</th>
      <td>TLS</td>
      <td>2020-05-26</td>
      <td>24</td>
      <td>12</td>
      <td>0</td>
      <td>0</td>
      <td>18.203</td>
      <td>9.102</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>NaN</td>
      <td>1.318442e+06</td>
      <td>87.176</td>
      <td>18.0</td>
      <td>3.556</td>
      <td>1.897</td>
      <td>6570.102</td>
      <td>30.3</td>
      <td>335.346</td>
      <td>6.86</td>
      <td>6.300</td>
      <td>78.100</td>
      <td>5.900</td>
    </tr>
    <tr>
      <th>Togo</th>
      <td>TGO</td>
      <td>2020-05-26</td>
      <td>386</td>
      <td>35</td>
      <td>13</td>
      <td>2</td>
      <td>46.625</td>
      <td>4.228</td>
      <td>1.570</td>
      <td>0.242</td>
      <td>NaN</td>
      <td>8.278737e+06</td>
      <td>143.366</td>
      <td>19.4</td>
      <td>2.839</td>
      <td>1.525</td>
      <td>1429.813</td>
      <td>49.2</td>
      <td>280.033</td>
      <td>6.15</td>
      <td>0.900</td>
      <td>14.200</td>
      <td>0.700</td>
    </tr>
    <tr>
      <th>Trinidad and Tobago</th>
      <td>TTO</td>
      <td>2020-05-26</td>
      <td>116</td>
      <td>40</td>
      <td>8</td>
      <td>2</td>
      <td>82.887</td>
      <td>28.582</td>
      <td>5.716</td>
      <td>1.429</td>
      <td>90.74</td>
      <td>1.399491e+06</td>
      <td>266.886</td>
      <td>36.2</td>
      <td>10.014</td>
      <td>5.819</td>
      <td>28763.071</td>
      <td>NaN</td>
      <td>228.467</td>
      <td>10.97</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>3.000</td>
    </tr>
    <tr>
      <th>Tunisia</th>
      <td>TUN</td>
      <td>2020-05-26</td>
      <td>1051</td>
      <td>61</td>
      <td>48</td>
      <td>5</td>
      <td>88.927</td>
      <td>5.161</td>
      <td>4.061</td>
      <td>0.423</td>
      <td>87.96</td>
      <td>1.181862e+07</td>
      <td>74.228</td>
      <td>32.7</td>
      <td>8.001</td>
      <td>5.075</td>
      <td>10849.297</td>
      <td>2.0</td>
      <td>318.991</td>
      <td>8.52</td>
      <td>1.100</td>
      <td>65.800</td>
      <td>2.300</td>
    </tr>
    <tr>
      <th>Turkey</th>
      <td>TUR</td>
      <td>2020-05-26</td>
      <td>157814</td>
      <td>5138</td>
      <td>4369</td>
      <td>127</td>
      <td>1871.185</td>
      <td>60.921</td>
      <td>51.803</td>
      <td>1.506</td>
      <td>80.56</td>
      <td>8.433907e+07</td>
      <td>104.914</td>
      <td>31.6</td>
      <td>8.153</td>
      <td>5.061</td>
      <td>25129.341</td>
      <td>0.2</td>
      <td>171.285</td>
      <td>12.13</td>
      <td>14.100</td>
      <td>41.100</td>
      <td>2.810</td>
    </tr>
    <tr>
      <th>Turks and Caicos Islands</th>
      <td>TCA</td>
      <td>2020-05-26</td>
      <td>12</td>
      <td>3</td>
      <td>1</td>
      <td>1</td>
      <td>309.933</td>
      <td>77.483</td>
      <td>25.828</td>
      <td>25.828</td>
      <td>NaN</td>
      <td>3.871800e+04</td>
      <td>37.312</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Uganda</th>
      <td>UGA</td>
      <td>2020-05-26</td>
      <td>326</td>
      <td>48</td>
      <td>0</td>
      <td>0</td>
      <td>7.127</td>
      <td>1.049</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>90.74</td>
      <td>4.574100e+07</td>
      <td>213.759</td>
      <td>16.4</td>
      <td>2.168</td>
      <td>1.308</td>
      <td>1697.707</td>
      <td>41.6</td>
      <td>213.333</td>
      <td>2.50</td>
      <td>3.400</td>
      <td>16.700</td>
      <td>0.500</td>
    </tr>
    <tr>
      <th>Ukraine</th>
      <td>UKR</td>
      <td>2020-05-26</td>
      <td>21245</td>
      <td>789</td>
      <td>623</td>
      <td>29</td>
      <td>485.780</td>
      <td>18.041</td>
      <td>14.245</td>
      <td>0.663</td>
      <td>88.89</td>
      <td>4.373376e+07</td>
      <td>77.390</td>
      <td>41.4</td>
      <td>16.462</td>
      <td>11.133</td>
      <td>7894.393</td>
      <td>0.1</td>
      <td>539.849</td>
      <td>7.11</td>
      <td>13.500</td>
      <td>47.400</td>
      <td>8.800</td>
    </tr>
    <tr>
      <th>United Arab Emirates</th>
      <td>ARE</td>
      <td>2020-05-26</td>
      <td>30307</td>
      <td>994</td>
      <td>248</td>
      <td>13</td>
      <td>3064.285</td>
      <td>100.501</td>
      <td>25.075</td>
      <td>1.314</td>
      <td>89.81</td>
      <td>9.890400e+06</td>
      <td>112.442</td>
      <td>34.0</td>
      <td>1.144</td>
      <td>0.526</td>
      <td>67293.483</td>
      <td>NaN</td>
      <td>317.840</td>
      <td>17.26</td>
      <td>1.200</td>
      <td>37.400</td>
      <td>1.200</td>
    </tr>
    <tr>
      <th>United Kingdom</th>
      <td>GBR</td>
      <td>2020-05-26</td>
      <td>261184</td>
      <td>8719</td>
      <td>36914</td>
      <td>1172</td>
      <td>3847.391</td>
      <td>128.436</td>
      <td>543.765</td>
      <td>17.264</td>
      <td>75.93</td>
      <td>6.788600e+07</td>
      <td>272.898</td>
      <td>40.8</td>
      <td>18.517</td>
      <td>12.527</td>
      <td>39753.244</td>
      <td>0.2</td>
      <td>122.137</td>
      <td>4.28</td>
      <td>20.000</td>
      <td>24.700</td>
      <td>2.540</td>
    </tr>
    <tr>
      <th>United States</th>
      <td>USA</td>
      <td>2020-05-26</td>
      <td>1662302</td>
      <td>48529</td>
      <td>98220</td>
      <td>4928</td>
      <td>5022.020</td>
      <td>146.612</td>
      <td>296.735</td>
      <td>14.888</td>
      <td>74.54</td>
      <td>3.310026e+08</td>
      <td>35.608</td>
      <td>38.3</td>
      <td>15.413</td>
      <td>9.732</td>
      <td>54225.446</td>
      <td>1.2</td>
      <td>151.089</td>
      <td>10.79</td>
      <td>19.100</td>
      <td>24.600</td>
      <td>2.770</td>
    </tr>
    <tr>
      <th>United States Virgin Islands</th>
      <td>VIR</td>
      <td>2020-05-26</td>
      <td>69</td>
      <td>17</td>
      <td>6</td>
      <td>1</td>
      <td>660.774</td>
      <td>162.799</td>
      <td>57.459</td>
      <td>9.576</td>
      <td>NaN</td>
      <td>1.044230e+05</td>
      <td>306.480</td>
      <td>42.2</td>
      <td>18.601</td>
      <td>10.799</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>273.670</td>
      <td>12.26</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Uruguay</th>
      <td>URY</td>
      <td>2020-05-26</td>
      <td>787</td>
      <td>36</td>
      <td>22</td>
      <td>2</td>
      <td>226.558</td>
      <td>10.364</td>
      <td>6.333</td>
      <td>0.576</td>
      <td>72.22</td>
      <td>3.473727e+06</td>
      <td>19.751</td>
      <td>35.6</td>
      <td>14.655</td>
      <td>10.361</td>
      <td>20551.409</td>
      <td>0.1</td>
      <td>160.708</td>
      <td>6.93</td>
      <td>14.000</td>
      <td>19.900</td>
      <td>2.800</td>
    </tr>
    <tr>
      <th>Uzbekistan</th>
      <td>UZB</td>
      <td>2020-05-26</td>
      <td>3261</td>
      <td>172</td>
      <td>13</td>
      <td>1</td>
      <td>97.433</td>
      <td>5.139</td>
      <td>0.388</td>
      <td>0.030</td>
      <td>96.30</td>
      <td>3.346920e+07</td>
      <td>76.134</td>
      <td>28.2</td>
      <td>4.469</td>
      <td>2.873</td>
      <td>6253.104</td>
      <td>NaN</td>
      <td>724.417</td>
      <td>7.57</td>
      <td>1.300</td>
      <td>24.700</td>
      <td>4.000</td>
    </tr>
    <tr>
      <th>Vatican</th>
      <td>VAT</td>
      <td>2020-05-26</td>
      <td>12</td>
      <td>4</td>
      <td>0</td>
      <td>0</td>
      <td>14833.127</td>
      <td>4944.376</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>NaN</td>
      <td>8.090000e+02</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Venezuela</th>
      <td>VEN</td>
      <td>2020-05-26</td>
      <td>1177</td>
      <td>177</td>
      <td>10</td>
      <td>2</td>
      <td>41.391</td>
      <td>6.225</td>
      <td>0.352</td>
      <td>0.070</td>
      <td>85.19</td>
      <td>2.843594e+07</td>
      <td>36.253</td>
      <td>29.0</td>
      <td>6.614</td>
      <td>3.915</td>
      <td>16745.022</td>
      <td>NaN</td>
      <td>204.850</td>
      <td>6.47</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.800</td>
    </tr>
    <tr>
      <th>Vietnam</th>
      <td>VNM</td>
      <td>2020-05-26</td>
      <td>326</td>
      <td>26</td>
      <td>0</td>
      <td>0</td>
      <td>3.349</td>
      <td>0.267</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>96.30</td>
      <td>9.733858e+07</td>
      <td>308.127</td>
      <td>32.6</td>
      <td>7.150</td>
      <td>4.718</td>
      <td>6171.884</td>
      <td>2.0</td>
      <td>245.465</td>
      <td>6.00</td>
      <td>1.000</td>
      <td>45.900</td>
      <td>2.600</td>
    </tr>
    <tr>
      <th>Western Sahara</th>
      <td>ESH</td>
      <td>2020-05-26</td>
      <td>6</td>
      <td>6</td>
      <td>0</td>
      <td>0</td>
      <td>10.045</td>
      <td>10.045</td>
      <td>0.000</td>
      <td>0.000</td>
      <td>NaN</td>
      <td>5.973300e+05</td>
      <td>NaN</td>
      <td>28.4</td>
      <td>NaN</td>
      <td>1.380</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>World</th>
      <td>OWID_WRL</td>
      <td>2020-05-26</td>
      <td>5459526</td>
      <td>107909</td>
      <td>345994</td>
      <td>10520</td>
      <td>700.406</td>
      <td>13.844</td>
      <td>44.388</td>
      <td>1.350</td>
      <td>NaN</td>
      <td>7.794799e+09</td>
      <td>58.045</td>
      <td>30.9</td>
      <td>8.696</td>
      <td>5.355</td>
      <td>15469.207</td>
      <td>10.0</td>
      <td>233.070</td>
      <td>8.51</td>
      <td>6.434</td>
      <td>34.635</td>
      <td>2.705</td>
    </tr>
    <tr>
      <th>Yemen</th>
      <td>YEM</td>
      <td>2020-05-26</td>
      <td>237</td>
      <td>37</td>
      <td>45</td>
      <td>8</td>
      <td>7.946</td>
      <td>1.241</td>
      <td>1.509</td>
      <td>0.268</td>
      <td>52.78</td>
      <td>2.982597e+07</td>
      <td>53.508</td>
      <td>20.3</td>
      <td>2.922</td>
      <td>1.583</td>
      <td>1479.147</td>
      <td>18.8</td>
      <td>495.003</td>
      <td>5.35</td>
      <td>7.600</td>
      <td>29.200</td>
      <td>0.700</td>
    </tr>
    <tr>
      <th>Zambia</th>
      <td>ZMB</td>
      <td>2020-05-26</td>
      <td>920</td>
      <td>208</td>
      <td>7</td>
      <td>3</td>
      <td>50.044</td>
      <td>11.314</td>
      <td>0.381</td>
      <td>0.163</td>
      <td>70.83</td>
      <td>1.838396e+07</td>
      <td>22.995</td>
      <td>17.7</td>
      <td>2.480</td>
      <td>1.542</td>
      <td>3689.251</td>
      <td>57.5</td>
      <td>234.499</td>
      <td>3.94</td>
      <td>3.100</td>
      <td>24.700</td>
      <td>2.000</td>
    </tr>
    <tr>
      <th>Zimbabwe</th>
      <td>ZWE</td>
      <td>2020-05-26</td>
      <td>56</td>
      <td>6</td>
      <td>4</td>
      <td>1</td>
      <td>3.768</td>
      <td>0.404</td>
      <td>0.269</td>
      <td>0.067</td>
      <td>87.96</td>
      <td>1.486293e+07</td>
      <td>42.729</td>
      <td>19.6</td>
      <td>2.822</td>
      <td>1.882</td>
      <td>1899.775</td>
      <td>21.4</td>
      <td>307.846</td>
      <td>1.82</td>
      <td>1.600</td>
      <td>30.700</td>
      <td>1.700</td>
    </tr>
  </tbody>
</table>
</div>




```python
data_drop.groupby('location').max().total_deaths.sort_values(ascending=False)
```




    location
    World                               345994
    United States                        98220
    United Kingdom                       36914
    Italy                                32877
    Spain                                28752
    France                               28432
    Brazil                               23473
    Belgium                               9312
    Germany                               8302
    Mexico                                7633
    Iran                                  7451
    Canada                                6545
    Netherlands                           5830
    China                                 4638
    Turkey                                4369
    India                                 4167
    Sweden                                4029
    Russia                                3633
    Peru                                  3629
    Ecuador                               3203
    Switzerland                           1641
    Ireland                               1606
    Indonesia                             1391
    Portugal                              1330
    Pakistan                              1197
    Romania                               1197
    Poland                                1007
    Philippines                            873
    Japan                                  846
    Egypt                                  783
    Chile                                  761
    Colombia                               750
    Austria                                641
    Ukraine                                623
    Algeria                                609
    Denmark                                563
    Bangladesh                             501
    Hungary                                499
    South Africa                           481
    Argentina                              467
    Dominican Republic                     460
    Saudi Arabia                           399
    Czech Republic                         317
    Panama                                 310
    Finland                                308
    Israel                                 281
    South Korea                            269
    Bolivia                                261
    Moldova                                261
    United Arab Emirates                   248
    Serbia                                 239
    Norway                                 235
    Nigeria                                233
    Afghanistan                            219
    Belarus                                204
    Morocco                                200
    Honduras                               182
    Greece                                 172
    Cameroon                               171
    Kuwait                                 165
    Sudan                                  165
    Iraq                                   163
    Bosnia and Herzegovina                 146
    Bulgaria                               130
    Puerto Rico                            129
    Malaysia                               115
    Macedonia                              113
    Luxembourg                             110
    Slovenia                               106
    Australia                              102
    Croatia                                100
    Armenia                                 87
    Cuba                                    82
    Democratic Republic of Congo            67
    Mali                                    67
    Somalia                                 66
    Estonia                                 65
    Lithuania                               63
    Niger                                   62
    Chad                                    61
    Guatemala                               59
    Thailand                                57
    Kenya                                   52
    Burkina Faso                            52
    Andorra                                 51
    Azerbaijan                              51
    Tunisia                                 48
    Tajikistan                              46
    Yemen                                   45
    Sierra Leone                            42
    San Marino                              42
    Oman                                    37
    Senegal                                 36
    El Salvador                             36
    Kazakhstan                              35
    Albania                                 32
    Ghana                                   32
    Haiti                                   31
    Cote d'Ivoire                           30
    Kosovo                                  30
    Jersey                                  29
    Slovakia                                28
    Qatar                                   26
    Lebanon                                 26
    Liberia                                 26
    Isle of Man                             24
    Singapore                               23
    Uruguay                                 22
    Latvia                                  22
    Tanzania                                21
    New Zealand                             21
    Guinea                                  20
    Congo                                   17
    Cyprus                                  17
    Nicaragua                               17
    Kyrgyzstan                              16
    Sint Maarten (Dutch part)               15
    Gabon                                   14
    Bahrain                                 14
    Djibouti                                14
    Uzbekistan                              13
    Togo                                    13
    Guernsey                                13
    Equatorial Guinea                       12
    Georgia                                 12
    Paraguay                                11
    Bahamas                                 11
    Guyana                                  11
    Sao Tome and Principe                   11
    Mauritius                               10
    Iceland                                 10
    Venezuela                               10
    Costa Rica                              10
    Sri Lanka                               10
    Bermuda                                  9
    Montenegro                               9
    Jordan                                   9
    Jamaica                                  9
    Trinidad and Tobago                      8
    South Sudan                              8
    Taiwan                                   7
    Zambia                                   7
    Barbados                                 7
    International                            7
    Malta                                    6
    Mauritania                               6
    Guinea-Bissau                            6
    United States Virgin Islands             6
    Myanmar                                  6
    Ethiopia                                 5
    Palestine                                5
    Guam                                     5
    Monaco                                   5
    Malawi                                   4
    Maldives                                 4
    Syria                                    4
    Zimbabwe                                 4
    Angola                                   4
    Nepal                                    4
    Antigua and Barbuda                      3
    Benin                                    3
    Libya                                    3
    Aruba                                    3
    Cape Verde                               3
    Swaziland                                2
    Madagascar                               2
    Northern Mariana Islands                 2
    Belize                                   2
    Cayman Islands                           1
    Burundi                                  1
    Brunei                                   1
    Suriname                                 1
    British Virgin Islands                   1
    Botswana                                 1
    Gambia                                   1
    Central African Republic                 1
    Turks and Caicos Islands                 1
    Liechtenstein                            1
    Comoros                                  1
    Curacao                                  1
    Mozambique                               1
    Montserrat                               1
    Bhutan                                   0
    Uganda                                   0
    Anguilla                                 0
    Vatican                                  0
    Western Sahara                           0
    Vietnam                                  0
    Lesotho                                  0
    Timor                                    0
    Fiji                                     0
    Laos                                     0
    Mongolia                                 0
    Hong Kong                                0
    Grenada                                  0
    Greenland                                0
    Namibia                                  0
    Gibraltar                                0
    New Caledonia                            0
    French Polynesia                         0
    Falkland Islands                         0
    Bonaire Sint Eustatius and Saba          0
    Faeroe Islands                           0
    Eritrea                                  0
    Papua New Guinea                         0
    Rwanda                                   0
    Saint Kitts and Nevis                    0
    Saint Lucia                              0
    Saint Vincent and the Grenadines         0
    Seychelles                               0
    Cambodia                                 0
    Dominica                                 0
    Name: total_deaths, dtype: int64



## A visual of the total Number of Deaths per country


```python
data_drop.groupby('location').max().total_deaths.sort_values(ascending=False).plot(kind='bar', figsize=(100,12));
```


![png](assets/images/covid/output_67_0.png)


## A visual of the total_deaths_per_million per country


```python
data_drop.groupby('location').max().total_deaths_per_million.sort_values(ascending=False).plot(kind='bar', figsize=(100,12));
```


![png](assets/images/covid/output_69_0.png)



```python
data_drop.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>iso_code</th>
      <th>location</th>
      <th>date</th>
      <th>total_cases</th>
      <th>new_cases</th>
      <th>total_deaths</th>
      <th>new_deaths</th>
      <th>total_cases_per_million</th>
      <th>new_cases_per_million</th>
      <th>total_deaths_per_million</th>
      <th>new_deaths_per_million</th>
      <th>stringency_index</th>
      <th>population</th>
      <th>population_density</th>
      <th>median_age</th>
      <th>aged_65_older</th>
      <th>aged_70_older</th>
      <th>gdp_per_capita</th>
      <th>extreme_poverty</th>
      <th>cvd_death_rate</th>
      <th>diabetes_prevalence</th>
      <th>female_smokers</th>
      <th>male_smokers</th>
      <th>hospital_beds_per_100k</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>ABW</td>
      <td>Aruba</td>
      <td>2020-03-13</td>
      <td>2</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>18.733</td>
      <td>18.733</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>106766.0</td>
      <td>584.8</td>
      <td>41.2</td>
      <td>13.085</td>
      <td>7.452</td>
      <td>35973.781</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>11.62</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>ABW</td>
      <td>Aruba</td>
      <td>2020-03-20</td>
      <td>4</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>37.465</td>
      <td>18.733</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>30.56</td>
      <td>106766.0</td>
      <td>584.8</td>
      <td>41.2</td>
      <td>13.085</td>
      <td>7.452</td>
      <td>35973.781</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>11.62</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>ABW</td>
      <td>Aruba</td>
      <td>2020-03-24</td>
      <td>12</td>
      <td>8</td>
      <td>0</td>
      <td>0</td>
      <td>112.395</td>
      <td>74.930</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>41.67</td>
      <td>106766.0</td>
      <td>584.8</td>
      <td>41.2</td>
      <td>13.085</td>
      <td>7.452</td>
      <td>35973.781</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>11.62</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>ABW</td>
      <td>Aruba</td>
      <td>2020-03-25</td>
      <td>17</td>
      <td>5</td>
      <td>0</td>
      <td>0</td>
      <td>159.227</td>
      <td>46.831</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>41.67</td>
      <td>106766.0</td>
      <td>584.8</td>
      <td>41.2</td>
      <td>13.085</td>
      <td>7.452</td>
      <td>35973.781</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>11.62</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>ABW</td>
      <td>Aruba</td>
      <td>2020-03-26</td>
      <td>19</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>177.959</td>
      <td>18.733</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>41.67</td>
      <td>106766.0</td>
      <td>584.8</td>
      <td>41.2</td>
      <td>13.085</td>
      <td>7.452</td>
      <td>35973.781</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>11.62</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
data_drop.shape
```




    (19918, 24)



## Correlation among the columns in the dataframe using ‘Pearson’


```python
# Is there a corelation between total_deaths_per_million and Median age
data_drop.corr(method ='pearson')

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>total_cases</th>
      <th>new_cases</th>
      <th>total_deaths</th>
      <th>new_deaths</th>
      <th>total_cases_per_million</th>
      <th>new_cases_per_million</th>
      <th>total_deaths_per_million</th>
      <th>new_deaths_per_million</th>
      <th>stringency_index</th>
      <th>population</th>
      <th>population_density</th>
      <th>median_age</th>
      <th>aged_65_older</th>
      <th>aged_70_older</th>
      <th>gdp_per_capita</th>
      <th>extreme_poverty</th>
      <th>cvd_death_rate</th>
      <th>diabetes_prevalence</th>
      <th>female_smokers</th>
      <th>male_smokers</th>
      <th>hospital_beds_per_100k</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>total_cases</th>
      <td>1.000000</td>
      <td>0.907625</td>
      <td>0.990031</td>
      <td>0.804693</td>
      <td>0.059672</td>
      <td>0.026590</td>
      <td>0.087117</td>
      <td>0.043499</td>
      <td>0.098873</td>
      <td>0.552607</td>
      <td>-0.017212</td>
      <td>0.028564</td>
      <td>0.029799</td>
      <td>0.028719</td>
      <td>0.016983</td>
      <td>-0.025413</td>
      <td>-0.035107</td>
      <td>0.012486</td>
      <td>0.005616</td>
      <td>-0.002328</td>
      <td>-0.004294</td>
    </tr>
    <tr>
      <th>new_cases</th>
      <td>0.907625</td>
      <td>1.000000</td>
      <td>0.882493</td>
      <td>0.935345</td>
      <td>0.038111</td>
      <td>0.043059</td>
      <td>0.048081</td>
      <td>0.053932</td>
      <td>0.111741</td>
      <td>0.633411</td>
      <td>-0.019680</td>
      <td>0.023766</td>
      <td>0.023398</td>
      <td>0.021609</td>
      <td>0.015252</td>
      <td>-0.027491</td>
      <td>-0.033499</td>
      <td>0.017300</td>
      <td>0.000605</td>
      <td>-0.004228</td>
      <td>-0.009356</td>
    </tr>
    <tr>
      <th>total_deaths</th>
      <td>0.990031</td>
      <td>0.882493</td>
      <td>1.000000</td>
      <td>0.796899</td>
      <td>0.069334</td>
      <td>0.022502</td>
      <td>0.134849</td>
      <td>0.058148</td>
      <td>0.098758</td>
      <td>0.534678</td>
      <td>-0.017217</td>
      <td>0.036963</td>
      <td>0.043504</td>
      <td>0.043733</td>
      <td>0.017758</td>
      <td>-0.025642</td>
      <td>-0.046849</td>
      <td>-0.000596</td>
      <td>0.016877</td>
      <td>-0.008880</td>
      <td>-0.006940</td>
    </tr>
    <tr>
      <th>new_deaths</th>
      <td>0.804693</td>
      <td>0.935345</td>
      <td>0.796899</td>
      <td>1.000000</td>
      <td>0.044048</td>
      <td>0.037763</td>
      <td>0.082606</td>
      <td>0.101375</td>
      <td>0.104486</td>
      <td>0.589340</td>
      <td>-0.019301</td>
      <td>0.034492</td>
      <td>0.041111</td>
      <td>0.040624</td>
      <td>0.018149</td>
      <td>-0.027958</td>
      <td>-0.049374</td>
      <td>0.003112</td>
      <td>0.014164</td>
      <td>-0.014241</td>
      <td>-0.010768</td>
    </tr>
    <tr>
      <th>total_cases_per_million</th>
      <td>0.059672</td>
      <td>0.038111</td>
      <td>0.069334</td>
      <td>0.044048</td>
      <td>1.000000</td>
      <td>0.371221</td>
      <td>0.707395</td>
      <td>0.238842</td>
      <td>0.170376</td>
      <td>-0.036672</td>
      <td>0.074563</td>
      <td>0.248323</td>
      <td>0.218413</td>
      <td>0.221008</td>
      <td>0.343841</td>
      <td>-0.175675</td>
      <td>-0.228723</td>
      <td>-0.016315</td>
      <td>0.217735</td>
      <td>-0.064022</td>
      <td>0.071563</td>
    </tr>
    <tr>
      <th>new_cases_per_million</th>
      <td>0.026590</td>
      <td>0.043059</td>
      <td>0.022502</td>
      <td>0.037763</td>
      <td>0.371221</td>
      <td>1.000000</td>
      <td>0.205754</td>
      <td>0.175513</td>
      <td>0.173674</td>
      <td>-0.020604</td>
      <td>0.051333</td>
      <td>0.149447</td>
      <td>0.084576</td>
      <td>0.085995</td>
      <td>0.305669</td>
      <td>-0.137989</td>
      <td>-0.159231</td>
      <td>0.038454</td>
      <td>0.100288</td>
      <td>-0.041050</td>
      <td>0.029304</td>
    </tr>
    <tr>
      <th>total_deaths_per_million</th>
      <td>0.087117</td>
      <td>0.048081</td>
      <td>0.134849</td>
      <td>0.082606</td>
      <td>0.707395</td>
      <td>0.205754</td>
      <td>1.000000</td>
      <td>0.352267</td>
      <td>0.128779</td>
      <td>-0.019136</td>
      <td>0.017285</td>
      <td>0.232389</td>
      <td>0.270789</td>
      <td>0.281061</td>
      <td>0.206233</td>
      <td>-0.121843</td>
      <td>-0.211833</td>
      <td>-0.084857</td>
      <td>0.252208</td>
      <td>-0.059725</td>
      <td>0.057992</td>
    </tr>
    <tr>
      <th>new_deaths_per_million</th>
      <td>0.043499</td>
      <td>0.053932</td>
      <td>0.058148</td>
      <td>0.101375</td>
      <td>0.238842</td>
      <td>0.175513</td>
      <td>0.352267</td>
      <td>1.000000</td>
      <td>0.113149</td>
      <td>-0.011243</td>
      <td>0.010782</td>
      <td>0.201079</td>
      <td>0.235289</td>
      <td>0.242979</td>
      <td>0.139483</td>
      <td>-0.115243</td>
      <td>-0.180665</td>
      <td>-0.060852</td>
      <td>0.212053</td>
      <td>-0.062233</td>
      <td>0.040321</td>
    </tr>
    <tr>
      <th>stringency_index</th>
      <td>0.098873</td>
      <td>0.111741</td>
      <td>0.098758</td>
      <td>0.104486</td>
      <td>0.170376</td>
      <td>0.173674</td>
      <td>0.128779</td>
      <td>0.113149</td>
      <td>1.000000</td>
      <td>-0.035481</td>
      <td>-0.024091</td>
      <td>-0.214348</td>
      <td>-0.194098</td>
      <td>-0.201418</td>
      <td>-0.220012</td>
      <td>0.133959</td>
      <td>0.120986</td>
      <td>0.026397</td>
      <td>-0.123183</td>
      <td>0.039476</td>
      <td>-0.106730</td>
    </tr>
    <tr>
      <th>population</th>
      <td>0.552607</td>
      <td>0.633411</td>
      <td>0.534678</td>
      <td>0.589340</td>
      <td>-0.036672</td>
      <td>-0.020604</td>
      <td>-0.019136</td>
      <td>-0.011243</td>
      <td>-0.035481</td>
      <td>1.000000</td>
      <td>-0.025050</td>
      <td>-0.014543</td>
      <td>-0.026351</td>
      <td>-0.032263</td>
      <td>-0.057237</td>
      <td>-0.004185</td>
      <td>-0.000812</td>
      <td>0.022867</td>
      <td>-0.084393</td>
      <td>0.025822</td>
      <td>-0.031753</td>
    </tr>
    <tr>
      <th>population_density</th>
      <td>-0.017212</td>
      <td>-0.019680</td>
      <td>-0.017217</td>
      <td>-0.019301</td>
      <td>0.074563</td>
      <td>0.051333</td>
      <td>0.017285</td>
      <td>0.010782</td>
      <td>-0.024091</td>
      <td>-0.025050</td>
      <td>1.000000</td>
      <td>0.163888</td>
      <td>0.073021</td>
      <td>0.044126</td>
      <td>0.311339</td>
      <td>-0.013442</td>
      <td>-0.174624</td>
      <td>0.011360</td>
      <td>-0.076867</td>
      <td>-0.002682</td>
      <td>0.329226</td>
    </tr>
    <tr>
      <th>median_age</th>
      <td>0.028564</td>
      <td>0.023766</td>
      <td>0.036963</td>
      <td>0.034492</td>
      <td>0.248323</td>
      <td>0.149447</td>
      <td>0.232389</td>
      <td>0.201079</td>
      <td>-0.214348</td>
      <td>-0.014543</td>
      <td>0.163888</td>
      <td>1.000000</td>
      <td>0.907955</td>
      <td>0.893803</td>
      <td>0.610401</td>
      <td>-0.680899</td>
      <td>-0.356446</td>
      <td>0.076149</td>
      <td>0.682293</td>
      <td>0.168650</td>
      <td>0.660018</td>
    </tr>
    <tr>
      <th>aged_65_older</th>
      <td>0.029799</td>
      <td>0.023398</td>
      <td>0.043504</td>
      <td>0.041111</td>
      <td>0.218413</td>
      <td>0.084576</td>
      <td>0.270789</td>
      <td>0.235289</td>
      <td>-0.194098</td>
      <td>-0.026351</td>
      <td>0.073021</td>
      <td>0.907955</td>
      <td>1.000000</td>
      <td>0.994216</td>
      <td>0.453285</td>
      <td>-0.554519</td>
      <td>-0.354093</td>
      <td>-0.161165</td>
      <td>0.778360</td>
      <td>0.060770</td>
      <td>0.648285</td>
    </tr>
    <tr>
      <th>aged_70_older</th>
      <td>0.028719</td>
      <td>0.021609</td>
      <td>0.043733</td>
      <td>0.040624</td>
      <td>0.221008</td>
      <td>0.085995</td>
      <td>0.281061</td>
      <td>0.242979</td>
      <td>-0.201418</td>
      <td>-0.032263</td>
      <td>0.044126</td>
      <td>0.893803</td>
      <td>0.994216</td>
      <td>1.000000</td>
      <td>0.445106</td>
      <td>-0.535142</td>
      <td>-0.361768</td>
      <td>-0.190296</td>
      <td>0.784293</td>
      <td>0.064296</td>
      <td>0.650374</td>
    </tr>
    <tr>
      <th>gdp_per_capita</th>
      <td>0.016983</td>
      <td>0.015252</td>
      <td>0.017758</td>
      <td>0.018149</td>
      <td>0.343841</td>
      <td>0.305669</td>
      <td>0.206233</td>
      <td>0.139483</td>
      <td>-0.220012</td>
      <td>-0.057237</td>
      <td>0.311339</td>
      <td>0.610401</td>
      <td>0.453285</td>
      <td>0.445106</td>
      <td>1.000000</td>
      <td>-0.484366</td>
      <td>-0.493594</td>
      <td>0.211156</td>
      <td>0.329673</td>
      <td>-0.148443</td>
      <td>0.248837</td>
    </tr>
    <tr>
      <th>extreme_poverty</th>
      <td>-0.025413</td>
      <td>-0.027491</td>
      <td>-0.025642</td>
      <td>-0.027958</td>
      <td>-0.175675</td>
      <td>-0.137989</td>
      <td>-0.121843</td>
      <td>-0.115243</td>
      <td>0.133959</td>
      <td>-0.004185</td>
      <td>-0.013442</td>
      <td>-0.680899</td>
      <td>-0.554519</td>
      <td>-0.535142</td>
      <td>-0.484366</td>
      <td>1.000000</td>
      <td>0.188561</td>
      <td>-0.374315</td>
      <td>-0.375238</td>
      <td>-0.195320</td>
      <td>-0.401701</td>
    </tr>
    <tr>
      <th>cvd_death_rate</th>
      <td>-0.035107</td>
      <td>-0.033499</td>
      <td>-0.046849</td>
      <td>-0.049374</td>
      <td>-0.228723</td>
      <td>-0.159231</td>
      <td>-0.211833</td>
      <td>-0.180665</td>
      <td>0.120986</td>
      <td>-0.000812</td>
      <td>-0.174624</td>
      <td>-0.356446</td>
      <td>-0.354093</td>
      <td>-0.361768</td>
      <td>-0.493594</td>
      <td>0.188561</td>
      <td>1.000000</td>
      <td>0.074682</td>
      <td>-0.215974</td>
      <td>0.460542</td>
      <td>-0.024100</td>
    </tr>
    <tr>
      <th>diabetes_prevalence</th>
      <td>0.012486</td>
      <td>0.017300</td>
      <td>-0.000596</td>
      <td>0.003112</td>
      <td>-0.016315</td>
      <td>0.038454</td>
      <td>-0.084857</td>
      <td>-0.060852</td>
      <td>0.026397</td>
      <td>0.022867</td>
      <td>0.011360</td>
      <td>0.076149</td>
      <td>-0.161165</td>
      <td>-0.190296</td>
      <td>0.211156</td>
      <td>-0.374315</td>
      <td>0.074682</td>
      <td>1.000000</td>
      <td>-0.173618</td>
      <td>0.155261</td>
      <td>-0.159378</td>
    </tr>
    <tr>
      <th>female_smokers</th>
      <td>0.005616</td>
      <td>0.000605</td>
      <td>0.016877</td>
      <td>0.014164</td>
      <td>0.217735</td>
      <td>0.100288</td>
      <td>0.252208</td>
      <td>0.212053</td>
      <td>-0.123183</td>
      <td>-0.084393</td>
      <td>-0.076867</td>
      <td>0.682293</td>
      <td>0.778360</td>
      <td>0.784293</td>
      <td>0.329673</td>
      <td>-0.375238</td>
      <td>-0.215974</td>
      <td>-0.173618</td>
      <td>1.000000</td>
      <td>0.142621</td>
      <td>0.472443</td>
    </tr>
    <tr>
      <th>male_smokers</th>
      <td>-0.002328</td>
      <td>-0.004228</td>
      <td>-0.008880</td>
      <td>-0.014241</td>
      <td>-0.064022</td>
      <td>-0.041050</td>
      <td>-0.059725</td>
      <td>-0.062233</td>
      <td>0.039476</td>
      <td>0.025822</td>
      <td>-0.002682</td>
      <td>0.168650</td>
      <td>0.060770</td>
      <td>0.064296</td>
      <td>-0.148443</td>
      <td>-0.195320</td>
      <td>0.460542</td>
      <td>0.155261</td>
      <td>0.142621</td>
      <td>1.000000</td>
      <td>0.316532</td>
    </tr>
    <tr>
      <th>hospital_beds_per_100k</th>
      <td>-0.004294</td>
      <td>-0.009356</td>
      <td>-0.006940</td>
      <td>-0.010768</td>
      <td>0.071563</td>
      <td>0.029304</td>
      <td>0.057992</td>
      <td>0.040321</td>
      <td>-0.106730</td>
      <td>-0.031753</td>
      <td>0.329226</td>
      <td>0.660018</td>
      <td>0.648285</td>
      <td>0.650374</td>
      <td>0.248837</td>
      <td>-0.401701</td>
      <td>-0.024100</td>
      <td>-0.159378</td>
      <td>0.472443</td>
      <td>0.316532</td>
      <td>1.000000</td>
    </tr>
  </tbody>
</table>
</div>



## Heatmap on the correlations between features in the data


```python
# Heatmap on the correlations between features in the loan data
data_drop_correlations = data_drop.corr()
plt.figure(figsize=(20, 20,))
plt.imshow(data_drop_correlations, cmap=None, interpolation='none', aspect='auto')
plt.colorbar()
plt.xticks(range(len(data_drop_correlations)), data_drop_correlations.columns, rotation='vertical')
plt.yticks(range(len(data_drop_correlations)), data_drop_correlations.columns);
plt.suptitle('Loan correlations Heat Map', fontsize=30, fontweight='bold');
plt.show()
```




    <Figure size 1440x1440 with 0 Axes>






    <matplotlib.image.AxesImage at 0x12ae16dd8>






    <matplotlib.colorbar.Colorbar at 0x12adf9668>






    ([<matplotlib.axis.XTick at 0x12a1697b8>,
      <matplotlib.axis.XTick at 0x12a169710>,
      <matplotlib.axis.XTick at 0x12a18b3c8>,
      <matplotlib.axis.XTick at 0x12adf9e80>,
      <matplotlib.axis.XTick at 0x126c69470>,
      <matplotlib.axis.XTick at 0x126c69908>,
      <matplotlib.axis.XTick at 0x126c69da0>,
      <matplotlib.axis.XTick at 0x126c69a58>,
      <matplotlib.axis.XTick at 0x126c690b8>,
      <matplotlib.axis.XTick at 0x126c8b668>,
      <matplotlib.axis.XTick at 0x126c8bb00>,
      <matplotlib.axis.XTick at 0x126c8be80>,
      <matplotlib.axis.XTick at 0x126c86470>,
      <matplotlib.axis.XTick at 0x126c86908>,
      <matplotlib.axis.XTick at 0x126c86dd8>,
      <matplotlib.axis.XTick at 0x126c922b0>,
      <matplotlib.axis.XTick at 0x126c92748>,
      <matplotlib.axis.XTick at 0x126c869e8>,
      <matplotlib.axis.XTick at 0x126c8b5c0>,
      <matplotlib.axis.XTick at 0x126c92358>,
      <matplotlib.axis.XTick at 0x126c92dd8>],
     [Text(0, 0, 'total_cases'),
      Text(0, 0, 'new_cases'),
      Text(0, 0, 'total_deaths'),
      Text(0, 0, 'new_deaths'),
      Text(0, 0, 'total_cases_per_million'),
      Text(0, 0, 'new_cases_per_million'),
      Text(0, 0, 'total_deaths_per_million'),
      Text(0, 0, 'new_deaths_per_million'),
      Text(0, 0, 'stringency_index'),
      Text(0, 0, 'population'),
      Text(0, 0, 'population_density'),
      Text(0, 0, 'median_age'),
      Text(0, 0, 'aged_65_older'),
      Text(0, 0, 'aged_70_older'),
      Text(0, 0, 'gdp_per_capita'),
      Text(0, 0, 'extreme_poverty'),
      Text(0, 0, 'cvd_death_rate'),
      Text(0, 0, 'diabetes_prevalence'),
      Text(0, 0, 'female_smokers'),
      Text(0, 0, 'male_smokers'),
      Text(0, 0, 'hospital_beds_per_100k')])






    ([<matplotlib.axis.YTick at 0x12a169b70>,
      <matplotlib.axis.YTick at 0x12a1697f0>,
      <matplotlib.axis.YTick at 0x126c277f0>,
      <matplotlib.axis.YTick at 0x126c84908>,
      <matplotlib.axis.YTick at 0x126c84da0>,
      <matplotlib.axis.YTick at 0x126c79128>,
      <matplotlib.axis.YTick at 0x126c79550>,
      <matplotlib.axis.YTick at 0x126c84c50>,
      <matplotlib.axis.YTick at 0x126c92d30>,
      <matplotlib.axis.YTick at 0x126c79908>,
      <matplotlib.axis.YTick at 0x126c79160>,
      <matplotlib.axis.YTick at 0x126c8c160>,
      <matplotlib.axis.YTick at 0x126c8c5c0>,
      <matplotlib.axis.YTick at 0x126c8ca58>,
      <matplotlib.axis.YTick at 0x126c8cef0>,
      <matplotlib.axis.YTick at 0x126c953c8>,
      <matplotlib.axis.YTick at 0x126c95860>,
      <matplotlib.axis.YTick at 0x126c8ca20>,
      <matplotlib.axis.YTick at 0x126c79f60>,
      <matplotlib.axis.YTick at 0x126c95ba8>,
      <matplotlib.axis.YTick at 0x126c950b8>],
     [Text(0, 0, 'total_cases'),
      Text(0, 0, 'new_cases'),
      Text(0, 0, 'total_deaths'),
      Text(0, 0, 'new_deaths'),
      Text(0, 0, 'total_cases_per_million'),
      Text(0, 0, 'new_cases_per_million'),
      Text(0, 0, 'total_deaths_per_million'),
      Text(0, 0, 'new_deaths_per_million'),
      Text(0, 0, 'stringency_index'),
      Text(0, 0, 'population'),
      Text(0, 0, 'population_density'),
      Text(0, 0, 'median_age'),
      Text(0, 0, 'aged_65_older'),
      Text(0, 0, 'aged_70_older'),
      Text(0, 0, 'gdp_per_capita'),
      Text(0, 0, 'extreme_poverty'),
      Text(0, 0, 'cvd_death_rate'),
      Text(0, 0, 'diabetes_prevalence'),
      Text(0, 0, 'female_smokers'),
      Text(0, 0, 'male_smokers'),
      Text(0, 0, 'hospital_beds_per_100k')])






    Text(0.5, 0.98, 'Loan correlations Heat Map')




![png](assets/images/covid/output_75_6.png)



```python
from pandas.util.testing import assert_frame_equal
```


```python
myBasicCorr = data_drop.corr()
sns.heatmap(myBasicCorr);
```


![png](assets/images/covid/output_77_0.png)


## The is stronger Correlation between female smokers and age above 65 years
From the heat map above, there is an indication of a correlation between female smokers and old age. In this data set focus is on ages 65 and 70 and/or older. Lets use  a Scatter plot of female smokers against age to focus more on these two variables



```python
data.plot(kind='scatter', x='female_smokers', y='aged_65_older');
```


![png](assets/images/covid/output_79_0.png)



```python
data.plot(kind='scatter', x='female_smokers', y='aged_70_older');
```


![png](assets/images/covid/output_80_0.png)


## Correlation on female smokers vs age from other sources


```python
from IPython.display import IFrame
IFrame('https://www.ncbi.nlm.nih.gov/pmc/articles/PMC1175093/', width=800, height=450)

```





<iframe
    width="800"
    height="450"
    src="https://www.ncbi.nlm.nih.gov/pmc/articles/PMC1175093/"
    frameborder="0"
    allowfullscreen
></iframe>





```python
from IPython.display import IFrame
IFrame('https://en.wikipedia.org/wiki/Corona_virus', width=800, height=450)

```





<iframe
    width="800"
    height="450"
    src="https://en.wikipedia.org/wiki/Corona_virus"
    frameborder="0"
    allowfullscreen
></iframe>





```python
from IPython.display import YouTubeVideo
YouTubeVideo('mCa0JXEwDEk', width=800, height=300)
```





<iframe
    width="800"
    height="300"
    src="https://www.youtube.com/embed/mCa0JXEwDEk"
    frameborder="0"
    allowfullscreen
></iframe>





```python

```
