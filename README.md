This repository contains hands-on scenarios for practicing Certified Kubernetes Application Developer. Each scenario is designed to test specific skills and knowledge areas.

## Prerequisites

- Kubernetes cluster (minikube, kind, or cloud provider)
- kubectl configured to access your cluster
- Basic understanding of Kubernetes concepts (Pods, Deployments, Services, etc.)

## How to Use This Repository

1. **Navigate to the scenario directory:**
   ```bash
   cd scenarios/[scenario-name]
   ```
2. **Read the scenario README** to understand the task requirements
3. **Set up the initial environment:**
   ```bash
   kubectl apply -k setup
   ```
4. **Complete the scenario tasks** as described in the README
5. **Verify your solution** using the provided verification steps
6. **Clean up when done:**
   ```bash
   kubectl delete -k setup
   ```

## How to Create Scenarios

Refer to [template/README.md](template/README.md)
