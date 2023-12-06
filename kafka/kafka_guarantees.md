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

- How kafka ensures or assumes that transaction is not commited in consumer if it did not get acknowledgement? 
    - in simple words it is the responsibility of the consumer to acknowledge only after successfuly processing message. 
    - ``` python
        try:
        for message in consumer
            custom_process(message)
            consumer.commit()
        except Exception as e:
            print("some exception while processing")    
        
        def custom_process(message) :
            try
            // process message
            if some_err:
                raise Exception("exception while processing message")
      ```
    - kafka responsibility of a `transactional producer` in `exactly once scemantics` is to make all messages committed to partition or none of them are commited. So consumer will have chance to process all the messages of a transaction.
    - say a transactional producer produces 2 messages as a part of a transaction then kafka makes sure that 2 messages are available for consumer to read but in consumer's perspective those 2 messages are separate and `consumer donot have any knowledge of transaction`
    - ```python
        producer.init_transactions()
        producer.begin_transaction()

        try:
            producer.send("topicA","message1")
            producer.send("topicA", "message2")
            producer.commit_transaction()
            print("transaction is successful)
        except Exception as e:
            producer.abort_transaction()                                                
      ```
    - now producers will commit both `message1` and `message2` or abort both if the transaction fails.
    - And consumer will read messages `message1` and `message2` respectively.
    - if consumer fails after reading `message1` and able to commit offset to __consumers_offset then when the consumer is re-upped kafka will send `message2` as it has offset till `message`
    - where as consumer reads `message1` but fails before commiting offset back to kafka then kafka will actually resend the message. 
    - so it is application's/consumer's responsibility to handle the extra scenarios where offset is not committed back to the __consumers_offset or consumer fails before processing all messages of a transaction as consumer has no idea about a transaction. 
              
- How kafka ensures message is not acknowledge without proccessing and committed in the consumer?
    - Kafka has no such mechanism to know if a message is processed in cosumer until consumer acknowledges with `consumer.commit()`.
    - consumer has to explicitly call `consumer.commit()` which sends back an acknowledgement to kafka that message is proccessed and commits the offset into `__consumers_offset`. 

- What are the guarantees of kafka about ordering of messages in a partition ?
