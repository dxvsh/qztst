---
share: "true"
---


MapReduce is a programming model for processing large datasets by splitting the work across many machines (nodes), collectively referred to as a cluster.

For a simple explanation, we can take a look at the classic word count example (considered to be the hello world equivalent for MapReduce). Although the toy example below is extremely simplistic, the same ideas apply even if our dataset was in terabytes or petabytes.

![[map_reduce.png]]

Now, suppose we have a large collection of documents and we want to find the frequency of words across all of them. Here's how MapReduce would go through this:

1.  **Input**: You start with a large amount of data, like a collection of documents. In the above example it's just the following three strings: "Deer Bear River", "Car Car River", and "Deer Car Bear"
2.  **Splitting**: The input data is split into smaller chunks. In the example image, each string is its own chunk: "Deer Bear River", "Car Car River", and "Deer Car Bear".
3.  **Mapping**: Each chunk is processed independently by a "map" function. This function transforms each input item (like a sentence) into key-value pairs. In our case, the "map" function converts each word into a key with its corresponding value (the number of occurrences). For the "Deer Bear River" string, the mapping becomes `Deer, 1`, `Bear, 1`, `River, 1`.
4.  **Shuffling**: The key-value pairs are then shuffled and **grouped by key**. So all the pairs with the key `Bear` get grouped together, all pairs with the key `car` get grouped together and same for other words.
5.  **Reducing**: A "reduce" function processes each group of key-value pairs to produce the final output. In our example, the "reduce" function sums the counts for each word. So, it adds all the `Bear, 1` values, resulting in `Bear, 2`.
6.  **Final result**: The result is the count for each word: `Bear, 2`, `Car, 3`, `Deer, 2`, `River, 2`.

In essence, MapReduce divides a large problem into smaller, independent problems that can be solved in parallel, and then combines the results to get the final answer.

## Apache Hadoop

Apache Hadoop is a **big data processing framework** and has an implementation of the MapReduce programming model.

Hadoop is an open-source, distributed computing framework that enables the processing of large datasets across a cluster of computers. It can handle massive amounts of data, by breaking it down into smaller, manageable chunks and processing them in parallel.

**Key points to note:**

- **Scalability:** Handles large volumes of data that exceed the capacity of a single machine by distributing the processing across a cluster of machines.
- **Flexibility**: supports various data formats and can handle unstructured and semi-structured data.
- **Fault Tolerance:** Ensures data processing continues even if some machines in the cluster fail.
- **Cost-Effectiveness:** Uses commodity hardware to create large, scalable clusters.

See also : [[Apache Spark]] which was built to address certain limitations of Hadoop.