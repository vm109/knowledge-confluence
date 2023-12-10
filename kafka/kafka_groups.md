### Producer Groups and Consumer Groups

- What are producer groups and consumer groups?
    - kafka producers and kafka consumers are group of producers/consumers which produce and consumer in parallel.
    - `producer group` is `not explicit` defined in kafka, where `consumer group` is `relevant`. 

- What is producer group?
    - In kafka there is no producer group. 
    - producers are usually independent and stateless    
    - each producer sends message to kafka topic without much coordination with other producers. 

- What is consumer group?
    - A consumer group is more `relevant` in kafka. 
    - Consumer Group is a logical group[of consumers] which work together to read messages out of a topic. 
    - **consumer group coordinator**: kafka assigns one of the consumer as the group coordinator. group coordinator will manage which consumer consumes out of which partition of a topic.
    - **rebalance of consumergroup**: consumer group rebalance occurs whenever a consumer leaves or a new one adds. Whenever a rebalance occurs partitions are reassigned among the consumers in the consumer group. 
    - **consumer offset** each consumer of group which reads out of partitions in topic will mainatin an offset in `__consumers_offset`, so this is the position of the consumer upto where it consumed in the partition. [ if a consumer goes down the next consumer knows the offset of the partition from the __consumers_offset topic]
    - **Hearbeats** consumers will send heartbeat or healthcheck to the group coordinator. Heatbeats will let us know the consumers are alive and if not triggers a consumer rebalance. 
    - **consumer group id** each `consumer group is identified by a unique consumer group id`. The group Id is `specified` when a consumer joins a consumer group.

- Explain the concept of consumer groups in kafka and how does it enable parallel processing of messages?
    - A consumer group is a logical group of consumers where they come under a group id and consume messages of different partitions of a topic parallely.
    - So each consumer of a consumer group can act on a subset of partitions, so multiple consumers in a consumer group can act parallely on all partitions of the topic and achieve parallel processing.

- What happens during a consumer group rebalance? How does kafka ensure even distribution of partitions among consumers? 
    - A rebalance occurs when a consumer joins or leaves the group. 
    - During rebalance group coordinator is notified that a consumer is joining or leaving the group. 
    - group coordinator will assign the partitions among the consumers.     
    - partitions are assigned equally to the consumers in the consumer group during rebalance. 
    - kafka ensures to avoid overlapping assignemnt. i.e no single partition is assigned to more than one consumer.

- Can you explain the Join and Sync phases of a consumer group rebalance? What happens in each phase, and how do consumers participate in the process?    
    - A consumer group rebalance occurs when a consumer joins or leaves a group. 
    - For example a consumer joins a consumer group then a `Join` signal is sent to the consumer group coordinator. 
        - In the Jon Phase consumer will signal readiness to participate and express their capability to handle certain number of partitions.
        - group coordinator will collect the readiness information from all consumers and `proopses new partition assignment`.
    - Once the coordinator proposes new partition assignment `Sync` phase is started.
        - consumer group coordinator will communicate new partition assignment to all consumers.
        - consumer syncronize with nee assigned partitions and get the offsets of partitions from the `consumers_offset` topic.
        - consumers will transition to new state that is with newly assigned partitions and new offsets in sync phase.
    - Rebalance is done once all consumers are syncronized and change their state.     

- Describe a situation where you had to scale a Kafka consumer group to handle increased message loads. What strategies did you employ, and what challenges did you encounter?

- What are the potential risks or pitfalls when working with consumer groups in a distributed environment? How can these risks be mitigated?

- Discuss strategies for optimizing the performance of Kafka consumer groups. What considerations should be taken into account to achieve high throughput and low latency?

- How did you setup a kafka consumer group as side car to read from kafka splitter topics of several microservices and add those messages to mongo for processing?
    - multiple consumer like story topic consumer, video topic consumer, image topic consumer are all a part of `Kafka_GroupId`.
    - usually consumers groups makes sense when multiple consumers read messages out of a topic so that they can conccurrently read messages from multiple partitions of the topic. 
    - but here multiple consumers are within a group and reading out of different/separate topics which wont benefit from group parallel processing, as each consumer will handle a topic. [ like many consumers will consume out of many topics]
    - similarly kafka splitter which is separate from the side car and comes before denormalizing is subscribing to the input topic using a `KAFKA_GroupId` and in each deployment there are several such input_topics, so there are multiple consumers in the group which are subscribing to different topics [ as opposed to multiple consumers subscribing to the same topic]
    - `this could be a TECH TALK topic`
    - there might be ordering guarntee issues in this way.
    - consumer groups are optimized for low lag/latency in the context of single topic. Reading from multiple topics in a group may lead to uneven lag. 