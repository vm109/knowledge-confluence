### Middlware
- middleawre is a design pattern used to enhance or change the behavior of `http handler`
- middleware functions are between incoming http request and final http handler.

- What are the responsibilities of middleware? 
    - chain of responsibility
    - wrapping other handler
    - Modifying request/response

- What are the usecases of middleware? 
    - logging 
    - authentication 
    - compression 
    - instrumentaion    

- Give an example of middleware chaining in golang?
    - A middlware is which takes in a handler function and returns another handler function.
    - We can chain multiple middleware and either pass to the next middleware or not pass based on condition.
    - there are some libraries to chain middleware.    