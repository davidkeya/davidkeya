---
header:
  overlay_image: /assets/images/sql_pandas/sql_pandas.jpg
  caption: "Photo credit: [**casparrubin**](https://unsplash.com)"
permalink: /portfolio/Sql_Pandas/
date: 2021-04-13
toc: true
toc_label: "Contents"
---

# APPLE STOCK PRICES ANALYSIS USING SQL AND PANDAS

Here we are going to explore and manipulate the Apple stock dataset. The data was sourced from Google finance in January of 2014.There is one row for each day as indicated in the date field.
- **open and close**  : Opening and closing prices of stock on the particular day.
- **high and low**    : High and low prices on that day.
- **volume**          : Number of shares traded on that day

## Setting up Jupyter notebook display


```python
# Import pandas a python library
import pandas as pd

# Display more rows
pd.set_option('display.max_rows', 15000)
pd.set_option('display.max_columns', 1000)
pd.set_option('display.width', 1000)

# Increase display size
from IPython.core.display import display, HTML
display(HTML("<style>.container {width:90% !important;}</style>"))
```


<style>.container {width:90% !important;}</style>


## Getting Started: Load ipython-sql and import Create_engine


```python
# Load ipython-sql, using the following magic command:
%load_ext sql
```


```python
# Next, we will only need the create_engine() function from sqlalchemy so let’s import that with the following line:
from sqlalchemy import create_engine
```

## Connecting to a PostgreSQL the database
Once we’ve laid the groundwork, we can now connect to a PostgreSQL database!
The PostgreSQL database contains housing report data projects data in the portfolio database.


```python
# Use the following format to connect ipython-sql to a local database named portfolio.
%sql postgresql://postgres:1372Sql$@localhost/portfolio
```


```python
# To connect sqlalchemy to the database
engine = create_engine('postgresql://postgres:1372Sql$@localhost/portfolio')
```

## An exploration of the live table storing all of the data for Apple Stock Prices


```sql
%%sql
SELECT * FROM apple_stock_prices
LIMIT 5
```

     * postgresql://postgres:***@localhost/portfolio
    5 rows affected.





<table>
    <tr>
        <th>date</th>
        <th>year</th>
        <th>month</th>
        <th>open</th>
        <th>high</th>
        <th>low</th>
        <th>close</th>
        <th>volume</th>
        <th>id</th>
    </tr>
    <tr>
        <td>1/30/14</td>
        <td>2014.0</td>
        <td>1.0</td>
        <td>502.54</td>
        <td>506.5</td>
        <td>496.7</td>
        <td>499.78</td>
        <td>24182996.0</td>
        <td>1</td>
    </tr>
    <tr>
        <td>1/29/14</td>
        <td>2014.0</td>
        <td>1.0</td>
        <td>503.95</td>
        <td>507.37</td>
        <td>498.62</td>
        <td>500.75</td>
        <td>17991828.0</td>
        <td>2</td>
    </tr>
    <tr>
        <td>1/28/14</td>
        <td>2014.0</td>
        <td>1.0</td>
        <td>508.76</td>
        <td>515.0</td>
        <td>502.07</td>
        <td>506.5</td>
        <td>38119084.0</td>
        <td>3</td>
    </tr>
    <tr>
        <td>1/27/14</td>
        <td>2014.0</td>
        <td>1.0</td>
        <td>550.07</td>
        <td>554.8</td>
        <td>545.75</td>
        <td>550.5</td>
        <td>20602736.0</td>
        <td>4</td>
    </tr>
    <tr>
        <td>1/24/14</td>
        <td>2014.0</td>
        <td>1.0</td>
        <td>554.0</td>
        <td>555.62</td>
        <td>544.75</td>
        <td>546.07</td>
        <td>15483491.0</td>
        <td>5</td>
    </tr>
</table>



## Basic Data Exploration

### A count of all rows


```sql
%%sql
SELECT COUNT(*) FROM apple_stock_prices

```

     * postgresql://postgres:***@localhost/portfolio
    1 rows affected.





