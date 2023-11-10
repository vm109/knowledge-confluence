### go context

- What is go context? 
  - `context` package is used to maintain and transport values in a request through out the request function hierarchy.
  - `context` can also signal request timeout after a time.
    -  
    ```go
     ctx, cancel := context.WithTimeout(context.Background(), 4*time.Second)
    ```
    - WithTimeout will send a time to channel on ctx.Done()
  - `context` can also signal request cancellation with cancel.
    -  
    ```go
     ctx, cancel := context.WithCancel(context.Background())
    ```
    - WithCancel will return a cancel() function and it will stop processing immdiately

- When is go context `withtimeout` vs `withcancel` is used?
    - WithTimeout is hard deadline. i.e After a time cancel() is signalled.
    - WithCancel we have more control over cancel(), so we can call `cancel` based on the business logic.
    - After cancel() is called we can listen to the channel <-ctx.Done() for the cancellation signal and execute particular logic after cancellation. 