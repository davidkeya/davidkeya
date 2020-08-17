---
header:
  overlay_image: /assets/images/sales/rupixen.jpg
  caption: "Photo credit: [**rupixen**](https://unsplash.com)"
permalink: /portfolio/Sales_Analysis/
date: 2020-05-22
toc: true
toc_label: "Contents"
---

#  Twelve Months of Sales Data Analysis

## Summary
In this project I use Python Pandas & Python Matplotlib to analyze and answer business questions about 12 months worth of sales data. The data contains hundreds of thousands of electronics store purchases broken down by month, product type, cost, purchase address, etc.

I start by cleaning the data. Tasks during this section include:

Drop NaN values from DataFrame
Removing rows based on a condition
Change the type of columns (to_numeric, to_datetime, astype)
Once the data is cleaned up a bit, we move the data exploration section. In this section we explore 5 high level business questions related to our data:

What was the best month for sales? How much was earned that month?
What city sold the most product?
What time should we display advertisemens to maximize the likelihood of customer’s buying product?
What products are most often sold together?
What product sold the most? Why do you think it sold the most?
To answer these questions we walk through many different pandas & matplotlib methods. They include:

Concatenating multiple csvs together to create a new DataFrame (pd.concat)
Adding columns
Parsing cells as strings to make new columns (.str)
Using the .apply() method
Using groupby to perform aggregate analysis
Plotting bar charts and lines graphs to visualize our results
Labeling our graphs

#### Import Necessary files


```python
import pandas as pd
import os
```

###### Increase width display within the notebook


```python
from IPython.core.display import display, HTML
display(HTML("<style>.container {width:90% !important;}</style>"))
```


<style>.container {width:90% !important;}</style>


#### Merging 12 Months of data into a single file csv file


```python
df = pd.read_csv("./Sales_Data/Sales_April_2019.csv")

files = [file for file in os.listdir ('./Sales_Data')]

all_months_data = pd.DataFrame()

for file in files:
    df = pd.read_csv("./Sales_Data/"+file)
    all_months_data = pd.concat([all_months_data, df])

all_months_data.to_csv("all_data.csv", index=False)



```

#### Read in updated dataframe


```python
all_data = pd.read_csv("all_data.csv")

all_data.head()

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
      <th>Order ID</th>
      <th>Product</th>
      <th>Quantity Ordered</th>
      <th>Price Each</th>
      <th>Order Date</th>
      <th>Purchase Address</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>295665</td>
      <td>Macbook Pro Laptop</td>
      <td>1</td>
      <td>1700</td>
      <td>12/30/19 00:01</td>
      <td>136 Church St, New York City, NY 10001</td>
    </tr>
    <tr>
      <th>1</th>
      <td>295666</td>
      <td>LG Washing Machine</td>
      <td>1</td>
      <td>600.0</td>
      <td>12/29/19 07:03</td>
      <td>562 2nd St, New York City, NY 10001</td>
    </tr>
    <tr>
      <th>2</th>
      <td>295667</td>
      <td>USB-C Charging Cable</td>
      <td>1</td>
      <td>11.95</td>
      <td>12/12/19 18:21</td>
      <td>277 Main St, New York City, NY 10001</td>
    </tr>
    <tr>
      <th>3</th>
      <td>295668</td>
      <td>27in FHD Monitor</td>
      <td>1</td>
      <td>149.99</td>
      <td>12/22/19 15:13</td>
      <td>410 6th St, San Francisco, CA 94016</td>
    </tr>
    <tr>
      <th>4</th>
      <td>295669</td>
      <td>USB-C Charging Cable</td>
      <td>1</td>
      <td>11.95</td>
      <td>12/18/19 12:38</td>
      <td>43 Hill St, Atlanta, GA 30301</td>
    </tr>
  </tbody>
</table>
</div>



####  Augument Data with additional columns

##### Add Month column


```python
all_data['Month'] = all_data['Order Date'].str[0:2]
```


```python
all_data.head()
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
      <th>Order ID</th>
      <th>Product</th>
      <th>Quantity Ordered</th>
      <th>Price Each</th>
      <th>Order Date</th>
      <th>Purchase Address</th>
      <th>Month</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>295665</td>
      <td>Macbook Pro Laptop</td>
      <td>1</td>
      <td>1700</td>
      <td>12/30/19 00:01</td>
      <td>136 Church St, New York City, NY 10001</td>
      <td>12</td>
    </tr>
    <tr>
      <th>1</th>
      <td>295666</td>
      <td>LG Washing Machine</td>
      <td>1</td>
      <td>600.0</td>
      <td>12/29/19 07:03</td>
      <td>562 2nd St, New York City, NY 10001</td>
      <td>12</td>
    </tr>
    <tr>
      <th>2</th>
      <td>295667</td>
      <td>USB-C Charging Cable</td>
      <td>1</td>
      <td>11.95</td>
      <td>12/12/19 18:21</td>
      <td>277 Main St, New York City, NY 10001</td>
      <td>12</td>
    </tr>
    <tr>
      <th>3</th>
      <td>295668</td>
      <td>27in FHD Monitor</td>
      <td>1</td>
      <td>149.99</td>
      <td>12/22/19 15:13</td>
      <td>410 6th St, San Francisco, CA 94016</td>
      <td>12</td>
    </tr>
    <tr>
      <th>4</th>
      <td>295669</td>
      <td>USB-C Charging Cable</td>
      <td>1</td>
      <td>11.95</td>
      <td>12/18/19 12:38</td>
      <td>43 Hill St, Atlanta, GA 30301</td>
      <td>12</td>
    </tr>
  </tbody>
</table>
</div>



#### Clean up data

##### Count the number of missing values in a specific column


```python
null_count = all_data.Month.isnull()
null_count
```




    0         False
    1         False
    2         False
    3         False
    4         False
              ...  
    186845    False
    186846    False
    186847    False
    186848    False
    186849    False
    Name: Month, Length: 186850, dtype: bool



##### Show missing content in Month only


