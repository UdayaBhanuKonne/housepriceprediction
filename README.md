# House Price Prediction


## Usage:

if you are running scripts in local ubuntu then follow steps from section Local 1 to 5 otherwise run the containers using below command
```bash
docker-compose up
```
Local:
 
1. Download kafka, hadoop, spark and configure as mentioned in the Week 11_Requirements (2) file. 

2. Run zookeeper after moving to kafka folder using the command 

```bash
bin/zookeeper-server-start.sh config/zookeeper.properties
```
3. Run kafka broker using the below command.

```bash
bin/kafka-server-start.sh config/server.properties
```
4. Run hdfs services using the below commands. 

```bash
hdfs namenode -format
start-dfs.sh
```
5. Upload/copy the train.csv to hdfs filesystem with below command.
```bash
hdfs dfs -copyFromLocal train.csv /files/
```

6. Create kafka topic to publish the test data with below command.

```bash
bin/kafka-topics.sh --create --bootstrap-server localhost:9092 --replication-factor 1 --partitions 1 --topic housesalepredictor
```
7. Run stream_test_data_kafka.py in bash terminal to publish the data to kafka topic housesalepredictor(create the topic prior to running the script).

```bash
python3 stream_test_data_kafka.py
```

8. Run spark_streaming.py either with spark-submit command  if jar is not uploaded to spark jars folder or python3 which reads the kafka data stream, run the model and predict the values.

```python
spark-submit --jars spark-streaming-kafka-0-8-assembly_2.11-2.4.3.jar spark_streaming.py
```
or

```python
python3 spark_streaming.py
```
