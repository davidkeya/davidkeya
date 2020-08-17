---
header:
  overlay_image: /assets/images/data_cleaning/clean_wide.jpg
  caption: "Photo credit: [**Gratisography**](https://Gratisography.com)"
permalink: /portfolio/Data_Cleaning/
date: 2020-07-16
toc: true
toc_label: "Contents"
---


# Data Cleaning and handling Missing Values

## Introduction

The purpose of this project is to look at possible ways of preparing a dataset for exploratory data analysis.
This preparation can be achieved by carrying out the necessary steps as follows.

- Taking a first look at the data
- See how many missing data points are present
- Figure out why the data is missing
- Drop missing values
- Filling in missing values

##  Take a closer look at the data
The first task on exploratory data analysis(EDA) will be to examine closely the available datasets and libraries, before loading them. Datasets of events that occured in **American football** events are used in this this cleaning exercise. More specifically datasets of building permits issued in San Francisco.

The dataset is sourced from kaggle and contains all the regular seasons plays from the 2009-2016 NFL seasons. The dataset has 356,758 rows and 100 columns. Each play is broken down into great detail containing information on: game situation, players involved, results, and advanced metrics such as expected point and win probability values. Detailed information about the dataset can be found at the following web page, along with more NFL data: https://github.com/ryurko/nflscrapR-data.

The firs step in this process will involve loading in the necessary libraries for manipulating data and configuring the notebook.


```python
# Increase width display within the notebook
from IPython.core.display import display, HTML
display(HTML("<style>.container {width:90% !important;}</style>"))

```


<style>.container {width:90% !important;}</style>



```python
# import basic modules to be used at this level
import pandas as pd
import numpy as np
import os
from matplotlib import pyplot as plt
import io
import requests
%matplotlib inline
```


```python
# Avoid having displayed truncated output
pd.options.display.max_columns = 100

```


```python
# read in the Building_Permits dataset
sf_permits = pd.read_csv("./Building_Permits.csv",low_memory=False)
```

***Merging 9 Years of data into a single  csv file***


```python
# Merge data into a single csv file
df = pd.read_csv("./play_by_play/pbp_2009.csv",low_memory=False)

files = [file for file in os.listdir ('./play_by_play')]

all_years_data = pd.DataFrame()

for file in files:
    df = pd.read_csv("./play_by_play/"+file,low_memory=False)
    all_years_data = pd.concat([all_years_data, df])

all_years_data.to_csv("nfl_data.csv", index=False)

```

***Read in updated dataframe***

At this stage a look into the reading in of the dataset and missing values is important.


```python
# Read in updated dataframe
nfl_data = pd.read_csv("nfl_data.csv",low_memory=False)

```

***A look at the Missing values***


