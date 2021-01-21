---
title:  "Running Basic SQL Queries From a Jupyter Notebook (With Examples)"
category: posts
date: 2021-01-20
excerpt: "Here’s How to Run Basic SQL Queries From a Jupyter Notebook (With Examples)"
---


## Data
Real data from the U.S. Census. This dataset shows the number of completed housing units in major regions of the United States. The table has a column for each region. The values in each row represent the number of housing units completed in thousands during the corresponding month. The data was collected in August 2014 and can be accessed at the U.S. Census website.

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
# Use the following format to connect ipython-sql to the portfolio database.
%sql postgresql://postgres:1372Sql$@localhost/portfolio
```


```python
# To connect sqlalchemy to the database
engine = create_engine('postgresql://postgres:1372Sql$@localhost/portfolio')
```

## An exploration of the live table storing all of the Housing Units data



```sql
%%sql
SELECT * FROM housing_units
LIMIT 10
```

     * postgresql://postgres:***@localhost/portfolio
    10 rows affected.





<table>
    <tr>
        <th>year</th>
        <th>month</th>
        <th>month_name</th>
        <th>south</th>
        <th>west</th>
        <th>midwest</th>
        <th>northeast</th>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>1.0</td>
        <td>January</td>
        <td>35.6</td>
        <td>17.0</td>
        <td>22.6</td>
        <td>12.9</td>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>2.0</td>
        <td>February</td>
        <td>31.5</td>
        <td>18.6</td>
        <td>23.3</td>
        <td>9.7</td>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>3.0</td>
        <td>March</td>
        <td>42.5</td>
        <td>17.4</td>
        <td>24.4</td>
        <td>10.7</td>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>4.0</td>
        <td>April</td>
        <td>42.9</td>
        <td>20.6</td>
        <td>27.0</td>
        <td>12.0</td>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>5.0</td>
        <td>May</td>
        <td>46.2</td>
        <td>20.0</td>
        <td>25.1</td>
        <td>20.0</td>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>6.0</td>
        <td>June</td>
        <td>37.7</td>
        <td>23.2</td>
        <td>26.9</td>
        <td>16.8</td>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>7.0</td>
        <td>July</td>
        <td>50.3</td>
        <td>21.2</td>
        <td>25.7</td>
        <td>20.1</td>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>8.0</td>
        <td>August</td>
        <td>46.6</td>
        <td>23.1</td>
        <td>33.4</td>
        <td>15.3</td>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>9.0</td>
        <td>September</td>
        <td>48.7</td>
        <td>22.0</td>
        <td>37.9</td>
        <td>27.0</td>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>10.0</td>
        <td>October</td>
        <td>50.2</td>
        <td>23.0</td>
        <td>34.2</td>
        <td>20.5</td>
    </tr>
</table>



## Sql Limit


```sql
%%sql
SELECT south, west AS "West Region" FROM housing_units
LIMIT 10
```

     * postgresql://postgres:***@localhost/portfolio
    10 rows affected.





<table>
    <tr>
        <th>south</th>
        <th>West Region</th>
    </tr>
    <tr>
        <td>35.6</td>
        <td>17.0</td>
    </tr>
    <tr>
        <td>31.5</td>
        <td>18.6</td>
    </tr>
    <tr>
        <td>42.5</td>
        <td>17.4</td>
    </tr>
    <tr>
        <td>42.9</td>
        <td>20.6</td>
    </tr>
    <tr>
        <td>46.2</td>
        <td>20.0</td>
    </tr>
    <tr>
        <td>37.7</td>
        <td>23.2</td>
    </tr>
    <tr>
        <td>50.3</td>
        <td>21.2</td>
    </tr>
    <tr>
        <td>46.6</td>
        <td>23.1</td>
    </tr>
    <tr>
        <td>48.7</td>
        <td>22.0</td>
    </tr>
    <tr>
        <td>50.2</td>
        <td>23.0</td>
    </tr>
</table>



## Capitalize first letter of column


```sql
%%sql
SELECT year AS "Year", month AS "Month", month_name AS "Month_name", south AS "South", west AS "West", midwest AS "Midwest", northeast AS Northeast FROM housing_units
LIMIT 15
```

     * postgresql://postgres:***@localhost/portfolio
    15 rows affected.





<table>
    <tr>
        <th>Year</th>
        <th>Month</th>
        <th>Month_name</th>
        <th>South</th>
        <th>West</th>
        <th>Midwest</th>
        <th>northeast</th>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>1.0</td>
        <td>January</td>
        <td>35.6</td>
        <td>17.0</td>
        <td>22.6</td>
        <td>12.9</td>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>2.0</td>
        <td>February</td>
        <td>31.5</td>
        <td>18.6</td>
        <td>23.3</td>
        <td>9.7</td>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>3.0</td>
        <td>March</td>
        <td>42.5</td>
        <td>17.4</td>
        <td>24.4</td>
        <td>10.7</td>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>4.0</td>
        <td>April</td>
        <td>42.9</td>
        <td>20.6</td>
        <td>27.0</td>
        <td>12.0</td>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>5.0</td>
        <td>May</td>
        <td>46.2</td>
        <td>20.0</td>
        <td>25.1</td>
        <td>20.0</td>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>6.0</td>
        <td>June</td>
        <td>37.7</td>
        <td>23.2</td>
        <td>26.9</td>
        <td>16.8</td>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>7.0</td>
        <td>July</td>
        <td>50.3</td>
        <td>21.2</td>
        <td>25.7</td>
        <td>20.1</td>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>8.0</td>
        <td>August</td>
        <td>46.6</td>
        <td>23.1</td>
        <td>33.4</td>
        <td>15.3</td>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>9.0</td>
        <td>September</td>
        <td>48.7</td>
        <td>22.0</td>
        <td>37.9</td>
        <td>27.0</td>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>10.0</td>
        <td>October</td>
        <td>50.2</td>
        <td>23.0</td>
        <td>34.2</td>
        <td>20.5</td>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>11.0</td>
        <td>November</td>
        <td>45.7</td>
        <td>18.4</td>
        <td>35.8</td>
        <td>14.4</td>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>12.0</td>
        <td>December</td>
        <td>49.8</td>
        <td>21.6</td>
        <td>31.2</td>
        <td>19.5</td>
    </tr>
    <tr>
        <td>1969.0</td>
        <td>1.0</td>
        <td>January</td>
        <td>40.1</td>
        <td>19.7</td>
        <td>18.0</td>
        <td>11.0</td>
    </tr>
    <tr>
        <td>1969.0</td>
        <td>2.0</td>
        <td>February</td>
        <td>34.8</td>
        <td>23.0</td>
        <td>23.3</td>
        <td>14.9</td>
    </tr>
    <tr>
        <td>1969.0</td>
        <td>3.0</td>
        <td>March</td>
        <td>53.3</td>
        <td>21.1</td>
        <td>23.5</td>
        <td>17.0</td>
    </tr>
</table>



## Sql Where


```sql
%%sql
SELECT * FROM housing_units
WHERE month = 1
LIMIT 10
```

     * postgresql://postgres:***@localhost/portfolio
    10 rows affected.





<table>
    <tr>
        <th>year</th>
        <th>month</th>
        <th>month_name</th>
        <th>south</th>
        <th>west</th>
        <th>midwest</th>
        <th>northeast</th>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>1.0</td>
        <td>January</td>
        <td>35.6</td>
        <td>17.0</td>
        <td>22.6</td>
        <td>12.9</td>
    </tr>
    <tr>
        <td>1969.0</td>
        <td>1.0</td>
        <td>January</td>
        <td>40.1</td>
        <td>19.7</td>
        <td>18.0</td>
        <td>11.0</td>
    </tr>
    <tr>
        <td>1970.0</td>
        <td>1.0</td>
        <td>January</td>
        <td>43.7</td>
        <td>25.2</td>
        <td>23.1</td>
        <td>13.2</td>
    </tr>
    <tr>
        <td>1971.0</td>
        <td>1.0</td>
        <td>January</td>
        <td>46.8</td>
        <td>22.3</td>
        <td>24.0</td>
        <td>14.2</td>
    </tr>
    <tr>
        <td>1972.0</td>
        <td>1.0</td>
        <td>January</td>
        <td>67.6</td>
        <td>32.8</td>
        <td>26.6</td>
        <td>18.2</td>
    </tr>
    <tr>
        <td>1973.0</td>
        <td>1.0</td>
        <td>January</td>
        <td>72.2</td>
        <td>33.7</td>
        <td>32.4</td>
        <td>23.2</td>
    </tr>
    <tr>
        <td>1974.0</td>
        <td>1.0</td>
        <td>January</td>
        <td>65.8</td>
        <td>28.7</td>
        <td>27.5</td>
        <td>21.1</td>
    </tr>
    <tr>
        <td>1975.0</td>
        <td>1.0</td>
        <td>January</td>
        <td>50.3</td>
        <td>21.7</td>
        <td>31.4</td>
        <td>13.9</td>
    </tr>
    <tr>
        <td>1976.0</td>
        <td>1.0</td>
        <td>January</td>
        <td>36.5</td>
        <td>22.4</td>
        <td>23.8</td>
        <td>8.9</td>
    </tr>
    <tr>
        <td>1977.0</td>
        <td>1.0</td>
        <td>January</td>
        <td>37.7</td>
        <td>31.0</td>
        <td>25.5</td>
        <td>9.2</td>
    </tr>
</table>



## Sql Comparison Operators
- Equal to	=
- Not equal to	<> or !=
- Greater than	>
- Less than	<
- Greater than or equal to	>=
- Less than or equal to	<=



```sql
%%sql
SELECT * FROM housing_units
WHERE west > 30
LIMIT 10
```

     * postgresql://postgres:***@localhost/portfolio
    10 rows affected.





<table>
    <tr>
        <th>year</th>
        <th>month</th>
        <th>month_name</th>
        <th>south</th>
        <th>west</th>
        <th>midwest</th>
        <th>northeast</th>
    </tr>
    <tr>
        <td>1970.0</td>
        <td>9.0</td>
        <td>September</td>
        <td>49.7</td>
        <td>31.2</td>
        <td>29.7</td>
        <td>18.3</td>
    </tr>
    <tr>
        <td>1971.0</td>
        <td>4.0</td>
        <td>April</td>
        <td>60.6</td>
        <td>32.3</td>
        <td>25.1</td>
        <td>15.2</td>
    </tr>
    <tr>
        <td>1971.0</td>
        <td>5.0</td>
        <td>May</td>
        <td>60.4</td>
        <td>30.3</td>
        <td>27.1</td>
        <td>15.9</td>
    </tr>
    <tr>
        <td>1971.0</td>
        <td>6.0</td>
        <td>June</td>
        <td>63.4</td>
        <td>30.8</td>
        <td>28.7</td>
        <td>21.4</td>
    </tr>
    <tr>
        <td>1971.0</td>
        <td>7.0</td>
        <td>July</td>
        <td>62.3</td>
        <td>36.7</td>
        <td>28.5</td>
        <td>18.0</td>
    </tr>
    <tr>
        <td>1971.0</td>
        <td>8.0</td>
        <td>August</td>
        <td>69.3</td>
        <td>43.1</td>
        <td>37.9</td>
        <td>21.2</td>
    </tr>
    <tr>
        <td>1971.0</td>
        <td>9.0</td>
        <td>September</td>
        <td>65.5</td>
        <td>38.2</td>
        <td>40.2</td>
        <td>26.0</td>
    </tr>
    <tr>
        <td>1971.0</td>
        <td>10.0</td>
        <td>October</td>
        <td>66.4</td>
        <td>43.5</td>
        <td>37.7</td>
        <td>27.1</td>
    </tr>
    <tr>
        <td>1971.0</td>
        <td>11.0</td>
        <td>November</td>
        <td>63.7</td>
        <td>34.2</td>
        <td>34.2</td>
        <td>21.0</td>
    </tr>
    <tr>
        <td>1971.0</td>
        <td>12.0</td>
        <td>December</td>
        <td>73.6</td>
        <td>40.9</td>
        <td>32.8</td>
        <td>19.1</td>
    </tr>
</table>




```sql
%%sql
SELECT * FROM housing_units
LIMIT 10
```

     * postgresql://postgres:***@localhost/portfolio
    10 rows affected.





<table>
    <tr>
        <th>year</th>
        <th>month</th>
        <th>month_name</th>
        <th>south</th>
        <th>west</th>
        <th>midwest</th>
        <th>northeast</th>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>1.0</td>
        <td>January</td>
        <td>35.6</td>
        <td>17.0</td>
        <td>22.6</td>
        <td>12.9</td>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>2.0</td>
        <td>February</td>
        <td>31.5</td>
        <td>18.6</td>
        <td>23.3</td>
        <td>9.7</td>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>3.0</td>
        <td>March</td>
        <td>42.5</td>
        <td>17.4</td>
        <td>24.4</td>
        <td>10.7</td>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>4.0</td>
        <td>April</td>
        <td>42.9</td>
        <td>20.6</td>
        <td>27.0</td>
        <td>12.0</td>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>5.0</td>
        <td>May</td>
        <td>46.2</td>
        <td>20.0</td>
        <td>25.1</td>
        <td>20.0</td>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>6.0</td>
        <td>June</td>
        <td>37.7</td>
        <td>23.2</td>
        <td>26.9</td>
        <td>16.8</td>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>7.0</td>
        <td>July</td>
        <td>50.3</td>
        <td>21.2</td>
        <td>25.7</td>
        <td>20.1</td>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>8.0</td>
        <td>August</td>
        <td>46.6</td>
        <td>23.1</td>
        <td>33.4</td>
        <td>15.3</td>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>9.0</td>
        <td>September</td>
        <td>48.7</td>
        <td>22.0</td>
        <td>37.9</td>
        <td>27.0</td>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>10.0</td>
        <td>October</td>
        <td>50.2</td>
        <td>23.0</td>
        <td>34.2</td>
        <td>20.5</td>
    </tr>
</table>




```sql
%%sql
SELECT * FROM housing_units
WHERE month_name = 'June'
LIMIT 10
```

     * postgresql://postgres:***@localhost/portfolio
    10 rows affected.





<table>
    <tr>
        <th>year</th>
        <th>month</th>
        <th>month_name</th>
        <th>south</th>
        <th>west</th>
        <th>midwest</th>
        <th>northeast</th>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>6.0</td>
        <td>June</td>
        <td>37.7</td>
        <td>23.2</td>
        <td>26.9</td>
        <td>16.8</td>
    </tr>
    <tr>
        <td>1969.0</td>
        <td>6.0</td>
        <td>June</td>
        <td>53.7</td>
        <td>23.5</td>
        <td>31.6</td>
        <td>22.9</td>
    </tr>
    <tr>
        <td>1970.0</td>
        <td>6.0</td>
        <td>June</td>
        <td>60.1</td>
        <td>25.8</td>
        <td>29.9</td>
        <td>15.0</td>
    </tr>
    <tr>
        <td>1971.0</td>
        <td>6.0</td>
        <td>June</td>
        <td>63.4</td>
        <td>30.8</td>
        <td>28.7</td>
        <td>21.4</td>
    </tr>
    <tr>
        <td>1972.0</td>
        <td>6.0</td>
        <td>June</td>
        <td>73.5</td>
        <td>41.1</td>
        <td>35.2</td>
        <td>24.1</td>
    </tr>
    <tr>
        <td>1973.0</td>
        <td>6.0</td>
        <td>June</td>
        <td>87.1</td>
        <td>40.1</td>
        <td>43.3</td>
        <td>31.7</td>
    </tr>
    <tr>
        <td>1974.0</td>
        <td>6.0</td>
        <td>June</td>
        <td>69.4</td>
        <td>31.3</td>
        <td>42.2</td>
        <td>23.6</td>
    </tr>
    <tr>
        <td>1975.0</td>
        <td>6.0</td>
        <td>June</td>
        <td>49.0</td>
        <td>21.7</td>
        <td>24.2</td>
        <td>15.0</td>
    </tr>
    <tr>
        <td>1976.0</td>
        <td>6.0</td>
        <td>June</td>
        <td>45.4</td>
        <td>30.9</td>
        <td>26.7</td>
        <td>17.7</td>
    </tr>
    <tr>
        <td>1977.0</td>
        <td>6.0</td>
        <td>June</td>
        <td>55.0</td>
        <td>41.0</td>
        <td>34.6</td>
        <td>14.3</td>
    </tr>
</table>



### Did the West Region ever produce more than 50,000 housing units in one month?


```sql
%%sql
SELECT * FROM housing_units
WHERE midwest >= 50
```

     * postgresql://postgres:***@localhost/portfolio
    2 rows affected.





<table>
    <tr>
        <th>year</th>
        <th>month</th>
        <th>month_name</th>
        <th>south</th>
        <th>west</th>
        <th>midwest</th>
        <th>northeast</th>
    </tr>
    <tr>
        <td>1973.0</td>
        <td>10.0</td>
        <td>October</td>
        <td>75.3</td>
        <td>40.0</td>
        <td>55.7</td>
        <td>27.8</td>
    </tr>
    <tr>
        <td>1977.0</td>
        <td>9.0</td>
        <td>September</td>
        <td>61.3</td>
        <td>41.2</td>
        <td>51.1</td>
        <td>18.6</td>
    </tr>
</table>



West region produced more than 50,000 units each for the months of October and September

### Did the South Region ever produce 20,000 or fewer housing units in one month?


```sql
%%sql
SELECT * FROM housing_units
WHERE south <= 20
```

     * postgresql://postgres:***@localhost/portfolio
    4 rows affected.





<table>
    <tr>
        <th>year</th>
        <th>month</th>
        <th>month_name</th>
        <th>south</th>
        <th>west</th>
        <th>midwest</th>
        <th>northeast</th>
    </tr>
    <tr>
        <td>2011.0</td>
        <td>1.0</td>
        <td>January</td>
        <td>17.3</td>
        <td>7.2</td>
        <td>6.3</td>
        <td>4.2</td>
    </tr>
    <tr>
        <td>2011.0</td>
        <td>5.0</td>
        <td>May</td>
        <td>20.0</td>
        <td>11.1</td>
        <td>8.7</td>
        <td>5.6</td>
    </tr>
    <tr>
        <td>2012.0</td>
        <td>1.0</td>
        <td>January</td>
        <td>18.8</td>
        <td>6.0</td>
        <td>5.8</td>
        <td>5.8</td>
    </tr>
    <tr>
        <td>2012.0</td>
        <td>2.0</td>
        <td>February</td>
        <td>19.9</td>
        <td>7.4</td>
        <td>6.4</td>
        <td>5.3</td>
    </tr>
</table>




```sql
%%sql
SELECT *
  FROM housing_units
 WHERE month_name > 'J'
