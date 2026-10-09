# 🚀 Enterprise Network Architecture & Security Implementation

An end-to-end, multi-site enterprise network designed, configured, and simulated using **Cisco Packet Tracer**. This project connects the **Main HQ** with the **Giza Branch** through a redundant, high-availability, segmented, and secure network infrastructure.

---

## 📌 Network Topology Overview

![Network Topology](./topology.png)

> **Note:** Upload your topology screenshot to the root directory of this repository and name it `topology.png` so it renders automatically above.

---

## 🎯 Key Project Objectives

- **High Availability & L2/L3 Redundancy:** Elimination of single points of failure using **HSRP (First Hop Redundancy Protocol)**, **LACP EtherChannel**, and **Rapid PVST+**.
- **Structured Subnetting & Segmentation:** Efficient IP distribution using **VLSM** with strict departmental **VLAN** separation.
- **Perimeter & DMZ Security:** Multi-tiered defense using a **Cisco ASA 5506-X Firewall**, dedicated **DMZ isolation**, **Access Control Lists (ACLs)**, **SSH**, and **AAA / RADIUS** server authentication.
- **Inter-Site Connectivity:** Dynamic IP routing across WAN via **OSPF** and encrypted **Site-to-Site GRE Tunneling**.
- **Unified IP Services & Voice:** Centralized **DHCP Relay** (`ip helper-address`), **DNS**, **NTP**, DMZ-hosted application services (**Web, FTP, Email**), and **IP Telephony (Cisco CME)**.

---

## 🛠️ Implemented Technologies & Protocols

| Network Domain | Technologies & Protocols |
| :--- | :--- |
| **Network Architecture** | Hierarchical Three-Tier Model (Core, Distribution, Access) |
| **IP Addressing** | VLSM (Variable Length Subnet Masking) & Structured IPv4 Addressing |
| **Layer 2 Switching** | VLANs, 802.1Q Trunking, Inter-VLAN Routing, Rapid PVST+, LACP EtherChannel |
| **Layer 3 & Redundancy** | HSRP Gateway Redundancy, Dynamic OSPF Routing, Site-to-Site GRE Tunnel |
| **Core Network Services** | Centralized DHCP Server with Relay (`ip helper-address`), DNS, NTP Synchronization |
| **Network Security** | Cisco ASA 5506-X Firewall, DMZ Segmentation, ACLs, SSH Management, AAA / RADIUS |
| **DMZ Applications** | Web (HTTP/HTTPS), FTP, & Email Servers |
| **IP Telephony & Edge** | Cisco CallManager Express (CME), Voice VLANs, Wireless Access Points (WAP) |

---

## 📊 Network Segmentation & Services Overview

### **Internal LAN & Infrastructure**
* **Workstation VLANs:** Divided into dedicated VLANs for IT/Software, HR/Finance, and Sales/Operations.
* **Voice VLAN:** Dedicated Voice VLAN configured with Quality of Service (QoS) priorities for IP Telephony via Cisco CME.
* **Management & Native VLAN:** Secure SSH administration access and out-of-band device management.
* **Central Infrastructure VLAN:** Centralized hosting for DHCP, DNS, NTP, and AAA / RADIUS security servers.

### **DMZ Infrastructure (Demilitarized Zone)**
* **Isolated DMZ Zone:** Placed behind the Cisco ASA Firewall interface to allow controlled external/internal access to critical application servers:
  * **Web Server (HTTP/HTTPS)**
  * **FTP Server**
  * **Email Server**

---

## 🔐 Security Architecture & DMZ Enforcement

1. **Cisco ASA Firewall Policy:**
   * **DMZ Zone (Security Level 50):** Isolated hosting environment; accessible only via explicit stateful inspection and ACL policies.
   * **Outside / WAN Zone (Security Level 0):** Unreachable without explicit NAT/Firewall inspection rules.

2. **Centralized Identity Management (AAA / RADIUS):**
   * Network admin authentication mapped to a centralized RADIUS server for encrypted AAA logging and SSH CLI access across routers and switches.

---

## 🧪 Verification & Proof of Concept

The simulation includes complete validation and testing:
* ✅ **Inter-VLAN Connectivity:** Verified dynamic routing across Core and Distribution switches.
* ✅ **HSRP Gateway Failover:** Tested active-to-standby failover by simulating primary interface down state.
* ✅ **GRE Tunnel Routing:** Confirmed seamless end-to-end routing between HQ and Giza Branch over the WAN.
* ✅ **DMZ Reachability:** Confirmed successful HTTP, FTP, and Mail protocol sessions from inside and outside hosts.
* ✅ **IP Telephony Dialing:** Tested intra-site and inter-site call placement across extension numbers using Cisco CME.

---

## 📂 Repository Structure

```text
├── README.md                 # Complete Project Documentation
├── topology.png              # High-Resolution Network Diagram
├── Enterprise_Network.pkt    # Cisco Packet Tracer Project File
└── configs/                  # Saved Running Configurations
    ├── Core_Switch.txt
    ├── ASA_Firewall.txt
    └── HQ_Router.txt
