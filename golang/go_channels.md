### Channels
- Channels are bridges of communication between goroutines.
- When a piece of work is shared among multiple goroutines, the results can be communicated between the goroutines using a channel

### Channel Basics Questions
- What is Fan-IN and Fan-OUT in go channels?
    - When multiple go routines write to a channel it is called fan-in, while multiple go-routines read out of channel is called fan-out.

- What is buffered channel vs un-buffered channel? 
    - A buffered channel has the capacity to hold values till a goroutine reads out of the channel. 
    - And the buffered channel will not be blocked till the channel is filled with values to the capacity.
 
- What is blocking in channels? 
    - Sender Blocked: A sender in the caller function will be blocked if there are no known goroutines to the caller function for reading out of the channel. 
    - Receiver Blocked: If the caller function is receiving data/values from channel and if the caller function does not have any known sender goroutines that send data/values to the channel then it will create a deadlock. Receiver is blocke till a sender sends data to the channel. 

- How are un-buffered channels useful? 
    - Unbuffered channels are used for synchronization between sender and receiver goroutines.
    - There is a tight coupling between sender and receiver go-routines while communicating through a unbuffered channel. 
    - Deadlocks are prevented as we can clearly setup a receiver and sender for the unbuffered channel, unlike in buffered channel it is complex.

- How are select statements useful in go channels and go routines? 
    - One use case for `select` statement is to signal timeout on a caller function about a goroutine which is taking long time to execute a work. 
    # TODO continue... [ more use cases of select stamenet in channels]