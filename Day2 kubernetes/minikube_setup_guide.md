# 🚀 Minikube + Kubernetes Local Setup Guide (Windows)

This guide will help you install and run **Kubernetes locally** using **Minikube** and **kubectl**, with PowerShell as your command line.

---

## 📥 1. Install the Requirements

### 1.1 Minikube
Download from the official page:  
👉 [Minikube Installation Guide](https://minikube.sigs.k8s.io/docs/start/)

### 1.2 kubectl (Kubernetes CLI)
Download from the official page:  
👉 [kubectl Installation Guide](https://kubernetes.io/docs/tasks/tools/)

### 1.3 Container Runtime / Driver
Minikube needs a way to run containers. Options:
- **Docker Desktop** (recommended on Windows).  
  👉 [Download Docker Desktop](https://www.docker.com/products/docker-desktop/)
- Or **Hyper-V** / **VirtualBox** as VM drivers if not using Docker.

---

## ⚡ 2. Start Minikube Cluster

Open **PowerShell** and run:

```powershell
# Start Minikube using Docker as the driver
minikube start --driver=docker
```

Check that your cluster is running:

```powershell
kubectl get nodes
```

You should see one node (your local Minikube VM).

---

## 🌐 3. Deploy an Nginx App

Run the following to create a deployment:

```powershell
kubectl create deployment nginx --image=nginx
```

Check your Pods:

```powershell
kubectl get pods
```

---

## 🔗 4. Expose Nginx with a Service

Create a Service to expose Nginx:

```powershell
kubectl expose deployment nginx --type=NodePort --port=80
```

Check Services:

```powershell
kubectl get svc
```

---

## 🌍 5. Access Nginx in Browser

Run:

```powershell
minikube service nginx
```

This will automatically open Nginx in your default browser.

---

## 🛠️ 6. Useful Commands

- Stop cluster:
```powershell
minikube stop
```

- Delete cluster:
```powershell
minikube delete
```

- View logs of a Pod:
```powershell
kubectl logs <pod-name>
```

- Restart a Deployment:
```powershell
kubectl rollout restart deployment nginx
```

---

## ✅ Summary

1. Install Minikube, kubectl, and Docker Desktop.  
2. Start cluster: `minikube start --driver=docker`  
3. Deploy Nginx: `kubectl create deployment nginx --image=nginx`  
4. Expose service: `kubectl expose deployment nginx --type=NodePort --port=80`  
5. Access app: `minikube service nginx`  

🎉 You now have a working Kubernetes cluster locally on your Windows machine!