```python
all_data[null_count]
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
      <th>Order ID</th>
      <th>Product</th>
      <th>Quantity Ordered</th>
      <th>Price Each</th>
      <th>Order Date</th>
      <th>Purchase Address</th>
      <th>Month</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>264</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>648</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>680</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1385</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1495</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
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
    </tr>
    <tr>
      <th>185795</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>185868</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>185887</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>185960</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>186580</th>
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
<p>545 rows × 7 columns</p>
</div>




```python
# Rows and columns of missing data
all_data[null_count].shape
```




    (545, 7)



>##### Task1:Drop rows of NAN


```python
all_data = all_data.dropna(how='all')
all_data
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
      <th>Order ID</th>
      <th>Product</th>
      <th>Quantity Ordered</th>
      <th>Price Each</th>
      <th>Order Date</th>
      <th>Purchase Address</th>
      <th>Month</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>295665</td>
      <td>Macbook Pro Laptop</td>
      <td>1</td>
      <td>1700</td>
      <td>12/30/19 00:01</td>
      <td>136 Church St, New York City, NY 10001</td>
      <td>12</td>
    </tr>
    <tr>
      <th>1</th>
      <td>295666</td>
      <td>LG Washing Machine</td>
      <td>1</td>
      <td>600.0</td>
      <td>12/29/19 07:03</td>
      <td>562 2nd St, New York City, NY 10001</td>
      <td>12</td>
    </tr>
    <tr>
      <th>2</th>
      <td>295667</td>
      <td>USB-C Charging Cable</td>
      <td>1</td>
      <td>11.95</td>
      <td>12/12/19 18:21</td>
      <td>277 Main St, New York City, NY 10001</td>
      <td>12</td>
    </tr>
    <tr>
      <th>3</th>
      <td>295668</td>
      <td>27in FHD Monitor</td>
      <td>1</td>
      <td>149.99</td>
      <td>12/22/19 15:13</td>
      <td>410 6th St, San Francisco, CA 94016</td>
      <td>12</td>
    </tr>
    <tr>
      <th>4</th>
      <td>295669</td>
      <td>USB-C Charging Cable</td>
      <td>1</td>
      <td>11.95</td>
      <td>12/18/19 12:38</td>
      <td>43 Hill St, Atlanta, GA 30301</td>
      <td>12</td>
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
    </tr>
    <tr>
      <th>186845</th>
      <td>222905</td>
      <td>AAA Batteries (4-pack)</td>
      <td>1</td>
      <td>2.99</td>
      <td>06/07/19 19:02</td>
      <td>795 Pine St, Boston, MA 02215</td>
      <td>06</td>
    </tr>
    <tr>
      <th>186846</th>
      <td>222906</td>
      <td>27in FHD Monitor</td>
      <td>1</td>
      <td>149.99</td>
      <td>06/01/19 19:29</td>
      <td>495 North St, New York City, NY 10001</td>
      <td>06</td>
    </tr>
    <tr>
      <th>186847</th>
      <td>222907</td>
      <td>USB-C Charging Cable</td>
      <td>1</td>
      <td>11.95</td>
      <td>06/22/19 18:57</td>
      <td>319 Ridge St, San Francisco, CA 94016</td>
      <td>06</td>
    </tr>
    <tr>
      <th>186848</th>
      <td>222908</td>
      <td>USB-C Charging Cable</td>
      <td>1</td>
      <td>11.95</td>
      <td>06/26/19 18:35</td>
      <td>916 Main St, San Francisco, CA 94016</td>
      <td>06</td>
    </tr>
    <tr>
      <th>186849</th>
      <td>222909</td>
      <td>AAA Batteries (4-pack)</td>
      <td>1</td>
      <td>2.99</td>
      <td>06/25/19 14:33</td>
      <td>209 11th St, Atlanta, GA 30301</td>
      <td>06</td>
    </tr>
  </tbody>
</table>
<p>186305 rows × 7 columns</p>
</div>




```python
#Check data type for Month Column
all_data.Month.dtype
```




    dtype('O')



##### Data type for the month column is in the string format. Need to convert to int

>##### Task 2: Convert Month Column to Interger


```python
all_data['Month'] = all_data['Month'].astype('int32')

all_data.head()
```


    ---------------------------------------------------------------------------

    ValueError                                Traceback (most recent call last)

    <ipython-input-173-fa8ec1935ebb> in <module>
    ----> 1 all_data['Month'] = all_data['Month'].astype('int32')
          2
          3 all_data.head()


    ~/.pyenv/versions/3.7.3/lib/python3.7/site-packages/pandas/core/generic.py in astype(self, dtype, copy, errors)
       5696         else:
       5697             # else, only a single dtype is given
    -> 5698             new_data = self._data.astype(dtype=dtype, copy=copy, errors=errors)
       5699             return self._constructor(new_data).__finalize__(self)
       5700


    ~/.pyenv/versions/3.7.3/lib/python3.7/site-packages/pandas/core/internals/managers.py in astype(self, dtype, copy, errors)
        580
        581     def astype(self, dtype, copy: bool = False, errors: str = "raise"):
    --> 582         return self.apply("astype", dtype=dtype, copy=copy, errors=errors)
        583
        584     def convert(self, **kwargs):


    ~/.pyenv/versions/3.7.3/lib/python3.7/site-packages/pandas/core/internals/managers.py in apply(self, f, filter, **kwargs)
        440                 applied = b.apply(f, **kwargs)
        441             else:
    --> 442                 applied = getattr(b, f)(**kwargs)
        443             result_blocks = _extend_blocks(applied, result_blocks)
        444


    ~/.pyenv/versions/3.7.3/lib/python3.7/site-packages/pandas/core/internals/blocks.py in astype(self, dtype, copy, errors)
        623             vals1d = values.ravel()
        624             try:
    --> 625                 values = astype_nansafe(vals1d, dtype, copy=True)
        626             except (ValueError, TypeError):
        627                 # e.g. astype_nansafe can fail on object-dtype of strings


    ~/.pyenv/versions/3.7.3/lib/python3.7/site-packages/pandas/core/dtypes/cast.py in astype_nansafe(arr, dtype, copy, skipna)
        872         # work around NumPy brokenness, #1987
        873         if np.issubdtype(dtype.type, np.integer):
    --> 874             return lib.astype_intsafe(arr.ravel(), dtype).reshape(arr.shape)
        875
        876         # if we have a datetime/timedelta array of objects


    pandas/_libs/lib.pyx in pandas._libs.lib.astype_intsafe()


    ValueError: invalid literal for int() with base 10: 'Or'


##### Converting Month Column to Interger not possible because of invalid literal for int() with base 10: 'Or'

##### Find 'Or' and delete it


