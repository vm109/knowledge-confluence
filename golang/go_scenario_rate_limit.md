## Rate Limiting In Go API 

### How and Why did I use rate limiting in API
- APIs can be easily overused causing high CPU and Memory utilization which stress the system. 
- Rate limiting is very useful when the application is multitenant and offering the product to multiple clients/orgs.
- Rate Limiting In `go api` can be implemented using middleware.
    - A rate limiting middleware will wrap a request handler and check the rate limit before passing it to the next handler.
- I have used `redis-rate` which implements leaky bucket algorithm for checking the remainng rate limit for the org/client.
- Implemented NoopLimiter to allow requests which are internal to the application and donot need ratelimiting. 


### What is leaky bucket algorithm and what are the important things of leaky bucket algorithm?
- Leaky Bucket alogorithm emphasizes on continious flow of requests and saving the application from sudden bursts and also not rejecting the requests when sudden bursts happen. 
- Leaky bucket has the following components.
    - ratelimit per sec/per min
        - it is the rate limit per second or min we want the api endpoint to allow 
    - burst rate
        - the leaky bucket can process requests at a higher limit than configured as rate limit upto the `burst`
    - no delay
        - when nodelay is true when the ratelimit and burst are used the request are rejected immediately  
    - size
        - the total size of the bucket, that is it is the total number of tokens/requests the bucket can hold while the system is processing the requests at ratelimit. When bursts occur the tokens are processed at rate limit + burst. And if the total requests are sustained to be more than the bucket size after the burst time then the token will be rejected or delayed before rejection based on nodelay.