---
header:
  overlay_image: /assets/images/loan/loan_corr.png
  #caption: "Photo credit: [**Alexander Mils**](https://unsplash.com)"
permalink: /portfolio/Loan_Modelling/
date: 2020-05-25
toc: true
toc_label: "Contents"
---

# Model Selection
```python
import pandas as pd
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt
plt.style.use('fivethirtyeight')
%matplotlib inline
# Increase default figure and font sizes for easier viewing.
plt.rcParams['figure.figsize'] = (8, 6)
plt.rcParams['font.size'] = 14
```

# Logistic Regression
The data set has been prepared to be fed into a machine learning algorithm. Feature columns selection is necessary for the Logistic Regression Model


```python
# load loan data frame
loan = pd.read_csv('result1.csv', index_col=0)
```


```python
loan.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>loan_amnt</th>
      <th>term</th>
      <th>installment</th>
      <th>grade</th>
      <th>emp_length</th>
      <th>annual_inc</th>
      <th>loan_status</th>
      <th>dti</th>
      <th>delinq_2yrs</th>
      <th>inq_last_6mths</th>
      <th>...</th>
      <th>total_rev_hi_lim</th>
      <th>home_ownership_ANY</th>
      <th>home_ownership_MORTGAGE</th>
      <th>home_ownership_NONE</th>
      <th>home_ownership_OTHER</th>
      <th>home_ownership_OWN</th>
      <th>home_ownership_RENT</th>
      <th>verification_status_Not Verified</th>
      <th>verification_status_Source Verified</th>
      <th>verification_status_Verified</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>5000.0</td>
      <td>36.0</td>
      <td>162.87</td>
      <td>2</td>
      <td>10.0</td>
      <td>24000.0</td>
      <td>1</td>
      <td>27.65</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>...</td>
      <td>23700.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2500.0</td>
      <td>60.0</td>
      <td>59.83</td>
      <td>3</td>
      <td>1.0</td>
      <td>30000.0</td>
      <td>0</td>
      <td>1.00</td>
      <td>0.0</td>
      <td>5.0</td>
      <td>...</td>
      <td>23700.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2400.0</td>
      <td>36.0</td>
      <td>84.33</td>
      <td>3</td>
      <td>10.0</td>
      <td>12252.0</td>
      <td>1</td>
      <td>8.72</td>
      <td>0.0</td>
      <td>2.0</td>
      <td>...</td>
      <td>23700.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>10000.0</td>
      <td>36.0</td>
      <td>339.31</td>
      <td>3</td>
      <td>10.0</td>
      <td>49200.0</td>
      <td>1</td>
      <td>20.00</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>...</td>
      <td>23700.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5000.0</td>
      <td>36.0</td>
      <td>156.46</td>
      <td>1</td>
      <td>3.0</td>
      <td>36000.0</td>
      <td>1</td>
      <td>11.20</td>
      <td>0.0</td>
      <td>3.0</td>
      <td>...</td>
      <td>23700.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 30 columns</p>
</div>




```python
# Index of columns
loan.columns
```




    Index([u'loan_amnt', u'term', u'installment', u'grade', u'emp_length',
           u'annual_inc', u'loan_status', u'dti', u'delinq_2yrs',
           u'inq_last_6mths', u'open_acc', u'pub_rec', u'revol_bal', u'revol_util',
           u'total_acc', u'initial_list_status', u'last_pymnt_amnt',
           u'collections_12_mths_ex_med', u'tot_coll_amt', u'tot_cur_bal',
           u'total_rev_hi_lim', u'home_ownership_ANY', u'home_ownership_MORTGAGE',
           u'home_ownership_NONE', u'home_ownership_OTHER', u'home_ownership_OWN',
           u'home_ownership_RENT', u'verification_status_Not Verified',
           u'verification_status_Source Verified',
           u'verification_status_Verified'],
          dtype='object')




```python
# create feature matrix (X)
feature_cols = loan.columns.drop(['loan_status', 'dti', 'inq_last_6mths', 'pub_rec', 'revol_util',
                                 'collections_12_mths_ex_med', 'total_rev_hi_lim', 'home_ownership_ANY',
                                  'delinq_2yrs'])
