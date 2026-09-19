# Enterprise Network Infrastructure Lab

## Overview

This project simulates a multi-site enterprise network consisting of a Headquarters (HQ) site and a Branch office.

The lab focuses on practical enterprise networking concepts including VLAN segmentation, inter-VLAN routing, centralized DHCP services, dynamic routing, ACL-based access control, gateway redundancy, and WAN connectivity between sites.

The environment is implemented using Cisco Packet Tracer.

---

## Objectives

- Design a multi-site enterprise network
- Segment users and services using VLANs
- Implement inter-VLAN routing
- Provide centralized DHCP services using DHCP Relay
- Configure dynamic routing using OSPF
- Apply ACL-based network segmentation
- Implement gateway redundancy using HSRP
- Validate end-to-end connectivity between HQ and Branch

---

## Technologies

- Cisco Packet Tracer
- VLAN
- IEEE 802.1Q Trunking
- Inter-VLAN Routing
- DHCP Relay
- OSPF
- Extended ACL
- HSRP
- Rapid-PVST
- EtherChannel / LACP

---

## Network Topology

![Enterprise Network Topology](https://github.com/Anieast/enterprise-network-lab/blob/main/topology/Network%20topo.png)

The network consists of:

- Dual Layer 3 Core switches at HQ
- Redundant Access switches
- HQ Router
- ISP Transit Router
- Branch Router
- Branch LAN
- Centralized Server VLAN
- Multiple user VLANs

---

## Network Design

![Detailed IP planning is available in the repository.](https://github.com/Anieast/enterprise-network-lab/blob/main/docs/VLAN-planning.md)

---

## Implementation

### VLAN and Inter-VLAN Routing

VLANs are used to separate different user and service groups.

Layer 3 SVIs on the HQ Core switches provide inter-VLAN routing.

802.1Q trunk links are used between the Core and Access layers.

---

### Centralized DHCP

DHCP services are centralized in the Server VLAN.

DHCP Relay is configured on Layer 3 gateway interfaces so that clients from different VLANs can obtain IP addresses from the centralized DHCP server.

---

### Dynamic Routing

OSPF is used to exchange routes between:

- HQ Core Layer
- HQ Router
- ISP Transit Router
- Branch Router

This provides end-to-end routing between HQ and Branch networks.

---

### Network Segmentation with ACL

Extended ACLs are used to control communication between network segments.

Examples:

```text
STAFF → DNS Server             ALLOW
STAFF → Web Server HTTP/HTTPS  ALLOW
STAFF → Other Server traffic   DENY

GUEST → Internal networks      DENY