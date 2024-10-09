# Kafka Consumers and Producers

When working with Kafka for real-time data processing and message consumption, several key concepts are essential to understand. Below are explanations for the various components used in Kafka messaging.

## 1. Consumer for Consuming Messages
A **Kafka consumer** is responsible for reading and processing messages from Kafka topics. Consumers typically belong to a consumer group, allowing the workload to be distributed among multiple consumers.

## 2. Producer Poller
In a producer setup, you might want to capture information from external sources (e.g., sensors) and publish this data to a Kafka topic. This can be achieved using a Supplier function, which provides the data to be sent to Kafka.

## 3. Kafka Streams
Kafka Streams is a powerful library that enables you to process streams of data in real-time. You can perform operations such as filtering, transforming, or aggregating the data. The advantage of using Kafka Streams is that the processing occurs client-side, eliminating the need to manage a distributed cluster.

### Key Benefits of Kafka Streams:
- **No need for a separate cluster**: Kafka Streams can run within any application, removing the need for a separate cluster.
- **Client-side processing**: All data processing is conducted on the client, leading to faster decision-making.
- **Real-time decision making**: Ideal for real-time data processing.

### Data Record
Each message in Kafka Streams is referred to as a data record, which consists of two main components:
- **Key**: Represents the identifier of the data.
- **Value**: Represents the actual data associated with the key.

## 4. KTable
The output of a Kafka Streams transformation can be stored in a KTable, which represents a table of data that changes over time. KTables are useful for keeping track of the latest state of each key.

---

# Kafka Integration Methods

When working with Kafka for messaging, different methods can be used depending on the flexibility required with the message broker. Below are the common approaches:

## 1. KafkaTemplate and KafkaListener
This method is used when working solely with Kafka and directly interacts with it as the message broker.

- **KafkaTemplate**: Used for sending messages to the Kafka broker.
- **KafkaListener**: Creates a consumer that listens to messages or events from the broker.

## 2. Kafka Cloud Streams
This approach allows you to work with any message broker, not just Kafka. It provides an abstraction over messaging technologies and offers two methods to handle messaging.

### 1. MessageChannel and StreamListener
In this method, message sending and event consumption are managed through predefined channels that abstract the messaging broker, allowing for flexibility in changing brokers.

- **MessageChannel**: Used for sending messages to the broker.
- **StreamListener**: Used for consuming events from the broker.

### 2. Spring Cloud Stream Functions
This method utilizes functional programming to send and consume messages. Functions are registered as beans and automatically wired to the messaging system. 

You define a Supplier for sending messages and a Consumer or Function for receiving and processing them. With Spring Cloud Streams, you can easily switch to any broker by configuring the correct bindings, enhancing application flexibility.

---

# Needed Dependencies
To get started, ensure you have the following dependencies installed:

- Spring Web
- Lombok
- Spring for Apache Kafka 
- Spring for Apache Kafka Streams 
- Cloud Stream

---

# Commands to Run the Kafka Server and Kubernetes
Open the command line and ensure you're in the `Kafka_cluster` folder:

```bash
docker-compose up -d
```
Start a producer for topic R2:
```bash
docker exec --interactive --tty broker kafka-console-producer --bootstrap-server broker:9092 --topic R2
```

Start a consumer for topic R4 with key/value printing:
```bash
docker exec --interactive --tty broker kafka-console-consumer --bootstrap-server broker:9092 --topic R4 --property print.key=true --property print.value=true --property key.deserializer=org.apache.kafka.common.serialization.StringDeserializer --property value.deserializer=org.apache.kafka.common.serialization.LongDeserializer
```

List all topics:
```bash
docker exec --interactive --tty broker kafka-topics --bootstrap-server broker:9092 --list
```