LIMIT 10
```

     * postgresql://postgres:***@localhost/portfolio
    10 rows affected.





<table>
    <tr>
        <th>year</th>
        <th>month</th>
        <th>month_name</th>
        <th>south</th>
        <th>west</th>
        <th>midwest</th>
        <th>northeast</th>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>1.0</td>
        <td>January</td>
        <td>35.6</td>
        <td>17.0</td>
        <td>22.6</td>
        <td>12.9</td>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>3.0</td>
        <td>March</td>
        <td>42.5</td>
        <td>17.4</td>
        <td>24.4</td>
        <td>10.7</td>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>5.0</td>
        <td>May</td>
        <td>46.2</td>
        <td>20.0</td>
        <td>25.1</td>
        <td>20.0</td>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>6.0</td>
        <td>June</td>
        <td>37.7</td>
        <td>23.2</td>
        <td>26.9</td>
        <td>16.8</td>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>7.0</td>
        <td>July</td>
        <td>50.3</td>
        <td>21.2</td>
        <td>25.7</td>
        <td>20.1</td>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>9.0</td>
        <td>September</td>
        <td>48.7</td>
        <td>22.0</td>
        <td>37.9</td>
        <td>27.0</td>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>10.0</td>
        <td>October</td>
        <td>50.2</td>
        <td>23.0</td>
        <td>34.2</td>
        <td>20.5</td>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>11.0</td>
        <td>November</td>
        <td>45.7</td>
        <td>18.4</td>
        <td>35.8</td>
        <td>14.4</td>
    </tr>
    <tr>
        <td>1969.0</td>
        <td>1.0</td>
        <td>January</td>
        <td>40.1</td>
        <td>19.7</td>
        <td>18.0</td>
        <td>11.0</td>
    </tr>
    <tr>
        <td>1969.0</td>
        <td>3.0</td>
        <td>March</td>
        <td>53.3</td>
        <td>21.1</td>
        <td>23.5</td>
        <td>17.0</td>
    </tr>
</table>



### A query that only shows rows for which the month name is February.


```sql
%%sql
SELECT * FROM housing_units
WHERE month_name = 'February'
LIMIT 5
```

     * postgresql://postgres:***@localhost/portfolio
    5 rows affected.





<table>
    <tr>
        <th>year</th>
        <th>month</th>
        <th>month_name</th>
        <th>south</th>
        <th>west</th>
        <th>midwest</th>
        <th>northeast</th>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>2.0</td>
        <td>February</td>
        <td>31.5</td>
        <td>18.6</td>
        <td>23.3</td>
        <td>9.7</td>
    </tr>
    <tr>
        <td>1969.0</td>
        <td>2.0</td>
        <td>February</td>
        <td>34.8</td>
        <td>23.0</td>
        <td>23.3</td>
        <td>14.9</td>
    </tr>
    <tr>
        <td>1970.0</td>
        <td>2.0</td>
        <td>February</td>
        <td>39.6</td>
        <td>24.5</td>
        <td>19.6</td>
        <td>13.2</td>
    </tr>
    <tr>
        <td>1971.0</td>
        <td>2.0</td>
        <td>February</td>
        <td>45.1</td>
        <td>24.1</td>
        <td>14.3</td>
        <td>14.9</td>
    </tr>
    <tr>
        <td>1972.0</td>
        <td>2.0</td>
        <td>February</td>
        <td>61.2</td>
        <td>35.8</td>
        <td>27.5</td>
        <td>19.0</td>
    </tr>
</table>




```sql
%%sql
SELECT COUNT(month_name) FROM housing_units
WHERE month_name = 'February'
```

     * postgresql://postgres:***@localhost/portfolio
    1 rows affected.





<table>
    <tr>
        <th>count</th>
    </tr>
    <tr>
        <td>47</td>
    </tr>
</table>



### A query that only shows rows for which the month_name starts with the letter "N" or an earlier letter in the alphabet.


```sql
%%sql
SELECT * FROM housing_units
WHERE month_name < 'N'
LIMIT 5
```

     * postgresql://postgres:***@localhost/portfolio
    5 rows affected.





<table>
    <tr>
        <th>year</th>
        <th>month</th>
        <th>month_name</th>
        <th>south</th>
        <th>west</th>
        <th>midwest</th>
        <th>northeast</th>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>1.0</td>
        <td>January</td>
        <td>35.6</td>
        <td>17.0</td>
        <td>22.6</td>
        <td>12.9</td>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>2.0</td>
        <td>February</td>
        <td>31.5</td>
        <td>18.6</td>
        <td>23.3</td>
        <td>9.7</td>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>3.0</td>
        <td>March</td>
        <td>42.5</td>
        <td>17.4</td>
        <td>24.4</td>
        <td>10.7</td>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>4.0</td>
        <td>April</td>
        <td>42.9</td>
        <td>20.6</td>
        <td>27.0</td>
        <td>12.0</td>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>5.0</td>
        <td>May</td>
        <td>46.2</td>
        <td>20.0</td>
        <td>25.1</td>
        <td>20.0</td>
    </tr>
</table>



## Arithmetic in SQL


```sql
%%sql
SELECT year, month, month_name, south, west, midwest+northeast AS MidwestNorth
FROM housing_units
LIMIT 10
```

     * postgresql://postgres:***@localhost/portfolio
    10 rows affected.





<table>
    <tr>
        <th>year</th>
        <th>month</th>
        <th>month_name</th>
        <th>south</th>
        <th>west</th>
        <th>midwestnorth</th>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>1.0</td>
        <td>January</td>
        <td>35.6</td>
        <td>17.0</td>
        <td>35.5</td>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>2.0</td>
        <td>February</td>
        <td>31.5</td>
        <td>18.6</td>
        <td>33.0</td>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>3.0</td>
        <td>March</td>
        <td>42.5</td>
        <td>17.4</td>
        <td>35.1</td>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>4.0</td>
        <td>April</td>
        <td>42.9</td>
        <td>20.6</td>
        <td>39.0</td>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>5.0</td>
        <td>May</td>
        <td>46.2</td>
        <td>20.0</td>
        <td>45.1</td>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>6.0</td>
        <td>June</td>
        <td>37.7</td>
        <td>23.2</td>
        <td>43.699997</td>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>7.0</td>
        <td>July</td>
        <td>50.3</td>
        <td>21.2</td>
        <td>45.800003</td>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>8.0</td>
        <td>August</td>
        <td>46.6</td>
        <td>23.1</td>
        <td>48.7</td>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>9.0</td>
        <td>September</td>
        <td>48.7</td>
        <td>22.0</td>
        <td>64.9</td>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>10.0</td>
        <td>October</td>
        <td>50.2</td>
        <td>23.0</td>
        <td>54.7</td>
    </tr>
</table>




```sql
%%sql
SELECT year,
       month,
       west,
       south,
       west + south + 4 * year * 100 AS nonsense_column
  FROM housing_units
LIMIT 10

```

     * postgresql://postgres:***@localhost/portfolio
    10 rows affected.





<table>
    <tr>
        <th>year</th>
        <th>month</th>
        <th>west</th>
        <th>south</th>
        <th>nonsense_column</th>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>1.0</td>
        <td>17.0</td>
        <td>35.6</td>
        <td>787252.5999984741</td>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>2.0</td>
        <td>18.6</td>
        <td>31.5</td>
        <td>787250.0999984741</td>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>3.0</td>
        <td>17.4</td>
        <td>42.5</td>
        <td>787259.9000015259</td>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>4.0</td>
        <td>20.6</td>
        <td>42.9</td>
        <td>787263.5</td>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>5.0</td>
        <td>20.0</td>
        <td>46.2</td>
        <td>787266.1999969482</td>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>6.0</td>
        <td>23.2</td>
        <td>37.7</td>
        <td>787260.9000015259</td>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>7.0</td>
        <td>21.2</td>
        <td>50.3</td>
        <td>787271.5</td>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>8.0</td>
        <td>23.1</td>
        <td>46.6</td>
        <td>787269.6999969482</td>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>9.0</td>
        <td>22.0</td>
        <td>48.7</td>
        <td>787270.6999969482</td>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>10.0</td>
        <td>23.0</td>
        <td>50.2</td>
        <td>787273.1999969482</td>
    </tr>
</table>



### Calculates the sum of all four regions in a separate column.


```sql
%%sql
SELECT year AS "Year", month AS "Month", month_name AS "Month_name", south AS "South", west AS "West", midwest AS "Midwest", northeast AS Northeast, (south + west + midwest + northeast) AS Sum_of_Regions FROM housing_units
ORDER BY Sum_of_Regions
LIMIT 20
```

     * postgresql://postgres:***@localhost/portfolio
    20 rows affected.





<table>
    <tr>
        <th>Year</th>
        <th>Month</th>
        <th>Month_name</th>
        <th>South</th>
        <th>West</th>
        <th>Midwest</th>
        <th>northeast</th>
        <th>sum_of_regions</th>
    </tr>
    <tr>
        <td>2011.0</td>
        <td>1.0</td>
        <td>January</td>
        <td>17.3</td>
        <td>7.2</td>
        <td>6.3</td>
        <td>4.2</td>
        <td>35.0</td>
    </tr>
    <tr>
        <td>2012.0</td>
        <td>1.0</td>
        <td>January</td>
        <td>18.8</td>
        <td>6.0</td>
        <td>5.8</td>
        <td>5.8</td>
        <td>36.399998</td>
    </tr>
    <tr>
        <td>2012.0</td>
        <td>2.0</td>
        <td>February</td>
        <td>19.9</td>
        <td>7.4</td>
        <td>6.4</td>
        <td>5.3</td>
        <td>39.0</td>
    </tr>
    <tr>
        <td>2011.0</td>
        <td>2.0</td>
        <td>February</td>
        <td>23.1</td>
        <td>8.1</td>
        <td>6.4</td>
        <td>4.4</td>
        <td>42.000004</td>
    </tr>
    <tr>
        <td>2011.0</td>
        <td>4.0</td>
        <td>April</td>
        <td>21.9</td>
        <td>7.7</td>
        <td>7.4</td>
        <td>5.2</td>
        <td>42.2</td>
    </tr>
    <tr>
        <td>2011.0</td>
        <td>3.0</td>
        <td>March</td>
        <td>25.4</td>
        <td>7.4</td>
        <td>6.5</td>
        <td>4.5</td>
        <td>43.8</td>
    </tr>
    <tr>
        <td>2012.0</td>
        <td>3.0</td>
        <td>March</td>
        <td>22.1</td>
        <td>9.1</td>
        <td>8.4</td>
        <td>4.8</td>
        <td>44.399998</td>
    </tr>
    <tr>
        <td>2011.0</td>
        <td>5.0</td>
        <td>May</td>
        <td>20.0</td>
        <td>11.1</td>
        <td>8.7</td>
        <td>5.6</td>
        <td>45.399998</td>
    </tr>
    <tr>
        <td>2010.0</td>
        <td>2.0</td>
        <td>February</td>
        <td>23.0</td>
        <td>11.2</td>
        <td>5.7</td>
        <td>5.6</td>
        <td>45.5</td>
    </tr>
    <tr>
        <td>2010.0</td>
        <td>1.0</td>
        <td>January</td>
        <td>21.2</td>
        <td>13.9</td>
        <td>5.5</td>
        <td>5.8</td>
        <td>46.399998</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>1.0</td>
        <td>January</td>
        <td>24.8</td>
        <td>12.5</td>
        <td>5.5</td>
        <td>4.6</td>
        <td>47.399998</td>
    </tr>
    <tr>
        <td>2010.0</td>
        <td>7.0</td>
        <td>July</td>
        <td>23.8</td>
        <td>9.8</td>
        <td>8.8</td>
        <td>5.8</td>
        <td>48.199997</td>
    </tr>
    <tr>
        <td>2010.0</td>
        <td>11.0</td>
        <td>November</td>
        <td>22.4</td>
        <td>8.4</td>
        <td>11.0</td>
        <td>6.5</td>
        <td>48.3</td>
    </tr>
    <tr>
        <td>2010.0</td>
        <td>3.0</td>
        <td>March</td>
        <td>26.0</td>
        <td>12.5</td>
        <td>5.7</td>
        <td>4.4</td>
        <td>48.600002</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>2.0</td>
        <td>February</td>
        <td>26.4</td>
        <td>12.2</td>
        <td>7.1</td>
        <td>4.1</td>
        <td>49.799995</td>
    </tr>
    <tr>
        <td>2012.0</td>
        <td>5.0</td>
        <td>May</td>
        <td>24.5</td>
        <td>10.1</td>
        <td>8.5</td>
        <td>6.8</td>
        <td>49.899998</td>
    </tr>
    <tr>
        <td>2011.0</td>
        <td>11.0</td>
        <td>November</td>
        <td>26.0</td>
        <td>10.5</td>
        <td>8.8</td>
        <td>4.7</td>
        <td>50.0</td>
    </tr>
    <tr>
        <td>2011.0</td>
        <td>6.0</td>
        <td>June</td>
        <td>24.6</td>
        <td>8.8</td>
        <td>9.6</td>
        <td>7.5</td>
        <td>50.5</td>
    </tr>
    <tr>
        <td>2011.0</td>
        <td>10.0</td>
        <td>October</td>
        <td>25.6</td>
        <td>9.8</td>
        <td>9.0</td>
        <td>7.7</td>
        <td>52.100002</td>
    </tr>
    <tr>
        <td>2012.0</td>
        <td>4.0</td>
        <td>April</td>
        <td>26.1</td>
        <td>11.9</td>
        <td>8.3</td>
        <td>6.1</td>
        <td>52.399998</td>
    </tr>
</table>




```sql
%%sql
SELECT year,
       month,
       west,
       south,
       west + south - 4 * year AS nonsense_column
  FROM housing_units
LIMIT 10
```

     * postgresql://postgres:***@localhost/portfolio
    10 rows affected.





<table>
    <tr>
        <th>year</th>
        <th>month</th>
        <th>west</th>
        <th>south</th>
        <th>nonsense_column</th>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>1.0</td>
        <td>17.0</td>
        <td>35.6</td>
        <td>-7819.400001525879</td>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>2.0</td>
        <td>18.6</td>
        <td>31.5</td>
        <td>-7821.900001525879</td>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>3.0</td>
        <td>17.4</td>
        <td>42.5</td>
        <td>-7812.099998474121</td>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>4.0</td>
        <td>20.6</td>
        <td>42.9</td>
        <td>-7808.5</td>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>5.0</td>
        <td>20.0</td>
        <td>46.2</td>
        <td>-7805.800003051758</td>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>6.0</td>
        <td>23.2</td>
        <td>37.7</td>
        <td>-7811.099998474121</td>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>7.0</td>
        <td>21.2</td>
        <td>50.3</td>
        <td>-7800.5</td>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>8.0</td>
        <td>23.1</td>
        <td>46.6</td>
        <td>-7802.300003051758</td>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>9.0</td>
        <td>22.0</td>
        <td>48.7</td>
        <td>-7801.300003051758</td>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>10.0</td>
        <td>23.0</td>
        <td>50.2</td>
        <td>-7798.800003051758</td>
    </tr>
</table>



### Return all rows for which more units were produced in the West region than in the Midwest and Northeast combined.


```sql
%%sql
SELECT west, Midwest+Northeast AS Mid_and_North_Combined
FROM housing_units
WHERE west > (Midwest+Northeast)
LIMIT 10
```

     * postgresql://postgres:***@localhost/portfolio
    10 rows affected.





<table>
    <tr>
        <th>west</th>
        <th>mid_and_north_combined</th>
    </tr>
    <tr>
        <td>32.2</td>
        <td>32.1</td>
    </tr>
    <tr>
        <td>41.2</td>
        <td>40.6</td>
    </tr>
    <tr>
        <td>42.5</td>
        <td>38.0</td>
    </tr>
    <tr>
        <td>35.4</td>
        <td>34.800003</td>
    </tr>
    <tr>
        <td>35.7</td>
        <td>34.5</td>
    </tr>
    <tr>
        <td>33.9</td>
        <td>29.199999</td>
    </tr>
    <tr>
        <td>22.1</td>
        <td>21.6</td>
    </tr>
    <tr>
        <td>25.3</td>
        <td>23.2</td>
    </tr>
    <tr>
        <td>17.3</td>
        <td>17.1</td>
    </tr>
    <tr>
        <td>15.1</td>
        <td>14.5</td>
    </tr>
</table>




```python

```


```sql
%%sql
SELECT *
FROM housing_units
LIMIT 10

```

     * postgresql://postgres:***@localhost/portfolio
    10 rows affected.





<table>
    <tr>
        <th>year</th>
        <th>month</th>
        <th>month_name</th>
        <th>south</th>
        <th>west</th>
        <th>midwest</th>
        <th>northeast</th>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>1.0</td>
        <td>January</td>
        <td>35.6</td>
        <td>17.0</td>
        <td>22.6</td>
        <td>12.9</td>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>2.0</td>
        <td>February</td>
        <td>31.5</td>
        <td>18.6</td>
        <td>23.3</td>
        <td>9.7</td>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>3.0</td>
        <td>March</td>
        <td>42.5</td>
        <td>17.4</td>
        <td>24.4</td>
        <td>10.7</td>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>4.0</td>
        <td>April</td>
        <td>42.9</td>
        <td>20.6</td>
        <td>27.0</td>
        <td>12.0</td>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>5.0</td>
        <td>May</td>
        <td>46.2</td>
        <td>20.0</td>
        <td>25.1</td>
        <td>20.0</td>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>6.0</td>
        <td>June</td>
        <td>37.7</td>
        <td>23.2</td>
        <td>26.9</td>
        <td>16.8</td>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>7.0</td>
        <td>July</td>
        <td>50.3</td>
        <td>21.2</td>
        <td>25.7</td>
        <td>20.1</td>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>8.0</td>
        <td>August</td>
        <td>46.6</td>
        <td>23.1</td>
        <td>33.4</td>
        <td>15.3</td>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>9.0</td>
        <td>September</td>
        <td>48.7</td>
        <td>22.0</td>
        <td>37.9</td>
        <td>27.0</td>
    </tr>
    <tr>
        <td>1968.0</td>
        <td>10.0</td>
        <td>October</td>
        <td>50.2</td>
        <td>23.0</td>
        <td>34.2</td>
        <td>20.5</td>
    </tr>
</table>



### Calculates the percentage of all houses completed in the United States represented by each region. Only return results from the year 2000 and later.



```sql
%%sql
SELECT (SUM(south)/(SUM(south)+SUM(west)+SUM(midwest)+SUM(northeast)))*100 AS south_percentage, (SUM(west)/(SUM(south)+SUM(west)+SUM(midwest)+SUM(northeast)))*100 AS west_percentage, (SUM(midwest)/(SUM(south)+SUM(west)+SUM(midwest)+SUM(northeast)))*100 AS midwest_percentage, (SUM(northeast)/(SUM(south)+SUM(west)+SUM(midwest)+SUM(northeast)))*100 AS northeast_percentage

