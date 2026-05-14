# Deployment & Operations

## Overview

Infrastructure services are deployed using Docker Compose-based stack management.

The environment is designed around:

* reproducible deployments
* operational simplicity
* infrastructure version control
* stack-based service organization

---

## Compose Stack Layout

```text
~/docker/
├── monitoring/
├── dev-platform/
└── future-services/
```

---

## Current Stacks

### Monitoring Stack

Current monitoring services:

* Prometheus
* Grafana
* cAdvisor
* node-exporter

---

### Development Platform Stack

Current development services:

* Gitea

---

### Infrastructure Services

Additional infrastructure services:

* Portainer
* Nginx Proxy Manager

---

## Startup Workflow

Typical startup sequence:

1. Boot Proxmox host
2. Verify networking connectivity
3. Start Ubuntu VM
4. Start infrastructure stacks

Startup automation script:

```bash
~/start-lab.sh
```

---

## Infrastructure Version Control

Infrastructure configurations are version-controlled using:

* Git
* GitHub
* self-hosted Gitea

Tracked configuration includes:

* Docker Compose files
* Prometheus configuration
* operational documentation
* deployment structure

---

## Operational Goals

The deployment model focuses on:

* reproducibility
* maintainability
* simplified recovery
* infrastructure organization
* operational consistency

---

## Future Improvements

Planned deployment improvements:

* automated rebuild workflows
* GitOps-style deployment pipelines
* infrastructure validation scripts
* backup automation
* health monitoring workflows