<table>
    <tr>
        <th>count</th>
    </tr>
    <tr>
        <td>3555</td>
    </tr>
</table>



### Counting Individual Columns


```sql
%%sql
SELECT COUNT(high) FROM apple_stock_prices
```

     * postgresql://postgres:***@localhost/portfolio
    1 rows affected.





<table>
    <tr>
        <th>count</th>
    </tr>
    <tr>
        <td>3531</td>
    </tr>
</table>



### Non null rows in the 'low' column


```sql
%%sql
SELECT COUNT(low) AS low FROM apple_stock_prices

```

     * postgresql://postgres:***@localhost/portfolio
    1 rows affected.





<table>
    <tr>
        <th>low</th>
    </tr>
    <tr>
        <td>3535</td>
    </tr>
</table>



### A count of non numerical columns


```sql
%%sql
SELECT COUNT(date) AS date_range FROM apple_stock_prices
```

     * postgresql://postgres:***@localhost/portfolio
    1 rows affected.





<table>
    <tr>
        <th>date_range</th>
    </tr>
    <tr>
        <td>3555</td>
    </tr>
</table>




```sql
%%sql
SELECT COUNT(*) AS columns_date_range FROM apple_stock_prices
```

     * postgresql://postgres:***@localhost/portfolio
    1 rows affected.





<table>
    <tr>
        <th>columns_date_range</th>
    </tr>
    <tr>
        <td>3555</td>
    </tr>
</table>



### A Count for every single column


```sql
%%sql
SELECT COUNT(year), COUNT(month), COUNT(open), COUNT(high), COUNT(low), COUNT(close), COUNT(volume)
FROM apple_stock_prices
LIMIT 10
```

     * postgresql://postgres:***@localhost/portfolio
    1 rows affected.





<table>
    <tr>
        <th>count</th>
        <th>count_1</th>
        <th>count_2</th>
        <th>count_3</th>
        <th>count_4</th>
        <th>count_5</th>
        <th>count_6</th>
    </tr>
    <tr>
        <td>3555</td>
        <td>3555</td>
        <td>3541</td>
        <td>3531</td>
        <td>3535</td>
        <td>3555</td>
        <td>3547</td>
    </tr>
</table>




```sql
%%sql
SELECT COUNT(date) FROM apple_stock_prices
```

     * postgresql://postgres:***@localhost/portfolio
    1 rows affected.





<table>
    <tr>
        <th>count</th>
    </tr>
    <tr>
        <td>3555</td>
    </tr>
</table>




```sql
%%sql
SELECT COUNT(low) AS low
  FROM apple_stock_prices
```

     * postgresql://postgres:***@localhost/portfolio
    1 rows affected.





<table>
    <tr>
        <th>low</th>
    </tr>
    <tr>
        <td>3535</td>
    </tr>
</table>




```sql
%%sql
SELECT COUNT(year) AS year,
       COUNT(month) AS month,
       COUNT(open) AS open,
       COUNT(high) AS high,
       COUNT(low) AS low,
       COUNT(close) AS close,
       COUNT(volume) AS volume
  FROM apple_stock_prices
```

     * postgresql://postgres:***@localhost/portfolio
    1 rows affected.





<table>
    <tr>
        <th>year</th>
        <th>month</th>
        <th>open</th>
        <th>high</th>
        <th>low</th>
        <th>close</th>
        <th>volume</th>
    </tr>
    <tr>
        <td>3555</td>
        <td>3555</td>
        <td>3541</td>
        <td>3531</td>
        <td>3535</td>
        <td>3555</td>
        <td>3547</td>
    </tr>
</table>




```sql
%%sql
SELECT COUNT(year), COUNT(month), COUNT(open), COUNT(high), COUNT(low), COUNT(close), COUNT(volume)
FROM apple_stock_prices
```

     * postgresql://postgres:***@localhost/portfolio
    1 rows affected.