```python
all_data = all_data[all_data['Order Date'].str[0:2] != 'Or']

all_data.head()
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
      <th>Order ID</th>
      <th>Product</th>
      <th>Quantity Ordered</th>
      <th>Price Each</th>
      <th>Order Date</th>
      <th>Purchase Address</th>
      <th>Month</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>295665</td>
      <td>Macbook Pro Laptop</td>
      <td>1</td>
      <td>1700</td>
      <td>12/30/19 00:01</td>
      <td>136 Church St, New York City, NY 10001</td>
      <td>12</td>
    </tr>
    <tr>
      <th>1</th>
      <td>295666</td>
      <td>LG Washing Machine</td>
      <td>1</td>
      <td>600.0</td>
      <td>12/29/19 07:03</td>
      <td>562 2nd St, New York City, NY 10001</td>
      <td>12</td>
    </tr>
    <tr>
      <th>2</th>
      <td>295667</td>
      <td>USB-C Charging Cable</td>
      <td>1</td>
      <td>11.95</td>
      <td>12/12/19 18:21</td>
      <td>277 Main St, New York City, NY 10001</td>
      <td>12</td>
    </tr>
    <tr>
      <th>3</th>
      <td>295668</td>
      <td>27in FHD Monitor</td>
      <td>1</td>
      <td>149.99</td>
      <td>12/22/19 15:13</td>
      <td>410 6th St, San Francisco, CA 94016</td>
      <td>12</td>
    </tr>
    <tr>
      <th>4</th>
      <td>295669</td>
      <td>USB-C Charging Cable</td>
      <td>1</td>
      <td>11.95</td>
      <td>12/18/19 12:38</td>
      <td>43 Hill St, Atlanta, GA 30301</td>
      <td>12</td>
    </tr>
  </tbody>
</table>
</div>



##### From Task 2: Convert Month Column to Interger


```python
all_data['Month'] = all_data['Month'].astype('int32')

all_data.head()  
```

    /Users/davidkeya/.pyenv/versions/3.7.3/lib/python3.7/site-packages/ipykernel_launcher.py:1: SettingWithCopyWarning:
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead

    See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
      """Entry point for launching an IPython kernel.





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
      <th>Order ID</th>
      <th>Product</th>
      <th>Quantity Ordered</th>
      <th>Price Each</th>
      <th>Order Date</th>
      <th>Purchase Address</th>
      <th>Month</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>295665</td>
      <td>Macbook Pro Laptop</td>
      <td>1</td>
      <td>1700</td>
      <td>12/30/19 00:01</td>
      <td>136 Church St, New York City, NY 10001</td>
      <td>12</td>
    </tr>
    <tr>
      <th>1</th>
      <td>295666</td>
      <td>LG Washing Machine</td>
      <td>1</td>
      <td>600.0</td>
      <td>12/29/19 07:03</td>
      <td>562 2nd St, New York City, NY 10001</td>
      <td>12</td>
    </tr>
    <tr>
      <th>2</th>
      <td>295667</td>
      <td>USB-C Charging Cable</td>
      <td>1</td>
      <td>11.95</td>
      <td>12/12/19 18:21</td>
      <td>277 Main St, New York City, NY 10001</td>
      <td>12</td>
    </tr>
    <tr>
      <th>3</th>
      <td>295668</td>
      <td>27in FHD Monitor</td>
      <td>1</td>
      <td>149.99</td>
      <td>12/22/19 15:13</td>
      <td>410 6th St, San Francisco, CA 94016</td>
      <td>12</td>
    </tr>
    <tr>
      <th>4</th>
      <td>295669</td>
      <td>USB-C Charging Cable</td>
      <td>1</td>
      <td>11.95</td>
      <td>12/18/19 12:38</td>
      <td>43 Hill St, Atlanta, GA 30301</td>
      <td>12</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Month column now int32
all_data.Month.dtype
```




    dtype('int32')



>##### Task4: Convert columns to the correct type


```python
# Convert to Interger and float
all_data['Quantity Ordered'] = pd.to_numeric(all_data['Quantity Ordered'])
all_data['Price Each'] = pd.to_numeric(all_data['Price Each'])

all_data.head()
```

    /Users/davidkeya/.pyenv/versions/3.7.3/lib/python3.7/site-packages/ipykernel_launcher.py:2: SettingWithCopyWarning:
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead

    See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy

    /Users/davidkeya/.pyenv/versions/3.7.3/lib/python3.7/site-packages/ipykernel_launcher.py:3: SettingWithCopyWarning:
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead

    See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
      This is separate from the ipykernel package so we can avoid doing imports until





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
      <th>Order ID</th>
      <th>Product</th>
      <th>Quantity Ordered</th>
      <th>Price Each</th>
      <th>Order Date</th>
      <th>Purchase Address</th>
      <th>Month</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>295665</td>
      <td>Macbook Pro Laptop</td>
      <td>1</td>
      <td>1700.00</td>
      <td>12/30/19 00:01</td>
      <td>136 Church St, New York City, NY 10001</td>
      <td>12</td>
    </tr>
    <tr>
      <th>1</th>
      <td>295666</td>
      <td>LG Washing Machine</td>
      <td>1</td>
      <td>600.00</td>
      <td>12/29/19 07:03</td>
      <td>562 2nd St, New York City, NY 10001</td>
      <td>12</td>
    </tr>
    <tr>
      <th>2</th>
      <td>295667</td>
      <td>USB-C Charging Cable</td>
      <td>1</td>
      <td>11.95</td>
      <td>12/12/19 18:21</td>
      <td>277 Main St, New York City, NY 10001</td>
      <td>12</td>
    </tr>
    <tr>
      <th>3</th>
      <td>295668</td>
      <td>27in FHD Monitor</td>
      <td>1</td>
      <td>149.99</td>
      <td>12/22/19 15:13</td>
      <td>410 6th St, San Francisco, CA 94016</td>
      <td>12</td>
    </tr>
    <tr>
      <th>4</th>
      <td>295669</td>
      <td>USB-C Charging Cable</td>
      <td>1</td>
      <td>11.95</td>
      <td>12/18/19 12:38</td>
      <td>43 Hill St, Atlanta, GA 30301</td>
      <td>12</td>
    </tr>
  </tbody>
</table>
</div>



>##### Task 5: Add sales column


