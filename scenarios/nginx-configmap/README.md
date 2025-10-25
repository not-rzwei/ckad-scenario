# Nginx ConfigMap Scenario

## Overview
This scenario tests your ability to create ConfigMaps from files and mount them as volumes in a deployment. You'll configure nginx to use a custom configuration and serve a custom HTML page.

## Background
Your development team needs to deploy a custom nginx web server with specific configuration. The nginx server should:
- Listen on port 8080 instead of the default port 80
- Serve a custom HTML page instead of the default nginx welcome page
- Use configuration files stored in Kubernetes ConfigMaps for easy management

You have been provided with the necessary configuration files (`nginx.conf` and `index.html` in the `setup` folder) and need to create the ConfigMap and deployment.

## Your Task

- Create a ConfigMap named `nginx` from the provided `nginx.conf` and `index.html` files
- Deploy nginx using the `nginx:alpine` image
- Mount the ConfigMap as a volume in the deployment
- Mount `index.html` to `/usr/share/nginx/html/index.html`
- Mount `nginx.conf` to `/etc/nginx/conf.d/nginx.conf`
- The deployment should be named `nginx` and run 1 replica

## Success Criteria
- ConfigMap contains both nginx.conf and index.html files
- Deployment successfully mounts the ConfigMap as a volume
- Nginx serves the custom HTML page on port 8080
- Pod starts without errors and serves the custom content

## Verification

```bash
# Verify the ConfigMap was created correctly
kubectl get configmap nginx -o yaml

# Check that the deployment is running
kubectl get deployment nginx

# Test the custom configuration 
kubectl run test-pod --image=curlimages/curl --rm -it --restart=Never -- curl http://nginx:8080
```