```python
# A few rows of the nfl_data
nfl_data.sample(5)
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
      <th>Date</th>
      <th>GameID</th>
      <th>play_id</th>
      <th>Drive</th>
      <th>qtr</th>
      <th>down</th>
      <th>time</th>
      <th>TimeUnder</th>
      <th>TimeSecs</th>
      <th>PlayTimeDiff</th>
      <th>SideofField</th>
      <th>yrdln</th>
      <th>yrdline100</th>
      <th>ydstogo</th>
      <th>ydsnet</th>
      <th>GoalToGo</th>
      <th>FirstDown</th>
      <th>posteam</th>
      <th>DefensiveTeam</th>
      <th>desc</th>
      <th>PlayAttempted</th>
      <th>Yards.Gained</th>
      <th>sp</th>
      <th>Touchdown</th>
      <th>ExPointResult</th>
      <th>TwoPointConv</th>
      <th>DefTwoPoint</th>
      <th>Safety</th>
      <th>Onsidekick</th>
      <th>PuntResult</th>
      <th>PlayType</th>
      <th>Passer</th>
      <th>Passer_ID</th>
      <th>PassAttempt</th>
      <th>PassOutcome</th>
      <th>PassLength</th>
      <th>AirYards</th>
      <th>YardsAfterCatch</th>
      <th>QBHit</th>
      <th>PassLocation</th>
      <th>InterceptionThrown</th>
      <th>Interceptor</th>
      <th>Rusher</th>
      <th>Rusher_ID</th>
      <th>RushAttempt</th>
      <th>RunLocation</th>
      <th>RunGap</th>
      <th>Receiver</th>
      <th>Receiver_ID</th>
      <th>Reception</th>
      <th>...</th>
      <th>Tackler1</th>
      <th>Tackler2</th>
      <th>FieldGoalResult</th>
      <th>FieldGoalDistance</th>
      <th>Fumble</th>
      <th>RecFumbTeam</th>
      <th>RecFumbPlayer</th>
      <th>Sack</th>
      <th>Challenge.Replay</th>
      <th>ChalReplayResult</th>
      <th>Accepted.Penalty</th>
      <th>PenalizedTeam</th>
      <th>PenaltyType</th>
      <th>PenalizedPlayer</th>
      <th>Penalty.Yards</th>
      <th>PosTeamScore</th>
      <th>DefTeamScore</th>
      <th>ScoreDiff</th>
      <th>AbsScoreDiff</th>
      <th>HomeTeam</th>
      <th>AwayTeam</th>
      <th>Timeout_Indicator</th>
      <th>Timeout_Team</th>
      <th>posteam_timeouts_pre</th>
      <th>HomeTimeouts_Remaining_Pre</th>
      <th>AwayTimeouts_Remaining_Pre</th>
      <th>HomeTimeouts_Remaining_Post</th>
      <th>AwayTimeouts_Remaining_Post</th>
      <th>No_Score_Prob</th>
      <th>Opp_Field_Goal_Prob</th>
      <th>Opp_Safety_Prob</th>
      <th>Opp_Touchdown_Prob</th>
      <th>Field_Goal_Prob</th>
      <th>Safety_Prob</th>
      <th>Touchdown_Prob</th>
      <th>ExPoint_Prob</th>
      <th>TwoPoint_Prob</th>
      <th>ExpPts</th>
      <th>EPA</th>
      <th>airEPA</th>
      <th>yacEPA</th>
      <th>Home_WP_pre</th>
      <th>Away_WP_pre</th>
      <th>Home_WP_post</th>
      <th>Away_WP_post</th>
      <th>Win_Prob</th>
      <th>WPA</th>
      <th>airWPA</th>
      <th>yacWPA</th>
      <th>Season</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>86595</th>
      <td>2016-12-24</td>
      <td>2016122410</td>
      <td>3778</td>
      <td>24</td>
      <td>4</td>
      <td>2.0</td>
      <td>03:45</td>
      <td>4</td>
      <td>225.0</td>
      <td>3.0</td>
      <td>SEA</td>
      <td>41.0</td>
      <td>59.0</td>
      <td>10</td>
      <td>31</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>SEA</td>
      <td>ARI</td>
      <td>(3:45) (Shotgun) R.Wilson pass short left to P...</td>
      <td>1</td>
      <td>15</td>
      <td>0</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>0</td>
      <td>NaN</td>
      <td>Pass</td>
      <td>R.Wilson</td>
      <td>00-0029263</td>
      <td>1</td>
      <td>Complete</td>
      <td>Short</td>
      <td>11</td>
      <td>4</td>
      <td>0</td>
      <td>left</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>None</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>P.Richardson</td>
      <td>00-0031257</td>
      <td>1</td>
      <td>...</td>
      <td>B.Williams</td>
      <td>K.Minter</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>0</td>
      <td>NaN</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>18.0</td>
      <td>31.0</td>
      <td>-13.0</td>
      <td>13.0</td>
      <td>SEA</td>
      <td>ARI</td>
      <td>0</td>
      <td>None</td>
      <td>3</td>
      <td>3</td>
      <td>2</td>
      <td>3</td>
      <td>2</td>
      <td>0.364112</td>
      <td>0.078190</td>
      <td>0.001069</td>
      <td>0.115821</td>
      <td>0.188548</td>
      <td>0.002357</td>
      <td>0.249902</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.272217</td>
      <td>1.343985</td>
      <td>1.141106</td>
      <td>0.202879</td>
      <td>0.044705</td>
      <td>0.955295</td>
      <td>0.054534</td>
      <td>0.945466</td>
      <td>0.044705</td>
      <td>0.009829</td>
      <td>0.011814</td>
      <td>-0.001985</td>
      <td>2016</td>
    </tr>
    <tr>
      <th>261180</th>
      <td>2010-12-12</td>
      <td>2010121203</td>
      <td>3607</td>
      <td>24</td>
      <td>4</td>
      <td>3.0</td>
      <td>03:54</td>
      <td>4</td>
      <td>234.0</td>
      <td>42.0</td>
      <td>OAK</td>
      <td>35.0</td>
      <td>65.0</td>
      <td>3</td>
      <td>29</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>OAK</td>
      <td>JAC</td>
      <td>(3:54) (Shotgun) J.Campbell pass short middle ...</td>
      <td>1</td>
      <td>11</td>
      <td>0</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>0</td>
      <td>NaN</td>
      <td>Pass</td>
      <td>J.Campbell</td>
      <td>00-0023460</td>
      <td>1</td>
      <td>Complete</td>
      <td>Short</td>
      <td>9</td>
      <td>2</td>
      <td>0</td>
      <td>middle</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>None</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>L.Murphy</td>
      <td>00-0027089</td>
      <td>1</td>
      <td>...</td>
      <td>W.Middleton</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>0</td>
      <td>NaN</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>24.0</td>
      <td>31.0</td>
      <td>-7.0</td>
      <td>7.0</td>
      <td>JAC</td>
      <td>OAK</td>
      <td>0</td>
      <td>None</td>
      <td>1</td>
      <td>3</td>
      <td>1</td>
      <td>3</td>
      <td>1</td>
      <td>0.394325</td>
      <td>0.096105</td>
      <td>0.001779</td>
      <td>0.138861</td>
      <td>0.137737</td>
      <td>0.002207</td>
      <td>0.228984</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.756611</td>
      <td>1.221927</td>
      <td>1.172029</td>
      <td>0.049898</td>
      <td>0.817330</td>
      <td>0.182670</td>
      <td>0.781864</td>
      <td>0.218136</td>
      <td>0.182670</td>
      <td>0.035465</td>
      <td>0.049188</td>
      <td>-0.013723</td>
      <td>2010</td>
    </tr>
    <tr>
      <th>158137</th>
      <td>2015-11-08</td>
      <td>2015110800</td>
      <td>1641</td>
      <td>9</td>
      <td>2</td>
      <td>1.0</td>
      <td>05:22</td>
      <td>6</td>
      <td>2122.0</td>
      <td>36.0</td>
      <td>MIN</td>
      <td>35.0</td>
      <td>35.0</td>
      <td>10</td>
      <td>51</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>STL</td>
      <td>MIN</td>
      <td>(5:22) T.Austin right end to MIN 23 for 12 yar...</td>
      <td>1</td>
      <td>12</td>
      <td>0</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>0</td>
      <td>NaN</td>
      <td>Run</td>
      <td>NaN</td>
      <td>None</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>NaN</td>
      <td>0</td>
      <td>NaN</td>
      <td>T.Austin</td>
      <td>00-0030525</td>
      <td>1</td>
      <td>right</td>
      <td>end</td>
      <td>NaN</td>
      <td>None</td>
      <td>0</td>
      <td>...</td>
      <td>C.Munnerlyn</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>0</td>
      <td>NaN</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>9.0</td>
      <td>10.0</td>
      <td>-1.0</td>
      <td>1.0</td>
      <td>MIN</td>
      <td>STL</td>
      <td>0</td>
      <td>None</td>
      <td>2</td>
      <td>3</td>
      <td>2</td>
      <td>3</td>
      <td>2</td>
      <td>0.154721</td>
      <td>0.042511</td>
      <td>0.000101</td>
      <td>0.062457</td>
      <td>0.298527</td>
      <td>0.002429</td>
      <td>0.439254</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>3.410289</td>
      <td>0.504575</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.444750</td>
      <td>0.555250</td>
      <td>0.428518</td>
      <td>0.571482</td>
      <td>0.555250</td>
      <td>0.016232</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>136833</th>
      <td>2015-09-13</td>
      <td>2015091301</td>
      <td>593</td>
      <td>3</td>
      <td>1</td>
      <td>3.0</td>
      <td>02:40</td>
      <td>3</td>
      <td>2860.0</td>
      <td>40.0</td>
      <td>STL</td>
      <td>37.0</td>
      <td>63.0</td>
      <td>15</td>
      <td>34</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>STL</td>
      <td>SEA</td>
      <td>(2:40) (Shotgun) N.Foles pass short left to B....</td>
      <td>1</td>
      <td>17</td>
      <td>0</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>0</td>
      <td>NaN</td>
      <td>Pass</td>
      <td>N.Foles</td>
      <td>00-0029567</td>
      <td>1</td>
      <td>Complete</td>
      <td>Short</td>
      <td>3</td>
      <td>14</td>
      <td>0</td>
      <td>left</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>None</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>B.Cunningham</td>
      <td>00-0029795</td>
      <td>1</td>
      <td>...</td>
      <td>E.Thomas</td>
      <td>K.Wright</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>0</td>
      <td>NaN</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>0.0</td>
      <td>6.0</td>
      <td>-6.0</td>
      <td>6.0</td>
      <td>STL</td>
      <td>SEA</td>
      <td>0</td>
      <td>None</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>0.022387</td>
      <td>0.178140</td>
      <td>0.003121</td>
      <td>0.274570</td>
      <td>0.248693</td>
      <td>0.005036</td>
      <td>0.268054</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.169876</td>
      <td>3.131845</td>
      <td>-1.142966</td>
      <td>4.274810</td>
      <td>0.296522</td>
      <td>0.703478</td>
      <td>0.396721</td>
      <td>0.603279</td>
      <td>0.296522</td>
      <td>0.100199</td>
      <td>-0.036755</td>
      <td>0.136954</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>241511</th>
      <td>2010-10-17</td>
      <td>2010101706</td>
      <td>36</td>
      <td>1</td>
      <td>1</td>
      <td>NaN</td>
      <td>15:00</td>
      <td>15</td>
      <td>3600.0</td>
      <td>0.0</td>
      <td>PHI</td>
      <td>30.0</td>
      <td>30.0</td>
      <td>0</td>
      <td>0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>ATL</td>
      <td>PHI</td>
      <td>D.Akers kicks 70 yards from PHI 30 to end zone...</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>0</td>
      <td>NaN</td>
      <td>Kickoff</td>
      <td>NaN</td>
      <td>None</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>NaN</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>None</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>None</td>
      <td>0</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>0</td>
      <td>NaN</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>PHI</td>
      <td>ATL</td>
      <td>0</td>
      <td>None</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>0.001506</td>
      <td>0.179749</td>
      <td>0.006639</td>
      <td>0.281138</td>
      <td>0.213700</td>
      <td>0.003592</td>
      <td>0.313676</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.323526</td>
      <td>0.000000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.514325</td>
      <td>0.485675</td>
      <td>0.514325</td>
      <td>0.485675</td>
      <td>0.485675</td>
      <td>0.000000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2010</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 103 columns</p>
</div>




```python
# A few rows of the permits_dataset
sf_permits.sample(5)
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
      <th>Permit Number</th>
      <th>Permit Type</th>
      <th>Permit Type Definition</th>
      <th>Permit Creation Date</th>
      <th>Block</th>
      <th>Lot</th>
      <th>Street Number</th>
      <th>Street Number Suffix</th>
      <th>Street Name</th>
      <th>Street Suffix</th>
      <th>Unit</th>
      <th>Unit Suffix</th>
      <th>Description</th>
      <th>Current Status</th>
      <th>Current Status Date</th>
      <th>Filed Date</th>
      <th>Issued Date</th>
      <th>Completed Date</th>
      <th>First Construction Document Date</th>
      <th>Structural Notification</th>
      <th>Number of Existing Stories</th>
      <th>Number of Proposed Stories</th>
      <th>Voluntary Soft-Story Retrofit</th>
      <th>Fire Only Permit</th>
      <th>Permit Expiration Date</th>
      <th>Estimated Cost</th>
      <th>Revised Cost</th>
      <th>Existing Use</th>
      <th>Existing Units</th>
      <th>Proposed Use</th>
      <th>Proposed Units</th>
      <th>Plansets</th>
      <th>TIDF Compliance</th>
      <th>Existing Construction Type</th>
      <th>Existing Construction Type Description</th>
      <th>Proposed Construction Type</th>
      <th>Proposed Construction Type Description</th>
      <th>Site Permit</th>
      <th>Supervisor District</th>
      <th>Neighborhoods - Analysis Boundaries</th>
      <th>Zipcode</th>
      <th>Location</th>
      <th>Record ID</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>30900</th>
      <td>201311131736</td>
      <td>8</td>
      <td>otc alterations permit</td>
      <td>11/13/2013</td>
      <td>0263</td>
      <td>011</td>
      <td>101</td>
      <td>NaN</td>
      <td>California</td>
      <td>St</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>add 1 strobe light to existing fire alarm system</td>
      <td>complete</td>
      <td>02/04/2014</td>
      <td>11/13/2013</td>
      <td>11/13/2013</td>
      <td>02/04/2014</td>
      <td>11/13/2013</td>
      <td>NaN</td>
      <td>48.0</td>
      <td>48.0</td>
      <td>NaN</td>
      <td>Y</td>
      <td>11/08/2014</td>
      <td>1200.0</td>
      <td>1200.0</td>
      <td>office</td>
      <td>0.0</td>
      <td>office</td>
      <td>0.0</td>
      <td>2.0</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>constr type 1</td>
      <td>1.0</td>
      <td>constr type 1</td>
      <td>NaN</td>
      <td>3.0</td>
      <td>Financial District/South Beach</td>
      <td>94111.0</td>
      <td>(37.79294896659241, -122.39809861435491)</td>
      <td>132397466081</td>
    </tr>
    <tr>
      <th>19774</th>
      <td>201307262849</td>
      <td>8</td>
      <td>otc alterations permit</td>
      <td>07/26/2013</td>
      <td>3199</td>
      <td>019</td>
      <td>1226</td>
      <td>NaN</td>
      <td>Plymouth</td>
      <td>Av</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>install new walk in tub and wall surround show...</td>
      <td>issued</td>
      <td>07/26/2013</td>
      <td>07/26/2013</td>
      <td>07/26/2013</td>
      <td>NaN</td>
      <td>07/26/2013</td>
      <td>NaN</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>07/21/2014</td>
      <td>5000.0</td>
      <td>5000.0</td>
      <td>1 family dwelling</td>
      <td>1.0</td>
      <td>1 family dwelling</td>
      <td>1.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>5.0</td>
      <td>wood frame (5)</td>
      <td>5.0</td>
      <td>wood frame (5)</td>
      <td>NaN</td>
      <td>7.0</td>
      <td>West of Twin Peaks</td>
      <td>94112.0</td>
      <td>(37.72454002851795, -122.45618452712912)</td>
      <td>1312301154719</td>
    </tr>
    <tr>
      <th>27905</th>
      <td>201310159301</td>
      <td>8</td>
      <td>otc alterations permit</td>
      <td>10/15/2013</td>
      <td>1814</td>
      <td>016</td>
      <td>1475</td>
      <td>NaN</td>
      <td>39th</td>
      <td>Av</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>new bathroom sink, shower/bath, toilet, reloca...</td>
      <td>issued</td>
      <td>02/11/2014</td>
      <td>10/15/2013</td>
      <td>02/11/2014</td>
      <td>NaN</td>
      <td>02/11/2014</td>
      <td>Y</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>02/06/2015</td>
      <td>78025.0</td>
      <td>78025.0</td>
      <td>1 family dwelling</td>
      <td>1.0</td>
      <td>1 family dwelling</td>
      <td>1.0</td>
      <td>2.0</td>
      <td>NaN</td>
      <td>5.0</td>
      <td>wood frame (5)</td>
      <td>5.0</td>
      <td>wood frame (5)</td>
      <td>NaN</td>
      <td>4.0</td>
      <td>Sunset/Parkside</td>
      <td>94122.0</td>
      <td>(37.75936464993233, -122.4986565583755)</td>
      <td>1320836115474</td>
    </tr>
    <tr>
      <th>143327</th>
      <td>M741087</td>
      <td>8</td>
      <td>otc alterations permit</td>
      <td>11/22/2016</td>
      <td>4270</td>
      <td>004</td>
      <td>1232</td>
      <td>NaN</td>
      <td>Alabama</td>
      <td>St</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>street space</td>
      <td>issued</td>
      <td>11/22/2016</td>
      <td>11/22/2016</td>
      <td>11/22/2016</td>
      <td>NaN</td>
      <td>11/22/2016</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>9.0</td>
      <td>Mission</td>
      <td>94110.0</td>
      <td>(37.7521225461672, -122.41121293944622)</td>
      <td>1445244172870</td>
    </tr>
    <tr>
      <th>20715</th>
      <td>201308063587</td>
      <td>8</td>
      <td>otc alterations permit</td>
      <td>08/06/2013</td>
      <td>1363</td>
      <td>019</td>
      <td>4131</td>
      <td>NaN</td>
      <td>California</td>
      <td>St</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>unit #1 :install 10 cabinets in kitchen and ta...</td>
      <td>complete</td>
      <td>09/15/2013</td>
      <td>08/06/2013</td>
      <td>08/06/2013</td>
      <td>09/15/2013</td>
      <td>08/06/2013</td>
      <td>NaN</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>08/01/2014</td>
      <td>15063.0</td>
      <td>15063.0</td>
      <td>apartments</td>
      <td>8.0</td>
      <td>apartments</td>
      <td>8.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>5.0</td>
      <td>wood frame (5)</td>
      <td>5.0</td>
      <td>wood frame (5)</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>Inner Richmond</td>
      <td>94118.0</td>
      <td>(37.78513301323214, -122.46189451227963)</td>
      <td>1313283410829</td>
    </tr>
  </tbody>