FROM housing_units
WHERE year >= 2000
```

     * postgresql://postgres:***@localhost/portfolio
    1 rows affected.





<table>
    <tr>
        <th>south_percentage</th>
        <th>west_percentage</th>
        <th>midwest_percentage</th>
        <th>northeast_percentage</th>
    </tr>
    <tr>
        <td>47.94606864452362</td>
        <td>24.421729147434235</td>
        <td>18.069016933441162</td>
        <td>9.56319123506546</td>
    </tr>
</table>



## Logical Operators
Here we make use of data from Billboard Music Charts, It was collected in January 2014 and contains data from 1956 to 2013, the results is the top 100 songs at the end of each year.


```sql
%%sql
SELECT *
FROM bill_board
LIMIT 10
```

     * postgresql://postgres:***@localhost/portfolio
    10 rows affected.





<table>
    <tr>
        <th>year</th>
        <th>year_rank</th>
        <th>group</th>
        <th>artist</th>
        <th>song_name</th>
        <th>id</th>
    </tr>
    <tr>
        <td>1956.0</td>
        <td>1.0</td>
        <td>Elvis Presley</td>
        <td>Elvis Presley</td>
        <td>Heartbreak Hotel</td>
        <td>1</td>
    </tr>
    <tr>
        <td>1956.0</td>
        <td>2.0</td>
        <td>Elvis Presley</td>
        <td>Elvis Presley</td>
        <td>Don&#x27;t Be Cruel</td>
        <td>2</td>
    </tr>
    <tr>
        <td>1956.0</td>
        <td>3.0</td>
        <td>Nelson Riddle</td>
        <td>Nelson Riddle</td>
        <td>Lisbon Antigua</td>
        <td>3</td>
    </tr>
    <tr>
        <td>1956.0</td>
        <td>4.0</td>
        <td>Platters</td>
        <td>Platters</td>
        <td>My Prayer</td>
        <td>4</td>
    </tr>
    <tr>
        <td>1956.0</td>
        <td>5.0</td>
        <td>Gogi Grant</td>
        <td>Gogi Grant</td>
        <td>The Wayward Wind</td>
        <td>5</td>
    </tr>
    <tr>
        <td>1956.0</td>
        <td>6.0</td>
        <td>Les Baxter</td>
        <td>Les Baxter</td>
        <td>The Poor People Of Paris</td>
        <td>6</td>
    </tr>
    <tr>
        <td>1956.0</td>
        <td>7.0</td>
        <td>Doris Day</td>
        <td>Doris Day</td>
        <td>Whatever Will Be Will Be (Que Sera Sera)</td>
        <td>7</td>
    </tr>
    <tr>
        <td>1956.0</td>
        <td>8.0</td>
        <td>Elvis Presley</td>
        <td>Elvis Presley</td>
        <td>Hound Dog</td>
        <td>8</td>
    </tr>
    <tr>
        <td>1956.0</td>
        <td>9.0</td>
        <td>Dean Martin</td>
        <td>Dean Martin</td>
        <td>Memories Are Made Of This</td>
        <td>9</td>
    </tr>
    <tr>
        <td>1956.0</td>
        <td>10.0</td>
        <td>Kay Starr</td>
        <td>Kay Starr</td>
        <td>Rock And Roll Waltz</td>
        <td>10</td>
    </tr>
</table>




```sql
%%sql
SELECT *
FROM bill_board
ORDER BY year DESC, year_rank
LIMIT 10
```

     * postgresql://postgres:***@localhost/portfolio
    10 rows affected.





<table>
    <tr>
        <th>year</th>
        <th>year_rank</th>
        <th>group</th>
        <th>artist</th>
        <th>song_name</th>
        <th>id</th>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>1.0</td>
        <td>Macklemore and Ryan Lewis feat. Wanz</td>
        <td>Ryan Lewis</td>
        <td>Thrift Shop</td>
        <td>6335</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>1.0</td>
        <td>Macklemore and Ryan Lewis feat. Wanz</td>
        <td>Wanz</td>
        <td>Thrift Shop</td>
        <td>6336</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>1.0</td>
        <td>Macklemore and Ryan Lewis feat. Wanz</td>
        <td>Macklemore</td>
        <td>Thrift Shop</td>
        <td>6334</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>2.0</td>
        <td>Robin Thicke feat. T.I. and Pharrell</td>
        <td>Pharrell</td>
        <td>Blurred Lines</td>
        <td>6339</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>2.0</td>
        <td>Robin Thicke feat. T.I. and Pharrell</td>
        <td>T.I.</td>
        <td>Blurred Lines</td>
        <td>6338</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>2.0</td>
        <td>Robin Thicke feat. T.I. and Pharrell</td>
        <td>Robin Thicke</td>
        <td>Blurred Lines</td>
        <td>6337</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>3.0</td>
        <td>Imagine Dragons</td>
        <td>Imagine Dragons</td>
        <td>Radioactive</td>
        <td>6340</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>4.0</td>
        <td>Baauer</td>
        <td>Baauer</td>
        <td>Harlem Shake</td>
        <td>6341</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>5.0</td>
        <td>Macklemore and Ryan Lewis feat. Ray Dalton</td>
        <td>Macklemore</td>
        <td>Can&#x27;t Hold Us</td>
        <td>6342</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>5.0</td>
        <td>Macklemore and Ryan Lewis feat. Ray Dalton</td>
        <td>Ryan Lewis</td>
        <td>Can&#x27;t Hold Us</td>
        <td>6343</td>
    </tr>
</table>



### SQL LIKE
Logical operator in SQL that allows you to match on similar values rather than exact ones.
Where **LIKE** is case sensitive and **ILIKE** is not.


```sql
%%sql
SELECT * FROM bill_board
WHERE artist LIKE 'Michael%'
LIMIT 10
```

     * postgresql://postgres:***@localhost/portfolio
    10 rows affected.





<table>
    <tr>
        <th>year</th>
        <th>year_rank</th>
        <th>group</th>
        <th>artist</th>
        <th>song_name</th>
        <th>id</th>
    </tr>
    <tr>
        <td>1972.0</td>
        <td>20.0</td>
        <td>Michael Jackson</td>
        <td>Michael Jackson</td>
        <td>Ben</td>
        <td>1637</td>
    </tr>
    <tr>
        <td>1972.0</td>
        <td>41.0</td>
        <td>Michael Jackson</td>
        <td>Michael Jackson</td>
        <td>Rockin&#x27; Robin</td>
        <td>1658</td>
    </tr>
    <tr>
        <td>1975.0</td>
        <td>39.0</td>
        <td>Michael Murphy</td>
        <td>Michael Murphy</td>
        <td>Wildfire</td>
        <td>1965</td>
    </tr>
    <tr>
        <td>1978.0</td>
        <td>81.0</td>
        <td>Michael Johnson</td>
        <td>Michael Johnson</td>
        <td>Bluer Than Blue</td>
        <td>2319</td>
    </tr>
    <tr>
        <td>1979.0</td>
        <td>91.0</td>
        <td>Michael Jackson</td>
        <td>Michael Jackson</td>
        <td>Don&#x27;t Stop &#x27;Til You Get Enough</td>
        <td>2432</td>
    </tr>
    <tr>
        <td>1980.0</td>
        <td>4.0</td>
        <td>Michael Jackson</td>
        <td>Michael Jackson</td>
        <td>Rock With You</td>
        <td>2445</td>
    </tr>
    <tr>
        <td>1980.0</td>
        <td>65.0</td>
        <td>Michael Jackson</td>
        <td>Michael Jackson</td>
        <td>She&#x27;s Out Of My Life</td>
        <td>2508</td>
    </tr>
    <tr>
        <td>1980.0</td>
        <td>79.0</td>
        <td>Michael Jackson</td>
        <td>Michael Jackson</td>
        <td>Off The Wall</td>
        <td>2523</td>
    </tr>
    <tr>
        <td>1982.0</td>
        <td>81.0</td>
        <td>Michael McDonald</td>
        <td>Michael McDonald</td>
        <td>I Keep Forgettin&#x27;</td>
        <td>2741</td>
    </tr>
    <tr>
        <td>1982.0</td>
        <td>93.0</td>
        <td>Michael Murphy</td>
        <td>Michael Murphy</td>
        <td>What&#x27;s Forever For</td>
        <td>2753</td>
    </tr>
</table>



 #### A query that returns all rows for which Ludacris was a member of the group.


```sql
%%sql
SELECT * FROM bill_board
WHERE "group" ILIKE '%Ludacris%'
LIMIT 10
```

     * postgresql://postgres:***@localhost/portfolio
    10 rows affected.





<table>
    <tr>
        <th>year</th>
        <th>year_rank</th>
        <th>group</th>
        <th>artist</th>
        <th>song_name</th>
        <th>id</th>
    </tr>
    <tr>
        <td>2001.0</td>
        <td>77.0</td>
        <td>Ludacris</td>
        <td>Ludacris</td>
        <td>Southern Hospitality</td>
        <td>4770</td>
    </tr>
    <tr>
        <td>2002.0</td>
        <td>55.0</td>
        <td>Ludacris feat. Mystikal and Infamous 2.0</td>
        <td>Ludacris</td>
        <td>Move Bitch</td>
        <td>4880</td>
    </tr>
    <tr>
        <td>2002.0</td>
        <td>55.0</td>
        <td>Ludacris feat. Mystikal and Infamous 2.0</td>
        <td>Mystikal</td>
        <td>Move Bitch</td>
        <td>4881</td>
    </tr>
    <tr>
        <td>2002.0</td>
        <td>55.0</td>
        <td>Ludacris feat. Mystikal and Infamous 2.0</td>
        <td>Infamous 2.0</td>
        <td>Move Bitch</td>
        <td>4882</td>
    </tr>
    <tr>
        <td>2002.0</td>
        <td>77.0</td>
        <td>Ludacris</td>
        <td>Ludacris</td>
        <td>Roll Out (My Business)</td>
        <td>4913</td>
    </tr>
    <tr>
        <td>2003.0</td>
        <td>43.0</td>
        <td>Missy &quot;Misdemeanor&quot; Elliott feat. Ludacris</td>
        <td>Missy &quot;Misdemeanor&quot; Elliott</td>
        <td>Gossip Folks</td>
        <td>5007</td>
    </tr>
    <tr>
        <td>2003.0</td>
        <td>43.0</td>
        <td>Missy &quot;Misdemeanor&quot; Elliott feat. Ludacris</td>
        <td>Ludacris</td>
        <td>Gossip Folks</td>
        <td>5008</td>
    </tr>
    <tr>
        <td>2003.0</td>
        <td>51.0</td>
        <td>Ludacris feat. Shawnna</td>
        <td>Ludacris</td>
        <td>Stand Up</td>
        <td>5017</td>
    </tr>
    <tr>
        <td>2003.0</td>
        <td>51.0</td>
        <td>Ludacris feat. Shawnna</td>
        <td>Shawnna</td>
        <td>Stand Up</td>
        <td>5018</td>
    </tr>
    <tr>
        <td>2003.0</td>
        <td>76.0</td>
        <td>Chingy feat. Ludacris and Snoop Dogg</td>
        <td>Chingy</td>
        <td>Holidae In</td>
        <td>5052</td>
    </tr>
</table>



#### A query that returns all rows for which the first artist listed in the group has a name that begins with "DJ".


```sql
%%sql
SELECT * FROM bill_board
WHERE "group" ILIKE 'dj%'
```

     * postgresql://postgres:***@localhost/portfolio
    13 rows affected.





<table>
    <tr>
        <th>year</th>
        <th>year_rank</th>
        <th>group</th>
        <th>artist</th>
        <th>song_name</th>
        <th>id</th>
    </tr>
    <tr>
        <td>1997.0</td>
        <td>96.0</td>
        <td>DJ Kool</td>
        <td>DJ Kool</td>
        <td>Let Me Clear My Throat</td>
        <td>4325</td>
    </tr>
    <tr>
        <td>2002.0</td>
        <td>31.0</td>
        <td>DJ Sammy and Yanou feat. Do</td>
        <td>DJ Sammy</td>
        <td>Heaven</td>
        <td>4844</td>
    </tr>
    <tr>
        <td>2002.0</td>
        <td>31.0</td>
        <td>DJ Sammy and Yanou feat. Do</td>
        <td>Yanou</td>
        <td>Heaven</td>
        <td>4845</td>
    </tr>
    <tr>
        <td>2002.0</td>
        <td>31.0</td>
        <td>DJ Sammy and Yanou feat. Do</td>
        <td>Do</td>
        <td>Heaven</td>
        <td>4846</td>
    </tr>
    <tr>
        <td>2010.0</td>
        <td>79.0</td>
        <td>DJ Khaled feat. T-Pain, Ludacris, Snoop Dogg and Rick Ross</td>
        <td>DJ Khaled</td>
        <td>All I Do Is Win</td>
        <td>6023</td>
    </tr>
    <tr>
        <td>2010.0</td>
        <td>79.0</td>
        <td>DJ Khaled feat. T-Pain, Ludacris, Snoop Dogg and Rick Ross</td>
        <td>T-Pain</td>
        <td>All I Do Is Win</td>
        <td>6024</td>
    </tr>
    <tr>
        <td>2010.0</td>
        <td>79.0</td>
        <td>DJ Khaled feat. T-Pain, Ludacris, Snoop Dogg and Rick Ross</td>
        <td>Ludacris</td>
        <td>All I Do Is Win</td>
        <td>6025</td>
    </tr>
    <tr>
        <td>2010.0</td>
        <td>79.0</td>
        <td>DJ Khaled feat. T-Pain, Ludacris, Snoop Dogg and Rick Ross</td>
        <td>Snoop Dogg</td>
        <td>All I Do Is Win</td>
        <td>6026</td>
    </tr>
    <tr>
        <td>2010.0</td>
        <td>79.0</td>
        <td>DJ Khaled feat. T-Pain, Ludacris, Snoop Dogg and Rick Ross</td>
        <td>Rick Ross</td>
        <td>All I Do Is Win</td>
        <td>6027</td>
    </tr>
    <tr>
        <td>2011.0</td>
        <td>47.0</td>
        <td>DJ Khaled feat. Drake, Rick Ross and Lil Wayne</td>
        <td>DJ Khaled</td>
        <td>I&#x27;m On One</td>
        <td>6123</td>
    </tr>
    <tr>
        <td>2011.0</td>
        <td>47.0</td>
        <td>DJ Khaled feat. Drake, Rick Ross and Lil Wayne</td>
        <td>Drake</td>
        <td>I&#x27;m On One</td>
        <td>6124</td>
    </tr>
    <tr>
        <td>2011.0</td>
        <td>47.0</td>
        <td>DJ Khaled feat. Drake, Rick Ross and Lil Wayne</td>
        <td>Rick Ross</td>
        <td>I&#x27;m On One</td>
        <td>6125</td>
    </tr>
    <tr>
        <td>2011.0</td>
        <td>47.0</td>
        <td>DJ Khaled feat. Drake, Rick Ross and Lil Wayne</td>
        <td>Lil Wayne</td>
        <td>I&#x27;m On One</td>
        <td>6126</td>
    </tr>
</table>



### SQL IN
This allows one to specify a list of values that you'd like to include in the results.


```sql
%%sql
SELECT * FROM bill_board
WHERE year_rank IN (100)
LIMIT 10
```

     * postgresql://postgres:***@localhost/portfolio
    10 rows affected.





<table>
    <tr>
        <th>year</th>
        <th>year_rank</th>
        <th>group</th>
        <th>artist</th>
        <th>song_name</th>
        <th>id</th>
    </tr>
    <tr>
        <td>1956.0</td>
        <td>100.0</td>
        <td>Blue Stars</td>
        <td>Blue Stars</td>
        <td>Lullaby of Birdland</td>
        <td>103</td>
    </tr>
    <tr>
        <td>1957.0</td>
        <td>100.0</td>
        <td>Joe Bennett and the Sparkletones</td>
        <td>Joe Bennett and the Sparkletones</td>
        <td>Black Slacks</td>
        <td>203</td>
    </tr>
    <tr>
        <td>1958.0</td>
        <td>100.0</td>
        <td>Frankie Avalon</td>
        <td>Frankie Avalon</td>
        <td>Ginger Bread</td>
        <td>304</td>
    </tr>
    <tr>
        <td>1959.0</td>
        <td>100.0</td>
        <td>Paul Evans and The Curls</td>
        <td>Paul Evans and The Curls</td>
        <td>(Seven Little Girls) Sitting In The Back Seat</td>
        <td>406</td>
    </tr>
    <tr>
        <td>1960.0</td>
        <td>100.0</td>
        <td>Larry Hall</td>
        <td>Larry Hall</td>
        <td>Sandy</td>
        <td>508</td>
    </tr>
    <tr>
        <td>1961.0</td>
        <td>100.0</td>
        <td>Drifters</td>
        <td>Drifters</td>
        <td>Please Stay</td>
        <td>608</td>
    </tr>
    <tr>
        <td>1962.0</td>
        <td>100.0</td>
        <td>Beach Boys</td>
        <td>Beach Boys</td>
        <td>Surfin&#x27; Safari</td>
        <td>708</td>
    </tr>
    <tr>
        <td>1963.0</td>
        <td>100.0</td>
        <td>Del Shannon</td>
        <td>Del Shannon</td>
        <td>Little Town Flirt</td>
        <td>809</td>
    </tr>
    <tr>
        <td>1964.0</td>
        <td>100.0</td>
        <td>Searchers</td>
        <td>Searchers</td>
        <td>Needles And Pins</td>
        <td>911</td>
    </tr>
    <tr>
        <td>1965.0</td>
        <td>100.0</td>
        <td>Marvin Gaye</td>
        <td>Marvin Gaye</td>
        <td>How Sweet It Is (To Be Loved By You)</td>
        <td>1011</td>
    </tr>
</table>




```sql
%%sql
SELECT * FROM bill_board
WHERE year IN (2012,2013)
LIMIT 10

