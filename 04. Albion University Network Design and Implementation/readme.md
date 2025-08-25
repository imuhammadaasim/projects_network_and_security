# Albion University – Multi-Campus Network Design

## 📌 Project Overview
Albion University is a large university with two campuses located 20 miles apart. The university consists of four faculties:  

- Health & Sciences  
- Business  
- Engineering & Computing  
- Art & Design  

Each member of staff has a PC, and students have access to PCs in labs. This project outlines the **design and implementation** of the university’s campus network, including VLANs, Layer 2/3 switches, routers, DHCP, and RIP routing.

---

## 🎯 Project Objectives
- Deploy a scalable **multi-campus network** using Cisco devices.  
- Configure **VLANs for each department/faculty**.  
- Provide **dynamic IP addressing** using DHCP.  
- Enable **inter-VLAN communication** via Layer 3 switching and router sub-interfaces.  
- Implement **routing using RIP v2** for internal networks.  
- Provide connectivity to an **external cloud email server**.  

---

## 🖥️ Network Topology
### Main Campus
- **Building A:** Admin staff (Management, HR, Finance) and Faculty of Business  
- **Building B:** Faculty of Engineering & Computing, Faculty of Art & Design  
- **Building C:** Student labs and IT department hosting university web servers  

### Smaller Campus
- Faculty of Health & Sciences (separate floors for staff and student labs)  

### External Resources
- Cloud-hosted Email Server  

---

## 🌐 VLAN Design
| VLAN ID | Department / Faculty         | Switches                  |
|---------|-----------------------------|--------------------------|
| 10      | Admin                        | BA-admin-SW1, main-ABC-SW1 |
| 20      | HR                           | BA-HR-SW1, main-ABC-SW1  |
| 30      | Finance                      | BA-finance-SW1, main-ABC-SW1 |
| 40      | Business                     | BA-business-SW1, main-ABC-SW1 |
| 50      | Engineering & Computing      | BB-eng&comp-SW1, main-ABC-SW1 |
| 60      | Art & Design                 | BB-art&des-SW1, main-ABC-SW1 |
| 70      | Students Lab                 | BC-std.lab-SW1, main-ABC-SW1 |
| 80      | IT Department                | BC-it.dept-SW1, main-ABC-SW1 |
| 90      | Staff (Branch)               | branch-staff-SW1, branch-SW1 |
| 100     | Branch Student Lab           | branch-std.lab-SW1, branch-SW1 |

---

## ⚙️ Core Network Devices
### Routers
- **Main Campus R1:** Connects all main campus VLANs and branch WAN.  
- **Branch Campus R1:** Connects branch VLANs to main campus WAN.  
- **Cloud Router:** Connects internal network to cloud email server.  

### Switches
- **Layer 2 Switches:** Handle departmental VLANs and access ports.  
- **Layer 3 Switches:** Handle inter-VLAN routing, trunking between buildings and routers.  

---

## 📡 DHCP Pools
- Each VLAN has a separate DHCP pool for automatic IP assignment.  
- Default gateway set to the corresponding VLAN router sub-interface.  
- DNS server configured for internal IP resolution.

---

## 🌐 Routing
- **Internal routing:** RIP v2 is configured on all routers to share routes dynamically across campuses.  
- **External routing:** Static routes configured for cloud email server access.  

---

## 🔌 Trunk Configuration
- Trunk links configured between Layer 3 switches and between Layer 3 switches and routers.  
- Allowed VLANs are restricted to the VLANs in use to improve security and reduce broadcast traffic.  

---

## ✅ Testing & Verification
- **DHCP:** Check that PCs receive IPs from correct VLAN pools.  
- **Inter-VLAN Connectivity:** Ping between devices in different VLANs.  
- **Trunks:** Verify trunk port operation and VLAN propagation.  
- **Routing:** Ensure RIP updates propagate and external email server is reachable.  

---

## 🚀 Future Scalability
- Add VLANs for new faculties or departments.  
- Introduce a wireless controller for centralized AP management.  
- Implement redundancy for high availability.  
- Integrate additional cloud services or VPN access for remote students/staff.  

---

**Project:** Albion University – Multi-Campus Network Implementation  