<table>
    <tr>
        <th>count</th>
        <th>count_1</th>
        <th>count_2</th>
        <th>count_3</th>
        <th>count_4</th>
        <th>count_5</th>
        <th>count_6</th>
    </tr>
    <tr>
        <td>3555</td>
        <td>3555</td>
        <td>3541</td>
        <td>3531</td>
        <td>3535</td>
        <td>3555</td>
        <td>3547</td>
    </tr>
</table>




```python

```

### Average Opening Price


```sql
%%sql
SELECT * FROM apple_stock_prices
LIMIT 2
```

     * postgresql://postgres:***@localhost/portfolio
    2 rows affected.





<table>
    <tr>
        <th>date</th>
        <th>year</th>
        <th>month</th>
        <th>open</th>
        <th>high</th>
        <th>low</th>
        <th>close</th>
        <th>volume</th>
        <th>id</th>
    </tr>
    <tr>
        <td>1/30/14</td>
        <td>2014.0</td>
        <td>1.0</td>
        <td>502.54</td>
        <td>506.5</td>
        <td>496.7</td>
        <td>499.78</td>
        <td>24182996.0</td>
        <td>1</td>
    </tr>
    <tr>
        <td>1/29/14</td>
        <td>2014.0</td>
        <td>1.0</td>
        <td>503.95</td>
        <td>507.37</td>
        <td>498.62</td>
        <td>500.75</td>
        <td>17991828.0</td>
        <td>2</td>
    </tr>
</table>




```sql
%%sql
SELECT SUM(open) AS sum_of_open, COUNT(open) AS count_of_open, (SUM(open)/COUNT(open)) AS Average_Opening_Price FROM apple_stock_prices
```

     * postgresql://postgres:***@localhost/portfolio
    1 rows affected.





<table>
    <tr>
        <th>sum_of_open</th>
        <th>count_of_open</th>
        <th>average_opening_price</th>
    </tr>
    <tr>
        <td>583484.0</td>
        <td>3541</td>
        <td>164.77944083592206</td>
    </tr>
</table>



### Apple's lowest stock price at the time of data collection


```sql
%%sql
SELECT MIN(low) AS lowest_stock_price FROM apple_stock_prices
```

     * postgresql://postgres:***@localhost/portfolio
    1 rows affected.





<table>
    <tr>
        <th>lowest_stock_price</th>
    </tr>
    <tr>
        <td>6.36</td>
    </tr>
</table>




```sql
%%sql
SELECT * FROM apple_stock_prices
LIMIT 2
```

     * postgresql://postgres:***@localhost/portfolio
    2 rows affected.





<table>
    <tr>
        <th>date</th>
        <th>year</th>
        <th>month</th>
        <th>open</th>
        <th>high</th>
        <th>low</th>
        <th>close</th>
        <th>volume</th>
        <th>id</th>
    </tr>
    <tr>
        <td>1/30/14</td>
        <td>2014.0</td>
        <td>1.0</td>
        <td>502.54</td>
        <td>506.5</td>
        <td>496.7</td>
        <td>499.78</td>
        <td>24182996.0</td>
        <td>1</td>
    </tr>
    <tr>
        <td>1/29/14</td>
        <td>2014.0</td>
        <td>1.0</td>
        <td>503.95</td>
        <td>507.37</td>
        <td>498.62</td>
        <td>500.75</td>
        <td>17991828.0</td>
        <td>2</td>
    </tr>
</table>



 ### Highest single-day increase in Apple's share value


```sql
%%sql
SELECT MAX(close - open)
  FROM apple_stock_prices
```

     * postgresql://postgres:***@localhost/portfolio
    1 rows affected.





<table>
    <tr>
        <th>max</th>
    </tr>
    <tr>
        <td>32.58</td>
    </tr>
</table>



### Average daily trade volume for Apple stock.




```sql
%%sql
SELECT AVG(volume) AS "Daily Trade Volume" FROM apple_stock_prices
```

     * postgresql://postgres:***@localhost/portfolio
    1 rows affected.





<table>
    <tr>
        <th>Daily Trade Volume</th>
    </tr>
    <tr>
        <td>20745814.356075555</td>
    </tr>
</table>



