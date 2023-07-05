## observability with liveness and readiness probe

### liveness probe
- If a kubernetes pod is spun and functioning correctly it passes liveness probe.
- Kubernetes will restart a pod if it is in degraded state.
- liveness probe is either configured with endpoint or command to determine its liveness.

### readiness probe
- If a kubernetes pod is ready to serve any http requests it is called readiness probe.
- readiness probe is ususally configured with a endpoint to determine its readiness to serve traffic.
- kubernetes determines when to route traffic to the pod based on the readiness probe.