```python
all_data['Sales'] = all_data['Quantity Ordered'] * all_data['Price Each']

all_data.head()
```

    /Users/davidkeya/.pyenv/versions/3.7.3/lib/python3.7/site-packages/ipykernel_launcher.py:1: SettingWithCopyWarning:
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead

    See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
      """Entry point for launching an IPython kernel.





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
      <th>Order ID</th>
      <th>Product</th>
      <th>Quantity Ordered</th>
      <th>Price Each</th>
      <th>Order Date</th>
      <th>Purchase Address</th>
      <th>Month</th>
      <th>Sales</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>295665</td>
      <td>Macbook Pro Laptop</td>
      <td>1</td>
      <td>1700.00</td>
      <td>12/30/19 00:01</td>
      <td>136 Church St, New York City, NY 10001</td>
      <td>12</td>
      <td>1700.00</td>
    </tr>
    <tr>
      <th>1</th>
      <td>295666</td>
      <td>LG Washing Machine</td>
      <td>1</td>
      <td>600.00</td>
      <td>12/29/19 07:03</td>
      <td>562 2nd St, New York City, NY 10001</td>
      <td>12</td>
      <td>600.00</td>
    </tr>
    <tr>
      <th>2</th>
      <td>295667</td>
      <td>USB-C Charging Cable</td>
      <td>1</td>
      <td>11.95</td>
      <td>12/12/19 18:21</td>
      <td>277 Main St, New York City, NY 10001</td>
      <td>12</td>
      <td>11.95</td>
    </tr>
    <tr>
      <th>3</th>
      <td>295668</td>
      <td>27in FHD Monitor</td>
      <td>1</td>
      <td>149.99</td>
      <td>12/22/19 15:13</td>
      <td>410 6th St, San Francisco, CA 94016</td>
      <td>12</td>
      <td>149.99</td>
    </tr>
    <tr>
      <th>4</th>
      <td>295669</td>
      <td>USB-C Charging Cable</td>
      <td>1</td>
      <td>11.95</td>
      <td>12/18/19 12:38</td>
      <td>43 Hill St, Atlanta, GA 30301</td>
      <td>12</td>
      <td>11.95</td>
    </tr>
  </tbody>
</table>
</div>



> ##### Task 6: Add a city column


```python
# Using .apply()
def get_city(address):
    return address.split(',')[1]

def get_state(address):
    return address.split(',')[2].split(' ')[1]

all_data['City'] = all_data['Purchase Address'].apply(lambda x: get_city(x) + ' (' + get_state(x) + ')')

all_data.head()
```

    /Users/davidkeya/.pyenv/versions/3.7.3/lib/python3.7/site-packages/ipykernel_launcher.py:8: SettingWithCopyWarning:
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead

    See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy






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
      <th>Order ID</th>
      <th>Product</th>
      <th>Quantity Ordered</th>
      <th>Price Each</th>
      <th>Order Date</th>
      <th>Purchase Address</th>
      <th>Month</th>
      <th>Sales</th>
      <th>City</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>295665</td>
      <td>Macbook Pro Laptop</td>
      <td>1</td>
      <td>1700.00</td>
      <td>12/30/19 00:01</td>
      <td>136 Church St, New York City, NY 10001</td>
      <td>12</td>
      <td>1700.00</td>
      <td>New York City (NY)</td>
    </tr>
    <tr>
      <th>1</th>
      <td>295666</td>
      <td>LG Washing Machine</td>
      <td>1</td>
      <td>600.00</td>
      <td>12/29/19 07:03</td>
      <td>562 2nd St, New York City, NY 10001</td>
      <td>12</td>
      <td>600.00</td>
      <td>New York City (NY)</td>
    </tr>
    <tr>
      <th>2</th>
      <td>295667</td>
      <td>USB-C Charging Cable</td>
      <td>1</td>
      <td>11.95</td>
      <td>12/12/19 18:21</td>
      <td>277 Main St, New York City, NY 10001</td>
      <td>12</td>
      <td>11.95</td>
      <td>New York City (NY)</td>
    </tr>
    <tr>
      <th>3</th>
      <td>295668</td>
      <td>27in FHD Monitor</td>
      <td>1</td>
      <td>149.99</td>
      <td>12/22/19 15:13</td>
      <td>410 6th St, San Francisco, CA 94016</td>
      <td>12</td>
      <td>149.99</td>
      <td>San Francisco (CA)</td>
    </tr>
    <tr>
      <th>4</th>
      <td>295669</td>
      <td>USB-C Charging Cable</td>
      <td>1</td>
      <td>11.95</td>
      <td>12/18/19 12:38</td>
      <td>43 Hill St, Atlanta, GA 30301</td>
      <td>12</td>
      <td>11.95</td>
      <td>Atlanta (GA)</td>
    </tr>
  </tbody>
</table>
</div>



#### What was the best month for sales and how much was earned that month


```python
all_data.groupby('Month').sum()
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
      <th>Quantity Ordered</th>
      <th>Price Each</th>
      <th>Sales</th>
    </tr>
    <tr>
      <th>Month</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>10903</td>
      <td>1.811768e+06</td>
      <td>1.822257e+06</td>
    </tr>
    <tr>
      <th>2</th>
      <td>13449</td>
      <td>2.188885e+06</td>
      <td>2.202022e+06</td>
    </tr>
    <tr>
      <th>3</th>
      <td>17005</td>
      <td>2.791208e+06</td>
      <td>2.807100e+06</td>
    </tr>
    <tr>
      <th>4</th>
      <td>20558</td>
      <td>3.367671e+06</td>
      <td>3.390670e+06</td>
    </tr>
    <tr>
      <th>5</th>
      <td>18667</td>
      <td>3.135125e+06</td>
      <td>3.152607e+06</td>
    </tr>
    <tr>
      <th>6</th>
      <td>15253</td>
      <td>2.562026e+06</td>
      <td>2.577802e+06</td>
    </tr>
    <tr>
      <th>7</th>
      <td>16072</td>
      <td>2.632540e+06</td>
      <td>2.647776e+06</td>
    </tr>
    <tr>
      <th>8</th>
      <td>13448</td>
      <td>2.230345e+06</td>
      <td>2.244468e+06</td>
    </tr>
    <tr>
      <th>9</th>
      <td>13109</td>
      <td>2.084992e+06</td>
      <td>2.097560e+06</td>
    </tr>
    <tr>
      <th>10</th>
      <td>22703</td>
      <td>3.715555e+06</td>
      <td>3.736727e+06</td>
    </tr>
    <tr>
      <th>11</th>
      <td>19798</td>
      <td>3.180601e+06</td>
      <td>3.199603e+06</td>
    </tr>
    <tr>
      <th>12</th>
      <td>28114</td>
      <td>4.588415e+06</td>
      <td>4.613443e+06</td>
    </tr>
  </tbody>
</table>
</div>



##### A visual of the Sales for every month


```python
import matplotlib.pyplot as plt

all_data.groupby('Month').Sales.sum().plot(kind='bar', figsize=(16,8));

plt.ylabel('Sales in USD $')
plt.xlabel('Month Number')
plt.show()
```


![png](/assets/images/sales/output_40_0.png)


#### What city has the highest number of sales.


```python
all_data.groupby('City').sum()
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
      <th>Quantity Ordered</th>
      <th>Price Each</th>
      <th>Month</th>
      <th>Sales</th>
    </tr>
    <tr>
      <th>City</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Atlanta (GA)</th>
      <td>16602</td>
      <td>2.779908e+06</td>
      <td>104794</td>
      <td>2.795499e+06</td>
    </tr>
    <tr>
      <th>Austin (TX)</th>
      <td>11153</td>
      <td>1.809874e+06</td>
      <td>69829</td>
      <td>1.819582e+06</td>
    </tr>
    <tr>
      <th>Boston (MA)</th>
      <td>22528</td>
      <td>3.637410e+06</td>
      <td>141112</td>
      <td>3.661642e+06</td>
    </tr>
    <tr>
      <th>Dallas (TX)</th>
      <td>16730</td>
      <td>2.752628e+06</td>
      <td>104620</td>
      <td>2.767975e+06</td>
    </tr>
    <tr>
      <th>Los Angeles (CA)</th>
      <td>33289</td>
      <td>5.421435e+06</td>
      <td>208325</td>
      <td>5.452571e+06</td>
    </tr>
    <tr>
      <th>New York City (NY)</th>
      <td>27932</td>
      <td>4.635371e+06</td>
      <td>175741</td>
      <td>4.664317e+06</td>
    </tr>
    <tr>
      <th>Portland (ME)</th>
      <td>2750</td>
      <td>4.471893e+05</td>
      <td>17144</td>
      <td>4.497583e+05</td>
    </tr>
    <tr>
      <th>Portland (OR)</th>
      <td>11303</td>
      <td>1.860558e+06</td>
      <td>70621</td>
      <td>1.870732e+06</td>
    </tr>
    <tr>
      <th>San Francisco (CA)</th>
      <td>50239</td>
      <td>8.211462e+06</td>
      <td>315520</td>
      <td>8.262204e+06</td>
    </tr>
    <tr>
      <th>Seattle (WA)</th>
      <td>16553</td>
      <td>2.733296e+06</td>
      <td>104941</td>
      <td>2.747755e+06</td>
    </tr>
  </tbody>
</table>
</div>



##### A visual of the Sales for every City


```python
import matplotlib.pyplot as plt
all_data.groupby('City').Sales.sum().plot(kind='bar',figsize=(16,8))
plt.ylabel('Sales in USD $')
plt.xlabel('City')
plt.show()
```


![png](/assets/images/sales/output_44_0.png)


#### What time should we display advertisements to maximize likelihood of customers buying product?

##### Format the Order Date


```python
all_data['Order Date'] = pd.to_datetime(all_data['Order Date'])

all_data.head()
```

    /Users/davidkeya/.pyenv/versions/3.7.3/lib/python3.7/site-packages/ipykernel_launcher.py:1: SettingWithCopyWarning:
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead

    See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
      """Entry point for launching an IPython kernel.





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
      <th>Order ID</th>
      <th>Product</th>
      <th>Quantity Ordered</th>
      <th>Price Each</th>
      <th>Order Date</th>
      <th>Purchase Address</th>
      <th>Month</th>
      <th>Sales</th>
      <th>City</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>295665</td>
      <td>Macbook Pro Laptop</td>
      <td>1</td>
      <td>1700.00</td>
      <td>2019-12-30 00:01:00</td>
      <td>136 Church St, New York City, NY 10001</td>
      <td>12</td>
      <td>1700.00</td>
      <td>New York City (NY)</td>
    </tr>
    <tr>
      <th>1</th>
      <td>295666</td>
      <td>LG Washing Machine</td>
      <td>1</td>
      <td>600.00</td>
      <td>2019-12-29 07:03:00</td>
      <td>562 2nd St, New York City, NY 10001</td>
      <td>12</td>
      <td>600.00</td>
      <td>New York City (NY)</td>
    </tr>
    <tr>
      <th>2</th>
      <td>295667</td>
      <td>USB-C Charging Cable</td>
      <td>1</td>
      <td>11.95</td>
      <td>2019-12-12 18:21:00</td>
      <td>277 Main St, New York City, NY 10001</td>
      <td>12</td>
      <td>11.95</td>
      <td>New York City (NY)</td>
    </tr>
    <tr>
      <th>3</th>
      <td>295668</td>
      <td>27in FHD Monitor</td>
      <td>1</td>
      <td>149.99</td>
      <td>2019-12-22 15:13:00</td>
      <td>410 6th St, San Francisco, CA 94016</td>
      <td>12</td>
      <td>149.99</td>
      <td>San Francisco (CA)</td>
    </tr>
    <tr>
      <th>4</th>
      <td>295669</td>
      <td>USB-C Charging Cable</td>
      <td>1</td>
      <td>11.95</td>
      <td>2019-12-18 12:38:00</td>
      <td>43 Hill St, Atlanta, GA 30301</td>
      <td>12</td>
      <td>11.95</td>
      <td>Atlanta (GA)</td>
    </tr>
  </tbody>
