# Branch Office Network

## Overview

This home lab simulates a small enterprise network consisting of a Headquarters (HQ) and a Branch Office connected through a Wide Area Network (WAN). The project demonstrates how routers connect different networks, how a centralized DHCP server assigns IP addresses across multiple sites, and how DHCP Relay (`ip helper-address`) enables remote clients to receive IP addresses.

---

## Objectives

- Configure routers and switches using Cisco IOS CLI
- Configure static routing between two offices
- Configure a centralized DHCP server
- Implement DHCP Relay using `ip helper-address`
- Verify end-to-end network connectivity
- Practice network troubleshooting

---
## Network Topology
<img width="1602" height="625" alt="image" src="https://github.com/user-attachments/assets/cf6c98a2-a100-4f6d-a07c-02334c11f937" />



---

## IP Addressing

| Device | Interface | IP Address |
|---------|-----------|------------|
| Router R1 | G0/0 | 192.168.10.1/24 |
| Router R1 | G0/1 | 10.10.10.1/30 |
| Router R2 | G0/0 | 192.168.20.1/24 |
| Router R2 | G0/1 | 10.10.10.2/30 |
| DHCP Server | Fa0 | 192.168.10.2/24 |

---

## Technologies Used

- Cisco Packet Tracer
- Cisco IOS CLI
- Static Routing
- DHCP
- DHCP Relay (`ip helper-address`)
- WAN
- LAN

---

## Configuration Summary

### Router R1
- Configured LAN and WAN interfaces
- Added a static route to the Branch Office network

### Router R2
- Configured LAN and WAN interfaces
- Configured DHCP Relay using `ip helper-address`
- Added a static route to the Headquarters network

### DHCP Server
- Created separate DHCP pools for Headquarters and Branch Office
- Assigned default gateways and DNS server

---

## Verification

The following tests were successfully completed:

- Router-to-router connectivity verified using `ping`
- Headquarters PCs received IP addresses automatically
- Branch Office PCs received IP addresses through DHCP Relay
- End-to-end communication between both offices verified
- Routing table verified using `show ip route`

---

## Troubleshooting

During this lab, I encountered and resolved the following issues:

- Incorrect WAN IP address configured on Router R2
- DHCP requests not reaching the Branch Office due to incorrect configuration
- Verified routing using `show ip route`
- Verified interfaces using `show ip interface brief`

---

## Skills Demonstrated

- IP Addressing
- Cisco Router Configuration
- Cisco Switch Configuration
- Static Routing
- DHCP Configuration
- DHCP Relay
- WAN Configuration
- Network Troubleshooting
- Connectivity Verification

---

## Lessons Learned

This lab helped me understand how routers connect different networks through a WAN, how centralized DHCP works across multiple locations, and why DHCP Relay is required when the DHCP server is located on a different subnet. I also gained experience troubleshooting routing and addressing issues using Cisco IOS verification commands.
