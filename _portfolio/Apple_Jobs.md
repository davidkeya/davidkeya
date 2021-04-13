---
header:
  overlay_image: /assets/images/data_pipelines/apple.jpg
  caption: "Photo credit: [**Carl Heyerdahl**](https://unsplash.com)"
permalink: /portfolio/Apple_jobs/
date: 2020-11-15
toc: true
toc_label: "Contents"
---

# Creating Data Pipelines From Raw Data Using SQL
A data pipeline is a series of data processing steps. If the data is not currently loaded into the data platform, then it is ingested at the beginning of the pipeline. Then there are a series of steps in which each step delivers an output that is the input to the next step. This continues until the pipeline is complete. In some cases, independent steps may be run in parallel.

## Data Wrangling
Data wrangling is the process of gathering data, assessing it for quality and cleaning.

![wrangle.png](/assets/images/data_pipelines/wrangle.png)

## Data Transformation
Data transformation refers to operations that change data.This may include data standardization, sorting,duplication,validation and verification.The ultimate goal here is to make it possible to analyze data.
![transformation.png](/assets/images/data_pipelines/transformation.png)
Transforming raw data into clean readable and usable data is very important for any data scientist,data analyst or data engineer.The focus here will be to create a reliable data pipeline from the apple jobs dataset.

In this case, I am going to explore and manipulate a live table that stores all Apple's job listings using SQL, with the following goals.

* Show all the distinct skills mentioned.

* Extract a count of each skill mentioned segmented by state.

 ## PostgreSQL
I make use of PostgreSQL an advanced, enterprise class open source relational database that supports both SQL (relational) and JSON (non-relational) querying. SQL IDEs are not capable of visualizing data and to go around this, I run and visualize the results of a query using Jupyter notebook.


## Using ipython-sql
ipython-sql enables us to run SQL queries directly from a Jupyter Notebook. No need to write multiple lines of code to connect to the database or wrap the query in a string. ipython-sql makes querying a database from Jupyter Notebook “cleaner”.
ipython-sql can be installed simply by running "!pip install ipython-sql, then load the sql module.


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


## Getting Started


```python
# Load ipython-sql, using the following magic command:
%load_ext sql
```


```python
# Next, we will only need the create_engine() function from sqlalchemy so let’s import that with the following line:
from sqlalchemy import create_engine
```

## Connect to a PostgreSQL the database
Once we’ve laid the groundwork, we can now connect to a PostgreSQL database!
The PostgreSQL database contains apple's jobs listing in portfolio database.


```python
# To connect ipython-sql to database, use the following format
%sql postgresql://postgres:1372Sql$@localhost/portfolio
```


```python
# To connect sqlalchemy to the database
engine = create_engine('postgresql://postgres:1372Sql$@localhost/portfolio')
```

## An exploration of the live table storing all of the Apples's jobs llistings


**Explore rows and columns from the 'apple_jobs' table**


```sql
%%sql
SELECT * FROM apple_jobs
LIMIT 1

```

     * postgresql://postgres:***@localhost/portfolio
    1 rows affected.





<table>
    <tr>
        <th>title</th>
        <th>location</th>
        <th>minimum_qual</th>
        <th>preferred_qual</th>
        <th>responsibilities</th>
        <th>education_experience</th>
    </tr>
    <tr>
        <td>Software Technician</td>
        <td>Santa Clara Valley (Cupertino), California, United States</td>
        <td>2-5 years experience supporting or deploying application software for internal and external customers.<br>Experience configuring or maintaining commercial enterprise application software packages (for example: inventory systems, manufacturing systems, PDM, ERP, LIMS, etc…)<br>Experience providing first level software support to end users and issue triage<br>Proven problem solving and debugging skills<br>Comfortable with modern IT tech-stack concepts<br>Ability to navigate in a Linux/Unix environment<br>Able to train small and large groups<br>Able to write and execute basic database queries<br>You will be self directed, analytical, and work well in a team environment<br>Be a strong advocate for improving processes and a clear communicator of new ideas<br>Strong verbal interpersonal skills<br>Highly organized, ability to juggle multiple priorities at a time<br>Ability to quickly learn new software applications</td>
        <td>None</td>
        <td>As a software techician, you will assist with deployments and provide ongoing assistance to our internal Apple Battery Engineering customers.</td>
        <td>AS/BS in Information Technology, or equivalent</td>
    </tr>
</table>



>The table has 2148 rows and 6 columns
1. title - Describes the title of all jobs listed.
2. location - Specific locations for all the listed jobs (city, state, country).
3. minimum_qual - The minimum requirements for listed job.
4. preferred_qual - The good to have qualifications
5. responsibilities - Key role on the job
6. education_experience - Education and experience requirement for the job