### Number of Entries for each Year


```sql
%%sql
SELECT year, COUNT(*) AS entry_count FROM apple_stock_prices
GROUP BY year
ORDER BY year
```

     * postgresql://postgres:***@localhost/portfolio
    15 rows affected.





<table>
    <tr>
        <th>year</th>
        <th>entry_count</th>
    </tr>
    <tr>
        <td>2000.0</td>
        <td>252</td>
    </tr>
    <tr>
        <td>2001.0</td>
        <td>248</td>
    </tr>
    <tr>
        <td>2002.0</td>
        <td>252</td>
    </tr>
    <tr>
        <td>2003.0</td>
        <td>252</td>
    </tr>
    <tr>
        <td>2004.0</td>
        <td>252</td>
    </tr>
    <tr>
        <td>2005.0</td>
        <td>252</td>
    </tr>
    <tr>
        <td>2006.0</td>
        <td>251</td>
    </tr>
    <tr>
        <td>2007.0</td>
        <td>251</td>
    </tr>
    <tr>
        <td>2008.0</td>
        <td>255</td>
    </tr>
    <tr>
        <td>2009.0</td>
        <td>257</td>
    </tr>
    <tr>
        <td>2010.0</td>
        <td>259</td>
    </tr>
    <tr>
        <td>2011.0</td>
        <td>252</td>
    </tr>
    <tr>
        <td>2012.0</td>
        <td>250</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>252</td>
    </tr>
    <tr>
        <td>2014.0</td>
        <td>20</td>
    </tr>
</table>




```python
# Store the querry results in variable
year_entries = %sql SELECT year, COUNT(*) AS entry_count FROM apple_stock_prices GROUP BY year ORDER BY year
```

     * postgresql://postgres:***@localhost/portfolio
    15 rows affected.



```python
# Convert the table into a pandas data frame

year_entries_df = year_entries.DataFrame()
year_entries_df
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
      <th>year</th>
      <th>entry_count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2000.0</td>
      <td>252</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2001.0</td>
      <td>248</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2002.0</td>
      <td>252</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2003.0</td>
      <td>252</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2004.0</td>
      <td>252</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2005.0</td>
      <td>252</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2006.0</td>
      <td>251</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2007.0</td>
      <td>251</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2008.0</td>
      <td>255</td>
    </tr>
    <tr>
      <th>9</th>
      <td>2009.0</td>
      <td>257</td>
    </tr>
    <tr>
      <th>10</th>
      <td>2010.0</td>
      <td>259</td>
    </tr>
    <tr>
      <th>11</th>
      <td>2011.0</td>
      <td>252</td>
    </tr>
    <tr>
      <th>12</th>
      <td>2012.0</td>
      <td>250</td>
    </tr>
    <tr>
      <th>13</th>
      <td>2013.0</td>
      <td>252</td>
    </tr>
    <tr>
      <th>14</th>
      <td>2014.0</td>
      <td>20</td>
    </tr>
  </tbody>
</table>
</div>



#### A visual of Yearly Entries


```python
year_entries_df.plot.bar(x='year', y='entry_count', figsize=(18,10));
```



![png](output_44_0.png)




```python
year_entries_df.plot.line(x='year', y='entry_count', figsize=(18,6), subplots=True, color={"entry_count": "orange"});
```



![png](output_45_0.png)



> Year 2014 had the least count, while 2010 had the highest


```sql
%%sql
SELECT * FROM apple_stock_prices
LIMIT 5

