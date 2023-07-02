### K8 API objects
- What are API objects in k8?
  - These are the basic building blocks of K8:
    - pods
    - deployments
    - services
    - configmaps
    - persistent volume and persistent volume claims
    - namespaces

### Pods 
- Pods are where the container/containers of a application is created.

### Deployments 
- A group of pods or replicas of pods constitute a deployment. 

### Services
- A service is through which a deployment is reached from the external network. i.e service takes any request from external network and passes that request to the deployment/pods in the k8 network accordingly.

### Configmaps
- A configmap is where configurations required for the applications can be stored. 

### PV and PVC
- Persistent volumes 
  - they are external volumes for storing any data to be persisted by the pods/deployments. 
- Persistent volume claims
  - since pods are ephermal when pod dies and new pod is scheduled it has to use or associate to the persistent volume its predecessor pod has used. so it is possible with persistent volume claims. 

### Namespaces
- namespaces in kubernetes will allow to isolate environments from each other.
- so namespaces gives isolation and seperation among different environments within a cluster. 
- i.e in a cluster we can have dev and prod namepsaces and in each of that namespaces pods, deployments, addons, etc can be isolated.   

