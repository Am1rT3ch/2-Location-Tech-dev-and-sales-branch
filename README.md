# 🏪 2 Location Tech Sales and dev Branch with WiFi

A hybrid wired and wireless network for a simulated tech sales store and a product development center, built using Cisco Packet Tracer as part of my CCNA-level hands-on training.

---

## 📋 Project Overview

This project simulates the IT infrastructure of a small retail tech branch and a dev location. It combines VLAN-based segmentation with secure wireless access, designed to support both employees and visiting customers while maintaining a secure and manageable network.

---

## 🔧 Features

- **VLAN Segmentation**  
  Dedicated VLANs for staff and guests for network isolation and improved security.
  Six VLANs separating departments and security systems of 2 locations:
  * vlan 10 - tech support for sales
  * vlan 20 - accounting department
  * vlan 30 - accounting managment
  * vlan 40 - sales department
  * vlan 50 - sales managment
  * vlan 60 - reception department
  * vlan 70 - clients wifi
  * vlan 110 - tech support for dev
  * vlan 120 - managment department
  * vlan 130 - operations department
  * vlan 140 - development department
  * vlan 150 - wifi for workers

- **Router-on-a-Stick (ROAS)**  
  Central routing setup to enable communication between VLANs.

- **DHCP Server**  
  Dynamic IP allocation to all wired devices based on VLAN.

- **Wireless Access Point (WAP)**  
  Configured internet access to customers and workers.
  
- **OSPF (Dynamic Routing)**
Enables automatic route exchange between sites with fast convergence and efficient path selection.

- **Access Control Lists (ACLs)**  
  Network-level policies to restrict guest access to sensitive segments.

- **Ping Tests**  
  Used to validate inter-VLAN connectivity and troubleshoot issues.

---

## 🛠️ Tools & Technologies

- Cisco Packet Tracer  
- VLANs  
- DHCP  
- ROAS
- OSPF
- Wireless Access Point (WPA2)  
- SSH  
- ACLs  

---

## 📂 Files Included

- `.pkt` file of the full network topology  
- Documentation & Configuration 

---

## 🌐 Use Case

This type of setup is typical for small retail branches or customer-facing offices that need to support both internal operations and public Wi-Fi in a secure way.

---