```python
# Store the querry results in variable
results = %sql SELECT * FROM apple_jobs
```

     * postgresql://postgres:***@localhost/portfolio
    2148 rows affected.



```python
# Convert the table into a pandas data frame
df = results.DataFrame()
```


```python
# The first five rows of the data frame
df.head(5)
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
      <th>title</th>
      <th>location</th>
      <th>minimum_qual</th>
      <th>preferred_qual</th>
      <th>responsibilities</th>
      <th>education_experience</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Software Technician</td>
      <td>Santa Clara Valley (Cupertino), California, Un...</td>
      <td>2-5 years experience supporting or deploying a...</td>
      <td>None</td>
      <td>As a software techician, you will assist with ...</td>
      <td>AS/BS in Information Technology, or equivalent</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Software Engineer</td>
      <td>Santa Clara Valley (Cupertino), California, Un...</td>
      <td>KEY QUALIFICATIONS\nA genuine passion for fixi...</td>
      <td>ADDITIONAL REQUIREMENTS\nReal hands-on experie...</td>
      <td>DESCRIPTION\nWork with multi-functional teams ...</td>
      <td>EDUCATION\nBS or MS in Computer Engineering or...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Software Engineer</td>
      <td>Santa Clara Valley (Cupertino), California, Un...</td>
      <td>- 3+ years experience working on large scale d...</td>
      <td>None</td>
      <td>This position will design, implement and debug...</td>
      <td>BS, MS or PhD, in Computer Science, or equival...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Software Engineer</td>
      <td>Santa Clara Valley (Cupertino), California, Un...</td>
      <td>- 3+ years experience working on large scale d...</td>
      <td>None</td>
      <td>This position will design, implement and debug...</td>
      <td>BS, MS or PhD, in Computer Science, or equival...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Software Engineer</td>
      <td>Santa Clara Valley (Cupertino), California, Un...</td>
      <td>Demonstrated experience integrating full-syste...</td>
      <td>None</td>
      <td>Extraordinary planning, critical thinking, and...</td>
      <td>M.S. or PhD in Computer Science, Electrical En...</td>
    </tr>
  </tbody>
</table>
</div>



## The desired goal
The objective is to manipulate the available table to shows all of the *distinct skills* mentioned, as well as a *count of each skill* mentioned segmented *by state*.In summary,

- Visualize distinct skills
- Count of each skill
- Segment by state

### Segmentation by state
Let's filter the table to segment all the information by state. To achieve this, we make use of the location column. The location column stores the names of the city, state and country of each job listing in the table. Lets apply a suitable SQL querry to filter out the location column by state and display only the names of states for all the job listings.

#### Zero in on the location column


```sql
%%sql
SELECT * FROM apple_jobs
LIMIT 1
```

     * postgresql://postgres:***@localhost/portfolio
    1 rows affected.





<table>
    <tr>
        <th>title</th>
        <th>location</th>
        <th>minimum_qual</th>
        <th>preferred_qual</th>
        <th>responsibilities</th>
        <th>education_experience</th>
    </tr>
    <tr>
        <td>Software Technician</td>
        <td>Santa Clara Valley (Cupertino), California, United States</td>
        <td>2-5 years experience supporting or deploying application software for internal and external customers.<br>Experience configuring or maintaining commercial enterprise application software packages (for example: inventory systems, manufacturing systems, PDM, ERP, LIMS, etc…)<br>Experience providing first level software support to end users and issue triage<br>Proven problem solving and debugging skills<br>Comfortable with modern IT tech-stack concepts<br>Ability to navigate in a Linux/Unix environment<br>Able to train small and large groups<br>Able to write and execute basic database queries<br>You will be self directed, analytical, and work well in a team environment<br>Be a strong advocate for improving processes and a clear communicator of new ideas<br>Strong verbal interpersonal skills<br>Highly organized, ability to juggle multiple priorities at a time<br>Ability to quickly learn new software applications</td>
        <td>None</td>
        <td>As a software techician, you will assist with deployments and provide ongoing assistance to our internal Apple Battery Engineering customers.</td>
        <td>AS/BS in Information Technology, or equivalent</td>
    </tr>
</table>



#### Split location column to city, state and country


```sql
%%sql
SELECT
    title,

    split_part(location::TEXT,',', 1) city,
    split_part(location::TEXT,',', 2) state,
    split_part(location::TEXT,',', 3) country,

    minimum_qual,
    preferred_qual,
    responsibilities,
    education_experience

