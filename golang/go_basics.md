### go basics 

- What is the difference between thread and go-routine?
  - goroutines are managed by go runtime. 
  - goroutines are multiplexed on few threads. 
  - goroutines are lightweight than threads. 

- How are the goroutines lighter weight than go routines?
  - goroutines creation, scheduling and synchronization are handled by golang runtime and not by the OS
  - multiple goroutines can be multiplexed on to single OS threads.
  - goroutines are spinned with smaller initial stack size. The stack size shrinks and grows dynamically as needed. this allows for efficient memory usage.   
  - goroutines communication is through `channels` and do not need the locking and unlocking. 

- Give me an example of goroutines and where are they used.  