```

     * postgresql://postgres:***@localhost/portfolio
    10 rows affected.





<table>
    <tr>
        <th>year</th>
        <th>year_rank</th>
        <th>group</th>
        <th>artist</th>
        <th>song_name</th>
        <th>id</th>
    </tr>
    <tr>
        <td>2012.0</td>
        <td>1.0</td>
        <td>Gotye feat. Kimbra</td>
        <td>Gotye</td>
        <td>Somebody That I Used To Know</td>
        <td>6203</td>
    </tr>
    <tr>
        <td>2012.0</td>
        <td>1.0</td>
        <td>Gotye feat. Kimbra</td>
        <td>Kimbra</td>
        <td>Somebody That I Used To Know</td>
        <td>6204</td>
    </tr>
    <tr>
        <td>2012.0</td>
        <td>2.0</td>
        <td>Carly Rae Jepsen</td>
        <td>Carly Rae Jepsen</td>
        <td>Call Me Maybe</td>
        <td>6205</td>
    </tr>
    <tr>
        <td>2012.0</td>
        <td>3.0</td>
        <td>fun. feat. Janelle Monae</td>
        <td>fun.</td>
        <td>We Are Young</td>
        <td>6206</td>
    </tr>
    <tr>
        <td>2012.0</td>
        <td>3.0</td>
        <td>fun. feat. Janelle Monae</td>
        <td>Janelle Monae</td>
        <td>We Are Young</td>
        <td>6207</td>
    </tr>
    <tr>
        <td>2012.0</td>
        <td>4.0</td>
        <td>Maroon 5 feat. Wiz Khalifa</td>
        <td>Maroon 5</td>
        <td>Payphone</td>
        <td>6208</td>
    </tr>
    <tr>
        <td>2012.0</td>
        <td>4.0</td>
        <td>Maroon 5 feat. Wiz Khalifa</td>
        <td>Wiz Khalifa</td>
        <td>Payphone</td>
        <td>6209</td>
    </tr>
    <tr>
        <td>2012.0</td>
        <td>5.0</td>
        <td>Ellie Goulding</td>
        <td>Ellie Goulding</td>
        <td>Lights</td>
        <td>6210</td>
    </tr>
    <tr>
        <td>2012.0</td>
        <td>6.0</td>
        <td>The Wanted</td>
        <td>The Wanted</td>
        <td>Glad You Came</td>
        <td>6211</td>
    </tr>
    <tr>
        <td>2012.0</td>
        <td>7.0</td>
        <td>Kelly Clarkson</td>
        <td>Kelly Clarkson</td>
        <td>Stronger (What Doesn&#x27;t Kill You)</td>
        <td>6212</td>
    </tr>
</table>




```sql
%%sql
SELECT *
FROM bill_board
WHERE artist IN ('Taylor Swift', 'Usher', 'Ludacris')
LIMIT 10
```

     * postgresql://postgres:***@localhost/portfolio
    10 rows affected.





<table>
    <tr>
        <th>year</th>
        <th>year_rank</th>
        <th>group</th>
        <th>artist</th>
        <th>song_name</th>
        <th>id</th>
    </tr>
    <tr>
        <td>1997.0</td>
        <td>14.0</td>
        <td>Usher</td>
        <td>Usher</td>
        <td>You Make Me Wanna...</td>
        <td>4236</td>
    </tr>
    <tr>
        <td>1998.0</td>
        <td>9.0</td>
        <td>Usher</td>
        <td>Usher</td>
        <td>Nice and Slow</td>
        <td>4338</td>
    </tr>
    <tr>
        <td>1998.0</td>
        <td>15.0</td>
        <td>Usher</td>
        <td>Usher</td>
        <td>You Make Me Wanna...</td>
        <td>4344</td>
    </tr>
    <tr>
        <td>1998.0</td>
        <td>16.0</td>
        <td>Usher</td>
        <td>Usher</td>
        <td>My Way</td>
        <td>4345</td>
    </tr>
    <tr>
        <td>2001.0</td>
        <td>15.0</td>
        <td>Usher</td>
        <td>Usher</td>
        <td>U Remind Me</td>
        <td>4695</td>
    </tr>
    <tr>
        <td>2001.0</td>
        <td>77.0</td>
        <td>Ludacris</td>
        <td>Ludacris</td>
        <td>Southern Hospitality</td>
        <td>4770</td>
    </tr>
    <tr>
        <td>2002.0</td>
        <td>9.0</td>
        <td>Usher</td>
        <td>Usher</td>
        <td>U Got it Bad</td>
        <td>4810</td>
    </tr>
    <tr>
        <td>2002.0</td>
        <td>15.0</td>
        <td>P. Diddy feat. Usher and Loon</td>
        <td>Usher</td>
        <td>I Need a Girl (Part One)</td>
        <td>4819</td>
    </tr>
    <tr>
        <td>2002.0</td>
        <td>16.0</td>
        <td>Usher</td>
        <td>Usher</td>
        <td>U Don&#x27;t have to Call</td>
        <td>4821</td>
    </tr>
    <tr>
        <td>2002.0</td>
        <td>55.0</td>
        <td>Ludacris feat. Mystikal and Infamous 2.0</td>
        <td>Ludacris</td>
        <td>Move Bitch</td>
        <td>4880</td>
    </tr>
</table>



#### A query that shows all of the entries for Elvis and M.C. Hammer.


```sql
%%sql
SELECT * FROM bill_board
WHERE "group" IN ('M.C. Hammer', 'Elvis Presley')
LIMIT 10
```

     * postgresql://postgres:***@localhost/portfolio
    10 rows affected.





<table>
    <tr>
        <th>year</th>
        <th>year_rank</th>
        <th>group</th>
        <th>artist</th>
        <th>song_name</th>
        <th>id</th>
    </tr>
    <tr>
        <td>1956.0</td>
        <td>1.0</td>
        <td>Elvis Presley</td>
        <td>Elvis Presley</td>
        <td>Heartbreak Hotel</td>
        <td>1</td>
    </tr>
    <tr>
        <td>1956.0</td>
        <td>2.0</td>
        <td>Elvis Presley</td>
        <td>Elvis Presley</td>
        <td>Don&#x27;t Be Cruel</td>
        <td>2</td>
    </tr>
    <tr>
        <td>1956.0</td>
        <td>8.0</td>
        <td>Elvis Presley</td>
        <td>Elvis Presley</td>
        <td>Hound Dog</td>
        <td>8</td>
    </tr>
    <tr>
        <td>1956.0</td>
        <td>14.0</td>
        <td>Elvis Presley</td>
        <td>Elvis Presley</td>
        <td>I Want You, I Need You, I Love You</td>
        <td>14</td>
    </tr>
    <tr>
        <td>1956.0</td>
        <td>15.0</td>
        <td>Elvis Presley</td>
        <td>Elvis Presley</td>
        <td>Love Me Tender</td>
        <td>15</td>
    </tr>
    <tr>
        <td>1957.0</td>
        <td>1.0</td>
        <td>Elvis Presley</td>
        <td>Elvis Presley</td>
        <td>All Shook Up</td>
        <td>104</td>
    </tr>
    <tr>
        <td>1957.0</td>
        <td>9.0</td>
        <td>Elvis Presley</td>
        <td>Elvis Presley</td>
        <td>Too Much</td>
        <td>112</td>
    </tr>
    <tr>
        <td>1957.0</td>
        <td>14.0</td>
        <td>Elvis Presley</td>
        <td>Elvis Presley</td>
        <td>Teddy Bear / Loving You</td>
        <td>117</td>
    </tr>
    <tr>
        <td>1957.0</td>
        <td>16.0</td>
        <td>Elvis Presley</td>
        <td>Elvis Presley</td>
        <td>Jailhouse Rock</td>
        <td>119</td>
    </tr>
    <tr>
        <td>1957.0</td>
        <td>56.0</td>
        <td>Elvis Presley</td>
        <td>Elvis Presley</td>
        <td>Love Me</td>
        <td>159</td>
    </tr>
</table>



### SQL BETWEEN

A logical operator in SQL that allows one to select only rows that are within a specific range


```sql
%%sql
SELECT * FROM bill_board
WHERE year_rank BETWEEN 5 AND 10
LIMIT 10
```

     * postgresql://postgres:***@localhost/portfolio
    10 rows affected.





<table>
    <tr>
        <th>year</th>
        <th>year_rank</th>
        <th>group</th>
        <th>artist</th>
        <th>song_name</th>
        <th>id</th>
    </tr>
    <tr>
        <td>1956.0</td>
        <td>5.0</td>
        <td>Gogi Grant</td>
        <td>Gogi Grant</td>
        <td>The Wayward Wind</td>
        <td>5</td>
    </tr>
    <tr>
        <td>1956.0</td>
        <td>6.0</td>
        <td>Les Baxter</td>
        <td>Les Baxter</td>
        <td>The Poor People Of Paris</td>
        <td>6</td>
    </tr>
    <tr>
        <td>1956.0</td>
        <td>7.0</td>
        <td>Doris Day</td>
        <td>Doris Day</td>
        <td>Whatever Will Be Will Be (Que Sera Sera)</td>
        <td>7</td>
    </tr>
    <tr>
        <td>1956.0</td>
        <td>8.0</td>
        <td>Elvis Presley</td>
        <td>Elvis Presley</td>
        <td>Hound Dog</td>
        <td>8</td>
    </tr>
    <tr>
        <td>1956.0</td>
        <td>9.0</td>
        <td>Dean Martin</td>
        <td>Dean Martin</td>
        <td>Memories Are Made Of This</td>
        <td>9</td>
    </tr>
    <tr>
        <td>1956.0</td>
        <td>10.0</td>
        <td>Kay Starr</td>
        <td>Kay Starr</td>
        <td>Rock And Roll Waltz</td>
        <td>10</td>
    </tr>
    <tr>
        <td>1957.0</td>
        <td>5.0</td>
        <td>Jimmy Dorsey</td>
        <td>Jimmy Dorsey</td>
        <td>So Rare</td>
        <td>108</td>
    </tr>
    <tr>
        <td>1957.0</td>
        <td>6.0</td>
        <td>Pat Boone</td>
        <td>Pat Boone</td>
        <td>Don&#x27;t Forbid Me</td>
        <td>109</td>
    </tr>
    <tr>
        <td>1957.0</td>
        <td>7.0</td>
        <td>Guy Mitchell</td>
        <td>Guy Mitchell</td>
        <td>Singing The Blues</td>
        <td>110</td>
    </tr>
    <tr>
        <td>1957.0</td>
        <td>8.0</td>
        <td>Sonny James</td>
        <td>Sonny James</td>
        <td>Young Love</td>
        <td>111</td>
    </tr>
</table>



#### A query that shows all top 100 songs from January 1, 1985 through December 31, 1990.


```sql
%%sql
SELECT * FROM bill_board
WHERE year BETWEEN 1985 AND 1990
LIMIT 10
```

     * postgresql://postgres:***@localhost/portfolio
    10 rows affected.





<table>
    <tr>
        <th>year</th>
        <th>year_rank</th>
        <th>group</th>
        <th>artist</th>
        <th>song_name</th>
        <th>id</th>
    </tr>
    <tr>
        <td>1985.0</td>
        <td>1.0</td>
        <td>Wham!</td>
        <td>Wham!</td>
        <td>Careless Whisper</td>
        <td>2977</td>
    </tr>
    <tr>
        <td>1985.0</td>
        <td>2.0</td>
        <td>Madonna</td>
        <td>Madonna</td>
        <td>Like A Virgin</td>
        <td>2978</td>
    </tr>
    <tr>
        <td>1985.0</td>
        <td>3.0</td>
        <td>Wham!</td>
        <td>Wham!</td>
        <td>Wake Me Up Before You Go-Go</td>
        <td>2979</td>
    </tr>
    <tr>
        <td>1985.0</td>
        <td>4.0</td>
        <td>Foreigner</td>
        <td>Foreigner</td>
        <td>I Want To Know What Love Is</td>
        <td>2980</td>
    </tr>
    <tr>
        <td>1985.0</td>
        <td>5.0</td>
        <td>Chaka Khan</td>
        <td>Chaka Khan</td>
        <td>I Feel For You</td>
        <td>2981</td>
    </tr>
    <tr>
        <td>1985.0</td>
        <td>6.0</td>
        <td>Daryl Hall and John Oates</td>
        <td>Daryl Hall</td>
        <td>Out Of Touch</td>
        <td>2982</td>
    </tr>
    <tr>
        <td>1985.0</td>
        <td>6.0</td>
        <td>Daryl Hall and John Oates</td>
        <td>John Oates</td>
        <td>Out Of Touch</td>
        <td>2983</td>
    </tr>
    <tr>
        <td>1985.0</td>
        <td>7.0</td>
        <td>Tears For Fears</td>
        <td>Tears For Fears</td>
        <td>Everybody Wants To Rule The World</td>
        <td>2984</td>
    </tr>
    <tr>
        <td>1985.0</td>
        <td>8.0</td>
        <td>Dire Straits</td>
        <td>Dire Straits</td>
        <td>Money For Nothing</td>
        <td>2985</td>
    </tr>
    <tr>
        <td>1985.0</td>
        <td>9.0</td>
        <td>Madonna</td>
        <td>Madonna</td>
        <td>Crazy For You</td>
        <td>2986</td>
    </tr>
</table>



### SQL IS NULL


```sql
%%sql
SELECT * FROM bill_board
WHERE artist IS NULL
```

     * postgresql://postgres:***@localhost/portfolio
    9 rows affected.





<table>
    <tr>
        <th>year</th>
        <th>year_rank</th>
        <th>group</th>
        <th>artist</th>
        <th>song_name</th>
        <th>id</th>
    </tr>
    <tr>
        <td>1959.0</td>
        <td>4.0</td>
        <td>Frankie Avalon</td>
        <td>None</td>
        <td>Venus</td>
        <td>308</td>
    </tr>
    <tr>
        <td>1960.0</td>
        <td>20.0</td>
        <td>Roy Orbison</td>
        <td>None</td>
        <td>Only The Lonely</td>
        <td>426</td>
    </tr>
    <tr>
        <td>1961.0</td>
        <td>85.0</td>
        <td>Paul Anka</td>
        <td>None</td>
        <td>Tonight My Love, Tonight</td>
        <td>593</td>
    </tr>
    <tr>
        <td>1962.0</td>
        <td>77.0</td>
        <td>Rick Nelson</td>
        <td>None</td>
        <td>Teen Age Idol</td>
        <td>685</td>
    </tr>
    <tr>
        <td>1985.0</td>
        <td>24.0</td>
        <td>Bryan Adams</td>
        <td>None</td>
        <td>Heaven</td>
        <td>3002</td>
    </tr>
    <tr>
        <td>1991.0</td>
        <td>42.0</td>
        <td>Whitney Houston</td>
        <td>None</td>
        <td>I&#x27;m Your Baby Tonight</td>
        <td>3642</td>
    </tr>
    <tr>
        <td>1997.0</td>
        <td>89.0</td>
        <td>Michael Bolton</td>
        <td>None</td>
        <td>Go The Distance</td>
        <td>4318</td>
    </tr>
    <tr>
        <td>2005.0</td>
        <td>42.0</td>
        <td>Chris Brown</td>
        <td>None</td>
        <td>Run It!</td>
        <td>5280</td>
    </tr>
    <tr>
        <td>2009.0</td>
        <td>94.0</td>
        <td>Zac Brown Band</td>
        <td>None</td>
        <td>Whatever It Is</td>
        <td>5898</td>
    </tr>
</table>



WHERE artist = NULL will not work—you can't perform arithmetic on null values.



#### A query that shows all of the rows for which song_name is null.




```sql
%%sql
SELECT * FROM bill_board
WHERE song_name IS NULL
```

     * postgresql://postgres:***@localhost/portfolio
    6 rows affected.





<table>
    <tr>
        <th>year</th>
        <th>year_rank</th>
        <th>group</th>
        <th>artist</th>
        <th>song_name</th>
        <th>id</th>
    </tr>
    <tr>
        <td>1961.0</td>
        <td>18.0</td>
        <td>Connie Francis</td>
        <td>Connie Francis</td>
        <td>None</td>
        <td>526</td>
    </tr>
    <tr>
        <td>1962.0</td>
        <td>79.0</td>
        <td>Larry Finnegan</td>
        <td>Larry Finnegan</td>
        <td>None</td>
        <td>687</td>
    </tr>
    <tr>
        <td>1963.0</td>
        <td>97.0</td>
        <td>Beach Boys</td>
        <td>Beach Boys</td>
        <td>None</td>
        <td>806</td>
    </tr>
    <tr>
        <td>1974.0</td>
        <td>79.0</td>
        <td>Mike Oldfield</td>
        <td>Mike Oldfield</td>
        <td>None</td>
        <td>1903</td>
    </tr>
    <tr>
        <td>1997.0</td>
        <td>86.0</td>
        <td>Brian McKnight feat. Mase</td>
        <td>Mase</td>
        <td>None</td>
        <td>4315</td>
    </tr>
    <tr>
        <td>2011.0</td>
        <td>87.0</td>
        <td>Jason Derulo</td>
        <td>Jason Derulo</td>
        <td>None</td>
        <td>6183</td>
    </tr>
</table>



### SQL AND


```sql
%%sql
SELECT * FROM bill_board
WHERE year = 2012 and year_rank <=10 and "group" ILIKE '%kha%'

```

     * postgresql://postgres:***@localhost/portfolio
    2 rows affected.





<table>
    <tr>
        <th>year</th>
        <th>year_rank</th>
        <th>group</th>
        <th>artist</th>
        <th>song_name</th>
        <th>id</th>
    </tr>
    <tr>
        <td>2012.0</td>
        <td>4.0</td>
        <td>Maroon 5 feat. Wiz Khalifa</td>
        <td>Maroon 5</td>
        <td>Payphone</td>
        <td>6208</td>
    </tr>
    <tr>
        <td>2012.0</td>
        <td>4.0</td>
        <td>Maroon 5 feat. Wiz Khalifa</td>
        <td>Wiz Khalifa</td>
        <td>Payphone</td>
        <td>6209</td>
    </tr>
</table>



#### A query that surfaces all rows for top-10 hits for which Ludacris is part of the Group.


```sql
%%sql
SELECT * FROM bill_board
WHERE year_rank <= 10 AND "group" ILIKE '%ludacris%'
```

     * postgresql://postgres:***@localhost/portfolio
    7 rows affected.





<table>
    <tr>
        <th>year</th>
        <th>year_rank</th>
        <th>group</th>
        <th>artist</th>
        <th>song_name</th>
        <th>id</th>
    </tr>
    <tr>
        <td>2004.0</td>
        <td>1.0</td>
        <td>Usher feat. Lil Jon and Ludacris</td>
        <td>Usher</td>
        <td>Yeah!</td>
        <td>5082</td>
    </tr>
    <tr>
        <td>2004.0</td>
        <td>1.0</td>
        <td>Usher feat. Lil Jon and Ludacris</td>
        <td>Lil Jon</td>
        <td>Yeah!</td>
        <td>5083</td>
    </tr>
    <tr>
        <td>2004.0</td>
        <td>1.0</td>
        <td>Usher feat. Lil Jon and Ludacris</td>
        <td>Ludacris</td>
        <td>Yeah!</td>
        <td>5084</td>
    </tr>
    <tr>
        <td>2007.0</td>
        <td>10.0</td>
        <td>Fergie feat. Ludacris</td>
        <td>Fergie</td>
        <td>Glamorous</td>
        <td>5508</td>
    </tr>
    <tr>
        <td>2007.0</td>
        <td>10.0</td>
        <td>Fergie feat. Ludacris</td>
        <td>Ludacris</td>
        <td>Glamorous</td>
        <td>5509</td>
    </tr>
    <tr>
        <td>2010.0</td>
        <td>10.0</td>
        <td>Taio Cruz feat. Ludacris</td>
        <td>Taio Cruz</td>
        <td>Break Your Heart</td>
        <td>5922</td>
    </tr>
    <tr>
        <td>2010.0</td>
        <td>10.0</td>
        <td>Taio Cruz feat. Ludacris</td>
        <td>Ludacris</td>
        <td>Break Your Heart</td>
        <td>5923</td>
    </tr>
</table>



#### A query that surfaces the top-ranked records in 1990, 2000, and 2010.


```sql
%%sql
SELECT * FROM bill_board
WHERE year_rank = 1 and year IN (1990, 2000, 2010)
```

     * postgresql://postgres:***@localhost/portfolio
    3 rows affected.





<table>
    <tr>
        <th>year</th>
        <th>year_rank</th>
        <th>group</th>
        <th>artist</th>
        <th>song_name</th>
        <th>id</th>
    </tr>
    <tr>
        <td>1990.0</td>
        <td>1.0</td>
        <td>Wilson Phillips</td>
        <td>Wilson Phillips</td>
        <td>Hold On</td>
        <td>3498</td>
    </tr>
    <tr>
        <td>2000.0</td>
        <td>1.0</td>
        <td>Faith Hill</td>
        <td>Faith Hill</td>
        <td>Breathe</td>
        <td>4563</td>
    </tr>
    <tr>
        <td>2010.0</td>
        <td>1.0</td>
        <td>Ke$ha</td>
        <td>Ke$ha</td>
        <td>TiK ToK</td>
        <td>5909</td>
    </tr>
</table>



#### A query that lists all songs from the 1960s with "love" in the title.


```sql
%%sql
SELECT * FROM bill_board
WHERE song_name ILIKE '%love' AND year >= 1960
LIMIT 10
```

     * postgresql://postgres:***@localhost/portfolio
    10 rows affected.





<table>
    <tr>
        <th>year</th>
        <th>year_rank</th>
        <th>group</th>
        <th>artist</th>
        <th>song_name</th>
        <th>id</th>
    </tr>
    <tr>
        <td>1960.0</td>
        <td>23.0</td>
        <td>Paul Anka</td>
        <td>Paul Anka</td>
        <td>Puppy Love</td>
        <td>429</td>
    </tr>
    <tr>
        <td>1960.0</td>
        <td>45.0</td>
        <td>Johnny Preston</td>
        <td>Johnny Preston</td>
        <td>Cradle Of Love</td>
        <td>452</td>
    </tr>
    <tr>
        <td>1960.0</td>
        <td>65.0</td>
        <td>Marv Johnson</td>
        <td>Marv Johnson</td>
        <td>I Love The Way You Love</td>
        <td>472</td>
    </tr>
    <tr>
        <td>1961.0</td>
        <td>14.0</td>
        <td>Shirelles</td>
        <td>Shirelles</td>
        <td>Dedicated To The One I Love</td>
        <td>522</td>
    </tr>
    <tr>
        <td>1961.0</td>
        <td>30.0</td>
        <td>Steve Lawrence</td>
        <td>Steve Lawrence</td>
        <td>Portrait Of My Love</td>
        <td>538</td>
    </tr>
    <tr>
        <td>1962.0</td>
        <td>57.0</td>
        <td>Elvis Presley</td>
        <td>Elvis Presley</td>
        <td>Can&#x27;t Help Falling In Love</td>
        <td>665</td>
    </tr>
    <tr>
        <td>1962.0</td>
        <td>96.0</td>
        <td>Eddie Hodges</td>
        <td>Eddie Hodges</td>
        <td>(Girls, Girls, Girls) Were Made To Love</td>
        <td>704</td>
    </tr>
    <tr>
        <td>1963.0</td>
        <td>15.0</td>
        <td>Tymes</td>
        <td>Tymes</td>
        <td>So Much In Love</td>
        <td>723</td>
    </tr>
    <tr>
        <td>1963.0</td>
        <td>63.0</td>
        <td>Bill Pursell</td>
        <td>Bill Pursell</td>
        <td>Our Winter Love</td>
        <td>772</td>
    </tr>
    <tr>
        <td>1964.0</td>
        <td>21.0</td>
        <td>Dixie Cups</td>
        <td>Dixie Cups</td>
        <td>Chapel Of Love</td>
        <td>830</td>
    </tr>
</table>



### SQL OR
A logical operator in SQL that allows one to select rows that satisfy either of two conditions


```sql
%%sql
SELECT *
  FROM bill_board
 WHERE year_rank = 5 OR artist = 'Gotye'