```

     * postgresql://postgres:***@localhost/portfolio
    5 rows affected.





<table>
    <tr>
        <th>date</th>
        <th>year</th>
        <th>month</th>
        <th>open</th>
        <th>high</th>
        <th>low</th>
        <th>close</th>
        <th>volume</th>
        <th>id</th>
    </tr>
    <tr>
        <td>1/30/14</td>
        <td>2014.0</td>
        <td>1.0</td>
        <td>502.54</td>
        <td>506.5</td>
        <td>496.7</td>
        <td>499.78</td>
        <td>24182996.0</td>
        <td>1</td>
    </tr>
    <tr>
        <td>1/29/14</td>
        <td>2014.0</td>
        <td>1.0</td>
        <td>503.95</td>
        <td>507.37</td>
        <td>498.62</td>
        <td>500.75</td>
        <td>17991828.0</td>
        <td>2</td>
    </tr>
    <tr>
        <td>1/28/14</td>
        <td>2014.0</td>
        <td>1.0</td>
        <td>508.76</td>
        <td>515.0</td>
        <td>502.07</td>
        <td>506.5</td>
        <td>38119084.0</td>
        <td>3</td>
    </tr>
    <tr>
        <td>1/27/14</td>
        <td>2014.0</td>
        <td>1.0</td>
        <td>550.07</td>
        <td>554.8</td>
        <td>545.75</td>
        <td>550.5</td>
        <td>20602736.0</td>
        <td>4</td>
    </tr>
    <tr>
        <td>1/24/14</td>
        <td>2014.0</td>
        <td>1.0</td>
        <td>554.0</td>
        <td>555.62</td>
        <td>544.75</td>
        <td>546.07</td>
        <td>15483491.0</td>
        <td>5</td>
    </tr>
</table>



### Total Number of shares traded each month


```sql
%%sql
SELECT month, COUNT(*) AS share_count FROM apple_stock_prices
GROUP BY month
ORDER BY 1
```

     * postgresql://postgres:***@localhost/portfolio
    12 rows affected.





<table>
    <tr>
        <th>month</th>
        <th>share_count</th>
    </tr>
    <tr>
        <td>1.0</td>
        <td>307</td>
    </tr>
    <tr>
        <td>2.0</td>
        <td>270</td>
    </tr>
    <tr>
        <td>3.0</td>
        <td>306</td>
    </tr>
    <tr>
        <td>4.0</td>
        <td>291</td>
    </tr>
    <tr>
        <td>5.0</td>
        <td>299</td>
    </tr>
    <tr>
        <td>6.0</td>
        <td>298</td>
    </tr>
    <tr>
        <td>7.0</td>
        <td>297</td>
    </tr>
    <tr>
        <td>8.0</td>
        <td>312</td>
    </tr>
    <tr>
        <td>9.0</td>
        <td>281</td>
    </tr>
    <tr>
        <td>10.0</td>
        <td>309</td>
    </tr>
    <tr>
        <td>11.0</td>
        <td>289</td>
    </tr>
    <tr>
        <td>12.0</td>
        <td>296</td>
    </tr>
</table>




```python
# Store the querry results in variable
month_shares = %sql SELECT month, COUNT(*) AS share_count FROM apple_stock_prices GROUP BY month ORDER BY 1
```

     * postgresql://postgres:***@localhost/portfolio
    12 rows affected.



```python
# Convert the table into a pandas data frame
month_shares_df = month_shares.DataFrame()
month_shares_df
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
      <th>month</th>
      <th>share_count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1.0</td>
      <td>307</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2.0</td>
      <td>270</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3.0</td>
      <td>306</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4.0</td>
      <td>291</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5.0</td>
      <td>299</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6.0</td>
      <td>298</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7.0</td>
      <td>297</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8.0</td>
      <td>312</td>
    </tr>
    <tr>
      <th>8</th>
      <td>9.0</td>
      <td>281</td>
    </tr>
    <tr>
      <th>9</th>
      <td>10.0</td>
      <td>309</td>
    </tr>
    <tr>
      <th>10</th>
      <td>11.0</td>
      <td>289</td>
    </tr>
    <tr>
      <th>11</th>
      <td>12.0</td>
      <td>296</td>
    </tr>
  </tbody>
</table>
</div>



#### A visual of Monthly Entries


```python
month_shares_df.plot.bar(x='month', y='share_count', figsize = (18,10));
```



![png](/assets/images/sql_pandas/output_53_0.png)




```python
month_shares_df.plot.line(x='month', y='share_count', figsize = (18,6), subplots=True, color={"share_count": "green"});
```



