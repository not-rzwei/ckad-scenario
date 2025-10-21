# Secret Environment Variable Mapping Scenario

## Overview
This scenario tests your ability to consume secrets in a pod using environment variables where the environment variable names differ from the secret keys. You'll learn how to map secret keys to custom environment variable names.

## Background
You have a web application that needs to connect to a database. You need to create a secret to store the database credentials and then create a pod that consumes these credentials. However, your application expects environment variables with different names than the keys in the secret.

## Your Task
1. **Create a secret** named `database-credentials` in the `app-secrets` namespace with the following data:
   - `db-username`: `admin`
   - `db-password`: `password123`
   - `db-host`: `localhost`

2. **Create a pod** that consumes the database credentials from the secret, but maps them to environment variables with different names:
   - The pod must run in the `app-secrets` namespace
   - The name of the pod should be `webapp`
   - Use the `stefanprodan/podinfo` image
   - Map the secret keys to these environment variables:
     - `db-username` → `DATABASE_USER`
     - `db-password` → `DATABASE_PASS`
     - `db-host` → `DATABASE_HOST`

## Success Criteria
- Secret named `database-credentials` exists in the `app-secrets` namespace
- Pod named `webapp` is running in the `app-secrets` namespace
- Pod successfully consumes all three secret values as environment variables
- Environment variable names match the specified mapping
- Pod remains in Running state

## Verification

Verify your secret and pod are configured correctly:

```bash
# Verify the secret contents
kubectl describe secret database-credentials -n app-secrets

# Verify the environment variables are set correctly
kubectl exec webapp -n app-secrets -- env
```
