
# Multi-Node OpenStack Private Cloud

A multi-node private cloud infrastructure built using **OpenStack Antelope (2023.1)**, **Kolla-Ansible**, and **Ubuntu Server 22.04**. The platform provides multi-tenant IaaS and additional cloud services for students.

## Overview

This project focuses on building and expanding a private cloud environment using multiple physical servers. The infrastructure provides virtual machine provisioning, networking, storage, monitoring, and additional services.

The platform was initially deployed across three bare-metal nodes and later expanded with a fourth compute node.

## Infrastructure Architecture

| Node | Role |
|---|---|
| Controller | OpenStack control-plane services |
| Compute1 | Virtual machine workloads |
| Storage | Storage services |
| Compute2 | Additional compute capacity |

### Compute2 Hardware

A Dell Precision 7960 Tower workstation provided by Samsung Innovation Lab was integrated as the additional compute node.

- **Processor:** Intel Xeon w9-3475X (36 Cores / 72 Threads)
- **Memory:** 256 GB RAM
- **Storage:** Approximately 13 TB raw capacity

## OpenStack Services

Deployed using Kolla-Ansible on Ubuntu Server 22.04.

| Service | Purpose |
|---|---|
| Nova | Compute and virtual machine management |
| Neutron | Network management |
| Keystone | Identity and authentication |
| Glance | Virtual machine images |
| Cinder | Block storage |
| Swift | Object storage |
| Skyline | Cloud dashboard |
| Horizon | Administrative dashboard |
| Heat | Infrastructure orchestration |

## Networking

Configured cloud networking using:

- Open vSwitch (OVS)
- VXLAN tenant networks
- Provider networks
- Network routing
- Floating IP configuration
- Tenant network isolation

## Cloud Services

### 1. Student Cloud Dashboard

Skyline provides the student-facing cloud dashboard.

- https://cloud.openstacklab.me

Horizon is reserved for cloud-provider administration.

### 2. Personal Cloud Storage

Integrated OpenStack Swift with Nextcloud to provide personal file storage with account-level user separation.

- Web access: https://drive.openstacklab.me
- Mobile access through Nextcloud Android and iOS applications.

### 3. Infrastructure Monitoring

Implemented Prometheus and Grafana for infrastructure and workload monitoring.

- Dashboard: https://monitor.openstacklab.me
- User-scoped dashboards for students.
- Separate administrative monitoring.

### 4. Database-as-a-Service

Configured relational Database-as-a-Service capabilities.

- https://db.openstacklab.me

### 5. Kubernetes as a Service (KaaS)

Deployed a separate Kubernetes cluster on four virtual machines provisioned through OpenStack.

| Component | Configuration |
|---|---|
| Control Plane | 1 VM |
| Worker Nodes | 3 VMs |
| CPU per VM | 6 vCPUs |
| RAM per VM | 24 GB |
| Kubernetes Version | v1.30.14 |
| Cluster Setup | kubeadm |
| Container Runtime | containerd |
| CNI | Calico |

Additional details:

- Hosted containerized workloads.
- Deployed Coder & Chatwoot within Kubernetes.
- Configured remote Kubernetes API access through Cloudflare Tunnel.
- Enabled authenticated access from external machines using `kubectl` and appropriately scoped kubeconfig files.
- Kubernetes dashboard: https://kubernetes.openstacklab.me

### 6. Developer Services

- Deployed Jupyter with keycloak authentication(Available: https://jupyter.openstacklab.me)
- Deployed Coder for developer environment(Available: https://coder.kuberneteslab.me).
- Deployed Chatwoot to increase developer productivity and efficiency(Available: https://chatwoot.kuberneteslab.me). 

## Remote Access

Configured Cloudflare Tunnel to provide remote access to selected cloud services through the custom domain:

- https://openstacklab.me
- https://kuberneteslab.me

The tunnel also supports remote access to the Kubernetes API endpoint.

## Infrastructure as Code

Tested OpenStack Heat templates for infrastructure orchestration and automated resource provisioning.

## Resilience and High Availability

The infrastructure uses multiple nodes and incorporates logical resilience considerations.

However:
- Full OpenStack control-plane redundancy was not implemented due to hardware resource constraints.
- The Kubernetes cluster has a single control-plane node.
- Workload recovery was tested by deleting an NGINX pod and observing its automatic replacement by the Kubernetes ReplicaSet.

Application continuity was observed during this test; this does not guarantee zero downtime.

## Testing and Validation

- Virtual machine provisioning through OpenStack.
- Tenant and provider network configuration.
- Routing and floating IP connectivity.
- Swift and Nextcloud storage integration.
- OpenStack Heat template testing.
- Kubernetes workload deployment.
- NGINX pod deletion and automatic recovery testing.
- Remote Kubernetes API connectivity.

## Technology Stack

**Cloud Infrastructure:** OpenStack Antelope, Kolla-Ansible, Ansible

**Virtualization & Containers:** Docker, Kubernetes, containerd

**Networking:** Open vSwitch, Neutron, VXLAN, Calico

**Storage:** Cinder, Swift, Nextcloud

**Monitoring:** Prometheus, Grafana

**Orchestration:** OpenStack Heat

**Identity & Access:** Keystone, Keycloak, Kubernetes RBAC

**Remote Access:** Cloudflare Tunnel

**Additional Services:** Jupyter, Coder

**Operating System:** Ubuntu Server 22.04

## Project Highlights

- Built and expanded a multi-node OpenStack private cloud.
- Integrated additional enterprise-grade compute hardware.
- Implemented multi-tenant networking and storage.
- Provided student-facing cloud services.
- Integrated Nextcloud with OpenStack Swift.
- Deployed a separate Kubernetes cluster on OpenStack.
- Enabled remote access to selected cloud services.
- Implemented infrastructure monitoring using Prometheus and Grafana.

---

**Project:** Multi-Node OpenStack Private Cloud  
**Platform:** OpenStack Antelope (2023.1)  
**Deployment:** Kolla-Ansible  
**Environment:** Ubuntu Server 22.04
