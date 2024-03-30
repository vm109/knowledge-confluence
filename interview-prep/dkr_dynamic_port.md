Here's the updated version of the notes:

## Dynamic Port Allocation of Docker

### Allocating Host Ports to Containers in ECS
- In ECS, it is a common practice to share a cluster among multiple services.
- Each service can have multiple containers.
- To avoid port collision issues, host port allocation should be dynamic.
- To achieve this, we can opt for dynamic port allocation to the tasks in the ECS task definition.