</table>
</div>



From the few rows of the nfl and sf_permits data files, there are a handful of missing data already!

## See how many missing data points are present


> **nfl data**


```python
# getting the number of missing data points per column
missing_values_count = nfl_data.isnull().sum()
```


```python
# A look at the number of missing values for the first ten columns
missing_values_count[0:10]
```




    Date                0
    GameID              0
    play_id             0
    Drive               0
    qtr                 0
    down            61154
    time              224
    TimeUnder           0
    TimeSecs          224
    PlayTimeDiff      444
    dtype: int64



It might be helpful to see a percentage of the values in the dataset were missing to give us a better sense of the scale of this problem.


```python
# Total missing values in the nfl_dataset
total_cells_nfl = np.product(nfl_data.shape)
total_missing_nfl = missing_values_count.sum()
```


```python
# Percent of missing data in nfl dataset
(total_missing_nfl/total_cells_nfl) * 100

```




    24.63066416865896



Almost a quarter (24%) of the cells in this dataset are empty! In the next step, we're going to take a closer look at some of the columns with missing values and try to figure out what might be going on with them

> **sf_permits data**


```python
# getting the number of missing data points per column
missing_values_count_sf = sf_permits.isnull().sum()
```


```python
# Total missing values int the sf_permits dataset
total_cells_sf = np.product(sf_permits.shape)
total_missing_sf = missing_values_count_sf.sum()
```


```python
# Percent of missing data in sf_permits dataset
(total_missing_sf/total_cells_sf) * 100

```




    26.26002315058403



