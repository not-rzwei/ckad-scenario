# CronJob Batch Processing Scenario

## Overview
This scenario tests your ability to create and configure a CronJob for automated batch processing in Kubernetes. You'll learn how to schedule periodic tasks and configure job specifications.

## Background
Your application generates temporary files and logs that need to be cleaned up daily to prevent disk space issues. The operations team has requested an automated cleanup process that runs during low-traffic hours. The `batch` namespace has already been created for you.

## Your Task
Set up an automated data cleanup process with the following business requirements:
- Create a CronJob named `data-cleanup` in the `batch` namespace.
- Run daily during off-peak hours (2:00 AM)
- Use the `busybox:1.35` image for the cleanup task
- Execute the command: `echo "Cleaning up old data..." && sleep 5 && echo "Cleanup completed"`
- Ensure the cleanup process doesn't run longer than 30 seconds
- Allow 1 retry attempt if the job fails
- Keep the last 3 successful job runs for monitoring purposes

## Success Criteria
- CronJob is created and scheduled correctly
- Job configuration meets all specified requirements
- Job can be executed successfully

## Verification

```bash
# Check the CronJob
kubectl get cronjobs -n batch

# Verify the configuration
kubectl describe cronjob data-cleanup -n batch

# Test the job manually
kubectl create job --from=cronjob/data-cleanup manual-cleanup -n batch
kubectl logs job/manual-cleanup -n batch
```
