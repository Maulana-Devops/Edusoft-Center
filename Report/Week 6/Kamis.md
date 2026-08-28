# Article #1 — Network Packet Flow

> Project report for the Artikel Pribadi TJKT project.

## 1. Article Information

| Field            | Value                      |
| ---------------- | -------------------------- |
| Article          | #1                         |
| Topic            | Network Packet Flow        |
| Main Platform    | Hashnode                   |
| Technical Domain | Computer Networking / TJKT |
| Practical Tool   | Cisco Packet Tracer        |
| Status           | In Progress                |
| Primary Language | English                    |

---

## 2. Article Title

### H1

**Understanding Computer Networks: How a Packet Travels from One Host to Another**

### SEO Title

**How a Network Packet Travels Between Two Hosts**

### Slug

```text
understanding-network-packet-flow
```

---

## 3. Article Objective

The article explains how communication travels between two hosts on different IPv4 networks.

The main concepts covered are:

* Host
* IPv4 addressing
* MAC address
* ARP
* Ethernet frame
* Network switch
* Default gateway
* Router
* Routing table
* ICMP
* Packet flow

The article connects networking theory with a practical Cisco Packet Tracer experiment.

---

## 4. Practical Lab

### Devices

* 2 × PC-PT
* 2 × Cisco Catalyst 2960
* 1 × Cisco 1941 Router

### Topology

```text
PC-A
192.168.1.10/24
     |
     |
  Switch-A
     |
     |
  Router
G0/0: 192.168.1.1/24
G0/1: 192.168.2.1/24
     |
     |
  Switch-B
     |
     |
PC-B
192.168.2.10/24
```

---

## 5. Addressing Plan

| Device | Interface     | IP Address   | Subnet Mask   |
| ------ | ------------- | ------------ | ------------- |
| PC-A   | FastEthernet0 | 192.168.1.10 | 255.255.255.0 |
| Router | G0/0          | 192.168.1.1  | 255.255.255.0 |
| Router | G0/1          | 192.168.2.1  | 255.255.255.0 |
| PC-B   | FastEthernet0 | 192.168.2.10 | 255.255.255.0 |

### Default Gateways

| Device | Default Gateway |
| ------ | --------------- |
| PC-A   | 192.168.1.1     |
| PC-B   | 192.168.2.1     |

---

## 6. Practical Verification

### Router → PC-B

A connectivity test was performed from the router:

```text
Router#ping 192.168.2.10
```

Observed result:

```text
!!!!!
Success rate is 100 percent (5/5)
```

This confirms successful ICMP connectivity from the router to PC-B.

---

## 7. Verification Commands

### Router interface status

```text
show ip interface brief
```

Purpose:

* verify router interfaces
* verify IP addresses
* verify interface status

### Router ARP table

```text
show arp
```

Purpose:

* inspect IPv4-to-MAC address mappings known by the router

### Router routing table

```text
show ip route
```

Purpose:

* verify connected networks
* inspect the routes used for packet forwarding

### Switch MAC address table

```text
show mac address-table
```

Purpose:

* inspect MAC addresses learned by the switch

This command must be executed on the switch, not on the router.

---

## 8. Packet Flow Demonstration

The packet flow will be demonstrated using Cisco Packet Tracer Simulation Mode.

Expected logical path:

```text
PC-A
  ↓
Switch-A
  ↓
Router
  ↓
Switch-B
  ↓
PC-B
```

A Simple PDU / ICMP packet can be used to visualize the communication.

The simulation is intended to demonstrate the relationship between:

```text
IP addressing
     ↓
ARP
     ↓
MAC addressing
     ↓
Switch forwarding
     ↓
Default gateway
     ↓
Router forwarding
     ↓
ICMP
```

---

## 9. Screenshot Evidence

Target screenshots for the published article:

| # | Evidence                              | Purpose                        | Status  |
| - | ------------------------------------- | ------------------------------ | ------- |
| 1 | Full topology                         | Show complete lab              | Pending |
| 2 | PC-A IP configuration                 | Show host addressing           | Pending |
| 3 | Router interface configuration/status | Verify router interfaces       | Pending |
| 4 | ARP table                             | Demonstrate address resolution | Pending |
| 5 | Switch MAC address table              | Demonstrate Layer 2 learning   | Pending |
| 6 | Router routing table                  | Demonstrate Layer 3 routing    | Pending |
| 7 | PC-A → PC-B ping                      | Prove end-to-end connectivity  | Pending |
| 8 | Simulation Mode / Simple PDU          | Visualize packet flow          | Pending |

