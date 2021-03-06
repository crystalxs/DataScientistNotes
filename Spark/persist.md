# Efficiency

## Persist in Memory/Disk

> RDDs are by default recomputed each time. However, if you want to reuse an RDD for multiple actions, you can ask Spark to store the content in memory/disk and query repeatedly. 

`line_with_spark.persist(StorageLevel.persistency_level) `

### Persist Methods

- `.cache()`
  - Same as calling `.persist(StorageLevel.MEMORY_ONLY)` or `.persist()`. 
  - Once persisted, RDDs can be reused multiple times without requiring reevaluation (recalculation). 
  - If there is not enough memory available to cache the RDD, it will be reevaluated for each lineage triggered by an action. 
- `.persist(StorageLevel.persistency_level)` 
  - Defaults: MEMORY_ONLY
- `.unpersist()`
  - Lets you manually remove them from the storage. 

### Storage Level

| Storage level                                   | meaning                                                      |
| ----------------------------------------------- | ------------------------------------------------------------ |
| MEMORY_ONLY                                     | Store RDDs in memory. If an RDD does not fit in memory, some partitions will not be cached and will be recomputed on the fly each time they're needed. |
| DISK_ONLY                                       | Store RDDs on disk.                                          |
| MEMORY_AND_DISK                                 | If an RDD does not fit in memory, store the partitions that don't fit on disk, and read them from there when they're needed. |
| MEMORY_ONLY_2,<br />MEMORY_AND_DISK_2,<br />etc | Same as the levels above, but replicate each partition on two cluster nodes. (<_N> indicates the replication level) |

## Tuning Parallelism - Partitions

> For parallel collections, users can specify the min number of partitions to cut the RDD into.

- `your_rdd = sc.parallelize(data, partitionSize)` or `textFile(file_name, partitionSize)`
- `sc.parallelize(data).<transformation>(...,partitionSize)`
  - `sortBy()`
  - `sortByKey()`
  - `groupBy()`
  - `reduceByKey()`
  - `join()`
  - `leftOuterJoin()`
  - `rightOuterJoin()`
  - `partitionBy()`
  - `combineByKey()`
  - `aggregateByKey()`
  - `foldByKey()`
  - `groupByKey()`
  - `cogroup()`
  - `subtractByKey()`
  - `subtract()`
  - `repartition()`
  - `coalesce()`

### Check partitions

- `your_rdd.getNumPartitions()`: returns the number of partitions in RDD.
- `your_rdd.glom().collect()`: return an RDD created by coalescing all elements within each partition into a list.

### Partitioner

Pair RDDs: `partitionBy(partition_size, partitionFunc)`

- Defines how the elements in a key-value pair RDD are partitioned by key. 
  - Manage data commonly accessible together on the same node.
  - Organize data for minimizing network traffic/communication to improve performance.
  - Maps each key to a partition ID, from 0 to numPartitions - 1. 
- Types:
  - HashPartitioner: partitioner using a hash value of a key. **default**
  - RangePartitioner: partitioner partitioning sorted RDDs into roughly equal ranges.
  - Custom Partitioner: User-defined paritioner.

### Repartitioning RDDs

> Change the partitioning to distribute the workload more efficiently or avoid memory problems. 

- **`repartition(numPartitions: Int)`**
  - Shuffle data across the network to create a new set of partitions.
  - **Expensive.** 
- **`coalesce(numPartitions: Int, shuffle = false)`**
  - Optimized version of repartition() – avoid data movement and reduce the number of RDD partitions.
  - Match the locality as much as possible, but try to balance partitions across the machines. 

### Operations and Partitioning

- **Operations benefiting from partitioning**
  - Operations involving shuffling data by key across the network. 
  - `join()`, `leftOuterJoin()`, `rightOuterJoin()`, `groupByKey()`, `reduceByKey()`, `combineByKey()`, `lookUp()`, etc. 
- **Operations returns RDDs with known partitioning information.**
  - `sortByKey()`: range-partition
  - `groupByKey()`: hash-partition 
- **Operations forget the parent’s partitioning information.**
  - `map()`: because it can theoretically modify the key of each record. 
- **Partition-specific Methods**: operations specifically designed to interact with partitions as atomic units. 
  - `foreachPartition()`: apply a function to each partition of an RDD. 
  - `glom()`: return all elements within each partition. 
  - `lookup(key)`: return values for the key using the partitioner to narrow its search to only the partitions where the key would present. 
  - `mapPartitions()`: return a new RDD by applying a function to each partition of the RDD. 

## RDD Dependencies / Lineage

> A dependency between an old and a new RDD is created, every time a transformation is performed on an RDD. 

- Spark’s execution model is based on directed acyclic graphs (DAGs), where nodes are RDDs and edges are dependencies. **The new RDD depend on the old RDD.** 
- RDD Resilience - As Spark records the linage of each RDD, any RDDs can be reconstructed to the state it was at the time of the failure using RDD Lineage. 

RDD Dependency Types

- Narrow: when no data shuffle between partitions is required.
- Wide: when it requires shuffle when joining RDDs.

`toDebugString()`

- Shows a textual representation of RDD dependencies.
- The RDDs in the output appears in reverse order.
- Useful in trying to minimize the number of shuffles. 
- The numbers in parentheses show the number of partitions of the corresponding RDD. 
- Every time you see a ShuffleRDD in the lineage chain, you can be sure that a shuffle will be performed at that point. 

`.checkpoint()`

- `sc.setCheckpoinDir("dir")`: set the directory where RDDs will be check-pointed.
- Persist RDDs to disk.
- After checkpointing, the RDD ’s dependencies are erased, as well as the information about its parent(s), because they won’t be needed for its recomputation any more. 
- Will be triggered once an action operation is called.
- `.persist()`, `.cache()`: keeps RDD’s dependencies. 

## Using shared variables

> Normally, when a function passed to a Spark operation is executed, it works on separate copies of all the variables used in the function. These variables are copied to each partition, and updates to the variables are not propagated back to the driver program. 
> Shared variables help maintain a global state or share data across tasks and partitions. 

- **Accumulator**: aggregate information from executor nodes to the driver node. 

  - Is shared across executors that you can only add to. **Useful to implement global sums and counters.** 
  - Can be accessed by driver node, not from an executor node. The driver can call it using `.value`. 
  - The executor can add to the accumulator with `.add(val)` method or `+`. (it is **write-only**.) 
  - Create using `var_name = sc.accumulator(inital_value)`. 
  - If accumulators are used in transformation, the results may be erroneous. 
    - Can cause accumulator values to be counted more than once depending on what happens on the cluster. 
    - Should use accumulators within actions.
      - `.foreach(func)` 
      - Applies a function, <func> to all elements。

- **Broadcast variable**: efficiently distribute large read-only values to executor nodes. 

  - The value is sent to each node only once (not per task).

  - Create a broadcast variable using `var_name = sc.broadcast(value)`.

  - Access the value with `.value`. 

  - `.unpersist()`: removing a broadcast variable from memory on all workers. **It still stays on the driver node.** 

    