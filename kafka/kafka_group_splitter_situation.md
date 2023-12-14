### kafka splitter and content
- A input topic is split into 2 output topics [ standard and ingestion ]
- Each input topic is split and assigned to 2 consumer groups [ standard and ingestion ] consumer groups.
- Questions: 
    - When kafka splitter creates topics does it join the topic in the group_id?
    - When there are more ECS tasks[ i.e around 9 ] than the available partitions of a topic what will the consumer do. Will they be ideal?

- Understanding: 
    - kafka splitter will create a consumer for each topic that is mentioned in the `splits` config as per`Split.class` and `Splitter.class`
    - Each of that consumer is added to the group_id which is in `kakfa_input`
    - `Splitter.class` will consume messages and split them based on allowlist and the app_value of the kafka message
    - So `kafka_splitter` will create and add consumers equal to the number of topics in the splits. 
    - And the consumer will multiply based on the `desired_count` of the kafka_splitter

    - And also the java side car of denormalizer will create consumer per topic in the KAFKA topics config. 
    - And the number of consumer will be multipled based on denormalizer desired_tasks 
    - These consumers are only added to the consumer group configured in the denormalizer. 


    - now we have to remember that the total partions are around 6 for each topic. 
    - each consumer can be assigned to 1 or more partitions.
    - but no more than 1 consumer can be assigned to one topic. 
    - so if there are more consumers than partitions then consumers will wait. 
    - Dynamic Rebalancing Overhead: and Potential Latency Issues: [ we need to investigate this ]
    - When Tasks are killed and recreated the number of consumers are increasing, which results in rebalance of the consumer groups.