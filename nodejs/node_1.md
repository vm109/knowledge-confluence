### Nodejs Is it single threaded Or MultiThreaded?
- NodeJs at its heart has event loop which runs on single thread. 
- But **Event Loop** is Non-blocking I/O 
- Even though event loop is single thread we can off load CPU intensive work into separate workers, threads are not first class to NodeJs.
    - To compare this with java concurrecny, threads and parallel processing is first class.
- The Core philosophy of nodejs is based on non-blocking IO and event based architecture.
- While worker threads can off load CPU intensive tasks the primary use of nodejs can be in web applications where multiple connections can be gracefuly handled with non-blocking IO and events based architecture to callback once the requests are processed.    
