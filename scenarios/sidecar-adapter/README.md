# Sidecar Adapter Pattern Scenario

## Overview
This scenario tests your ability to implement the sidecar pattern with log adapters. You'll learn how to configure multi-container pods where a sidecar container processes logs from the main application using shared volumes.

## Background
Your company's microservices architecture requires standardized log formats across all applications. The main application generates logs in its native format, but the logging infrastructure expects JSON-structured logs. You need to implement a sidecar adapter that reads the main application's logs and converts them to the required JSON format without modifying the main application.

## Your Task
Configure a deployment with a sidecar log adapter that processes logs from the main application using shared volumes.

Business requirements:
- Add a sidecar container using the busybox:latest image as a simple log adapter
- Configure shared volume access between containers for log processing
- The main application should write logs to `/var/log/`
- The sidecar adapter should read logs from the shared volume and process them
- The sidecar should be named `log-adapter`

## Success Criteria
- Deployment is running with both containers
- Main application is accessible and generating logs
- Sidecar adapter is processing logs from the shared volume
- Logs are being converted by the adapter
- Both containers can access the shared log directory

## Verification

```bash
# Check if the deployment is running
kubectl get deployments -n sidecar-adapter
kubectl get pods -n sidecar-adapter

# Verify both containers are running
kubectl describe pod -n sidecar-adapter

# Check the shared log directory contents
kubectl exec -it deployment/critical-app -c critical-app -n sidecar-adapter -- ls -la /var/log/

# Check the sidecar adapter logs
kubectl logs deployment/critical-app -c log-adapter -n sidecar-adapter

# Verify log processing is working
kubectl exec -it deployment/critical-app -c log-adapter -n sidecar-adapter -- ls -la /var/log/
```
