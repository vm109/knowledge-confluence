### Worker Threads
- What are worker threads?
    - Worker threads are a way to run JavaScript code in parallel.
    - They are useful for CPU-intensive JavaScript operations.
    - They do not help much with I/O-intensive operations.
        - Why dont they help much in I/O operations?
            - Because I/O operations are already asynchronous in Node.js.

- How can we create worker threads if NodeJs runs on single thread event loop?
    - Node.js has a Worker module that allows you to create worker threads.
    - Worker threads are not first-class citizens in Node.js.
        - What does it mean by not first-class citizens?
            - It means that worker threads are not part of the event loop.
            - They run in a separate thread and communicate with the main thread using a message-passing mechanism.

- So does this mean NodeJs can create multiple threads?
    - Yes, Node.js can create multiple worker threads.
    - Each worker thread runs in a separate thread and has its **own event loop**.
    - Worker threads can communicate with each other using a message-passing mechanism.            
    
- How can we create a worker thread?
    - To create a worker thread, you need to use the Worker constructor.
    - The Worker constructor takes two arguments:
        - The path to the worker script.
        - An optional options object.
    - Here is an example of creating a worker thread:
        ```javascript
        const { Worker } = require('worker_threads');

        const worker = new Worker('./worker.js');
        ```
    - In the above example, we are creating a worker thread that runs the worker.js script.