X = loan[feature_cols]

# create response vector (y)
y = loan.loan_status

```


```python
# feature columnss
X.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>loan_amnt</th>
      <th>term</th>
      <th>installment</th>
      <th>grade</th>
      <th>emp_length</th>
      <th>annual_inc</th>
      <th>open_acc</th>
      <th>revol_bal</th>
      <th>total_acc</th>
      <th>initial_list_status</th>
      <th>...</th>
      <th>tot_coll_amt</th>
      <th>tot_cur_bal</th>
      <th>home_ownership_MORTGAGE</th>
      <th>home_ownership_NONE</th>
      <th>home_ownership_OTHER</th>
      <th>home_ownership_OWN</th>
      <th>home_ownership_RENT</th>
      <th>verification_status_Not Verified</th>
      <th>verification_status_Source Verified</th>
      <th>verification_status_Verified</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>5000.0</td>
      <td>36.0</td>
      <td>162.87</td>
      <td>2</td>
      <td>10.0</td>
      <td>24000.0</td>
      <td>3.0</td>
      <td>13648.0</td>
      <td>9.0</td>
      <td>1</td>
      <td>...</td>
      <td>0.0</td>
      <td>80559.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2500.0</td>
      <td>60.0</td>
      <td>59.83</td>
      <td>3</td>
      <td>1.0</td>
      <td>30000.0</td>
      <td>3.0</td>
      <td>1687.0</td>
      <td>4.0</td>
      <td>1</td>
      <td>...</td>
      <td>0.0</td>
      <td>80559.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2400.0</td>
      <td>36.0</td>
      <td>84.33</td>
      <td>3</td>
      <td>10.0</td>
      <td>12252.0</td>
      <td>2.0</td>
      <td>2956.0</td>
      <td>10.0</td>
      <td>1</td>
      <td>...</td>
      <td>0.0</td>
      <td>80559.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>10000.0</td>
      <td>36.0</td>
      <td>339.31</td>
      <td>3</td>
      <td>10.0</td>
      <td>49200.0</td>
      <td>10.0</td>
      <td>5598.0</td>
      <td>37.0</td>
      <td>1</td>
      <td>...</td>
      <td>0.0</td>
      <td>80559.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5000.0</td>
      <td>36.0</td>
      <td>156.46</td>
      <td>1</td>
      <td>3.0</td>
      <td>36000.0</td>
      <td>9.0</td>
      <td>7963.0</td>
      <td>12.0</td>
      <td>1</td>
      <td>...</td>
      <td>0.0</td>
      <td>80559.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 21 columns</p>
</div>




```python
y.sample(5)
```




    313868    0
    872067    1
    867047    1
    810490    1
    677152    1
    Name: loan_status, dtype: int64




```python
# Split X and y into training and testing sets
from sklearn.cross_validation import train_test_split
X_train, X_test, y_train, y_test = train_test_split(X,y, test_size=0.4, random_state=99)
```

    /Users/davidkeya/anaconda2/lib/python2.7/site-packages/sklearn/cross_validation.py:41: DeprecationWarning: This module was deprecated in version 0.18 in favor of the model_selection module into which all the refactored classes and functions are moved. Also note that the interface of the new CV iterators are different from that of this module. This module will be removed in 0.20.
      "This module will be removed in 0.20.", DeprecationWarning)



```python
# Shape of the new X objects
print X_train.shape
print X_test.shape
```

    (153401, 21)
    (102268, 21)



```python
# Shape of the new y response
print y_train.shape
print y_test.shape
```

    (153401,)
    (102268,)



```python
# Train the model on the training set
from sklearn.linear_model import LogisticRegression
logreg = LogisticRegression()
logreg.fit(X_train, y_train)
```




    LogisticRegression(C=1.0, class_weight=None, dual=False, fit_intercept=True,
              intercept_scaling=1, max_iter=100, multi_class='ovr', n_jobs=1,
              penalty='l2', random_state=None, solver='liblinear', tol=0.0001,
              verbose=0, warm_start=False)




