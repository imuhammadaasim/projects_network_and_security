# Vic Modern Hotel Network Design & Implementation

## 📌 Project Overview
As part of an end-of-year networking project, this documentation outlines the design and implementation of a comprehensive network infrastructure for Vic Modern Hotel. The hotel has three floors with multiple departments on each floor, requiring a segmented, secure, and fully connected network.

---

## 🏨 Hotel Layout & Department Structure

### 1st Floor Departments
- **Reception** - VLAN 80, Network: 192.168.8.0/24
- **Store** - VLAN 70, Network: 192.168.7.0/24
- **Logistics** - VLAN 60, Network: 192.168.6.0/24

### 2nd Floor Departments
- **Finance** - VLAN 50, Network: 192.168.5.0/24
- **HR** - VLAN 40, Network: 192.168.4.0/24
- **Sales/Marketing** - VLAN 30, Network: 192.168.3.0/24

### 3rd Floor Departments
- **Admin** - VLAN 20, Network: 192.168.2.0/24
- **IT** - VLAN 10, Network: 192.168.1.0/24

---

## 🎯 Technical Requirements

### Network Infrastructure
- Three routers (one per floor) located in the server room in the IT department
- Router interconnections using serial DCE cables
- Router network: 10.10.10.0/30, 10.10.10.4/30, 10.10.10.8/30
- One switch per floor (placed on respective floors)

### Connectivity Requirements
- WiFi networks on each floor for laptops and phones
- One printer per department
- Inter-VLAN routing for full network communication
- OSPF routing protocol for route advertisement

### Services & Security
- DHCP services on routers for dynamic IP addressing
- SSH configuration on all routers for remote access
- Port security on IT department switch (sticky MAC learning, violation shutdown)
- Test-PC in IT department (fa0/1) for remote login testing

---

## 🌐 Network Design Considerations

### Physical Design
- All routers centrally located in 3rd floor server room
- Serial connections between routers using DCE cables
- Floor switches connected to respective floor routers
- Departmental devices connected to floor switches

### Logical Design
- Separate VLAN for each department (8 total VLANs)
- OSPF routing protocol for dynamic route distribution
- DHCP scopes configured on respective routers
- Inter-VLAN routing enabled for complete connectivity

### Security Implementation
- SSH access configured on all routers
- Port security on critical IT department ports
- Network segmentation through VLAN implementation
- Separate subnets for each department

---

## ⚙️ Implementation Checklist

- [ ] Configure router interfaces with serial DCE connections
- [ ] Set up OSPF routing between all routers
- [ ] Create VLANs on all switches according to department requirements
- [ ] Configure router-on-a-stick or SVI interfaces for inter-VLAN routing
- [ ] Set up DHCP pools on routers for each VLAN
- [ ] Implement WiFi networks on each floor
- [ ] Connect and configure printers in each department
- [ ] Configure SSH on all routers for remote management
- [ ] Set up Test-PC in IT department and configure port security
- [ ] Test connectivity between all devices across VLANs
- [ ] Verify DHCP functionality across all departments
- [ ] Test remote SSH access to all routers

---

## 🔧 Technical Specifications

### Router-to-Router Connections
| Connection | Network | Subnet Mask |
|------------|---------|-------------|
| Router1-Router2 | 10.10.10.0 | 255.255.255.252 |
| Router2-Router3 | 10.10.10.4 | 255.255.255.252 |
| Router3-Router1 | 10.10.10.8 | 255.255.255.252 |

### Department VLAN Summary
| Department | VLAN ID | Network | Subnet Mask |
|------------|---------|---------|-------------|
| IT | 10 | 192.168.1.0 | 255.255.255.0 |
| Admin | 20 | 192.168.2.0 | 255.255.255.0 |
| Sales | 30 | 192.168.3.0 | 255.255.255.0 |
| HR | 40 | 192.168.4.0 | 255.255.255.0 |
| Finance | 50 | 192.168.5.0 | 255.255.255.0 |
| Logistics | 60 | 192.168.6.0 | 255.255.255.0 |
| Store | 70 | 192.168.7.0 | 255.255.255.0 |
| Reception | 80 | 192.168.8.0 | 255.255.255.0 |

---

## ✅ Verification Tests

- [ ] Ping tests between devices in different VLANs
- [ ] OSPF neighbor adjacency verification
- [ ] DHCP address assignment verification
- [ ] SSH connectivity to all routers
- [ ] Port security functionality test
- [ ] WiFi connectivity tests on all floors
- [ ] Printer accessibility from respective departments
- [ ] Inter-floor communication tests

---

This network design ensures secure, segmented, yet fully connected infrastructure for Vic Modern Hotel, meeting all specified requirements while maintaining scalability for future expansion.
