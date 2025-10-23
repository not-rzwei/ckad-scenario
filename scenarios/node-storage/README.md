# Node Storage Scenario

## Overview
This scenario tests your ability to configure Kubernetes storage using node volumes with size constraints. You'll learn how to mount host directories as volumes and apply storage limits to pods.

## Background
Your company's DevOps team needs to deploy a web server that serves custom content from the host node. The application requires access to files stored on the node's filesystem. The host has 100MB available in the `/data` directory that needs to be shared with the pod.

## Your Task
Configure the existing deployment to serve custom content from a node volume with strict storage limits.

- Add volume configuration to mount the host directory `/data` as a read-only volume
- Create a custom `index.html` file in the `/data` directory on the node for the web server to serve
- The web server should serve this custom index.html file from the mounted volume
- The deployment is already created and named `webserver`

## Success Criteria
- Deployment is running and accessible
- Volume is properly mounted as read-only from the host node
- Web server serves custom content from the mounted volume

## Verification

```bash
# Check if the deployment is running
kubectl get deployments -n node-storage
kubectl get pods -n node-storage

# Verify the volume mount and storage limits
kubectl describe deployment webserver -n node-storage

# Test if the web server is serving content using curl
kubectl run test-curl --image=curlimages/curl --rm -it --restart=Never -n node-storage -- curl http://webserver

# Check the mounted volume contents (read-only)
kubectl exec -it deployment/webserver -n node-storage -- ls -la /usr/share/nginx/html/

# Verify the volume is read-only
kubectl exec -it deployment/webserver -n node-storage -- touch /usr/share/nginx/html/test.txt
# This should fail if the volume is properly mounted as read-only
```
