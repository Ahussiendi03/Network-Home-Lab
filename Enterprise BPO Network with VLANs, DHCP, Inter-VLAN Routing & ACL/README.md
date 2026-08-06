## Overview

This home lab simulates a small enterprise Business Process Outsourcing (BPO) network using Cisco Packet Tracer. The project demonstrates core networking concepts used in enterprise environments, including VLAN segmentation, Router-on-a-Stick, DHCP configuration, Inter-VLAN Routing, Static IP Addressing, and Access Control Lists (ACLs).

The objective of this lab is to build a secure and scalable network similar to what is commonly deployed in corporate offices and BPO companies.

##Network Topology
<img width="1407" height="687" alt="image" src="https://github.com/user-attachments/assets/af506633-bf3f-49df-8610-90eb9e55faff" />

---

## Department VLANs

| VLAN | Department | Network |
|------|------------|----------------|
|10|Human Resources|192.168.10.0/24|
|20|Customer Support|192.168.20.0/24|
|30|IT Department|192.168.30.0/24|
|40|Server Room|192.168.40.0/24|

---

## IP Addressing Scheme

### Default Gateways

| VLAN | Gateway |
|------|-------------|
|10|192.168.10.1|
|20|192.168.20.1|
|30|192.168.30.1|
|40|192.168.40.1|

---

### Static IP Addresses

| Device | IP Address |
|----------|---------------|
|File Server|192.168.40.2|
|Network Printer|192.168.40.3|
|Wireless Access Point|192.168.40.4|

---

## Technologies Used

- Cisco Packet Tracer
- Cisco 2911 Router
- Cisco 2960 Switch
- VLAN
- IEEE 802.1Q Trunking
- Router-on-a-Stick
- DHCP
- Static IP Addressing
- Access Control Lists (ACL)
- Inter-VLAN Routing

---

## Features Implemented

- VLAN Segmentation
- Access Port Configuration
- Trunk Port Configuration
- Router-on-a-Stick
- DHCP Configuration
- Static IP Address Assignment
- Extended ACL
- Enterprise Network Documentation
- Network Verification
- Network Troubleshooting

---

## VLAN Configuration

| Department | VLAN | Ports |
|------------|------|---------|
|HR|10|Fa0/1–Fa0/2|
|Customer Support|20|Fa0/3–Fa0/4|
|IT|30|Fa0/5–Fa0/6|
|Server Room|40|Fa0/7–Fa0/9|

---

## DHCP Configuration

DHCP is configured on the Cisco 2911 Router.

Each VLAN has its own DHCP pool.

Infrastructure devices use Static IP addresses.

Excluded addresses reserve IPs for gateways and future infrastructure devices.

Example:

192.168.10.1–192.168.10.10

192.168.20.1–192.168.20.10

192.168.30.1–192.168.30.10

---

## Security Implementation

An Extended Access Control List (ACL) was implemented to protect sensitive company resources.

### Security Policy

| Department | File Server |
|------------|------------|
|HR|Allowed|
|IT|Allowed|
|Customer Support|Denied|

Customer Support users cannot access the File Server while maintaining access to other permitted network resources.

---

## Verification Commands

### Switch

```bash
show vlan brief

show interfaces trunk

show interfaces status

show running-config
```

### Router

```bash
show ip interface brief

show ip route

show ip dhcp binding

show ip dhcp pool

show access-lists

show running-config
```

---

## Connectivity Testing

### Successful Tests

- HR → Server
- HR → IT
- HR → Customer Support
- IT → Server
- IT → Printer
- Customer Support → Printer
- Customer Support → Wireless AP

### Blocked by ACL

Customer Support → File Server

Result:

```
Request timed out
```

---

## Troubleshooting Performed

- DHCP lease verification
- VLAN verification
- Trunk verification
- Router subinterface verification
- ACL verification
- Default gateway verification
- Inter-VLAN Routing verification

---

## Skills Demonstrated

- VLAN Configuration
- Router-on-a-Stick
- DHCP Configuration
- Static IP Addressing
- Inter-VLAN Routing
- Extended ACL Implementation
- Enterprise Network Security
- Cisco CLI
- Network Troubleshooting
- IT Support Documentation