Again about(26%) of the cells in this dataset are empty! In the next step, we're going to take a closer look at some of the columns with missing values and try to figure out what might be going on with them

## Why is data missing

Taking a look at the data and trying to find out why and how the data is the way it is and how it is likely to affect the analysis. The available information  from the documentation helps get a better understanding of the data.There is need to look at each column individually to figure out the best strategy for handling missing values.

#### A look at some of the columns with missing values from the sf_permits dataset.


```python
# getting the number of missing data points per column
sf_missing_values_count = sf_permits.isnull().sum()
```


```python
sf_missing_values_count
```




    Permit Number                                  0
    Permit Type                                    0
    Permit Type Definition                         0
    Permit Creation Date                           0
    Block                                          0
    Lot                                            0
    Street Number                                  0
    Street Number Suffix                      196684
    Street Name                                    0
    Street Suffix                               2768
    Unit                                      169421
    Unit Suffix                               196939
    Description                                  290
    Current Status                                 0
    Current Status Date                            0
    Filed Date                                     0
    Issued Date                                14940
    Completed Date                            101709
    First Construction Document Date           14946
    Structural Notification                   191978
    Number of Existing Stories                 42784
    Number of Proposed Stories                 42868
    Voluntary Soft-Story Retrofit             198865
    Fire Only Permit                          180073
    Permit Expiration Date                     51880
    Estimated Cost                             38066
    Revised Cost                                6066
    Existing Use                               41114
    Existing Units                             51538
    Proposed Use                               42439
    Proposed Units                             50911
    Plansets                                   37309
    TIDF Compliance                           198898
    Existing Construction Type                 43366
    Existing Construction Type Description     43366
    Proposed Construction Type                 43162
    Proposed Construction Type Description     43162
    Site Permit                               193541
    Supervisor District                         1717
    Neighborhoods - Analysis Boundaries         1725
    Zipcode                                     1716
    Location                                    1700
    Record ID                                      0
    dtype: int64




```python
# A visual of the number of missing data points per column
sf_missing_values_count = sf_permits.isnull().sum().plot(kind = 'bar', figsize=(16,8))
```


![png](assets/images/data_cleaning/output_32_0.png)


## Dropping missing values
One quick way of handling missing values is by removing rows and columns that have missing values,however not a recommended approach for important projects! It's usually worth it to take the time to go through data and really look at all the columns with missing values one-by-one to really get to know the dataset.

If you're sure you want to drop rows with missing values, pandas does have a handy function, dropna() to help you do this. Let's try it out on our NFL dataset!


