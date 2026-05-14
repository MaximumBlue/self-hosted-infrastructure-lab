# Observability Stack

## Overview

The observability stack was designed to provide visibility into:

* host system performance
* Docker container metrics
* infrastructure health
* operational behavior

The stack currently consists of:

* Prometheus
* Grafana
* cAdvisor
* node-exporter

---

## Components

### Prometheus

Prometheus is responsible for:

* metrics collection
* scrape target management
* time-series data storage

Current scrape targets include:

* node-exporter
* cAdvisor

---

### Grafana

Grafana provides:

* infrastructure dashboards
* metrics visualization
* operational monitoring

Dashboards currently monitor:

* CPU usage
* memory usage
* Docker container metrics
* network activity
* filesystem utilization

---

### cAdvisor

cAdvisor provides visibility into:

* Docker container resource usage
* container CPU utilization
* memory consumption
* container lifecycle metrics

This improves operational awareness for containerized workloads.

---

### node-exporter

node-exporter exposes Linux host metrics including:

* CPU utilization
* memory usage
* disk activity
* network statistics
* filesystem metrics

This provides infrastructure-level visibility for the Ubuntu VM.

---

## Operational Goals

The observability stack was implemented to:

* improve troubleshooting capability
* increase infrastructure visibility
* support operational awareness
* monitor containerized services
* develop practical monitoring experience

---

## Key Lessons Learned

Major concepts learned during deployment included:

* Prometheus scrape configuration
* YAML troubleshooting
* container restart debugging
* dashboard data source configuration
* infrastructure metrics collection

---

## Future Improvements

Planned observability improvements include:

* alerting workflows
* centralized logging
* uptime monitoring
* infrastructure health dashboards
* service dependency visualization
