# Rolling Update Scenario

## Overview
This scenario tests your ability to perform controlled rolling updates in Kubernetes. You'll learn how to configure deployment strategies to ensure zero-downtime updates while maintaining service availability and controlling resource usage during the update process.

## Background
Your production web application is currently running version 6.8.0 with 10 replicas serving critical traffic. The development team has released version 6.9.0 with important bug fixes and performance improvements. You need to upgrade the application while ensuring:

- No service interruption during the update
- The new version doesn't interfere with the existing version
- Resource usage remains controlled during the transition
- Only 20% of the total replicas are updated at any given time

The application uses a standard web server that can handle traffic immediately upon startup.

## Your Task
Update the `webapp` deployment while maintaining service continuity:

- Ensure the update process doesn't create additional replicas beyond the existing 10
- Configure the update to only affect 20% of replicas at any time
- Maintain service availability throughout the entire update process
- Use the new image `stefanprodan/podinfo:6.9.0` (current version is `stefanprodan/podinfo:6.8.0`)
- Ensure the update completes successfully without manual intervention

## Success Criteria
- All 10 replicas are running the new version
- Service remains accessible throughout the update
- No more than 2 replicas are updated simultaneously
- Update completes without creating additional replicas
- All pods are healthy and ready after the update

## Verification

```bash
# Check deployment status and update progress
kubectl get deployment webapp -n production

# Monitor the rolling update progress
kubectl rollout status deployment/webapp -n production

# Test service connectivity during update
kubectl run test-curl --image=quay.io/curl/curl:latest --rm -it --restart=Never -n production -- curl http://webapp:9898

# Check deployment history
kubectl rollout history deployment/webapp -n production
```