```python
nfl_data.sample(5)
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
      <th>Date</th>
      <th>GameID</th>
      <th>play_id</th>
      <th>Drive</th>
      <th>qtr</th>
      <th>down</th>
      <th>time</th>
      <th>TimeUnder</th>
      <th>TimeSecs</th>
      <th>PlayTimeDiff</th>
      <th>SideofField</th>
      <th>yrdln</th>
      <th>yrdline100</th>
      <th>ydstogo</th>
      <th>ydsnet</th>
      <th>GoalToGo</th>
      <th>FirstDown</th>
      <th>posteam</th>
      <th>DefensiveTeam</th>
      <th>desc</th>
      <th>PlayAttempted</th>
      <th>Yards.Gained</th>
      <th>sp</th>
      <th>Touchdown</th>
      <th>ExPointResult</th>
      <th>TwoPointConv</th>
      <th>DefTwoPoint</th>
      <th>Safety</th>
      <th>Onsidekick</th>
      <th>PuntResult</th>
      <th>PlayType</th>
      <th>Passer</th>
      <th>Passer_ID</th>
      <th>PassAttempt</th>
      <th>PassOutcome</th>
      <th>PassLength</th>
      <th>AirYards</th>
      <th>YardsAfterCatch</th>
      <th>QBHit</th>
      <th>PassLocation</th>
      <th>InterceptionThrown</th>
      <th>Interceptor</th>
      <th>Rusher</th>
      <th>Rusher_ID</th>
      <th>RushAttempt</th>
      <th>RunLocation</th>
      <th>RunGap</th>
      <th>Receiver</th>
      <th>Receiver_ID</th>
      <th>Reception</th>
      <th>...</th>
      <th>Tackler1</th>
      <th>Tackler2</th>
      <th>FieldGoalResult</th>
      <th>FieldGoalDistance</th>
      <th>Fumble</th>
      <th>RecFumbTeam</th>
      <th>RecFumbPlayer</th>
      <th>Sack</th>
      <th>Challenge.Replay</th>
      <th>ChalReplayResult</th>
      <th>Accepted.Penalty</th>
      <th>PenalizedTeam</th>
      <th>PenaltyType</th>
      <th>PenalizedPlayer</th>
      <th>Penalty.Yards</th>
      <th>PosTeamScore</th>
      <th>DefTeamScore</th>
      <th>ScoreDiff</th>
      <th>AbsScoreDiff</th>
      <th>HomeTeam</th>
      <th>AwayTeam</th>
      <th>Timeout_Indicator</th>
      <th>Timeout_Team</th>
      <th>posteam_timeouts_pre</th>
      <th>HomeTimeouts_Remaining_Pre</th>
      <th>AwayTimeouts_Remaining_Pre</th>
      <th>HomeTimeouts_Remaining_Post</th>
      <th>AwayTimeouts_Remaining_Post</th>
      <th>No_Score_Prob</th>
      <th>Opp_Field_Goal_Prob</th>
      <th>Opp_Safety_Prob</th>
      <th>Opp_Touchdown_Prob</th>
      <th>Field_Goal_Prob</th>
      <th>Safety_Prob</th>
      <th>Touchdown_Prob</th>
      <th>ExPoint_Prob</th>
      <th>TwoPoint_Prob</th>
      <th>ExpPts</th>
      <th>EPA</th>
      <th>airEPA</th>
      <th>yacEPA</th>
      <th>Home_WP_pre</th>
      <th>Away_WP_pre</th>
      <th>Home_WP_post</th>
      <th>Away_WP_post</th>
      <th>Win_Prob</th>
      <th>WPA</th>
      <th>airWPA</th>
      <th>yacWPA</th>
      <th>Season</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>135605</th>
      <td>2015-09-10</td>
      <td>2015091000</td>
      <td>836</td>
      <td>4</td>
      <td>1</td>
      <td>NaN</td>
      <td>00:00</td>
      <td>0</td>
      <td>2700.0</td>
      <td>12.0</td>
      <td>NE</td>
      <td>19.0</td>
      <td>19.0</td>
      <td>0</td>
      <td>18</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>END QUARTER 1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>0</td>
      <td>NaN</td>
      <td>Quarter End</td>
      <td>NaN</td>
      <td>None</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>NaN</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>None</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>None</td>
      <td>0</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>0</td>
      <td>NaN</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NE</td>
      <td>PIT</td>
      <td>0</td>
      <td>None</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.000000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>23009</th>
      <td>2009-11-15</td>
      <td>2009111506</td>
      <td>1729</td>
      <td>10</td>
      <td>2</td>
      <td>2.0</td>
      <td>02:34</td>
      <td>3</td>
      <td>1954.0</td>
      <td>6.0</td>
      <td>BUF</td>
      <td>46.0</td>
      <td>54.0</td>
      <td>10</td>
      <td>13</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>BUF</td>
      <td>TEN</td>
      <td>(2:34) (Shotgun) F.Jackson up the middle to BU...</td>
      <td>1</td>
      <td>3</td>
      <td>0</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>0</td>
      <td>NaN</td>
      <td>Run</td>
      <td>NaN</td>
      <td>None</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>NaN</td>
      <td>0</td>
      <td>NaN</td>
      <td>F.Jackson</td>
      <td>00-0024204</td>
      <td>1</td>
      <td>middle</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>None</td>
      <td>0</td>
      <td>...</td>
      <td>J.Haye</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>0</td>
      <td>NaN</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>14.0</td>
      <td>17.0</td>
      <td>-3.0</td>
      <td>3.0</td>
      <td>TEN</td>
      <td>BUF</td>
      <td>0</td>
      <td>None</td>
      <td>3</td>
      <td>2</td>
      <td>3</td>
      <td>2</td>
      <td>3</td>
      <td>0.402032</td>
      <td>0.063901</td>
      <td>0.000686</td>
      <td>0.094506</td>
      <td>0.190193</td>
      <td>0.002158</td>
      <td>0.246525</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>1.445952</td>
      <td>-0.354435</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.543043</td>
      <td>0.456957</td>
      <td>0.555135</td>
      <td>0.444865</td>
      <td>0.456957</td>
      <td>-0.012091</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2009</td>
    </tr>
    <tr>
      <th>60976</th>
      <td>2016-10-17</td>
      <td>2016101700</td>
      <td>1234</td>
      <td>8</td>
      <td>2</td>
      <td>3.0</td>
      <td>12:36</td>
      <td>13</td>
      <td>2556.0</td>
      <td>7.0</td>
      <td>ARI</td>
      <td>28.0</td>
      <td>28.0</td>
      <td>14</td>
      <td>58</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NYJ</td>
      <td>ARI</td>
      <td>(12:36) (Shotgun) R.Fitzpatrick pass short rig...</td>
      <td>1</td>
      <td>7</td>
      <td>0</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>0</td>
      <td>NaN</td>
      <td>Pass</td>
      <td>R.Fitzpatrick</td>
      <td>00-0023682</td>
      <td>1</td>
      <td>Complete</td>
      <td>Short</td>
      <td>3</td>
      <td>4</td>
      <td>0</td>
      <td>right</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>None</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>C.Peake</td>
      <td>00-0032959</td>
      <td>1</td>
      <td>...</td>
      <td>T.Simon</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>0</td>
      <td>NaN</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>0.0</td>
      <td>7.0</td>
      <td>-7.0</td>
      <td>7.0</td>
      <td>ARI</td>
      <td>NYJ</td>
      <td>0</td>
      <td>None</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>0.031910</td>
      <td>0.061637</td>
      <td>0.000242</td>
      <td>0.098008</td>
      <td>0.489252</td>
      <td>0.004273</td>
      <td>0.314678</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>2.807589</td>
      <td>-0.490937</td>
      <td>-0.732344</td>
      <td>0.241407</td>
      <td>0.660633</td>
      <td>0.339367</td>
      <td>0.676382</td>
      <td>0.323618</td>
      <td>0.339367</td>
      <td>-0.015749</td>
      <td>-0.024256</td>
      <td>0.008507</td>
      <td>2016</td>
    </tr>
    <tr>
      <th>60005</th>
      <td>2016-10-16</td>
      <td>2016101603</td>
      <td>2864</td>
      <td>16</td>
      <td>4</td>
      <td>3.0</td>
      <td>12:59</td>
      <td>13</td>
      <td>779.0</td>
      <td>42.0</td>
      <td>PIT</td>
      <td>36.0</td>
      <td>36.0</td>
      <td>6</td>
      <td>21</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>MIA</td>
      <td>PIT</td>
      <td>(12:59) (Shotgun) R.Tannehill pass short middl...</td>
      <td>1</td>
      <td>5</td>
      <td>0</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>0</td>
      <td>NaN</td>
      <td>Pass</td>
      <td>R.Tannehill</td>
      <td>00-0029701</td>
      <td>1</td>
      <td>Complete</td>
      <td>Short</td>
      <td>4</td>
      <td>1</td>
      <td>0</td>
      <td>middle</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>None</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>A.Foster</td>
      <td>00-0026796</td>
      <td>1</td>
      <td>...</td>
      <td>T.Matakevich</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>0</td>
      <td>NaN</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>23.0</td>
      <td>8.0</td>
      <td>15.0</td>
      <td>15.0</td>
      <td>MIA</td>
      <td>PIT</td>
      <td>0</td>
      <td>None</td>
      <td>2</td>
      <td>2</td>
      <td>3</td>
      <td>2</td>
      <td>3</td>
      <td>0.035894</td>
      <td>0.073555</td>
      <td>0.000403</td>
      <td>0.114025</td>
      <td>0.409034</td>
      <td>0.003828</td>
      <td>0.363261</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>2.757947</td>
      <td>-1.295620</td>
      <td>-0.916843</td>
      <td>-0.378777</td>
      <td>0.953454</td>
      <td>0.046546</td>
      <td>0.942452</td>
      <td>0.057548</td>
      <td>0.953454</td>
      <td>-0.011001</td>
      <td>-0.008786</td>
      <td>-0.002215</td>
      <td>2016</td>
    </tr>
    <tr>
      <th>33066</th>
      <td>2009-12-06</td>
      <td>2009120611</td>
      <td>2662</td>
      <td>15</td>
      <td>3</td>
      <td>NaN</td>
      <td>03:58</td>
      <td>4</td>
      <td>1138.0</td>
      <td>6.0</td>
      <td>NYG</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>0</td>
      <td>56</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>DAL</td>
      <td>NYG</td>
      <td>N.Folk extra point is GOOD, Center-L.Ladouceur...</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>Made</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>0</td>
      <td>NaN</td>
      <td>Extra Point</td>
      <td>NaN</td>
      <td>None</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>NaN</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>None</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>None</td>
      <td>0</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>0</td>
      <td>NaN</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0</td>
      <td>16.0</td>
      <td>14.0</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>NYG</td>
      <td>DAL</td>
      <td>0</td>
      <td>None</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.990795</td>
      <td>0.0</td>
      <td>0.990795</td>
      <td>0.009205</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.419846</td>
      <td>0.580154</td>
      <td>0.392572</td>
      <td>0.607428</td>
      <td>0.580154</td>
      <td>0.027274</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2009</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 103 columns</p>
</div>




```python
 # Remove all the rows that contain a missing values
nfl_data.dropna()
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
      <th>Date</th>
      <th>GameID</th>
      <th>play_id</th>
      <th>Drive</th>
      <th>qtr</th>
      <th>down</th>
      <th>time</th>
      <th>TimeUnder</th>
      <th>TimeSecs</th>
      <th>PlayTimeDiff</th>
      <th>SideofField</th>
      <th>yrdln</th>
      <th>yrdline100</th>
      <th>ydstogo</th>
      <th>ydsnet</th>
      <th>GoalToGo</th>
      <th>FirstDown</th>
      <th>posteam</th>
      <th>DefensiveTeam</th>
      <th>desc</th>
      <th>PlayAttempted</th>
      <th>Yards.Gained</th>
      <th>sp</th>
      <th>Touchdown</th>
      <th>ExPointResult</th>
      <th>TwoPointConv</th>
      <th>DefTwoPoint</th>
      <th>Safety</th>
      <th>Onsidekick</th>
      <th>PuntResult</th>
      <th>PlayType</th>
      <th>Passer</th>
      <th>Passer_ID</th>
      <th>PassAttempt</th>
      <th>PassOutcome</th>
      <th>PassLength</th>
      <th>AirYards</th>
      <th>YardsAfterCatch</th>
      <th>QBHit</th>
      <th>PassLocation</th>
      <th>InterceptionThrown</th>
      <th>Interceptor</th>
      <th>Rusher</th>
      <th>Rusher_ID</th>
      <th>RushAttempt</th>
      <th>RunLocation</th>
      <th>RunGap</th>
      <th>Receiver</th>
      <th>Receiver_ID</th>
      <th>Reception</th>
      <th>...</th>
      <th>Tackler1</th>
      <th>Tackler2</th>
      <th>FieldGoalResult</th>
      <th>FieldGoalDistance</th>
      <th>Fumble</th>
      <th>RecFumbTeam</th>
      <th>RecFumbPlayer</th>
      <th>Sack</th>
      <th>Challenge.Replay</th>
      <th>ChalReplayResult</th>
      <th>Accepted.Penalty</th>
      <th>PenalizedTeam</th>
      <th>PenaltyType</th>
      <th>PenalizedPlayer</th>
      <th>Penalty.Yards</th>
      <th>PosTeamScore</th>
      <th>DefTeamScore</th>
      <th>ScoreDiff</th>
      <th>AbsScoreDiff</th>
      <th>HomeTeam</th>
      <th>AwayTeam</th>
      <th>Timeout_Indicator</th>
      <th>Timeout_Team</th>
      <th>posteam_timeouts_pre</th>
      <th>HomeTimeouts_Remaining_Pre</th>
      <th>AwayTimeouts_Remaining_Pre</th>
      <th>HomeTimeouts_Remaining_Post</th>
      <th>AwayTimeouts_Remaining_Post</th>
      <th>No_Score_Prob</th>
      <th>Opp_Field_Goal_Prob</th>
      <th>Opp_Safety_Prob</th>
      <th>Opp_Touchdown_Prob</th>
      <th>Field_Goal_Prob</th>
      <th>Safety_Prob</th>
      <th>Touchdown_Prob</th>
      <th>ExPoint_Prob</th>
      <th>TwoPoint_Prob</th>
      <th>ExpPts</th>
      <th>EPA</th>
      <th>airEPA</th>
      <th>yacEPA</th>
      <th>Home_WP_pre</th>
      <th>Away_WP_pre</th>
      <th>Home_WP_post</th>
      <th>Away_WP_post</th>
      <th>Win_Prob</th>
      <th>WPA</th>
      <th>airWPA</th>
      <th>yacWPA</th>
      <th>Season</th>
    </tr>
  </thead>
  <tbody>
  </tbody>
