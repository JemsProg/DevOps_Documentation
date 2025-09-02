# Kubernetes fundamentals

---

## 1. What is Kubernetes?

Kubernetes (often called **K8s**) is like the **manager of a big computer system**.  
It takes care of apps so that they always run, even if one part of the system fails.

- **How it works:**  
  - It runs apps inside **containers** (tiny boxes that package apps).  
  - It makes sure apps are running correctly, restarts them if they crash, and can run them on different machines.  

- **Why it’s important to learn:**  
  - Almost every big company uses it (Google, Netflix, TikTok).  
  - It’s the modern way to keep apps **always available**, **scalable**, and **automatic**.  
  - If you want to work in DevOps, Cloud, or Software Engineering → Kubernetes is essential.

```mermaid
graph TD
  A[User] -->|Request| B[API Server]
  B -->|Schedule| C[Scheduler]
  C --> D[Kubelet on Node]
  D --> E[Pod Running App]
```

---

## 2. Key Concepts: Pods, Services, Ingress, ConfigMap, Volumes, Secrets

### Pod
- The **smallest unit** in Kubernetes.  
- Holds **1 or more containers**.  

### Service
- A **stable address** to reach Pods.  

### Ingress
- A **gateway from the internet** into your cluster.  

### ConfigMap
- Stores **settings** (not secret).  

### Volumes
- Storage that Pods can use.  

### Secrets
- For **sensitive data** (passwords, API keys).  

```mermaid
graph TD
  A[User Request] --> B[Ingress]
  B --> C[Service]
  C --> D[Pod]
  D --> E[ConfigMap / Secrets / Volumes]
```

---

## 3. Running Applications

### Deployment (Stateless Apps)
- For apps that don’t need memory of the past (e.g., web server).  

### StatefulSet (Stateful Apps)
- For apps that **must remember data** (e.g., databases).  

```mermaid
graph TD
  A[Deployment] -->|Creates| B[Pods]
  C[StatefulSet] -->|Creates| D[Pods + Storage]
```

---

## 4. Node Processes (on each worker machine)

- **Kubelet** → Ensures Pods are running.  
- **Kube-Proxy** → Handles networking.  
- **Container Runtime** → Actually runs containers (like Docker).  

```mermaid
graph TD
  A[Node] --> B[Kubelet]
  A --> C[Kube-Proxy]
  A --> D[Container Runtime]
  D --> E[Running Pods]
```

---

## 5. How Everything Works Together

- A **Cluster** = many worker machines (Nodes).  
- Each Node runs Pods.  
- Control plane (masters) tells Nodes what to do.  

```mermaid
graph TD
  A[Control Plane] --> B[Node 1]
  A --> C[Node 2]
  A --> D[Node 3]
  B -->|Runs| E[Pods]
  C -->|Runs| F[Pods]
  D -->|Runs| G[Pods]
```

---

## 6. How to Interact with a Cluster

We use **kubectl** (command-line tool).

- **Schedule a Pod**  
  ```bash
  kubectl run nginx --image=nginx
  ```

- **Monitor Pods**  
  ```bash
  kubectl get pods
  kubectl describe pod <pod-name>
  ```

- **Reschedule / Restart Pod**  
  ```bash
  kubectl delete pod <pod-name>
  ```

```mermaid
sequenceDiagram
  participant U as User
  participant K as kubectl
  participant A as API Server
  participant N as Node
  U->>K: kubectl run nginx
  K->>A: Request to create Pod
  A->>N: Assign Pod to Node
  N->>U: Pod Running
```

---

## 7. The Master Processes (Control Plane)

- **API Server**  
  Receives and validates requests.  

- **Scheduler**  
  Decides where Pods run.  

- **Controller Manager**  
  Watches the cluster and heals it.  

- **etcd**  
  Stores all cluster data (the brain).  

```mermaid
graph TD
  A[User Request] --> B[API Server]
  B --> C[Scheduler]
  C --> D[Kubelet]
  D --> E[Pod Running]
  B --> F[Controller Manager]
  F --> C
  B --> G[etcd Database]
```

---

# 📌 Summary
Kubernetes is like a giant automatic system that:
- Runs apps in containers  
- Keeps them alive  
- Scales them up or down  
- Makes sure users can always connect  

And it does all this **without you manually babysitting servers**.
