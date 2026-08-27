# Understanding Computer Networks by Following a Packet from One Host to Another

When learning computer networking, it is easy to encounter terms such as IP address, MAC address, ARP, switch, router, default gateway, and routing table.

The difficult part is not simply memorizing what each term means.

The more important question is:

> **What actually happens when one computer sends data to another computer?**

In this article, I will follow a simple packet flow from one host to another to understand how these networking concepts work together.

> **In short:** a host uses its IP configuration to determine where traffic should go, ARP can resolve IPv4 addresses to MAC addresses on the local network, switches forward Ethernet frames, and routers forward packets between different IP networks.

**[SCREENSHOT 1 — PLACE YOUR NETWORK TOPOLOGY HERE]**

*Figure 1 — The network topology used to demonstrate packet flow.*

---

## Why Understanding Packet Flow Matters

When studying networking, it is easy to treat every concept as a separate definition.

For example:

* An **IP address** identifies a host at the network layer.
* A **MAC address** identifies a network interface at the local network.
* **ARP** helps discover the MAC address associated with an IPv4 address on a local network.
* A **switch** forwards Ethernet frames based on MAC addresses.
* A **router** forwards packets between IP networks.
* A **default gateway** provides the next hop for traffic destined outside the local network.

Knowing these definitions is useful, but it does not explain how they interact.

A better way to learn networking is to follow an actual communication process.

Instead of only asking:

> What is a router?

we can ask:

> What happens when a host wants to communicate with another host in a different network?

This approach is also useful for troubleshooting because a failed connection can be investigated step by step.

---

## The Network Topology

For this experiment, I use a simple topology:

```text
PC-A ── Switch-A ── Router ── Switch-B ── PC-B
```

The addressing plan is:

| Device | Interface | IP Address        | Network          |
| ------ | --------- | ----------------- | ---------------- |
| PC-A   | NIC       | `192.168.1.10/24` | `192.168.1.0/24` |
| Router | G0/0      | `192.168.1.1/24`  | `192.168.1.0/24` |
| Router | G0/1      | `192.168.2.1/24`  | `192.168.2.0/24` |
| PC-B   | NIC       | `192.168.2.10/24` | `192.168.2.0/24` |

PC-A uses `192.168.1.1` as its default gateway, while PC-B uses `192.168.2.1`.

**[SCREENSHOT 2 — PLACE THE IP CONFIGURATION OF PC-A HERE]**

*Figure 2 — IP address and default gateway configuration on PC-A.*

**[SCREENSHOT 3 — PLACE THE ROUTER INTERFACE CONFIGURATION HERE]**

*Figure 3 — Router interfaces connecting the two networks.*

---

## 1. Host: Where Communication Begins

A host is a device that participates in network communication.

Examples include:

* computers
* servers
* virtual machines
* smartphones
* network-connected devices

In this experiment, PC-A is the source host and PC-B is the destination host.

PC-A has:

```text
IP address:       192.168.1.10
Subnet:           /24
Default gateway:  192.168.1.1
```

PC-B has:

```text
IP address:       192.168.2.10
Subnet:           /24
Default gateway:  192.168.2.1
```

When PC-A wants to communicate with `192.168.2.10`, it first needs to determine whether the destination belongs to its local network.

Because `192.168.1.10/24` and `192.168.2.10/24` belong to different networks, PC-A needs to send the traffic toward a router.

---

## 2. IP Address: Identifying the Destination

An IPv4 address provides logical addressing for devices on an IP network.

In this experiment:

```text
PC-A
192.168.1.10/24
```

is located in:

```text
192.168.1.0/24
```

while PC-B:

```text
192.168.2.10/24
```

is located in:

```text
192.168.2.0/24
```

The two hosts are therefore on different IP networks.

This distinction matters because a host handles local and remote destinations differently.

For a local destination, the host can communicate through the local network.

For a remote destination, the host sends the traffic toward its default gateway.

---

## 3. ARP: Resolving an IPv4 Address to a MAC Address

