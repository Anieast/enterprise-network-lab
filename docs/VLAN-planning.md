# VLAN & IP Addressing Plan

## Headquarters (HQ)

| VLAN | Name | Network | CORE1 SVI | CORE2 SVI | HSRP VIP |
|---|---|---|---|---|---|
| 110 | IT | 10.10.10.0/24 | 10.10.10.1 | 10.10.10.2 | 10.10.10.254 |
| 120 | STAFF | 10.10.20.0/24 | 10.10.20.1 | 10.10.20.2 | 10.10.20.254 |
| 130 | SERVER | 10.10.30.0/24 | 10.10.30.1 | 10.10.30.2 | 10.10.30.254 |
| 140 | GUEST | 10.10.40.0/24 | 10.10.40.1 | 10.10.40.2 | 10.10.40.254 |

---

## Branch

| VLAN | Name | Network |
|---|---|---|
| 210 | STAFF | 10.20.10.0/24 |
| 220 | GUEST | 10.20.20.0/24 |

---

## WAN / Transit Networks

### HQ Router ↔ ISP

| Link | Network |
|---|---|
| HQ-R1 ↔ ISP | 10.255.0.0/30 |

### HQ Router ↔ HQ Core

| Link | Network |
|---|---|
| HQ-R1 ↔ HQ-CORE1 | 10.255.10.0/30 |
| HQ-R1 ↔ HQ-CORE2 | 10.255.10.4/30 |

### ISP ↔ Branch Router

| Link | Network |
|---|---|
| ISP ↔ Branch-R1 | 10.255.0.4/30 |

---

## Branch Router ↔ Branch LAN

Branch LAN connectivity is provided through the following VLANs:

| VLAN | Network |
|---|---|
| 210 | 10.20.10.0/24 |
| 220 | 10.20.20.0/24 |

---

## Server Addressing

| Server | IP Address | Network |
|---|---|---|
| DHCP / DNS Server | 10.10.30.10 | 10.10.30.0/24 |
| Web Server | 10.10.30.20 | 10.10.30.0/24 |

---

## Default Gateway Design

HQ VLANs use HSRP virtual IP addresses as their default gateways.

| VLAN | Default Gateway |
|---|---|
| 110 | 10.10.10.254 |
| 120 | 10.10.20.254 |
| 130 | 10.10.30.254 |
| 140 | 10.10.40.254 |

CORE1 is the preferred HSRP Active gateway, while CORE2 operates as Standby.

---

## Addressing Summary

```text
HQ
├── VLAN 110 IT       10.10.10.0/24
├── VLAN 120 STAFF    10.10.20.0/24
├── VLAN 130 SERVER   10.10.30.0/24
└── VLAN 140 GUEST    10.10.40.0/24

Branch
├── VLAN 210 STAFF    10.20.10.0/24
└── VLAN 220 GUEST    10.20.20.0/24

WAN
├── HQ-R1 ↔ ISP       10.255.0.0/30
├── ISP ↔ Branch-R1   10.255.0.4/30
├── HQ-R1 ↔ CORE1     10.255.10.0/30
└── HQ-R1 ↔ CORE2     10.255.10.4/30

Servers
├── DHCP/DNS          10.10.30.10
└── Web Server        10.10.30.20