---
share: "true"
---

**Problem Statement**

This week we need to analyze some cooked up clickstream data (containing `user_id`, `timestamp`, `date`) using PySpark. Given this data, we need to find the number of user clicks that happened between `00-06`, `06-12`, `12-18`, `18-24` hours. 

**Solution**

First, we'll need to generate some random clickstream data, containing User ID's and the timestamps of the clicks. We can do this using a simple Python script:

```python
import csv
import random
from datetime import timedelta, datetime

def generate_random_timestamp(base_date = datetime(2025, 1, 1)):
    """
    Generate a random timestamp between base_date and base_date + 1 year
    """
    
    return base_date + timedelta(
        days=random.randint(1, 365),
        hours=random.randint(0, 23),
        minutes=random.randint(0, 59),
        seconds=random.randint(0, 59)
    )

data = [
    (f"User_{i}", generate_random_timestamp()) for i in range(1, 51) 
]

output_file = "clickstream.csv"
with open(output_file, "w", newline="") as f:
    writer = csv.writer(f)
    writer.writerow(["id", "timestamp", "date"])
    writer.writerows((user_id, ts.strftime("%Y-%m-%d %H:%M:%S"), ts.strftime("%Y-%m-%d")) for user_id, ts in data)
```

Running this script will give us a CSV file like this:

```CSV
id,timestamp,date
User_1,2025-08-09 23:51:31,2025-08-09
User_2,2025-12-23 17:55:18,2025-12-23
User_3,2025-11-25 10:30:57,2025-11-25
User_4,2025-12-11 07:16:27,2025-12-11
User_5,2025-11-10 01:47:19,2025-11-10
....
....
User_50,2025-10-26 22:23:32,2025-10-26
```

Save this file somewhere in your storage bucket.

Now that we have our data, we need divide it into 4 bins (`00-06`, `06-12`, `12-18`, `18-24`) based on the hour of the timestamp and then we need to count the number of clicks/occurrences in each bin.

We can use the following PySpark code for doing this task. Make sure to replace the placeholder input and output location in the code with the actual `gsutil` URI:

```python
from pyspark.sql import SparkSession
from pyspark.sql.functions import col, hour, when

spark = SparkSession.builder.appName("count_clicker").getOrCreate()

# file path of the clickstream file stored in google cloud storage bucket
input_file = "gs://<storage_bucket>/clickstream.csv"

# read the csv file into a spark dataframe
data = spark.read.csv(input_file, header=True, inferSchema=True)

# add a new column that extracts the hour from the timestamp
data = data.withColumn("hour", hour(col("timestamp")))

# add a new column that divides data into 4 bins: 00-06, 06-12, 12-18, 18-24
data = data.withColumn(
    "time_interval", 
    when(col("hour") < 6, "00-06").
    when(col("hour") < 12, "06-12").
    when(col("hour") < 18, "12-18").
    when(col("hour") < 24, "18-24")
)

# groupby the time interval to find the number of clicks in each interval
results = data.groupBy("time_interval").count().sort("time_interval")
results.show()

# save the results to a csv file
output_file = "gs://<storage_bucket>/output.csv"
results.toPandas().to_csv(output_file, index=False, header=True)

spark.stop()
```

Save this spark file to your storage bucket as well and note down its `gsutil` URI. We'll need it for creating our PySpark job. Before we can run our PySpark job, we'll first need to create a Dataproc cluster on which our job will run.

Search for Dataproc and create a new Dataproc cluster on Compute Engine. There are a whole host of options which you can configure (compute resources, number of worker nodes, cluster auto deletion, etc). The defaults are a bit overkill for such a simple task so you can tone it down a bit and choose lower end hardware. 
Once the cluster is provisioned, we can submit a job. Go to the jobs section, select the cluster that we created earlier and set the job type to `PySpark`. In the main python file section, specify the `gsutil` URI of the PySpark file we just created. It will be responsible for running the job. 

Once the job runs successfully, we'll get an output counting the number of clicks in each interval:

```TXT
+-------------+-----+
|time_interval|count|
+-------------+-----+
|        00-06|   15|
|        06-12|    9|
|        12-18|   11|
|        18-24|   15|
+-------------+-----+
```
