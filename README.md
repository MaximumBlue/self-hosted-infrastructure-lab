# Self-Hosted Platform Engineering Lab

## Overview

A self-hosted infrastructure and observability platform built using Proxmox, Docker Compose, Linux networking, and containerized services.

This project focuses on:

* infrastructure automation
* service orchestration
* observability and monitoring
* reverse proxy routing
* Git-based infrastructure management
* operational troubleshooting
* reproducible deployments

The goal of this environment is to develop practical platform engineering and infrastructure operations experience through building and maintaining a real-world virtualized lab environment.

---

## Technologies Used

### Virtualization

* Proxmox VE
* Ubuntu Server VM

### Containerization

* Docker
* Docker Compose

### Observability Stack

* Prometheus
* Grafana
* cAdvisor
* node-exporter

### Infrastructure Services

* Gitea
* Portainer
* Nginx Proxy Manager

### Networking

* Linux NAT
* iptables
* netfilter-persistent
* reverse proxy routing

### Version Control

* Git
* GitHub
* self-hosted Gitea

---

## Architecture Overview

```text
Internet/LAN
      ↓
Proxmox Host
      ↓
Ubuntu VM
      ↓
Docker Engine
 ├── Monitoring Stack
 │    ├── Prometheus
 │    ├── Grafana
 │    ├── cAdvisor
 │    └── node-exporter
 │
 ├── Dev Platform Stack
 │    └── Gitea
 │
 └── Infrastructure Services
      ├── Portainer
      └── Nginx Proxy Manager
```

---

## Current Features

### Infrastructure

* Virtualized environment using Proxmox
* Ubuntu Server VM hosting Docker workloads
* Persistent NAT and forwarding configuration

### Monitoring & Observability

* Metrics collection with Prometheus
* Infrastructure visualization with Grafana
* Container metrics via cAdvisor
* Host metrics via node-exporter

### Platform Services

* Self-hosted Git service using Gitea
* Container management via Portainer
* Reverse proxy management using Nginx Proxy Manager

### Operations

* Git version-controlled infrastructure
* Docker Compose stack management
* Persistent firewall/network configuration
* Startup automation scripting

---

## Project Goals

This lab environment was designed to:

* simulate real platform engineering workflows
* improve Linux infrastructure administration skills
* develop operational troubleshooting experience
* practice observability and monitoring concepts
* build reproducible infrastructure workflows
* strengthen networking and systems knowledge

---

## Roadmap

### Phase 1 — Core Infrastructure

* [x] Proxmox deployment
* [x] Ubuntu VM setup
* [x] Docker installation
* [x] Monitoring stack deployment
* [x] Gitea deployment
* [x] Reverse proxy deployment

### Phase 2 — Operational Maturity

* [ ] Startup automation
* [ ] Infrastructure rebuild testing
* [ ] Backup workflows
* [ ] Health checks
* [ ] Centralized logging

### Phase 3 — Platform Engineering Expansion

* [ ] GitOps-style workflows
* [ ] CI/CD integration
* [ ] Additional infrastructure services
* [ ] Secret management
* [ ] Automated deployment pipelines