IP addresses are used for logical addressing, but Ethernet communication on a local network uses MAC addresses.

This creates an important question:

> If PC-A knows the IP address it needs to reach, how does it determine the MAC address needed for the Ethernet frame?

For IPv4 communication on a local Ethernet network, one mechanism used for this purpose is **Address Resolution Protocol (ARP)**.

Conceptually, a host can send an ARP request asking:

```text
Who has this IPv4 address?
```

The host that owns that IPv4 address can respond with its MAC address.

For example:

```text
PC-A
192.168.1.10
     │
     │ ARP Request
     ▼
Local Network
     │
     │ ARP Reply
     ▼
Destination / Gateway MAC
```

On Linux, the neighbor table can be inspected with:

```bash
ip neigh
```

On Windows:

```powershell
arp -a
```

**[SCREENSHOT 4 — PLACE YOUR ARP / NEIGHBOR TABLE HERE]**

*Figure 4 — ARP or neighbor information observed during the experiment.*

---

## 4. Switch: Forwarding Ethernet Frames

A switch operates primarily at Layer 2 and uses MAC addresses to make forwarding decisions.

A simplified network looks like this:

```text
PC-A
  │
  ▼
Switch
  │
  ├── PC-B
  ├── PC-C
  └── PC-D
```

A switch learns which MAC addresses are associated with its ports and stores this information in a MAC address table.

A simplified example:

```text
MAC Address          Port
-------------------------
AA:AA:AA:AA:AA:AA    1
BB:BB:BB:BB:BB:BB    2
CC:CC:CC:CC:CC:CC    3
```

When a frame arrives, the switch examines the destination MAC address and determines how to forward the frame.

**[SCREENSHOT 5 — PLACE YOUR SWITCH MAC ADDRESS TABLE HERE]**

*Figure 5 — MAC address table observed on the switch.*

---

## 5. Default Gateway: The Path Out of the Local Network

A default gateway is the router address a host uses when it needs to reach a destination outside its local network.

For PC-A:

```text
IP address:
192.168.1.10

Default gateway:
192.168.1.1
```

If PC-A wants to communicate with:

```text
192.168.1.20
```

the destination is inside the local network.

But if the destination is:

```text
192.168.2.10
```

the destination belongs to another network.

PC-A therefore sends the traffic toward:

```text
192.168.1.1
```

its default gateway.

This is an important distinction:

> **The host does not send an Ethernet frame directly to the remote host's MAC address across the router. The first-hop Ethernet frame is addressed to the local gateway's MAC address.**

---

## 6. Router: Connecting Different IP Networks

A router connects different IP networks and makes forwarding decisions based on IP addressing and its routing information.

In this experiment, the router has two interfaces:

```text
G0/0
192.168.1.1/24

G0/1
192.168.2.1/24
```

The router therefore has connectivity to both networks:

```text
192.168.1.0/24
        │
        │
      Router
        │
        │
192.168.2.0/24
```

When the router receives traffic destined for `192.168.2.10`, it examines the destination IP address and determines how the packet should be forwarded.

**[SCREENSHOT 6 — PLACE YOUR ROUTING TABLE HERE]**

*Figure 6 — Routing information used by the router.*

---

## 7. Following a Ping from PC-A to PC-B

Now we can combine the concepts.

PC-A runs:

```bash
ping 192.168.2.10
```

At a high level, the communication follows this process:

```text
PC-A
 │
 │ 1. Determine destination network
 ▼
IP decision
 │
 │ 2. Send traffic toward gateway
 ▼
Switch-A
 │
 │ 3. Forward Ethernet frame
 ▼
Router
 │
 │ 4. Examine destination IP
 │
 │ 5. Make forwarding decision
 ▼
Switch-B
 │
 │ 6. Forward frame
 ▼
PC-B
```

The return traffic follows the reverse path.

**[SCREENSHOT 7 — PLACE YOUR SUCCESSFUL PING RESULT HERE]**

*Figure 7 — Connectivity test from PC-A to PC-B.*

The important point is that a simple `ping` is not merely a packet moving directly from one computer to another.

