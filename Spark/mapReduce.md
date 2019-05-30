# MapReduce

> Allow computations to be parallelized over a cluster.

**Map**: apply a function to each data over a portion of data in parallel;

**Reduce**: return one value from multiple values.

Hadoop MapReduce solved issues of:

* **Distribution**: Distribute the data.
* **Parallelism**: Perform subsets of the computation simultaneously.
* **Fault Tolerance**: Handle component failure.

Limitations:

* **Slow**: MapReduce job results need to be stored in HDFS (disk) before they can be used by another job. ➔ Slow with iterative algorithms. 
* Many kinds of problems don’t easily fit MapReduce’s two-step paradigm. 
* Hadoop is a low-level framework, so myriad tools have sprung up around it and brings additional complexity and requirements. 

##Hadoop MapReduce vs. Spark

|                 | Hadoop MapReduce                       | Spark                                        |
| --------------- | -------------------------------------- | -------------------------------------------- |
| Speed           | Decently fast                          | 100 times faster than Hadoop                 |
| Ease of Use     | No interactive modes and hard to learn | Provides interactive modes and easy to learn |
| Costs           | Open source                            | Open source                                  |
| Data Processing | Batch Processing                       | Batch Processing + Streaming                 |
| Fault Tolerance | Fault Tolerance                        | Fault Tolerance                              |
| Security        | Kerberos authentication                | Password authentication                      |