LIMIT 10
```

     * postgresql://postgres:***@localhost/portfolio
    10 rows affected.





<table>
    <tr>
        <th>year</th>
        <th>year_rank</th>
        <th>group</th>
        <th>artist</th>
        <th>song_name</th>
        <th>id</th>
    </tr>
    <tr>
        <td>1956.0</td>
        <td>5.0</td>
        <td>Gogi Grant</td>
        <td>Gogi Grant</td>
        <td>The Wayward Wind</td>
        <td>5</td>
    </tr>
    <tr>
        <td>1957.0</td>
        <td>5.0</td>
        <td>Jimmy Dorsey</td>
        <td>Jimmy Dorsey</td>
        <td>So Rare</td>
        <td>108</td>
    </tr>
    <tr>
        <td>1958.0</td>
        <td>5.0</td>
        <td>Perez Prado</td>
        <td>Perez Prado</td>
        <td>Patricia</td>
        <td>208</td>
    </tr>
    <tr>
        <td>1959.0</td>
        <td>5.0</td>
        <td>Paul Anka</td>
        <td>Paul Anka</td>
        <td>Lonely Boy</td>
        <td>309</td>
    </tr>
    <tr>
        <td>1960.0</td>
        <td>5.0</td>
        <td>Mark Dinning</td>
        <td>Mark Dinning</td>
        <td>Teen Angel</td>
        <td>411</td>
    </tr>
    <tr>
        <td>1961.0</td>
        <td>5.0</td>
        <td>Del Shannon</td>
        <td>Del Shannon</td>
        <td>Runaway</td>
        <td>513</td>
    </tr>
    <tr>
        <td>1962.0</td>
        <td>5.0</td>
        <td>David Rose</td>
        <td>David Rose</td>
        <td>The Stripper</td>
        <td>613</td>
    </tr>
    <tr>
        <td>1963.0</td>
        <td>5.0</td>
        <td>Chiffons</td>
        <td>Chiffons</td>
        <td>He&#x27;s So Fine</td>
        <td>713</td>
    </tr>
    <tr>
        <td>1964.0</td>
        <td>5.0</td>
        <td>Beach Boys</td>
        <td>Beach Boys</td>
        <td>I Get Around</td>
        <td>814</td>
    </tr>
    <tr>
        <td>1965.0</td>
        <td>5.0</td>
        <td>Righteous Brothers</td>
        <td>Righteous Brothers</td>
        <td>You&#x27;ve Lost That Lovin&#x27; Feelin&#x27;</td>
        <td>916</td>
    </tr>
</table>



#### A query that returns all rows for top-10 songs that featured either Katy Perry or Bon Jovi.


```sql
%%sql
SELECT * FROM bill_board
WHERE year_rank <= 10 AND (artist ILIKE '%katy%' OR  artist ILIKE '%jovi%')
```

     * postgresql://postgres:***@localhost/portfolio
    6 rows affected.





<table>
    <tr>
        <th>year</th>
        <th>year_rank</th>
        <th>group</th>
        <th>artist</th>
        <th>song_name</th>
        <th>id</th>
    </tr>
    <tr>
        <td>1987.0</td>
        <td>10.0</td>
        <td>Bon Jovi</td>
        <td>Bon Jovi</td>
        <td>Livin&#x27; On A Prayer</td>
        <td>3193</td>
    </tr>
    <tr>
        <td>1990.0</td>
        <td>10.0</td>
        <td>Jon Bon Jovi</td>
        <td>Jon Bon Jovi</td>
        <td>Blaze Of Glory</td>
        <td>3507</td>
    </tr>
    <tr>
        <td>2010.0</td>
        <td>4.0</td>
        <td>Katy Perry feat. Snoop Dogg</td>
        <td>Katy Perry</td>
        <td>California Gurls</td>
        <td>5912</td>
    </tr>
    <tr>
        <td>2011.0</td>
        <td>3.0</td>
        <td>Katy Perry</td>
        <td>Katy Perry</td>
        <td>Firework</td>
        <td>6060</td>
    </tr>
    <tr>
        <td>2011.0</td>
        <td>4.0</td>
        <td>Katy Perry feat. Kanye West</td>
        <td>Katy Perry</td>
        <td>E.T.</td>
        <td>6061</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>10.0</td>
        <td>Katy Perry</td>
        <td>Katy Perry</td>
        <td>Roar</td>
        <td>6351</td>
    </tr>
</table>



#### A query that returns all songs with titles that contain the word "California" in either the 1970s or 1990s.




```sql
%%sql
SELECT * FROM bill_board
WHERE song_name ILIKE '%california%' AND (year BETWEEN 1970 AND 1979 OR year BETWEEN 1990 AND 1999)
```

     * postgresql://postgres:***@localhost/portfolio
    3 rows affected.





<table>
    <tr>
        <th>year</th>
        <th>year_rank</th>
        <th>group</th>
        <th>artist</th>
        <th>song_name</th>
        <th>id</th>
    </tr>
    <tr>
        <td>1973.0</td>
        <td>98.0</td>
        <td>Albert Hammond</td>
        <td>Albert Hammond</td>
        <td>It Never Rains In Southern California</td>
        <td>1820</td>
    </tr>
    <tr>
        <td>1977.0</td>
        <td>19.0</td>
        <td>Eagles</td>
        <td>Eagles</td>
        <td>Hotel California</td>
        <td>2151</td>
    </tr>
    <tr>
        <td>1996.0</td>
        <td>17.0</td>
        <td>2Pac</td>
        <td>2Pac</td>
        <td>How Do U Want It / California Love</td>
        <td>4133</td>
    </tr>
</table>



#### A query that lists all top-100 recordings that feature Dr. Dre before 2001 or after 2009.


```sql
%%sql
SELECT * FROM bill_board
WHERE year_rank <= 100 AND artist ILIKE '%dr. dre%' AND (year <= 2001 OR year >= 2009)
```

     * postgresql://postgres:***@localhost/portfolio
    9 rows affected.





<table>
    <tr>
        <th>year</th>
        <th>year_rank</th>
        <th>group</th>
        <th>artist</th>
        <th>song_name</th>
        <th>id</th>
    </tr>
    <tr>
        <td>1993.0</td>
        <td>11.0</td>
        <td>Dr. Dre</td>
        <td>Dr. Dre</td>
        <td>Nuthin&#x27; But A &quot;G&quot; Thang</td>
        <td>3815</td>
    </tr>
    <tr>
        <td>1993.0</td>
        <td>53.0</td>
        <td>Dr. Dre</td>
        <td>Dr. Dre</td>
        <td>Dre Day</td>
        <td>3860</td>
    </tr>
    <tr>
        <td>1995.0</td>
        <td>53.0</td>
        <td>Dr. Dre</td>
        <td>Dr. Dre</td>
        <td>Keep Their Heads Ringin&#x27;</td>
        <td>4066</td>
    </tr>
    <tr>
        <td>1996.0</td>
        <td>42.0</td>
        <td>BLACKstreet (feat. Dr. Dre)</td>
        <td>BLACKstreet (feat. Dr. Dre)</td>
        <td>No Diggity</td>
        <td>4159</td>
    </tr>
    <tr>
        <td>1997.0</td>
        <td>23.0</td>
        <td>BLACKstreet feat. Dr. Dre</td>
        <td>Dr. Dre</td>
        <td>No Diggity</td>
        <td>4247</td>
    </tr>
    <tr>
        <td>2000.0</td>
        <td>73.0</td>
        <td>Dr. Dre feat. Eminem</td>
        <td>Dr. Dre</td>
        <td>Forget About Dre</td>
        <td>4644</td>
    </tr>
    <tr>
        <td>2000.0</td>
        <td>76.0</td>
        <td>Dr. Dre feat. Snoop Dogg</td>
        <td>Dr. Dre</td>
        <td>The Next Episode</td>
        <td>4648</td>
    </tr>
    <tr>
        <td>2009.0</td>
        <td>47.0</td>
        <td>Eminem, Dr. Dre and 50 Cent</td>
        <td>Dr. Dre</td>
        <td>Crack A Bottle</td>
        <td>5838</td>
    </tr>
    <tr>
        <td>2011.0</td>
        <td>51.0</td>
        <td>Dr. Dre feat. Eminem and Skylar Grey</td>
        <td>Dr. Dre</td>
        <td>I Need A Doctor</td>
        <td>6132</td>
    </tr>
</table>



### SQL NOT
The NOT operator displays a record if the condition(s) is NOT TRUE


```sql
%%sql
SELECT * FROM bill_board
WHERE year = 2013 AND year_rank BETWEEN 0 AND 50
```

     * postgresql://postgres:***@localhost/portfolio
    81 rows affected.





<table>
    <tr>
        <th>year</th>
        <th>year_rank</th>
        <th>group</th>
        <th>artist</th>
        <th>song_name</th>
        <th>id</th>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>1.0</td>
        <td>Macklemore and Ryan Lewis feat. Wanz</td>
        <td>Macklemore</td>
        <td>Thrift Shop</td>
        <td>6334</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>1.0</td>
        <td>Macklemore and Ryan Lewis feat. Wanz</td>
        <td>Ryan Lewis</td>
        <td>Thrift Shop</td>
        <td>6335</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>1.0</td>
        <td>Macklemore and Ryan Lewis feat. Wanz</td>
        <td>Wanz</td>
        <td>Thrift Shop</td>
        <td>6336</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>2.0</td>
        <td>Robin Thicke feat. T.I. and Pharrell</td>
        <td>Robin Thicke</td>
        <td>Blurred Lines</td>
        <td>6337</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>2.0</td>
        <td>Robin Thicke feat. T.I. and Pharrell</td>
        <td>T.I.</td>
        <td>Blurred Lines</td>
        <td>6338</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>2.0</td>
        <td>Robin Thicke feat. T.I. and Pharrell</td>
        <td>Pharrell</td>
        <td>Blurred Lines</td>
        <td>6339</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>3.0</td>
        <td>Imagine Dragons</td>
        <td>Imagine Dragons</td>
        <td>Radioactive</td>
        <td>6340</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>4.0</td>
        <td>Baauer</td>
        <td>Baauer</td>
        <td>Harlem Shake</td>
        <td>6341</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>5.0</td>
        <td>Macklemore and Ryan Lewis feat. Ray Dalton</td>
        <td>Macklemore</td>
        <td>Can&#x27;t Hold Us</td>
        <td>6342</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>5.0</td>
        <td>Macklemore and Ryan Lewis feat. Ray Dalton</td>
        <td>Ryan Lewis</td>
        <td>Can&#x27;t Hold Us</td>
        <td>6343</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>5.0</td>
        <td>Macklemore and Ryan Lewis feat. Ray Dalton</td>
        <td>Ray Dalton</td>
        <td>Can&#x27;t Hold Us</td>
        <td>6344</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>6.0</td>
        <td>Justin Timberlake</td>
        <td>Justin Timberlake</td>
        <td>Mirrors</td>
        <td>6345</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>7.0</td>
        <td>P!nk feat. Nate Ruess</td>
        <td>P!nk</td>
        <td>Just Give Me A Reason</td>
        <td>6346</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>7.0</td>
        <td>P!nk feat. Nate Ruess</td>
        <td>Nate Ruess</td>
        <td>Just Give Me A Reason</td>
        <td>6347</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>8.0</td>
        <td>Bruno Mars</td>
        <td>Bruno Mars</td>
        <td>When I Was Your Man</td>
        <td>6348</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>9.0</td>
        <td>Florida Georgia Line feat. Nelly</td>
        <td>Florida Georgia Line</td>
        <td>Cruise</td>
        <td>6349</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>9.0</td>
        <td>Florida Georgia Line feat. Nelly</td>
        <td>Nelly</td>
        <td>Cruise</td>
        <td>6350</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>10.0</td>
        <td>Katy Perry</td>
        <td>Katy Perry</td>
        <td>Roar</td>
        <td>6351</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>11.0</td>
        <td>Bruno Mars</td>
        <td>Bruno Mars</td>
        <td>Locked Out Of Heaven</td>
        <td>6352</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>12.0</td>
        <td>Lumineers</td>
        <td>Lumineers</td>
        <td>Ho Hey</td>
        <td>6353</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>13.0</td>
        <td>Rihanna feat. Mikky Ekko</td>
        <td>Rihanna</td>
        <td>Stay</td>
        <td>6354</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>13.0</td>
        <td>Rihanna feat. Mikky Ekko</td>
        <td>Mikky Ekko</td>
        <td>Stay</td>
        <td>6355</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>14.0</td>
        <td>Daft Punk feat. Pharrell Williams</td>
        <td>Daft Punk</td>
        <td>Get Lucky</td>
        <td>6356</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>14.0</td>
        <td>Daft Punk feat. Pharrell Williams</td>
        <td>Pharrell Williams</td>
        <td>Get Lucky</td>
        <td>6357</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>15.0</td>
        <td>Lorde</td>
        <td>Lorde</td>
        <td>Royals</td>
        <td>6358</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>16.0</td>
        <td>Taylor Swift</td>
        <td>Taylor Swift</td>
        <td>I Knew You Were Trouble</td>
        <td>6359</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>17.0</td>
        <td>Miley Cyrus</td>
        <td>Miley Cyrus</td>
        <td>We Can&#x27;t Stop</td>
        <td>6360</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>18.0</td>
        <td>Miley Cyrus</td>
        <td>Miley Cyrus</td>
        <td>Wrecking Ball</td>
        <td>6361</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>19.0</td>
        <td>Avicii</td>
        <td>Avicii</td>
        <td>Wake Me Up!</td>
        <td>6362</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>20.0</td>
        <td>Justin Timberlake feat. Jay Z</td>
        <td>Justin Timberlake</td>
        <td>Suit and Tie</td>
        <td>6363</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>20.0</td>
        <td>Justin Timberlake feat. Jay Z</td>
        <td>Jay Z</td>
        <td>Suit and Tie</td>
        <td>6364</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>21.0</td>
        <td>Anna Kendrick</td>
        <td>Anna Kendrick</td>
        <td>Cups (Pitch Perfect&#x27;s When I&#x27;m Gone)</td>
        <td>6365</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>22.0</td>
        <td>Jay Z feat. Justin Timberlake</td>
        <td>Jay Z</td>
        <td>Holy Grail</td>
        <td>6366</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>22.0</td>
        <td>Jay Z feat. Justin Timberlake</td>
        <td>Justin Timberlake</td>
        <td>Holy Grail</td>
        <td>6367</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>23.0</td>
        <td>will.i.am and Britney Spears</td>
        <td>will.i.am</td>
        <td>Scream and Shout</td>
        <td>6368</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>23.0</td>
        <td>will.i.am and Britney Spears</td>
        <td>Britney Spears</td>
        <td>Scream and Shout</td>
        <td>6369</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>24.0</td>
        <td>Zedd feat. Foxes</td>
        <td>Zedd</td>
        <td>Clarity</td>
        <td>6370</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>24.0</td>
        <td>Zedd feat. Foxes</td>
        <td>Foxes</td>
        <td>Clarity</td>
        <td>6371</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>25.0</td>
        <td>AWOLNATION</td>
        <td>AWOLNATION</td>
        <td>Sail</td>
        <td>6372</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>26.0</td>
        <td>Swedish House Mafia feat. John Martin</td>
        <td>Swedish House Mafia</td>
        <td>Don&#x27;t You Worry Child</td>
        <td>6373</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>26.0</td>
        <td>Swedish House Mafia feat. John Martin</td>
        <td>John Martin</td>
        <td>Don&#x27;t You Worry Child</td>
        <td>6374</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>27.0</td>
        <td>Rihanna</td>
        <td>Rihanna</td>
        <td>Diamonds</td>
        <td>6375</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>28.0</td>
        <td>Icona Pop feat. Charli XCX</td>
        <td>Icona Pop</td>
        <td>I Love It</td>
        <td>6376</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>28.0</td>
        <td>Icona Pop feat. Charli XCX</td>
        <td>Charli XCX</td>
        <td>I Love It</td>
        <td>6377</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>29.0</td>
        <td>Capital Cities</td>
        <td>Capital Cities</td>
        <td>Safe And Sound</td>
        <td>6378</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>30.0</td>
        <td>Bruno Mars</td>
        <td>Bruno Mars</td>
        <td>Treasure</td>
        <td>6379</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>31.0</td>
        <td>Ariana Grande feat. Mac Miller</td>
        <td>Ariana Grande</td>
        <td>The Way</td>
        <td>6380</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>31.0</td>
        <td>Ariana Grande feat. Mac Miller</td>
        <td>Mac Miller</td>
        <td>The Way</td>
        <td>6381</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>32.0</td>
        <td>Drake</td>
        <td>Drake</td>
        <td>Started From The Bottom</td>
        <td>6382</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>33.0</td>
        <td>Selena Gomez</td>
        <td>Selena Gomez</td>
        <td>Come and Get It</td>
        <td>6383</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>34.0</td>
        <td>Drake feat. Majid Jordan</td>
        <td>Drake</td>
        <td>Hold On, We&#x27;re Going Home</td>
        <td>6384</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>34.0</td>
        <td>Drake feat. Majid Jordan</td>
        <td>Majid Jordan</td>
        <td>Hold On, We&#x27;re Going Home</td>
        <td>6385</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>35.0</td>
        <td>Maroon 5</td>
        <td>Maroon 5</td>
        <td>Daylight</td>
        <td>6386</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>36.0</td>
        <td>Pitbull feat. Christina Aguilera</td>
        <td>Pitbull</td>
        <td>Feel This Moment</td>
        <td>6387</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>36.0</td>
        <td>Pitbull feat. Christina Aguilera</td>
        <td>Christina Aguilera</td>
        <td>Feel This Moment</td>
        <td>6388</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>37.0</td>
        <td>Lady Gaga</td>
        <td>Lady Gaga</td>
        <td>Applause</td>
        <td>6389</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>38.0</td>
        <td>Maroon 5</td>
        <td>Maroon 5</td>
        <td>One More Night</td>
        <td>6390</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>39.0</td>
        <td>Lil Wayne feat. Drake and Future</td>
        <td>Lil Wayne</td>
        <td>Love Me</td>
        <td>6391</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>39.0</td>
        <td>Lil Wayne feat. Drake and Future</td>
        <td>Drake</td>
        <td>Love Me</td>
        <td>6392</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>39.0</td>
        <td>Lil Wayne feat. Drake and Future</td>
        <td>Future</td>
        <td>Love Me</td>
        <td>6393</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>40.0</td>
        <td>Fall Out Boy</td>
        <td>Fall Out Boy</td>
        <td>My Songs Know What You Did In The Dark (Light Em Up)</td>
        <td>6394</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>41.0</td>
        <td>A$AP Rocky feat. Drake, 2 Chainz and Kendrick Lamar</td>
        <td>A$AP Rocky</td>
        <td>F**kin Problems</td>
        <td>6395</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>41.0</td>
        <td>A$AP Rocky feat. Drake, 2 Chainz and Kendrick Lamar</td>
        <td>Drake</td>
        <td>F**kin Problems</td>
        <td>6396</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>41.0</td>
        <td>A$AP Rocky feat. Drake, 2 Chainz and Kendrick Lamar</td>
        <td>2 Chainz</td>
        <td>F**kin Problems</td>
        <td>6397</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>41.0</td>
        <td>A$AP Rocky feat. Drake, 2 Chainz and Kendrick Lamar</td>
        <td>Kendrick Lamar</td>
        <td>F**kin Problems</td>
        <td>6398</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>42.0</td>
        <td>Justin Bieber feat. Nicki Minaj</td>
        <td>Justin Bieber</td>
        <td>Beauty And A Beat</td>
        <td>6399</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>42.0</td>
        <td>Justin Bieber feat. Nicki Minaj</td>
        <td>Nicki Minaj</td>
        <td>Beauty And A Beat</td>
        <td>6400</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>43.0</td>
        <td>Macklemore and Ryan Lewis feat. Mary Lambert</td>
        <td>Macklemore</td>
        <td>Same Love</td>
        <td>6401</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>43.0</td>
        <td>Macklemore and Ryan Lewis feat. Mary Lambert</td>
        <td>Ryan Lewis</td>
        <td>Same Love</td>
        <td>6402</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>43.0</td>
        <td>Macklemore and Ryan Lewis feat. Mary Lambert</td>
        <td>Mary Lambert</td>
        <td>Same Love</td>
        <td>6403</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>44.0</td>
        <td>Calvin Harris feat. Florence Welch</td>
        <td>Calvin Harris</td>
        <td>Sweet Nothing</td>
        <td>6404</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>44.0</td>
        <td>Calvin Harris feat. Florence Welch</td>
        <td>Florence Welch</td>
        <td>Sweet Nothing</td>
        <td>6405</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>45.0</td>
        <td>Lana Del Rey and Cedric Gervais</td>
        <td>Lana Del Rey</td>
        <td>Summertime Sadness</td>
        <td>6406</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>45.0</td>
        <td>Lana Del Rey and Cedric Gervais</td>
        <td>Cedric Gervais</td>
        <td>Summertime Sadness</td>
        <td>6407</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>46.0</td>
        <td>Phillip Phillips</td>
        <td>Phillip Phillips</td>
        <td>Home</td>
        <td>6408</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>47.0</td>
        <td>Imagine Dragons</td>
        <td>Imagine Dragons</td>
        <td>It&#x27;s Time</td>
        <td>6409</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>48.0</td>
        <td>J. Cole feat. Miguel</td>
        <td>J. Cole</td>
        <td>Power Trip</td>
        <td>6410</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>48.0</td>
        <td>J. Cole feat. Miguel</td>
        <td>Miguel</td>
        <td>Power Trip</td>
        <td>6411</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>49.0</td>
        <td>Alicia Keys feat. Nicki Minaj</td>
        <td>Alicia Keys</td>
        <td>Girl On Fire</td>
        <td>6412</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>49.0</td>
        <td>Alicia Keys feat. Nicki Minaj</td>
        <td>Nicki Minaj</td>
        <td>Girl On Fire</td>
        <td>6413</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>50.0</td>
        <td>Demi Lovato</td>
        <td>Demi Lovato</td>
        <td>Heart Attack</td>
        <td>6414</td>
    </tr>
</table>




```sql
%%sql
SELECT * FROM bill_board
WHERE year = 2013 AND year_rank NOT BETWEEN 0 AND 50
```

     * postgresql://postgres:***@localhost/portfolio
    62 rows affected.





<table>
    <tr>
        <th>year</th>
        <th>year_rank</th>
        <th>group</th>
        <th>artist</th>
        <th>song_name</th>
        <th>id</th>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>51.0</td>
        <td>Maroon 5</td>
        <td>Maroon 5</td>
        <td>Love Somebody</td>
        <td>6415</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>52.0</td>
        <td>Mumford and Sons</td>
        <td>Mumford and Sons</td>
        <td>I Will Wait</td>
        <td>6416</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>53.0</td>
        <td>P!nk</td>
        <td>P!nk</td>
        <td>Try</td>
        <td>6417</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>54.0</td>
        <td>Darius Rucker</td>
        <td>Darius Rucker</td>
        <td>Wagon Wheel</td>
        <td>6418</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>55.0</td>
        <td>Psy</td>
        <td>Psy</td>
        <td>Gangnam Style</td>
        <td>6419</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>56.0</td>
        <td>Calvin Harris feat. Ellie Goulding</td>
        <td>Calvin Harris</td>
        <td>I Need Your Love</td>
        <td>6420</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>56.0</td>
        <td>Calvin Harris feat. Ellie Goulding</td>
        <td>Ellie Goulding</td>
        <td>I Need Your Love</td>
        <td>6421</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>57.0</td>
        <td>Ke$ha</td>
        <td>Ke$ha</td>
        <td>Die Young</td>
        <td>6422</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>58.0</td>
        <td>fun.</td>
        <td>fun.</td>
        <td>Some Nights</td>
        <td>6423</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>59.0</td>
        <td>Wale feat. Tiara Thomas or Rihanna</td>
        <td>Wale</td>
        <td>Bad</td>
        <td>6424</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>59.0</td>
        <td>Wale feat. Tiara Thomas or Rihanna</td>
        <td>Tiara Thomas</td>
        <td>Bad</td>
        <td>6425</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>59.0</td>
        <td>Wale feat. Tiara Thomas or Rihanna</td>
        <td>Rihanna</td>
        <td>Bad</td>
        <td>6426</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>60.0</td>
        <td>Blake Shelton feat. Pistol Annies and Friends</td>
        <td>Blake Shelton</td>
        <td>Boys &#x27;Round Here</td>
        <td>6427</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>60.0</td>
        <td>Blake Shelton feat. Pistol Annies and Friends</td>
        <td>Piston Annies</td>
        <td>Boys &#x27;Round Here</td>
        <td>6428</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>61.0</td>
        <td>Phillip Phillips</td>
        <td>Phillip Phillips</td>
        <td>Gone, Gone, Gone</td>
        <td>6429</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>62.0</td>
        <td>Imagine Dragons</td>
        <td>Imagine Dragons</td>
        <td>Demons</td>
        <td>6430</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>63.0</td>
        <td>OneRepublic</td>
        <td>OneRepublic</td>
        <td>Counting Stars</td>
        <td>6431</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>64.0</td>
        <td>Flo Rida</td>
        <td>Flo Rida</td>
        <td>I Cry</td>
        <td>6432</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>65.0</td>
        <td>Of Monsters And Men</td>
        <td>Of Monsters And Men</td>
        <td>Little Talks</td>
        <td>6433</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>66.0</td>
        <td>Jason Derulo</td>
        <td>Jason Derulo</td>
        <td>The Other Side</td>
        <td>6434</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>67.0</td>
        <td>Eminem</td>
        <td>Eminem</td>
        <td>Berzerk</td>
        <td>6435</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>68.0</td>
        <td>Kelly Clarkson</td>
        <td>Kelly Clarkson</td>
        <td>Catch My Breath</td>
        <td>6436</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>69.0</td>
        <td>Luke Bryan</td>
        <td>Luke Bryan</td>
        <td>Crash My Party</td>
        <td>6437</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>70.0</td>
        <td>Rihanna</td>
        <td>Rihanna</td>
        <td>Pour It Up</td>
        <td>6438</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>71.0</td>
        <td>Taylor Swift</td>
        <td>Taylor Swift</td>
        <td>22</td>
        <td>6439</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>72.0</td>
        <td>Hunter Hayes</td>
        <td>Hunter Hayes</td>
        <td>I Want Crazy</td>
        <td>6440</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>73.0</td>
        <td>Ylvis</td>
        <td>Ylvis</td>
        <td>The Fox</td>
        <td>6441</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>74.0</td>
        <td>One Direction</td>
        <td>One Direction</td>
        <td>Best Song Ever</td>
        <td>6442</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>75.0</td>
        <td>Ed Sheeran</td>
        <td>Ed Sheeran</td>
        <td>The A Team</td>
        <td>6443</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>76.0</td>
        <td>fun.</td>
        <td>fun.</td>
        <td>Carry On</td>
        <td>6444</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>77.0</td>
        <td>Tim McGraw with Taylor Swift</td>
        <td>Tim McGraw with Taylor Swift</td>
        <td>Highway Don&#x27;t Care</td>
        <td>6445</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>78.0</td>
        <td>Luke Bryan</td>
        <td>Luke Bryan</td>
        <td>That&#x27;s My Kind Of Night</td>
        <td>6446</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>79.0</td>
        <td>Kendrick Lamar</td>
        <td>Kendrick Lamar</td>
        <td>Swimming Pools (Drank)</td>
        <td>6447</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>80.0</td>
        <td>Blake Shelton</td>
        <td>Blake Shelton</td>
        <td>Sure Be Cool If You Did</td>
        <td>6448</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>81.0</td>
        <td>Mariah Carey feat. Miguel</td>
        <td>Mariah Carey</td>
        <td>#Beautiful</td>
        <td>6449</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>81.0</td>
        <td>Mariah Carey feat. Miguel</td>
        <td>Miguel</td>
        <td>#Beautiful</td>
        <td>6450</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>82.0</td>
        <td>Olly Murs feat. Flo Rida</td>
        <td>Olly Murs</td>
        <td>Troublemaker</td>
        <td>6451</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>82.0</td>
        <td>Olly Murs feat. Flo Rida</td>
        <td>Flo Rida</td>
        <td>Troublemaker</td>
        <td>6452</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>83.0</td>
        <td>Ciara</td>
        <td>Ciara</td>
        <td>Body Party</td>
        <td>6453</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>84.0</td>
        <td>Miguel</td>
        <td>Miguel</td>
        <td>Adorn</td>
        <td>6454</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>85.0</td>
        <td>The Script feat. will.i.am</td>
        <td>The Script</td>
        <td>Hall Of Fame</td>
        <td>6455</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>85.0</td>
        <td>The Script feat. will.i.am</td>
        <td>will.i.am</td>
        <td>Hall Of Fame</td>
        <td>6456</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>86.0</td>
        <td>Ne-Yo</td>
        <td>Ne-Yo</td>
        <td>Let Me Love You (Until You Learn To Love Yourself)</td>
        <td>6457</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>87.0</td>
        <td>Rocko feat. Future and Rick Ross</td>
        <td>Rocko</td>
        <td>U.O.E.N.O.</td>
        <td>6458</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>87.0</td>
        <td>Rocko feat. Future and Rick Ross</td>
        <td>Future</td>
        <td>U.O.E.N.O.</td>
        <td>6459</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>87.0</td>
        <td>Rocko feat. Future and Rick Ross</td>
        <td>Rick Ross</td>
        <td>U.O.E.N.O.</td>
        <td>6460</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>88.0</td>
        <td>Emeli Sande</td>
        <td>Emeli Sande</td>
        <td>Next To Me</td>
        <td>6461</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>89.0</td>
        <td>Miranda Lambert</td>
        <td>Miranda Lambert</td>
        <td>Mama&#x27;s Broken Heart</td>
        <td>6462</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>90.0</td>
        <td>Thomas Rhett</td>
        <td>Thomas Rhett</td>
        <td>It Goes Like This</td>
        <td>6463</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>91.0</td>
        <td>Ace Hood feat. Future and Rick Ross</td>
        <td>Ace Hood</td>
        <td>Bugatti</td>
        <td>6464</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>91.0</td>
        <td>Ace Hood feat. Future and Rick Ross</td>
        <td>Future</td>
        <td>Bugatti</td>
        <td>6465</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>91.0</td>
        <td>Ace Hood feat. Future and Rick Ross</td>
        <td>Rick Ross</td>
        <td>Bugatti</td>
        <td>6466</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>92.0</td>
        <td>Hunter Hayes</td>
        <td>Hunter Hayes</td>
        <td>Wanted</td>
        <td>6467</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>93.0</td>
        <td>Lady Antebellum</td>
        <td>Lady Antebellum</td>
        <td>Downtown</td>
        <td>6468</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>94.0</td>
        <td>Florida Georgia Line</td>
        <td>Florida Georgia Line</td>
        <td>Get Your Shine On</td>
        <td>6469</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>95.0</td>
        <td>will.i.am feat. Justin Bieber</td>
        <td>will.i.am</td>
        <td>#thatPOWER</td>
        <td>6470</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>95.0</td>
        <td>will.i.am feat. Justin Bieber</td>
        <td>Justin Bieber</td>
        <td>#thatPOWER</td>
        <td>6471</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>96.0</td>
        <td>Sara Bareilles</td>
        <td>Sara Bareilles</td>
        <td>Brave</td>
        <td>6472</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>97.0</td>
        <td>Passenger</td>
        <td>Passenger</td>
        <td>Let Her Go</td>
        <td>6473</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>98.0</td>
        <td>Randy Houser</td>
        <td>Randy Houser</td>
        <td>Runnin&#x27; Outta Moonlight</td>
        <td>6474</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>99.0</td>
        <td>2 Chainz</td>
        <td>2 Chainz</td>
        <td>I&#x27;m Different</td>
        <td>6475</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>100.0</td>
        <td>Paramore</td>
        <td>Paramore</td>
        <td>Still Into You</td>
        <td>6476</td>
    </tr>
</table>




```sql
%%sql
SELECT * FROM bill_board
WHERE year = 2013
    AND year_rank <= 3
