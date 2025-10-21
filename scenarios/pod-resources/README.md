# Pod Resource Management Scenario

## Overview
This scenario tests your ability to configure pod resource requests and limits to achieve specific Quality of Service (QoS) classes in Kubernetes. You'll learn how to set up guaranteed QoS for critical applications.

## Background
You have a critical application running in the `production` namespace that requires guaranteed resources to ensure consistent performance. The application needs to be configured with specific CPU and memory requirements to achieve guaranteed QoS class.

## Your Task
Configure the `critical-app` deployment to have **Guaranteed QoS** with the following resource requirements:
- **CPU**: 100m (0.1 CPU cores)
- **Memory**: 128Mi

The deployment is already running but needs proper resource configuration to ensure it receives guaranteed resources and won't be evicted under resource pressure.

## Success Criteria
- Pod has Guaranteed QoS class
- Pod remains running and stable
- Resource configuration is properly applied

## Hints

- Use `kubectl describe pod` to verify QoS class
- Resource units: CPU uses "m" for millicores (1000m = 1 core), memory uses "Mi" for mebibytes

## Verification

Verify your resource configuration:

```bash
# Check if the pod is running
kubectl get pods -n production

# Verify the QoS class and resource configuration
kubectl describe pod -l app=critical-app -n production
```
