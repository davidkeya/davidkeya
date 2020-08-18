---
header:
  overlay_image: /assets/images/loan/money.jpg
  caption: "Photo credit: [**Alexander Mils**](https://unsplash.com)"
permalink: /portfolio/Loan_Eda/
date: 2020-05-25
toc: true
toc_label: "Contents"
---

# An Exploratory Data Analysis on Predicting Loan Status

## Data Source
This data science problem uses a data set from Lending Club marketplace. The marketplace is a platform for personal loans that marches borrowers who are seeking a loan with investors seeking to lend money and make a return.

## Summary
A borrower is required to fill out an application, providing their past financial history. Comprehensive evaluation is made on each borrower's credit score using past historical data and an interest rate is assigned to to the borrower. Approved loans are listed on the Lending Club website, where qualified investors can browse recently approved loans, the borrower's credit score, the purpose for the loan, and other information from the application. Once an investor decides to fund a loan, the borrower then makes monthly payments back to Lending Club. Lending Club redistributes these payments to the investors.
An investor requires a machine learning model that reliably predict if a loan will be paid off or not. The model should effectively filter out the percentage of loan defaulters.
The file containing loan data through the "present" contains complete loan data for all loans issued through the previous completed calendar quarter.
## Goal
The aim of this data science project is to develop a machine learning model that reliably predict if a loan will be paid off or not.
## Description of Data Analysis Tools
Exploratory data analysis, modeling (using machine learning), tools will be useful in process of making an accurate prediction.
- Looping concepts in Python
- Machine learning libraries in Python
- Python NumPy Library
- Python Pandas Library
- Python Matplotlib Library
- Seaborn