It is the result of several networking mechanisms working together.

---

## 8. Observing the Packet Flow

The most useful part of this experiment is not simply checking whether the ping succeeds.

The goal is to observe the components involved in the communication.

During the experiment, I check:

| Component | What to Observe            |
| --------- | -------------------------- |
| PC-A      | IP address and subnet      |
| PC-A      | Default gateway            |
| PC-A      | ARP / neighbor information |
| Switch-A  | MAC address table          |
| Router    | Interface status           |
| Router    | Routing information        |
| PC-B      | IP address and subnet      |
| PC-B      | Default gateway            |
| Network   | ICMP connectivity          |

**[SCREENSHOT 8 — PLACE YOUR PACKET / SIMULATION VIEW HERE, IF AVAILABLE]**

*Figure 8 — Packet flow observed using the network simulation environment.*

---

## 9. Troubleshooting Perspective

Understanding packet flow changes how I approach network problems.

When a ping fails, I do not need to immediately assume that the router is the problem.

Instead, I can break the path into smaller questions:

```text
Ping fails
   │
   ├── Is the IP configuration correct?
   │
   ├── Is the destination in the local network?
   │
   ├── Is the default gateway correct?
   │
   ├── Is ARP resolving correctly?
   │
   ├── Is the switch forwarding the frame?
   │
   ├── Are the router interfaces operational?
   │
   ├── Does the router have a route?
   │
   └── Can the destination host respond?
```

This gives me a more systematic troubleshooting process.

Instead of asking:

> Which device is broken?

I can ask:

> **At which stage of the packet's journey did communication stop?**

That is a much more useful question when troubleshooting networks.

---

## What I Learned

Before following the complete packet flow, concepts such as IP addresses, MAC addresses, ARP, switches, routers, and default gateways can look like separate topics.

After connecting them through a practical network scenario, their relationship becomes clearer.

The overall process can be simplified as:

```text
Host
  ↓
Determine destination network
  ↓
ARP / MAC resolution
  ↓
Ethernet frame
  ↓
Switch
  ↓
Default gateway
  ↓
Router
  ↓
Routing decision
  ↓
Destination network
  ↓
Destination host
```

The main lesson for me is that learning networking should not stop at memorizing definitions.

Understanding **why each component is involved in a communication path** makes it much easier to reason about network behavior and troubleshoot problems.

---

## Conclusion

A simple `ping` between two hosts can involve multiple networking concepts.

The source host uses its IP configuration to determine whether the destination is local or remote. For remote destinations, the host sends traffic toward its default gateway. Switches forward Ethernet frames using MAC addresses, while routers forward packets between different IP networks.

Understanding this packet flow provides a foundation for more advanced networking topics such as subnetting, VLANs, routing protocols, NAT, and network troubleshooting.

The next step in this learning journey is **subnetting**.

Once I understand how packets move between networks, I also need to understand how those networks are divided and how an IPv4 address identifies the network and host portions.

---

## Further Reading

* IPv4 addressing
* ARP
* Ethernet switching
* IP routing
* Default gateways
* ICMP and `ping`

---

## Frequently Asked Questions

### What is a network packet?

A network packet is a unit of data handled at the network layer. In an IP network, the packet contains information such as source and destination IP addresses.

### What is the difference between an IP address and a MAC address?

An IP address provides logical addressing for communication across IP networks, while a MAC address is used for link-layer communication on a local network.

### What does a switch do?

A switch primarily forwards Ethernet frames using MAC address information.

### What does a router do?

A router forwards packets between IP networks based on destination IP addresses and routing information.

### What is a default gateway?

A default gateway is the router address a host uses to forward traffic destined for networks that are not directly local.

### Why is ARP needed?

For IPv4 communication over Ethernet, ARP can resolve a local IPv4 address to the corresponding MAC address needed for frame delivery.

---

*This article is part of my learning journey as a TJKT student, starting from networking fundamentals and progressing toward Linux, containers, monitoring, troubleshooting, and infrastructure.*
