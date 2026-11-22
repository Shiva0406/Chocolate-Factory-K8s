# 🍫 Chocolate Factory – Kubernetes Deployment

A simple static website deployed on a Kubernetes Kind cluster using Nginx, ConfigMap,  Deployment and NodePort Service.

## 📁 Project Structure

```text
chocolate-factory/
│
├── index.html
│
└── k8s/
    ├── 01-configmap.yaml
    ├── 02-deployment.yaml
    └── 03-service.yaml
```

## 🛠️ Prerequisites

Make sure the following tools are installed:

- AWS EC2 Ubuntu
- Docker
- Kind
- kubectl

## 🚀 Deployment Steps

### Step 1: Start Docker

```bash
sudo systemctl start docker
```

### Step 2: Check Kind Cluster

```bash
kind get clusters
kubectl get nodes
```

If the cluster does not exist, create it:

```bash
kind create cluster --name tws-cluster
```

### Step 3: Navigate to Project

```bash
cd ~/chocolate-factory
```

### Step 4: Deploy Kubernetes Resources

```bash
kubectl apply -f k8s/
```

### Step 5: Verify Deployment

```bash
kubectl get pods
kubectl get deployments
kubectl get services
```

Wait until both pods show `Running`.

### Step 6: Access the Website

Run port forwarding:

```bash
kubectl port-forward service/chocolate-service 8088:80 --address 0.0.0.0
```

Keep this terminal running.

### Step 7: Configure AWS Security Group

Allow the following inbound traffic:

| Type | Protocol | Port | Source |
|---|---|---|---|
| Custom TCP | TCP | 8080 | My IP |

### Step 8: Open Website

Open your browser:

```text
http://YOUR-EC2-PUBLIC-IP:8088
```

Replace `YOUR-EC2-PUBLIC-IP` with your EC2 public IPv4 address.

## 🔍 Useful Kubernetes Commands

| Command | Purpose |
|---|---|
| `kubectl get pods` | Check pods |
| `kubectl get deployments` | Check deployments |
| `kubectl get services` | Check services |
| `kubectl get all` | List resources |
| `kubectl describe pod POD_NAME` | Inspect a pod |
| `kubectl logs POD_NAME` | View pod logs |
| `kubectl scale deployment chocolate-deployment --replicas=4` | Scale pods |
| `kubectl delete -f k8s/` | Delete project resources |

## 🧹 Cleanup

To remove the deployed application:

```bash
kubectl delete -f k8s/
```

To delete the Kind cluster:

```bash
kind delete cluster --name tws-cluster
```

## 📚 Technologies Used

- AWS EC2 – Cloud server
- Docker – Container runtime
- Kind – Local Kubernetes cluster
- Kubernetes – Container orchestration
- Nginx – Web server
- ConfigMap – Website configuration
- YAML – Kubernetes resource definitions

---

**Project:** Chocolate Factory Website

**Deployment:** Kubernetes using Kind

**Purpose:** Beginner-friendly Kubernetes deployment practice.
