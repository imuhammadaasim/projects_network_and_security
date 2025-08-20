# Accounts & Delivery Department Network Design – Cisco Packet Tracer

## 📌 Project Overview
This project demonstrates the design and implementation of a small office network in **Cisco Packet Tracer** connecting two departments:  

- **Accounts Department**  
- **Delivery Department**  

The network is built using subnetting, switches, and a router to ensure both departments can communicate with each other while remaining in separate subnets. The project highlights key networking skills such as subnetting, IP addressing, and router configuration.

---

## 🎯 Objectives
- Create a network with at least 2 PCs in each department.  
- Use an appropriate number of switches and a router for inter-department communication.  
- Subnet the given network `192.168.40.0/24` into two subnets.  
- Assign IP addresses, subnet masks, and gateways to all devices.  
- Connect devices using the correct cables.  
- Verify connectivity by successfully pinging between Accounts and Delivery PCs.  

---

## 🔢 Subnetting Design
The base network is **192.168.40.0/24**. We need **2 subnets**, so we borrow **1 bit**:


- **New Subnet Mask:** `255.255.255.128 (/25)`  

### Subnet Allocation
**Subnet 1 – Accounts Department**
- Network Address: 192.168.40.0  
- Subnet Mask: 255.255.255.128  
- Valid Hosts: 192.168.40.1 – 192.168.40.126  
- Broadcast: 192.168.40.127  

**Subnet 2 – Delivery Department**
- Network Address: 192.168.40.128  
- Subnet Mask: 255.255.255.128  
- Valid Hosts: 192.168.40.129 – 192.168.40.254  
- Broadcast: 192.168.40.255  

---

## 🖥️ Network Topology
**Devices Used:**
- 1 Router  
- 2 Switches (one for each department)  
- 2 PCs in **Accounts**  
- 2 PCs in **Delivery**  
- Copper straight-through cables  


---

## 📋 IP Addressing Scheme
| Department | Device           | IP Address     | Subnet Mask       | Gateway        |
|------------|------------------|----------------|-------------------|----------------|
| Accounts   | PC1              | 192.168.40.10  | 255.255.255.128   | 192.168.40.1   |
| Accounts   | PC2              | 192.168.40.20  | 255.255.255.128   | 192.168.40.1   |
| Accounts   | Router Fa0/0     | 192.168.40.1   | 255.255.255.128   | -              |
| Delivery   | PC3              | 192.168.40.130 | 255.255.255.128   | 192.168.40.129 |
| Delivery   | PC4              | 192.168.40.140 | 255.255.255.128   | 192.168.40.129 |
| Delivery   | Router Fa0/1     | 192.168.40.129 | 255.255.255.128   | -              |

---

## ⚙️ Configuration Steps
### Router Setup
```bash
Router> enable
Router# configure terminal

Router(config)# interface fa0/0
Router(config-if)# ip address 192.168.40.1 255.255.255.128
Router(config-if)# no shutdown

Router(config)# interface fa0/1
Router(config-if)# ip address 192.168.40.129 255.255.255.128
Router(config-if)# no shutdown
