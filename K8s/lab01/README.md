
# Kubernetes Lab 1: Node Isolation Using Taints in Kubernetes

This lab demonstrates how to isolate workloads in a Kubernetes cluster using node taints. A taint prevents pods from being scheduled on a node unless they tolerate the taint.

----------

## Tasks Overview

-   Run Kubernetes cluster with 2 nodes
-   Taint one node with:
    -   Key: `node`
    -   Value: `worker`
    -   Effect: `NoSchedule`
-   Describe all nodes to verify the taint
----------

## Steps and Screenshots

### 1. Start Minikube Cluster

Start the Kubernetes cluster with 2 nodes:

```bash
minikube start -n 2 -d docker
```

![Minikube Cluster Start](screenshots/1.png)

----------

### 2. Apply Taint to Worker Node

Taint the second node so that pods cannot be scheduled on it unless they tolerate the taint:

`kubectl taint nodes minikube-m02 node=worker:NoSchedule` 

![Applying Node Taint](screenshots/2.png)

----------

### 3. Verify Node Taints

Describe all nodes to check that the taint has been applied through:
```bash
kubectl describe nodes | grep -E "Name:|Taints:
```
 ![Verifying Nodes Taints](screenshots/3.png)