![png](/assets/images/sql_pandas/output_54_0.png)




```python
month_shares_df.plot();
```



![png](/assets/images/sql_pandas/output_55_0.png)



> The month of February had the least number of entries, while August had the highest.


```sql
%%sql
SELECT * FROM apple_stock_prices
LIMIT 5
```

     * postgresql://postgres:***@localhost/portfolio
    5 rows affected.





<table>
    <tr>
        <th>date</th>
        <th>year</th>
        <th>month</th>
        <th>open</th>
        <th>high</th>
        <th>low</th>
        <th>close</th>
        <th>volume</th>
        <th>id</th>
    </tr>
    <tr>
        <td>1/30/14</td>
        <td>2014.0</td>
        <td>1.0</td>
        <td>502.54</td>
        <td>506.5</td>
        <td>496.7</td>
        <td>499.78</td>
        <td>24182996.0</td>
        <td>1</td>
    </tr>
    <tr>
        <td>1/29/14</td>
        <td>2014.0</td>
        <td>1.0</td>
        <td>503.95</td>
        <td>507.37</td>
        <td>498.62</td>
        <td>500.75</td>
        <td>17991828.0</td>
        <td>2</td>
    </tr>
    <tr>
        <td>1/28/14</td>
        <td>2014.0</td>
        <td>1.0</td>
        <td>508.76</td>
        <td>515.0</td>
        <td>502.07</td>
        <td>506.5</td>
        <td>38119084.0</td>
        <td>3</td>
    </tr>
    <tr>
        <td>1/27/14</td>
        <td>2014.0</td>
        <td>1.0</td>
        <td>550.07</td>
        <td>554.8</td>
        <td>545.75</td>
        <td>550.5</td>
        <td>20602736.0</td>
        <td>4</td>
    </tr>
    <tr>
        <td>1/24/14</td>
        <td>2014.0</td>
        <td>1.0</td>
        <td>554.0</td>
        <td>555.62</td>
        <td>544.75</td>
        <td>546.07</td>
        <td>15483491.0</td>
        <td>5</td>
    </tr>
</table>



### Average daily price change in Apple stock, grouped by year.


```sql
%%sql
SELECT year, open, low, close, (open-close) AS price_change FROM apple_stock_prices
LIMIT 10
```

     * postgresql://postgres:***@localhost/portfolio
    10 rows affected.





<table>
    <tr>
        <th>year</th>
        <th>open</th>
        <th>low</th>
        <th>close</th>
        <th>price_change</th>
    </tr>
    <tr>
        <td>2014.0</td>
        <td>502.54</td>
        <td>496.7</td>
        <td>499.78</td>
        <td>2.7600098</td>
    </tr>
    <tr>
        <td>2014.0</td>
        <td>503.95</td>
        <td>498.62</td>
        <td>500.75</td>
        <td>3.2000122</td>
    </tr>
    <tr>
        <td>2014.0</td>
        <td>508.76</td>
        <td>502.07</td>
        <td>506.5</td>
        <td>2.2600098</td>
    </tr>
    <tr>
        <td>2014.0</td>
        <td>550.07</td>
        <td>545.75</td>
        <td>550.5</td>
        <td>-0.42999268</td>
    </tr>
    <tr>
        <td>2014.0</td>
        <td>554.0</td>
        <td>544.75</td>
        <td>546.07</td>
        <td>7.9299927</td>
    </tr>
    <tr>
        <td>2014.0</td>
        <td>549.94</td>
        <td>544.81</td>
        <td>556.18</td>
        <td>-6.23999</td>
    </tr>
    <tr>
        <td>2014.0</td>
        <td>550.91</td>
        <td>547.81</td>
        <td>551.51</td>
        <td>-0.6000366</td>
    </tr>
    <tr>
        <td>2014.0</td>
        <td>540.99</td>
        <td>540.42</td>
        <td>549.07</td>
        <td>-8.080017</td>
    </tr>
    <tr>
        <td>2014.0</td>
        <td>551.48</td>
        <td>539.9</td>
        <td>540.67</td>
        <td>10.809998</td>
    </tr>
    <tr>
        <td>2014.0</td>
        <td>554.9</td>
        <td>551.68</td>
        <td>554.25</td>
        <td>0.6500244</td>
    </tr>
