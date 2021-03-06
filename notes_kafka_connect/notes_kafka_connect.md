# Lesson Notes for Kafka Connect API

## Part 1: Source Connector: FileStreamConnectors

### Standalone Mode

1. Start Kafka Cluster  
`docker-compose up kafka-cluster`

2. Start a hosted tool  
`docker run -rm -it -v "$(pwd)":/tutorial --net=host landoop/fast-data-dev:cp3.3.0 bash`

3. Create a topic with 3 partitions  
`kafka-topics --create --topic demo-1-standalone --partition 3 --replication-factor 1 --zookeeper 127.0.0.1:2181`

4. In the docker container, cd to the demo folder.  
`cd /tutorial/demo-1`

5. Connect using worker.properties and file-stream-demo-standalone.properties  
`connect-standalone worker.properties file-stream-demo-standalone.properties`

### Distributed Mode

1. Start Kafka Cluster  
`docker-compose up kafka-cluster`

2. Start a hosted tool  
`docker run -rm -it -v "$(pwd)":/tutorial --net=host landoop/fast-data-dev:cp3.3.0 bash`

3. Create a topic with 3 partitions  
`kafka-topics --create --topic demo-2-distributed --partition 3 --replication-factor 1 --zookeeper 127.0.0.1:2181`

4. Head over to 127.0.0.1:3030 -> Connect UI  
Create a new connector with File  
Paste the confirguration in source/demo-2/file-stream-demo-distributed.properties.

5. Now that the configuration is launched, create demo-file.txt in docker.  
`docker ps`  # get the containerId
`docker exec -it <containerId> bash`
`touch demo-file.txt`
`echo "hi" >> demo-file.txt`  # add messages
`echo "hello" >> demo-file.txt`
`echo "from the other side" >> demo-file.txt`

6. Read the topic data.  
`docker run --rm -it --net=host landoop/fast-data-dev:cp3.3.0 bash`
`kafka-console-consumer --topic demo-2-distributed --from-beginning --bootstrap-server 127.0.0.1:9092`

