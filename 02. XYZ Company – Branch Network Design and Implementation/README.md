# XYZ Company – Branch Network Design and Implementation


## 📌 Project Overview
XYZ Company is a fast-growing organization in Eastern Australia with over 2 million global customers. The company specializes in buying and selling food items, primarily managed from its headquarters. A new branch is planned in Bonalbo village, requiring a standalone network infrastructure. This document outlines the **network design and implementation** plan for the new branch.


---


## 🎯 Objectives
- Build a **small but scalable network** using Cisco devices.
- Implement **separate VLANs** for different departments.
- Provide **wireless connectivity** for users in all departments.
- Enable **DHCP for automatic IP addressing**.
- Allow **inter-VLAN routing** so departments can communicate.
- Ensure the network operates independently of the HQ network.


---


## 🖥️ Network Requirements
- **Devices**:
- 1 × Cisco Router (2911)
- 1 × Cisco Switch (2960)
- **Departments & VLANs**:
- VLAN 10 → Admin/IT
- VLAN 20 → Finance/HR
- VLAN 30 → Customer Service/Reception
- **Wireless**: Separate SSIDs for each department.
- **IP Addressing**: ISP provides base network `192.168.1.0/24`.
- **DHCP**: Each department must have its own DHCP pool.
- **Routing**: Inter-VLAN routing configured on the router.


---


## 🌐 Network Design


### Subnetting
- Base Network: `192.168.1.0/24`
- Required Subnets: 3
- New Subnet Mask: `/26 (255.255.255.192)` → Block size = 64


| VLAN | Department | Network Address | Broadcast Address | Host Range |
|------|---------------------|-----------------|------------------|-----------------------------|
| 10 | Admin/IT | 192.168.1.0 | 192.168.1.63 | 192.168.1.1 – 192.168.1.62 |
| 20 | Finance/HR | 192.168.1.64 | 192.168.1.127 | 192.168.1.65 – 192.168.1.126|
| 30 | CS/Reception | 192.168.1.128 | 192.168.1.191 | 192.168.1.129 – 192.168.1.190|


---


## ⚙️ Router Configuration

| Configuration Section | Command |
| :--- | :--- |
| **Hostname** | `hostname Router` |
| **Admin DHCP Pool** | `ip dhcp pool Admin-Pool`<br>`network 192.168.1.0 255.255.255.192`<br>`default-router 192.168.1.1`<br>`dns-server 192.168.1.1`<br>`domain-name admin.com` |
| **Finance DHCP Pool** | `ip dhcp pool Finance-Pool`<br>`network 192.168.1.64 255.255.255.192`<br>`default-router 192.168.1.65`<br>`dns-server 192.168.1.65`<br>`domain-name finance.com` |
| **Reception DHCP Pool** | `ip dhcp pool Reception-Pool`<br>`network 192.168.1.128 255.255.255.192`<br>`default-router 192.168.1.129`<br>`dns-server 192.168.1.129`<br>`domain-name reception.com` |
| **Main Interface** | `interface GigabitEthernet0/0`<br>`no ip address`<br>`duplex auto`<br>`speed auto` |
| **VLAN 10 Subinterface** | `interface GigabitEthernet0/0.10`<br>`encapsulation dot1Q 10`<br>`ip address 192.168.1.1 255.255.255.192` |
| **VLAN 20 Subinterface** | `interface GigabitEthernet0/0.20`<br>`encapsulation dot1Q 20`<br>`ip address 192.168.1.65 255.255.255.192` |
| **VLAN 30 Subinterface** | `interface GigabitEthernet0/0.30`<br>`encapsulation dot1Q 30`<br>`ip address 192.168.1.129 255.255.255.192` |
| **IP Routing** | `ip routing` |

## ⚙️ Switch Configuration

| Configuration Section | Command |
| :--- | :--- |
| **Hostname** | `hostname Switch` |
| **VLAN 10** | `vlan 10`<br>`name VLAN0010` |
| **VLAN 20** | `vlan 20`<br>`name VLAN0020` |
| **VLAN 30** | `vlan 30`<br>`name VLAN0030` |
| **VLAN 10 Access Ports** | `interface range FastEthernet0/2-4`<br>`switchport mode access`<br>`switchport access vlan 10` |
| **VLAN 20 Access Ports** | `interface range FastEthernet0/5-7`<br>`switchport mode access`<br>`switchport access vlan 20` |
| **VLAN 30 Access Ports** | `interface range FastEthernet0/8-10`<br>`switchport mode access`<br>`switchport access vlan 30` |
| **Trunk Port Configuration** | `interface FastEthernet0/1`<br>`switchport mode trunk`<br>`switchport trunk encapsulation dot1q`<br>`switchport trunk native vlan 1`<br>`switchport trunk allowed vlan 1-1005` |


---


## 📡 Wireless Setup

**SSIDs per Department:**
- **Admin_IT_WiFi** → VLAN 10
- **Finance_HR_WiFi** → VLAN 20
- **Reception_WiFi** → VLAN 30

Access Points connect to VLAN-configured switch ports.

---

## 🔍 Testing & Verification

**DHCP:** Verify hosts receive IPs from correct pool (`ipconfig /all`)

**VLANs:** Check with `show vlan brief`

**Trunk:** Verify with `show interfaces trunk`

**Routing:** Test inter-department ping

**Wireless:** Confirm correct SSID and IP assignment


---


## ✅ Conclusion

This network design ensures that the new XYZ branch in Bonalbo operates independently while fulfilling requirements of segmentation, wireless connectivity, DHCP automation, and inter-department communication. The modular design allows for easy scalability and future HQ integration.
