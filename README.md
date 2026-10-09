# 🚀 Enterprise Network Architecture & Security Implementation

[![Cisco Packet Tracer](https://img.shields.io/badge/Cisco_Packet_Tracer-v8.2%2B-005073?style=for-the-badge&logo=cisco&logoColor=white)](https://www.netacad.com/)
[![CCNA](https://img.shields.io/badge/CCNA-Enterprise_Networking-008080?style=for-the-badge)](https://www.cisco.com/)
[![Security](https://img.shields.io/badge/Network_Security-Cisco_ASA-red?style=for-the-badge)](https://www.cisco.com/)

An enterprise-style, multi-site network designed, configured, and simulated using **Cisco Packet Tracer**. The project connects the **Main Headquarters (HQ)** with the **Giza Branch (BRANCH B)**, combining network segmentation, routing, redundancy, centralized services, IP telephony, and perimeter security.

The goal is to apply CCNA networking concepts in a practical environment and demonstrate how different network technologies work together through configuration and verification.

---

## 📋 Table of Contents

- [Project Overview](#-project-overview)
- [Network Topology](#-network-topology)
- [Technologies Implemented](#-technologies-implemented)
- [VLAN and IP Addressing Scheme](#-vlan-and-ip-addressing-scheme)
- [High Availability and HSRP](#-high-availability-and-hsrp)
- [Routing and GRE Tunnel](#-routing-and-gre-tunnel)
- [Network Security and DMZ](#-network-security-and-dmz)
- [AAA and RADIUS Authentication](#-aaa-and-radius-authentication)
- [Network Services and VoIP](#-network-services-and-voip)
- [Verification and Testing](#-verification-and-testing)
- [How to Run the Project](#-how-to-run-the-project)
- [Project Structure](#-project-structure)
- [Author](#-author)

---

## 📋 Project Overview

The network is designed around a **Three-Tier Architecture** consisting of Core, Distribution, and Access layers at the Main HQ, with a remote branch connected over a simulated WAN.

The design focuses on:

- **Network Segmentation:** Departmental VLANs and a dedicated voice VLAN.
- **High Availability:** HSRP gateway redundancy and LACP EtherChannel.
- **Dynamic Routing:** OSPF for exchanging routes between network devices and sites.
- **Site Connectivity:** A GRE tunnel connecting the HQ and Giza Branch.
- **Perimeter Security:** Cisco ASA Firewall, access control lists, and a separated DMZ.
- **Centralized Services:** DHCP, DNS, NTP, and RADIUS.
- **Unified Communications:** Cisco CallManager Express (CME) and IP phones.

The project was implemented in Cisco Packet Tracer to practice configuration, troubleshooting, and end-to-end connectivity verification.

---

## 🖧 Network Topology

The topology is divided into the following logical areas:

| Network Zone | Purpose |
|---|---|
| **Main HQ** | Hosts departmental networks and the core infrastructure. |
| **Core and Distribution** | Provides Layer 3 connectivity, routing, and gateway redundancy. |
| **Access Layer** | Connects end devices, IP phones, and wireless access points. |
| **Central Server VLAN** | Hosts internal network services, including DHCP, DNS, NTP, and RADIUS. |
| **DMZ** | Hosts services intended to be accessed through controlled firewall rules. |
| **Giza Branch** | Connects remote clients to permitted HQ and DMZ resources. |
| **WAN and GRE Tunnel** | Provides routed connectivity between the sites. |

### Network Topology Diagram

![Enterprise Network Topology](./topology.png)

> **Note:** Ensure the topology image is named `topology.png` and is located in the repository root. Update the image path if your filename or folder structure differs.

---

## ⚙️ Technologies Implemented

| Category | Technologies | Purpose |
|---|---|---|
| Architecture | Three-Tier Network Design | Separates Core, Distribution, and Access responsibilities. |
| IP Addressing | IPv4, VLSM, Subnetting | Organizes networks and IP address allocation. |
| Switching | VLANs, 802.1Q Trunking, Rapid PVST+ | Provides segmentation and Layer 2 loop prevention. |
| Link Aggregation | LACP EtherChannel | Combines physical links into logical bundles. |
| Layer 3 Switching | SVIs, Inter-VLAN Routing | Enables communication between VLANs. |
| Gateway Redundancy | HSRP | Provides a virtual default gateway with active/standby roles. |
| Routing | Single-Area OSPF, Area 0 | Exchanges routing information dynamically. |
| WAN Connectivity | GRE Site-to-Site Tunnel | Carries routed traffic between tunnel endpoints. |
| NAT | PAT | Allows multiple internal clients to share an external IPv4 address, where configured. |
| Security | Cisco ASA Firewall, ACLs, DMZ | Controls traffic between network security zones. |
| Authentication | AAA, RADIUS, SSH | Supports centralized administrative authentication and secure device management. |
| Network Services | DHCP, DHCP Relay, DNS, NTP | Provides address assignment, name resolution, and time synchronization. |
| Voice | Cisco CME, Voice VLAN 88 | Supports IP phone registration and extension dialing. |
| Wireless | Wireless Access Points | Provides wireless client connectivity. |

---

## 📐 VLAN and IP Addressing Scheme

### Main HQ Departmental Networks

The following table documents the planned HQ VLAN and gateway structure.

| Floor / Zone | VLAN ID | Department | Network Subnet | Virtual Gateway |
|---|---:|---|---|---|
| Floor 1 | 10 | Software Developers | `10.50.10.0/24` | `10.50.10.1` |
| Floor 1 | 20 | IT Department | `10.50.20.0/24` | `10.50.20.1` |
| Floor 2 | 30 | HR Department | `10.50.30.0/24` | `10.50.30.1` |
| Floor 2 | 40 | Finance Department | `10.50.40.0/24` | `10.50.40.1` |
| Floor 3 | 50 | Marketing Department | `10.50.50.0/24` | `10.50.50.1` |
| Floor 3 | 60 | Customer Support | `10.50.60.0/24` | `10.50.60.1` |
| Infrastructure | 70 | Central Servers | `10.50.70.0/24` | `10.50.70.1` |
| Voice | 88 | IP Telephony | `10.50.88.0/24` | `10.50.88.1` |

The HQ departmental networks use the `10.50.0.0/16` address space, with individual `/24` subnets allocated to the listed VLANs.

### HSRP Interface Addresses

The intended gateway arrangement uses a virtual IP shared by two Layer 3 switches.

| VLAN | Virtual IP | Primary Switch IP | Secondary Switch IP |
|---:|---|---|---|
| 10 | `10.50.10.1` | `10.50.10.2` | `10.50.10.3` |
| 20 | `10.50.20.1` | `10.50.20.2` | `10.50.20.3` |
| 30 | `10.50.30.1` | `10.50.30.2` | `10.50.30.3` |
| 40 | `10.50.40.1` | `10.50.40.2` | `10.50.40.3` |
| 50 | `10.50.50.1` | `10.50.50.2` | `10.50.50.3` |
| 60 | `10.50.60.1` | `10.50.60.2` | `10.50.60.3` |
| 70 | `10.50.70.1` | `10.50.70.2` | `10.50.70.3` |
| 88 | `10.50.88.1` | `10.50.88.2` | `10.50.88.3` |

### DMZ Network

| Component | IP Address |
|---|---|
| ASA DMZ Gateway | `192.168.100.1/24` |
| Web Server | `192.168.100.10` |
| DNS Server | `192.168.100.11` |
| FTP Server | `192.168.100.12` |
| Email Server | `192.168.100.13` |

### Giza Branch Network

| Component | IP Address |
|---|---|
| Branch Gateway | `192.168.1.1/24` |
| Branch Client 1 | `192.168.1.2` |
| Branch Client 2 | `192.168.1.3` |

**Important:** Update these tables if the final `.pkt` file uses different addresses or interface assignments.

---

## 🔄 High Availability and HSRP

**Hot Standby Router Protocol (HSRP)** provides gateway redundancy for the configured VLANs. End devices use a virtual IP as their default gateway, while the two Layer 3 switches maintain their own interface addresses.

If the active switch becomes unavailable, the standby switch can take over the active gateway role, provided the HSRP configuration and relevant connectivity support the failover.

### Example Configuration — VLAN 10

**Primary switch:**

```cisco
interface Vlan10
 ip address 10.50.10.2 255.255.255.0
 standby 10 ip 10.50.10.1
 standby 10 priority 110
 standby 10 preempt
```

**Secondary switch:**

```cisco
interface Vlan10
 ip address 10.50.10.3 255.255.255.0
 standby 10 ip 10.50.10.1
 standby 10 priority 100
```

These commands are illustrative examples. The actual project configuration may use different HSRP priorities or group numbers.

### Verification Commands

```cisco
show standby brief
show standby
show ip interface brief
```

---

## 🌐 Routing and GRE Tunnel

### OSPF Dynamic Routing

The network uses **single-area OSPF (Area 0)** to exchange routes between configured routing devices. This supports connectivity between the HQ, the branch, and the networks advertised into OSPF.

Example verification commands:

```cisco
show ip ospf neighbor
show ip route ospf
show ip protocols
show ip ospf database
```

A neighbor state of `FULL` indicates that the OSPF adjacency has reached the full state. Reachability should also be verified by checking routing tables and testing connectivity to remote subnets.

### GRE Site-to-Site Tunnel

A **Generic Routing Encapsulation (GRE)** tunnel provides a logical point-to-point interface between the configured tunnel endpoints. The tunnel uses an underlay path between its source and destination addresses.

Example configuration template:

```cisco
interface Tunnel0
 ip address <TUNNEL_IP> <TUNNEL_MASK>
 tunnel source <SOURCE_INTERFACE_OR_IP>
 tunnel destination <REMOTE_UNDERLAY_IP>
```

Replace the placeholders with the actual addresses and interface names from the project configuration.

### Verification Commands

```cisco
show interfaces tunnel 0
show ip interface brief
show ip route
ping <REMOTE_TUNNEL_IP>
```

> **Security note:** GRE provides encapsulation, not encryption. The tunnel should not be described as encrypted unless a separate encryption mechanism, such as IPsec, is also configured.

---

## 🔐 Network Security and DMZ

The network uses a Cisco ASA Firewall to separate the DMZ from other network zones and control traffic through interface security levels and access control lists.

The DMZ contains the following services:

- **Web Server:** Hosts the company website.
- **DNS Server:** Provides DNS service for the configured environment.
- **FTP Server:** Supports file transfer.
- **Email Server:** Provides the configured email services.

ACLs define which traffic is permitted between the relevant zones. The intended design allows access to selected DMZ services while restricting other traffic according to the configured rules.

### Security Components

- Cisco ASA Firewall
- DMZ network segmentation
- Access Control Lists (ACLs)
- Controlled access to hosted services
- SSH for remote device administration
- AAA with RADIUS authentication for supported administrative logins

### Verification

Test the services from the intended source networks and confirm both permitted and denied traffic behaves as expected. For example, verify that the web server is reachable from authorized clients and that restricted traffic is blocked by the relevant firewall or ACL rules.

---

## 🔑 AAA and RADIUS Authentication

The project includes **Authentication, Authorization, and Accounting (AAA)** with a centralized RADIUS server for administrative login authentication on the configured core switches.

- **RADIUS Server:** `10.50.70.80`
- **Server Network:** VLAN 70 — `10.50.70.0/24`
- **Configured Network Devices:** Core and Secondary switches
- **Management Access:** SSH

### Example Configuration Template

```cisco
aaa new-model
radius-server host <RADIUS_SERVER_IP> key <SHARED_SECRET>
aaa authentication login default group radius local
```

Replace the placeholders with the values used in the actual configuration. The `local` method provides a fallback to the local username database if RADIUS authentication is unavailable, subject to the configured login method list and platform behavior.

**Security recommendation:** Do not publish actual shared secrets, passwords, or other credentials in a public repository. Use placeholders in documentation and keep the real values in the Packet Tracer lab only as needed.

### Verification

Test SSH login with a valid RADIUS account, then verify the intended fallback behavior if the RADIUS server is unavailable.

---

## 📞 Network Services and VoIP

### Centralized DHCP and DHCP Relay

The central DHCP server provides dynamic IP address allocation to configured client VLANs.

Layer 3 interfaces use `ip helper-address` to relay DHCP requests from remote VLANs to the central server. This enables clients to obtain addresses without placing a separate DHCP server in every VLAN.

Example:

```cisco
interface Vlan10
 ip helper-address 10.50.70.70
```

The helper address should point to the actual DHCP server, and the DHCP server must have the correct scope, subnet mask, default gateway, and any required DNS options for each client network.

### DNS and NTP

- **DNS:** Resolves configured hostnames to IP addresses.
- **NTP:** Synchronizes device clocks when the relevant clients and server are configured correctly.

### Cisco CallManager Express (CME)

The project includes Cisco CME-based IP telephony with a dedicated **Voice VLAN 88**. IP phones receive network configuration and register with the configured call-control service. Extensions are configured for dialing between phones.

Example CME configuration:

```cisco
telephony-service
 max-ephones 20
 max-dn 20
 ip source-address <CME_SOURCE_IP> port 2000
 auto assign 1 to 10

ephone-dn 1
 number 111
```

This is an example, not a complete phone configuration. Use the actual CME source address, directory numbers, phone registrations, and DHCP voice settings from the final project.

---

## 🧪 Verification and Testing

The project includes configuration and connectivity checks for the following features:

| Feature | Verification Goal |
|---|---|
| VLAN Segmentation | Confirm devices are assigned to the intended VLANs. |
| Trunking | Verify the required VLANs are carried across trunk links. |
| LACP EtherChannel | Confirm port-channel formation and member-link status. |
| Rapid PVST+ | Verify spanning-tree roles and states for relevant VLANs. |
| HSRP | Confirm active/standby roles and test gateway failover. |
| OSPF | Check neighbor adjacencies and advertised routes. |
| GRE Tunnel | Check tunnel interface status and remote reachability. |
| DHCP Relay | Confirm clients in different VLANs receive valid addresses. |
| Inter-VLAN Routing | Test communication between permitted VLANs. |
| AAA/RADIUS | Test administrative authentication through the configured RADIUS server. |
| DMZ Services | Test access to the configured web, DNS, FTP, and email services. |
| VoIP | Confirm phone registration and calls between configured extensions. |
| Wireless | Verify client connectivity and the configured wireless security settings. |

### Useful Cisco CLI Commands

```cisco
show vlan brief
show interfaces trunk
show etherchannel summary
show spanning-tree
show standby brief
show ip ospf neighbor
show ip route
show ip interface brief
show access-lists
```

Use these commands to collect screenshots or CLI output for the repository. Include only verification results that correspond to tests you have actually performed.

---

## 🚀 How to Run the Project

### Prerequisites

- Cisco Packet Tracer compatible with the saved project file.
- The Packet Tracer project file (`.pkt`).
- Optional: topology images and CLI verification screenshots.

### Steps

1. **Clone the repository:**

   ```bash
   git clone https://github.com/faresmohamed/CCNA-Full-Project.git
   ```

2. **Open the project:** Launch Cisco Packet Tracer and open `FinalProject.pkt`.

3. **Allow convergence:** Wait for switching, routing, and redundancy protocols to initialize.

4. **Verify connectivity:** Test client addressing, inter-VLAN routing, branch reachability, DMZ services, and VoIP calls.

5. **Inspect configurations:** Use the CLI verification commands above to review the relevant devices and protocols.

> File names are case-sensitive in some environments. Make sure `FinalProject.pkt` and `topology.png` match the actual filenames in your repository.

---

## 📁 Project Structure

A suggested repository structure:

```text
CCNA-Full-Project/
├── README.md
├── FinalProject.pkt
├── topology.png
└── screenshots/
    ├── hsrp-verification.png
    ├── ospf-neighbors.png
    ├── etherchannel-status.png
    ├── aaa-radius-test.png
    ├── dmz-connectivity.png
    └── voip-test-ring.png
    └── voip-test-connect.png
```

Rename or remove the example screenshot paths to match the files you actually upload.

---

## 👨‍💻 Author

**Fares Mohamed**

Computer Engineering & Systems Graduate

- **Focus Areas:** Networking, Routing & Switching, Network Security, and System Administration
- **Project Tools:** Cisco Packet Tracer and Cisco IOS CLI
- **LinkedIn:** [Fares Salem](https://www.linkedin.com/in/faresmohamed185/)

---

⭐ If you find this project useful, feel free to explore the topology and configuration examples.

*This project is a simulated learning environment built for hands-on practice with enterprise networking concepts. It is not a production deployment.*
