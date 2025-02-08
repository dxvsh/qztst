---
share: "true"
---
Apache Spark is an open-source, unified analytics engine for large-scale data processing. It was designed to overcome the limitations of [[MapReduce#Apache Hadoop|Hadoop]]'s MapReduce model and provide a more efficient, flexible, and scalable platform for big data processing.

## Benefits over Hadoop

- **Performance**: Spark processes data in-memory reducing the need for disk I/O. This makes it significantly faster than Hadoop's disk-based approach. It can process data upto a 100x faster than Hadoop's MapReduce model.
- **Real-Time Processing:** Spark can handle real-time data processing and streaming, while Hadoop is better suited for batch processing.
- **Built-in Libraries** : Spark comes with several built-in libraries that provide a range of functionalities for data processing, machine learning, and graph processing.
	- **Spark SQL**: A library for working with structured data, providing support for SQL queries and DataFrames.
	- **Spark Streaming**: A library for processing real-time data streams, providing support for batch and streaming processing.
	- **MLlib (Machine Learning Library)**: A library for machine learning, providing implementations of popular algorithms for classification, regression, clustering, and more.
	- **GraphX**: A library for graph processing, providing support for graph-parallel computation and graph algorithms.
- **Support for multiple languages**: Spark supports Java, Python (PySpark), Scala, and R, making it easier for developers to work with the platform.

## PySpark

Apache Spark is written in Scala and PySpark is the Python API for Apache Spark. It enables you to perform real-time, large-scale data processing in a distributed environment using Python. It also supports all of Spark's features such as Spark SQL, DataFrames, Structured Streaming, Machine Learning (MLlib) and Spark Core. 

On GCP, [Dataproc](https://cloud.google.com/dataproc/docs) is a managed Apache Spark and Apache Hadoop solution that lets you take advantage of open source data tools for batch processing, querying, streaming, and machine learning.

Relevant Docs for PySpark:
[PySpark - Getting Started](https://spark.apache.org/docs/latest/api/python/getting_started/index.html)
[Spark SQL - Getting Started](https://spark.apache.org/docs/latest/sql-getting-started.html)
[MLlib Guide](https://spark.apache.org/docs/latest/ml-guide.html)
