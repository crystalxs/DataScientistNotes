# Loading data

# Load text format data from local

## As one RDD

### Load one text file

`textFile(file_name)`

### Load all text files under a same folder

`textFile(folder_name)`

## Load multiple text files as `pair RDDs`

the key being the file name and the value being the file content.

`wholeTextFiles(dir_name)`

# From various file system

| Data Source | Address Prefix Format   |
| ----------- | ----------------------- |
| Local File  | file://path             |
| Amazon S3   | s3n://bucket/path       |
| HDFS        | hdfs://master:port/path |

## Local file

`textFile(file://path)`

**The filesystem should be available at the same path on all nodes in the cluster for both the
master and executors.** If the file is not on all nodes in the cluster, load it locally and then call parallelize to distribute the contents to workers.

## Amazon S3



## HDFS



