# Service Account Troubleshooting Scenario

## Overview
This scenario tests your ability to troubleshoot and fix service account permissions for cross-namespace resource access, specifically debugging RBAC configurations that prevent pods from accessing resources in other namespaces.

## Background
Your company has implemented a security auditing system that runs in the `auditor` namespace and needs to monitor pods in the `developer` namespace.

The auditing application is deployed with a dedicated service account, but something is preventing cross-namespace access. The application logs show permission denied errors when trying to list pods in the `developer` namespace.

## Your Task

- Fix the service account permissions so the auditing application can access pods in the `developer` namespace
- Ensure the auditing application running in `auditor` namespace can successfully list pods in `developer` namespace
- Maintain proper security boundaries while enabling necessary cross-namespace access
- Verify the fix works by testing the application's ability to retrieve pod information

## Success Criteria
- The auditing application can successfully list pods in the `developer` namespace
- No permission denied errors in the application logs
- The service account has appropriate permissions for cross-namespace access
- The RBAC configuration follows security best practices
- The application can retrieve pod details from the `developer` namespace

## Verification

```bash

# Verify the service account has the correct permissions
kubectl auth can-i list pods --as=system:serviceaccount:auditor:auditor -n developer

# Test the application logs for any remaining errors
kubectl logs -n auditor deployment/auditor-app --tail=20
```