</table>




```sql
%%sql
SELECT year, SUM (open-close) AS price_change FROM apple_stock_prices
GROUP BY year
```

     * postgresql://postgres:***@localhost/portfolio
    15 rows affected.





<table>
    <tr>
        <th>year</th>
        <th>price_change</th>
    </tr>
    <tr>
        <td>2001.0</td>
        <td>-6.490012</td>
    </tr>
    <tr>
        <td>2002.0</td>
        <td>-1.4900026</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>118.84003</td>
    </tr>
    <tr>
        <td>2004.0</td>
        <td>-14.889998</td>
    </tr>
    <tr>
        <td>2011.0</td>
        <td>12.539581</td>
    </tr>
    <tr>
        <td>2007.0</td>
        <td>28.850082</td>
    </tr>
    <tr>
        <td>2003.0</td>
        <td>-2.1699963</td>
    </tr>
    <tr>
        <td>2009.0</td>
        <td>-49.10002</td>
    </tr>
    <tr>
        <td>2005.0</td>
        <td>-11.629986</td>
    </tr>
    <tr>
        <td>2012.0</td>
        <td>150.7504</td>
    </tr>
    <tr>
        <td>2000.0</td>
        <td>-173.54001</td>
    </tr>
    <tr>
        <td>2006.0</td>
        <td>46.25996</td>
    </tr>
    <tr>
        <td>2014.0</td>
        <td>19.179993</td>
    </tr>
    <tr>
        <td>2010.0</td>
        <td>29.420197</td>
    </tr>
    <tr>
        <td>2008.0</td>
        <td>84.70016</td>
    </tr>
</table>




```python
# Store the querry results in a variable
price_change = %sql SELECT year, SUM (open-close) AS price_change FROM apple_stock_prices GROUP BY year

```

     * postgresql://postgres:***@localhost/portfolio
    15 rows affected.



```python
# Convert the table into a pandas data frame
price_change_df = price_change.DataFrame()

```


```python
price_change_df
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
      <th>year</th>
      <th>price_change</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2001.0</td>
      <td>-6.490012</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2002.0</td>
      <td>-1.490003</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2013.0</td>
      <td>118.840030</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2004.0</td>
      <td>-14.889998</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2011.0</td>
      <td>12.539581</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2007.0</td>
      <td>28.850082</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2003.0</td>
      <td>-2.169996</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2009.0</td>
      <td>-49.100020</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2005.0</td>
      <td>-11.629986</td>
    </tr>
    <tr>
      <th>9</th>
      <td>2012.0</td>
      <td>150.750400</td>
    </tr>
    <tr>
      <th>10</th>
      <td>2000.0</td>
      <td>-173.540010</td>
    </tr>
    <tr>
      <th>11</th>
      <td>2006.0</td>
      <td>46.259960</td>
    </tr>
    <tr>
      <th>12</th>
      <td>2014.0</td>
      <td>19.179993</td>
    </tr>
    <tr>
      <th>13</th>
      <td>2010.0</td>
      <td>29.420197</td>
    </tr>
    <tr>
      <th>14</th>
      <td>2008.0</td>
      <td>84.700160</td>
    </tr>
  </tbody>
</table>
</div>




```python
price_change_df.plot.bar(x='year', y='price_change', figsize = (24,5));
```



![png](/assets/images/sql_pandas/output_64_0.png)



***The above graph displays daily price changes of apple stock price grouped yearly. Maximum changes registered in 2013, 2012 and 2000, while the least changes in 2002, 2003, 2004 and 2005***


```python

