### Kafka Guarantees

- What are the general guarantees of a messaging broker?
    - Delivery: messaging brokers guarantees `atleast once` or `exactly once`
    - Ordering: messages are delivered in order in which they are produced either in channel or partitions.
    - Persistance: messages are persisted for some configured time ensuring that they are not lost in the event of failure.
    - Acknowledgement: it is a mechanism to acknowledge message is succefully sent and received to producers and consumers.

- What are the delivery guarantees of kafka? And how is that useful?
    - Kafka supports both `atleast once` and `exactly once` message delivery guarantees. 
    - If there is a application failure and kafka consumer did not acknowledge the message is received then kafka re-sends the message to the consumer.
    - So the scenario is where a kafka consumer reads a message but exactly before sending an acknowledgement the app/consumer crashes and kafka donot know consumer has received the message already and so it has no correct offset commited to consumers_offset topic. So consumer again reads the same message. [ AKA redelivery ]
    - How much long do kafka wait before re-sending the message?
        - it is not about timeout, consumer will acknowledge without timeout if it did not crash. But if it crashed then message is re-delivered when the app/consumer is re-upped
    - `exactly once` delivery guarantee: In transactional use cases like banking applications messages are expected to be delivered exactly once. 
    
- What are the key differences which allow kafka to send messages exactly once?
    - kafka supports transactional and idempotent producers. 
    - i.e if a producer commits all the messages within a transaction or none of them are. [ messages are atomic in `transactional producers`]
    - So when a consumer reads message from a partition in `exactly once` kafka assumes that message is not processed and committed until there is an acknowledgement back. 
    - i.e if a crash occurs before kafka receives a acknowledgement from consumer after reading the message it assumes that the message is not processed and committed in exactly once scemantics.

- how kafka ensures or assumes that transaction is not commited if it did not get acknowledgement =? 
- how kafka ensures message is not acknowledge without commiting first in the consumer?

