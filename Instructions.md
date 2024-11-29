# WIKIPEDIA DATASET


## Lab Exercise 1

### Dataset 

The Wikipedia Pageviews dataset records user interactions with Wikipedia pages,
including date, time, language, title, and view counts. It offers insights into web traffic, user
behavior, and content trends. For a project, students can analyze traffic patterns, evaluate
topics, and practice big data techniques to derive actionable insights from large-scale
datasets.

### Prerequisites: 

Create a Dataproc cluster with Jupyter & Component Gateway on GCP.

Set Up Apache Spark and Jupyter Notebooks on Dataproc (https://github.com/josephtugah/spark-tutorials/blob/main/gcp-spark-jupyter-setup/README(dataproc-jupyter).md)

## Objective:

By the end of this lab, you will be able to use Spark DataFrames and SQL to
retrieve and manipulate Wikipedia page views data, write the data to BigQuery (a data
warehouse on GCP) and query the data for insights.

### Tasks:

Follow the instructions on the page via this link to perform the tasks ( [Repo
Instructions Page](https://github.com/josephtugah/spark-tutorials/blob/main/gcp-spark-jupyter-setup/README(dataproc-jupyter).md) )

Task 1: Read the Bigquery table into Spark DataFrame.

Task 2: Filter for English version of Wikipedia for both desktop and mobile versions (‘en’ and
‘en.m’) with more than 100 views

Task 3: Group by title and order by page views to see the top pages.

Task 4: Write the spark Dataframe to a BigQuery table

Task 5: Write a query to retrieve the top 10 most-viewed pages where the title contains the
word "United".

Task 6: Repeat the same steps but perform the transformations using Spark SQL ([Steps to
Use Spark SQL](https://github.com/GoogleCloudDataproc/cloud-dataproc/blob/master/notebooks/python/1.2.%20BigQuery%20Storage%20%26%20Spark%20SQL%20-%20Python.ipynb))

Task 7: Visualize the total views across datehour using Pandas plotting ( [Steps to Pandas
Plotting](https://github.com/GoogleCloudDataproc/cloud-dataproc/blob/master/notebooks/python/3.1.%20Spark%20DataFrame%20%26%20Pandas%20Plotting%20-%20Python.ipynb) )



## Lab Exercise 2

Task 1. Open an interactive shell with your docker container using command prompt
    
Task 2. Create a Kafka topic on your broker with 3 partitions and write a command to describe the Kafka topic
    
Task 3. Write a spark application to read the device data from the topic and to write it a console sink
   
Task 4. Create a Kafka producer and post a sample device data to your Kafka topic
   
Task 5. Write the stream to the console
   
Task 6. Post more data into the Kafka producer
   
Task 7. Inspect the output data in your docker container logs
 
