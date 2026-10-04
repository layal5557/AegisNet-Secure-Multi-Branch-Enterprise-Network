# AegisNet --- Secure Multi-Branch Enterprise Network {#aegisnet--secure-multi-branch-enterprise-network}

![Cisco Packet
Tracer](https://img.shields.io/badge/Cisco-Packet%20Tracer-1BA0D7)
![Networking](https://img.shields.io/badge/Focus-Networking%20%26%20Network%20Security-0A66C2)
![Routing](https://img.shields.io/badge/Routing-OSPF-orange)
![Status](https://img.shields.io/badge/Project-Completed-success)

## 📌 Project Overview {#pushpin-project-overview}

**AegisNet** is a large-scale enterprise network simulation designed and
implemented in **Cisco Packet Tracer**.

The project combines practical networking, routing, switching,
infrastructure security, network services, and troubleshooting skills
into one realistic multi-branch enterprise environment.

The design includes a redundant Headquarters network, regional and
remote branches, an ISP/Internet segment, and centralized internal
services.

## 🎯 Project Objectives {#dart-project-objectives}

-   Design a scalable multi-branch enterprise network.
-   Segment the network using VLANs.
-   Implement Layer 3 switching and inter-VLAN routing.
-   Provide redundancy and loop prevention using STP.
-   Implement dynamic routing with OSPF.
-   Provide centralized DHCP services.
-   Implement secure remote device management using SSH.
-   Implement NAT/PAT for Internet connectivity.
-   Deploy internal DNS and Web services.
-   Centralize time synchronization using NTP.
-   Centralize device logging using Syslog.
-   Apply Layer 2 security controls.
-   Validate end-to-end connectivity and troubleshoot configuration
    issues.

## 🏗️ Network Architecture {#building_construction-network-architecture}

## Network Topology
![AegisNet Network Topology]
(topology.png) 

The network contains **31 devices** across Headquarters, two remote
sites, and an ISP/Internet segment.

### Headquarters

-   2 × Cisco 3560 Multilayer Switches --- Core
-   2 × Cisco 3560 Multilayer Switches --- Distribution
-   4 × Cisco 2960 Switches --- Access
-   1 × Cisco 2911 --- HQ Edge Router
-   4 × Internal Servers
-   8 × PCs

### Regional Branch

-   1 × Cisco 2911 Router
-   1 × Cisco 2960 Switch
-   2 × PCs

### Remote Branch

-   1 × Cisco 2911 Router
-   1 × Cisco 2960 Switch
-   2 × PCs

### ISP / Internet {#isp--internet}

-   1 × Cisco 2911 ISP Router
-   1 × Internet Server

## 🗂️ VLAN Design {#card_index_dividers-vlan-design}

  VLAN   Name         Purpose                        Network
  ------ ------------ ------------------------------ ----------------
  10     USERS        User endpoints                 `10.10.0.0/24`
  20     SERVERS      Internal servers               `10.20.0.0/24`
  30     IT           IT infrastructure / services   `10.30.0.0/24`
  40     SECURITY     Security-related devices       `10.40.0.0/24`
  99     MANAGEMENT   Network management             `10.99.0.0/24`

## 🔀 Switching & Layer 3 Design {#twisted_rightwards_arrows-switching--layer-3-design}

The Headquarters uses a **Core / Distribution / Access** architecture.

Implemented technologies include:

-   VLAN segmentation
-   802.1Q trunking
-   Layer 3 switching
-   Switched Virtual Interfaces (SVIs)
-   Inter-VLAN routing
-   Spanning Tree Protocol (STP)
-   Redundant Core/Distribution paths
-   Port Security
-   Sticky MAC

STP was verified to prevent Layer 2 loops while maintaining redundant
paths.

## 🌐 Routing {#globe_with_meridians-routing}

## OSPF Verification
![OSPF Verification] (ospf.png)

### OSPF

**OSPF** was implemented as the dynamic routing protocol between the HQ
and branch networks.

OSPF neighbor relationships were verified successfully, and learned
routes were confirmed using routing-table verification.

### WAN Networks

Point-to-point `/30` networks were used for routed WAN links.

``` text
HQ Edge ↔ HQ Distribution
10.255.0.0/30

HQ Edge ↔ Regional Branch
10.255.0.4/30

HQ Edge ↔ Remote Branch
10.255.0.8/30
```

Branch LANs:

``` text
Regional Branch
10.50.0.0/24

Remote Branch
10.60.0.0/24
```

## 📡 DHCP {#satellite-dhcp}

Centralized DHCP was implemented on **HQ-Core1**.

DHCP pools were configured for:

-   VLAN 10 --- USERS
-   VLAN 20 --- SERVERS
-   VLAN 30 --- IT
-   VLAN 40 --- SECURITY

DHCP relay/helper configuration was used on the appropriate distribution
SVIs.

DHCP allocation was tested successfully on client devices.

## 🔐 Secure Device Management {#closed_lock_with_key-secure-device-management}

Network devices were configured for secure remote administration.

Implemented controls include:

-   SSH version 2
-   Local user authentication
-   Enable Secret
-   Password encryption
-   Console security
-   VTY access restricted to SSH
-   Telnet disabled

Verification included:

``` text
show ip ssh
show running-config | include username
show running-config | include transport input
```

## 🛡️ Layer 2 Security {#shield-layer-2-security}

Basic switch-level security controls were implemented, including:

-   Port Security
-   Sticky MAC

These controls help reduce the risk of unauthorized devices connecting
to protected access ports.

## 🌍 NAT / PAT & Internet Connectivity {#earth_africa-nat--pat--internet-connectivity}

## NAT/PAT Verification
![NAT/PAT Verfication] (nat.png)

NAT/PAT was implemented on the **HQ Edge Router** to provide Internet
connectivity for internal networks.

The design separates internal enterprise networks from the ISP/outside
network.

Verification included:

``` text
show ip nat translations
show ip nat statistics
```

Internal-to-Internet connectivity was successfully tested.

## 🧭 DNS & Internal Web Service {#compass-dns--internal-web-service}

## DNS & Web Verification
![DNS and Web Verification] (dns-web.png)

A dedicated DNS server was deployed for internal name resolution.

The internal web service was made accessible through:

``` text
http://www.aegisnet.local
```

DNS resolution and web access were tested successfully from internal
client devices.

## ⏱️ NTP {#stopwatch-ntp}

## NTP Verification
![NTP Verification] (ntp.png)

A dedicated NTP server was configured for centralized time
synchronization.

NTP server:

``` text
10.30.0.30
```

Verification:

``` text
show ntp status
show ntp associations
```

The NTP status was successfully verified as synchronized.

## 📝 Centralized Syslog {#pencil-centralized-syslog}

## Syslog Verification
![Syslog Verification] (syslog.png)

A dedicated Syslog server was configured at:

``` text
10.30.0.40
```

Network devices were configured to send system logs to the centralized
server.

Verification:

``` text
show logging
```

Syslog messages were successfully observed from configured devices.

## 🧪 Testing & Verification {#test_tube-testing--verification}

The network was validated through:

### Connectivity

-   Inter-VLAN ping tests
-   Branch-to-HQ connectivity
-   HQ-to-Internet connectivity
-   Server reachability
-   End-to-end connectivity

### Routing {#routing}

-   OSPF neighbor verification
-   Routing-table verification
-   Learned route validation

### NAT

-   NAT translation verification
-   NAT statistics
-   Internal-to-Internet testing

### Services

-   DHCP address assignment
-   DNS name resolution
-   Internal web access
-   NTP synchronization
-   Syslog message delivery

### Security

-   SSH access verification
-   Telnet restriction verification
-   Port Security / Sticky MAC verification

All major implemented services and connectivity paths were tested
successfully.

## 🛠️ Troubleshooting Experience {#hammer_and_wrench-troubleshooting-experience}

AegisNet was built as a hands-on project, so troubleshooting was an
important part of the implementation.

Issues were identified and resolved through:

-   Interface verification
-   VLAN verification
-   Trunk verification
-   Ping testing
-   Routing-table inspection
-   OSPF neighbor inspection
-   NAT translation inspection
-   DNS testing
-   Service verification
-   Configuration inspection

Useful Cisco IOS commands included:

``` text
show ip interface brief
show vlan brief
show interfaces trunk
show spanning-tree
show ip route
show ip ospf neighbor
show ip nat translations
show ip nat statistics
show ip ssh
show ntp status
show ntp associations
show logging
show running-config
```

## 📁 Project Structure {#file_folder-project-structure}

``` text
AegisNet-Secure-Multi-Branch-Enterprise-Network/
│
├── AegisNet-Secure-Multi-Branch-Enterprise-Network.pkt
├── README.md
│
└── screenshots/
    ├── topology.png
    ├── ospf.png
    ├── nat.png
    ├── dns-web.png
    ├── ntp.png
    └── syslog.png
```

## 💻 Technologies & Tools {#computer-technologies--tools}

-   Cisco Packet Tracer
-   Cisco IOS
-   VLAN
-   802.1Q
-   STP
-   Layer 3 Switching
-   SVI
-   DHCP
-   OSPF
-   NAT/PAT
-   DNS
-   HTTP
-   SSH
-   Port Security
-   Sticky MAC
-   NTP
-   Syslog

## 📚 Skills Demonstrated {#books-skills-demonstrated}

This project demonstrates practical experience in:

-   Enterprise network design
-   Network segmentation
-   Switching
-   Routing
-   Dynamic routing
-   Redundancy
-   Network services
-   Network security
-   Secure device management
-   NAT and Internet connectivity
-   Network troubleshooting
-   Cisco IOS configuration
-   Infrastructure documentation

## 👩‍💻 Author {#woman_technologist-author}

**Layal Sharaf**

Information Engineering Student\
Cybersecurity & Networking

GitHub: [\@layal5557](https://github.com/layal5557)

## 📌 Project Status {#pushpin-project-status}

**Completed --- September 2026**

AegisNet was developed as a hands-on portfolio project to consolidate
networking and network-security concepts and provide a practical
foundation for further cybersecurity and security-automation projects.