```python
# Making predictions on the testing set
y_pred = logreg.predict(X_test)
```


```python
# Comparing actual response values of y_test and the predicted values y_pred
from sklearn import metrics
print metrics.accuracy_score(y_test, y_pred)
```

    0.852524738921


 ### Logistic Regression Testing Accuracy
 - **After making predictions on the testing set, the model achieves a testing accuracy of 85.2% is achieved.**


```python

```

## KNN Classification
Use KNN with K=5


```python
from sklearn.neighbors import KNeighborsClassifier
```


```python
# Calculating the accuracy score
knn = KNeighborsClassifier(n_neighbors=5)
knn.fit(X_train, y_train)
yk_pred = knn.predict(X_test)
print metrics.accuracy_score(y_test, yk_pred)
```

    0.851204677905


### Determining a better value of K
**Testing accuracy** worked out for k ranging from 1 to 20


```python
# Testing accuracy for k ranging from 1 to 20
k_range = range(1, 20)
scores = []
for k in k_range:
    knn = KNeighborsClassifier(n_neighbors=k)
    knn.fit(X_train, y_train)
    y_pred = knn.predict(X_test)
    scores.append(metrics.accuracy_score(y_test, y_pred))
```


```python
# Create a DataFrame of K and scores
column_dict = {'K':k_range, 'accuracy score':scores}
df = pd.DataFrame(column_dict).set_index('K')
df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>accuracy score</th>
    </tr>
    <tr>
      <th>K</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>0.831570</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.813607</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0.844546</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0.838728</td>
    </tr>
    <tr>
      <th>5</th>
      <td>0.851205</td>
    </tr>
    <tr>
      <th>6</th>
      <td>0.849855</td>
    </tr>
    <tr>
      <th>7</th>
      <td>0.855820</td>
    </tr>
    <tr>
      <th>8</th>
      <td>0.855243</td>
    </tr>
    <tr>
      <th>9</th>
      <td>0.858793</td>
    </tr>
    <tr>
      <th>10</th>
      <td>0.858607</td>
    </tr>
    <tr>
      <th>11</th>
      <td>0.860093</td>
    </tr>
    <tr>
      <th>12</th>
      <td>0.861042</td>
    </tr>
    <tr>
      <th>13</th>
      <td>0.860748</td>
    </tr>
    <tr>
      <th>14</th>
      <td>0.861804</td>
    </tr>
    <tr>
      <th>15</th>
      <td>0.861354</td>
    </tr>
    <tr>
      <th>16</th>
      <td>0.861990</td>
    </tr>
    <tr>
      <th>17</th>
      <td>0.860934</td>
    </tr>
    <tr>
      <th>18</th>
      <td>0.861892</td>
    </tr>
    <tr>
      <th>19</th>
      <td>0.861022</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Plot the relationship between K and Accuracy score.
df.plot(y='accuracy score');
plt.xlabel('Value of K for KNN');
plt.ylabel('Accuracy Score');
```


![png](/assets/images/loan/output_23_0.png)



```python
# Find the maximum accuracy score and the associated K value.
df.sort_values('accuracy score').head().sort_index(ascending=False)
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>accuracy score</th>
    </tr>
    <tr>
      <th>K</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>6</th>
      <td>0.849855</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0.838728</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0.844546</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.813607</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.831570</td>
    </tr>
  </tbody>
</table>
</div>



## Conclusion
- **When using KNN on this data set with the selected features, the best value for K at 16 and 18**
- **The model achieves a testing accuracy of 82.3%**


```python

```

# Classification Using Decision Trees
This method classifies a population into branch-like segments that construct an inverted tree with a root node, internal nodes, and leaf nodes. The algorithm is non-parametric and can efficiently deal with large, complicated datasets without imposing a complicated parametric structure.

 **Building a classification tree using the Loan data set**
- First find the best max_depth for the decision tree using cross validation


```python
from sklearn.tree import DecisionTreeClassifier
# List of values to try for max_depth:
max_depth_range = list(range(1, 10))

# Store the average RMSE for each value of max_depth in the list
RMSE_scores = []

