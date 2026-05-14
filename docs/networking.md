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

---

# Implementation Notes

## Wireless Networking Initialization

Wireless connectivity on the Proxmox host was established using manual `wpa_supplicant` configuration and DHCP initialization.

Because Proxmox is primarily designed for wired infrastructure environments, additional Linux networking configuration was required to establish stable wireless connectivity for virtualization workloads.

Example operational workflow:

```bash
wpa_supplicant -B -i wlo1 -c /etc/wpa_supplicant/wpa_supplicant.conf
dhclient wlo1
```

This initializes:

* wireless authentication
* DHCP address assignment
* external network connectivity

---

## Example `wpa_supplicant` Configuration

Example wireless configuration used for Proxmox host connectivity:

```text
ctrl_interface=/run/wpa_supplicant
update_config=1
country=US

network={
    ssid="YOUR_WIFI_NAME"
    psk="YOUR_WIFI_PASSWORD"
}
```

This configuration was required to manually authenticate the Proxmox host against the wireless LAN before virtualization networking and NAT forwarding could function correctly.

---

## Linux IP Forwarding

IP forwarding was required to allow communication between:

* external LAN interfaces
* internal VM/container networks

Example runtime configuration:

```bash
echo 1 > /proc/sys/net/ipv4/ip_forward
```

Persistent configuration:

```text
net.ipv4.ip_forward=1
```

This enabled packet forwarding between the Proxmox wireless uplink and internally routed VM/container networks.

---

## NAT Forwarding Rules

iptables NAT rules were used to expose internal services externally.

Example forwarding approach:

```bash
iptables -t nat -A PREROUTING ...
iptables -t nat -A POSTROUTING ...
```

Persistent rule storage was implemented using:

```bash
netfilter-persistent save
```

This allowed externally reachable access to internally hosted services such as:

* Grafana
* Portainer
* Gitea
* Nginx Proxy Manager

---

## Operational Challenges

Major troubleshooting areas included:

* NAT routing behavior
* internal vs external access paths
* reverse proxy routing
* Docker port exposure
* persistence after reboot
* wireless interface initialization
* forwarding rule persistence
* service accessibility across layered virtualized networking

## Routing Summary

Traffic flow in this environment follows a layered model:

Client → Proxmox Host (wireless uplink) → NAT forwarding → Ubuntu VM → Docker networks → containerized services

Reverse proxy routing (Nginx Proxy Manager) is used to abstract direct port access and provide service-level routing for internal applications.

## Why NAT Was Required

Due to the use of a wireless uplink and virtualized network isolation within Proxmox, NAT was required to allow communication between the external LAN and internal VM/container networks.

This approach enabled service exposure without requiring bridged Ethernet networking.
