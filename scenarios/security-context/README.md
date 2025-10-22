# Security Hardening Scenario

## Overview
This scenario tests your ability to implement security best practices in Kubernetes by hardening a deployment to prevent privilege escalation attacks. You'll learn how to configure containers to run as non-root users and disable privileged access.

## Background
Your company's security team has identified a critical vulnerability in your web application deployment. The current configuration allows containers to run with root privileges, which poses a significant security risk. If an attacker gains access to the container, they could potentially escalate privileges and compromise the entire Kubernetes node.

The security team has mandated that all production workloads must run as non-root users and cannot have privileged access. You need to modify the existing deployment to meet these security requirements while ensuring the application continues to function properly.

## Your Task
Secure the web application deployment by implementing the following security measures:

Business requirements:
- Ensure the application runs as a non-root user to prevent privilege escalation
- Disable privileged access to prevent container breakout attacks
- Maintain application functionality while implementing security controls
- Use the nginx:alpine image for the web server
- Ensure the deployment is named "webapp" in the "security" namespace
- Configure the container to run on port 8080

## Success Criteria
- The deployment runs successfully with security controls enabled
- No containers are running as root user
- Privileged access is disabled
- The application remains accessible and functional
- All security best practices are properly implemented

## Verification

```bash
# Check that the deployment is running
kubectl get deployment webapp -n security

# Verify the pod is running as non-root by checking whoami inside the container
kubectl exec deployment/webapp -n security -- whoami
# Should return a non-root user (not 'root')

# Verify the container cannot escalate privileges by testing id command
kubectl exec deployment/webapp -n security -- id
# Should show a non-root UID (not 0)
```