</table>
<p>0 rows × 103 columns</p>
</div>



***All data removed! this is because every row has atleat one missing value***


```python
# remove all columns with at least one missing value
columns_with_na_dropped = nfl_data.dropna(axis=1)
columns_with_na_dropped.head()
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
      <th>Date</th>
      <th>GameID</th>
      <th>play_id</th>
      <th>Drive</th>
      <th>qtr</th>
      <th>TimeUnder</th>
      <th>ydstogo</th>
      <th>ydsnet</th>
      <th>PlayAttempted</th>
      <th>Yards.Gained</th>
      <th>sp</th>
      <th>Touchdown</th>
      <th>Safety</th>
      <th>Onsidekick</th>
      <th>PlayType</th>
      <th>Passer_ID</th>
      <th>PassAttempt</th>
      <th>AirYards</th>
      <th>YardsAfterCatch</th>
      <th>QBHit</th>
      <th>InterceptionThrown</th>
      <th>Rusher_ID</th>
      <th>RushAttempt</th>
      <th>Receiver_ID</th>
      <th>Reception</th>
      <th>Fumble</th>
      <th>Sack</th>
      <th>Challenge.Replay</th>
      <th>Accepted.Penalty</th>
      <th>Penalty.Yards</th>
      <th>HomeTeam</th>
      <th>AwayTeam</th>
      <th>Timeout_Indicator</th>
      <th>Timeout_Team</th>
      <th>posteam_timeouts_pre</th>
      <th>HomeTimeouts_Remaining_Pre</th>
      <th>AwayTimeouts_Remaining_Pre</th>
      <th>HomeTimeouts_Remaining_Post</th>
      <th>AwayTimeouts_Remaining_Post</th>
      <th>ExPoint_Prob</th>
      <th>TwoPoint_Prob</th>
      <th>Season</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2009-09-10</td>
      <td>2009091000</td>
      <td>46</td>
      <td>1</td>
      <td>1</td>
      <td>15</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>39</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Kickoff</td>
      <td>None</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>None</td>
      <td>0</td>
      <td>None</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>PIT</td>
      <td>TEN</td>
      <td>0</td>
      <td>None</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>2009</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2009-09-10</td>
      <td>2009091000</td>
      <td>68</td>
      <td>1</td>
      <td>1</td>
      <td>15</td>
      <td>10</td>
      <td>5</td>
      <td>1</td>
      <td>5</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Pass</td>
      <td>00-0022924</td>
      <td>1</td>
      <td>-3</td>
      <td>8</td>
      <td>0</td>
      <td>0</td>
      <td>None</td>
      <td>0</td>
      <td>00-0017162</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>PIT</td>
      <td>TEN</td>
      <td>0</td>
      <td>None</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>2009</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2009-09-10</td>
      <td>2009091000</td>
      <td>92</td>
      <td>1</td>
      <td>1</td>
      <td>15</td>
      <td>5</td>
      <td>2</td>
      <td>1</td>
      <td>-3</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Run</td>
      <td>None</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>00-0022250</td>
      <td>1</td>
      <td>None</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>PIT</td>
      <td>TEN</td>
      <td>0</td>
      <td>None</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>2009</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2009-09-10</td>
      <td>2009091000</td>
      <td>113</td>
      <td>1</td>
      <td>1</td>
      <td>14</td>
      <td>8</td>
      <td>2</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Pass</td>
      <td>00-0022924</td>
      <td>1</td>
      <td>34</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>None</td>
      <td>0</td>
      <td>00-0026901</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>PIT</td>
      <td>TEN</td>
      <td>0</td>
      <td>None</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>2009</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2009-09-10</td>
      <td>2009091000</td>
      <td>139</td>
      <td>1</td>
      <td>1</td>
      <td>14</td>
      <td>8</td>
      <td>2</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>Punt</td>
      <td>None</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>None</td>
      <td>0</td>
      <td>None</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>PIT</td>
      <td>TEN</td>
      <td>0</td>
      <td>None</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>2009</td>
    </tr>
  </tbody>
</table>
</div>



***By removing columns with missing values, how much data is los*t**


```python
# Computation of how data much is lost
print("Columns in original dataset: %d \n" % nfl_data.shape[1])
print("Columns with na's dropped: %d" % columns_with_na_dropped.shape[1])
```

    Columns in original dataset: 103

    Columns with na's dropped: 42


## Fill in  missing values (Imputation)


```python
 # First five rows of the sf_permits dataset
