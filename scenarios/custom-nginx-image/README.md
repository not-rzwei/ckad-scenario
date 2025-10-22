# Custom Nginx Image Scenario

## Overview
This scenario tests your ability to build Docker images using provided HTML content and Dockerfile, then save and manage image backups for distribution.

## Background
Your development team has created a custom website that needs to be containerized and distributed. You've been provided with the HTML content and a Dockerfile template. Your task is to build the custom nginx image, test it locally, and create a backup that can be easily shared with other team members or deployed to different environments.

The company needs a reliable way to package and distribute this custom web application, ensuring consistency across development, staging, and production environments.

## Your Task

Business requirements:
- Build a custom nginx image using the provided HTML content and Dockerfile
- Test the image locally to ensure it serves the content correctly
- Create a backup of the built image for distribution to other team members
- Ensure the image can be easily loaded and used by anyone who receives the backup

Technical constraints:
- Use the provided `index.html` file as the web content
- Use the provided `Dockerfile` for building the image
- Tag the image as `custom-nginx:1.0.0`
- Save the image backup as `custom-nginx-backup.tar`
- Test the image by running it locally

## Success Criteria
- Custom nginx image builds successfully without errors
- Image serves the provided HTML content when accessed
- Image backup file is created and can be loaded on other systems
- Local testing confirms the web application works correctly
- Image is properly tagged and ready for distribution

## Verification

```bash
# Verify the image exists and is properly tagged
podman images custom-nginx:1.0.0

# Test that the image runs and serves content correctly
podman run -p 8080:80 --rm --name verify-nginx custom-nginx:1.0.0

# Verify backup can be loaded
podman rmi custom-nginx:1.0.0
podman load -i custom-nginx-backup.tar
podman images custom-nginx:1.0.0
```
