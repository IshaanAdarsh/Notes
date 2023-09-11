# Apache Kafka:
- Kafka is a distributed Message streaming platform that uses publish and subscribe mechanism to stream the records (data flow).

### Features:
- **Distribution:** If the data is kept in a single system then the data can be easily lost(centralized). Storing the data on different system is called distribution, there are 2 types of distribution:
  - Split ditsribution -> e = e/3 + e/3 + e/3
      - In this type of distribution the data is split into n parts with ratio e/n. So if data is lost then not all parts are affected
  - Total distribution -> e = e + e + e
    - In this type of distribution the data is completely copeied to n different systems. so copy of data is preent in multiple places. Plems like data redundancy crop up, but the data is much safer

- **Message Streaming:**
  - Reduces the load and number of connections by introducing a buffer.
  - In-Efficient: O(n*m)

  <img width="470" alt="In-efficient" src="https://github.com/IshaanAdarsh/TIL/assets/100434702/72879744-8d7b-4247-b959-9f0f7a98d229">
  
  - Efficent:O(n+m)
  
<img width="467" alt="efficient" src="https://github.com/IshaanAdarsh/TIL/assets/100434702/4110dad5-e38e-4e8e-90e0-4aeecf14cfdc">

- **MESSAGING SYSTEMS**
  - A messaging system is responsible for transferring data from one application to another so the applications can focus on data without getting bogged down on data transmission and sharing.
    - Point to Point Messaging System
        - Messages are persisted in a Queue.
        - A particular message can be consumed by a maximum of one receiver only
        - There is no time dependency laid for the receiver to receive the message.
        - When the Receiver receives the message, it will send an acknowledgement back to the Sender.
    - Publish-Subscribe Messaging System
        - Messages are persisted in a Topic.
        - A particular. message can be consumed by any number of consumers.
        - There is time dependency laid for the consumer to consume the message.
        - When the Subscriber receives the message, it doesn't send an acknowledgement back to the Publisher.

<img width="547" alt="Messaging System" src="https://github.com/IshaanAdarsh/TIL/assets/100434702/93613e9b-6f56-4555-9feb-7166fd1584d5">

## Apache Kafka Architecture:
<img width="1108" alt="Kafka Architechture" src="https://github.com/IshaanAdarsh/TIL/assets/100434702/3dc385f9-38ca-4799-80f0-d57d122ddb65">

### TOPICS:
- A stream of messages belonging to a particular category is called a topic.
- It is a logical feed name to which records are published. Similar to a table in a database. (records are considered messages here.)
- Unique identifier of a topic is its NAME. We can create as many topics as we want.
<img width="411" alt="topic" src="https://github.com/IshaanAdarsh/TIL/assets/100434702/d5bf96f9-e4ff-459a-80bb-6fb25eac9bab">

### PARTITIONS
- Topics are split in Partitions. All the messages within a partition are ordered and immutable.
- Partitions are done in round robin method
- Each message within a partition has a unique Id associated known as Offset.

<img width="534" alt="Partition(Before)" src="https://github.com/IshaanAdarsh/TIL/assets/100434702/9f69ead0-41ad-4809-8ef8-cdc2799ae1ed">

<img width="553" alt="Partition(After)" src="https://github.com/IshaanAdarsh/TIL/assets/100434702/61b17f31-e042-436a-9823-4fd2c50a2c63">

### REPLICA & REPLICATION
- Replicas are backups of a partition. Replicas are never read or write data.
- They are used to prevent data loss. (Fault-Tolerance)

<img width="545" alt="Replication(before)" src="https://github.com/IshaanAdarsh/TIL/assets/100434702/87298e33-9791-4238-a3ce-821dc3ed4682">

<img width="589" alt="Replication(After)" src="https://github.com/IshaanAdarsh/TIL/assets/100434702/9b464e7b-c396-4279-be3e-d74652ac9642">

### PRODUCER:
- Producers are applications which write/publish data to the topics within a cluster using the Producing APIs.
- The producers can write data at 2 levels:
  - Topic level: In this all the messages are given to all the partitions
  - Partition level: In this all the messages are given to on a perticular partition

### CONSUMER:
- Consumers are applications which read/consume data from the topics within cluster using the Consuming APls. Consumers can read data either on the topic level(All the partitions of that topic) or specific partitions of the topic.
- Consumers are always associated with exactly one Consumer Group.
  - A Consumer Group is a group of related consumers that perform a task.

### BROKERS:
- Brokers are simple software processes who maintain and manage the published messages. Also known as kafka servers.
- Brokers also manage the consumer-offsets and are responsible for the delivery of messages to the right consumers.
- A Set of brokers who are communicating with each other to perform the management and maintenance task are collectively known as Kafka Cluster. We can add more brokers in a already running kafka cluster without any downtime.


### ZOOKEEPER:
- Zookeeper is used to monitor kafka Cluster and co-ordinate with each broker.
- Keeps all the metadata information related to kafka cluster in the form of a key-value pair.
- Metadata includes
  1. Configuration information.
  2. Health status of each broker.
- It is used for the controller election within kafka cluster. A Set of Zookeepers nodes working together to manage other distributed systems is known as Zookeeper Cluster or "Zookeeper Ensemble"

#### KAFKA FEATURES:
- Scalable.
  - Horizontal Scaling is done by adding new brokers to the existing clusters.
- Fault Tolerance.
  - Kafka clusters can handle failures because of its distributed nature.
- Durable.
  - Kafka uses "Distributed commit log" which means messages persists on disk as fast as possible.
- Performance
  - Kafka has high throughput for both publishing and subscribing messages.
- No Data loss
  - It ensures no data loss if we configure it properly.
- Zero Down Time
  - It ensures zero downtime when required number of brokers are present in the cluster.
- Reliability
  - Kafka is reliable because it provides above features. 
