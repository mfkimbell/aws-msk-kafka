# aws-msk-kafka



`sudo yum install java-1.8.0`

`wget https://archive.apache.org/dist/kafka/2.6.2/kafka_2.12-2.6.2.tgz`

`aws configure` (set to us-east-1, can keep everything else blank)

`aws kafka list-clusters`

bootstrap server address:
b-2.testmsk.sqb9zi.c10.kafka.us-east-1.amazonaws.com:9092,b-3.testmsk.sqb9zi.c10.kafka.us-east-1.amazonaws.com:9092,b-1.testmsk.sqb9zi.c10.kafka.us-east-1.amazonaws.com:9092

Create a Topic
-----------------------------------------------------------------------
```
/home/ec2-user/kafka_2.12-2.6.2/bin/kafka-topics.sh --create --bootstrap-server <bootstrap server address> --replication-factor 3 --partitions 1 --topic MSK101Topic
```

```
/home/ec2-user/kafka_2.12-2.6.2/bin/kafka-topics.sh --create --bootstrap-server b-2.testmsk.sqb9zi.c10.kafka.us-east-1.amazonaws.com:9092,b-3.testmsk.sqb9zi.c10.kafka.us-east-1.amazonaws.com:9092,b-1.testmsk.sqb9zi.c10.kafka.us-east-1.amazonaws.com:9092 --replication-factor 3 --partitions 1 --topic MSK101Topic
```

List Topics
--------------------

```
/home/ec2-user/kafka_2.12-2.6.2/bin/kafka-topics.sh --bootstrap-server <bootstrap server address> --list
```
```
/home/ec2-user/kafka_2.12-2.6.2/bin/kafka-topics.sh --bootstrap-server b-2.testmsk.sqb9zi.c10.kafka.us-east-1.amazonaws.com:9092,b-3.testmsk.sqb9zi.c10.kafka.us-east-1.amazonaws.com:9092,b-1.testmsk.sqb9zi.c10.kafka.us-east-1.amazonaws.com:9092 --list
```

Produce to Topic
----------------
```
/home/ec2-user/kafka_2.12-2.6.2/bin/kafka-console-producer.sh --bootstrap-server <bootstrap server address> --topic MSK101Topic
```
```
/home/ec2-user/kafka_2.12-2.6.2/bin/kafka-console-producer.sh --bootstrap-server b-2.testmsk.sqb9zi.c10.kafka.us-east-1.amazonaws.com:9092,b-3.testmsk.sqb9zi.c10.kafka.us-east-1.amazonaws.com:9092,b-1.testmsk.sqb9zi.c10.kafka.us-east-1.amazonaws.com:9092
 --topic MSK101Topic
```

Consume From Topic
------
```
/home/ec2-user/kafka_2.12-2.6.2/bin/kafka-console-consumer.sh --bootstrap-server <bootstrap server address> --topic MSK101Topic --from-beginning
```
```
/home/ec2-user/kafka_2.12-2.6.2/bin/kafka-console-consumer.sh --bootstrap-server b-2.testmsk.sqb9zi.c10.kafka.us-east-1.amazonaws.com:9092,b-3.testmsk.sqb9zi.c10.kafka.us-east-1.amazonaws.com:9092,b-1.testmsk.sqb9zi.c10.kafka.us-east-1.amazonaws.com:9092 --topic MSK101Topic --from-beginning
```

References:
* https://www.youtube.com/watch?v=5WaIgJwYpS8&list=PLhr1KZpdzukd2EuSB1F9zoWMTwinTkqVn
