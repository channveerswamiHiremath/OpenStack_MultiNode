# Multi-Node Private Cloud Infrastructure Using OpenStack and Kolla-Ansible

## Project Overview

Designed, deployed and expanded a multi-node private cloud infrastructure using OpenStack Antelope (2023.1) and Kolla-Ansible on Ubuntu Server 22.04.

The project started with a three-node bare-metal deployment consisting of Controller, Compute1 and Storage nodes. It was later expanded by integrating a high-performance Dell Precision 7960 workstation as an additional Compute2 node.

The infrastructure was further extended into a multi-tenant cloud platform, providing virtual machine provisioning, networking, object storage, monitoring, database access and developer services for students.

## Infrastructure Architecture

The cloud infrastructure consists of four physical nodes:

- **Controller Node:** Hosts OpenStack control-plane and API services.
- **Compute1 Node:** Provides virtual machine compute resources.
- **Storage Node:** Provides storage resources for the cloud environment.
- **Compute2 Node:** Additional compute capacity provided by a Dell Precision 7960 workstation from Samsung Innovation Lab.

### Compute2 Hardware Specifications

- Processor: Intel Xeon w9-3475X
- CPU: 36 Cores / 72 Threads
- RAM: 256 GB
- Storage: Approximately 13 TB raw capacity

The additional workstation significantly expanded the available compute and storage resources.

## Technologies Used

**Cloud Infrastructure**
- OpenStack Antelope (2023.1)
- Kolla-Ansible
- Ansible
- Docker
- Ubuntu Server 22.04

**OpenStack Services**
- Nova – Compute
- Neutron – Networking
- Keystone – Identity
- Glance – Image Management
- Cinder – Block Storage
- Swift – Object Storage
- Skyline – Cloud Dashboard
- Horizon – Administrative Dashboard
- Heat – Infrastructure as Code
- Trove - DataBase as a Service

**Networking**
- Open vSwitch (OVS)
- VXLAN
- Provider Networks
- Floating IPs
- Virtual Routers
- Cloudflare Tunnel

**Monitoring and Storage**
- Prometheus
- Grafana
- Nextcloud
- OpenStack Swift

**DevOps and Developer Services**
- GitLab
- Jenkins
- Dokku
- Jupyter
- Keycloak
- Coder
- Kubernetes

## Cloud Services Provided

### 1. Cloud Management Dashboard

Configured OpenStack Skyline as the primary user-facing dashboard for students.

- Hosted at: https://cloud.openstacklab.me
- Horizon administrative access restricted to cloud providers.

### 2. Object Storage as a Service

Integrated OpenStack Swift with Nextcloud to provide a familiar cloud storage experience.

- Hosted at: https://drive.openstacklab.me
- Student-specific storage access and isolation.
- Web-based file management.
- Android and iOS mobile application support.

### 3. Monitoring as a Service

Implemented Prometheus and Grafana for infrastructure and virtual machine monitoring.

- Hosted at: https://monitor.openstacklab.me
- User-scoped dashboards for individual projects and virtual machines.
- 24 monitoring panels configured for student-facing dashboards.
- Extended administrative monitoring for cloud operators.

### 4. Database as a Service

Configured relational database environments for student projects.

- Hosted at: https://db.openstacklab.me
- Provides database access for application development.

### 5. Infrastructure as Code

Tested OpenStack Heat templates for declarative infrastructure provisioning, enabling resources to be created using predefined configuration templates.

## DevOps and Application Hosting

Integrated GitLab, Jenkins and Dokku to implement an application deployment workflow.

The workflow:

1. User pushes application code to GitLab.
2. Jenkins detects the repository update.
3. Jenkins executes the configured pipeline.
4. The deployment workflow forwards the application to Dokku.
5. Dokku hosts the deployed application.

Additional developer services:

- **Jupyter:** Hosted development and notebook environment with Keycloak authentication.
- **Coder:** Browser-based development environment deployed within Kubernetes.

## Remote Access and Networking

Configured Cloudflare Tunnel to provide remote access to selected cloud services using the custom domain:

**openstacklab.me**

Configured dedicated subdomains for Skyline, Nextcloud, Grafana and database access.

This allows authorized users to access selected services remotely without directly exposing each service through public inbound networking.

## Kubernetes Integration

Deployed a separate four-node Kubernetes cluster using virtual machines provisioned through OpenStack.

The cluster consists of:

- 1 Control Plane Node
- 3 Worker Nodes
- 24 GB RAM and 6 vCPUs per virtual machine

Technologies used:

- Kubernetes v1.30.14
- kubeadm
- containerd
- Calico

Tested application deployment, workload replication, pod recovery and self-healing behaviour.

The Kubernetes cluster is an independent workload hosted on OpenStack and is documented separately as another project.

## High Availability Considerations

Designed the platform with logical high-availability and resilience principles.

Workload replication and recovery behaviour were tested in the Kubernetes environment.

A fully redundant OpenStack control plane was not implemented due to available hardware resource constraints. Therefore, the deployment demonstrates multi-node infrastructure and HA-oriented design considerations rather than a fully redundant control-plane architecture.

## Implementation Challenges

During implementation, several infrastructure and configuration challenges were encountered:

- Kolla-Ansible deployment and Ansible dependency issues.
- Open vSwitch networking and tenant connectivity.
- VXLAN networking and routing configuration.
- Storage service configuration and integration.
- Integration of an additional physical compute node.
- Secure remote access through Cloudflare Tunnel.
- Multi-tenant access and user-specific monitoring configuration.

These challenges provided practical experience in troubleshooting distributed cloud infrastructure.

## Results and Outcomes

- Successfully deployed a multi-node OpenStack private cloud.
- Expanded the original three-node environment with a fourth physical Compute2 node.
- Integrated high-performance hardware with 256 GB RAM.
- Provided cloud dashboards and isolated storage for student users.
- Implemented user-scoped virtual machine monitoring.
- Configured relational database access.
- Tested template-based infrastructure provisioning.
- Integrated GitLab, Jenkins and Dokku for application deployment.
- Deployed additional developer services.
- Hosted an independent Kubernetes cluster on OpenStack virtual machines.
- Enabled remote access to selected cloud services through Cloudflare Tunnel.

## Learning Outcomes

- Practical understanding of distributed OpenStack architecture.
- Experience with multi-node cloud deployment and scaling.
- Understanding of software-defined networking using Open vSwitch and VXLAN.
- Experience with cloud storage integration and multi-tenancy.
- Hands-on experience with monitoring and observability.
- Understanding of Infrastructure as Code and DevOps workflows.
- Experience integrating Kubernetes with private cloud infrastructure.
- Practical Linux system administration and infrastructure troubleshooting.

## Conclusion

This project demonstrates the design, deployment and expansion of a multi-node private cloud infrastructure using OpenStack.

By integrating additional physical compute resources and extending the platform with storage, monitoring, database and developer services, the infrastructure evolved into a shared cloud environment for student workloads.

The project provided practical experience in cloud infrastructure engineering, distributed systems, networking, storage, automation, monitoring and platform services.
