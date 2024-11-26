# DATA-ENGINEERING-LAB-3

Lab Exercise 1: Analyzing Wikipedia Pageviews

**Dataset Overview**
The Wikipedia Pageviews dataset records user interactions with Wikipedia pages, including:
*Date
*Time
*Language
*Title
*View Counts

This dataset provides insights into web traffic, user behavior, and content trends. Students can analyze traffic patterns, evaluate topics, and practice big data techniques to derive actionable insights from large-scale datasets.

**Prerequisites**

Create a Dataproc cluster with Jupyter & Component Gateway on Google Cloud Platform (GCP).


**Objective**

By the end of this lab, you will be able to:
Use Spark DataFrames and SQL to retrieve and manipulate Wikipedia page views data.
Write the data to BigQuery (a data warehouse on GCP) and query the data for insights.
Tasks
Follow the instructions on the provided link to complete the tasks:

**Read the BigQuery table into a Spark DataFrame.**

Filter for the English version of Wikipedia for both desktop and mobile versions ('en' and 'en.m') with more than 100 views.
Group by title and order by page views to see the top pages.
Write the Spark DataFrame to a BigQuery table.
Retrieve the top 10 most-viewed pages where the title contains the word "United."
Perform the same transformations using Spark SQL.
Visualize the total views across datehour using Pandas plotting.

**Additional Resources**


Repo Instructions Page (https://github.com/GoogleCloudDataproc/cloud-dataproc/blob/master/notebooks/python/1.1.%20BigQuery%20Storage%20%26%20Spark%20DataFrames%20-%20Python.ipynb)

Steps to Use Spark SQL (https://github.com/GoogleCloudDataproc/cloud-dataproc/blob/master/notebooks/python/1.2.%20BigQuery%20Storage%20%26%20Spark%20SQL%20-%20Python.ipynb)

Steps to Pandas Plotting (https://github.com/GoogleCloudDataproc/cloud-dataproc/blob/master/notebooks/python/3.1.%20Spark%20DataFrame%20%26%20Pandas%20Plotting%20-%20Python.ipynb)


****Lab Exercise 2:****

**Creating a Streaming Data Pipeline with Kafka

Overview**

In this provisioned lab environment, you will create a streaming data pipeline using Kafka, providing a hands-on look at the Kafka Streams API. You will run a Java application that showcases a simple end-to-end data pipeline powered by Apache Kafka.


**Prerequisites**

An account on Cloud Skills Boost(https://www.cloudskillsboost.google/).


**Objective**

By the end of this lab, you will be able to:
Start a Kafka cluster on a Compute Engine single machine.
Write example input data to a Kafka topic using the console producer included in Kafka.
Process the input data and inspect the output data using the console consumer.

Setup and Requirements

Before you click the Start Lab button, read and follow the instructions. The lab is timed, and you cannot pause it.


**Tasks**

Follow the instructions on the provided link to complete the tasks:

**Set up Kafka.**

Prepare the topics and the input data.
Process the input data with Kafka Streams.
Inspect the output data.
Stop the Kafka cluster.

Additional Resources

Link to Lab (https://www.cloudskillsboost.google/course_templates/703/labs/502033)
