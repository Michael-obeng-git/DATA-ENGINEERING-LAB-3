Create Spark Session
Include the correct version of the spark-bigquery-connector jar

Scala version 2.11 - 'gs://spark-lib/bigquery/spark-bigquery-latest.jar'.

Scala version 2.12 - 'gs://spark-lib/bigquery/spark-bigquery-latest_2.12.jar'.

from pyspark.sql import SparkSession
spark = SparkSession.builder \
  .appName('1.1. BigQuery Storage & Spark DataFrames - Python')\
  .config('spark.jars', 'gs://spark-lib/bigquery/spark-bigquery-latest.jar') \
  .getOrCreate()
Enable repl.eagerEval
This will output the results of DataFrames in each step without the new need to show df.show() and also improves the formatting of the output

spark.conf.set("spark.sql.repl.eagerEval.enabled",True)
Read BigQuery table into Spark DataFrame
Use filter() to query data from a partitioned table.

table = "bigquery-public-data.wikipedia.pageviews_2020"
df_wiki_pageviews = spark.read \
  .format("bigquery") \
  .option("table", table) \
  .option("filter", "datehour >= '2020-03-01' AND datehour < '2020-03-02'") \
  .load()

df_wiki_pageviews.printSchema()
root
 |-- datehour: timestamp (nullable = true)
 |-- wiki: string (nullable = true)
 |-- title: string (nullable = true)
 |-- views: long (nullable = true)

Select required columns and apply a filter using where() which is an alias for filter() then cache the table

df_wiki_en = df_wiki_pageviews \
  .select("title", "wiki", "views") \
  .where("views > 1000 AND wiki in ('en', 'en.m')") \
  .cache()

df_wiki_en
title	wiki	views
2020_Democratic_P...	en	3242
Eurovision_Song_C...	en	2368
Colin_McRae	en	2360
Donald_trump	en	2223
Comparison_of_onl...	en	1398
Coronavirus	en	1872
-	en	136620
Bombshell_(2019_f...	en	1084
Brooklyn	en	1946
2019–20_coronavir...	en	8313
2019–20_Wuhan_cor...	en	1084
Apple_Network_Server	en	3524
Catholic_moral_th...	en	1328
Bernie_Sanders	en	1297
2019–20_coronavir...	en	1968
Brooklyn	en	1139
Charlie's_Angels_...	en	1006
Corrupted_Blood_i...	en	1511
Donald_trump	en	1526
Coronavirus_disea...	en	1405
only showing top 20 rows
Group by title and order by page views to see the top pages

import pyspark.sql.functions as F

df_wiki_en_totals = df_wiki_en \
.groupBy("title") \
.agg(F.sum('views').alias('total_views'))

df_wiki_en_totals.orderBy('total_views', ascending=False)
title	total_views
Main_Page	10939337
United_States_Senate	5619797
-	3852360
Special:Search	1538334
2019–20_coronavir...	407042
2020_Democratic_P...	260093
Coronavirus	254861
The_Invisible_Man...	233718
Super_Tuesday	201077
Colin_McRae	200219
David_Byrne	189989
2019–20_coronavir...	156803
John_Mulaney	155605
2020_South_Caroli...	152137
AEW_Revolution	140503
Boris_Johnson	120957
Tom_Steyer	120926
Dyatlov_Pass_inci...	117704
Spanish_flu	108335
2020_coronavirus_...	107653
only showing top 20 rows
Write Spark Dataframe to BigQuery table
Write the Spark Dataframe to BigQuery table using BigQuery Storage connector. This will also create the table if it does not exist. The GCS bucket and BigQuery dataset must already exist.

If the GCS bucket and BigQuery dataset do not exist they will need to be created before running df.write

Instructions here for creating a GCS bucket
Instructions here for creating a BigQuery Dataset
# Update to your GCS bucket
gcs_bucket = 'dataproc-bucket-name'

# Update to your BigQuery dataset name you created
bq_dataset = 'dataset_name'

# Enter BigQuery table name you want to create or overwite. 
# If the table does not exist it will be created when you run the write function
bq_table = 'wiki_total_pageviews'

df_wiki_en_totals.write \
  .format("bigquery") \
  .option("table","{}.{}".format(bq_dataset, bq_table)) \
  .option("temporaryGcsBucket", gcs_bucket) \
  .mode('overwrite') \
  .save()
Use BigQuery magic to query table
Use the BigQuery magic to check if the data was created successfully in BigQuery. This will run the SQL query in BigQuery and the return the results

%%bigquery
SELECT title, total_views
FROM dataset_name.wiki_total_pageviews
ORDER BY total_views DESC
LIMIT 10
title	total_views
0	Main_Page	10939337
1	United_States_Senate	5619797
2	-	3852360
3	Special:Search	1538334
4	2019–20_coronavirus_outbreak	407042
5	2020_Democratic_Party_presidential_primaries	260093
6	Coronavirus	254861
7	The_Invisible_Man_(2020_film)	233718
8	Super_Tuesday	201077
9	Colin_McRae	200219
