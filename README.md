# 🚀 The Holodeck: Enterprise GitOps on Bare Metal

Welcome to the Holodeck. This repository isn't just a home lab—it's a fully automated, highly available Kubernetes proving ground built from the hypervisor up. 

Designed to bridge the gap between standard hardware and cloud-native architecture, this project transforms three bare-metal Dell Optiplex nodes running Proxmox into a self-healing, heavily monitored, and purely declarative enterprise environment. 

The core philosophy here is strict GitOps: **If it's running in the cluster, it lives in this repository.** No manual `kubectl` configurations. No configuration drift. Just automated, scalable infrastructure deployed seamlessly through ArgoCD.

## 🏗️ Architecture Overview

* **Infrastructure:** 3-node high-availability cluster running **Proxmox VE** on Dell Optiplex enterprise hardware.
* **Virtualization:** Kubernetes nodes are provisioned as Ubuntu Server Virtual Machines within the Proxmox environment, demonstrating resource allocation and hypervisor management.
* **Orchestration:** Lightweight, highly available **k3s** container orchestration.
* **GitOps Controller:** [ArgoCD](https://argoproj.github.io/cd/) configured with the "App of Apps" pattern for fully automated state synchronization.
* **Ingress & Routing:** Traefik Ingress Controller managing external traffic routing to internal services (e.g., `grafana.myholodeck.org`).
* **Observability Stack:** `kube-prometheus-stack` (Prometheus, Grafana, Alertmanager) deployed via Server-Side Apply to handle complex CRDs and monitor real-time hardware, node, and pod health.
* **Storage:** NFS external provisioning dynamically mapped from an Unraid storage array.

## 🛠️ Tech Stack

| Category | Technology | Purpose |
| :--- | :--- | :--- |
| **Hypervisor** | Proxmox VE | Type-1 bare-metal virtualization and resource management |
| **Orchestration** | Kubernetes (k3s) | Highly available container orchestration |
| **Storage** | Unraid (NFS) | Persistent volume provisioning for stateful applications |
| **GitOps** | ArgoCD | Continuous Deployment and declarative cluster state |
| **Monitoring** | Prometheus | Time-series database for hardware and cluster metrics |
| **Visualization** | Grafana | Dashboards for real-time compute resource tracking |
| **Networking** | Traefik | Reverse proxy and Ingress controller |

## ⚙️ Deployment Strategy

This cluster follows a strict GitOps methodology. **No manual `kubectl apply` commands are used in production.** 1. Infrastructure configurations and application manifests are committed to this repository.
2. ArgoCD detects the drift between the repository branch and the live cluster.
3. ArgoCD automatically synchronizes and applies the changes, ensuring the cluster always matches the declarative state defined in Git.

## 📈 Current Status & Roadmap (7-Day Sprint)

- [x] Provision Proxmox VMs and bootstrap k3s nodes
- [x] Configure NFS storage class via Unraid
- [x] Install and configure ArgoCD (App of Apps pattern)
- [x] Deploy full observability stack (Prometheus/Grafana)
- [x] Configure custom Traefik Ingress routing (`myholodeck.org`)
- [ ] Implement Sealed Secrets for encrypted configuration management
- [ ] Configure CI/CD pipelines via GitHub Actions
- [ ] Deploy custom automated workloads
- [ ] Implement cluster-wide log aggregation (Loki)
- [ ] Configure disaster recovery and state backups (Velero)
