---
layout: post
title: "How Kubernetes Works: The Architecture Behind the Scenes"
date: 2025-05-19
author: "Viral Solani"
categories:
  - DevOps
  - Kubernetes
tags:
  - Kubernetes
  - Architecture
  - Control Plane
  - Nodes
  - Cloud Native
---

# 🔧 How Kubernetes Works: The Architecture Behind the Scenes

> _Note: If you’re new to Kubernetes components, check out [Part 1 – What is Kubernetes & Overview of Components](https://viralsolani.github.io/devops/kubernetes/2025/05/12/what-is-kubernetes-and-components-overview.md.html) before diving into how it all works together._

Kubernetes is powerful — but understanding **how** it works under the hood makes it even more effective. Today, let’s break down the **Kubernetes architecture**, and see how various components like the Control Plane and Nodes work together to orchestrate containers.

---

## 🏗️ High-Level View

At a high level, Kubernetes has two main categories of components:

1. **Control Plane** – The brain 🧠 of the cluster  
2. **Worker Nodes** – The muscle 💪 where your workloads run

Let’s explore both.

---

## 🧠 Control Plane (Master Components)

The Control Plane is responsible for making global decisions about the cluster and responding to cluster events.

### 📡 API Server
- The front door to your Kubernetes cluster
- All commands (`kubectl`, REST calls) talk to the API server

### 🧮 Scheduler
- Assigns new Pods to Nodes
- Makes decisions based on resource availability, affinity rules, taints, etc.

### 🔄 Controller Manager
- Runs various background controllers
- Ensures the actual state matches the desired state
- Examples: Deployment Controller, Node Controller

### ☁️ Cloud Controller Manager
- Connects your Kubernetes cluster to your cloud provider (e.g., AWS, Azure, GCP)
- Manages external load balancers, persistent volumes, etc.

### 🧠 etcd
- A distributed key-value store used to persist cluster state
- Stores data like Pod status, config maps, secrets, etc.

---

## 💪 Worker Nodes (Where Pods Run)

Worker Nodes host the actual **containers** (via Pods). Each node has the following key components:

### 👷 Kubelet
- An agent that runs on each node
- Communicates with the API Server
- Ensures containers are running as expected

### 🔗 Kube Proxy
- Handles networking for Pods on the Node
- Implements service discovery and routing rules

### 🐳 Container Runtime
- The software that runs containers (e.g., containerd, Docker, CRI-O)

---

## 🔁 How It All Works (End-to-End Flow)

1. You submit a YAML file to the API Server (`kubectl apply -f app.yaml`)  
2. The API Server stores this data in `etcd`  
3. The Scheduler identifies a Node to run the Pod  
4. The Controller Manager ensures the required number of Pods are maintained  
5. The Kubelet on that Node pulls the container image and starts the Pod  
6. The Kube Proxy routes traffic to your app based on Services  

---

## 🧭 Diagram Summary

        +------------------------+
        |     kubectl/API       |
        +------------------------+
                    |
                    v
    +------------------------------------+
    |           Control Plane            |
    |------------------------------------|
    |  API Server  | Scheduler | etcd    |
    |  Controllers | CloudMgr  |         |
    +------------------------------------+
                    |
                    v
    +--------------------+     +--------------------+
    |   Worker Node 1    | ... |   Worker Node N    |
    +--------------------+     +--------------------+
    | Kubelet | KubeProxy|     | Kubelet | KubeProxy|
    | Pods    | Runtime  |     | Pods    | Runtime  |
    +--------------------+     +--------------------+


---

## 🎯 Conclusion

Kubernetes architecture may look complex at first, but it follows a clean separation of concerns:
- The **Control Plane** manages the cluster  
- The **Worker Nodes** run the workloads

Once you understand these internals, debugging and scaling your apps gets much easier.