</table>
</div>



##### Add hour and Minute column


```python
all_data['Hour'] = all_data['Order Date'].dt.hour
all_data['Minute'] = all_data['Order Date'].dt.minute

all_data.head()
```

    /Users/davidkeya/.pyenv/versions/3.7.3/lib/python3.7/site-packages/ipykernel_launcher.py:1: SettingWithCopyWarning:
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead

    See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
      """Entry point for launching an IPython kernel.
    /Users/davidkeya/.pyenv/versions/3.7.3/lib/python3.7/site-packages/ipykernel_launcher.py:2: SettingWithCopyWarning:
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead

    See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy






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
      <th>Order ID</th>
      <th>Product</th>
      <th>Quantity Ordered</th>
      <th>Price Each</th>
      <th>Order Date</th>
      <th>Purchase Address</th>
      <th>Month</th>
      <th>Sales</th>
      <th>City</th>
      <th>Hour</th>
      <th>Minute</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>295665</td>
      <td>Macbook Pro Laptop</td>
      <td>1</td>
      <td>1700.00</td>
      <td>2019-12-30 00:01:00</td>
      <td>136 Church St, New York City, NY 10001</td>
      <td>12</td>
      <td>1700.00</td>
      <td>New York City (NY)</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>295666</td>
      <td>LG Washing Machine</td>
      <td>1</td>
      <td>600.00</td>
      <td>2019-12-29 07:03:00</td>
      <td>562 2nd St, New York City, NY 10001</td>
      <td>12</td>
      <td>600.00</td>
      <td>New York City (NY)</td>
      <td>7</td>
      <td>3</td>
    </tr>
    <tr>
      <th>2</th>
      <td>295667</td>
      <td>USB-C Charging Cable</td>
      <td>1</td>
      <td>11.95</td>
      <td>2019-12-12 18:21:00</td>
      <td>277 Main St, New York City, NY 10001</td>
      <td>12</td>
      <td>11.95</td>
      <td>New York City (NY)</td>
      <td>18</td>
      <td>21</td>
    </tr>
    <tr>
      <th>3</th>
      <td>295668</td>
      <td>27in FHD Monitor</td>
      <td>1</td>
      <td>149.99</td>
      <td>2019-12-22 15:13:00</td>
      <td>410 6th St, San Francisco, CA 94016</td>
      <td>12</td>
      <td>149.99</td>
      <td>San Francisco (CA)</td>
      <td>15</td>
      <td>13</td>
    </tr>
    <tr>
      <th>4</th>
      <td>295669</td>
      <td>USB-C Charging Cable</td>
      <td>1</td>
      <td>11.95</td>
      <td>2019-12-18 12:38:00</td>
      <td>43 Hill St, Atlanta, GA 30301</td>
      <td>12</td>
      <td>11.95</td>
      <td>Atlanta (GA)</td>
      <td>12</td>
      <td>38</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Total sales for every hour
all_data.groupby('Hour').sum()['Sales']
```




    Hour
    0      713721.27
    1      460866.88
    2      234851.44
    3      145757.89
    4      162661.01
    5      230679.82
    6      448113.00
    7      744854.12
    8     1192348.97
    9     1639030.58
    10    1944286.77
    11    2300610.24
    12    2316821.34
    13    2155389.80
    14    2083672.73
    15    1941549.60
    16    1904601.31
    17    2129361.61
    18    2219348.30
    19    2412938.54
    20    2281716.24
    21    2042000.86
    22    1607549.21
    23    1179304.44
    Name: Sales, dtype: float64



##### A visual of Sales for every hour


```python
all_data.groupby('Hour').Sales.sum().plot(kind='line',figsize=(20,8))
plt.ylabel('Sales in USD $')
plt.xlabel('Hour')
plt.grid()
plt.xticks()
plt.show()
```


![png](/assets/images/sales/output_52_0.png)


#### What products are most often sold together


```python
all_data.head()
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
      <th>Order ID</th>
      <th>Product</th>
      <th>Quantity Ordered</th>
      <th>Price Each</th>
      <th>Order Date</th>
      <th>Purchase Address</th>
      <th>Month</th>
      <th>Sales</th>
      <th>City</th>
      <th>Hour</th>
      <th>Minute</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>295665</td>
      <td>Macbook Pro Laptop</td>
      <td>1</td>
      <td>1700.00</td>
      <td>2019-12-30 00:01:00</td>
      <td>136 Church St, New York City, NY 10001</td>
      <td>12</td>
      <td>1700.00</td>
      <td>New York City (NY)</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>295666</td>
      <td>LG Washing Machine</td>
      <td>1</td>
      <td>600.00</td>
      <td>2019-12-29 07:03:00</td>
      <td>562 2nd St, New York City, NY 10001</td>
      <td>12</td>
      <td>600.00</td>
      <td>New York City (NY)</td>
      <td>7</td>
      <td>3</td>
    </tr>
    <tr>
      <th>2</th>
      <td>295667</td>
      <td>USB-C Charging Cable</td>
      <td>1</td>
      <td>11.95</td>
      <td>2019-12-12 18:21:00</td>
      <td>277 Main St, New York City, NY 10001</td>
      <td>12</td>
      <td>11.95</td>
      <td>New York City (NY)</td>
      <td>18</td>
      <td>21</td>
    </tr>
    <tr>
      <th>3</th>
      <td>295668</td>
      <td>27in FHD Monitor</td>
      <td>1</td>
      <td>149.99</td>
      <td>2019-12-22 15:13:00</td>
      <td>410 6th St, San Francisco, CA 94016</td>
      <td>12</td>
      <td>149.99</td>
      <td>San Francisco (CA)</td>
      <td>15</td>
      <td>13</td>
    </tr>
    <tr>
      <th>4</th>
      <td>295669</td>
      <td>USB-C Charging Cable</td>
      <td>1</td>
      <td>11.95</td>
      <td>2019-12-18 12:38:00</td>
      <td>43 Hill St, Atlanta, GA 30301</td>
      <td>12</td>
      <td>11.95</td>
      <td>Atlanta (GA)</td>
      <td>12</td>
      <td>38</td>
    </tr>
  </tbody>
</table>
</div>




```python
same_order = all_data[all_data['Order ID'].isin(all_data['Order ID'].value_counts()[all_data['Order ID'].value_counts()>2].index)]
```


```python
same_order.head()
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
      <th>Order ID</th>
      <th>Product</th>
      <th>Quantity Ordered</th>
      <th>Price Each</th>
      <th>Order Date</th>
      <th>Purchase Address</th>
      <th>Month</th>
      <th>Sales</th>
      <th>City</th>
      <th>Hour</th>
      <th>Minute</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>16</th>
      <td>295681</td>
      <td>Google Phone</td>
      <td>1</td>
      <td>600.00</td>
      <td>2019-12-25 12:37:00</td>
      <td>79 Elm St, Boston, MA 02215</td>
      <td>12</td>
      <td>600.00</td>
      <td>Boston (MA)</td>
      <td>12</td>
      <td>37</td>
    </tr>
    <tr>
      <th>17</th>
      <td>295681</td>
      <td>USB-C Charging Cable</td>
      <td>1</td>
      <td>11.95</td>
      <td>2019-12-25 12:37:00</td>
      <td>79 Elm St, Boston, MA 02215</td>
      <td>12</td>
      <td>11.95</td>
      <td>Boston (MA)</td>
      <td>12</td>
      <td>37</td>
    </tr>
    <tr>
      <th>18</th>
      <td>295681</td>
      <td>Bose SoundSport Headphones</td>
      <td>1</td>
      <td>99.99</td>
      <td>2019-12-25 12:37:00</td>
      <td>79 Elm St, Boston, MA 02215</td>
      <td>12</td>
      <td>99.99</td>
      <td>Boston (MA)</td>
      <td>12</td>
      <td>37</td>
    </tr>
    <tr>
      <th>19</th>
      <td>295681</td>
      <td>Wired Headphones</td>
      <td>1</td>
      <td>11.99</td>
      <td>2019-12-25 12:37:00</td>
      <td>79 Elm St, Boston, MA 02215</td>
      <td>12</td>
      <td>11.99</td>
      <td>Boston (MA)</td>
      <td>12</td>
      <td>37</td>
    </tr>
    <tr>
      <th>76</th>
      <td>295735</td>
      <td>iPhone</td>
      <td>1</td>
      <td>700.00</td>
      <td>2019-12-22 18:25:00</td>
      <td>374 Lincoln St, New York City, NY 10001</td>
      <td>12</td>
      <td>700.00</td>
      <td>New York City (NY)</td>
      <td>18</td>
      <td>25</td>
    </tr>
  </tbody>
</table>
</div>



 ##### Create a new column


```python
same_order['Grouped'] = same_order.groupby('Order ID')['Product'].transform(lambda x: ','.join(x))
same_order.head()


```

    /Users/davidkeya/.pyenv/versions/3.7.3/lib/python3.7/site-packages/ipykernel_launcher.py:1: SettingWithCopyWarning:
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead

    See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
      """Entry point for launching an IPython kernel.





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
      <th>Order ID</th>
      <th>Product</th>
      <th>Quantity Ordered</th>
      <th>Price Each</th>
      <th>Order Date</th>
      <th>Purchase Address</th>
      <th>Month</th>
      <th>Sales</th>
      <th>City</th>
      <th>Hour</th>
      <th>Minute</th>
      <th>Grouped</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>16</th>
      <td>295681</td>
      <td>Google Phone</td>
      <td>1</td>
      <td>600.00</td>
      <td>2019-12-25 12:37:00</td>
      <td>79 Elm St, Boston, MA 02215</td>
      <td>12</td>
      <td>600.00</td>
      <td>Boston (MA)</td>
      <td>12</td>
      <td>37</td>
      <td>Google Phone,USB-C Charging Cable,Bose SoundSp...</td>
    </tr>
    <tr>
      <th>17</th>
      <td>295681</td>
      <td>USB-C Charging Cable</td>
      <td>1</td>
      <td>11.95</td>
      <td>2019-12-25 12:37:00</td>
      <td>79 Elm St, Boston, MA 02215</td>
      <td>12</td>
      <td>11.95</td>
      <td>Boston (MA)</td>
      <td>12</td>
      <td>37</td>
      <td>Google Phone,USB-C Charging Cable,Bose SoundSp...</td>
    </tr>
    <tr>
      <th>18</th>
      <td>295681</td>
      <td>Bose SoundSport Headphones</td>
      <td>1</td>
      <td>99.99</td>
      <td>2019-12-25 12:37:00</td>
      <td>79 Elm St, Boston, MA 02215</td>
      <td>12</td>
      <td>99.99</td>
      <td>Boston (MA)</td>
      <td>12</td>
      <td>37</td>
      <td>Google Phone,USB-C Charging Cable,Bose SoundSp...</td>
    </tr>
    <tr>
      <th>19</th>
      <td>295681</td>
      <td>Wired Headphones</td>
      <td>1</td>
      <td>11.99</td>
      <td>2019-12-25 12:37:00</td>
      <td>79 Elm St, Boston, MA 02215</td>
      <td>12</td>
      <td>11.99</td>
      <td>Boston (MA)</td>
      <td>12</td>
      <td>37</td>
      <td>Google Phone,USB-C Charging Cable,Bose SoundSp...</td>
    </tr>
    <tr>
      <th>76</th>
      <td>295735</td>
      <td>iPhone</td>
      <td>1</td>
      <td>700.00</td>
      <td>2019-12-22 18:25:00</td>
      <td>374 Lincoln St, New York City, NY 10001</td>
      <td>12</td>
      <td>700.00</td>
      <td>New York City (NY)</td>
      <td>18</td>
      <td>25</td>
      <td>iPhone,Apple Airpods Headphones,Wired Headphones</td>
    </tr>
  </tbody>
