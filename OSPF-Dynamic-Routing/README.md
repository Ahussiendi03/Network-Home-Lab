# OSPF Dynamic Routing

## Objective

Build an enterprise network using three Cisco 2911 routers connected with OSPF Area 0.

## Scenario

The company consists of:

- Headquarters
- Branch Office A
- Branch Office B

Each office contains:

- Cisco 2911 Router
- Cisco 2960 Switch
- Two PCs
- One Network Printer
- One Wireless Access Point

Infrastructure devices use static IP addresses.

Client devices obtain IP addresses automatically using DHCP.

---

## IP Addressing

### Headquarters

| Device | IP |
|---------|----|
| Router | 192.168.10.1 |
| Printer | 192.168.10.2 |
| Wireless AP | 192.168.10.3 |
| PC1 | DHCP |
| PC2 | DHCP |

### Branch A

| Device | IP |
|---------|----|
| Router | 192.168.20.1 |
| Printer | 192.168.20.2 |
| Wireless AP | 192.168.20.3 |
| PC3 | DHCP |
| PC4 | DHCP |

### Branch B

| Device | IP |
|---------|----|
| Router | 192.168.30.1 |
| Printer | 192.168.30.2 |
| Wireless AP | 192.168.30.3 |
| PC5 | DHCP |
| PC6 | DHCP |

---

## Routing Protocol

- OSPF Process ID: 1
- Area: 0

---

## DHCP Configuration

Each router provides DHCP services for its local LAN.

Infrastructure devices use static IP addresses and are excluded from the DHCP pool.

Example:


ip dhcp excluded-address 192.168.10.1 192.168.10.10


---

## Verification Commands


show ip interface brief
show ip route
show ip ospf neighbor
show ip protocols
show ip dhcp binding


---

## Skills Learned

- OSPF Dynamic Routing
- Enterprise IP Addressing
- DHCP Configuration
- Static IP Assignment
- Route Advertisement
- Network Troubleshooting
- Cisco IOS CLI
