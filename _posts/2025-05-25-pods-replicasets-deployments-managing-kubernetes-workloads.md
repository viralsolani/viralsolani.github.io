---
layout: post
title: "Pods, ReplicaSets & Deployments – Managing Kubernetes Workloads"
date: 2025-05-25
author: "Viral Solani"
categories:
  - DevOps
  - Kubernetes
tags:
  - Kubernetes
  - Pods
  - Deployments
  - ReplicaSets
  - Microservices
  - Containers
---

# 🧱 Pods, ReplicaSets & Deployments – Managing Kubernetes Workloads

In our previous posts, we explored [Kubernetes Components](https://viralsolani.github.io/devops/kubernetes/2025/04/27/what-is-kubernetes-and-components-overview.html) and how [Kubernetes Architecture](https://viralsolani.github.io/devops/kubernetes/2025/05/04/how-kubernetes-works-the-architecture-behind-the-scenes.html) functions behind the scenes.

Now it’s time to dive into **how applications actually run on Kubernetes** — starting with:
- **Pods**
- **ReplicaSets**
- **Deployments**

---

## What is a Pod?

A **Pod** is the **smallest unit of deployment** in Kubernetes.
It represents:
- One or more **containers** that share storage/network
- Run as a single logical unit

### Multi-container Pods
Sometimes a Pod has **sidecar containers** — for example:
- One container runs your app
- Another handles logging, proxying, or configuration

### Pod Lifecycle
- Pods are **ephemeral**: if a Pod dies, Kubernetes creates a new one
- For that reason, Pods are almost always managed by higher-level objects like ReplicaSets

---

## What is a ReplicaSet?

A **ReplicaSet** ensures that a specified number of identical Pods are running at any given time.

- It watches the state of your cluster and **automatically replaces failed Pods**
- Each ReplicaSet is tied to a specific template (i.e., Pod spec)

However, you typically won’t create ReplicaSets manually — they’re usually managed by **Deployments**.

---

## What is a Deployment?

A **Deployment** provides declarative updates for Pods and ReplicaSets.  
Think of it as a **blueprint** that defines:
- How many replicas (Pods) you want
- Which image to deploy
- How to perform updates or rollbacks

### Example YAML Snippet
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
      - name: my-app
        image: my-app-image:v1
```

✅ This will ensure 3 Pods are always running using the `my-app-image:v1` image.

## Updates & Rollbacks
You can update the image version:

```bash
kubectl set image deployment/my-app my-app=my-app-image:v2
```
Roll back to the previous version:

```bash
kubectl rollout undo deployment/my-app
```

## Conclusion

Pods are the basic execution unit

ReplicaSets ensure Pods are always available

Deployments manage ReplicaSets declaratively and allow updates & rollback

These three resources form the core of how apps run in Kubernetes.

Next, we’ll look at how to expose those apps using Services — including ClusterIP, NodePort, and LoadBalancer types. ☸️