</table>
</div>



##### Remove duplicates


```python
# Drop duplicates
same_order = same_order[['Order ID', 'Grouped']].drop_duplicates()
same_order.head()
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
      <th>Order ID</th>
      <th>Grouped</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>16</th>
      <td>295681</td>
      <td>Google Phone,USB-C Charging Cable,Bose SoundSp...</td>
    </tr>
    <tr>
      <th>76</th>
      <td>295735</td>
      <td>iPhone,Apple Airpods Headphones,Wired Headphones</td>
    </tr>
    <tr>
      <th>723</th>
      <td>296353</td>
      <td>iPhone,Lightning Charging Cable,Wired Headphon...</td>
    </tr>
    <tr>
      <th>1401</th>
      <td>296998</td>
      <td>Google Phone,USB-C Charging Cable,Wired Headph...</td>
    </tr>
    <tr>
      <th>1462</th>
      <td>297056</td>
      <td>iPhone,Apple Airpods Headphones,Wired Headphones</td>
    </tr>
  </tbody>
</table>
</div>



##### List of items commonly sold  together


```python
from itertools import combinations
from collections import Counter

count = Counter()
for row in same_order['Grouped']:
    row_list = row.split(',')
    count.update(Counter(combinations(row_list, 2)))


for key, value in count.most_common(10):
    print(key, value)

