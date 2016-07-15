# HADOOP

[TOC]

---

### Installation

1. Install docker
1. Upload image `docker pull cloudera/quickstart`
1. Run docker container
```
sudo docker run --hostname=quickstart.cloudera --privileged=true -t -i -v /home/vasyl:/mnt/vasyl cloudera/quickstart /usr/bin/docker-quickstart
```

---

### Run MapReduce job with python

Upload the file to HDFS
```
hdfs dfs -put /path/to/file.csv file_name_in_hdfs
```
Run the job
```
hadoop jar /usr/lib/hadoop-0.20-mapreduce/contrib/streaming/hadoop-streaming-2.6.0-mr1-cdh5.7.0.jar \
    -mapper mapper.py \
    -reducer reducer.py \
    -input file_name_in_hdfs \
    -output output \
    -file mapper.py \
    -file reducer.py
```