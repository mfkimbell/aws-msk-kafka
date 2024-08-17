# aws-msk-kafka

Live Update from Athena:
-----
![live_results](https://github.com/user-attachments/assets/c8221f8e-f68a-4b0e-a1f2-20e2518f2ff3)


EC2 setup for Producer and Consumer
-----------------------------------------------------------------------
`sudo yum install java-1.8.0`

`wget https://archive.apache.org/dist/kafka/2.6.2/kafka_2.12-2.6.2.tgz`

`cd kafka`

`aws configure` (set to us-east-1, can keep everything else blank)

`aws kafka list-clusters`

How to Find Bootstrap Server/Broker Addresses:
-----
* Go to your msk instance
<img width="578" alt="Screenshot 2024-08-17 at 4 29 16 PM" src="https://github.com/user-attachments/assets/87458d29-3376-4e27-8043-bf459d30258a">
<img width="489" alt="Screenshot 2024-08-17 at 4 30 02 PM" src="https://github.com/user-attachments/assets/73e64142-b438-4a07-a875-4668b8c29889">



Create a Topic (for test)
----------------------
Template
```
/home/ec2-user/kafka_2.12-2.6.2/bin/kafka-topics.sh --create --bootstrap-server <bootstrap server address> --replication-factor 3 --partitions 1 --topic <topic name>
```
Actual
```
/home/ec2-user/kafka_2.12-2.6.2/bin/kafka-topics.sh --create --bootstrap-server b-2.testmsk.sqb9zi.c10.kafka.us-east-1.amazonaws.com:9092,b-3.testmsk.sqb9zi.c10.kafka.us-east-1.amazonaws.com:9092,b-1.testmsk.sqb9zi.c10.kafka.us-east-1.amazonaws.com:9092 --replication-factor 3 --partitions 1 --topic MSK101Topic
```

List Topics
--------------------
Template
```
/home/ec2-user/kafka_2.12-2.6.2/bin/kafka-topics.sh --bootstrap-server <bootstrap server address> --list
```
Actual
```
/home/ec2-user/kafka_2.12-2.6.2/bin/kafka-topics.sh --bootstrap-server b-2.testmsk.sqb9zi.c10.kafka.us-east-1.amazonaws.com:9092,b-3.testmsk.sqb9zi.c10.kafka.us-east-1.amazonaws.com:9092,b-1.testmsk.sqb9zi.c10.kafka.us-east-1.amazonaws.com:9092 --list
```

Produce to Topic
----------------
Template
```
/home/ec2-user/kafka_2.12-2.6.2/bin/kafka-console-producer.sh --bootstrap-server <bootstrap server address> --topic <topic name>
```
Actual
```
/home/ec2-user/kafka_2.12-2.6.2/bin/kafka-console-producer.sh --bootstrap-server b-2.testmsk.sqb9zi.c10.kafka.us-east-1.amazonaws.com:9092,b-3.testmsk.sqb9zi.c10.kafka.us-east-1.amazonaws.com:9092,b-1.testmsk.sqb9zi.c10.kafka.us-east-1.amazonaws.com:9092 --topic MSK101Topic
```

Consume From Topic
------
Template
```
/home/ec2-user/kafka_2.12-2.6.2/bin/kafka-console-consumer.sh --bootstrap-server <bootstrap server address> --topic <topic name> --from-beginning
```
Actual
```
/home/ec2-user/kafka_2.12-2.6.2/bin/kafka-console-consumer.sh --bootstrap-server b-2.testmsk.sqb9zi.c10.kafka.us-east-1.amazonaws.com:9092,b-3.testmsk.sqb9zi.c10.kafka.us-east-1.amazonaws.com:9092,b-1.testmsk.sqb9zi.c10.kafka.us-east-1.amazonaws.com:9092 --topic MSK101Topic --from-beginning
```

Setting up Jupyter EC2
------
```
sudo yum install -y python3 python3-pip python3-devel
```
```
pip3 install --user jupyter
```
```
jupyter notebook --ip=0.0.0.0 --no-browser --port=8888
```
```
http://<public IP address>:8888/?token=<token provided by jupyter>
```
```
http://52.90.179.27:8888/?token=<token provided by jupyter>
```
Getting Stock Market Data on EC2:
------
* Upload data to S3
* Get S3 URI
```
aws configure
```
* Enter access keys
  
Template
```
aws s3 cp s3://<path to bucket>/<file name> /home/<user>/
```
Actual
```
aws s3 cp s3://data-mfkimbell/indexProcessed.csv /home/ec2-user/
```




# References:

### Originally followed this guide (but i'm implementing it in the cloud):

* https://www.youtube.com/watch?v=KerNf0NANMo&t=1903s
  
### Good Resource for MSK kafka

* https://www.youtube.com/watch?v=5WaIgJwYpS8&list=PLhr1KZpdzukd2EuSB1F9zoWMTwinTkqVn
  
### Good resource for confluence_python library

* https://docs.confluent.io/kafka-clients/python/current/overview.html
