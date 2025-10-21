# Canary Deployment Scenario

## Overview
This scenario tests your ability to implement a canary deployment strategy in Kubernetes. You'll learn how to gradually roll out a new version of an application while maintaining service availability and minimizing risk.


## Background
You have a production web application running in the `canary-deployment` namespace. Your team has developed a new version and wants to perform a canary deployment to test it with a small percentage of users before rolling it out completely.

## Your Task
Implement a canary deployment strategy where:
- **40% of traffic** goes to the new canary version
- Stable version uses image `stefanprodan/podinfo:6.9.0`
- Both versions accessible through the same service endpoint

## Success Criteria
- Both stable and canary versions are running
- Traffic is distributed approximately 60/40 between stable and canary
- Service remains accessible throughout the process
- You can easily identify which version is receiving traffic


## Verification

Test your canary deployment by making requests and observing traffic distribution:

```bash
# Create a test pod and make multiple requests
kubectl run test-pod --image=quay.io/curl/curl -n canary-deployment --rm -it -- sh
# Inside the pod, make multiple requests to see traffic distribution
curl webapp
```


