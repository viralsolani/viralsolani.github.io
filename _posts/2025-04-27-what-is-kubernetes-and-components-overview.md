---
layout: post
title: "What is Kubernetes & Overview of Components"
date: 2025-04-27
author: "Viral Solani"
categories:
  - DevOps
  - Kubernetes
tags:
  - Kubernetes
  - Containers
  - Cloud Native
  - YAML
  - Infrastructure
---

# 🚀 What is Kubernetes?

Kubernetes (often abbreviated as **K8s**) is an open-source system for automating deployment, scaling, and management of containerized applications. Originally developed by Google, Kubernetes has become the industry standard for orchestrating containers at scale.

Instead of manually managing containers one-by-one, Kubernetes allows you to manage thousands of them efficiently using declarative configuration and robust tooling.

---

## Kubernetes Components Overview

Kubernetes is made up of several key components that work together to run your applications reliably at scale. Here's an overview:

### Cluster
- A **Cluster** is the top-level structure in Kubernetes that includes all components: control plane, worker nodes, and resources.

### Namespace
- A logical grouping used to isolate workloads within a cluster.
- Useful when multiple teams or environments (dev, test, prod) share the same cluster.

### Node
- A physical or virtual machine.
- Two types:
  - **Control Plane Node**: Manages the cluster.
  - **Worker Node**: Runs your application workloads.

### Pod
- The **smallest unit** in Kubernetes.
- Wraps one or more containers.
- Represents a single instance of a running process.

### Service
- Provides a stable IP and DNS name for accessing Pods.
- Can load balance across multiple Pods.
- Persists even if the underlying Pods are restarted or rescheduled.

### Ingress
- Manages external HTTP/S traffic and routes it to Services.
- Offers routing rules, SSL termination, and virtual hosting.

---

## Control Plane Components

### API Server
- Acts as the front-end to the cluster.
- All CLI commands or API requests go through the API Server.

### Kubelet
- Agent running on all Nodes.
- Communicates with the API Server to manage Pods on its Node.

### KubeCTL
- Command-line tool to interact with the Kubernetes API Server.

### Controller Manager
- Watches the current state of the cluster and ensures the desired state matches.
- Examples: Node controller, Replication controller, etc.

### Scheduler
- Decides which Node a Pod should run on based on resource availability.

### Cloud Controller Manager
- Integrates Kubernetes with Cloud Service Providers like AWS, Azure, or GCP.

---

## Networking & Policies

### Kube Proxy
- Maintains network rules and routes traffic inside the cluster.

### Network Policy
- Virtual firewall for controlling communication at the Pod or Namespace level.

---

## Configuration & Storage

### ConfigMap
- Stores non-sensitive config data as key-value pairs.

### Secret
- Stores sensitive data like passwords, tokens, or SSH keys.

### Volume
- Mounts persistent storage to Pods — either local or cloud-based.

---

## Workload Controllers

### Deployment
- Manages the rollout and lifecycle of Pods.
- Think of it as a blueprint for your application.

### ReplicaSet
- Ensures a specified number of identical Pods are running.
- Automatically replaces failed Pods.

### StatefulSet
- Designed for **stateful** applications like databases.
- Maintains order and identity of Pods.

---

## Conclusion

By understanding these core building blocks, you're better prepared to architect, deploy, and manage reliable, scalable applications on Kubernetes.

Let’s orchestrate the future! ☸️