```

 ### The lowest and highest prices that Apple stock achieved each month.


```sql
%%sql
SELECT month, MIN(low) AS lowest_price, MAX(high) AS highest_price FROM apple_stock_prices
GROUP BY month
ORDER BY month
```

     * postgresql://postgres:***@localhost/portfolio
    12 rows affected.





<table>
    <tr>
        <th>month</th>
        <th>lowest_price</th>
        <th>highest_price</th>
    </tr>
    <tr>
        <td>1.0</td>
        <td>6.78</td>
        <td>97.8</td>
    </tr>
    <tr>
        <td>2.0</td>
        <td>7.03</td>
        <td>99.94</td>
    </tr>
    <tr>
        <td>3.0</td>
        <td>7.02</td>
        <td>99.69</td>
    </tr>
    <tr>
        <td>4.0</td>
        <td>6.36</td>
        <td>99.95</td>
    </tr>
    <tr>
        <td>5.0</td>
        <td>7.0</td>
        <td>9.5</td>
    </tr>
    <tr>
        <td>6.0</td>
        <td>7.99</td>
        <td>9.84</td>
    </tr>
    <tr>
        <td>7.0</td>
        <td>6.9</td>
        <td>9.97</td>
    </tr>
    <tr>
        <td>8.0</td>
        <td>6.98</td>
        <td>9.96</td>
    </tr>
    <tr>
        <td>9.0</td>
        <td>7.02</td>
        <td>9.54</td>
    </tr>
    <tr>
        <td>10.0</td>
        <td>6.68</td>
        <td>99.25</td>
    </tr>
    <tr>
        <td>11.0</td>
        <td>7.5</td>
        <td>99.85</td>
    </tr>
    <tr>
        <td>12.0</td>
        <td>6.81</td>
        <td>99.49</td>
    </tr>
</table>




```python
# Store query results in a variable
monthly_price_variation = %sql SELECT month, MIN(low) AS lowest_price, MAX(high) AS highest_price FROM apple_stock_prices GROUP BY month ORDER BY month
```

     * postgresql://postgres:***@localhost/portfolio
    12 rows affected.



```python
# Convert the variable into a pandas dataframe
monthly_price_variation_df = monthly_price_variation.DataFrame()
monthly_price_variation_df
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
      <th>month</th>
      <th>lowest_price</th>
      <th>highest_price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1.0</td>
      <td>6.78</td>
      <td>97.8</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2.0</td>
      <td>7.03</td>
      <td>99.94</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3.0</td>
      <td>7.02</td>
      <td>99.69</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4.0</td>
      <td>6.36</td>
      <td>99.95</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5.0</td>
      <td>7.00</td>
      <td>9.5</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6.0</td>
      <td>7.99</td>
      <td>9.84</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7.0</td>
      <td>6.90</td>
      <td>9.97</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8.0</td>
      <td>6.98</td>
      <td>9.96</td>
    </tr>
    <tr>
      <th>8</th>
      <td>9.0</td>
      <td>7.02</td>
      <td>9.54</td>
    </tr>
    <tr>
      <th>9</th>
      <td>10.0</td>
      <td>6.68</td>
      <td>99.25</td>
    </tr>
    <tr>
      <th>10</th>
      <td>11.0</td>
      <td>7.50</td>
      <td>99.85</td>
    </tr>
    <tr>
      <th>11</th>
      <td>12.0</td>
      <td>6.81</td>
      <td>99.49</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Convert highest_price column into numeric
monthly_price_variation_df.highest_price=pd.to_numeric(monthly_price_variation_df.highest_price)
```


```python
# Set the figure size - handy for larger output
from matplotlib import pyplot as plt
plt.rcParams["figure.figsize"] = [10, 6]
# Set up with a higher resolution screen (useful on Mac)
%config InlineBackend.figure_format = 'retina'
```


```python
# A plot of the lowest and highest prices that Apple stock achieved each month
monthly_price_variation_df.plot(
    x="month", y=["lowest_price", "highest_price"], kind="bar"
)
plt.title("The lowest and highest prices that Apple stock achieved each month")
plt.xlabel("Month")
plt.ylabel("Stock Price");
```



![png](/assets/images/sql_pandas/output_73_0.png)



**A smaller variation noted in the months of May, June, July, August and September**
