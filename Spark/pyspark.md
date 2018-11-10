# Pyspark

https://spark.apache.org/docs/2.1.0/quick-start.html



## Running a spark application using the spark-submit

```
spark-submit yourscript
```

## SparkContext

### Load pyspark package



```
import pyspark
```

### SparkContext Object

A driver program can access spark.

Application instance representing the connection to the spark cluster.

Instantiated at the beginning of a Spark application and created by spark driver.

Once we have a SparkContext, we can use it to build resilient distributed data set (RDDs).

### Create a SparkContext Object



```
sc = pyspark.Sparkcontext(appName = "MSDS694")
sc = pyspark.SparkContext(appName='day2_ex01').getOrCreate()
```

### Stop SparkContext



```
sc.stop()
```

## Resilient Distributed Dataset (RDD)

Distributed datasets that consists of records.

### Key ideas

- Distributed: The data in RDDs is divided into one or many partitions as in-memory collections of objects across worker nodes.
- Immutable: Read-only, once created, RDD never change.
- Resilient: Automatically rebuilt on failure, RDDs track lineage info to rebuild lost data (instead of replication).

### Create distributed data sets



```
# load external data
lines = sc.textFile("README.md", Partition#)

# take a collection or list of values
lines = sc.parallelize(["spark", "spark is fun!"], Partition#))
```

### Get the number of partitions



```
lines.getNumPartitions()
```

### Coalescing data within each partition and see what is in each partition



```
lines.glom().collect()
```

`glom()`: return the RDD created by coalescing all elements within each partition into a list.

`collect()`: return a list that contains all of the elements in this RDD.

Try to output the content of RDDs every-time after each operation.

### Save distributed data sets

`saveAsTextFile(new_subdir_name)`: return multiple output files (each partition in a separate file + success indicator: `_SUCCESS`) underneath the `new_subdir_name`, as spark writes the output from multiple nodes.

# RDD Operation

<http://spark.apache.org/docs/latest/rdd-programming-guide.html>

## Transformation Operation

Perform functions against each element in an RDD and return a new RDD. **Doesn't change the original RDDs.**

Lazy evaluation: operations are only evaluated when an action is requested. Doesn't return the output, return something like: `PythonRDD[10] at RDD at PythonRDD.scala:49`.

### Element wise transformation

`map(func)`: apply a function to each element in the RDD.

`flatmap(func)`: similar to `map()`, but concatenates multiple arrays into a collections that has one level structure, generate a list of words within one level structure.

`filter(func)`: return an RDD that passes the filtering requirement.

### Partition wise transformation

`mapPartitions(func)`: return a new RDD by applying a function to each partition of the RDD.

### Set Operation

format: `rdd1.operation(rdd2)`

`distinct()`: return only one of each element.

`union()`: return all duplicates.

`intersection()`: return common elements.

`substract()`: return elements that are in rdd1 only.

`cartesian()`: return cartesian product.

### Sample

Create a sampled subset RDD from an original RDD based on a percentage of the overall data set.

Format: `rdd.sample(withReplacement, fraction, seed)`

`withReplacement`: `True/False` Allow sample multiple times.

`fraction`:

- When replacement is used:
  - expected number of times each element is going to be sampled (positive double);
- When replacement is not used:
  - expected probability that each element is going to be sampled ( between 0 and 1);
  - if fraction is > 1, it will default back to 1;

`seed`: Random number generation to determine whether to include an element in the resulting RDD. **When a seed is given, it will generate same output.**

This is not guaranteed to provide exactly the fraction specified of the total count. It won't return the exactly number, but the roughly number.

## Action Operation

Trigger a computation and return a value to the Spark driver.

Return **non-RDDs** like a single number, string, array, etc.

`collect()`: return a list that contains all of the elements of the dataset. **This is usually useful after a filter or other operation that returns a sufficiently small subset of the data.**

`first()`: return a list that contain the first item of the dataset, similar to `take(1)`.

`take(n)`: return an array with the first n elements of the dataset.

`top(n)`: return the top (largest) n elements of the RDD.

`count()`: return the number of items in the dataset.

`countByValue()`: return a default dictionary of the number of times each element occurs in the RDD.

`reduce(func)`: 

- take a function that operates on two elements of the type in RDD;
- returns a new element of the same type;
- when the partition or RDD is empty, `reduce()` don't do anything, return an error.

`fold(zero, func)`:

- same as `reduce()`;
- but with the provided `zero value`: deal with the situation when the partition or RDD is empty;
- add `zero value` into it at the first step and the last step;
- sensitive to how many partition RDD has, the number of `zero value` it added.

`aggregate(zero, SeqOp, combOp)`:

- Similar to `reduce()`;
- but used to return a different type: `SeqOp` works for each group, `combOp` merging outputs from different partitions;
- 

`saveAsTextFile(path)`: Write the elements of the dataset as a text file (or set of text files) in a given directory in the local filesystem, HDFS or any other Hadoop-supported file system. Spark will call toString on each element to convert it to a line of text in the file.

`takeSample(withReplacement, num, [seed])`:

- Return an **array**
- with a random sample of num elements of the dataset, with or without replacement, optionally pre-specifying a random number generator seed.

### Numeric RDD Action

`count()`:

| count()    | Return the number of elements in the RDD.            |
| ---------- | ---------------------------------------------------- |
| mean()     | Return the mean of the RDD's elements.               |
| sum()      | Add up the elements in the RDD.                      |
| max()      | Return the maximum item in the RDD.                  |
| min()      | Return the minimum item in the RDD.                  |
| variance() | Return the variance of the RDD's elements.           |
| stdev()    | Return the standard deviation of the RDD's elements. |

| count()    | Return the number of elements in the RDD.            |
| ---------- | ---------------------------------------------------- |
| mean()     | Return the mean of the RDD's elements.               |
| sum()      | Add up the elements in the RDD.                      |
| max()      | Return the maximum item in the RDD.                  |
| min()      | Return the minimum item in the RDD.                  |
| variance() | Return the variance of the RDD's elements.           |
| stdev()    | Return the standard deviation of the RDD's elements. |

##  