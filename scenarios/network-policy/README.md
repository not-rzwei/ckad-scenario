# Network Policy Scenario

## Overview
This scenario tests your ability to implement network policies in Kubernetes to control traffic flow between pods. You'll learn how to create ingress and egress rules to enforce network segmentation and security boundaries.

## Background
You have a three-tier application architecture running in the `network-test` namespace:
- **Frontend**: Web application that serves user requests
- **Backend**: API service that processes business logic
- **Database**: Data storage service

All pods are running HTTP services on different ports for simulation purposes:
- **Frontend**: HTTP service on port 80
- **Backend**: HTTP service on port 8080  
- **Database**: HTTP service on port 5432 (simulating database port)

You need to implement network policies to control traffic flow according to security requirements.

## Your Task
Create network policies to enforce the following traffic rules:

1. **Frontend pods**:
   - Can accept requests from anywhere (ingress from all sources)
   - Can only send requests to backend pods (egress to backend only)

2. **Backend pods**:
   - Can only accept requests from frontend pods (ingress from frontend only)
   - Can only send requests to database pods (egress to database only)

3. **Database pods**:
   - Can only accept requests from backend pods (ingress from backend only)
   - Cannot send requests to any other pods (no egress)

## Hints

- When using `curl service-name`, DNS resolution is required. Make sure your network policies allow pods to communicate with the DNS service; otherwise, DNS lookups will fail and `curl` commands using service names won't work.
- NetworkPolicies are enforced at the Pod level, not the Service level.

## Success Criteria
- All three network policies are created and applied
- Frontend can receive traffic from external sources
- Frontend can communicate with backend
- Backend can only communicate with frontend and database
- Database can only receive traffic from backend
- Traffic is blocked between unauthorized pod pairs

## Verification

Test the network policies by attempting connections between pods:

```bash
# Check all pods are running
kubectl get pods -n network-test

# Verify network policies are applied
kubectl get networkpolicies -n network-test
kubectl describe networkpolicy -n network-test

# Test frontend to backend (should work)
kubectl exec -it deployment/frontend -n network-test -- curl backend:8080

# Test backend to database (should work)
kubectl exec -it deployment/backend -n network-test -- curl database:5432

# Test frontend to database (should be blocked)
kubectl exec -it deployment/frontend -n network-test -- curl database:5432

# Test backend to frontend (should be blocked)
kubectl exec -it deployment/backend -n network-test -- curl frontend:80

# Test database to backend (should be blocked)
kubectl exec -it deployment/database -n network-test -- curl backend:8080

# Test external access to frontend (should work)
kubectl port-forward service/frontend 8080:80 -n network-test
# In another terminal: curl localhost:8080
```
