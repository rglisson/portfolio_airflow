# Apache Airflow Demo

![](images/airflow_logo.PNG)

# Introduction & Goals
- The goal of the project was to create a pipeline using Airflow using python, bash, and hive operators


# The Data Set
- Data type: 
  - CSV
  - 3219 rows

![](images/data.PNG)

# Used Tools
- Apache Airflow
  - Apache Airflow is an open-source platform to Author, Schedule, and Monitor workflows.
- How were the tools setup?
  - Used an Ubuntu OS on VirtualBox for the dev environment
  - Installed airflow, celery, crypto, mysql, rabbitmq, redis
- Start airflow
  - airflow webserver (for webserver UI)

![](images/airflow_webserver.PNG)

  - airflow scheduler (allows you to start scheduler and trigger your dags)

![](images/airflow_scheduler.PNG)


# Creating a DAG
- Created file 'twitter_dag.py' in folder /airflow/dags

![](images/twitter_dag.PNG)

# Task 1
- waiting_for_tweets
  - At a given interval of time, this task is checking to see if the file containing the tweets is available
  - Added a connection for sensor operator, to check if a file is in a specified location
  - ![](images/sensor.PNG)
  - ![](images/sensor_1.PNG)

# Task 2
- fetching_tweets
  - fetch tweets from CSV file, format timestamp, drop null columns, export formatted data into 'data_fetched.csv'
  - this script extracts tweet
  - ![](images/fetching_tweet.PNG)

  - added PythonOperator to twitter_dag.py script
  - ![](images/fetching_tweet_1.PNG)

# Task 3
- cleaning_tweets
  - transforming and cleaning data to be loaded
  - new script: 'cleaning_tweet.py'
  - ![](images/cleaning_tweet.PNG)

  - Added cleaning_tweets function to DAG script
  - ![](images/cleaning_tweet_1.PNG)

# Task 4
- storing_tweets
  - push the data into HDFS
  - add the function to the DAG script:
  - ![](images/storing_tweets.PNG)

# Task 5
- loading_tweets
  - load tweets into Hive table
  - add the function to the DAG script:
  - ![](images/loading_tweets.PNG)

# Dependencies
- Organize our tasks in order
  - add the dependencies to the DAG script:
  - ![](images/dependencies.PNG)
  - ![](images/dag_graph.PNG)

# Run DAG
- ![](images/start_dag.PNG)
- Copy CSV file to dags folder and refresh UI
 - ![](images/copy_files.PNG)
- Create Hive table
 - ![](images/hive.PNG)
- Run Hive 'hive'
- Query table
  - ![](images/query.PNG)

- Success:
  - ![](images/query_1.PNG)

# Results
- The DAG successfully ran when the new CSV data file appeared in the desired folder. Normally the data would populate in the folder from the Twitter API, but for the purpose of the demo, I manually copied the CSV file into the folder

# Conclusion
- Apache Airflow is an excellent tool to create an automated pipeline to run Cron jobs at the desired interval of time. A DAG is a collection of tasks designed to run in order using various operators.


