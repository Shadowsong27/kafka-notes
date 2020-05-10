# Chapter 1: Meet Kafka

# Overview

Apache Kafka is

- a publish/subscribe messaging system
- distributed commit log 
- distributing streaming platform 

Apache Kafka provides the circulatory system for the data ecosystem.

It carries messages between the various members of the infrastructure, providing a consistent interface for all clients. 

Consistency in data format allows writing and reading messages to be decoupled. 

# Some reasons to use Kafka:

1. Multiple producers: allows aggregating and centralising similar data sources

2. Multiple consumers: allows multiple consumers to share a stream - achieving load balancing and failure tolerance

3. Disk-Based Retention: 
	- no loss of data due to slow processing due to burst in traffic etc
	- maintenance can be performed on consumer without worrying losing data

4. Scalability
	- strong horizontal scalability to increase performance
	- scale without reboot, not damaging availability
	- failure tolerance

# Key Concepts

### Message 
- The basic unit of data in Kafka
- similar to a database record, without a specific format

### Key 
- metadata of a message

### Batch
- a collection of messages 
- tradeoff between latency and throughput
- typically compressed - tradeoff between efficient data transmission and storage at the expense of processing power

### Schema 
- data schema / structure for message
- JSON, XML etc … lacking features such as robust type handling and compatibility between schema versions
- Recommended Apache Avro

### Topic 
- similar to a folder in file system (a table in database in the original book is less accurate
compared to a folder IMO)

### Partition - further breakdown of a topic (like a file)
- messages are written in an append-only fashion
- time-ordering is preserved across partition
- provides redundancy and scalability
- each partition can be hosted on a different server - a single topic can be scaled horizontally across multiple servers to provide performance far beyond the ability of a single server 

### Producer / Publisher
- create messages - produce to a speicfic topic

### Consumer / Subscriber
- read messages - subscribe to one or more topics and read message in order
- offset - allows reading the last read position

### Consumer Group
- one or more consumers that work together to consume a topic
- each partition is only con‐ sumed by one member -> ownership of the partition by the consumer
- this achieves load balancing and auto scaling

### Broker 
- single Kafka server
- receives messages from producers, assigns offsets to them, and commits the messages to storage on disk 
- services consumers, responding to fetch requests for partitions and responding with the messages that have been committed to disk
- can be part of a cluster

### Cluster
- one broker will also function as the cluster controller (automatically elected)
- responsible for administrative operation e.g. assinging partitions to brokers and monitoring for broker failures

### Partition & Broker
- a partition is owned by a single broker in the cluster - leader
- a partition may be assigned to multiple brokers (result in replication)

### Retention 
- retaining messages for a period of time (can be days) / certain size (can be certain GBs)
- broker retention 
- topic retention

# Other Useful Info

Advantages of Multiple Clusters Setup:

- Segregation of types of data 

- Isolation for security requirements 

- Multiple datacenters (disaster recovery) 

Tool / Lib I should keep an eye on afterwards: *MirrorMaker*

- handles the replication across brokers

- simply a Kafka consumer and producer, linked to a queue

History and origin are omitted, it's interesting to know. 





