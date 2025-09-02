# Kubernetes Local Setup Guide

## 1. 🟦 Minikube
This is what creates a mini Kubernetes cluster on your computer.

Without Minikube, you don’t actually have Kubernetes running locally.

You’ll use it to start, stop, and manage your local cluster.

👉 **Example command:**
```bash
minikube start
```

---

## 2. 🟨 kubectl (Kubernetes CLI)
This is the remote control for Kubernetes.

Once Minikube starts your cluster, you need a way to talk to it → that’s kubectl.

With kubectl, you can create Pods, deploy nginx, expose services, etc.

👉 **Example command:**
```bash
kubectl create deployment my-nginx --image=nginx
```

---

## 3. 🟩 Container Runtime / Driver
Kubernetes itself doesn’t run containers — it needs a “driver” to do that.

Think of it like Kubernetes is the bus driver, but it needs an engine to move the bus.

### Options:
- Docker Desktop (recommended ✅ for Windows/Mac) → most popular container runtime.
- VirtualBox / Hyper-V if you don’t want Docker.

👉 Without this, your Pods (like nginx) cannot actually start because there’s nothing to run containers.

---

## ⚡ Why all 3 are needed together
- **Minikube** → makes the Kubernetes cluster.
- **kubectl** → lets you control that cluster.
- **Docker Desktop (or driver)** → runs the actual containers (like nginx).

---

## 🎓 Simple Analogy
- **Minikube** = a mini “school” you just built (the Kubernetes cluster).
- **kubectl** = the walkie-talkie to give instructions to the school.
- **Docker Desktop** = the electricity that powers the classrooms (containers).

If one is missing → the whole system doesn’t work.

---

## ✅ For your task (“instantiate locally and deploy nginx”), you need:
1. Minikube (to run Kubernetes)
2. kubectl (to control it)
3. Docker Desktop (to actually run nginx in a container)
