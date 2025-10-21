# Container Probes Scenario

## Overview
This scenario tests your ability to configure liveness, readiness, and startup probes in Kubernetes. You'll learn how to set up proper health checks to ensure application reliability and prevent traffic routing to unhealthy pods.

## Background
You have a backend application running in the `backend-system` namespace with 3 replicas that has specific health check endpoints and startup behavior:
- **Slow startup**: The application takes time to initialize and needs to wait for the `/healthz` endpoint to return successfully before it's ready
- **Health endpoint**: `/healthz` - indicates the application is healthy but not necessarily ready to accept traffic
- **Readiness endpoint**: `/readyz` - indicates the application is ready to accept traffic and all dependencies are working
- **Multi-replica scenario**: With multiple pods, you can test how traffic is distributed and how individual pod failures affect the service

## Your Task
Configure the `backend-app` deployment with appropriate probes to handle the application's behavior:

1. **Startup Probe**: 
   - Check GET `/healthz` endpoint
   - Allow sufficient time for slow startup (30 seconds)

2. **Liveness Probe**:
   - Check GET `/healthz` endpoint  
   - Restart container if health check fails 1 times

3. **Readiness Probe**:
   - Check GET `/readyz` endpoint
   - Remove from service endpoints if readiness fails 3 times

## Success Criteria
- Pod starts successfully despite slow startup
- Pod is removed from service when dependencies fail
- Pod recovers and rejoins service when dependencies are restored
- Probes use appropriate timeouts and intervals

## Hints

- **Startup probe**: Runs before liveness/readiness, allows slow initialization
- **Liveness probe**: Determines if container should be restarted
- **Readiness probe**: Determines if pod should receive traffic
- Use `kubectl describe pod` to see probe status and events
- **Testing endpoints**:
  - `POST /readyz/enable` - Enables readiness endpoint
  - `POST /readyz/disable` - Disables readiness endpoint (simulates dependency failure)

## Verification

Test your probe configuration:

```bash
# Check if all pods are running
kubectl get pods -n backend-system

# Verify probe configuration
kubectl describe pod -l app=backend-app -n backend-system

# Check service endpoints (should include all ready pods)
kubectl get endpoints backend-service -n backend-system

# Test readiness manipulation
kubectl exec -it deployment/backend-app -n backend-system -- curl -X POST backend-service:8080/readyz/disable
kubectl exec -it deployment/backend-app -n backend-system -- curl -X POST backend-service:8080/readyz/enable

# Monitor pod events during startup and failures
kubectl get events -n backend-system --sort-by='.lastTimestamp'

# Test traffic routing
kubectl exec -it deployment/backend-app -n backend-system -- curl backend-service:8080

# Test individual pod readiness (replace POD_NAME with actual pod name)
kubectl exec -it POD_NAME -n backend-system -- curl -X POST localhost:9898/readyz/disable
kubectl get endpoints backend-service -n backend-system  # Should show fewer endpoints
kubectl exec -it POD_NAME -n backend-system -- curl -X POST localhost:9898/readyz/enable
kubectl get endpoints backend-service -n backend-system  # Should show all endpoints again
```
