# Lesson Notes for Kafka Beginners

### Part 1. Starting Kafka

* Launch zookeeper  
`zookeeper-server-start zookeeper.properties`
* Launch kafka  
`kafka-server-start server.properties`

### Part 2. Kafka CLI
  
* Create new kafka topics  
`kafka-topics --zookeeper 127.0.0.1:2181 --topic first_topic --create --partitions 3 --replication-factor 1`  
***Note**: replicator-factor cannot be greater than the amount of brokers.*

* List all kafka topics  
`kafka-topics --zookeeper 127.0.0.1:2181 --list`

* Show information of certain topic  
`kafka-topics --zookeeper 127.0.0.1:2181 --topic first_topic --describe`

