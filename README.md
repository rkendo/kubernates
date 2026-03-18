<img width="1400" height="646" alt="image" src="https://github.com/user-attachments/assets/5090bfae-03ba-419b-8554-08ccbb233bc8" /># The Kubernetes Control Plane, often called the Master or Control Node, is a set of components that collectively manage the state of a Kubernetes cluster.
It acts as the brain of the cluster, making worldwide decisions about the cluster (for example, scheduling), as well as detecting and responding to cluster events

Components of Control Plane:
🔹 Kube-API Server
🔹 Kube-Scheduler
🔹 Controller Manager
🔹 Etcd Database

If you’ve deployed apps on Kubernetes, you’ve used it.
But here’s what actually happens inside the Control Plane 👇

1️⃣ Kube-API Server – The Front Door
Every request (kubectl, CI/CD, controllers) hits the API Server.
It:
• Authenticates & authorizes (RBAC)
• Validates objects
• Updates cluster state
It’s the single source of truth.

2️⃣ etcd – The Brain’s Memory
Kubernetes stores the entire cluster state inside etcd (a distributed key-value store).
Pods, Deployments, Secrets, ConfigMaps — everything lives here.
If etcd is unhealthy → your cluster is effectively down.

3️⃣ Controller Manager – The Reconciliation Engine
This is where the magic happens.
Controllers constantly run control loops:
Desired State (YAML)
vs
Current State (Cluster Reality)
If replicas = 3 but running = 2 → it creates another Pod.
No human intervention needed.
This loop runs continuously.

4️⃣ Scheduler – The Decision Maker
The Scheduler watches for unscheduled Pods.
It selects the best node based on:
• Resource requests
• Taints & tolerations
• Affinity / anti-affinity
• Topology constraints
It assigns the Pod — but does not run it.

5️⃣ Kubelet – The Node Enforcer
On each node, Kubelet ensures containers are running as declared.
It talks to the container runtime (docker / containerd / CRI-O).
It reports status back to the API Server.
<img width="1400" height="646" alt="image" src="https://github.com/user-attachments/assets/6cd52797-cfc9-41cf-834c-650e42f73996" />

6️⃣ kube-proxy – Networking Layer
It maintains networking rules so Services can load balance traffic across Pods.