## Data Source and description
The dataset for this project has been sourced from [kaggle.com](https://www.kaggle.com/wendykan/lending-club-loan-data/data)
The dataset contains about 890 thousand observations and 74 variables, with a data dictionary provided in a separate file.
Features include credit scores, number of finance inquiries, address including zip codes, and state, and collections among others.

Loan_status is the outcome variable, while possible feature variables include  the following:
1. **addr_state**	The state provided by the borrower in the loan application
2. **annual_inc**	The self-reported annual income provided by the borrower during registration.
3. **annual_inc_joint**	The combined self-reported annual income provided by the co-borrowers during registration
4. **application_type**	Indicates whether the loan is an individual application or a joint application with two co-borrowers
5. **collection_recovery_fee**	post charge off collection fee
6. **collections_12_mths_ex_med**	Number of collections in 12 months excluding medical collections
7. **delinq_2yrs**	The number of 30+ days past-due incidences of delinquency in the borrower's credit file for the past 2 years
8. **desc**	Loan description provided by the borrower
9. **dti**	A ratio calculated using the borrower’s total monthly debt payments on the total debt obligations, excluding mortgage and the requested LC loan, divided by the borrower’s self-reported monthly income.
10. **dti_joint**	A ratio calculated using the co-borrowers' total monthly payments on the total debt obligations, excluding mortgages and the requested LC loan, divided by the co-borrowers' combined self-reported monthly income
11. **earliest_cr_line**	The month the borrower's earliest reported credit line was opened
12. **emp_length**	Employment length in years. Possible values are between 0 and 10 where 0 means less than one year and 10 means ten or more years.
13. **emp_title**	The job title supplied by the Borrower when applying for the loan.*
14. **fico_range_high**	The upper boundary range the borrower’s FICO at loan origination belongs to.
15. **fico_range_low**	The lower boundary range the borrower’s FICO at loan origination belongs to.
16. **funded_amnt**	The total amount committed to that loan at that point in time.
17. **funded_amnt_inv**	The total amount committed by investors for that loan at that point in time.
18. **grade**	LC assigned loan grade
19. **home_ownership**	The home ownership status provided by the borrower during registration. Our values are: RENT, OWN, MORTGAGE, OTHER.
20. **id**	A unique LC assigned ID for the loan listing.
21. **initial_list_status**	The initial listing status of the loan. Possible values are – W, F
22. **inq_last_6mths**	The number of inquiries in past 6 months (excluding auto and mortgage inquiries)
23. **installment**	The monthly payment owed by the borrower if the loan originates.
24. **int_rate**	Interest Rate on the loan
25. **is_inc_v**	Indicates if income was verified by LC, not verified, or if the income source was verified
26. **issue_d**	The month which the loan was funded
27. **last_credit_pull_d**	The most recent month LC pulled credit for this loan
28. **last_fico_range_high**	The upper boundary range the borrower’s last FICO pulled belongs to.
29. **last_fico_range_low**	The lower boundary range the borrower’s last FICO pulled belongs to.
30. **last_pymnt_amnt**	Last total payment amount received
31. **last_pymnt_d**	Last month payment was received
32. **loan_amnt**	The listed amount of the loan applied for by the borrower. If at some point in time, the credit department reduces the loan amount, then it will be reflected in this value.
33. **loan_status**	Current status of the loan
34. **member_id**	A unique LC assigned Id for the borrower member.
35. **mths_since_last_delinq**	The number of months since the borrower's last delinquency.
36. **mths_since_last_major_derog**	Months since most recent 90-day or worse rating
37. **mths_since_last_record**	The number of months since the last public record.
38. **next_pymnt_d**	Next scheduled payment date
39. **open_acc**	The number of open credit lines in the borrower's credit file.
40. **out_prncp**	Remaining outstanding principal for total amount funded
41. **out_prncp_inv**	Remaining outstanding principal for portion of total amount funded by investors
42. **policy_code**	publicly available policy_code=1 new products not publicly available policy_code=2
43. **pub_rec**	Number of derogatory public records
44. **purpose**	A category provided by the borrower for the loan request.
45. **pymnt_plan**	Indicates if a payment plan has been put in place for the loan
recoveries	post charge off gross recovery
46. **revol_bal**	Total credit revolving balance
47. **revol_util**	Revolving line utilization rate, or the amount of credit the borrower is using relative to all available revolving credit.
48. **sub_grade**	LC assigned loan subgrade
49. **term**	The number of payments on the loan. Values are in months and can be either 36 or 60.
50. **title**	The loan title provided by the borrower
51. **total_acc**	The total number of credit lines currently in the borrower's credit file
52. **total_pymnt**	Payments received to date for total amount funded
53. **total_pymnt_inv**	Payments received to date for portion of total amount funded by investors
54. **total_rec_int**	Interest received to date
55. **total_rec_late_fee**	Late fees received to date
56. **total_rec_prncp**	Principal received to date
57. **url**	URL for the LC page with listing data.
58. **verified_status_joint**	Indicates if the co-borrowers' joint income was verified by LC, not verified, or if the income source was verified
59. **zip_code**	The first 3 numbers of the zip code provided by the borrower in the loan application.
60. **open_acc_6m**	Number of open trades in last 6 months
61. **open_il_6m**	Number of currently active installment trades
62. **open_il_12m**	Number of installment accounts opened in past 12 months
63. **open_il_24m**	Number of installment accounts opened in past 24 months
64. **mths_since_rcnt_il**	Months since most recent installment accounts opened
65. **total_bal_il**	Total current balance of all installment accounts
66. **il_util**	Ratio of total current balance to high credit/credit limit on all install acct
67. **open_rv_12m**	Number of revolving trades opened in past 12 months
68. **open_rv_24m**	Number of revolving trades opened in past 24 months
69. **max_bal_bc**	Maximum current balance owed on all revolving accounts
70. **all_util**	Balance to credit limit on all trades
71. **total_rev_hi_lim**  	Total revolving high credit/credit limit
72. **inq_fi**	Number of personal finance inquiries
73. **total_cu_tl**	Number of finance trades
74. **inq_last_12m**	Number of credit inquiries in past 12 months
75. **acc_now_delinq**	The number of accounts on which the borrower is now delinquent.
76. **tot_coll_amt**	Total collection amounts ever owed
77. **tot_cur_bal**	Total current balance of all accounts

The approved loans dataset contains information on current loans, completed loans, and defaulted loans. For this project, I worked with approved loans.
Before any exploratory analysis the assumption is that the data has the necessary structure to reveal the, necessary patterns in the data,



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


```python
loan = pd.read_csv('loan.csv', low_memory=False)
```


```python
loan.shape
```




    (887379, 74)




```python
loan.head() # Print the first 5 rows.
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
      <th>id</th>
      <th>member_id</th>
      <th>loan_amnt</th>
      <th>funded_amnt</th>
      <th>funded_amnt_inv</th>
      <th>term</th>
      <th>int_rate</th>
      <th>installment</th>
      <th>grade</th>
      <th>sub_grade</th>
      <th>...</th>
      <th>total_bal_il</th>
      <th>il_util</th>
      <th>open_rv_12m</th>
      <th>open_rv_24m</th>
      <th>max_bal_bc</th>
      <th>all_util</th>
      <th>total_rev_hi_lim</th>
      <th>inq_fi</th>
      <th>total_cu_tl</th>
      <th>inq_last_12m</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1077501</td>
      <td>1296599</td>
      <td>5000.0</td>
      <td>5000.0</td>
      <td>4975.0</td>
      <td>36 months</td>
      <td>10.65</td>
      <td>162.87</td>
      <td>B</td>
      <td>B2</td>
      <td>...</td>
      <td>NaN</td>
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
      <th>1</th>
      <td>1077430</td>
      <td>1314167</td>
      <td>2500.0</td>
      <td>2500.0</td>
      <td>2500.0</td>
      <td>60 months</td>
      <td>15.27</td>
      <td>59.83</td>
      <td>C</td>
      <td>C4</td>
      <td>...</td>
      <td>NaN</td>
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
      <th>2</th>
      <td>1077175</td>
      <td>1313524</td>
      <td>2400.0</td>
      <td>2400.0</td>
      <td>2400.0</td>
      <td>36 months</td>
      <td>15.96</td>
      <td>84.33</td>
      <td>C</td>
      <td>C5</td>
      <td>...</td>
      <td>NaN</td>
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
      <th>3</th>
      <td>1076863</td>
      <td>1277178</td>
      <td>10000.0</td>
      <td>10000.0</td>
      <td>10000.0</td>
      <td>36 months</td>
      <td>13.49</td>
      <td>339.31</td>
      <td>C</td>
      <td>C1</td>
      <td>...</td>
      <td>NaN</td>
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
      <th>4</th>
      <td>1075358</td>
      <td>1311748</td>
      <td>3000.0</td>
      <td>3000.0</td>
      <td>3000.0</td>
      <td>60 months</td>
      <td>12.69</td>
      <td>67.79</td>
      <td>B</td>
      <td>B5</td>
      <td>...</td>
      <td>NaN</td>
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
<p>5 rows × 74 columns</p>
</div>




```python
loan.tail() # Print the last 5 rows.
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
      <th>id</th>
      <th>member_id</th>
      <th>loan_amnt</th>
      <th>funded_amnt</th>
      <th>funded_amnt_inv</th>
      <th>term</th>
      <th>int_rate</th>
      <th>installment</th>
      <th>grade</th>
      <th>sub_grade</th>
      <th>...</th>
      <th>total_bal_il</th>
      <th>il_util</th>
      <th>open_rv_12m</th>
      <th>open_rv_24m</th>
      <th>max_bal_bc</th>
      <th>all_util</th>
      <th>total_rev_hi_lim</th>
      <th>inq_fi</th>
      <th>total_cu_tl</th>
      <th>inq_last_12m</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>887374</th>
      <td>36371250</td>
      <td>39102635</td>
      <td>10000.0</td>
      <td>10000.0</td>
      <td>10000.0</td>
      <td>36 months</td>
      <td>11.99</td>
      <td>332.10</td>
      <td>B</td>
      <td>B5</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>17100.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>887375</th>
      <td>36441262</td>
      <td>39152692</td>
      <td>24000.0</td>
      <td>24000.0</td>
      <td>24000.0</td>
      <td>36 months</td>
      <td>11.99</td>
      <td>797.03</td>
      <td>B</td>
      <td>B5</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>10200.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>887376</th>
      <td>36271333</td>
      <td>38982739</td>
      <td>13000.0</td>
      <td>13000.0</td>
      <td>13000.0</td>
      <td>60 months</td>
      <td>15.99</td>
      <td>316.07</td>
      <td>D</td>
      <td>D2</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>18000.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>887377</th>
      <td>36490806</td>
      <td>39222577</td>
      <td>12000.0</td>
      <td>12000.0</td>
      <td>12000.0</td>
      <td>60 months</td>
      <td>19.99</td>
      <td>317.86</td>
      <td>E</td>
      <td>E3</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>27000.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>887378</th>
      <td>36271262</td>
      <td>38982659</td>
      <td>20000.0</td>
      <td>20000.0</td>
      <td>20000.0</td>
      <td>36 months</td>
      <td>11.99</td>
      <td>664.20</td>
      <td>B</td>
      <td>B5</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>41700.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 74 columns</p>
</div>




```python
loan.info() #summary (including memory usage) — useful to quickly see if nulls exist
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 887379 entries, 0 to 887378
    Data columns (total 74 columns):
    id                             887379 non-null int64
    member_id                      887379 non-null int64
    loan_amnt                      887379 non-null float64
    funded_amnt                    887379 non-null float64
    funded_amnt_inv                887379 non-null float64
    term                           887379 non-null object
    int_rate                       887379 non-null float64
    installment                    887379 non-null float64
    grade                          887379 non-null object
    sub_grade                      887379 non-null object
    emp_title                      835922 non-null object
    emp_length                     887379 non-null object
    home_ownership                 887379 non-null object
    annual_inc                     887375 non-null float64
    verification_status            887379 non-null object
    issue_d                        887379 non-null object
    loan_status                    887379 non-null object
    pymnt_plan                     887379 non-null object
    url                            887379 non-null object
    desc                           126029 non-null object
    purpose                        887379 non-null object
    title                          887228 non-null object
    zip_code                       887379 non-null object
    addr_state                     887379 non-null object
    dti                            887379 non-null float64
    delinq_2yrs                    887350 non-null float64
    earliest_cr_line               887350 non-null object
    inq_last_6mths                 887350 non-null float64
    mths_since_last_delinq         433067 non-null float64
    mths_since_last_record         137053 non-null float64
    open_acc                       887350 non-null float64
    pub_rec                        887350 non-null float64
    revol_bal                      887379 non-null float64
    revol_util                     886877 non-null float64
    total_acc                      887350 non-null float64
    initial_list_status            887379 non-null object
    out_prncp                      887379 non-null float64
    out_prncp_inv                  887379 non-null float64
    total_pymnt                    887379 non-null float64
    total_pymnt_inv                887379 non-null float64
    total_rec_prncp                887379 non-null float64
    total_rec_int                  887379 non-null float64
    total_rec_late_fee             887379 non-null float64
    recoveries                     887379 non-null float64
    collection_recovery_fee        887379 non-null float64
    last_pymnt_d                   869720 non-null object
    last_pymnt_amnt                887379 non-null float64
    next_pymnt_d                   634408 non-null object
    last_credit_pull_d             887326 non-null object
    collections_12_mths_ex_med     887234 non-null float64
    mths_since_last_major_derog    221703 non-null float64
    policy_code                    887379 non-null float64
    application_type               887379 non-null object
    annual_inc_joint               511 non-null float64
    dti_joint                      509 non-null float64
    verification_status_joint      511 non-null object
    acc_now_delinq                 887350 non-null float64
    tot_coll_amt                   817103 non-null float64
    tot_cur_bal                    817103 non-null float64
    open_acc_6m                    21372 non-null float64
    open_il_6m                     21372 non-null float64
    open_il_12m                    21372 non-null float64
    open_il_24m                    21372 non-null float64
    mths_since_rcnt_il             20810 non-null float64
    total_bal_il                   21372 non-null float64
    il_util                        18617 non-null float64
    open_rv_12m                    21372 non-null float64
    open_rv_24m                    21372 non-null float64
    max_bal_bc                     21372 non-null float64
    all_util                       21372 non-null float64
    total_rev_hi_lim               817103 non-null float64
    inq_fi                         21372 non-null float64
    total_cu_tl                    21372 non-null float64
    inq_last_12m                   21372 non-null float64
    dtypes: float64(49), int64(2), object(23)
    memory usage: 501.0+ MB



```python
loan.index #"the row labels"
```




    RangeIndex(start=0, stop=887379, step=1)




```python
# Column names
loan.columns
```




    Index([u'id', u'member_id', u'loan_amnt', u'funded_amnt', u'funded_amnt_inv',
           u'term', u'int_rate', u'installment', u'grade', u'sub_grade',
           u'emp_title', u'emp_length', u'home_ownership', u'annual_inc',
           u'verification_status', u'issue_d', u'loan_status', u'pymnt_plan',
           u'url', u'desc', u'purpose', u'title', u'zip_code', u'addr_state',
           u'dti', u'delinq_2yrs', u'earliest_cr_line', u'inq_last_6mths',
           u'mths_since_last_delinq', u'mths_since_last_record', u'open_acc',
           u'pub_rec', u'revol_bal', u'revol_util', u'total_acc',
           u'initial_list_status', u'out_prncp', u'out_prncp_inv', u'total_pymnt',
           u'total_pymnt_inv', u'total_rec_prncp', u'total_rec_int',
           u'total_rec_late_fee', u'recoveries', u'collection_recovery_fee',
           u'last_pymnt_d', u'last_pymnt_amnt', u'next_pymnt_d',
           u'last_credit_pull_d', u'collections_12_mths_ex_med',
           u'mths_since_last_major_derog', u'policy_code', u'application_type',
           u'annual_inc_joint', u'dti_joint', u'verification_status_joint',
           u'acc_now_delinq', u'tot_coll_amt', u'tot_cur_bal', u'open_acc_6m',
           u'open_il_6m', u'open_il_12m', u'open_il_24m', u'mths_since_rcnt_il',
           u'total_bal_il', u'il_util', u'open_rv_12m', u'open_rv_24m',
           u'max_bal_bc', u'all_util', u'total_rev_hi_lim', u'inq_fi',
           u'total_cu_tl', u'inq_last_12m'],
          dtype='object')




```python
# Datatypes of each column
loan.dtypes
```




    id                               int64
    member_id                        int64
    loan_amnt                      float64
    funded_amnt                    float64
    funded_amnt_inv                float64
    term                            object
    int_rate                       float64
    installment                    float64
    grade                           object
    sub_grade                       object
    emp_title                       object
    emp_length                      object
    home_ownership                  object
    annual_inc                     float64
    verification_status             object
    issue_d                         object
    loan_status                     object
    pymnt_plan                      object
    url                             object
    desc                            object
    purpose                         object
    title                           object
    zip_code                        object
    addr_state                      object
    dti                            float64
    delinq_2yrs                    float64
    earliest_cr_line                object
    inq_last_6mths                 float64
    mths_since_last_delinq         float64
    mths_since_last_record         float64
                                    ...   
    collection_recovery_fee        float64
    last_pymnt_d                    object
    last_pymnt_amnt                float64
    next_pymnt_d                    object
    last_credit_pull_d              object
    collections_12_mths_ex_med     float64
    mths_since_last_major_derog    float64
    policy_code                    float64
    application_type                object
    annual_inc_joint               float64
    dti_joint                      float64
    verification_status_joint       object
    acc_now_delinq                 float64
    tot_coll_amt                   float64
    tot_cur_bal                    float64
    open_acc_6m                    float64
    open_il_6m                     float64
    open_il_12m                    float64
    open_il_24m                    float64
    mths_since_rcnt_il             float64
    total_bal_il                   float64
    il_util                        float64
    open_rv_12m                    float64
    open_rv_24m                    float64
    max_bal_bc                     float64
    all_util                       float64
    total_rev_hi_lim               float64
    inq_fi                         float64
    total_cu_tl                    float64
    inq_last_12m                   float64
    Length: 74, dtype: object




```python
# Count the missing values in each column
loan.isnull().sum().sort_values(ascending=False)
```




    dti_joint                      886870
    verification_status_joint      886868
    annual_inc_joint               886868
    il_util                        868762
    mths_since_rcnt_il             866569
    all_util                       866007
    max_bal_bc                     866007
    open_rv_24m                    866007
    open_rv_12m                    866007
    total_cu_tl                    866007
    total_bal_il                   866007
    open_il_24m                    866007
    open_il_12m                    866007
    open_il_6m                     866007
    open_acc_6m                    866007
    inq_fi                         866007
    inq_last_12m                   866007
    desc                           761350
    mths_since_last_record         750326
    mths_since_last_major_derog    665676
    mths_since_last_delinq         454312
    next_pymnt_d                   252971
    tot_cur_bal                     70276
    total_rev_hi_lim                70276
    tot_coll_amt                    70276
    emp_title                       51457
    last_pymnt_d                    17659
    revol_util                        502
    title                             151
    collections_12_mths_ex_med        145
                                    ...  
    home_ownership                      0
    sub_grade                           0
    grade                               0
    installment                         0
    int_rate                            0
    term                                0
    funded_amnt_inv                     0
    url                                 0
    loan_amnt                           0
    member_id                           0
    funded_amnt                         0
    out_prncp                           0
    purpose                             0
    zip_code                            0
    application_type                    0
    policy_code                         0
    last_pymnt_amnt                     0
    collection_recovery_fee             0
    recoveries                          0
    total_rec_late_fee                  0
    total_rec_int                       0
    total_rec_prncp                     0
    total_pymnt_inv                     0
    total_pymnt                         0
    out_prncp_inv                       0
    initial_list_status                 0
    revol_bal                           0
    dti                                 0
    addr_state                          0
    id                                  0
    Length: 74, dtype: int64




```python
# Visuallize the missing values in each column
loan.isnull().sum().plot(kind='bar', figsize=(18,8), fontsize=14,);
plt.ylabel('Null values');
```


![Png](/assets/images/loan/output_12_0.png)




```python
# Remove columns with the highest number of null values
loan =loan.drop(['dti_joint',
'verification_status_joint',
'annual_inc_joint',
'il_util',
'mths_since_rcnt_il',
'all_util',
'max_bal_bc',
'open_rv_24m',
'open_rv_12m',
'total_cu_tl',
'total_bal_il',
'open_il_24m',
'open_il_12m',
'open_il_6m',
'open_acc_6m',
'inq_fi',
'inq_last_12m',
'desc',
'mths_since_last_record',
'mths_since_last_major_derog',
'mths_since_last_delinq',
'next_pymnt_d'
], axis=1)
```


```python
# Number of null values in each column
loan.isnull().sum().sort_values(ascending=False)
```




    total_rev_hi_lim              70276
    tot_coll_amt                  70276
    tot_cur_bal                   70276
    emp_title                     51457
    last_pymnt_d                  17659
    revol_util                      502
    title                           151
    collections_12_mths_ex_med      145
    last_credit_pull_d               53
    total_acc                        29
    delinq_2yrs                      29
    inq_last_6mths                   29
    open_acc                         29
    pub_rec                          29
    earliest_cr_line                 29
    acc_now_delinq                   29
    annual_inc                        4
    total_pymnt_inv                   0
    pymnt_plan                        0
    issue_d                           0
    verification_status               0
    home_ownership                    0
    emp_length                        0
    sub_grade                         0
    grade                             0
    installment                       0
    int_rate                          0
    term                              0
    funded_amnt_inv                   0
    funded_amnt                       0
    loan_amnt                         0
    member_id                         0
    loan_status                       0
    url                               0
    total_pymnt                       0
    purpose                           0
    out_prncp_inv                     0
    out_prncp                         0
    initial_list_status               0
    total_rec_prncp                   0
    total_rec_int                     0
    revol_bal                         0
    total_rec_late_fee                0
    recoveries                        0
    collection_recovery_fee           0
    last_pymnt_amnt                   0
    policy_code                       0
    dti                               0
    addr_state                        0
    zip_code                          0
    application_type                  0
    id                                0
    dtype: int64




```python
# Datatypes of column with highest null values
loan[['total_rev_hi_lim',
'tot_coll_amt',
'tot_cur_bal',
'emp_title',
'last_pymnt_d', 'revol_util', 'title',
'collections_12_mths_ex_med',
'last_credit_pull_d',
'total_acc',
'delinq_2yrs',
'inq_last_6mths',
'open_acc',
'pub_rec',
'earliest_cr_line',
'acc_now_delinq',
'annual_inc']].dtypes
```




    total_rev_hi_lim              float64
    tot_coll_amt                  float64
    tot_cur_bal                   float64
    emp_title                      object
    last_pymnt_d                   object
    revol_util                    float64
    title                          object
    collections_12_mths_ex_med    float64
    last_credit_pull_d             object
    total_acc                     float64
    delinq_2yrs                   float64
    inq_last_6mths                float64
    open_acc                      float64
    pub_rec                       float64
    earliest_cr_line               object
    acc_now_delinq                float64
    annual_inc                    float64
    dtype: object




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
      <th>id</th>
      <th>member_id</th>
      <th>loan_amnt</th>
      <th>funded_amnt</th>
      <th>funded_amnt_inv</th>
      <th>term</th>
      <th>int_rate</th>
      <th>installment</th>
      <th>grade</th>
      <th>sub_grade</th>
      <th>...</th>
      <th>last_pymnt_d</th>
      <th>last_pymnt_amnt</th>
      <th>last_credit_pull_d</th>
      <th>collections_12_mths_ex_med</th>
      <th>policy_code</th>
      <th>application_type</th>
      <th>acc_now_delinq</th>
      <th>tot_coll_amt</th>
      <th>tot_cur_bal</th>
      <th>total_rev_hi_lim</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1077501</td>
      <td>1296599</td>
      <td>5000.0</td>
      <td>5000.0</td>
      <td>4975.0</td>
      <td>36 months</td>
      <td>10.65</td>
      <td>162.87</td>
      <td>B</td>
      <td>B2</td>
      <td>...</td>
      <td>Jan-2015</td>
      <td>171.62</td>
      <td>Jan-2016</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>INDIVIDUAL</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1077430</td>
      <td>1314167</td>
      <td>2500.0</td>
      <td>2500.0</td>
      <td>2500.0</td>
      <td>60 months</td>
      <td>15.27</td>
      <td>59.83</td>
      <td>C</td>
      <td>C4</td>
      <td>...</td>
      <td>Apr-2013</td>
      <td>119.66</td>
      <td>Sep-2013</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>INDIVIDUAL</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1077175</td>
      <td>1313524</td>
      <td>2400.0</td>
      <td>2400.0</td>
      <td>2400.0</td>
      <td>36 months</td>
      <td>15.96</td>
      <td>84.33</td>
      <td>C</td>
      <td>C5</td>
      <td>...</td>
      <td>Jun-2014</td>
      <td>649.91</td>
      <td>Jan-2016</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>INDIVIDUAL</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1076863</td>
      <td>1277178</td>
      <td>10000.0</td>
      <td>10000.0</td>
      <td>10000.0</td>
      <td>36 months</td>
      <td>13.49</td>
      <td>339.31</td>
      <td>C</td>
      <td>C1</td>
      <td>...</td>
      <td>Jan-2015</td>
      <td>357.48</td>
      <td>Jan-2015</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>INDIVIDUAL</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1075358</td>
      <td>1311748</td>
      <td>3000.0</td>
      <td>3000.0</td>
      <td>3000.0</td>
      <td>60 months</td>
      <td>12.69</td>
      <td>67.79</td>
      <td>B</td>
      <td>B5</td>
      <td>...</td>
      <td>Jan-2016</td>
      <td>67.79</td>
      <td>Jan-2016</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>INDIVIDUAL</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 52 columns</p>
</div>




```python
loan.pymnt_plan.value_counts()
```




    n    887369
    y        10
    Name: pymnt_plan, dtype: int64




```python
# Visuallize pymnt_plan column values distribution
loan.pymnt_plan.value_counts().plot(kind='bar', figsize=(6,8), fontsize=14);
plt.xlabel("Plan");
plt.ylabel("Count");
plt.title("Distribution of pymnt_plan");
```


![png](assets/images/loan/output_18_0.png)



```python
loan.application_type.value_counts()
```




    INDIVIDUAL    886868
    JOINT            511
    Name: application_type, dtype: int64




```python
# Visuallize application_type column values distribution
loan.application_type.value_counts().plot(kind='bar', figsize=(6,8), fontsize=14);
plt.xlabel("application_type");
plt.ylabel("Count");
plt.title("Application_type column values distribution");
```


![png](assets/images/loan/output_20_0.png)



```python
# Percentage of 'INDIVIDUAL' to the total values in loan.application_type
(886868.0/(loan.application_type.value_counts().sum()))*100
```




    99.94241468414286




```python
loan.acc_now_delinq.value_counts()
```




    0.0     883236
    1.0       3866
    2.0        208
    3.0         28
    4.0          7
    5.0          3
    6.0          1
    14.0         1
    Name: acc_now_delinq, dtype: int64




```python
# Visuallize acc_now_delinq column values distribution
loan.acc_now_delinq.value_counts().plot(kind='bar');
plt.xlabel("acc_now_delinq distribution");
plt.ylabel("Count");
plt.title("Distribution of acc_now_delinq");
```


![png](assets/images/loan/output_23_0.png)



```python
# Percentage of '0' to the total values in 'acc_now_delinq'
(883236.0/(loan.acc_now_delinq.value_counts().sum()))*100
```




    99.53637234462163



# Columns with little information
- policy_code is always == 1
- payment_plan has only 10 y and 887372 n
- url not needed, but might be useful if it contains payment data
- id and member_id are all unique and do not show payment histories, they represent a single customer
- application_type is 'INDIVIDUAL' for 99.94% of all the records
- acc_now_delinq is 0 for 99.54% all of the records
- emp_title not needed here, but it might be useful for the modelling.
- zip_code not need because mostly redundant with the addr_state column since only the first 3 digits of the 5 digit zip code are visible.
- title might to be ignore for now
Numbers above have been calculated by grouping by counting the size of each group and sorting.


```python
# Drop columns with little information
drp = ['policy_code', 'pymnt_plan', 'url', 'id', 'member_id', 'application_type', 'acc_now_delinq',
'emp_title', 'zip_code','title']
loan.drop(drp, axis=1, inplace=True)
```

Columns that;
- leaks information from the future (after the loan has already been funded)
- are formatted poorly,
- requires more data or a lot of preprocessing to turn into useful a feature, or
- contains redundant information.are further dropped.
Data leakage can cause the model to overfit, because the model would also be learning from features that wouldn't be available when we're using it to make predictions on future loans.


```python
# Drop columns that leaks information from the future, requires more data or a lot of preprocessing
#to turn into useful a feature, or contains redundant information.
drp = ['funded_amnt', 'funded_amnt_inv', 'sub_grade', 'int_rate', 'out_prncp', 'out_prncp_inv',
'total_pymnt', 'total_pymnt_inv', 'total_rec_prncp', 'total_rec_int', 'total_rec_late_fee', 'recoveries',
'collection_recovery_fee', 'last_pymnt_d']
loan.drop(drp, axis=1, inplace=True)
```


```python
loan.sample(10)
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
      <th>home_ownership</th>
      <th>annual_inc</th>
      <th>verification_status</th>
      <th>issue_d</th>
      <th>loan_status</th>
      <th>...</th>
      <th>revol_bal</th>
      <th>revol_util</th>
      <th>total_acc</th>
      <th>initial_list_status</th>
      <th>last_pymnt_amnt</th>
      <th>last_credit_pull_d</th>
      <th>collections_12_mths_ex_med</th>
      <th>tot_coll_amt</th>
      <th>tot_cur_bal</th>
      <th>total_rev_hi_lim</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>350536</th>
      <td>12000.0</td>
      <td>60 months</td>
      <td>279.10</td>
      <td>C</td>
      <td>10+ years</td>
      <td>RENT</td>
      <td>90000.0</td>
      <td>Source Verified</td>
      <td>Jul-2014</td>
      <td>Fully Paid</td>
      <td>...</td>
      <td>2067.0</td>
      <td>13.2</td>
      <td>40.0</td>
      <td>w</td>
      <td>10032.97</td>
      <td>Jan-2016</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>35126.0</td>
      <td>15700.0</td>
    </tr>
    <tr>
      <th>749768</th>
      <td>15000.0</td>
      <td>36 months</td>
      <td>512.60</td>
      <td>C</td>
      <td>3 years</td>
      <td>MORTGAGE</td>
      <td>95000.0</td>
      <td>Verified</td>
      <td>May-2015</td>
      <td>Current</td>
      <td>...</td>
      <td>7132.0</td>
      <td>31.8</td>
      <td>15.0</td>
      <td>w</td>
      <td>512.60</td>
      <td>Jan-2016</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>38675.0</td>
      <td>22400.0</td>
    </tr>
    <tr>
      <th>286127</th>
      <td>10000.0</td>
      <td>36 months</td>
      <td>338.63</td>
      <td>C</td>
      <td>&lt; 1 year</td>
      <td>RENT</td>
      <td>75000.0</td>
      <td>Source Verified</td>
      <td>Oct-2014</td>
      <td>Current</td>
      <td>...</td>
      <td>3046.0</td>
      <td>45.5</td>
      <td>24.0</td>
      <td>f</td>
      <td>338.63</td>
      <td>Jan-2016</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>100742.0</td>
      <td>6700.0</td>
    </tr>
    <tr>
      <th>256502</th>
      <td>22000.0</td>
      <td>60 months</td>
      <td>582.75</td>
      <td>E</td>
      <td>2 years</td>
      <td>MORTGAGE</td>
      <td>141000.0</td>
      <td>Verified</td>
      <td>Nov-2014</td>
      <td>Current</td>
      <td>...</td>
      <td>16968.0</td>
      <td>72.5</td>
      <td>36.0</td>
      <td>w</td>
      <td>582.75</td>
      <td>Jan-2016</td>
      <td>0.0</td>
      <td>2183.0</td>
      <td>46911.0</td>
      <td>23400.0</td>
    </tr>
    <tr>
      <th>616237</th>
      <td>4800.0</td>
      <td>36 months</td>
      <td>165.58</td>
      <td>C</td>
      <td>1 year</td>
      <td>RENT</td>
      <td>18500.0</td>
      <td>Source Verified</td>
      <td>Sep-2015</td>
      <td>Current</td>
      <td>...</td>
      <td>13511.0</td>
      <td>101.6</td>
      <td>6.0</td>
      <td>w</td>
      <td>165.58</td>
      <td>Jan-2016</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>13511.0</td>
      <td>13300.0</td>
    </tr>
    <tr>
      <th>222447</th>
      <td>10000.0</td>
      <td>36 months</td>
      <td>304.36</td>
      <td>A</td>
      <td>10+ years</td>
      <td>RENT</td>
      <td>50000.0</td>
      <td>Verified</td>
      <td>Apr-2012</td>
      <td>Fully Paid</td>
      <td>...</td>
      <td>6099.0</td>
      <td>54.0</td>
      <td>24.0</td>
      <td>f</td>
      <td>4129.38</td>
      <td>Mar-2014</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>502351</th>
      <td>15000.0</td>
      <td>36 months</td>
      <td>464.95</td>
      <td>A</td>
      <td>&lt; 1 year</td>
      <td>OWN</td>
      <td>86000.0</td>
      <td>Verified</td>
      <td>Dec-2015</td>
      <td>Current</td>
      <td>...</td>
      <td>25657.0</td>
      <td>56.4</td>
      <td>17.0</td>
      <td>w</td>
      <td>464.95</td>
      <td>Jan-2016</td>
      <td>0.0</td>
      <td>65.0</td>
      <td>27981.0</td>
      <td>45500.0</td>
    </tr>
    <tr>
      <th>399135</th>
      <td>8000.0</td>
      <td>36 months</td>
      <td>275.92</td>
      <td>C</td>
      <td>10+ years</td>
      <td>RENT</td>
      <td>24000.0</td>
      <td>Source Verified</td>
      <td>May-2014</td>
      <td>Current</td>
      <td>...</td>
      <td>3518.0</td>
      <td>32.9</td>
      <td>30.0</td>
      <td>w</td>
      <td>275.92</td>
      <td>Jan-2016</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>29906.0</td>
      <td>10700.0</td>
    </tr>
    <tr>
      <th>501634</th>
      <td>18000.0</td>
      <td>36 months</td>
      <td>554.89</td>
      <td>A</td>
      <td>5 years</td>
      <td>MORTGAGE</td>
      <td>149000.0</td>
      <td>Not Verified</td>
      <td>Dec-2015</td>
      <td>Current</td>
      <td>...</td>
      <td>30056.0</td>
      <td>33.5</td>
      <td>64.0</td>
      <td>w</td>
      <td>554.89</td>
      <td>Jan-2016</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>810210.0</td>
      <td>89600.0</td>
    </tr>
    <tr>
      <th>514967</th>
      <td>4300.0</td>
      <td>36 months</td>
      <td>129.50</td>
      <td>A</td>
      <td>10+ years</td>
      <td>MORTGAGE</td>
      <td>71250.0</td>
      <td>Not Verified</td>
      <td>Nov-2015</td>
      <td>Current</td>
      <td>...</td>
      <td>4370.0</td>
      <td>9.3</td>
      <td>30.0</td>
      <td>w</td>
      <td>129.50</td>
      <td>Jan-2016</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>181442.0</td>
      <td>47000.0</td>
    </tr>
  </tbody>
</table>
<p>10 rows × 28 columns</p>
</div>




```python
loan.shape
```




    (887379, 28)



## Feature Preparation for machine learning
The data set has been reduced to 28 columns. There is need to carry out further transformations on the metrics.This will involve filling in missing values, stripping to change values from string to integer, transforming datetime to period.etc.
Missing values and categorical features dealt with before feeding the data into a machine learning algorithm,


```python
loan.isnull().sum().sort_values(ascending=False).head(15)
```




    total_rev_hi_lim              70276
    tot_coll_amt                  70276
    tot_cur_bal                   70276
    revol_util                      502
    collections_12_mths_ex_med      145
    last_credit_pull_d               53
    pub_rec                          29
    earliest_cr_line                 29
    inq_last_6mths                   29
    open_acc                         29
    delinq_2yrs                      29
    total_acc                        29
    annual_inc                        4
    revol_bal                         0
    verification_status               0
    dtype: int64




```python
# Fill in the missing values for 'total_rev_hi_lim' with the median 'total_rev_hi_lim'.
loan.total_rev_hi_lim.fillna(loan.total_rev_hi_lim.median(), inplace=True)

# Fill in the missing values for 'tot_coll_amt' with the median 'tot_coll_amt'.
loan.tot_coll_amt.fillna(loan.tot_coll_amt.median(), inplace=True)

# Fill in the missing values for 'tot_cur_bal' with the median 'tot_cur_bal'.
loan.tot_cur_bal.fillna(loan.tot_cur_bal.median(), inplace=True)

# Fill in the missing values for 'revol_util' with the median 'revol_util'.
loan.revol_util.fillna(loan.revol_util.median(), inplace=True)

# Fill in the missing values for 'collections_12_mths_ex_med' with the median 'collections_12_mths_ex_med'.
loan.collections_12_mths_ex_med.fillna(loan.collections_12_mths_ex_med.median(), inplace=True)

# Fill in the missing values for 'revol_utilrevol_utilrevol_utilrevol_util' with the median 'revol_utilrevol_utilrevol_util'.
loan.revol_util.fillna(loan.revol_util.median(), inplace=True)

# Fill in the missing values for 'total_acc' with the median 'total_acc'.
loan.total_acc.fillna(loan.total_acc.median(), inplace=True)

# Fill in the missing values for 'delinq_2yrsdelinq_2yrs' with the median 'delinq_2yrs'.
loan.delinq_2yrs.fillna(loan.delinq_2yrs.median(), inplace=True)

# Fill in the missing values for 'inq_last_6mths' with the median 'inq_last_6mths'.
loan.inq_last_6mths.fillna(loan.inq_last_6mths.median(), inplace=True)

# Fill in the missing values for 'pub_rec' with the median 'pub_rec'.
loan.pub_rec.fillna(loan.pub_rec.median(), inplace=True)

# Fill in the missing values for 'open_acc' with the median 'open_acc'.
loan.open_acc.fillna(loan.open_acc.median(), inplace=True)

# Fill in the missing values for 'annual_inc' with the median 'annual_inc'.
loan.annual_inc.fillna(loan.annual_inc.median(), inplace=True)
```


```python
# Remaining object type columns with missing values
loan.isnull().sum().sort_values(ascending=False).head()
```




    last_credit_pull_d    53
    earliest_cr_line      29
    total_rev_hi_lim       0
    dti                    0
    term                   0
    dtype: int64




```python
# Drop rows with missing values
loan = loan.dropna()
print loan.isnull().sum().sort_values(ascending=False)
```

    total_rev_hi_lim              0
    tot_cur_bal                   0
    term                          0
    installment                   0
    grade                         0
    emp_length                    0
    home_ownership                0
    annual_inc                    0
    verification_status           0
    issue_d                       0
    loan_status                   0
    purpose                       0
    addr_state                    0
    dti                           0
    delinq_2yrs                   0
    earliest_cr_line              0
    inq_last_6mths                0
    open_acc                      0
    pub_rec                       0
    revol_bal                     0
    revol_util                    0
    total_acc                     0
    initial_list_status           0
    last_pymnt_amnt               0
    last_credit_pull_d            0
    collections_12_mths_ex_med    0
    tot_coll_amt                  0
    loan_amnt                     0
    dtype: int64



```python
# strip months from 'term' and make it an int
loan['term'] = loan['term'].str.split(' ').str[1]
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
      <th>home_ownership</th>
      <th>annual_inc</th>
      <th>verification_status</th>
      <th>issue_d</th>
      <th>loan_status</th>
      <th>...</th>
      <th>revol_bal</th>
      <th>revol_util</th>
      <th>total_acc</th>
      <th>initial_list_status</th>
      <th>last_pymnt_amnt</th>
      <th>last_credit_pull_d</th>
      <th>collections_12_mths_ex_med</th>
      <th>tot_coll_amt</th>
      <th>tot_cur_bal</th>
      <th>total_rev_hi_lim</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>5000.0</td>
      <td>36</td>
      <td>162.87</td>
      <td>B</td>
      <td>10+ years</td>
      <td>RENT</td>
      <td>24000.0</td>
      <td>Verified</td>
      <td>Dec-2011</td>
      <td>Fully Paid</td>
      <td>...</td>
      <td>13648.0</td>
      <td>83.7</td>
      <td>9.0</td>
      <td>f</td>
      <td>171.62</td>
      <td>Jan-2016</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>80559.0</td>
      <td>23700.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2500.0</td>
      <td>60</td>
      <td>59.83</td>
      <td>C</td>
      <td>&lt; 1 year</td>
      <td>RENT</td>
      <td>30000.0</td>
      <td>Source Verified</td>
      <td>Dec-2011</td>
      <td>Charged Off</td>
      <td>...</td>
      <td>1687.0</td>
      <td>9.4</td>
      <td>4.0</td>
      <td>f</td>
      <td>119.66</td>
      <td>Sep-2013</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>80559.0</td>
      <td>23700.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2400.0</td>
      <td>36</td>
      <td>84.33</td>
      <td>C</td>
      <td>10+ years</td>
      <td>RENT</td>
      <td>12252.0</td>
      <td>Not Verified</td>
      <td>Dec-2011</td>
      <td>Fully Paid</td>
      <td>...</td>
      <td>2956.0</td>
      <td>98.5</td>
      <td>10.0</td>
      <td>f</td>
      <td>649.91</td>
      <td>Jan-2016</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>80559.0</td>
      <td>23700.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>10000.0</td>
      <td>36</td>
      <td>339.31</td>
      <td>C</td>
      <td>10+ years</td>
      <td>RENT</td>
      <td>49200.0</td>
      <td>Source Verified</td>
      <td>Dec-2011</td>
      <td>Fully Paid</td>
      <td>...</td>
      <td>5598.0</td>
      <td>21.0</td>
      <td>37.0</td>
      <td>f</td>
      <td>357.48</td>
      <td>Jan-2015</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>80559.0</td>
      <td>23700.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>3000.0</td>
      <td>60</td>
      <td>67.79</td>
      <td>B</td>
      <td>1 year</td>
      <td>RENT</td>
      <td>80000.0</td>
      <td>Source Verified</td>
      <td>Dec-2011</td>
      <td>Current</td>
      <td>...</td>
      <td>27783.0</td>
      <td>53.9</td>
      <td>38.0</td>
      <td>f</td>
      <td>67.79</td>
      <td>Jan-2016</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>80559.0</td>
      <td>23700.0</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 28 columns</p>
</div>




```python
# Extract numbers from emp_length and fill missing values with the median
loan['emp_length'] = loan['emp_length'].str.extract('(\d+)').astype(float)
loan['emp_length'] = loan['emp_length'].fillna(loan.emp_length.median())
```

    /Users/davidkeya/anaconda2/lib/python2.7/site-packages/ipykernel_launcher.py:2: FutureWarning: currently extract(expand=None) means expand=False (return Index/Series/DataFrame) but in a future version of pandas this will be changed to expand=True (return DataFrame)




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
      <th>home_ownership</th>
      <th>annual_inc</th>
      <th>verification_status</th>
      <th>issue_d</th>
      <th>loan_status</th>
      <th>...</th>
      <th>revol_bal</th>
      <th>revol_util</th>
      <th>total_acc</th>
      <th>initial_list_status</th>
      <th>last_pymnt_amnt</th>
      <th>last_credit_pull_d</th>
      <th>collections_12_mths_ex_med</th>
      <th>tot_coll_amt</th>
      <th>tot_cur_bal</th>
      <th>total_rev_hi_lim</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>5000.0</td>
      <td>36</td>
      <td>162.87</td>
      <td>B</td>
      <td>10.0</td>
      <td>RENT</td>
      <td>24000.0</td>
      <td>Verified</td>
      <td>Dec-2011</td>
      <td>Fully Paid</td>
      <td>...</td>
      <td>13648.0</td>
      <td>83.7</td>
      <td>9.0</td>
      <td>f</td>
      <td>171.62</td>
      <td>Jan-2016</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>80559.0</td>
      <td>23700.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2500.0</td>
      <td>60</td>
      <td>59.83</td>
      <td>C</td>
      <td>1.0</td>
      <td>RENT</td>
      <td>30000.0</td>
      <td>Source Verified</td>
      <td>Dec-2011</td>
      <td>Charged Off</td>
      <td>...</td>
      <td>1687.0</td>
      <td>9.4</td>
      <td>4.0</td>
      <td>f</td>
      <td>119.66</td>
      <td>Sep-2013</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>80559.0</td>
      <td>23700.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2400.0</td>
      <td>36</td>
      <td>84.33</td>
      <td>C</td>
      <td>10.0</td>
      <td>RENT</td>
      <td>12252.0</td>
      <td>Not Verified</td>
      <td>Dec-2011</td>
      <td>Fully Paid</td>
      <td>...</td>
      <td>2956.0</td>
      <td>98.5</td>
      <td>10.0</td>
      <td>f</td>
      <td>649.91</td>
      <td>Jan-2016</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>80559.0</td>
      <td>23700.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>10000.0</td>
      <td>36</td>
      <td>339.31</td>
      <td>C</td>
      <td>10.0</td>
      <td>RENT</td>
      <td>49200.0</td>
      <td>Source Verified</td>
      <td>Dec-2011</td>
      <td>Fully Paid</td>
      <td>...</td>
      <td>5598.0</td>
      <td>21.0</td>
      <td>37.0</td>
      <td>f</td>
      <td>357.48</td>
      <td>Jan-2015</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>80559.0</td>
      <td>23700.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>3000.0</td>
      <td>60</td>
      <td>67.79</td>
      <td>B</td>
      <td>1.0</td>
      <td>RENT</td>
      <td>80000.0</td>
      <td>Source Verified</td>
      <td>Dec-2011</td>
      <td>Current</td>
      <td>...</td>
      <td>27783.0</td>
      <td>53.9</td>
      <td>38.0</td>
      <td>f</td>
      <td>67.79</td>
      <td>Jan-2016</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>80559.0</td>
      <td>23700.0</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 28 columns</p>
</div>




```python
# Convert date inputs
cols = ["earliest_cr_line","issue_d","last_credit_pull_d"]
for col in cols:
    loan[col] = pd.to_datetime(loan[col],format="%b-%Y")
loan[cols].head()
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
      <th>earliest_cr_line</th>
      <th>issue_d</th>
      <th>last_credit_pull_d</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1985-01-01</td>
      <td>2011-12-01</td>
      <td>2016-01-01</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1999-04-01</td>
      <td>2011-12-01</td>
      <td>2013-09-01</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2001-11-01</td>
      <td>2011-12-01</td>
      <td>2016-01-01</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1996-02-01</td>
      <td>2011-12-01</td>
      <td>2015-01-01</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1996-01-01</td>
      <td>2011-12-01</td>
      <td>2016-01-01</td>
    </tr>
  </tbody>
</table>
</div>




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
      <th>home_ownership</th>
      <th>annual_inc</th>
      <th>verification_status</th>
      <th>issue_d</th>
      <th>loan_status</th>
      <th>...</th>
      <th>revol_bal</th>
      <th>revol_util</th>
      <th>total_acc</th>
      <th>initial_list_status</th>
      <th>last_pymnt_amnt</th>
      <th>last_credit_pull_d</th>
      <th>collections_12_mths_ex_med</th>
      <th>tot_coll_amt</th>
      <th>tot_cur_bal</th>
      <th>total_rev_hi_lim</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>5000.0</td>
      <td>36</td>
      <td>162.87</td>
      <td>B</td>
      <td>10.0</td>
      <td>RENT</td>
      <td>24000.0</td>
      <td>Verified</td>
      <td>2011-12-01</td>
      <td>Fully Paid</td>
      <td>...</td>
      <td>13648.0</td>
      <td>83.7</td>
      <td>9.0</td>
      <td>f</td>
      <td>171.62</td>
      <td>2016-01-01</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>80559.0</td>
      <td>23700.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2500.0</td>
      <td>60</td>
      <td>59.83</td>
      <td>C</td>
      <td>1.0</td>
      <td>RENT</td>
      <td>30000.0</td>
      <td>Source Verified</td>
      <td>2011-12-01</td>
      <td>Charged Off</td>
      <td>...</td>
      <td>1687.0</td>
      <td>9.4</td>
      <td>4.0</td>
      <td>f</td>
      <td>119.66</td>
      <td>2013-09-01</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>80559.0</td>
      <td>23700.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2400.0</td>
      <td>36</td>
      <td>84.33</td>
      <td>C</td>
      <td>10.0</td>
      <td>RENT</td>
      <td>12252.0</td>
      <td>Not Verified</td>
      <td>2011-12-01</td>
      <td>Fully Paid</td>
      <td>...</td>
      <td>2956.0</td>
      <td>98.5</td>
      <td>10.0</td>
      <td>f</td>
      <td>649.91</td>
      <td>2016-01-01</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>80559.0</td>
      <td>23700.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>10000.0</td>
      <td>36</td>
      <td>339.31</td>
      <td>C</td>
      <td>10.0</td>
      <td>RENT</td>
      <td>49200.0</td>
      <td>Source Verified</td>
      <td>2011-12-01</td>
      <td>Fully Paid</td>
      <td>...</td>
      <td>5598.0</td>
      <td>21.0</td>
      <td>37.0</td>
      <td>f</td>
      <td>357.48</td>
      <td>2015-01-01</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>80559.0</td>
      <td>23700.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>3000.0</td>
      <td>60</td>
      <td>67.79</td>
      <td>B</td>
      <td>1.0</td>
      <td>RENT</td>
      <td>80000.0</td>
      <td>Source Verified</td>
      <td>2011-12-01</td>
      <td>Current</td>
      <td>...</td>
      <td>27783.0</td>
      <td>53.9</td>
      <td>38.0</td>
      <td>f</td>
      <td>67.79</td>
      <td>2016-01-01</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>80559.0</td>
      <td>23700.0</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 28 columns</p>
</div>



## **Exploratory Data Analysis**  helps in  understand the various demographics better


```python
# Distribution of employment length for issued loans
print loan.emp_length.value_counts()
print loan.emp_length.value_counts().plot(kind='bar', figsize=(16,8), fontsize=14);
plt.xlabel("Length");
plt.ylabel("Count");
plt.title("Distribution of Employement Length For Issued Loans");
```

    10.0    291547
    1.0     127670
    6.0      87769
    2.0      78860
    3.0      70023
    5.0      55701
    4.0      52529
    7.0      44591
    8.0      43954
    9.0      34654
    Name: emp_length, dtype: int64
    AxesSubplot(0.08,0.125;0.87x0.755)



![png](assets/images/loan/output_43_1.png)


In the above bar chart, a significant number of customers have been employed for more than 10 years


```python
# Distribution of average amount loaned, by loan grade
print loan.grade.value_counts()
print loan.grade.value_counts().plot(kind='bar', figsize=(16,8), fontsize=14);
```

    B    254508
    C    245843
    A    148178
    D    139534
    E     70701
    F     23045
    G      5489
    Name: grade, dtype: int64
    AxesSubplot(0.08,0.125;0.87x0.755)



![png](assets/images/loan/output_45_1.png)


In the above relationship, loan amount tends to vary inversely to the grade


```python
# Boxplot of loan grade distribution
print loan.grade.value_counts().plot(kind='box');
plt.title("Loan Grade distribution")
```

    AxesSubplot(0.08,0.125;0.87x0.755)





    Text(0.5,1,u'Loan Grade distribution')




![png](assets/images/loan/output_47_2.png)



```python
# The distribution of loan amounts by grade
plt.subplots(figsize=(20,8))
plt.title("The distribution of loan amounts by grade").set_size(30)
sns.barplot(x="loan_amnt", y="grade", data=loan);
```


![png](assets/images/loan/output_48_0.png)


## Focus on Outcome/Target variable
Keeping in mind that the main goal is predict who will pay off a loan and who will default, loan_status is the only field in the dataset that describe a loan status, so it is used as the target column.


```python
# Loan staus mapping
loan["loan_status"].replace("Late (31-120 days)","Late",inplace=True)
loan["loan_status"].replace("Late (16-30 days)","Late",inplace=True)
loan["loan_status"].replace("Does not meet the credit policy. Status:Fully Paid","Fully Paid",inplace=True)
loan["loan_status"].replace("Does not meet the credit policy. Status:Charged Off","Charged Off",inplace=True)
print loan.loan_status.unique()
```

    ['Fully Paid' 'Charged Off' 'Current' 'Default' 'Late' 'In Grace Period'
     'Issued']



```python
# Frequency of the unique values in the loan_status column.
loan.loan_status.value_counts()
```




    Current            601750
    Fully Paid         209669
    Charged Off         46000
    Late                13947
    Issued               8460
    In Grace Period      6253
    Default              1219
    Name: loan_status, dtype: int64




```python
# A plot of loan status distribution
loan.loan_status.value_counts().plot(kind='bar', figsize=(16,8), fontsize=14);
plt.title('Loan Status Distribution');
plt.xlabel('Status');
plt.ylabel('Number of loan Applicants');
```


![png](assets/images/loan/output_52_0.png)


The Loan status is highly varied with many customers in the Current and Fully paid of status


```python
# The distribution of loan amounts by status
plt.subplots(figsize=(20,8))
plt.title("The distribution of loan amounts by status").set_size(30)
sns.barplot(x="loan_amnt", y="loan_status", data=loan);
```


![png](assets/images/loan/output_54_0.png)


* Fully Paid loans tend to be smaller. Possibly due to the age of the loans


```python
loan.loan_status.value_counts()
```




    Current            601750
    Fully Paid         209669
    Charged Off         46000
    Late                13947
    Issued               8460
    In Grace Period      6253
    Default              1219
    Name: loan_status, dtype: int64



## Binary classification
Default status is similar the Charged Off status, in Lending Club's eyes, loans that are charged off have essentially no chance of being repaid while default ones have a small chance. Therefore, samples where the loan_status column is 'Fully Paid' or 'Charged Off' are used. This is a case of binary classification.
Status that indicate that the loan is ongoing does not help in making prediction.

Focus here is to build a machine learning model that can learn from past loans in trying to predict which loans will be **paid off** and which will go into **default**. From the above table, only the Fully Paid and Charged Off values describe the final outcome of a loan. The other values describe loans that are still on going, and even though some loans are late on payments, it is not logical to classify them as Charged Off. Statuses that indicate the loan is ongoing, doesnt give neccesary information for prediction


```python
loan[['loan_status']].sample(10)
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
      <th>loan_status</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>316522</th>
      <td>Charged Off</td>
    </tr>
    <tr>
      <th>297489</th>
      <td>Current</td>
    </tr>
    <tr>
      <th>654903</th>
      <td>Current</td>
    </tr>
    <tr>
      <th>191636</th>
      <td>Fully Paid</td>
    </tr>
    <tr>
      <th>19882</th>
      <td>Fully Paid</td>
    </tr>
    <tr>
      <th>140911</th>
      <td>Current</td>
    </tr>
    <tr>
      <th>5545</th>
      <td>Fully Paid</td>
    </tr>
    <tr>
      <th>611538</th>
      <td>Current</td>
    </tr>
    <tr>
      <th>842049</th>
      <td>Current</td>
    </tr>
    <tr>
      <th>669999</th>
      <td>Current</td>
    </tr>
  </tbody>
</table>
</div>



Loans that that do not contain either **Fully Paid** or **Charged off** as the the loan status are removed and then transform the **Fully paid** values to **1** for positive case and the **Charged off** values to **0** for the negative case


```python
# Loans that that do not contain either Fully Paid or Charged off as the the loan status are removed
loan = loan[(loan["loan_status"] == "Fully Paid") |
                            (loan["loan_status"] == "Charged Off")]
```


```python
# Sample of transformed loan_status values
loan[['loan_status']].sample(10)
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
      <th>loan_status</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>15418</th>
      <td>Fully Paid</td>
    </tr>
    <tr>
      <th>444878</th>
      <td>Fully Paid</td>
    </tr>
    <tr>
      <th>223342</th>
      <td>Fully Paid</td>
    </tr>
    <tr>
      <th>396933</th>
      <td>Charged Off</td>
    </tr>
    <tr>
      <th>55732</th>
      <td>Charged Off</td>
    </tr>
    <tr>
      <th>225115</th>
      <td>Fully Paid</td>
    </tr>
    <tr>
      <th>172156</th>
      <td>Fully Paid</td>
    </tr>
    <tr>
      <th>55913</th>
      <td>Fully Paid</td>
    </tr>
    <tr>
      <th>749941</th>
      <td>Fully Paid</td>
    </tr>
    <tr>
      <th>221851</th>
      <td>Fully Paid</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Mapping values of the loan_status to 1/0 representation
mapping_dictionary = {"loan_status":{ "Fully Paid": 1, "Charged Off": 0}}
loan = loan.replace(mapping_dictionary)
```


```python
# Sample of target column outcome
loan[['loan_status']].sample(5)
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
      <th>loan_status</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>300670</th>
      <td>1</td>
    </tr>
    <tr>
      <th>195065</th>
      <td>1</td>
    </tr>
    <tr>
      <th>19003</th>
      <td>1</td>
    </tr>
    <tr>
      <th>268582</th>
      <td>1</td>
    </tr>
    <tr>
      <th>202649</th>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
# A visual of target column outcome
loan.loan_status.value_counts().plot.bar(stacked=True)
plt.xlabel('loan_status');
plt.ylabel('count');
```


![png](assets/images/loan/output_65_0.png)



```python
loan.loan_status.value_counts().plot.pie(autopct='%1.2f%%');
```


![png](assets/images/loan/output_66_0.png)


The plots indicate that majority of borrowers paid off their loan - 82.01% of loan borrowers paid off amount borrowed, while 17.99%  defaulted. From the loan data it is these 'defaulters' that we're more interested in filtering out as much as possible to reduce loses on investment returns.

## Working with Categorical Columns
The goal at this stage is to transform all categorical columns into numerical columns(int or float data type)
Columns of the data type object are identified for further processing into the numeric form


```python
# Data type of columns
loan.dtypes
```




    loan_amnt                            float64
    term                                  object
    installment                          float64
    grade                                 object
    emp_length                           float64
    home_ownership                        object
    annual_inc                           float64
    verification_status                   object
    issue_d                       datetime64[ns]
    loan_status                            int64
    purpose                               object
    addr_state                            object
    dti                                  float64
    delinq_2yrs                          float64
    earliest_cr_line              datetime64[ns]
    inq_last_6mths                       float64
    open_acc                             float64
    pub_rec                              float64
    revol_bal                            float64
    revol_util                           float64
    total_acc                            float64
    initial_list_status                   object
    last_pymnt_amnt                      float64
    last_credit_pull_d            datetime64[ns]
    collections_12_mths_ex_med           float64
    tot_coll_amt                         float64
    tot_cur_bal                          float64
    total_rev_hi_lim                     float64
    dtype: object




```python
# Columns  with Non-numeric data types
loan.dtypes.sort_values(ascending=True)
```




    loan_amnt                            float64
    tot_coll_amt                         float64
    collections_12_mths_ex_med           float64
    last_credit_pull_d            datetime64[ns]
    loan_status                            int64
    last_pymnt_amnt                      float64
    total_acc                            float64
    revol_util                           float64
    revol_bal                            float64
    pub_rec                              float64
    open_acc                             float64
    inq_last_6mths                       float64
    earliest_cr_line              datetime64[ns]
    delinq_2yrs                          float64
    dti                                  float64
    issue_d                       datetime64[ns]
    annual_inc                           float64
    emp_length                           float64
    installment                          float64
    tot_cur_bal                          float64
    total_rev_hi_lim                     float64
    addr_state                            object
    purpose                               object
    verification_status                   object
    home_ownership                        object
    initial_list_status                   object
    grade                                 object
    term                                  object
    dtype: object




```python
# A list of object type columns
object_type = ['addr_state', 'purpose','verification_status', 'home_ownership', 'initial_list_status', 'grade',
               'term', 'last_credit_pull_d', 'earliest_cr_line', 'issue_d']
```


```python
# Dataframe extract of oblect type columns
loan[object_type].sample(10)
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
      <th>addr_state</th>
      <th>purpose</th>
      <th>verification_status</th>
      <th>home_ownership</th>
      <th>initial_list_status</th>
      <th>grade</th>
      <th>term</th>
      <th>last_credit_pull_d</th>
      <th>earliest_cr_line</th>
      <th>issue_d</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>459492</th>
      <td>NJ</td>
      <td>debt_consolidation</td>
      <td>Verified</td>
      <td>RENT</td>
      <td>w</td>
      <td>C</td>
      <td>60</td>
      <td>2015-12-01</td>
      <td>2008-07-01</td>
      <td>2014-01-01</td>
    </tr>
    <tr>
      <th>395970</th>
      <td>IL</td>
      <td>debt_consolidation</td>
      <td>Verified</td>
      <td>MORTGAGE</td>
      <td>w</td>
      <td>B</td>
      <td>36</td>
      <td>2016-01-01</td>
      <td>1984-05-01</td>
      <td>2014-05-01</td>
    </tr>
    <tr>
      <th>128324</th>
      <td>NY</td>
      <td>other</td>
      <td>Not Verified</td>
      <td>RENT</td>
      <td>w</td>
      <td>D</td>
      <td>36</td>
      <td>2015-09-01</td>
      <td>2010-01-01</td>
      <td>2013-06-01</td>
    </tr>
    <tr>
      <th>220926</th>
      <td>MO</td>
      <td>home_improvement</td>
      <td>Source Verified</td>
      <td>MORTGAGE</td>
      <td>f</td>
      <td>A</td>
      <td>36</td>
      <td>2013-07-01</td>
      <td>1999-11-01</td>
      <td>2012-04-01</td>
    </tr>
    <tr>
      <th>394600</th>
      <td>CA</td>
      <td>debt_consolidation</td>
      <td>Source Verified</td>
      <td>RENT</td>
      <td>w</td>
      <td>C</td>
      <td>36</td>
      <td>2015-03-01</td>
      <td>2006-08-01</td>
      <td>2014-05-01</td>
    </tr>
    <tr>
      <th>174625</th>
      <td>CT</td>
      <td>debt_consolidation</td>
      <td>Not Verified</td>
      <td>MORTGAGE</td>
      <td>f</td>
      <td>B</td>
      <td>36</td>
      <td>2014-09-01</td>
      <td>1996-07-01</td>
      <td>2013-01-01</td>
    </tr>
    <tr>
      <th>306348</th>
      <td>AL</td>
      <td>debt_consolidation</td>
      <td>Source Verified</td>
      <td>RENT</td>
      <td>f</td>
      <td>C</td>
      <td>36</td>
      <td>2016-01-01</td>
      <td>2004-05-01</td>
      <td>2014-09-01</td>
    </tr>
    <tr>
      <th>323618</th>
      <td>NJ</td>
      <td>home_improvement</td>
      <td>Verified</td>
      <td>OWN</td>
      <td>f</td>
      <td>D</td>
      <td>36</td>
      <td>2016-01-01</td>
      <td>2009-10-01</td>
      <td>2014-08-01</td>
    </tr>
    <tr>
      <th>350713</th>
      <td>WA</td>
      <td>credit_card</td>
      <td>Verified</td>
      <td>RENT</td>
      <td>w</td>
      <td>A</td>
      <td>36</td>
      <td>2015-12-01</td>
      <td>1999-08-01</td>
      <td>2014-07-01</td>
    </tr>
    <tr>
      <th>455101</th>
      <td>MA</td>
      <td>credit_card</td>
      <td>Verified</td>
      <td>MORTGAGE</td>
      <td>f</td>
      <td>B</td>
      <td>36</td>
      <td>2016-01-01</td>
      <td>2007-06-01</td>
      <td>2014-01-01</td>
    </tr>
  </tbody>
</table>
</div>



The following columns represent categorical values:
- home_ownership — home ownership status, can only be 1 of 4 categorical values according to the data dictionary.
- verification_status — indicates if income was verified by Lending Club.
- term — number of payments on the loan, either 36 or 60.
- addr_state — borrower's state of residence.
- grade — LC assigned loan grade based on credit score.
- purpose — a category provided by the borrower for the loan request.
- initial_list_status - The initial listing status of the loan. Possible values are – W, F
- last_credit_pull_d - The most recent month Lending Club pulled credit for this loan
- earliest_cr_line - The month the borrower's earliest reported credit line
- issue_d


```python
loan.purpose.value_counts()
```




    debt_consolidation    149450
    credit_card            50412
    home_improvement       15142
    other                  14672
    major_purchase          6388
    small_business          4906
    car                     3709
    medical                 2910
    moving                  2074
    wedding                 2011
    house                   1696
    vacation                1607
    educational              422
    renewable_energy         270
    Name: purpose, dtype: int64



**The following Columns are dropped**
- Date columns from the DataFrame
- The addr_state column, however,contains too many unique values, so it's better to drop it.
- Purpose has many unique values
- addr_state



```python
# Drop the selected columns
drop_cols = ['purpose', 'addr_state', 'last_credit_pull_d', 'earliest_cr_line', 'issue_d']

loan = loan.drop(drop_cols, axis=1)
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
      <th>home_ownership</th>
      <th>annual_inc</th>
      <th>verification_status</th>
      <th>loan_status</th>
      <th>dti</th>
      <th>...</th>
      <th>pub_rec</th>
      <th>revol_bal</th>
      <th>revol_util</th>
      <th>total_acc</th>
      <th>initial_list_status</th>
      <th>last_pymnt_amnt</th>
      <th>collections_12_mths_ex_med</th>
      <th>tot_coll_amt</th>
      <th>tot_cur_bal</th>
      <th>total_rev_hi_lim</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>5000.0</td>
      <td>36</td>
      <td>162.87</td>
      <td>B</td>
      <td>10.0</td>
      <td>RENT</td>
      <td>24000.0</td>
      <td>Verified</td>
      <td>1</td>
      <td>27.65</td>
      <td>...</td>
      <td>0.0</td>
      <td>13648.0</td>
      <td>83.7</td>
      <td>9.0</td>
      <td>f</td>
      <td>171.62</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>80559.0</td>
      <td>23700.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2500.0</td>
      <td>60</td>
      <td>59.83</td>
      <td>C</td>
      <td>1.0</td>
      <td>RENT</td>
      <td>30000.0</td>
      <td>Source Verified</td>
      <td>0</td>
      <td>1.00</td>
      <td>...</td>
      <td>0.0</td>
      <td>1687.0</td>
      <td>9.4</td>
      <td>4.0</td>
      <td>f</td>
      <td>119.66</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>80559.0</td>
      <td>23700.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2400.0</td>
      <td>36</td>
      <td>84.33</td>
      <td>C</td>
      <td>10.0</td>
      <td>RENT</td>
      <td>12252.0</td>
      <td>Not Verified</td>
      <td>1</td>
      <td>8.72</td>
      <td>...</td>
      <td>0.0</td>
      <td>2956.0</td>
      <td>98.5</td>
      <td>10.0</td>
      <td>f</td>
      <td>649.91</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>80559.0</td>
      <td>23700.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>10000.0</td>
      <td>36</td>
      <td>339.31</td>
      <td>C</td>
      <td>10.0</td>
      <td>RENT</td>
      <td>49200.0</td>
      <td>Source Verified</td>
      <td>1</td>
      <td>20.00</td>
      <td>...</td>
      <td>0.0</td>
      <td>5598.0</td>
      <td>21.0</td>
      <td>37.0</td>
      <td>f</td>
      <td>357.48</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>80559.0</td>
      <td>23700.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5000.0</td>
      <td>36</td>
      <td>156.46</td>
      <td>A</td>
      <td>3.0</td>
      <td>RENT</td>
      <td>36000.0</td>
      <td>Source Verified</td>
      <td>1</td>
      <td>11.20</td>
      <td>...</td>
      <td>0.0</td>
      <td>7963.0</td>
      <td>28.3</td>
      <td>12.0</td>
      <td>f</td>
      <td>161.03</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>80559.0</td>
      <td>23700.0</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 23 columns</p>
</div>




```python
loan.dtypes.sort_values()
```




    loan_status                     int64
    loan_amnt                     float64
    tot_coll_amt                  float64
    collections_12_mths_ex_med    float64
    last_pymnt_amnt               float64
    total_acc                     float64
    revol_util                    float64
    revol_bal                     float64
    pub_rec                       float64
    open_acc                      float64
    tot_cur_bal                   float64
    inq_last_6mths                float64
    dti                           float64
    annual_inc                    float64
    emp_length                    float64
    installment                   float64
    delinq_2yrs                   float64
    total_rev_hi_lim              float64
    verification_status            object
    home_ownership                 object
    initial_list_status            object
    grade                          object
    term                           object
    dtype: object




```python
# DataFrame of categorical columns
loan[['verification_status', 'home_ownership', 'initial_list_status', 'grade', 'term']].sample(5)
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
      <th>verification_status</th>
      <th>home_ownership</th>
      <th>initial_list_status</th>
      <th>grade</th>
      <th>term</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>459321</th>
      <td>Not Verified</td>
      <td>MORTGAGE</td>
      <td>f</td>
      <td>A</td>
      <td>36</td>
    </tr>
    <tr>
      <th>217683</th>
      <td>Source Verified</td>
      <td>RENT</td>
      <td>f</td>
      <td>B</td>
      <td>36</td>
    </tr>
    <tr>
      <th>182833</th>
      <td>Not Verified</td>
      <td>NONE</td>
      <td>w</td>
      <td>B</td>
      <td>36</td>
    </tr>
    <tr>
      <th>176652</th>
      <td>Verified</td>
      <td>RENT</td>
      <td>f</td>
      <td>C</td>
      <td>36</td>
    </tr>
    <tr>
      <th>12037</th>
      <td>Source Verified</td>
      <td>RENT</td>
      <td>f</td>
      <td>B</td>
      <td>36</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Ordinal/Nominal values count check
print loan.verification_status.value_counts();
print''
print loan.home_ownership.value_counts();
print ''
print loan.initial_list_status.value_counts();
print ''
print loan.grade.value_counts();
print ''
print loan.term.value_counts();
```

    Verified           93514
    Not Verified       87859
    Source Verified    74296
    Name: verification_status, dtype: int64

    MORTGAGE    126082
    RENT        107196
    OWN          22167
    OTHER          179
    NONE            44
    ANY              1
    Name: home_ownership, dtype: int64

    f    184784
    w     70885
    Name: initial_list_status, dtype: int64

    B    76401
    C    65939
    A    42378
    D    41194
    E    19718
    F     7907
    G     2132
    Name: grade, dtype: int64

    36    199049
    60     56620
    Name: term, dtype: int64



```python
# For initial_listing_status encode w as 0 and f as 1.
loan['initial_list_status'] = loan.initial_list_status.map({'w':0, 'f':1})
```


```python
loan.initial_list_status.sample(5)
```




    40253     1
    767247    0
    9622      1
    76177     1
    809701    1
    Name: initial_list_status, dtype: int64




```python
# For term encode 36 as 36.0 and 60 as 60.0.
loan['term'] = loan.term.map({'36':36.0, '60':60.0})
```


```python
loan.term.sample(5)
```




    382548    36.0
    148903    36.0
    315525    60.0
    133094    60.0
    3249      36.0
    Name: term, dtype: float64




```python
# Map grade values to intergers
mapping_dict = {"grade":{"A": 1,"B": 2,"C": 3,"D": 4,"E": 5,"F": 6,"G": 7}}
loan = loan.replace(mapping_dict)
```


```python
loan['grade'].sample(5)
```




    58037     4
    423202    2
    7690      2
    139193    5
    814213    2
    Name: grade, dtype: int64




```python
# Converting nominal features into numerical features by encoding them as dummy variables
nominal_columns = ["home_ownership", "verification_status"]
dummy_loan = pd.get_dummies(loan[nominal_columns])
print dummy_loan.head()
```

       home_ownership_ANY  home_ownership_MORTGAGE  home_ownership_NONE  \
    0                   0                        0                    0   
    1                   0                        0                    0   
    2                   0                        0                    0   
    3                   0                        0                    0   
    5                   0                        0                    0   

       home_ownership_OTHER  home_ownership_OWN  home_ownership_RENT  \
    0                     0                   0                    1   
    1                     0                   0                    1   
    2                     0                   0                    1   
    3                     0                   0                    1   
    5                     0                   0                    1   

       verification_status_Not Verified  verification_status_Source Verified  \
    0                                 0                                    0   
    1                                 0                                    1   
    2                                 1                                    0   
    3                                 0                                    1   
    5                                 0                                    1   

       verification_status_Verified  
    0                             1  
    1                             0  
    2                             0  
    3                             0  
    5                             0  



```python
# Insert the dummy variables into the original DataFrame, drop nominal columns
loan = pd.concat([loan, dummy_loan], axis=1)
loan = loan.drop(nominal_columns, axis=1)
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
# Inspect all columns to ensure they contain no object type values
loan.dtypes
```




    loan_amnt                              float64
    term                                   float64
    installment                            float64
    grade                                    int64
    emp_length                             float64
    annual_inc                             float64
    loan_status                              int64
    dti                                    float64
    delinq_2yrs                            float64
    inq_last_6mths                         float64
    open_acc                               float64
    pub_rec                                float64
    revol_bal                              float64
    revol_util                             float64
    total_acc                              float64
    initial_list_status                      int64
    last_pymnt_amnt                        float64
    collections_12_mths_ex_med             float64
    tot_coll_amt                           float64
    tot_cur_bal                            float64
    total_rev_hi_lim                       float64
    home_ownership_ANY                       uint8
    home_ownership_MORTGAGE                  uint8
    home_ownership_NONE                      uint8
    home_ownership_OTHER                     uint8
    home_ownership_OWN                       uint8
    home_ownership_RENT                      uint8
    verification_status_Not Verified         uint8
    verification_status_Source Verified      uint8
    verification_status_Verified             uint8
    dtype: object



The final data preparation has been done to ensure the dataset is in the correct format ready to be fed into machine learning algorithms


```python
# Heatmap on the correlations between features in the loan data
loan_correlations = loan.corr()
plt.figure(figsize=(20, 20,))
plt.imshow(loan_correlations, cmap=None, interpolation='none', aspect='auto')
plt.colorbar()
plt.xticks(range(len(loan_correlations)), loan_correlations.columns, rotation='vertical')
plt.yticks(range(len(loan_correlations)), loan_correlations.columns);
plt.suptitle('Loan correlations Heat Map', fontsize=30, fontweight='bold')
plt.show()
```


![png](assets/images/loan/output_92_0.png)



```python
# Save loan DataFrame
loan.to_csv('result1.csv')
```