Only screenshots obtained from the actual lab should be included.

---

## 10. SEO Specification

### Search Intent

**Informational**

Main question:

> How does a network packet travel from one host to another?

### Primary Keyword

```text
network packet flow
```

### Secondary Keywords

```text
computer networking
network packet
IP address
MAC address
ARP
Ethernet
network switch
router
default gateway
ICMP
Cisco Packet Tracer
```

### Meta Description

```text
Learn how a network packet travels between two hosts using IP, ARP, MAC addresses, switches, routers, and ICMP.
```

### Tags

```text
networking
computer-networks
tjkt
cisco-packet-tracer
```

---

## 11. GEO / AEO Strategy

The article uses direct answers and explicit questions to make the technical information easy to understand and retrieve.

Example:

> **In short:** a host uses its IP configuration to determine where traffic should go, ARP can resolve a local IPv4 address to a MAC address, switches forward Ethernet frames, and routers forward packets between different IP networks.

FAQ topics:

* What is a network packet?
* What is the difference between an IP address and a MAC address?
* What does a switch do?
* What does a router do?
* What is a default gateway?
* Why is ARP needed?

---

## 12. Visual Identity

The article uses a reusable Canva OG image concept.

### Canva Template

**TJKT Article #1 — Network Packet Flow**

The visual system should be reused for future TJKT articles.

Canva design:

https://www.canva.com/d/Nuq1lkD-phG_qFL

Target OG image size:

```text
1200 × 630 px
```

---

## 13. Technical Lessons

The practical work demonstrates several important networking relationships:

```text
IP Address
    ↓
Determines logical destination
    ↓
ARP
    ↓
Resolves local IPv4 address to MAC address
    ↓
Ethernet Frame
    ↓
Switch forwards using MAC information
    ↓
Default Gateway
    ↓
Router forwards between IP networks
    ↓
ICMP
    ↓
Connectivity verification
```

The important distinction is:

* **Switch:** primarily forwards Ethernet frames using MAC addresses.
* **Router:** forwards packets between IP networks.
* **ARP:** helps map an IPv4 address to a MAC address on a local network segment.
* **ICMP:** provides the protocol used by tools such as `ping` for connectivity testing.

---

## 14. Troubleshooting Notes

During the lab, the following command distinction was identified:

### Incorrect on the router

```text
Router#show mac address-table
```

This produced:

```text
% Invalid input detected
```

### Correct on the switch

```text
Switch#show mac address-table
```

This demonstrates that the MAC address table is a Layer 2 switching function associated with the switch.

For the router, use:

```text
show arp
show ip route
show ip interface brief
```

---

## 15. Current Status

### Completed

* [x] Article topic selected
* [x] Article structure defined
* [x] Hashnode slug defined
* [x] SEO title defined
* [x] Meta description defined
* [x] Primary keyword defined
* [x] Secondary keywords defined
* [x] Lab topology defined
* [x] Device models defined
* [x] Addressing plan defined
* [x] Router → PC-B connectivity verified
* [x] Command distinction between router and switch verified
* [x] OG image concept created

### Remaining

* [ ] Capture final topology screenshot
* [ ] Capture PC-A configuration
* [ ] Capture router interface status
* [ ] Capture ARP table
* [ ] Capture switch MAC address table
* [ ] Capture routing table
* [ ] Capture PC-A → PC-B ping
* [ ] Capture Simulation Mode / Simple PDU
* [ ] Complete article draft
* [ ] Technical accuracy review
* [ ] SEO review
* [ ] GEO/AEO review
* [ ] Final Hashnode settings review
* [ ] Publish

---

## 16. Next Article

Planned direction:

> **IPv4 Addressing and Subnetting**

The next article should build on the network addressing concepts introduced in Article #1.

The exact topic and lab should be finalized after Article #1 is completed.

---

## 17. Project Principle

This article follows the main principle of the Artikel Pribadi TJKT project:

> **Build it. Observe it. Explain it. Prove it. Document it.**

The purpose is not simply to publish an article, but to document the development of practical TJKT/networking skills through real experimentation.
