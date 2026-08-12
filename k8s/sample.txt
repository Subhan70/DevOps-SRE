1. Why Kubernetes?
Problem without Kubernetes

Suppose you have:

Container 1 → Application
Container 2 → Database
Container 3 → Redis

Problems:

Container crashes
Manual restart needed
Difficult scaling
Difficult networking
Hard to manage 100+ containers
Kubernetes Solution
Kubernetes =
Container Manager

It:
✓ Starts containers
✓ Restarts failed containers
✓ Scales applications
✓ Handles networking
✓ Handles storage
2. Simple Real-Time Example

Imagine a food delivery company.

Manager → Kubernetes Master Node
Workers → Worker Nodes
Food Boxes → Containers
Group of Food Boxes → Pod
Customers → Users

Manager assigns work to workers.

Similarly:

Control Plane → Manages
Worker Nodes → Run Applications
3. Kubernetes Architecture
                Control Plane
          +---------------------+
          | API Server          |
          | Scheduler           |
          | Controller Manager  |
          | ETCD               |
          +---------------------+
                     |
     --------------------------------
     |                              |
+-----------+                +-----------+
| Worker-1  |                | Worker-2  |
| Pods      |                | Pods      |
+-----------+                +-----------+
4. Control Plane Components
API Server

Entry point of Kubernetes.

kubectl → API Server → Cluster

Example:

kubectl get pods
ETCD

Database of Kubernetes.

Stores:

Pods
Nodes
Services
Secrets
Configurations
Scheduler

Decides:

Which pod runs on which node
Controller Manager

Checks:

Desired Pods = Actual Pods

Example:

Desired = 3 Pods
Running = 2 Pods

Controller creates 1 more Pod
5. Worker Node Components
Worker Node
├── Kubelet
├── Container Runtime
└── Kube Proxy
Kubelet

Node agent.

Checks:

Are pods running?
Container Runtime

Examples:

Containerd
CRI-O
Docker (older)

Runs containers.

Kube Proxy

Handles networking.

6. Pod

Smallest object in Kubernetes.

Pod
 ├── Container-1
 └── Container-2

Example:

Nginx Container
Log Container

Create Pod:

kubectl run nginx --image=nginx

Check:

kubectl get pods
7. ReplicaSet

Maintains required pod count.

Example:

Required = 3 Pods

One Pod crashes

ReplicaSet creates another Pod
8. Deployment

Deployment manages ReplicaSets.

Example:

Deployment
     ↓
ReplicaSet
     ↓
Pods

Features:

Scaling
Rolling Update
Rollback

Create:

kubectl create deployment nginx --image=nginx
9. Service

Pods IPs change.

Service gives fixed access.

Types:

ClusterIP
NodePort
LoadBalancer

Example:

User
   ↓
Service
   ↓
Pods
10. Namespace

Separates environments.

Example:

default
dev
test
prod

Commands:

kubectl get ns

kubectl create ns dev
11. ConfigMap

Stores normal configuration.

Example:

DB_HOST
APP_PORT
URL
12. Secret

Stores sensitive information.

Example:

Passwords
Tokens
API Keys
13. Volumes

Without volume:

Pod deleted
Data lost

With volume:

Data persists
14. Ingress

Single entry point.

Without Ingress:

App1 → LoadBalancer
App2 → LoadBalancer
App3 → LoadBalancer

With Ingress:

One LoadBalancer
        ↓
Ingress
 ├── app1.com
 ├── app2.com
 └── app3.com
15. Important Commands
kubectl get nodes

kubectl get pods

kubectl get deployments

kubectl get svc

kubectl get ns

kubectl describe pod <pod>

kubectl logs <pod>

kubectl exec -it <pod> -- /bin/bash

kubectl delete pod <pod>

kubectl apply -f file.yaml
16. YAML Structure
apiVersion: v1
kind: Pod

metadata:
  name: nginx

spec:
  containers:
  - name: nginx
    image: nginx

Explain:

apiVersion → API version
kind → Object type
metadata → Name
spec → Configuration
17. Kubernetes Learning Order
Linux
↓
Docker
↓
Kubernetes Architecture
↓
Pod
↓
ReplicaSet
↓
Deployment
↓
Service
↓
Namespace
↓
ConfigMap
↓
Secret
↓
Volume
↓
Ingress
↓
Troubleshooting
