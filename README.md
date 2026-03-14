# SRE Kubernetes Observability Lab

## Architecture

![Architecture](architecture/architecture.png)

This project simulates a production SRE environment with Kubernetes,
Prometheus monitoring, Grafana dashboards, and incident simulations.

## Infrastructure

Host: Windows Laptop  
Virtualization: VirtualBox  
OS: Ubuntu Server  

## Kubernetes

Lightweight cluster deployed using k3s.

Verified using:

kubectl get nodes
kubectl get pods -A

## Applications

Deployed nginx container.

kubectl create deployment nginx --image=nginx

Exposed service using NodePort.

## Observability Stack

Installed kube-prometheus-stack using Helm.

Components:

Prometheus
Grafana
Alertmanager
Node Exporter

## Incident Simulations

CPU Spike Simulation  
Pod Crash Investigation  
Memory Leak Simulation  

## Autoscaling

Horizontal Pod Autoscaler based on CPU usage.

## Architecture

Ubuntu VM
↓
K3s Kubernetes
↓
Applications
↓
Prometheus
↓
Grafana