```

     * postgresql://postgres:***@localhost/portfolio
    7 rows affected.





<table>
    <tr>
        <th>year</th>
        <th>year_rank</th>
        <th>group</th>
        <th>artist</th>
        <th>song_name</th>
        <th>id</th>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>1.0</td>
        <td>Macklemore and Ryan Lewis feat. Wanz</td>
        <td>Macklemore</td>
        <td>Thrift Shop</td>
        <td>6334</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>1.0</td>
        <td>Macklemore and Ryan Lewis feat. Wanz</td>
        <td>Ryan Lewis</td>
        <td>Thrift Shop</td>
        <td>6335</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>1.0</td>
        <td>Macklemore and Ryan Lewis feat. Wanz</td>
        <td>Wanz</td>
        <td>Thrift Shop</td>
        <td>6336</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>2.0</td>
        <td>Robin Thicke feat. T.I. and Pharrell</td>
        <td>Robin Thicke</td>
        <td>Blurred Lines</td>
        <td>6337</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>2.0</td>
        <td>Robin Thicke feat. T.I. and Pharrell</td>
        <td>T.I.</td>
        <td>Blurred Lines</td>
        <td>6338</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>2.0</td>
        <td>Robin Thicke feat. T.I. and Pharrell</td>
        <td>Pharrell</td>
        <td>Blurred Lines</td>
        <td>6339</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>3.0</td>
        <td>Imagine Dragons</td>
        <td>Imagine Dragons</td>
        <td>Radioactive</td>
        <td>6340</td>
    </tr>
</table>




```sql
%%sql
SELECT * FROM bill_board
WHERE year = 2013 AND "group" NOT ILIKE '%Robin%'
```

     * postgresql://postgres:***@localhost/portfolio
    140 rows affected.





<table>
    <tr>
        <th>year</th>
        <th>year_rank</th>
        <th>group</th>
        <th>artist</th>
        <th>song_name</th>
        <th>id</th>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>1.0</td>
        <td>Macklemore and Ryan Lewis feat. Wanz</td>
        <td>Macklemore</td>
        <td>Thrift Shop</td>
        <td>6334</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>1.0</td>
        <td>Macklemore and Ryan Lewis feat. Wanz</td>
        <td>Ryan Lewis</td>
        <td>Thrift Shop</td>
        <td>6335</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>1.0</td>
        <td>Macklemore and Ryan Lewis feat. Wanz</td>
        <td>Wanz</td>
        <td>Thrift Shop</td>
        <td>6336</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>3.0</td>
        <td>Imagine Dragons</td>
        <td>Imagine Dragons</td>
        <td>Radioactive</td>
        <td>6340</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>4.0</td>
        <td>Baauer</td>
        <td>Baauer</td>
        <td>Harlem Shake</td>
        <td>6341</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>5.0</td>
        <td>Macklemore and Ryan Lewis feat. Ray Dalton</td>
        <td>Macklemore</td>
        <td>Can&#x27;t Hold Us</td>
        <td>6342</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>5.0</td>
        <td>Macklemore and Ryan Lewis feat. Ray Dalton</td>
        <td>Ryan Lewis</td>
        <td>Can&#x27;t Hold Us</td>
        <td>6343</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>5.0</td>
        <td>Macklemore and Ryan Lewis feat. Ray Dalton</td>
        <td>Ray Dalton</td>
        <td>Can&#x27;t Hold Us</td>
        <td>6344</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>6.0</td>
        <td>Justin Timberlake</td>
        <td>Justin Timberlake</td>
        <td>Mirrors</td>
        <td>6345</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>7.0</td>
        <td>P!nk feat. Nate Ruess</td>
        <td>P!nk</td>
        <td>Just Give Me A Reason</td>
        <td>6346</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>7.0</td>
        <td>P!nk feat. Nate Ruess</td>
        <td>Nate Ruess</td>
        <td>Just Give Me A Reason</td>
        <td>6347</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>8.0</td>
        <td>Bruno Mars</td>
        <td>Bruno Mars</td>
        <td>When I Was Your Man</td>
        <td>6348</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>9.0</td>
        <td>Florida Georgia Line feat. Nelly</td>
        <td>Florida Georgia Line</td>
        <td>Cruise</td>
        <td>6349</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>9.0</td>
        <td>Florida Georgia Line feat. Nelly</td>
        <td>Nelly</td>
        <td>Cruise</td>
        <td>6350</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>10.0</td>
        <td>Katy Perry</td>
        <td>Katy Perry</td>
        <td>Roar</td>
        <td>6351</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>11.0</td>
        <td>Bruno Mars</td>
        <td>Bruno Mars</td>
        <td>Locked Out Of Heaven</td>
        <td>6352</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>12.0</td>
        <td>Lumineers</td>
        <td>Lumineers</td>
        <td>Ho Hey</td>
        <td>6353</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>13.0</td>
        <td>Rihanna feat. Mikky Ekko</td>
        <td>Rihanna</td>
        <td>Stay</td>
        <td>6354</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>13.0</td>
        <td>Rihanna feat. Mikky Ekko</td>
        <td>Mikky Ekko</td>
        <td>Stay</td>
        <td>6355</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>14.0</td>
        <td>Daft Punk feat. Pharrell Williams</td>
        <td>Daft Punk</td>
        <td>Get Lucky</td>
        <td>6356</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>14.0</td>
        <td>Daft Punk feat. Pharrell Williams</td>
        <td>Pharrell Williams</td>
        <td>Get Lucky</td>
        <td>6357</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>15.0</td>
        <td>Lorde</td>
        <td>Lorde</td>
        <td>Royals</td>
        <td>6358</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>16.0</td>
        <td>Taylor Swift</td>
        <td>Taylor Swift</td>
        <td>I Knew You Were Trouble</td>
        <td>6359</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>17.0</td>
        <td>Miley Cyrus</td>
        <td>Miley Cyrus</td>
        <td>We Can&#x27;t Stop</td>
        <td>6360</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>18.0</td>
        <td>Miley Cyrus</td>
        <td>Miley Cyrus</td>
        <td>Wrecking Ball</td>
        <td>6361</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>19.0</td>
        <td>Avicii</td>
        <td>Avicii</td>
        <td>Wake Me Up!</td>
        <td>6362</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>20.0</td>
        <td>Justin Timberlake feat. Jay Z</td>
        <td>Justin Timberlake</td>
        <td>Suit and Tie</td>
        <td>6363</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>20.0</td>
        <td>Justin Timberlake feat. Jay Z</td>
        <td>Jay Z</td>
        <td>Suit and Tie</td>
        <td>6364</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>21.0</td>
        <td>Anna Kendrick</td>
        <td>Anna Kendrick</td>
        <td>Cups (Pitch Perfect&#x27;s When I&#x27;m Gone)</td>
        <td>6365</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>22.0</td>
        <td>Jay Z feat. Justin Timberlake</td>
        <td>Jay Z</td>
        <td>Holy Grail</td>
        <td>6366</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>22.0</td>
        <td>Jay Z feat. Justin Timberlake</td>
        <td>Justin Timberlake</td>
        <td>Holy Grail</td>
        <td>6367</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>23.0</td>
        <td>will.i.am and Britney Spears</td>
        <td>will.i.am</td>
        <td>Scream and Shout</td>
        <td>6368</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>23.0</td>
        <td>will.i.am and Britney Spears</td>
        <td>Britney Spears</td>
        <td>Scream and Shout</td>
        <td>6369</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>24.0</td>
        <td>Zedd feat. Foxes</td>
        <td>Zedd</td>
        <td>Clarity</td>
        <td>6370</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>24.0</td>
        <td>Zedd feat. Foxes</td>
        <td>Foxes</td>
        <td>Clarity</td>
        <td>6371</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>25.0</td>
        <td>AWOLNATION</td>
        <td>AWOLNATION</td>
        <td>Sail</td>
        <td>6372</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>26.0</td>
        <td>Swedish House Mafia feat. John Martin</td>
        <td>Swedish House Mafia</td>
        <td>Don&#x27;t You Worry Child</td>
        <td>6373</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>26.0</td>
        <td>Swedish House Mafia feat. John Martin</td>
        <td>John Martin</td>
        <td>Don&#x27;t You Worry Child</td>
        <td>6374</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>27.0</td>
        <td>Rihanna</td>
        <td>Rihanna</td>
        <td>Diamonds</td>
        <td>6375</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>28.0</td>
        <td>Icona Pop feat. Charli XCX</td>
        <td>Icona Pop</td>
        <td>I Love It</td>
        <td>6376</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>28.0</td>
        <td>Icona Pop feat. Charli XCX</td>
        <td>Charli XCX</td>
        <td>I Love It</td>
        <td>6377</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>29.0</td>
        <td>Capital Cities</td>
        <td>Capital Cities</td>
        <td>Safe And Sound</td>
        <td>6378</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>30.0</td>
        <td>Bruno Mars</td>
        <td>Bruno Mars</td>
        <td>Treasure</td>
        <td>6379</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>31.0</td>
        <td>Ariana Grande feat. Mac Miller</td>
        <td>Ariana Grande</td>
        <td>The Way</td>
        <td>6380</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>31.0</td>
        <td>Ariana Grande feat. Mac Miller</td>
        <td>Mac Miller</td>
        <td>The Way</td>
        <td>6381</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>32.0</td>
        <td>Drake</td>
        <td>Drake</td>
        <td>Started From The Bottom</td>
        <td>6382</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>33.0</td>
        <td>Selena Gomez</td>
        <td>Selena Gomez</td>
        <td>Come and Get It</td>
        <td>6383</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>34.0</td>
        <td>Drake feat. Majid Jordan</td>
        <td>Drake</td>
        <td>Hold On, We&#x27;re Going Home</td>
        <td>6384</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>34.0</td>
        <td>Drake feat. Majid Jordan</td>
        <td>Majid Jordan</td>
        <td>Hold On, We&#x27;re Going Home</td>
        <td>6385</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>35.0</td>
        <td>Maroon 5</td>
        <td>Maroon 5</td>
        <td>Daylight</td>
        <td>6386</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>36.0</td>
        <td>Pitbull feat. Christina Aguilera</td>
        <td>Pitbull</td>
        <td>Feel This Moment</td>
        <td>6387</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>36.0</td>
        <td>Pitbull feat. Christina Aguilera</td>
        <td>Christina Aguilera</td>
        <td>Feel This Moment</td>
        <td>6388</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>37.0</td>
        <td>Lady Gaga</td>
        <td>Lady Gaga</td>
        <td>Applause</td>
        <td>6389</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>38.0</td>
        <td>Maroon 5</td>
        <td>Maroon 5</td>
        <td>One More Night</td>
        <td>6390</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>39.0</td>
        <td>Lil Wayne feat. Drake and Future</td>
        <td>Lil Wayne</td>
        <td>Love Me</td>
        <td>6391</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>39.0</td>
        <td>Lil Wayne feat. Drake and Future</td>
        <td>Drake</td>
        <td>Love Me</td>
        <td>6392</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>39.0</td>
        <td>Lil Wayne feat. Drake and Future</td>
        <td>Future</td>
        <td>Love Me</td>
        <td>6393</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>40.0</td>
        <td>Fall Out Boy</td>
        <td>Fall Out Boy</td>
        <td>My Songs Know What You Did In The Dark (Light Em Up)</td>
        <td>6394</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>41.0</td>
        <td>A$AP Rocky feat. Drake, 2 Chainz and Kendrick Lamar</td>
        <td>A$AP Rocky</td>
        <td>F**kin Problems</td>
        <td>6395</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>41.0</td>
        <td>A$AP Rocky feat. Drake, 2 Chainz and Kendrick Lamar</td>
        <td>Drake</td>
        <td>F**kin Problems</td>
        <td>6396</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>41.0</td>
        <td>A$AP Rocky feat. Drake, 2 Chainz and Kendrick Lamar</td>
        <td>2 Chainz</td>
        <td>F**kin Problems</td>
        <td>6397</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>41.0</td>
        <td>A$AP Rocky feat. Drake, 2 Chainz and Kendrick Lamar</td>
        <td>Kendrick Lamar</td>
        <td>F**kin Problems</td>
        <td>6398</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>42.0</td>
        <td>Justin Bieber feat. Nicki Minaj</td>
        <td>Justin Bieber</td>
        <td>Beauty And A Beat</td>
        <td>6399</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>42.0</td>
        <td>Justin Bieber feat. Nicki Minaj</td>
        <td>Nicki Minaj</td>
        <td>Beauty And A Beat</td>
        <td>6400</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>43.0</td>
        <td>Macklemore and Ryan Lewis feat. Mary Lambert</td>
        <td>Macklemore</td>
        <td>Same Love</td>
        <td>6401</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>43.0</td>
        <td>Macklemore and Ryan Lewis feat. Mary Lambert</td>
        <td>Ryan Lewis</td>
        <td>Same Love</td>
        <td>6402</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>43.0</td>
        <td>Macklemore and Ryan Lewis feat. Mary Lambert</td>
        <td>Mary Lambert</td>
        <td>Same Love</td>
        <td>6403</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>44.0</td>
        <td>Calvin Harris feat. Florence Welch</td>
        <td>Calvin Harris</td>
        <td>Sweet Nothing</td>
        <td>6404</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>44.0</td>
        <td>Calvin Harris feat. Florence Welch</td>
        <td>Florence Welch</td>
        <td>Sweet Nothing</td>
        <td>6405</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>45.0</td>
        <td>Lana Del Rey and Cedric Gervais</td>
        <td>Lana Del Rey</td>
        <td>Summertime Sadness</td>
        <td>6406</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>45.0</td>
        <td>Lana Del Rey and Cedric Gervais</td>
        <td>Cedric Gervais</td>
        <td>Summertime Sadness</td>
        <td>6407</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>46.0</td>
        <td>Phillip Phillips</td>
        <td>Phillip Phillips</td>
        <td>Home</td>
        <td>6408</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>47.0</td>
        <td>Imagine Dragons</td>
        <td>Imagine Dragons</td>
        <td>It&#x27;s Time</td>
        <td>6409</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>48.0</td>
        <td>J. Cole feat. Miguel</td>
        <td>J. Cole</td>
        <td>Power Trip</td>
        <td>6410</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>48.0</td>
        <td>J. Cole feat. Miguel</td>
        <td>Miguel</td>
        <td>Power Trip</td>
        <td>6411</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>49.0</td>
        <td>Alicia Keys feat. Nicki Minaj</td>
        <td>Alicia Keys</td>
        <td>Girl On Fire</td>
        <td>6412</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>49.0</td>
        <td>Alicia Keys feat. Nicki Minaj</td>
        <td>Nicki Minaj</td>
        <td>Girl On Fire</td>
        <td>6413</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>50.0</td>
        <td>Demi Lovato</td>
        <td>Demi Lovato</td>
        <td>Heart Attack</td>
        <td>6414</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>51.0</td>
        <td>Maroon 5</td>
        <td>Maroon 5</td>
        <td>Love Somebody</td>
        <td>6415</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>52.0</td>
        <td>Mumford and Sons</td>
        <td>Mumford and Sons</td>
        <td>I Will Wait</td>
        <td>6416</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>53.0</td>
        <td>P!nk</td>
        <td>P!nk</td>
        <td>Try</td>
        <td>6417</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>54.0</td>
        <td>Darius Rucker</td>
        <td>Darius Rucker</td>
        <td>Wagon Wheel</td>
        <td>6418</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>55.0</td>
        <td>Psy</td>
        <td>Psy</td>
        <td>Gangnam Style</td>
        <td>6419</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>56.0</td>
        <td>Calvin Harris feat. Ellie Goulding</td>
        <td>Calvin Harris</td>
        <td>I Need Your Love</td>
        <td>6420</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>56.0</td>
        <td>Calvin Harris feat. Ellie Goulding</td>
        <td>Ellie Goulding</td>
        <td>I Need Your Love</td>
        <td>6421</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>57.0</td>
        <td>Ke$ha</td>
        <td>Ke$ha</td>
        <td>Die Young</td>
        <td>6422</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>58.0</td>
        <td>fun.</td>
        <td>fun.</td>
        <td>Some Nights</td>
        <td>6423</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>59.0</td>
        <td>Wale feat. Tiara Thomas or Rihanna</td>
        <td>Wale</td>
        <td>Bad</td>
        <td>6424</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>59.0</td>
        <td>Wale feat. Tiara Thomas or Rihanna</td>
        <td>Tiara Thomas</td>
        <td>Bad</td>
        <td>6425</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>59.0</td>
        <td>Wale feat. Tiara Thomas or Rihanna</td>
        <td>Rihanna</td>
        <td>Bad</td>
        <td>6426</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>60.0</td>
        <td>Blake Shelton feat. Pistol Annies and Friends</td>
        <td>Blake Shelton</td>
        <td>Boys &#x27;Round Here</td>
        <td>6427</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>60.0</td>
        <td>Blake Shelton feat. Pistol Annies and Friends</td>
        <td>Piston Annies</td>
        <td>Boys &#x27;Round Here</td>
        <td>6428</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>61.0</td>
        <td>Phillip Phillips</td>
        <td>Phillip Phillips</td>
        <td>Gone, Gone, Gone</td>
        <td>6429</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>62.0</td>
        <td>Imagine Dragons</td>
        <td>Imagine Dragons</td>
        <td>Demons</td>
        <td>6430</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>63.0</td>
        <td>OneRepublic</td>
        <td>OneRepublic</td>
        <td>Counting Stars</td>
        <td>6431</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>64.0</td>
        <td>Flo Rida</td>
        <td>Flo Rida</td>
        <td>I Cry</td>
        <td>6432</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>65.0</td>
        <td>Of Monsters And Men</td>
        <td>Of Monsters And Men</td>
        <td>Little Talks</td>
        <td>6433</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>66.0</td>
        <td>Jason Derulo</td>
        <td>Jason Derulo</td>
        <td>The Other Side</td>
        <td>6434</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>67.0</td>
        <td>Eminem</td>
        <td>Eminem</td>
        <td>Berzerk</td>
        <td>6435</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>68.0</td>
        <td>Kelly Clarkson</td>
        <td>Kelly Clarkson</td>
        <td>Catch My Breath</td>
        <td>6436</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>69.0</td>
        <td>Luke Bryan</td>
        <td>Luke Bryan</td>
        <td>Crash My Party</td>
        <td>6437</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>70.0</td>
        <td>Rihanna</td>
        <td>Rihanna</td>
        <td>Pour It Up</td>
        <td>6438</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>71.0</td>
        <td>Taylor Swift</td>
        <td>Taylor Swift</td>
        <td>22</td>
        <td>6439</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>72.0</td>
        <td>Hunter Hayes</td>
        <td>Hunter Hayes</td>
        <td>I Want Crazy</td>
        <td>6440</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>73.0</td>
        <td>Ylvis</td>
        <td>Ylvis</td>
        <td>The Fox</td>
        <td>6441</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>74.0</td>
        <td>One Direction</td>
        <td>One Direction</td>
        <td>Best Song Ever</td>
        <td>6442</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>75.0</td>
        <td>Ed Sheeran</td>
        <td>Ed Sheeran</td>
        <td>The A Team</td>
        <td>6443</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>76.0</td>
        <td>fun.</td>
        <td>fun.</td>
        <td>Carry On</td>
        <td>6444</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>77.0</td>
        <td>Tim McGraw with Taylor Swift</td>
        <td>Tim McGraw with Taylor Swift</td>
        <td>Highway Don&#x27;t Care</td>
        <td>6445</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>78.0</td>
        <td>Luke Bryan</td>
        <td>Luke Bryan</td>
        <td>That&#x27;s My Kind Of Night</td>
        <td>6446</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>79.0</td>
        <td>Kendrick Lamar</td>
        <td>Kendrick Lamar</td>
        <td>Swimming Pools (Drank)</td>
        <td>6447</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>80.0</td>
        <td>Blake Shelton</td>
        <td>Blake Shelton</td>
        <td>Sure Be Cool If You Did</td>
        <td>6448</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>81.0</td>
        <td>Mariah Carey feat. Miguel</td>
        <td>Mariah Carey</td>
        <td>#Beautiful</td>
        <td>6449</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>81.0</td>
        <td>Mariah Carey feat. Miguel</td>
        <td>Miguel</td>
        <td>#Beautiful</td>
        <td>6450</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>82.0</td>
        <td>Olly Murs feat. Flo Rida</td>
        <td>Olly Murs</td>
        <td>Troublemaker</td>
        <td>6451</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>82.0</td>
        <td>Olly Murs feat. Flo Rida</td>
        <td>Flo Rida</td>
        <td>Troublemaker</td>
        <td>6452</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>83.0</td>
        <td>Ciara</td>
        <td>Ciara</td>
        <td>Body Party</td>
        <td>6453</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>84.0</td>
        <td>Miguel</td>
        <td>Miguel</td>
        <td>Adorn</td>
        <td>6454</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>85.0</td>
        <td>The Script feat. will.i.am</td>
        <td>The Script</td>
        <td>Hall Of Fame</td>
        <td>6455</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>85.0</td>
        <td>The Script feat. will.i.am</td>
        <td>will.i.am</td>
        <td>Hall Of Fame</td>
        <td>6456</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>86.0</td>
        <td>Ne-Yo</td>
        <td>Ne-Yo</td>
        <td>Let Me Love You (Until You Learn To Love Yourself)</td>
        <td>6457</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>87.0</td>
        <td>Rocko feat. Future and Rick Ross</td>
        <td>Rocko</td>
        <td>U.O.E.N.O.</td>
        <td>6458</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>87.0</td>
        <td>Rocko feat. Future and Rick Ross</td>
        <td>Future</td>
        <td>U.O.E.N.O.</td>
        <td>6459</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>87.0</td>
        <td>Rocko feat. Future and Rick Ross</td>
        <td>Rick Ross</td>
        <td>U.O.E.N.O.</td>
        <td>6460</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>88.0</td>
        <td>Emeli Sande</td>
        <td>Emeli Sande</td>
        <td>Next To Me</td>
        <td>6461</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>89.0</td>
        <td>Miranda Lambert</td>
        <td>Miranda Lambert</td>
        <td>Mama&#x27;s Broken Heart</td>
        <td>6462</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>90.0</td>
        <td>Thomas Rhett</td>
        <td>Thomas Rhett</td>
        <td>It Goes Like This</td>
        <td>6463</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>91.0</td>
        <td>Ace Hood feat. Future and Rick Ross</td>
        <td>Ace Hood</td>
        <td>Bugatti</td>
        <td>6464</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>91.0</td>
        <td>Ace Hood feat. Future and Rick Ross</td>
        <td>Future</td>
        <td>Bugatti</td>
        <td>6465</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>91.0</td>
        <td>Ace Hood feat. Future and Rick Ross</td>
        <td>Rick Ross</td>
        <td>Bugatti</td>
        <td>6466</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>92.0</td>
        <td>Hunter Hayes</td>
        <td>Hunter Hayes</td>
        <td>Wanted</td>
        <td>6467</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>93.0</td>
        <td>Lady Antebellum</td>
        <td>Lady Antebellum</td>
        <td>Downtown</td>
        <td>6468</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>94.0</td>
        <td>Florida Georgia Line</td>
        <td>Florida Georgia Line</td>
        <td>Get Your Shine On</td>
        <td>6469</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>95.0</td>
        <td>will.i.am feat. Justin Bieber</td>
        <td>will.i.am</td>
        <td>#thatPOWER</td>
        <td>6470</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>95.0</td>
        <td>will.i.am feat. Justin Bieber</td>
        <td>Justin Bieber</td>
        <td>#thatPOWER</td>
        <td>6471</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>96.0</td>
        <td>Sara Bareilles</td>
        <td>Sara Bareilles</td>
        <td>Brave</td>
        <td>6472</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>97.0</td>
        <td>Passenger</td>
        <td>Passenger</td>
        <td>Let Her Go</td>
        <td>6473</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>98.0</td>
        <td>Randy Houser</td>
        <td>Randy Houser</td>
        <td>Runnin&#x27; Outta Moonlight</td>
        <td>6474</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>99.0</td>
        <td>2 Chainz</td>
        <td>2 Chainz</td>
        <td>I&#x27;m Different</td>
        <td>6475</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>100.0</td>
        <td>Paramore</td>
        <td>Paramore</td>
        <td>Still Into You</td>
        <td>6476</td>
    </tr>
</table>




```sql
%%sql
SELECT * FROM bill_board
WHERE year = 2013 AND artist IS NOT NULL
LIMIT 10
```

     * postgresql://postgres:***@localhost/portfolio
    10 rows affected.





<table>
    <tr>
        <th>year</th>
        <th>year_rank</th>
        <th>group</th>
        <th>artist</th>
        <th>song_name</th>
        <th>id</th>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>1.0</td>
        <td>Macklemore and Ryan Lewis feat. Wanz</td>
        <td>Macklemore</td>
        <td>Thrift Shop</td>
        <td>6334</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>1.0</td>
        <td>Macklemore and Ryan Lewis feat. Wanz</td>
        <td>Ryan Lewis</td>
        <td>Thrift Shop</td>
        <td>6335</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>1.0</td>
        <td>Macklemore and Ryan Lewis feat. Wanz</td>
        <td>Wanz</td>
        <td>Thrift Shop</td>
        <td>6336</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>2.0</td>
        <td>Robin Thicke feat. T.I. and Pharrell</td>
        <td>Robin Thicke</td>
        <td>Blurred Lines</td>
        <td>6337</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>2.0</td>
        <td>Robin Thicke feat. T.I. and Pharrell</td>
        <td>T.I.</td>
        <td>Blurred Lines</td>
        <td>6338</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>2.0</td>
        <td>Robin Thicke feat. T.I. and Pharrell</td>
        <td>Pharrell</td>
        <td>Blurred Lines</td>
        <td>6339</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>3.0</td>
        <td>Imagine Dragons</td>
        <td>Imagine Dragons</td>
        <td>Radioactive</td>
        <td>6340</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>4.0</td>
        <td>Baauer</td>
        <td>Baauer</td>
        <td>Harlem Shake</td>
        <td>6341</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>5.0</td>
        <td>Macklemore and Ryan Lewis feat. Ray Dalton</td>
        <td>Macklemore</td>
        <td>Can&#x27;t Hold Us</td>
        <td>6342</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>5.0</td>
        <td>Macklemore and Ryan Lewis feat. Ray Dalton</td>
        <td>Ryan Lewis</td>
        <td>Can&#x27;t Hold Us</td>
        <td>6343</td>
    </tr>
</table>



### SQL ORDER BY
ORDER BY clause enables reordering results based on data from other columns.


```sql
%%sql
SELECT * FROM bill_board
ORDER BY artist
LIMIT 10
```

     * postgresql://postgres:***@localhost/portfolio
    10 rows affected.





<table>
    <tr>
        <th>year</th>
        <th>year_rank</th>
        <th>group</th>
        <th>artist</th>
        <th>song_name</th>
        <th>id</th>
    </tr>
    <tr>
        <td>2002.0</td>
        <td>75.0</td>
        <td>&#x27;N Sync</td>
        <td>&#x27;N Sync</td>
        <td>Gone</td>
        <td>4910</td>
    </tr>
    <tr>
        <td>2000.0</td>
        <td>21.0</td>
        <td>&#x27;N Sync</td>
        <td>&#x27;N Sync</td>
        <td>Bye Bye Bye</td>
        <td>4585</td>
    </tr>
    <tr>
        <td>2001.0</td>
        <td>51.0</td>
        <td>&#x27;N Sync</td>
        <td>&#x27;N Sync</td>
        <td>This I Promise You</td>
        <td>4741</td>
    </tr>
    <tr>
        <td>2002.0</td>
        <td>33.0</td>
        <td>&#x27;N Sync feat. Nelly</td>
        <td>&#x27;N Sync</td>
        <td>Girlfriend</td>
        <td>4849</td>
    </tr>
    <tr>
        <td>1999.0</td>
        <td>97.0</td>
        <td>&#x27;N Sync and Gloria Estefan</td>
        <td>&#x27;N Sync</td>
        <td>Music Of My Heart</td>
        <td>4556</td>
    </tr>
    <tr>
        <td>1999.0</td>
        <td>45.0</td>
        <td>&#x27;N Sync</td>
        <td>&#x27;N Sync</td>
        <td>(God Must Have Spent) A Little More Time On You</td>
        <td>4491</td>
    </tr>
    <tr>
        <td>1998.0</td>
        <td>37.0</td>
        <td>&#x27;N Sync</td>
        <td>&#x27;N Sync</td>
        <td>I Want You Back</td>
        <td>4366</td>
    </tr>
    <tr>
        <td>2000.0</td>
        <td>27.0</td>
        <td>&#x27;N Sync</td>
        <td>&#x27;N Sync</td>
        <td>It&#x27;s Gonna Be Me</td>
        <td>4591</td>
    </tr>
    <tr>
        <td>1999.0</td>
        <td>100.0</td>
        <td>Alabama feat. &#x27;N Sync</td>
        <td>&#x27;N Sync</td>
        <td>God Must Have Spent A Little More Time On You</td>
        <td>4562</td>
    </tr>
    <tr>
        <td>1985.0</td>
        <td>68.0</td>
        <td>&#x27;Til Tuesday</td>
        <td>&#x27;Til Tuesday</td>
        <td>Voices Carry</td>
        <td>3047</td>
    </tr>
</table>




```sql
%%sql
SELECT * FROM bill_board
WHERE year = 2013
ORDER BY year_rank DESC
LIMIT 10
```

     * postgresql://postgres:***@localhost/portfolio
    10 rows affected.





<table>
    <tr>
        <th>year</th>
        <th>year_rank</th>
        <th>group</th>
        <th>artist</th>
        <th>song_name</th>
        <th>id</th>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>100.0</td>
        <td>Paramore</td>
        <td>Paramore</td>
        <td>Still Into You</td>
        <td>6476</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>99.0</td>
        <td>2 Chainz</td>
        <td>2 Chainz</td>
        <td>I&#x27;m Different</td>
        <td>6475</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>98.0</td>
        <td>Randy Houser</td>
        <td>Randy Houser</td>
        <td>Runnin&#x27; Outta Moonlight</td>
        <td>6474</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>97.0</td>
        <td>Passenger</td>
        <td>Passenger</td>
        <td>Let Her Go</td>
        <td>6473</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>96.0</td>
        <td>Sara Bareilles</td>
        <td>Sara Bareilles</td>
        <td>Brave</td>
        <td>6472</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>95.0</td>
        <td>will.i.am feat. Justin Bieber</td>
        <td>will.i.am</td>
        <td>#thatPOWER</td>
        <td>6470</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>95.0</td>
        <td>will.i.am feat. Justin Bieber</td>
        <td>Justin Bieber</td>
        <td>#thatPOWER</td>
        <td>6471</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>94.0</td>
        <td>Florida Georgia Line</td>
        <td>Florida Georgia Line</td>
        <td>Get Your Shine On</td>
        <td>6469</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>93.0</td>
        <td>Lady Antebellum</td>
        <td>Lady Antebellum</td>
        <td>Downtown</td>
        <td>6468</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>92.0</td>
        <td>Hunter Hayes</td>
        <td>Hunter Hayes</td>
        <td>Wanted</td>
        <td>6467</td>
    </tr>
</table>



#### A query that returns all rows from 2012, ordered by song title from Z to A.




```sql
%%sql
SELECT * FROM bill_board
WHERE year >= 2012
ORDER BY song_name DESC
LIMIT 10

