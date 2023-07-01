### kubernetes addons 
- addons in kubernetes will provide extra capability to the cluster. 
- some of the types of kubernetes addons are: 
    - network addons
    - monitoring and observability addons [ like prometheus ]
    - ingress controllers [ reverse proxies to handle external traffic ]
    - DNS [ dns helps for service discovery ]

### some addons
``` bash
kubectl get namespace

kubectl get pods -n namespace
#eg. kubectl get pods -n kube-system
```    

- we use kubectl get pods to get the addons as addons are maintained as pods in kubernetes cluster.

### More description 
- what are network addons in kubernetes?
  - network addons are useful for adding virtual network interfaces to kubernetes cluster. 
  - some network addons are also useful for adding security, policies and for achieving fine grained control of network.
- what are DNS addons in kubernetes?
  - DNS is for resolving hostnames to ip address in kubernetes network  
- what are monitoring addons in kubernetes?
  - monitoring resources are achieved by these addons. 
  - example: prometheus