#10-fold cross-validation with each value of max_depth used.
from sklearn.model_selection import cross_val_score
for depth in max_depth_range:
    treereg = DecisionTreeClassifier(max_depth=depth, random_state=1)
    MSE_scores = cross_val_score(treereg, X, y, cv=10, scoring='neg_mean_squared_error')
    RMSE_scores.append(np.mean(np.sqrt(-MSE_scores)))

```


```python
# Plot max_depth (x-axis) versus RMSE (y-axis).
plt.plot(max_depth_range, RMSE_scores);
plt.xlabel('max_depth');
plt.ylabel('RMSE ');
```


![png](/assets/images/loan/output_30_0.png)


- ** A lower RMSE is better**
- ** From the above plot Max dept of around 8 has the least RMSE score**
- ** Fit the tree with max_depth=8**


```python
# Fit a classification tree with max_depth=8 on all data.
treeclf = DecisionTreeClassifier(max_depth=8, random_state=99)
treeclf.fit(X, y)
```




    DecisionTreeClassifier(class_weight=None, criterion='gini', max_depth=8,
                max_features=None, max_leaf_nodes=None,
                min_impurity_decrease=0.0, min_impurity_split=None,
                min_samples_leaf=1, min_samples_split=2,
                min_weight_fraction_leaf=0.0, presort=False, random_state=99,
                splitter='best')




```python
# Compute feature importances.
pd.DataFrame({'feature':feature_cols, 'importance':treeclf.feature_importances_}).sort_values(by='importance',
                                                                                              ascending=False)
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>feature</th>
      <th>importance</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>10</th>
      <td>last_pymnt_amnt</td>
      <td>0.662615</td>
    </tr>
    <tr>
      <th>1</th>
      <td>term</td>
      <td>0.132081</td>
    </tr>
    <tr>
      <th>12</th>
      <td>tot_cur_bal</td>
      <td>0.103070</td>
    </tr>
    <tr>
      <th>2</th>
      <td>installment</td>
      <td>0.052520</td>
    </tr>
    <tr>
      <th>3</th>
      <td>grade</td>
      <td>0.041712</td>
    </tr>
    <tr>
      <th>0</th>
      <td>loan_amnt</td>
      <td>0.005031</td>
    </tr>
    <tr>
      <th>5</th>
      <td>annual_inc</td>
      <td>0.000835</td>
    </tr>
    <tr>
      <th>9</th>
      <td>initial_list_status</td>
      <td>0.000756</td>
    </tr>
    <tr>
      <th>7</th>
      <td>revol_bal</td>
      <td>0.000710</td>
    </tr>
    <tr>
      <th>6</th>
      <td>open_acc</td>
      <td>0.000262</td>
    </tr>
    <tr>
      <th>11</th>
      <td>tot_coll_amt</td>
      <td>0.000106</td>
    </tr>
    <tr>
      <th>8</th>
      <td>total_acc</td>
      <td>0.000080</td>
    </tr>
    <tr>
      <th>13</th>
      <td>home_ownership_MORTGAGE</td>
      <td>0.000078</td>
    </tr>
    <tr>
      <th>17</th>
      <td>home_ownership_RENT</td>
      <td>0.000066</td>
    </tr>
    <tr>
      <th>20</th>
      <td>verification_status_Verified</td>
      <td>0.000053</td>
    </tr>
    <tr>
      <th>4</th>
      <td>emp_length</td>
      <td>0.000024</td>
    </tr>
    <tr>
      <th>19</th>
      <td>verification_status_Source Verified</td>
      <td>0.000002</td>
    </tr>
    <tr>
      <th>14</th>
      <td>home_ownership_NONE</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>15</th>
      <td>home_ownership_OTHER</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>16</th>
      <td>home_ownership_OWN</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>18</th>
      <td>verification_status_Not Verified</td>
      <td>0.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python

```


```python
# Create a Graphviz file.
from sklearn.tree import export_graphviz
export_graphviz(treeclf, out_file='./tree_loan.dot', feature_names=feature_cols)
```


```python

```


```python

```