```

     * postgresql://postgres:***@localhost/portfolio
    10 rows affected.





<table>
    <tr>
        <th>year</th>
        <th>year_rank</th>
        <th>group</th>
        <th>artist</th>
        <th>song_name</th>
        <th>id</th>
    </tr>
    <tr>
        <td>2012.0</td>
        <td>32.0</td>
        <td>Snoop Dogg and Wiz Khalifa feat. Bruno Mars</td>
        <td>Bruno Mars</td>
        <td>Young, Wild and Free</td>
        <td>6249</td>
    </tr>
    <tr>
        <td>2012.0</td>
        <td>32.0</td>
        <td>Snoop Dogg and Wiz Khalifa feat. Bruno Mars</td>
        <td>Wiz Khalifa</td>
        <td>Young, Wild and Free</td>
        <td>6248</td>
    </tr>
    <tr>
        <td>2012.0</td>
        <td>32.0</td>
        <td>Snoop Dogg and Wiz Khalifa feat. Bruno Mars</td>
        <td>Snoop Dogg</td>
        <td>Young, Wild and Free</td>
        <td>6247</td>
    </tr>
    <tr>
        <td>2012.0</td>
        <td>89.0</td>
        <td>Rihanna</td>
        <td>Rihanna</td>
        <td>You Da One</td>
        <td>6321</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>18.0</td>
        <td>Miley Cyrus</td>
        <td>Miley Cyrus</td>
        <td>Wrecking Ball</td>
        <td>6361</td>
    </tr>
    <tr>
        <td>2012.0</td>
        <td>63.0</td>
        <td>J. Cole</td>
        <td>J. Cole</td>
        <td>Work Out</td>
        <td>6291</td>
    </tr>
    <tr>
        <td>2012.0</td>
        <td>73.0</td>
        <td>Wiz Khalifa</td>
        <td>Wiz Khalifa</td>
        <td>Work Hard, Play Hard</td>
        <td>6302</td>
    </tr>
    <tr>
        <td>2012.0</td>
        <td>50.0</td>
        <td>David Guetta feat. Usher</td>
        <td>David Guetta</td>
        <td>Without You</td>
        <td>6273</td>
    </tr>
    <tr>
        <td>2012.0</td>
        <td>50.0</td>
        <td>David Guetta feat. Usher</td>
        <td>Usher</td>
        <td>Without You</td>
        <td>6274</td>
    </tr>
    <tr>
        <td>2012.0</td>
        <td>11.0</td>
        <td>Flo Rida feat. Sia</td>
        <td>Sia</td>
        <td>Wild Ones</td>
        <td>6218</td>
    </tr>
</table>



### Ordering data by multiple columns


```sql
%%sql
SELECT * FROM bill_board
WHERE year_rank <= 3
ORDER BY year DESC, year_rank
LIMIT 10
```

     * postgresql://postgres:***@localhost/portfolio
    10 rows affected.





<table>
    <tr>
        <th>year</th>
        <th>year_rank</th>
        <th>group</th>
        <th>artist</th>
        <th>song_name</th>
        <th>id</th>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>1.0</td>
        <td>Macklemore and Ryan Lewis feat. Wanz</td>
        <td>Wanz</td>
        <td>Thrift Shop</td>
        <td>6336</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>1.0</td>
        <td>Macklemore and Ryan Lewis feat. Wanz</td>
        <td>Ryan Lewis</td>
        <td>Thrift Shop</td>
        <td>6335</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>1.0</td>
        <td>Macklemore and Ryan Lewis feat. Wanz</td>
        <td>Macklemore</td>
        <td>Thrift Shop</td>
        <td>6334</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>2.0</td>
        <td>Robin Thicke feat. T.I. and Pharrell</td>
        <td>T.I.</td>
        <td>Blurred Lines</td>
        <td>6338</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>2.0</td>
        <td>Robin Thicke feat. T.I. and Pharrell</td>
        <td>Pharrell</td>
        <td>Blurred Lines</td>
        <td>6339</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>2.0</td>
        <td>Robin Thicke feat. T.I. and Pharrell</td>
        <td>Robin Thicke</td>
        <td>Blurred Lines</td>
        <td>6337</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>3.0</td>
        <td>Imagine Dragons</td>
        <td>Imagine Dragons</td>
        <td>Radioactive</td>
        <td>6340</td>
    </tr>
    <tr>
        <td>2012.0</td>
        <td>1.0</td>
        <td>Gotye feat. Kimbra</td>
        <td>Gotye</td>
        <td>Somebody That I Used To Know</td>
        <td>6203</td>
    </tr>
    <tr>
        <td>2012.0</td>
        <td>1.0</td>
        <td>Gotye feat. Kimbra</td>
        <td>Kimbra</td>
        <td>Somebody That I Used To Know</td>
        <td>6204</td>
    </tr>
    <tr>
        <td>2012.0</td>
        <td>2.0</td>
        <td>Carly Rae Jepsen</td>
        <td>Carly Rae Jepsen</td>
        <td>Call Me Maybe</td>
        <td>6205</td>
    </tr>
</table>



The above query makes the most recent years come first but orders top-ranks songs before lower-ranked songs:


```sql
%%sql
SELECT * FROM bill_board
WHERE year_rank <= 3
ORDER BY year_rank, year DESC
LIMIT 10
```

     * postgresql://postgres:***@localhost/portfolio
    10 rows affected.





<table>
    <tr>
        <th>year</th>
        <th>year_rank</th>
        <th>group</th>
        <th>artist</th>
        <th>song_name</th>
        <th>id</th>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>1.0</td>
        <td>Macklemore and Ryan Lewis feat. Wanz</td>
        <td>Macklemore</td>
        <td>Thrift Shop</td>
        <td>6334</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>1.0</td>
        <td>Macklemore and Ryan Lewis feat. Wanz</td>
        <td>Wanz</td>
        <td>Thrift Shop</td>
        <td>6336</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>1.0</td>
        <td>Macklemore and Ryan Lewis feat. Wanz</td>
        <td>Ryan Lewis</td>
        <td>Thrift Shop</td>
        <td>6335</td>
    </tr>
    <tr>
        <td>2012.0</td>
        <td>1.0</td>
        <td>Gotye feat. Kimbra</td>
        <td>Kimbra</td>
        <td>Somebody That I Used To Know</td>
        <td>6204</td>
    </tr>
    <tr>
        <td>2012.0</td>
        <td>1.0</td>
        <td>Gotye feat. Kimbra</td>
        <td>Gotye</td>
        <td>Somebody That I Used To Know</td>
        <td>6203</td>
    </tr>
    <tr>
        <td>2011.0</td>
        <td>1.0</td>
        <td>Adele</td>
        <td>Adele</td>
        <td>Rolling In The Deep</td>
        <td>6056</td>
    </tr>
    <tr>
        <td>2010.0</td>
        <td>1.0</td>
        <td>Ke$ha</td>
        <td>Ke$ha</td>
        <td>TiK ToK</td>
        <td>5909</td>
    </tr>
    <tr>
        <td>2009.0</td>
        <td>1.0</td>
        <td>The Black Eyed Peas</td>
        <td>The Black Eyed Peas</td>
        <td>Boom Boom Pow</td>
        <td>5779</td>
    </tr>
    <tr>
        <td>2008.0</td>
        <td>1.0</td>
        <td>Flo Rida feat. T-Pain</td>
        <td>T-Pain</td>
        <td>Low</td>
        <td>5639</td>
    </tr>
    <tr>
        <td>2008.0</td>
        <td>1.0</td>
        <td>Flo Rida feat. T-Pain</td>
        <td>Flo Rida</td>
        <td>Low</td>
        <td>5638</td>
    </tr>
</table>



### Substituting numbers for column names in the ORDER BY clause


```sql
%%sql
SELECT * FROM bill_board--(This wont affect the code)
WHERE year_rank <= 3
LIMIT 10
```

     * postgresql://postgres:***@localhost/portfolio
    10 rows affected.





<table>
    <tr>
        <th>year</th>
        <th>year_rank</th>
        <th>group</th>
        <th>artist</th>
        <th>song_name</th>
        <th>id</th>
    </tr>
    <tr>
        <td>1956.0</td>
        <td>1.0</td>
        <td>Elvis Presley</td>
        <td>Elvis Presley</td>
        <td>Heartbreak Hotel</td>
        <td>1</td>
    </tr>
    <tr>
        <td>1956.0</td>
        <td>2.0</td>
        <td>Elvis Presley</td>
        <td>Elvis Presley</td>
        <td>Don&#x27;t Be Cruel</td>
        <td>2</td>
    </tr>
    <tr>
        <td>1956.0</td>
        <td>3.0</td>
        <td>Nelson Riddle</td>
        <td>Nelson Riddle</td>
        <td>Lisbon Antigua</td>
        <td>3</td>
    </tr>
    <tr>
        <td>1957.0</td>
        <td>1.0</td>
        <td>Elvis Presley</td>
        <td>Elvis Presley</td>
        <td>All Shook Up</td>
        <td>104</td>
    </tr>
    <tr>
        <td>1957.0</td>
        <td>2.0</td>
        <td>Pat Boone</td>
        <td>Pat Boone</td>
        <td>Love Letters In The Sand</td>
        <td>105</td>
    </tr>
    <tr>
        <td>1957.0</td>
        <td>3.0</td>
        <td>Diamonds</td>
        <td>Diamonds</td>
        <td>Little Darlin&#x27;</td>
        <td>106</td>
    </tr>
    <tr>
        <td>1958.0</td>
        <td>1.0</td>
        <td>Domenico Modugno</td>
        <td>Domenico Modugno</td>
        <td>Volare (Nel Blu Dipinto Di Blu)</td>
        <td>204</td>
    </tr>
    <tr>
        <td>1958.0</td>
        <td>2.0</td>
        <td>Everly Brothers</td>
        <td>Everly Brothers</td>
        <td>All I Have To Do Is Dream / Claudette</td>
        <td>205</td>
    </tr>
    <tr>
        <td>1958.0</td>
        <td>3.0</td>
        <td>Elvis Presley</td>
        <td>Elvis Presley</td>
        <td>Don&#x27;t / I Beg Of You</td>
        <td>206</td>
    </tr>
    <tr>
        <td>1959.0</td>
        <td>1.0</td>
        <td>Johnny Horton</td>
        <td>Johnny Horton</td>
        <td>The Battle Of New Orleans</td>
        <td>305</td>
    </tr>
</table>




```sql
%%sql
SELECT *
  FROM bill_board
 WHERE year_rank <= 10
 ORDER BY 1, 2
