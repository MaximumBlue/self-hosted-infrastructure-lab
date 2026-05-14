# Networking Documentation

## Overview

This environment uses a layered networking model consisting of:

* Proxmox host networking
* Ubuntu VM internal networking
* Docker container networking
* NAT and forwarding rules
* reverse proxy routing

The networking configuration was designed to expose containerized services to the local network while maintaining a flexible and reproducible lab environment.

---

## Network Topology

```text
LAN
  ↓
Proxmox Host
  ↓
Ubuntu VM
  ↓
Docker Networks
  ├── Monitoring Services
  ├── Infrastructure Services
  └── Development Services
```

---

## Core Networking Concepts Implemented

### IP Forwarding

Linux IP forwarding was enabled on the Proxmox host to allow traffic routing between the external network and internal VM/container networks.

Persistent forwarding configuration was implemented using:

```text
net.ipv4.ip_forward=1
```

---

### NAT and Port Forwarding

iptables NAT rules were configured to expose internal services externally.

Examples include:

* Grafana
* Portainer
* Nginx Proxy Manager
* Gitea

Persistent firewall behavior was configured using:

* netfilter-persistent
* iptables-persistent

---

### Reverse Proxy Routing

Nginx Proxy Manager was deployed to simplify service access and reduce dependence on direct port exposure.

Example internal routes:

* portainer.local
* gitea.local

This approach improves:

* maintainability
* service organization
* operational consistency

---

## Key Lessons Learned

### Internal vs External Networking

One major challenge involved understanding differences between:

* internal container networking
* VM networking
* externally routed access paths

This required troubleshooting:

* NAT behavior
* forwarding rules
* Docker port exposure
* reverse proxy configuration

---

### Persistence and Reboots

Another key operational lesson involved persistence across system reboots.

Critical services required:

* persistent iptables rules
* persistent IP forwarding configuration
* Docker restart policies
* Compose-based service recovery

---

## Future Improvements

Planned networking improvements include:

* reduced manual NAT management
* improved reverse proxy integration
* infrastructure health validation
* automated networking recovery
* centralized DNS management
