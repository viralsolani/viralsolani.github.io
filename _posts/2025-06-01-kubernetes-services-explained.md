---
layout: post
title: "Kubernetes Services Explained – Exposing and Connecting Applications"
date: 2025-06-01
author: "Viral Solani"
categories:
  - DevOps
  - Kubernetes
tags:
  - Kubernetes
  - Services
  - Networking
  - Microservices
  - DevOps
---

# Kubernetes Services Explained – Exposing and Connecting Applications

In the [previous post](https://viralsolani.github.io/devops/kubernetes/2025/05/25/pods-replicasets-deployments-managing-kubernetes-workloads.html), we explored how Kubernetes runs applications using Pods, ReplicaSets, and Deployments.

Now, let’s understand how users — or other applications — can actually **access** those workloads. That’s where **Kubernetes Services** come into play.

---

## Why Services Matter

In Kubernetes, Pods are:
- Ephemeral (they can restart, move, or scale)
- Assigned dynamic IPs

So if an app wants to talk to another app (say, frontend to backend), it can’t rely on Pod IPs.
That’s where **Services** step in:
- Provide a **stable endpoint** (IP and DNS)
- Load balance traffic across a group of Pods
- Simplify service discovery inside the cluster

---

## Types of Kubernetes Services

### ClusterIP (default)
- Internal communication only
- Used when apps talk to each other inside the cluster

> Example: `frontend` Pod calling the `backend` service by name

### NodePort
- Exposes a service on **each node’s IP** at a fixed port (e.g., 30000–32767)
- Enables access from **outside the cluster**

> Good for dev/test environments or basic external exposure

### LoadBalancer
- Provisions a cloud-provider **external IP + load balancer**
- Common in production setups on AWS, GCP, Azure

> Ideal for exposing services to the internet

### ExternalName
- Maps the service to an **external DNS name**

> Useful when a Kubernetes workload needs to talk to an external system (e.g., database or API outside the cluster)

---

## How Services Work Internally

- Services **select Pods** using labels (`selector`)
- Kubernetes creates a **virtual IP (ClusterIP)** that routes to those Pods
- Traffic is balanced across the available Pods

### Example:

```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  selector:
    app: my-app
  ports:
    - port: 80
      targetPort: 8080
  type: ClusterIP

```
✅ This exposes Pods with label app: my-app on port 80 inside the cluster.


## Real-World Scenarios

| Use Case                              | Service Type        |
|---------------------------------------|--------------------|
| App-to-app internal communication     | ClusterIP          |
| Quick external access in dev          | NodePort           |
| Public access via cloud load balancer | LoadBalancer       |
| Connect to an external DB             | ExternalName       |

## Bonus: Ingress vs Service

A Service handles routing based on IP:Port, whereas an Ingress enables HTTP-based routing (e.g., /login, /cart) to multiple services behind a single IP.

We’ll explore Ingress in a future post!

## Conclusion

Kubernetes Services decouple your workload's location from how it's accessed.
They offer consistency, scalability, and discoverability — essential in microservice environments.

