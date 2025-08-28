## [get-started-sql-and-bigQuery](https://www.kaggle.com/code/dansbecker/getting-started-with-sql-and-bigquery)

--> Bigquery: web service to apply SQL to huge datasets

--> your 1st bigQuery Commands

```
from google.cloud import bigquery
```

--> create a client Object:

```
# Create a "Client" object
client = bigquery.Client()
```

- start with a dataset of posts in [Hacker News](https://news.ycombinator.com/)

hacker news dataset is contained in bigquery-public-data:
	- build a reference with dataset() method
	- use get_dataset() along with reference to fetch the dataset

```
# Construct a reference to the "hacker_news" dataset
dataset_ref = client.dataset("hacker_news", project="bigquery-public-data")

# API request - fetch the dataset
dataset = client.get_dataset(dataset_ref)
```

--> dataset = spreadsheet with multiple tables

use list_tables() to list tables in dataset

```
# List all the tables in the "hacker_news" dataset
tables = list(client.list_tables(dataset))

# Print names of all tables in the dataset (there are four!)
for table in tables:  
    print(table.table_id)
```

--> fetch a full table inside hacker_news dataset:

```
# Construct a reference to the "full" table
table_ref = dataset_ref.table("full")

# API request - fetch the table
table = client.get_table(table_ref)
```

--> client object hold projects + bigquery connection
	- bigquery-public-data is a project ( collection of datasets
	- hacker_news is a dataset (collection of tables)
	- comments, full, full_201510 are tables


--> Table Schema - the structure of a table

```
# Print information on all the columns in the "full" table in the "hacker_news" dataset
table.schema
```

	- use list_rows() method to check 1st five lines of full table --> returns bigquery RowIterator object 
		- convert to pandas DataFrame with the to_dataframe() method

```
# Preview the first five lines of the "full" table
client.list_rows(table, max_results=5).to_dataframe()
```

--> can also check info at specific column 
	- example: 1st five entries in the by column:

```
# Preview the first five entries in the "by" column of the "full" table
client.list_rows(table, selected_fields=table.schema[:1], max_results=5).to_dataframe()
```

--> Disclaimer: Each Kaggle user can scan 5TB every 30 days for free. Once you hit that limit, you'll have to wait for it to reset.


------

exercises:


-------

## [select-from-where](https://www.kaggle.com/code/dansbecker/select-from-where)

	- start with imaginary dataset 'pet_records'

--> SELECT... FROM
	- FROM `table` --> use backticks(`)

--> WHERE ...
	- filter by condition.
	- Example: What are all the U.S. cities in the OpenAQ dataset?

check [openAQ dataset](https://openaq.org/)

	- 1st: check tables in the dataset:

```
from google.cloud import bigquery

# Create a "Client" object
client = bigquery.Client()

# Construct a reference to the "openaq" dataset
dataset_ref = client.dataset("openaq", project="bigquery-public-data")

# API request - fetch the dataset
dataset = client.get_dataset(dataset_ref)

# List all the tables in the "openaq" dataset
tables = list(client.list_tables(dataset))

# Print names of all tables in the dataset (there's only one!)
for table in tables:  
    print(table.table_id
```

- only one table was found: global_air_quality - fetch the table an check 1st rows to see data

```
# Construct a reference to the "global_air_quality" table
table_ref = dataset_ref.table("global_air_quality")

# API request - fetch the table
table = client.get_table(table_ref)

# Preview the first five lines of the "global_air_quality" table
client.list_rows(table, max_results=5).to_dataframe()
```

example: get all values from 'city' column that has 'country' = 'US'

```
# Query to select all the items from the "city" column where the "country" column is 'US'
query = """
        SELECT city
        FROM `bigquery-public-data.openaq.global_air_quality`
        WHERE country = 'US'
        """
```


--> Submit query to dataset
	-1st step: create Client object:

```
# Create a "Client" object
client = bigquery.Client()
```

run query() with default parameters: check [manual](https://google-cloud.readthedocs.io/en/latest/bigquery/generated/google.cloud.bigquery.client.Client.query.html#google.cloud.bigquery.client.Client.query)

```
# Set up the query
query_job = client.query(query)
```

--> run query and convert results to pd.DataFrame:

```
# API request - run the query, and return a pandas DataFrame
us_cities = query_job.to_dataframe()
```

- what 5 cities has most measurements?

```
# What five cities have the most measurements?
us_cities.city.value_counts().head()
```

--> more queries
	-get multiple columns using comma between names:

``` 
query = """
        SELECT city, country
        FROM `bigquery-public-data.openaq.global_air_quality`
        WHERE country = 'US'
        """
```

--> select all columns with '*'

```
query = """
        SELECT *
        FROM `bigquery-public-data.openaq.global_air_quality`
        WHERE country = 'US'
        """
```

--> Q&A: Notes on formatting
	- triple quotaion marks (""") to indicate single string that is broken in pieces
	- SELECT and FROM in capital letters? no need for this

--> working with BIG datasets:
	- Each Kaggle user can scan 5TB every 30 days for free. Once you hit that limit, you'll have to wait for it to reset.
	- biggest dataset is 3TB [here](https://www.kaggle.com/github/github-repos)

--> check how much data a query will scan:

```
# Query to get the score column from every row where the type column has value "job"
query = """
        SELECT score, title
        FROM `bigquery-public-data.hacker_news.full`
        WHERE type = "job" 
        """

# Create a QueryJobConfig object to estimate size of query without running it
dry_run_config = bigquery.QueryJobConfig(dry_run=True)

# API request - dry run query to estimate costs
dry_run_query_job = client.query(query, job_config=dry_run_config)

print("This query will process {} bytes.".format(dry_run_query_job.total_bytes_processed))
```

--> you can place a limiter to data that will be scanned:

```
# Only run the query if it's less than 1 MB
ONE_MB = 1000*1000
safe_config = bigquery.QueryJobConfig(maximum_bytes_billed=ONE_MB)

# Set up the query (will only run if it's less than 1 MB)
safe_query_job = client.query(query, job_config=safe_config)

# API request - try to run the query, and return a pandas DataFrame
safe_query_job.to_dataframe()
```

--> query will be cancelled if limit is exceeded:

```
# Only run the query if it's less than 1 GB
ONE_GB = 1000*1000*1000
safe_config = bigquery.QueryJobConfig(maximum_bytes_billed=ONE_GB)

# Set up the query (will only run if it's less than 1 GB)
safe_query_job = client.query(query, job_config=safe_config)

# API request - try to run the query, and return a pandas DataFrame
job_post_scores = safe_query_job.to_dataframe()

# Print average score for job posts
job_post_scores.score.mean()
```

-------

Exercises


-------

## [GroupBy-having-count](https://www.kaggle.com/code/dansbecker/group-by-having-count)

--> Intro
	- keep using made up info on pets


--> COUNT()
	- pass name of a column --> it counts entries in the column
	- aggregate function (takes many values and return one)
		- others are: sum(), avg(), min() and max()

--> Group by
	- takes name of 1+ columns treats all rows with that same value as a single group 
		- when applying aggregate fucntions
	- example: get count of all rows by the Animal column ( how many rabbits, dogs and cats?)

---> Group by... Having
	-use a condition for having 


- Example: Which Hacker News comments generated the most discussion?

```
from google.cloud import bigquery

# Create a "Client" object
client = bigquery.Client()

# Construct a reference to the "hacker_news" dataset
dataset_ref = client.dataset("hacker_news", project="bigquery-public-data")

# API request - fetch the dataset
dataset = client.get_dataset(dataset_ref)

# Construct a reference to the "comments" table
table_ref = dataset_ref.table("comments")

# API request - fetch the table
table = client.get_table(table_ref)

# Preview the first five lines of the "comments" table
client.list_rows(table, max_results=5).to_dataframe()
```

- 'parent' column has the 1st comment and 'id' column is the unique key
	-groupby parent and count id
	-only return comments that has more than 10 replies:

```
# Query to select comments that received more than 10 replies
query_popular = """
                SELECT parent, COUNT(id)
                FROM `bigquery-public-data.hacker_news.comments`
                GROUP BY parent
                HAVING COUNT(id) > 10
                """
```

 -when query is ready -- run and store it in a DataFrame

```
# Set up the query (cancel the query if it would use too much of 
# your quota, with the limit set to 10 GB)
safe_config = bigquery.QueryJobConfig(maximum_bytes_billed=10**10)
query_job = client.query(query_popular, job_config=safe_config)

# API request - run the query, and convert the results to a pandas DataFrame
popular_comments = query_job.to_dataframe()

# Print the first five rows of the DataFrame
popular_comments.head()
```


--> aliasing and other improvements
	- make your queries even better --> give a more descriptive name for the resulting columns of your queries:
	- use 'AS NumPosts' after specifying aggregation
- use count(1) to count rows in each group --> scans less data

 - rewrite query:
```
# Improved version of earlier query, now with aliasing & improved readability
query_improved = """
                 SELECT parent, COUNT(1) AS NumPosts
                 FROM `bigquery-public-data.hacker_news.comments`
                 GROUP BY parent
                 HAVING COUNT(1) > 10
                 """

safe_config = bigquery.QueryJobConfig(maximum_bytes_billed=10**10)
query_job = client.query(query_improved, job_config=safe_config)

# API request - run the query, and convert the results to a pandas DataFrame
improved_df = query_job.to_dataframe()

# Print the first five rows of the DataFrame
improved_df.head()
```

---> note on using Group BY
	- dont use GroupBy without an aggregate function

```
query_good = """
             SELECT parent, COUNT(id)
             FROM `bigquery-public-data.hacker_news.comments`
             GROUP BY parent
             """
```

- 2 variables: parent and id:
	
- the following is a bad query exapmle:
```
query_bad = """
            SELECT author, parent, COUNT(id)
            FROM `bigquery-public-data.hacker_news.comments`
            GROUP BY parent
            """
```

- this query returns error: If make this error, you'll get the error message `SELECT list expression references column (column's name) which is neither grouped nor aggregated at`.

-------

Exercises


-------


## [Order By](https://www.kaggle.com/code/dansbecker/order-by)

--> Intro: learn to change order of your results with ORDER BY
	-usually the last clause
	- can use ORDER BY column DESC --> to reverse order

--> DAtes
	- store as DATE or DATETIME
	- DATE = YYYY-MM-DD
	- DATETIME = yyyy-mm-dd hh-mm-ss

--> Extract
	-to extract part of a date
	- check all functions that can be used with dates in [BigQuery](https://cloud.google.com/bigquery/docs/reference/legacy-sql#datetimefunctions)

- Example: which day of week has most fatal motor accidents?
	- cehck accident_2015 table

```
from google.cloud import bigquery

# Create a "Client" object
client = bigquery.Client()

# Construct a reference to the "nhtsa_traffic_fatalities" dataset
dataset_ref = client.dataset("nhtsa_traffic_fatalities", project="bigquery-public-data")

# API request - fetch the dataset
dataset = client.get_dataset(dataset_ref)

# Construct a reference to the "accident_2015" table
table_ref = dataset_ref.table("accident_2015")

# API request - fetch the table
table = client.get_table(table_ref)

# Preview the first five lines of the "accident_2015" table
client.list_rows(table, max_results=5).to_dataframe()
```

- use ORDER BY to get the days with most accidents:
```
# Query to find out the number of accidents for each day of the week
query = """
        SELECT COUNT(consecutive_number) AS num_accidents, 
               EXTRACT(DAYOFWEEK FROM timestamp_of_crash) AS day_of_week
        FROM `bigquery-public-data.nhtsa_traffic_fatalities.accident_2015`
        GROUP BY day_of_week
        ORDER BY num_accidents DESC
        """
```

- run it as follows:

```
# Set up the query (cancel the query if it would use too much of 
# your quota, with the limit set to 1 GB)
safe_config = bigquery.QueryJobConfig(maximum_bytes_billed=10**9)
query_job = client.query(query, job_config=safe_config)

# API request - run the query, and convert the results to a pandas DataFrame
accidents_by_day = query_job.to_dataframe()

# Print the DataFrame
accidents_by_day
```


