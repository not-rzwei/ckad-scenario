# Basic Pod Scenario

## Overview
This scenario tests your ability to create and configure a basic pod in Kubernetes. You'll learn how to specify container images, expose ports, and ensure the pod runs in the correct namespace.

## Background
A web application requires a specific version of Redis to be used as a cache. The `web` namespace has already been created for you. You need to create and deploy a Redis instance that will serve as the caching layer for your web application.

## Your Task
Create a pod with the following characteristics, and leave it running when complete:
- The pod must run in the `web` namespace (the namespace has already been created)
- The name of the pod should be `cache`
- Use the Redis Alpine version 8.2
- Expose port 6379

## Success Criteria
- Pod named `cache` is running in the `web` namespace
- Pod is using the correct Redis Alpine 8.2 image
- Port 6379 is properly exposed
- Pod remains in Running state

## Verification

Verify your pod is running correctly:

```bash
# Check if the pod is running
kubectl get pods -n web

# Verify the pod details
kubectl describe pod cache -n web

# Test Redis connectivity (optional)
kubectl exec -it cache -n web -- redis-cli ping
```
