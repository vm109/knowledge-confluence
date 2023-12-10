### Basic Components of kafka
- What are the core components of kafka?
    - brokers
        - Kafka is a distributed system, so a kafka cluster is made up of multiple servers together called brokers.
    - topics 
        - kafka producers will write messages into topics. 
    - partitions
        - each topic is split into multiple partitions to achieve parllelism.
    - producers
        - Producers will write messages into kafka topics.
    - consumers
        - Consumers will consume messages out of topics.

- How does Kafka handle schema evolution in data streams?
    - Kafka is schema-agnostic; it treats messages as byte arrays.
    - Serialization and deserialization of messages are the responsibilities of producers and consumers.
    - While Kafka itself doesn't enforce or manage schemas, it's a good practice at the application level to define and maintain schemas for message validation.
    - Schema evolution can be managed through versioning, and adopting additive changes ensures backward compatibility.

- What is the significance of partitions in kafka?
    - a single topic can be split into multiple partitions for parllelism.
    - each partition of a kafka topic can live on a different broker of the cluster.
    - kafka `scrictly` makes sure that each message in partition is `ordered`
    - In kafka producers can produce messages to `specific` partition by chosing a `partitioning strategy` or `partition key`, similarly consumers can consume messages from a specific partition of the topic.
    
- What are the ideal number of partitions we can have for a topic?

- How does partitions help consumers with consuming process and is there any trade offs having many partitions?
    - In partitions messages are devided among partitions and messages in each partition are strictly ordered. 
    - By having multiple partitions consumers can achieve `paralell processing` and `load balancing` load between consumers.
    - Ordering in partitions is strictly maintained by kafka. So if a consumer expects ordered messages it can be achieved by partitions.
    - with partitions we can achieve high throughput of consuming.
    - Drawbacks:
        - maintaining multiple partitions and deciding on `partitioning strategy` or `partition key` is complex
        - global ordering cannot be achieved with partitions as, partition only gaurantees order of messages within that partition and not across partitions
        - data skew, due to `partitioning strategy` if data in one partition becomes more than others it will create bottlenecks in overall system.

- Is partitions of kafka similar to replication?
    - Partition: 
        - are necessary to gain parallelism in kafka. 
        - A single topic is devided into multiple parallel partitions.
    - Replication:
        - replication is a way of duplicating messages for achieving availability and distaster recovery. 
        - replicas are the copies of the same partition. 
        - replicas are stored on different brokers to ensure disaster recovery.
        - replication is a feature applied on partitions to achieve reliability and availability.

- How can we chose specific partition of a kafka topic to produce and consume? [ eloborate about partition strategy or partition key ]

- How many topics can we have in a kafka cluster?

- What are the guarantess of kafka? i.e atleast once? Actually what are the usual guarantees of a messaging broker system?

- What is parallelism and what is the significance of paralellism in the context of kafka?
    - `paralellism` is the ability to execute a piece of work in parallel by multiple workers
    - i.e a piece of work can be devided into multiple small pieces and can be worked exactly at the same time. 
    - with multiple partitions of a topic messages are flown from producer to consumer in `parallel`, which improves the throughput of message flow.
    - `concurrency` on the other hand similar but may not mean to work on different pieces of work exactly at the same time but to manage to complete multiple tasks in overlapping times and thus achieving near simultaneous completion. 
    - `concurrency` is about managing multiple tasks to achieve completion at near simultaneously by overlapping time periods but not necessarily exactly simultaneous completion.
    - with multiple consumers of a topic messages are processed `concurrently`. [ each consumer in a group proccess a subset of partitions. ]

- What is a consumer group in kafka and its components?
    - A group of consumers assigned to consume messages out of partitions of the topic.
    - it is ideal to have balanced number of consumers and partitions. i.e; equal number of consumers as partitions of the topic `ensuring each consumer has a partition assigned`.
    - But atleast each consumer should have a partition assigned else if the total consumers are more than the total partitions then consumers will be left idle or without consuming work.
    - kafka makes sure that each partition is consumed by no more than one consumer.
    - scenario where consumers are less than partitions, some consumers may be overloaded due to skewed partitions.
    - `components of consumer group`
        - **offset management**
            - each consumer maintains offset/log of a partition upto where it had consumed the partition. [ i.e in `__consumers_offset` consumer will store the position of the partition until where it had read so in failure another consumer can start reading from that position/offset ]
            - offset is a way for consumer to pick reading messages from where it left off in case of failure or restart.
        - **partition assignment** 
            - kafka broker dynamically assigns partitions to a consumer of a consumer group.
        - **loadbalancing**
            - if there is heavy load and room for adding consumers we can add consumers to consumer group for balancing that heavy load.

- Scenario: Say a kafka has 2 consumers and 4 partitions. each consumer is assigned 2 partitions. Now a consumer goes down after consumption. So what happens now?
    - first step of kafka is `rebalancing the consumer group`. i.e; partitions of the topic are reassigned to remaining consumers of the consumer group. 
    - now offset of the partition: say a consumer1 is assigned to partition0 previously and has a offset, that offset is maintained in __consumer_offsets topic. So when consumer2 is reassigned to consumer partition0 it will check the offset maintained for partition0 by consumer1 and consumer2 will restart reading messages from that offset. 
    - so when consumers maintain offset in `__consumers_offset` topic it is actually the offset of the topic.             


- What is the role of `timestamp` in kafka?