```

    ('Google Phone', 'USB-C Charging Cable') 131
    ('iPhone', 'Lightning Charging Cable') 123
    ('USB-C Charging Cable', 'Wired Headphones') 120
    ('Google Phone', 'Wired Headphones') 111
    ('iPhone', 'Wired Headphones') 86
    ('iPhone', 'Apple Airpods Headphones') 74
    ('Lightning Charging Cable', 'Wired Headphones') 62
    ('Google Phone', 'Bose SoundSport Headphones') 59
    ('USB-C Charging Cable', 'Bose SoundSport Headphones') 51
    ('Vareebadd Phone', 'USB-C Charging Cable') 49


> ##### This data will help make decisions on items to be for instance advertised together

#### What products sold the most and Why


```python
all_data.head()
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
      <th>Order ID</th>
      <th>Product</th>
      <th>Quantity Ordered</th>
      <th>Price Each</th>
      <th>Order Date</th>
      <th>Purchase Address</th>
      <th>Month</th>
      <th>Sales</th>
      <th>City</th>
      <th>Hour</th>
      <th>Minute</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>295665</td>
      <td>Macbook Pro Laptop</td>
      <td>1</td>
      <td>1700.00</td>
      <td>2019-12-30 00:01:00</td>
      <td>136 Church St, New York City, NY 10001</td>
      <td>12</td>
      <td>1700.00</td>
      <td>New York City (NY)</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>295666</td>
      <td>LG Washing Machine</td>
      <td>1</td>
      <td>600.00</td>
      <td>2019-12-29 07:03:00</td>
      <td>562 2nd St, New York City, NY 10001</td>
      <td>12</td>
      <td>600.00</td>
      <td>New York City (NY)</td>
      <td>7</td>
      <td>3</td>
    </tr>
    <tr>
      <th>2</th>
      <td>295667</td>
      <td>USB-C Charging Cable</td>
      <td>1</td>
      <td>11.95</td>
      <td>2019-12-12 18:21:00</td>
      <td>277 Main St, New York City, NY 10001</td>
      <td>12</td>
      <td>11.95</td>
      <td>New York City (NY)</td>
      <td>18</td>
      <td>21</td>
    </tr>
    <tr>
      <th>3</th>
      <td>295668</td>
      <td>27in FHD Monitor</td>
      <td>1</td>
      <td>149.99</td>
      <td>2019-12-22 15:13:00</td>
      <td>410 6th St, San Francisco, CA 94016</td>
      <td>12</td>
      <td>149.99</td>
      <td>San Francisco (CA)</td>
      <td>15</td>
      <td>13</td>
    </tr>
    <tr>
      <th>4</th>
      <td>295669</td>
      <td>USB-C Charging Cable</td>
      <td>1</td>
      <td>11.95</td>
      <td>2019-12-18 12:38:00</td>
      <td>43 Hill St, Atlanta, GA 30301</td>
      <td>12</td>
      <td>11.95</td>
      <td>Atlanta (GA)</td>
      <td>12</td>
      <td>38</td>
    </tr>
  </tbody>
