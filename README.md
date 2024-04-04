# Full Cycle - Kafka

Based on the course: "Full Cycle 3.0 - Kafka"

## Control Center
http://localhost:9021/

## Kafka CLI

Connecting to the container:
```
docker exec -it fullcycle_kafka-kafka-1 bash
```

### Managing Topic

Creating a topic
```
kafka-topics --create --topic=mytest --bootstrap-server=localhost:9092 --partitions=3
```

Listing existing topics
```
kafka-topics --list --bootstrap-server=localhost:9092
```

Listing details of a topic
```
kafka-topics --bootstrap-server=localhost:9092 --topic=mytest --describe
```

### Testing consumer and producer
```
kafka-console-consumer --bootstrap-server=localhost:9092 --topic=mytest
```
Consuming from beginning:
```
kafka-console-consumer --bootstrap-server=localhost:9092 --topic=mytest --from-beginning
```
Consuming with group:
```
kafka-console-consumer --bootstrap-server=localhost:9092 --topic=mytest --group=x
``` 

Producing:
```
kafka-console-producer --bootstrap-server=localhost:9092 --topic=mytest
```

In case of consuming with the --group=x we should use the parse.key=true
```
kafka-console-producer --bootstrap-server=localhost:9092 --topic=mytest --property parse.key=true --property key.separator=:
```
Now just add any key and value using : as separator, example
```
any_key:any_value
any_key2:any_value2
any_key3:any_value3
```

Listing group consumers:
```
$ kafka-consumer-groups --bootstrap-server=localhost:9092 --describe --group=x

GROUP           TOPIC           PARTITION  CURRENT-OFFSET  LOG-END-OFFSET  LAG             CONSUMER-ID                                           HOST            CLIENT-ID
x               mytest          0          3               3               0               console-consumer-9c7a5258-4c71-4020-889b-7bb5d165624b /172.26.0.3     console-consumer
x               mytest          1          15              15              0               console-consumer-9c7a5258-4c71-4020-889b-7bb5d165624b /172.26.0.3     console-consumer
x               mytest          2          3               3               0               console-consumer-bc4ad2e9-cd5f-4425-85f0-83ec0f3e7fcd /172.26.0.3     console-consumer
```
In this case we have two consumers, with 3 partitions. Therefore, one of the consumers is consuming from two partitions.