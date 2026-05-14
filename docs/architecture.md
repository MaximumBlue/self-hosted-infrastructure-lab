# Architecture Documentation

## Overview

This document describes the infrastructure architecture, virtualization layout, networking model, and container platform organization used within the platform engineering lab environment.

---

## Physical Infrastructure

Current environment:

* Proxmox VE host
* Ubuntu Server virtual machine
* Docker-based service platform

---

## Virtualization Layer

Proxmox is used as the primary virtualization platform responsible for:

* VM lifecycle management
* network bridging
* infrastructure isolation
* resource allocation

---

## Container Platform

Docker and Docker Compose are used to manage:

* observability services
* infrastructure tooling
* development platform services
* operational workflows

Services are organized into logical Compose stacks for maintainability and reproducibility.

---

## Future Improvements

Planned architecture improvements:

* infrastructure rebuild automation
* centralized logging
* GitOps-style deployment workflows
* automated backup systems
* infrastructure health validation

---

# Non-Standard Infrastructure Design

## Wireless Proxmox Deployment

One unique challenge in this environment involved operating Proxmox using a wireless network uplink instead of traditional Ethernet connectivity.

Because Proxmox is typically designed for wired infrastructure deployments, additional Linux networking configuration was required to establish stable wireless connectivity and VM network routing.

This included:

* manual `wpa_supplicant` configuration
* DHCP management for wireless interfaces
* Linux IP forwarding
* NAT-based VM routing
* persistent forwarding configuration

While unconventional, this design provided:

* deployment flexibility
* lower hardware requirements
* practical Linux networking experience
* operational troubleshooting opportunities

The implementation significantly improved understanding of:

* Linux networking internals
* virtualization networking
* packet forwarding behavior
* NAT architecture
* infrastructure persistence handling