LIMIT 10

```

     * postgresql://postgres:***@localhost/portfolio
    10 rows affected.





<table>
    <tr>
        <th>year</th>
        <th>year_rank</th>
        <th>group</th>
        <th>artist</th>
        <th>song_name</th>
        <th>id</th>
    </tr>
    <tr>
        <td>1956.0</td>
        <td>1.0</td>
        <td>Elvis Presley</td>
        <td>Elvis Presley</td>
        <td>Heartbreak Hotel</td>
        <td>1</td>
    </tr>
    <tr>
        <td>1956.0</td>
        <td>2.0</td>
        <td>Elvis Presley</td>
        <td>Elvis Presley</td>
        <td>Don&#x27;t Be Cruel</td>
        <td>2</td>
    </tr>
    <tr>
        <td>1956.0</td>
        <td>3.0</td>
        <td>Nelson Riddle</td>
        <td>Nelson Riddle</td>
        <td>Lisbon Antigua</td>
        <td>3</td>
    </tr>
    <tr>
        <td>1956.0</td>
        <td>4.0</td>
        <td>Platters</td>
        <td>Platters</td>
        <td>My Prayer</td>
        <td>4</td>
    </tr>
    <tr>
        <td>1956.0</td>
        <td>5.0</td>
        <td>Gogi Grant</td>
        <td>Gogi Grant</td>
        <td>The Wayward Wind</td>
        <td>5</td>
    </tr>
    <tr>
        <td>1956.0</td>
        <td>6.0</td>
        <td>Les Baxter</td>
        <td>Les Baxter</td>
        <td>The Poor People Of Paris</td>
        <td>6</td>
    </tr>
    <tr>
        <td>1956.0</td>
        <td>7.0</td>
        <td>Doris Day</td>
        <td>Doris Day</td>
        <td>Whatever Will Be Will Be (Que Sera Sera)</td>
        <td>7</td>
    </tr>
    <tr>
        <td>1956.0</td>
        <td>8.0</td>
        <td>Elvis Presley</td>
        <td>Elvis Presley</td>
        <td>Hound Dog</td>
        <td>8</td>
    </tr>
    <tr>
        <td>1956.0</td>
        <td>9.0</td>
        <td>Dean Martin</td>
        <td>Dean Martin</td>
        <td>Memories Are Made Of This</td>
        <td>9</td>
    </tr>
    <tr>
        <td>1956.0</td>
        <td>10.0</td>
        <td>Kay Starr</td>
        <td>Kay Starr</td>
        <td>Rock And Roll Waltz</td>
        <td>10</td>
    </tr>
</table>



#### A query that returns all rows from 2010 ordered by rank, with artists ordered alphabetically for each song.


```sql
%%sql
SELECT * FROM bill_board
WHERE year >= 2010
ORDER BY year_rank, "artist"
LIMIT 10

```

     * postgresql://postgres:***@localhost/portfolio
    10 rows affected.





<table>
    <tr>
        <th>year</th>
        <th>year_rank</th>
        <th>group</th>
        <th>artist</th>
        <th>song_name</th>
        <th>id</th>
    </tr>
    <tr>
        <td>2011.0</td>
        <td>1.0</td>
        <td>Adele</td>
        <td>Adele</td>
        <td>Rolling In The Deep</td>
        <td>6056</td>
    </tr>
    <tr>
        <td>2012.0</td>
        <td>1.0</td>
        <td>Gotye feat. Kimbra</td>
        <td>Gotye</td>
        <td>Somebody That I Used To Know</td>
        <td>6203</td>
    </tr>
    <tr>
        <td>2010.0</td>
        <td>1.0</td>
        <td>Ke$ha</td>
        <td>Ke$ha</td>
        <td>TiK ToK</td>
        <td>5909</td>
    </tr>
    <tr>
        <td>2012.0</td>
        <td>1.0</td>
        <td>Gotye feat. Kimbra</td>
        <td>Kimbra</td>
        <td>Somebody That I Used To Know</td>
        <td>6204</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>1.0</td>
        <td>Macklemore and Ryan Lewis feat. Wanz</td>
        <td>Macklemore</td>
        <td>Thrift Shop</td>
        <td>6334</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>1.0</td>
        <td>Macklemore and Ryan Lewis feat. Wanz</td>
        <td>Ryan Lewis</td>
        <td>Thrift Shop</td>
        <td>6335</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>1.0</td>
        <td>Macklemore and Ryan Lewis feat. Wanz</td>
        <td>Wanz</td>
        <td>Thrift Shop</td>
        <td>6336</td>
    </tr>
    <tr>
        <td>2012.0</td>
        <td>2.0</td>
        <td>Carly Rae Jepsen</td>
        <td>Carly Rae Jepsen</td>
        <td>Call Me Maybe</td>
        <td>6205</td>
    </tr>
    <tr>
        <td>2011.0</td>
        <td>2.0</td>
        <td>LMFAO feat. Lauren Bennett and GoonRock</td>
        <td>GoonRock</td>
        <td>Party Rock Anthem</td>
        <td>6059</td>
    </tr>
    <tr>
        <td>2011.0</td>
        <td>2.0</td>
        <td>LMFAO feat. Lauren Bennett and GoonRock</td>
        <td>LMFAO</td>
        <td>Party Rock Anthem</td>
        <td>6057</td>
    </tr>
</table>



### Using comments
One can use-- (two dashes) or /* (forward slash and asterisk)


```sql
%%sql
SELECT *  --This comment won't affect the way the code runs
  FROM bill_board
 WHERE year = 2013
LIMIT 10
```

     * postgresql://postgres:***@localhost/portfolio
    10 rows affected.





<table>
    <tr>
        <th>year</th>
        <th>year_rank</th>
        <th>group</th>
        <th>artist</th>
        <th>song_name</th>
        <th>id</th>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>1.0</td>
        <td>Macklemore and Ryan Lewis feat. Wanz</td>
        <td>Macklemore</td>
        <td>Thrift Shop</td>
        <td>6334</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>1.0</td>
        <td>Macklemore and Ryan Lewis feat. Wanz</td>
        <td>Ryan Lewis</td>
        <td>Thrift Shop</td>
        <td>6335</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>1.0</td>
        <td>Macklemore and Ryan Lewis feat. Wanz</td>
        <td>Wanz</td>
        <td>Thrift Shop</td>
        <td>6336</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>2.0</td>
        <td>Robin Thicke feat. T.I. and Pharrell</td>
        <td>Robin Thicke</td>
        <td>Blurred Lines</td>
        <td>6337</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>2.0</td>
        <td>Robin Thicke feat. T.I. and Pharrell</td>
        <td>T.I.</td>
        <td>Blurred Lines</td>
        <td>6338</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>2.0</td>
        <td>Robin Thicke feat. T.I. and Pharrell</td>
        <td>Pharrell</td>
        <td>Blurred Lines</td>
        <td>6339</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>3.0</td>
        <td>Imagine Dragons</td>
        <td>Imagine Dragons</td>
        <td>Radioactive</td>
        <td>6340</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>4.0</td>
        <td>Baauer</td>
        <td>Baauer</td>
        <td>Harlem Shake</td>
        <td>6341</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>5.0</td>
        <td>Macklemore and Ryan Lewis feat. Ray Dalton</td>
        <td>Macklemore</td>
        <td>Can&#x27;t Hold Us</td>
        <td>6342</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>5.0</td>
        <td>Macklemore and Ryan Lewis feat. Ray Dalton</td>
        <td>Ryan Lewis</td>
        <td>Can&#x27;t Hold Us</td>
        <td>6343</td>
    </tr>
</table>




```sql
%%sql
SELECT * FROM bill_board/* Here's a comment so long and descriptive that
it could only fit on multiple lines. Fortunately,
it, too, will not affect how this code runs. */
WHERE year = 2013
LIMIT 10
```

     * postgresql://postgres:***@localhost/portfolio
    10 rows affected.





<table>
    <tr>
        <th>year</th>
        <th>year_rank</th>
        <th>group</th>
        <th>artist</th>
        <th>song_name</th>
        <th>id</th>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>1.0</td>
        <td>Macklemore and Ryan Lewis feat. Wanz</td>
        <td>Macklemore</td>
        <td>Thrift Shop</td>
        <td>6334</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>1.0</td>
        <td>Macklemore and Ryan Lewis feat. Wanz</td>
        <td>Ryan Lewis</td>
        <td>Thrift Shop</td>
        <td>6335</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>1.0</td>
        <td>Macklemore and Ryan Lewis feat. Wanz</td>
        <td>Wanz</td>
        <td>Thrift Shop</td>
        <td>6336</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>2.0</td>
        <td>Robin Thicke feat. T.I. and Pharrell</td>
        <td>Robin Thicke</td>
        <td>Blurred Lines</td>
        <td>6337</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>2.0</td>
        <td>Robin Thicke feat. T.I. and Pharrell</td>
        <td>T.I.</td>
        <td>Blurred Lines</td>
        <td>6338</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>2.0</td>
        <td>Robin Thicke feat. T.I. and Pharrell</td>
        <td>Pharrell</td>
        <td>Blurred Lines</td>
        <td>6339</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>3.0</td>
        <td>Imagine Dragons</td>
        <td>Imagine Dragons</td>
        <td>Radioactive</td>
        <td>6340</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>4.0</td>
        <td>Baauer</td>
        <td>Baauer</td>
        <td>Harlem Shake</td>
        <td>6341</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>5.0</td>
        <td>Macklemore and Ryan Lewis feat. Ray Dalton</td>
        <td>Macklemore</td>
        <td>Can&#x27;t Hold Us</td>
        <td>6342</td>
    </tr>
    <tr>
        <td>2013.0</td>
        <td>5.0</td>
        <td>Macklemore and Ryan Lewis feat. Ray Dalton</td>
        <td>Ryan Lewis</td>
        <td>Can&#x27;t Hold Us</td>
        <td>6343</td>
    </tr>
</table>



#### A query that shows all rows for which T-Pain was a group member, ordered by rank on the charts, from lowest to highest rank (from 100 to 1).




```sql
%%sql
SELECT * FROM bill_board
WHERE "group" ILIKE '%T-Pain%'
ORDER BY year_rank DESC
LIMIT 10
```

     * postgresql://postgres:***@localhost/portfolio
    10 rows affected.





<table>
    <tr>
        <th>year</th>
        <th>year_rank</th>
        <th>group</th>
        <th>artist</th>
        <th>song_name</th>
        <th>id</th>
    </tr>
    <tr>
        <td>2008.0</td>
        <td>100.0</td>
        <td>2 Pistols feat. T-Pain and Tay Dizm</td>
        <td>T-Pain</td>
        <td>She Got It</td>
        <td>5777</td>
    </tr>
    <tr>
        <td>2008.0</td>
        <td>100.0</td>
        <td>2 Pistols feat. T-Pain and Tay Dizm</td>
        <td>Tay Dizm</td>
        <td>She Got It</td>
        <td>5778</td>
    </tr>
    <tr>
        <td>2008.0</td>
        <td>100.0</td>
        <td>2 Pistols feat. T-Pain and Tay Dizm</td>
        <td>2 Pistols</td>
        <td>She Got It</td>
        <td>5776</td>
    </tr>
    <tr>
        <td>2006.0</td>
        <td>98.0</td>
        <td>T-Pain</td>
        <td>T-Pain</td>
        <td>I&#x27;m Sprung</td>
        <td>5492</td>
    </tr>
    <tr>
        <td>2005.0</td>
        <td>95.0</td>
        <td>T-Pain</td>
        <td>T-Pain</td>
        <td>I&#x27;m Sprung</td>
        <td>5348</td>
    </tr>
    <tr>
        <td>2007.0</td>
        <td>93.0</td>
        <td>Chris Brown feat. T-Pain</td>
        <td>Chris Brown</td>
        <td>Kiss Kiss</td>
        <td>5626</td>
    </tr>
    <tr>
        <td>2007.0</td>
        <td>93.0</td>
        <td>Chris Brown feat. T-Pain</td>
        <td>T-Pain</td>
        <td>Kiss Kiss</td>
        <td>5627</td>
    </tr>
    <tr>
        <td>2007.0</td>
        <td>88.0</td>
        <td>Bow Wow feat. T-Pain and Johnta Austin</td>
        <td>Johnta Austin</td>
        <td>Outta My System</td>
        <td>5620</td>
    </tr>
    <tr>
        <td>2007.0</td>
        <td>88.0</td>
        <td>Bow Wow feat. T-Pain and Johnta Austin</td>
        <td>Bow Wow</td>
        <td>Outta My System</td>
        <td>5618</td>
    </tr>
    <tr>
        <td>2007.0</td>
        <td>88.0</td>
        <td>Bow Wow feat. T-Pain and Johnta Austin</td>
        <td>T-Pain</td>
        <td>Outta My System</td>
        <td>5619</td>
    </tr>
</table>



#### A query that returns songs that ranked between 10 and 20 (inclusive) in 1993, 2003, or 2013. Order the results by year and rank, and leave a comment on each line of the WHERE clause to indicate what that line does




```sql
%%sql
SELECT * FROM bill_board
WHERE year IN (1993,2003,2013) AND year_rank BETWEEN 10 AND 20
ORDER BY year, year_rank
LIMIT 15
```

     * postgresql://postgres:***@localhost/portfolio
    15 rows affected.





<table>
    <tr>
        <th>year</th>
        <th>year_rank</th>
        <th>group</th>
        <th>artist</th>
        <th>song_name</th>
        <th>id</th>
    </tr>
    <tr>
        <td>1993.0</td>
        <td>10.0</td>
        <td>Snow</td>
        <td>Snow</td>
        <td>Informer</td>
        <td>3814</td>
    </tr>
    <tr>
        <td>1993.0</td>
        <td>11.0</td>
        <td>Dr. Dre</td>
        <td>Dr. Dre</td>
        <td>Nuthin&#x27; But A &quot;G&quot; Thang</td>
        <td>3815</td>
    </tr>
    <tr>
        <td>1993.0</td>
        <td>12.0</td>
        <td>Boyz II Men</td>
        <td>Boyz II Men</td>
        <td>In The Still Of The Nite</td>
        <td>3816</td>
    </tr>
    <tr>
        <td>1993.0</td>
        <td>13.0</td>
        <td>Jade</td>
        <td>Jade</td>
        <td>Don&#x27;t Walk Away</td>
        <td>3817</td>
    </tr>
    <tr>
        <td>1993.0</td>
        <td>14.0</td>
        <td>H-Town</td>
        <td>H-Town</td>
        <td>Knockin&#x27; Da Boots</td>
        <td>3818</td>
    </tr>
    <tr>
        <td>1993.0</td>
        <td>15.0</td>
        <td>Jodeci</td>
        <td>Jodeci</td>
        <td>Lately</td>
        <td>3819</td>
    </tr>
    <tr>
        <td>1993.0</td>
        <td>16.0</td>
        <td>Duice</td>
        <td>Duice</td>
        <td>Dazzey Duks</td>
        <td>3820</td>
    </tr>
    <tr>
        <td>1993.0</td>
        <td>17.0</td>
        <td>Robin S.</td>
        <td>Robin S.</td>
        <td>Show Me Love</td>
        <td>3821</td>
    </tr>
    <tr>
        <td>1993.0</td>
        <td>18.0</td>
        <td>Peabo Bryson and Regina Belle</td>
        <td>Regina Belle</td>
        <td>A Whole New World</td>
        <td>3823</td>
    </tr>
    <tr>
        <td>1993.0</td>
        <td>18.0</td>
        <td>Peabo Bryson and Regina Belle</td>
        <td>Peabo Bryson</td>
        <td>A Whole New World</td>
        <td>3822</td>
    </tr>
    <tr>
        <td>1993.0</td>
        <td>19.0</td>
        <td>Janet Jackson</td>
        <td>Janet Jackson</td>
        <td>If</td>
        <td>3824</td>
    </tr>
    <tr>
        <td>1993.0</td>
        <td>20.0</td>
        <td>SWV</td>
        <td>SWV</td>
        <td>I&#x27;m So Into You</td>
        <td>3825</td>
    </tr>
    <tr>
        <td>2003.0</td>
        <td>10.0</td>
        <td>Evanescence feat. Paul McCoy</td>
        <td>Paul McCoy</td>
        <td>Bring Me To Life</td>
        <td>4951</td>
    </tr>
    <tr>
        <td>2003.0</td>
        <td>10.0</td>
        <td>Evanescence feat. Paul McCoy</td>
        <td>Evanescence</td>
        <td>Bring Me To Life</td>
        <td>4950</td>
    </tr>
    <tr>
        <td>2003.0</td>
        <td>11.0</td>
        <td>Lil Jon and The East Side Boyz feat. Ying Yang Twins</td>
        <td>Lil Jon and the East Side Boyz</td>
        <td>Get Low</td>
        <td>4952</td>
    </tr>
</table>




```python

```


```python

```


```python

```