sf_permits.head(5)
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
      <th>Permit Number</th>
      <th>Permit Type</th>
      <th>Permit Type Definition</th>
      <th>Permit Creation Date</th>
      <th>Block</th>
      <th>Lot</th>
      <th>Street Number</th>
      <th>Street Number Suffix</th>
      <th>Street Name</th>
      <th>Street Suffix</th>
      <th>Unit</th>
      <th>Unit Suffix</th>
      <th>Description</th>
      <th>Current Status</th>
      <th>Current Status Date</th>
      <th>Filed Date</th>
      <th>Issued Date</th>
      <th>Completed Date</th>
      <th>First Construction Document Date</th>
      <th>Structural Notification</th>
      <th>Number of Existing Stories</th>
      <th>Number of Proposed Stories</th>
      <th>Voluntary Soft-Story Retrofit</th>
      <th>Fire Only Permit</th>
      <th>Permit Expiration Date</th>
      <th>Estimated Cost</th>
      <th>Revised Cost</th>
      <th>Existing Use</th>
      <th>Existing Units</th>
      <th>Proposed Use</th>
      <th>Proposed Units</th>
      <th>Plansets</th>
      <th>TIDF Compliance</th>
      <th>Existing Construction Type</th>
      <th>Existing Construction Type Description</th>
      <th>Proposed Construction Type</th>
      <th>Proposed Construction Type Description</th>
      <th>Site Permit</th>
      <th>Supervisor District</th>
      <th>Neighborhoods - Analysis Boundaries</th>
      <th>Zipcode</th>
      <th>Location</th>
      <th>Record ID</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>201505065519</td>
      <td>4</td>
      <td>sign - erect</td>
      <td>05/06/2015</td>
      <td>0326</td>
      <td>023</td>
      <td>140</td>
      <td>NaN</td>
      <td>Ellis</td>
      <td>St</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>ground fl facade: to erect illuminated, electr...</td>
      <td>expired</td>
      <td>12/21/2017</td>
      <td>05/06/2015</td>
      <td>11/09/2015</td>
      <td>NaN</td>
      <td>11/09/2015</td>
      <td>NaN</td>
      <td>6.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>11/03/2016</td>
      <td>4000.0</td>
      <td>4000.0</td>
      <td>tourist hotel/motel</td>
      <td>143.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2.0</td>
      <td>NaN</td>
      <td>3.0</td>
      <td>constr type 3</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>3.0</td>
      <td>Tenderloin</td>
      <td>94102.0</td>
      <td>(37.785719256680785, -122.40852313194863)</td>
      <td>1380611233945</td>
    </tr>
    <tr>
      <th>1</th>
      <td>201604195146</td>
      <td>4</td>
      <td>sign - erect</td>
      <td>04/19/2016</td>
      <td>0306</td>
      <td>007</td>
      <td>440</td>
      <td>NaN</td>
      <td>Geary</td>
      <td>St</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>remove (e) awning and associated signs.</td>
      <td>issued</td>
      <td>08/03/2017</td>
      <td>04/19/2016</td>
      <td>08/03/2017</td>
      <td>NaN</td>
      <td>08/03/2017</td>
      <td>NaN</td>
      <td>7.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>12/03/2017</td>
      <td>1.0</td>
      <td>500.0</td>
      <td>tourist hotel/motel</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2.0</td>
      <td>NaN</td>
      <td>3.0</td>
      <td>constr type 3</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>3.0</td>
      <td>Tenderloin</td>
      <td>94102.0</td>
      <td>(37.78733980600732, -122.41063199757738)</td>
      <td>1420164406718</td>
    </tr>
    <tr>
      <th>2</th>
      <td>201605278609</td>
      <td>3</td>
      <td>additions alterations or repairs</td>
      <td>05/27/2016</td>
      <td>0595</td>
      <td>203</td>
      <td>1647</td>
      <td>NaN</td>
      <td>Pacific</td>
      <td>Av</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>installation of separating wall</td>
      <td>withdrawn</td>
      <td>09/26/2017</td>
      <td>05/27/2016</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>6.0</td>
      <td>6.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>20000.0</td>
      <td>NaN</td>
      <td>retail sales</td>
      <td>39.0</td>
      <td>retail sales</td>
      <td>39.0</td>
      <td>2.0</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>constr type 1</td>
      <td>1.0</td>
      <td>constr type 1</td>
      <td>NaN</td>
      <td>3.0</td>
      <td>Russian Hill</td>
      <td>94109.0</td>
      <td>(37.7946573324287, -122.42232562979227)</td>
      <td>1424856504716</td>
    </tr>
    <tr>
      <th>3</th>
      <td>201611072166</td>
      <td>8</td>
      <td>otc alterations permit</td>
      <td>11/07/2016</td>
      <td>0156</td>
      <td>011</td>
      <td>1230</td>
      <td>NaN</td>
      <td>Pacific</td>
      <td>Av</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>repair dryrot &amp; stucco at front of bldg.</td>
      <td>complete</td>
      <td>07/24/2017</td>
      <td>11/07/2016</td>
      <td>07/18/2017</td>
      <td>07/24/2017</td>
      <td>07/18/2017</td>
      <td>NaN</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>07/13/2018</td>
      <td>2000.0</td>
      <td>2000.0</td>
      <td>1 family dwelling</td>
      <td>1.0</td>
      <td>1 family dwelling</td>
      <td>1.0</td>
      <td>2.0</td>
      <td>NaN</td>
      <td>5.0</td>
      <td>wood frame (5)</td>
      <td>5.0</td>
      <td>wood frame (5)</td>
      <td>NaN</td>
      <td>3.0</td>
      <td>Nob Hill</td>
      <td>94109.0</td>
      <td>(37.79595867909168, -122.41557405519474)</td>
      <td>1443574295566</td>
    </tr>
    <tr>
      <th>4</th>
      <td>201611283529</td>
      <td>6</td>
      <td>demolitions</td>
      <td>11/28/2016</td>
      <td>0342</td>
      <td>001</td>
      <td>950</td>
      <td>NaN</td>
      <td>Market</td>
      <td>St</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>demolish retail/office/commercial 3-story buil...</td>
      <td>issued</td>
      <td>12/01/2017</td>
      <td>11/28/2016</td>
      <td>12/01/2017</td>
      <td>NaN</td>
      <td>11/20/2017</td>
      <td>NaN</td>
      <td>3.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>12/01/2018</td>
      <td>100000.0</td>
      <td>100000.0</td>
      <td>retail sales</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2.0</td>
      <td>NaN</td>
      <td>3.0</td>
      <td>constr type 3</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>6.0</td>
      <td>Tenderloin</td>
      <td>94102.0</td>
      <td>(37.78315261897309, -122.40950883997789)</td>
      <td>144548169992</td>
    </tr>
  </tbody>
</table>
</div>



 #### Replacing  NaN's  with a value coming directly after it and then replace any remaining NaN's with 0

In this section an attempt is made to replace all the NaN's in the sf_permits data with the one that comes directly after it and then replace any remaining NaN's with 0


```python
# replace all the NaN's in the sf_permits data with the one that comes directly after it and then replace any remaining NaN's with 0
sf_permits_fill = sf_permits.fillna(method = 'bfill', axis=0).fillna(0)
```


