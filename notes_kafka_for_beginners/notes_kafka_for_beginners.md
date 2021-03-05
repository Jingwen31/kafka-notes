# Lesson Notes for Kafka Beginners

## Part 1. Starting Kafka

* Launch zookeeper  
`zookeeper-server-start zookeeper.properties`

* Launch kafka  
`kafka-server-start server.properties`

## Part 2. Kafka CLI

#### Kafka Topics CLI
  
* Create new kafka topics  
`kafka-topics --zookeeper 127.0.0.1:2181 --topic first_topic --create --partitions 3 --replication-factor 1`  
***Note**: replicator-factor cannot be greater than the amount of brokers.*

* List all kafka topics  
`kafka-topics --zookeeper 127.0.0.1:2181 --list`

* Show information of certain topic  
`kafka-topics --zookeeper 127.0.0.1:2181 --topic first_topic --describe`

* Delete a topic  
`kafka-topics --zookeeper 127.0.0.1:2181 --topic second_topic --delete`

#### Kafka Producer CLI

* Produce messages  
`kafka-console-producer --broker-list 127.0.0.1:9092 --topic first_topic`

* Produce messages and add other properties  
`kafka-console-producer --broker-list 127.0.0.1:9092 --topic first_topic --producer-property acks=all`

* Produce message to a topic that does not exist  
`kafka-console-producer --broker-list 127.0.0.1:9092 --topic first_topic`  
***Note**: This will create this topic with the default partition 1 and replication factor 1, which is not what you want usually. The default properties can be changed in server.properties.*

* Producer with keys
`kafka-console-producer --broker-list 127.0.0.1:9092 --topic first_topic --property parse.key=true --property key.separator=,`


#### Kafka Console Consumer CLI

* Read message  
`kafka-console-consumer --bootstrap-server 127.0.0.1:9092 --topic first_topic`  
***Note**: This will only read the new messages arrives because it's streaming/real-time.*

* Read all the messages  
`kafka-console-consumer --bootstrap-server 127.0.0.1:9092 --topic first_topic --from-beginning`

* Consumer with keys
`kafka-console-consumer --bootstrap-server 127.0.0.1:9092 --topic first_topic --from-beginning --property print.key=true --property key.separator=,`

#### Kafka Consumers in group

* read message from part of the group  
`kafka-console-consumer --bootstrap-server 127.0.0.1:9092 --topic first_topic --group my-first-application`

*  start another consumer in the console
`kafka-console-consumer --bootstrap-server 127.0.0.1:9092 --topic first_topic --group my-first-application`
***Note**: the messages will be split to the 2 consumer because thwy share the same group.*

* read with a new group from beginning
`kafka-console-consumer --bootstrap-server 127.0.0.1:9092 --topic first_topic --group my-second-application --from-beginning`
***Note**: If stop and rerun the same command, there will be no old messages show up, since it't the same group and commited offset.*

#### Kafka Consumer Groups CLI

* List all consumer groups  
`kafka-consumer-groups --bootstrap-server locahost:9092 --list`

* Show the description of certain consumer group  
`kafka-consumer-groups --bootstrap-server locahost:9092 --describe --group my-second-application`

#### Reset Offsets

* reset offset to earlist
`kafka-consumer-groups --bootstrap-server localhost:9092 --group my-first-application --reset-offsets --to-earlist --execute --topic first_topic`

* reset offset shift forward  
`kafka-consumer-groups --bootstrap-server localhost:9092 --group my-first-application --reset-offsets --shift-by -2 --execute --topic first_topic`

