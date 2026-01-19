# Lab 04: VLAN Segmentation & Network Address Translation (NAT)

## 📌 Overview
This lab demonstrates the integration of **Virtual Local Area Networks (VLANs)** for network segmentation and **Network Address Translation (NAT)** for external connectivity. The setup utilizes **Router-on-a-Stick** for inter-VLAN communication and **Port Address Translation (PAT)** to allow multiple private internal hosts to share a single public IP address.

## 🛠️ Network Topology
The lab simulates a small enterprise network connected to an ISP:
* **1 Cisco Router (2911):** Functions as the internal gateway and performs NAT/Routing.
* **1 Cisco Switch (2960):** Manages Layer 2 segmentation (VLANs).
* **1 ISP Router:** Represents the external internet backbone.
* **PCs:** Assigned to specific VLANs (e.g., Data, Voice).

## 🚀 Key Configurations

### 1. Switch Configuration (VLANs & Trunking)
We created distinct VLANs to isolate broadcast domains and configured a **Trunk Link** to the router to carry tagged traffic.

```bash
! Create VLANs
Switch(config)# vlan 10
Switch(config-vlan)# name DATA
Switch(config)# vlan 20
Switch(config-vlan)# name VOICE

! Configure Access Ports
Switch(config)# interface range fa0/1-10
Switch(config-if-range)# switchport mode access
Switch(config-if-range)# switchport access vlan 10

! Configure Trunk Port to Router
Switch(config)# interface gig0/1
Switch(config-if)# switchport mode trunk