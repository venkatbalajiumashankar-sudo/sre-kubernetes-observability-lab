![Kubernetes](https://img.shields.io/badge/Kubernetes-K3s-blue)
![Docker](https://img.shields.io/badge/Container-Docker-blue)
![Prometheus](https://img.shields.io/badge/Monitoring-Prometheus-orange)
![Grafana](https://img.shields.io/badge/Dashboard-Grafana-yellow)
![Jenkins](https://img.shields.io/badge/CI/CD-Jenkins-red)
![Linux](https://img.shields.io/badge/OS-Ubuntu%2024.04-E95420)

# SRE Kubernetes Observability Lab

Production-style **Site Reliability Engineering lab** demonstrating Kubernetes deployment, CI/CD automation, and observability using **Prometheus and Grafana**.

## Table of Contents

- Project Overview
- Architecture
- Infrastructure
- Kubernetes Cluster
- Monitoring Stack
- CI/CD Pipeline
- Screenshots
- Incident Simulation
- Skills Demonstrated
- Author

## 🚀 Project Overview

This project simulates a **real-world Site Reliability Engineering (SRE) environment** built on Kubernetes.

The lab demonstrates how infrastructure engineers deploy applications, monitor cluster health, investigate incidents, and automate deployments using CI/CD pipelines.

### Key Components

- Kubernetes (k3s) cluster
- Containerized workloads
- Prometheus monitoring
- Grafana observability dashboards
- Jenkins CI/CD pipelines
- Incident simulation and troubleshooting

### What This Project Demonstrates

- Kubernetes cluster operations
- Observability and monitoring practices
- CI/CD automation workflows
- SRE incident investigation process

## 🛠 Tech Stack

| Technology | Purpose |
|------------|--------|
| Kubernetes (K3s) | Container orchestration |
| Docker | Containerization |
| Prometheus | Metrics collection |
| Grafana | Monitoring dashboards |
| Jenkins | CI/CD automation |
| Ubuntu Server | Infrastructure environment |
| VirtualBox | Virtualization platform |

---

# Architecture

![Architecture](architecture/architecture.png)

This environment simulates a production infrastructure stack.

Windows Laptop
↓
VirtualBox VM
↓
Ubuntu Server
↓
K3s Kubernetes Cluster
↓
Applications (nginx, demo workloads)
↓
Prometheus Monitoring
↓
Grafana Dashboards

---

# Infrastructure

Host Machine  
Windows Laptop

Virtualization  
VirtualBox

Operating System  
Ubuntu Server 24.04 LTS

Kubernetes Distribution  
K3s Kubernetes

This environment runs a full Kubernetes stack inside a virtual machine.

---

# Step 1 – VM Network Configuration

Networking inside the Ubuntu VM was verified.

Command used:

hostname -I

This shows interfaces used by:

- VirtualBox networking
- Docker bridge network
- Kubernetes pod networking

![VM Network](screenshots/01_vm_network_configuration.png)

---

# Step 2 – Kubernetes Cluster Verification

A lightweight Kubernetes cluster was deployed using **k3s**.

Cluster health verification:

kubectl get nodes

The node status shows **Ready**, confirming the Kubernetes control plane is running.

![Kubernetes Node](screenshots/02_kubernetes_cluster_nodes.png)

---

# Step 3 – Running Kubernetes Pods

All running workloads were verified across namespaces.

kubectl get pods -A

Running components include:

Monitoring Stack

- Prometheus
- Grafana
- Node Exporter
- kube-state-metrics

Applications

- nginx deployment
- demo workloads

System Components

- CoreDNS
- metrics-server
- Traefik ingress controller

![Running Pods](screenshots/03_kubernetes_all_pods_running.png)

---

# Step 4 – Kubernetes Services

Services expose applications and monitoring components.

kubectl get svc

Services include:

- Grafana service
- Prometheus service
- nginx NodePort service
- demo application services

![Kubernetes Services](screenshots/04_kubernetes_services.png)

---

# Step 5 – Docker Images

Applications were containerized using Docker before deployment.

docker images

Custom application image:

venkatbalajiumashankar/sre-ci-cd-demo

![Docker Images](screenshots/05_docker_images_local_registry.png)

---

# Step 6 – Accessing Grafana

Grafana dashboards were accessed using Kubernetes port forwarding.

kubectl port-forward svc/monitoring-grafana 3000:80

Access Grafana:

[http://localhost:3000](http://127.0.0.1:3000)


![Grafana Port Forward](screenshots/06_grafana_port_forward.png)

---

# Step 7 – Grafana Monitoring Dashboards

Grafana visualizes Prometheus metrics for the Kubernetes cluster.

Metrics monitored include:

- CPU utilization
- Memory utilization
- Pod resource consumption
- Namespace workloads
- Cluster health metrics

![Grafana Dashboard](screenshots/07_grafana_kubernetes_dashboard.png)

---

# Step 8 – Jenkins CI/CD Pipelines

Jenkins automates container build and deployment.

Configured pipelines:

Docker Build Pipeline  
Builds container images.

Kubernetes Deployment Pipeline  
Deploys applications into the cluster.

![Jenkins Pipeline](screenshots/08_jenkins_pipeline_dashboard.png)

---

# Step 9 – Successful CI/CD Deployment

The Jenkins pipeline builds the Docker image and deploys it automatically.

Pipeline output confirms success.

Finished: SUCCESS

![Pipeline Success](screenshots/09_jenkins_pipeline_success.png)

---

# Step 10 – Kubernetes Deployment Verification

Final verification of running deployments.

kubectl get deployments


Running deployments include:

- nginx
- web-demo
- sre-demo
- monitoring components

![Deployments](screenshots/10_kubernetes_deployments.png)

---

# Observability Stack

The monitoring system consists of:

Prometheus  
Collects metrics from Kubernetes nodes and pods.

Grafana  
Visualizes cluster metrics.

Alertmanager  
Manages alert notifications.

Node Exporter  
Provides node-level system metrics.

This stack enables full **cluster observability and monitoring**.

---

# Production Incident Simulation

This lab includes simulated production incidents.

CPU Spike Simulation

A stress workload was deployed to generate high CPU usage.

Incident investigation workflow:

1. Deploy stress workload
2. Observe CPU spike in Grafana
3. Identify affected pods
4. Analyze metrics
5. Adjust deployment resources

This demonstrates how SRE teams detect and investigate system issues.

---

## Reliability Engineering Design

This project also demonstrates core **Site Reliability Engineering (SRE) reliability practices** inspired by Google's SRE methodology.

### Service Level Indicators (SLI)

The following indicators are used to evaluate system health:

- API / application availability
- Pod restart rate
- CPU utilization
- Memory utilization
- Request latency
- Deployment success rate

These metrics are collected through **Prometheus exporters** and visualized in **Grafana dashboards**.

---

### Service Level Objectives (SLO)

Example reliability targets for the demo application:

| Metric | Target |
|------|------|
| Application Availability | 99.9% |
| Pod Restart Rate | < 1 per hour |
| Deployment Success Rate | 100% |
| CPU Utilization | < 80% sustained |

If the system violates these thresholds, alerts or investigation workflows should be triggered.

---

### Error Budget Concept

Using a 99.9% availability target:


This allows teams to balance **reliability vs feature velocity**.

If error budget is exhausted, new deployments should pause until reliability stabilizes.

---

### Monitoring Strategy

The monitoring stack follows a layered observability model:

| Layer | Tool |
|-----|-----|
| Infrastructure Metrics | Node Exporter |
| Kubernetes Metrics | kube-state-metrics |
| Application Metrics | Prometheus |
| Visualization | Grafana |
| Alerting | Alertmanager |

This layered approach ensures visibility across the full stack.

---

### Incident Response Workflow

A simulated production incident was performed as part of this lab.

Example scenario: **CPU spike in application pods**

Investigation workflow:

1. CPU spike detected in Grafana dashboard
2. Prometheus metrics confirmed abnormal resource consumption
3. `kubectl top pods` used to identify affected workloads
4. Kubernetes events and pod logs inspected
5. Mitigation applied through scaling or workload adjustment

This demonstrates how SRE teams diagnose and resolve production issues.

---

### Lessons Learned

Key SRE practices demonstrated in this project:

- Observability-driven troubleshooting
- Infrastructure monitoring with Prometheus
- CI/CD automation for deployments
- Kubernetes workload management
- Incident investigation using metrics and logs

## Distributed Systems Failure Scenarios

Modern distributed systems must be designed to tolerate failures.  
This lab includes several simulated failure scenarios to demonstrate how Kubernetes and observability tools help diagnose and recover from incidents.

### Scenario 1 — Pod Crash

A pod failure was simulated to observe Kubernetes self-healing behavior.

Expected system behavior:

- Kubernetes automatically restarts the failed pod
- ReplicaSet ensures the desired number of replicas are maintained
- Pod restart events are visible via `kubectl describe pod`

Investigation steps:

1. Detect pod failure using `kubectl get pods`
2. Inspect events using `kubectl describe pod`
3. Verify restart behavior through Grafana dashboards

---

### Scenario 2 — CPU Spike

A stress workload was deployed to generate abnormal CPU usage.

Investigation workflow:

1. Grafana dashboard detects CPU spike
2. Prometheus metrics confirm resource saturation
3. `kubectl top pods` identifies the high-CPU container
4. Horizontal scaling or resource limits mitigate the issue

This demonstrates how observability tools support **performance troubleshooting**.

---

### Scenario 3 — Deployment Failure

A misconfigured deployment can lead to application downtime.

Kubernetes protects against this using:

- rolling updates
- deployment revision history
- automatic rollback

Engineers can recover using:


---

### Scenario 4 — Node Failure

If a Kubernetes node fails:

- workloads are automatically rescheduled on healthy nodes
- cluster state remains consistent through the control plane

This self-healing behavior is a core property of Kubernetes reliability.

---

### Key Distributed System Principles Demonstrated

This lab demonstrates several distributed system concepts:

- Fault tolerance
- Self-healing infrastructure
- Observability-driven debugging
- Horizontal scalability
- Automated deployment pipelines


# Skills Demonstrated

Kubernetes cluster deployment  
Containerized application management  
CI/CD automation with Jenkins  
Prometheus monitoring setup  
Grafana dashboard visualization  
Infrastructure observability  
Incident investigation workflows  
Kubernetes autoscaling

---

# Author

Venkat Balaji Umashankar  
MS Information Technology – Cybersecurity  
Arizona State University

Focus Areas

Site Reliability Engineering  
Cloud Infrastructure  
Kubernetes Operations  
Observability Systems











