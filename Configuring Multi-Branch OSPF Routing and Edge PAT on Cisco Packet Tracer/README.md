# Cisco Multi-Site Enterprise Network Lab

## Overview

This home lab simulates a multi-site enterprise network infrastructure consisting of a Corporate Headquarters (HQ) and two remote Branch Offices connected to an Internet Service Provider (ISP). The project demonstrates 802.1Q inter-VLAN routing, dynamic OSPF WAN routing across multiple locations, default route injection, and centralized Internet breakout using Port Address Translation (PAT) at the HQ edge.

---

## Objectives

- Configure 802.1Q Router-on-a-Stick (ROAS) inter-VLAN routing on Cisco IOS CLI
- Implement single-area OSPF (Area 0) dynamic routing across serial WAN links
- Configure dynamic default route propagation (`default-information originate`) from HQ
- Implement Port Address Translation (PAT / NAT Overload) using standard ACL wildcard summarization
- Verify cross-site inter-VLAN, inter-branch, and external ISP connectivity
- Perform Root Cause Analysis (RCA) and state table verification for NAT and OSPF

---

## Network Topology & Interface Plan

<img width="1877" height="657" alt="image" src="https://github.com/user-attachments/assets/e84382cc-4473-4259-89da-cf8768b9561b" />

| Device | Interface | IP Address / Subnet | Function / Role |
| :--- | :--- | :--- | :--- |
| **HQ-R1** | `Gig0/1.10` | `192.168.10.1/24` | VLAN 10 Gateway (HR) |
| **HQ-R1** | `Gig0/1.20` | `192.168.20.1/24` | VLAN 20 Gateway (Customer Support) |
| **HQ-R1** | `Gig0/1.30` | `192.168.30.1/24` | VLAN 30 Gateway (IT) |
| **HQ-R1** | `Gig0/1.40` | `192.168.40.1/24` | VLAN 40 Gateway (Server) |
| **HQ-R1** | `Serial0/0/1` | `10.10.10.1/30` | Point-to-Point WAN to BR1-R1 (`2.2.2.2`) |
| **HQ-R1** | `Serial0/0/0` | `10.10.20.1/30` | Point-to-Point WAN to BR2-R1 (`3.3.3.3`) |
| **HQ-R1** | `Gig0/0` | `10.10.50.2/30` | Public WAN Handoff (`ip nat outside`) |
| **BR1-R1** | `Serial0/0/1` | `10.10.10.2/30` | Branch 1 Serial WAN Gateway |
| **BR1-R1** | `Gig0/0`–`2` | `192.168.110.0/24`–`130.0/24` | Branch 1 Internal LAN Subnets |
| **BR2-R1** | `Serial0/0/0` | `10.10.20.2/30` | Branch 2 Serial WAN Gateway |
| **BR2-R1** | `Gig0/0`–`2` | `192.168.210.0/24`–`230.0/24` | Branch 2 Internal LAN Subnets |
| **ISP** | `Gig0/0` | `10.10.50.1/30` | Next-Hop ISP Gateway |
| **ISP Host** | Loopback / NIC | `203.0.113.1/24` | External Internet Target |

---

## Technologies Used

- Cisco Packet Tracer
- Cisco IOS CLI
- 802.1Q Trunking & Subinterfaces (ROAS)
- Open Shortest Path First (OSPF Area 0)
- Port Address Translation (PAT / NAT Overload)
- Standard Access Control Lists (ACLs) & Wildcard Summarization
- Serial Point-to-Point WAN Links

---

## Configuration Summary

### Headquarter Router (`HQ-R1`)
- Configured 802.1Q subinterfaces (`Gig0/1.10` through `Gig0/1.40`) and designated them as `ip nat inside`
- Configured point-to-point serial WAN interfaces (`Serial0/0/1` and `Serial0/0/0`)
- Configured OSPF Area 0 and dynamic default route injection using `default-information originate`
- Configured dynamic PAT on `Gig0/0` (`ip nat outside`) using summarized wildcard matching (`192.168.0.0 0.0.255.255`)

### Branch Routers (`BR1-R1` & `BR2-R1`)
- Configured local LAN subnets and WAN serial interfaces
- Configured OSPF Area 0 to dynamically publish internal subnets and receive the HQ default route (`0.0.0.0/0`)

---

## Troubleshooting & RCA

During testing, I encountered and resolved the following issue:

- **Issue:** Branch Office PCs (`192.168.110.0/24` through `230.0/24`) could ping HQ LANs via OSPF, but pings to the public ISP server (`203.0.113.1`) timed out.
- **Diagnosis:** Verified that `BR1-R1` and `BR2-R1` had active `O*E2` default routes in their routing tables. Checked `show ip nat translations` on `HQ-R1` during active pings, which showed zero translations being generated.
- **Root Cause:** `NAT_ACL` on `HQ-R1` initially permitted only HQ-local subnets (`192.168.10.0/24`–`40.0/24`). Traffic from branch subnets reached `HQ-R1`, but failed to match `NAT_ACL`, causing `HQ-R1` to route the packets out `Gig0/0` untranslated with private RFC 1918 addresses, which were dropped at the ISP boundary.
- **Resolution:** Replaced individual `/24` entries in `NAT_ACL` with wildcard mask summarization (`permit 192.168.0.0 0.0.255.255`), allowing all current and future branch subnets to translate to public IP `10.10.50.2`.

---

## Verification

The following tests were successfully completed:

- **OSPF Adjacencies:** Verified `FULL/-` state across WAN links using `show ip ospf neighbor`.
- **Routing Table Integrity:** Verified dynamic propagation of all branch subnets and default routes using `show ip route ospf`.
- **NAT State Table:** Confirmed active dynamic IP/Port translations during host ping/HTTP sessions using `show ip nat translations`.
- **End-to-End Reachability:** Successfully pinged external target `203.0.113.1` from PCs across HQ and both Branch offices.

---

## Skills Demonstrated

- Router-on-a-Stick (ROAS) Configuration
- Dynamic OSPF Area 0 Deployment
- Default Route Injection
- Network Address Translation (PAT / Overload)
- Access Control List (ACL) Wildcard Summarization
- Serial WAN Connectivity
- Root Cause Analysis & Packet Flow Inspection