</table>
</div>



##### Group products, sum of quatity for each product


```python
prod_quantity = all_data.groupby('Product')['Quantity Ordered'].sum()
prod_quantity

```




    Product
    20in Monitor                   4129
    27in 4K Gaming Monitor         6244
    27in FHD Monitor               7550
    34in Ultrawide Monitor         6199
    AA Batteries (4-pack)         27635
    AAA Batteries (4-pack)        31017
    Apple Airpods Headphones      15661
    Bose SoundSport Headphones    13457
    Flatscreen TV                  4819
    Google Phone                   5532
    LG Dryer                        646
    LG Washing Machine              666
    Lightning Charging Cable      23217
    Macbook Pro Laptop             4728
    ThinkPad Laptop                4130
    USB-C Charging Cable          23975
    Vareebadd Phone                2068
    Wired Headphones              20557
    iPhone                         6849
    Name: Quantity Ordered, dtype: int64



##### A visual of the most sold products


```python
prod_quantity.plot(kind='bar', figsize = (16, 8));
```


![png](assets/images/sales/output_69_0.png)


##### AAA Batteries sold the most, could be because they are cheap. To prove this hypothesis, the quantity sold will be overlayed by the mean price for each product


```python
all_data.head()
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
      <th>Order ID</th>
      <th>Product</th>
      <th>Quantity Ordered</th>
      <th>Price Each</th>
      <th>Order Date</th>
      <th>Purchase Address</th>
      <th>Month</th>
      <th>Sales</th>
      <th>City</th>
      <th>Hour</th>
      <th>Minute</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>295665</td>
      <td>Macbook Pro Laptop</td>
      <td>1</td>
      <td>1700.00</td>
      <td>2019-12-30 00:01:00</td>
      <td>136 Church St, New York City, NY 10001</td>
      <td>12</td>
      <td>1700.00</td>
      <td>New York City (NY)</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>295666</td>
      <td>LG Washing Machine</td>
      <td>1</td>
      <td>600.00</td>
      <td>2019-12-29 07:03:00</td>
      <td>562 2nd St, New York City, NY 10001</td>
      <td>12</td>
      <td>600.00</td>
      <td>New York City (NY)</td>
      <td>7</td>
      <td>3</td>
    </tr>
    <tr>
      <th>2</th>
      <td>295667</td>
      <td>USB-C Charging Cable</td>
      <td>1</td>
      <td>11.95</td>
      <td>2019-12-12 18:21:00</td>
      <td>277 Main St, New York City, NY 10001</td>
      <td>12</td>
      <td>11.95</td>
      <td>New York City (NY)</td>
      <td>18</td>
      <td>21</td>
    </tr>
    <tr>
      <th>3</th>
      <td>295668</td>
      <td>27in FHD Monitor</td>
      <td>1</td>
      <td>149.99</td>
      <td>2019-12-22 15:13:00</td>
      <td>410 6th St, San Francisco, CA 94016</td>
      <td>12</td>
      <td>149.99</td>
      <td>San Francisco (CA)</td>
      <td>15</td>
      <td>13</td>
    </tr>
    <tr>
      <th>4</th>
      <td>295669</td>
      <td>USB-C Charging Cable</td>
      <td>1</td>
      <td>11.95</td>
      <td>2019-12-18 12:38:00</td>
      <td>43 Hill St, Atlanta, GA 30301</td>
      <td>12</td>
      <td>11.95</td>
      <td>Atlanta (GA)</td>
      <td>12</td>
      <td>38</td>
    </tr>
  </tbody>
</table>
</div>




```python
prices = all_data.groupby('Product')['Price Each'].mean()

prices
```




    Product
    20in Monitor                   109.99
    27in 4K Gaming Monitor         389.99
    27in FHD Monitor               149.99
    34in Ultrawide Monitor         379.99
    AA Batteries (4-pack)            3.84
    AAA Batteries (4-pack)           2.99
    Apple Airpods Headphones       150.00
    Bose SoundSport Headphones      99.99
    Flatscreen TV                  300.00
    Google Phone                   600.00
    LG Dryer                       600.00
    LG Washing Machine             600.00
    Lightning Charging Cable        14.95
    Macbook Pro Laptop            1700.00
    ThinkPad Laptop                999.99
    USB-C Charging Cable            11.95
    Vareebadd Phone                400.00
    Wired Headphones                11.99
    iPhone                         700.00
    Name: Price Each, dtype: float64



##### Combine Product Quantity and Prices  into a DataFrame


```python
df = pd.concat([prod_quantity, prices], axis=1)

df.head()
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
      <th>Quantity Ordered</th>
      <th>Price Each</th>
    </tr>
    <tr>
      <th>Product</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>20in Monitor</th>
      <td>4129</td>
      <td>109.99</td>
    </tr>
    <tr>
      <th>27in 4K Gaming Monitor</th>
      <td>6244</td>
      <td>389.99</td>
    </tr>
    <tr>
      <th>27in FHD Monitor</th>
      <td>7550</td>
      <td>149.99</td>
    </tr>
    <tr>
      <th>34in Ultrawide Monitor</th>
      <td>6199</td>
      <td>379.99</td>
    </tr>
    <tr>
      <th>AA Batteries (4-pack)</th>
      <td>27635</td>
      <td>3.84</td>
    </tr>
  </tbody>
</table>
</div>




```python
import matplotlib.pyplot as plt
ax = df[['Quantity Ordered']].plot(kind='bar', figsize=(16, 8), use_index=True)
ax2 = ax.twinx()
ax2.plot(ax.get_xticks(),df[['Price Each']].values, linestyle='-', marker='o', linewidth=2.0, color='orange')
plt.show()
```


![png](/assets/images/sales/output_75_0.png)
> ##### _From the plot, generally cheaper products have a high sales quantity for instance the AAA batteries sold the most because most customer could afford._
