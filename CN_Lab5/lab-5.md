# Lab 05: Network Security & Multi-User Collaboration

## Overview

This lab integrates three core networking concepts:

1. **Multi-User (PTMP):** Establishing a Peer-to-Peer connection between two separate Packet Tracer instances to simulate a collaborative environment.
2. **Static Routing:** Manually defining paths between two routers managed by different peers.
3. **Standard ACLs:** Implementing security policies to deny specific host access across the peering link.

## Network Topology & Addressing

The environment consists of two peer networks connected via a Multi-User link on the `Gig0/1` interfaces.

| Device | Interface | IP Address | Default Gateway | Peer Assignment |
| --- | --- | --- | --- | --- |
| **PC 1** | FastEthernet0 | 192.168.1.100 | 192.168.1.1 | Peer 1 |
| **PC 2** | FastEthernet0 | 192.168.3.2 | 192.168.3.1 | Peer 2 |
| **PC 3** | FastEthernet0 | 192.168.3.3 | 192.168.3.1 | Peer 2 |
| **Router 0** | Gig0/1 (WAN) | 192.168.2.1 | N/A | Peer 1 |
| **Router 1** | Gig0/1 (WAN) | 192.168.2.2 | N/A | Peer 2 |

## Key Configurations

### 1. Multi-User (PTMP) Setup

To bridge the two separate lab files, the following was performed:

* **Peer 1 (Listener):** Enabled the Multi-User agent to "Listen" for incoming connections on port 38000.
* **Peer 2 (Client):** Used the Multi-User Cloud tool to "Connect" using Peer 1's physical IP address.
* The link was established using a standard cross-router cable configuration once the peering handshake was successful.

### 2. Static Routing Table

To enable end-to-end connectivity, static routes were added to each router's routing table.

| Router | Destination Network | Subnet Mask | Next Hop (Gateway) |
| --- | --- | --- | --- |
| **Router 0** | 192.168.3.0 | 255.255.255.0 | 192.168.2.2 |
| **Router 1** | 192.168.1.0 | 255.255.255.0 | 192.168.2.1 |

### 3. Access Control List (ACL) Table

A security policy was implemented on **Router 0** to block **PC 3** from reaching Network 1, while allowing **PC 2** and all other traffic.

| ACL Line | Action | Source IP | Wildcard Mask | Application Interface |
| --- | --- | --- | --- | --- |
| **Line 1** | `deny` | 192.168.3.3 | 0.0.0.0 | Gig0/0 (Outbound) |
| **Line 2** | `permit` | `any` | `any` | Gig0/0 (Outbound) |

## Verification

Verification was performed using the Packet Tracer Simulation mode and Command Prompt:

1. **Multi-User Link:** Verified the Multi-User port status as "Connected" and "Active."
2. **Connectivity Test (Permitted):** PC 2 (`192.168.3.2`) successfully pinged PC 1 (`192.168.1.100`).
3. **Security Test (Denied):** PC 3 (`192.168.3.3`) attempted to ping PC 1. The router dropped the packets, returning a **"Destination host unreachable"** message.
4. **ACL Statistics:**
* Command: `show access-lists`
* Result: Verified "matches" on the deny line for IP 192.168.3.3.