# ☸️ Kubernetes in One Shot

A **beginner-to-advanced Kubernetes learning repository** containing essential Kubernetes concepts, practical commands, YAML manifests, deployment examples, troubleshooting techniques, and cloud-native tools.

This repository is designed as a **one-shot Kubernetes reference** for DevOps learners who want to learn Kubernetes practically and use it in real-world projects.

### 🚀 Resources

<p align="left">
  <img src="https://img.shields.io/badge/Kubernetes-326CE5?style=for-the-badge&logo=kubernetes&logoColor=white" />
  <img src="https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white" />
  <img src="https://img.shields.io/badge/Helm-0F1689?style=for-the-badge&logo=helm&logoColor=white" />
  <img src="https://img.shields.io/badge/AWS-232F3E?style=for-the-badge&logo=amazonaws&logoColor=white" />
  <img src="https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black" />
  <img src="https://img.shields.io/badge/Git-F05032?style=for-the-badge&logo=git&logoColor=white" />
</p>

---

## 📚 Table of Contents

* [What is Kubernetes?](#-what-is-kubernetes)
* [Kubernetes Architecture](#-kubernetes-architecture)
* [Cluster Setup](#-cluster-setup)
* [Kubectl Commands](#-kubectl-commands)
* [Namespaces](#-namespaces)
* [Workloads](#-workloads)
* [Networking](#-networking)
* [Storage](#-storage)
* [Configuration](#-configuration)
* [Scaling & Scheduling](#-scaling--scheduling)
* [RBAC & Security](#-rbac--security)
* [Monitoring & Logging](#-monitoring--logging)
* [Helm](#-helm)
* [Advanced Kubernetes](#-advanced-kubernetes)
* [Cloud Kubernetes](#-cloud-kubernetes)
* [Troubleshooting](#-troubleshooting)
* [Projects](#-projects)
* [Learning Path](#-learning-path)

---

# ☸️ What is Kubernetes?

**Kubernetes (K8s)** is an open-source container orchestration platform used to automate:

* 🚀 Container deployment
* 📈 Application scaling
* 🔄 Rolling updates
* 🔧 Self-healing
* 🌐 Service discovery
* ⚖️ Load balancing
* 🔐 Configuration & secrets management
* 💾 Persistent storage

Kubernetes is widely used in modern **DevOps, Cloud and Microservices environments**.

---

# 🏗️ Kubernetes Architecture

A Kubernetes cluster consists mainly of:

### Control Plane

* API Server
* Scheduler
* Controller Manager
* etcd

### Worker Node

* kubelet
* kube-proxy
* Container Runtime
* Pods

Useful command:

```bash
kubectl cluster-info
```

---

# 🛠️ Cluster Setup

## Kind

Create a local Kubernetes cluster using Kind:

```bash
kind create cluster --name tws-cluster --config config.yml
```

Check clusters:

```bash
kind get clusters
```

Switch Kubernetes context:

```bash
kubectl config use-context kind-tws-cluster
```

Check cluster nodes:

```bash
kubectl get nodes
```

---

# ⌨️ Kubectl Commands

`kubectl` is the primary CLI tool for interacting with Kubernetes clusters.

### Get Resources

```bash
kubectl get pods
kubectl get nodes
kubectl get deployments
kubectl get services
kubectl get all
```

### Detailed Information

```bash
kubectl describe pod nginx
kubectl describe deployment nginx
kubectl describe service nginx
```

### Create a Pod

```bash
kubectl run nginx --image=nginx
```

### Delete a Resource

```bash
kubectl delete pod nginx
```

### Apply YAML

```bash
kubectl apply -f deployment.yml
```

---

# 📦 Namespaces

Namespaces provide logical isolation inside a Kubernetes cluster.

Create namespace:

```bash
kubectl create namespace monitoring
```

List namespaces:

```bash
kubectl get namespaces
```

Add a label:

```bash
kubectl label namespace monitoring team=devops
```

Describe namespace:

```bash
kubectl describe namespace monitoring
```

---

# 🚀 Workloads

## Deployment

Deploy an application:

```bash
kubectl apply -f deployment.yml
```

Scale deployment:

```bash
kubectl scale deployment nginx-deployment --replicas=3 -n nginx
```

Check deployment:

```bash
kubectl get deployments
```

---

## StatefulSet

Useful for stateful applications such as databases.

```bash
kubectl apply -f statefulset.yml
```

```bash
kubectl describe statefulset mysql -n database
```

---

## DaemonSet

Runs a pod on each eligible node.

```bash
kubectl apply -f daemonset.yml
```

```bash
kubectl describe daemonset fluentd -n logging
```

---

## ReplicaSet

Maintains a specified number of pod replicas.

```bash
kubectl apply -f replicaset.yml
```

```bash
kubectl describe replicaset nginx-replicaset -n nginx
```

---

## Jobs

```bash
kubectl apply -f job.yml
```

## CronJobs

```bash
kubectl apply -f cronjob.yml
```

---

# 🌐 Networking

## Services

List services:

```bash
kubectl get svc -A
```

Create a service:

```bash
kubectl apply -f service.yml
```

Describe service:

```bash
kubectl describe svc nginx-service -n nginx
```

---

## Ingress

Ingress manages external HTTP/HTTPS access to services.

```bash
kubectl apply -f ingress.yml
```

```bash
kubectl describe ingress nginx-ingress -n nginx
```

---

## Network Policies

Control communication between pods:

```bash
kubectl apply -f networkpolicy.yml
```

---

# 💾 Storage

## PersistentVolume

```bash
kubectl apply -f persistentVolume.yml
```

## PersistentVolumeClaim

```bash
kubectl apply -f persistentVolumeClaim.yml
```

## StorageClass

```bash
kubectl get storageclass
```

---

# ⚙️ Configuration

## ConfigMap

Create ConfigMap from a file:

```bash
kubectl create configmap app-config \
  --from-file=config.properties
```

View ConfigMaps:

```bash
kubectl get configmaps
```

---

## Secrets

Create a Secret:

```bash
kubectl create secret generic db-credentials \
  --from-literal=username=admin \
  --from-literal=password=admin123
```

> ⚠️ Never commit real passwords, API keys, tokens, or credentials to GitHub.

---

# 📈 Scaling & Scheduling

## Horizontal Pod Autoscaler

```bash
kubectl autoscale deployment nginx \
  --cpu-percent=50 \
  --min=1 \
  --max=10 \
  -n nginx
```

Check HPA:

```bash
kubectl get hpa
```

---

## Vertical Pod Autoscaler

```bash
kubectl apply -f vpa.yml
```

---

## Taints & Tolerations

Apply a taint:

```bash
kubectl taint nodes node1 key=value:NoSchedule
```

---

## Node Affinity

```bash
kubectl apply -f node-affinity.yml
```

---

# 📊 Resource Management

## ResourceQuota

```bash
kubectl apply -f resourcequota.yml
```

Check quota:

```bash
kubectl describe quota my-quota -n dev
```

---

## Probes

Kubernetes supports:

* ❤️ Liveness Probe
* 🩺 Readiness Probe
* 🚀 Startup Probe

These help Kubernetes determine whether an application is healthy and ready to receive traffic.

---

# 🔐 RBAC & Security

## Role

```bash
kubectl apply -f role.yml
```

## RoleBinding

```bash
kubectl apply -f rolebinding.yml
```

Check RBAC resources:

```bash
kubectl get roles
kubectl get rolebindings
```

---

## Custom Resource Definitions

Create CRD:

```bash
kubectl apply -f crd.yml
```

List CRDs:

```bash
kubectl get crd
```

---

# 📊 Monitoring & Logging

## Metrics Server

Deploy Metrics Server:

```bash
kubectl apply -f metrics-server.yml
```

View node resource usage:

```bash
kubectl top nodes
```

View pod resource usage:

```bash
kubectl top pods
```

---

## Prometheus & Grafana

Install the Prometheus + Grafana stack using Helm:

```bash
helm install prometheus-stack \
  prometheus-community/kube-prometheus-stack \
  --namespace monitoring \
  --create-namespace
```

Access Grafana:

```bash
kubectl port-forward \
  svc/prometheus-stack-grafana \
  3000:80 \
  -n monitoring \
  --address=0.0.0.0
```

---

# ⛵ Helm

Helm is the package manager for Kubernetes.

Create a chart:

```bash
helm create my-chart
```

Install a chart:

```bash
helm install my-app my-chart \
  -n my-namespace \
  --create-namespace
```

List Helm releases:

```bash
helm list -A
```

Upgrade:

```bash
helm upgrade my-app my-chart
```

Uninstall:

```bash
helm uninstall my-app
```

---

# 🔥 Advanced Kubernetes

## Init Containers

```bash
kubectl apply -f init-container.yml
```

Init Containers run before the application's main containers.

---

## Sidecar Containers

```bash
kubectl apply -f sidecar-container.yml
```

Sidecar containers run alongside the main application container to provide supporting functionality such as logging, proxying, or monitoring.

---

# ☁️ Cloud-Native Kubernetes

Kubernetes is available through managed cloud services such as:

* ☁️ AWS EKS
* ☁️ Azure AKS
* ☁️ Google GKE

### AWS EKS

Create an EKS cluster:

```bash
eksctl create cluster --name my-cluster
```

---

## Cluster Autoscaler

```bash
kubectl apply -f cluster-autoscaler.yml
```

---

# 🐛 Debugging & Troubleshooting

Check pod status:

```bash
kubectl get pods
```

Detailed pod information:

```bash
kubectl describe pod pod-name -n namespace
```

View logs:

```bash
kubectl logs pod-name -n namespace
```

Follow logs:

```bash
kubectl logs -f pod-name -n namespace
```

Execute commands inside a container:

```bash
kubectl exec -it pod-name -n namespace -- bash
```

Check events:

```bash
kubectl get events -A
```

---

# 🧪 Practical Projects

This repository is focused on **hands-on Kubernetes learning**.

## 🗳️ Kubernetes Voting App

A Kubernetes-based voting application demonstrating:

* Pods
* Deployments
* Services
* ConfigMaps
* Kubernetes networking
* Monitoring

---

## 💬 Full Stack Chat Application

Deploy a full-stack application using Kubernetes and modern DevOps practices.

---

## 🔄 CI/CD with Kubernetes

Practice Kubernetes deployment with CI/CD technologies such as:

* Jenkins
* GitHub Actions
* ArgoCD

---

# 🗺️ Learning Path

Recommended order for learning Kubernetes:

```text
Linux
  ↓
Docker
  ↓
Kubernetes Fundamentals
  ↓
Pods
  ↓
Deployments
  ↓
Services
  ↓
ConfigMaps & Secrets
  ↓
Storage
  ↓
Ingress
  ↓
Probes & Resources
  ↓
RBAC
  ↓
Helm
  ↓
Monitoring
  ↓
CI/CD
  ↓
AWS EKS
  ↓
Advanced Kubernetes
```

---

# 🎯 Goal

The goal of this repository is to build a **strong practical foundation in Kubernetes** and understand how Kubernetes is used in real-world DevOps and cloud-native environments.

> **Learn → Practice → Deploy → Monitor → Troubleshoot → Automate**

---

# 📚 Resources

* ☸️ Kubernetes Documentation — https://kubernetes.io/docs/
* 🐳 Docker Documentation — https://docs.docker.com/
* ⛵ Helm Documentation — https://helm.sh/docs/
* ☁️ AWS EKS — https://aws.amazon.com/eks/
* 📈 Prometheus — https://prometheus.io/
* 📊 Grafana — https://grafana.com/

---

# 👨‍💻 Author

**Muhammad Hussnain Ashiq**

DevOps & Cloud Learning Journey 🚀

This repository is part of my practical journey toward becoming a **DevOps / Cloud Engineer**.

---

## ⭐ Support

If this repository helps you learn Kubernetes, consider giving it a ⭐ on GitHub.

**Happy Learning & Keep Building! 🚀☸️**
