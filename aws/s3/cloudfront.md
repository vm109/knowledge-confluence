## cloudfront
- The basic components of cloudfront are 
```
Origin
Edge Location
Distribution
```
### Origin
- Origin is the source of actual resource.

### Edge Location
- Edge location is the node nearest to the user. 
- Edge Location is served by a CDN node; i.e content delivery network node. 

### Distribution
- Distribution is the network of edge nodes through which content is delivered. 
- there are 2 types of distributions in AWS
    - web distribution for delivering web pages 
    - RTMP [ they are used as CDN distribution for media files]

### BackBone network
- AWS backbone network is aws own network over which transfer of data is quick as data transfer does not need to go through other external network nodes. 

### TTL [ time to live]
- it is the amount of time a media or web page is cache on a CDN node. 
- after the TTL cache is cleared.
- we can also clear cache by cache busting. 