FROM apple_jobs
LIMIT 1;
```

     * postgresql://postgres:***@localhost/portfolio
    1 rows affected.





<table>
    <tr>
        <th>title</th>
        <th>city</th>
        <th>state</th>
        <th>country</th>
        <th>minimum_qual</th>
        <th>preferred_qual</th>
        <th>responsibilities</th>
        <th>education_experience</th>
    </tr>
    <tr>
        <td>Software Technician</td>
        <td>Santa Clara Valley (Cupertino)</td>
        <td> California</td>
        <td> United States</td>
        <td>2-5 years experience supporting or deploying application software for internal and external customers.<br>Experience configuring or maintaining commercial enterprise application software packages (for example: inventory systems, manufacturing systems, PDM, ERP, LIMS, etc…)<br>Experience providing first level software support to end users and issue triage<br>Proven problem solving and debugging skills<br>Comfortable with modern IT tech-stack concepts<br>Ability to navigate in a Linux/Unix environment<br>Able to train small and large groups<br>Able to write and execute basic database queries<br>You will be self directed, analytical, and work well in a team environment<br>Be a strong advocate for improving processes and a clear communicator of new ideas<br>Strong verbal interpersonal skills<br>Highly organized, ability to juggle multiple priorities at a time<br>Ability to quickly learn new software applications</td>
        <td>None</td>
        <td>As a software techician, you will assist with deployments and provide ongoing assistance to our internal Apple Battery Engineering customers.</td>
        <td>AS/BS in Information Technology, or equivalent</td>
    </tr>
</table>



#### Convert Table to Pandas dataframe , analyze skills per state
All of the distinct skills mentioned, as well as a count of each skill mentioned segmented by state


```python
# Store the querry results in skills_var variable
skills_table = %sql SELECT title, split_part(location::TEXT,',', 1) city, split_part(location::TEXT,',', 2) state, split_part(location::TEXT,',', 3) country, minimum_qual, preferred_qual, responsibilities, education_experience FROM apple_jobs ORDER BY state

```

     * postgresql://postgres:***@localhost/portfolio
    2148 rows affected.



```python
# Convert the table into a pandas data frame
skills_df = skills_table.DataFrame()
```


```python
# The first five rows of the data frame
skills_df.head(5)
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
      <th>title</th>
      <th>city</th>
      <th>state</th>
      <th>country</th>
      <th>minimum_qual</th>
      <th>preferred_qual</th>
      <th>responsibilities</th>
      <th>education_experience</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>CAE Engineer (Yokohama Technology Center)</td>
      <td>Japan</td>
      <td></td>
      <td></td>
      <td>The ideal candidate will have over 5 years of ...</td>
      <td>Experience in optical testing (MTF, interferom...</td>
      <td>Work on new generation optical component devel...</td>
      <td>Preference is put on current skills, experienc...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>SG-Technical Support Advisor</td>
      <td>Singapore</td>
      <td></td>
      <td></td>
      <td>Strong customer service and communication skil...</td>
      <td>None</td>
      <td>The Technical Support Advisor will provide fir...</td>
      <td>Degree or Diploma preferred plus 1-2 years pro...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>At Home Advisor - Applecare (AUS)</td>
      <td>Australia</td>
      <td></td>
      <td></td>
      <td>Professional troubleshooting expertise or prov...</td>
      <td>None</td>
      <td>As an Apple At Home Advisor, you’ll be support...</td>
      <td>None</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Data Center Break Fix Technician</td>
      <td>Mesa</td>
      <td>Arizona</td>
      <td>United States</td>
      <td>A minimum of 2 or more years experience instal...</td>
      <td>None</td>
      <td>We are seeking a forward-thinking teammate tha...</td>
      <td>Associates or Bachelors degree or relevant exp...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Data Center Break Fix Technician</td>
      <td>Mesa</td>
      <td>Arizona</td>
      <td>United States</td>
      <td>A minimum of 2 or more years experience instal...</td>
      <td>None</td>
      <td>We are seeking a forward-thinking teammate tha...</td>
      <td>Associates or Bachelors degree or relevant exp...</td>
    </tr>
  </tbody>
</table>
</div>




```python
skills_df.minimum_qual.head()
```




    0    The ideal candidate will have over 5 years of ...
    1    Strong customer service and communication skil...
    2    Professional troubleshooting expertise or prov...
    3    A minimum of 2 or more years experience instal...
    4    A minimum of 2 or more years experience instal...
    Name: minimum_qual, dtype: object




```python
# change qual_lst list to string
# using list comprehension
qual_str = ' '.join([str(elem) for elem in qual_lst])

```