```python
# First five rows of the dataset filled with missing values
sf_permits_fill.head()
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
      <th>Permit Number</th>
      <th>Permit Type</th>
      <th>Permit Type Definition</th>
      <th>Permit Creation Date</th>
      <th>Block</th>
      <th>Lot</th>
      <th>Street Number</th>
      <th>Street Number Suffix</th>
      <th>Street Name</th>
      <th>Street Suffix</th>
      <th>Unit</th>
      <th>Unit Suffix</th>
      <th>Description</th>
      <th>Current Status</th>
      <th>Current Status Date</th>
      <th>Filed Date</th>
      <th>Issued Date</th>
      <th>Completed Date</th>
      <th>First Construction Document Date</th>
      <th>Structural Notification</th>
      <th>Number of Existing Stories</th>
      <th>Number of Proposed Stories</th>
      <th>Voluntary Soft-Story Retrofit</th>
      <th>Fire Only Permit</th>
      <th>Permit Expiration Date</th>
      <th>Estimated Cost</th>
      <th>Revised Cost</th>
      <th>Existing Use</th>
      <th>Existing Units</th>
      <th>Proposed Use</th>
      <th>Proposed Units</th>
      <th>Plansets</th>
      <th>TIDF Compliance</th>
      <th>Existing Construction Type</th>
      <th>Existing Construction Type Description</th>
      <th>Proposed Construction Type</th>
      <th>Proposed Construction Type Description</th>
      <th>Site Permit</th>
      <th>Supervisor District</th>
      <th>Neighborhoods - Analysis Boundaries</th>
      <th>Zipcode</th>
      <th>Location</th>
      <th>Record ID</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>201505065519</td>
      <td>4</td>
      <td>sign - erect</td>
      <td>05/06/2015</td>
      <td>0326</td>
      <td>023</td>
      <td>140</td>
      <td>A</td>
      <td>Ellis</td>
      <td>St</td>
      <td>0.0</td>
      <td>A</td>
      <td>ground fl facade: to erect illuminated, electr...</td>
      <td>expired</td>
      <td>12/21/2017</td>
      <td>05/06/2015</td>
      <td>11/09/2015</td>
      <td>07/24/2017</td>
      <td>11/09/2015</td>
      <td>Y</td>
      <td>6.0</td>
      <td>6.0</td>
      <td>Y</td>
      <td>Y</td>
      <td>11/03/2016</td>
      <td>4000.0</td>
      <td>4000.0</td>
      <td>tourist hotel/motel</td>
      <td>143.0</td>
      <td>retail sales</td>
      <td>39.0</td>
      <td>2.0</td>
      <td>Y</td>
      <td>3.0</td>
      <td>constr type 3</td>
      <td>1.0</td>
      <td>constr type 1</td>
      <td>Y</td>
      <td>3.0</td>
      <td>Tenderloin</td>
      <td>94102.0</td>
      <td>(37.785719256680785, -122.40852313194863)</td>
      <td>1380611233945</td>
    </tr>
    <tr>
      <th>1</th>
      <td>201604195146</td>
      <td>4</td>
      <td>sign - erect</td>
      <td>04/19/2016</td>
      <td>0306</td>
      <td>007</td>
      <td>440</td>
      <td>A</td>
      <td>Geary</td>
      <td>St</td>
      <td>0.0</td>
      <td>A</td>
      <td>remove (e) awning and associated signs.</td>
      <td>issued</td>
      <td>08/03/2017</td>
      <td>04/19/2016</td>
      <td>08/03/2017</td>
      <td>07/24/2017</td>
      <td>08/03/2017</td>
      <td>Y</td>
      <td>7.0</td>
      <td>6.0</td>
      <td>Y</td>
      <td>Y</td>
      <td>12/03/2017</td>
      <td>1.0</td>
      <td>500.0</td>
      <td>tourist hotel/motel</td>
      <td>39.0</td>
      <td>retail sales</td>
      <td>39.0</td>
      <td>2.0</td>
      <td>Y</td>
      <td>3.0</td>
      <td>constr type 3</td>
      <td>1.0</td>
      <td>constr type 1</td>
      <td>Y</td>
      <td>3.0</td>
      <td>Tenderloin</td>
      <td>94102.0</td>
      <td>(37.78733980600732, -122.41063199757738)</td>
      <td>1420164406718</td>
    </tr>
    <tr>
      <th>2</th>
      <td>201605278609</td>
      <td>3</td>
      <td>additions alterations or repairs</td>
      <td>05/27/2016</td>
      <td>0595</td>
      <td>203</td>
      <td>1647</td>
      <td>A</td>
      <td>Pacific</td>
      <td>Av</td>
      <td>0.0</td>
      <td>A</td>
      <td>installation of separating wall</td>
      <td>withdrawn</td>
      <td>09/26/2017</td>
      <td>05/27/2016</td>
      <td>07/18/2017</td>
      <td>07/24/2017</td>
      <td>07/18/2017</td>
      <td>Y</td>
      <td>6.0</td>
      <td>6.0</td>
      <td>Y</td>
      <td>Y</td>
      <td>07/13/2018</td>
      <td>20000.0</td>
      <td>2000.0</td>
      <td>retail sales</td>
      <td>39.0</td>
      <td>retail sales</td>
      <td>39.0</td>
      <td>2.0</td>
      <td>Y</td>
      <td>1.0</td>
      <td>constr type 1</td>
      <td>1.0</td>
      <td>constr type 1</td>
      <td>Y</td>
      <td>3.0</td>
      <td>Russian Hill</td>
      <td>94109.0</td>
      <td>(37.7946573324287, -122.42232562979227)</td>
      <td>1424856504716</td>
    </tr>
    <tr>
      <th>3</th>
      <td>201611072166</td>
      <td>8</td>
      <td>otc alterations permit</td>
      <td>11/07/2016</td>
      <td>0156</td>
      <td>011</td>
      <td>1230</td>
      <td>A</td>
      <td>Pacific</td>
      <td>Av</td>
      <td>0.0</td>
      <td>A</td>
      <td>repair dryrot &amp; stucco at front of bldg.</td>
      <td>complete</td>
      <td>07/24/2017</td>
      <td>11/07/2016</td>
      <td>07/18/2017</td>
      <td>07/24/2017</td>
      <td>07/18/2017</td>
      <td>Y</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>Y</td>
      <td>Y</td>
      <td>07/13/2018</td>
      <td>2000.0</td>
      <td>2000.0</td>
      <td>1 family dwelling</td>
      <td>1.0</td>
      <td>1 family dwelling</td>
      <td>1.0</td>
      <td>2.0</td>
      <td>Y</td>
      <td>5.0</td>
      <td>wood frame (5)</td>
      <td>5.0</td>
      <td>wood frame (5)</td>
      <td>Y</td>
      <td>3.0</td>
      <td>Nob Hill</td>
      <td>94109.0</td>
      <td>(37.79595867909168, -122.41557405519474)</td>
      <td>1443574295566</td>
    </tr>
    <tr>
      <th>4</th>
      <td>201611283529</td>
      <td>6</td>
      <td>demolitions</td>
      <td>11/28/2016</td>
      <td>0342</td>
      <td>001</td>
      <td>950</td>
      <td>A</td>
      <td>Market</td>
      <td>St</td>
      <td>0.0</td>
      <td>A</td>
      <td>demolish retail/office/commercial 3-story buil...</td>
      <td>issued</td>
      <td>12/01/2017</td>
      <td>11/28/2016</td>
      <td>12/01/2017</td>
      <td>07/12/2017</td>
      <td>11/20/2017</td>
      <td>Y</td>
      <td>3.0</td>
      <td>5.0</td>
      <td>Y</td>
      <td>Y</td>
      <td>12/01/2018</td>
      <td>100000.0</td>
      <td>100000.0</td>
      <td>retail sales</td>
      <td>326.0</td>
      <td>apartments</td>
      <td>326.0</td>
      <td>2.0</td>
      <td>Y</td>
      <td>3.0</td>
      <td>constr type 3</td>
      <td>1.0</td>
      <td>constr type 1</td>
      <td>Y</td>
      <td>6.0</td>
      <td>Tenderloin</td>
      <td>94102.0</td>
      <td>(37.78315261897309, -122.40950883997789)</td>
      <td>144548169992</td>
    </tr>
  </tbody>
</table>
</div>



#### Verify if the missing values have been filled


```python
# getting the number of missing data points per column
sf_missing_values_count_fill = sf_permits_fill.isnull().sum()
sf_missing_values_count_fill
```




    Permit Number                             0
    Permit Type                               0
    Permit Type Definition                    0
    Permit Creation Date                      0
    Block                                     0
    Lot                                       0
    Street Number                             0
    Street Number Suffix                      0
    Street Name                               0
    Street Suffix                             0
    Unit                                      0
    Unit Suffix                               0
    Description                               0
    Current Status                            0
    Current Status Date                       0
    Filed Date                                0
    Issued Date                               0
    Completed Date                            0
    First Construction Document Date          0
    Structural Notification                   0
    Number of Existing Stories                0
    Number of Proposed Stories                0
    Voluntary Soft-Story Retrofit             0
    Fire Only Permit                          0
    Permit Expiration Date                    0
    Estimated Cost                            0
    Revised Cost                              0
    Existing Use                              0
    Existing Units                            0
    Proposed Use                              0
    Proposed Units                            0
    Plansets                                  0
    TIDF Compliance                           0
    Existing Construction Type                0
    Existing Construction Type Description    0
    Proposed Construction Type                0
    Proposed Construction Type Description    0
    Site Permit                               0
    Supervisor District                       0
    Neighborhoods - Analysis Boundaries       0
    Zipcode                                   0
    Location                                  0
    Record ID                                 0
    dtype: int64



## Conclusion

The dataset preprocessing is a very crucial step in any data science project. Its only after a through process of cleaning and handling missing values in a dataset, that we can more confidently move forward to Exploratory data analysis and Modeling in depth. In this particular exercise we looked at the following stages of the cleaning process.
1. Taking a first look at the data
2. See how many missing data points are present
3. Figure out why the data is missing
4. Drop missing values
5. Filling in missing values

Ultimately all the stages are important in ensuring a clean and ready dataset for analysis. There will obviously be variations in terms of the depth and scope  of application to different datasets. The biggest differentiator will be in terms of how dirty or clean a dataset is.
