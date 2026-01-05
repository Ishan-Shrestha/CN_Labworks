# CN_Labworks

---

# Lab 03: Dynamic Routing Configurations (RIP & EIGRP)

## Overview

This lab focuses on implementing dynamic routing protocols within a complex network topology. We explored two primary Distance Vector protocols: **RIP (Routing Information Protocol)** and **EIGRP (Enhanced Interior Gateway Routing Protocol)** to enable communication across multiple subnets.

## Network Topology

The setup consists of the following components for each model:

* **3 Routers:** Serving as the Layer 3 gateways.
* **3 Switches:** Providing Layer 2 connectivity for each local network.
* **3 PCs:** End devices used to verify end-to-end connectivity.
* **1 Laptop:** Used specifically in the RIP configuration to perform **Console Configuration** on Router 0.

## Key Configurations

### 1. RIP (Routing Information Protocol)

In this section, we configured RIP to allow routers to share their routing tables automatically.

* **Console Access:** Router 0 was configured using a Laptop via a **Console Cable** to simulate a real-world physical connection.
* **Routing Table:** Used `router rip` and `network` commands to advertise subnets.

### 2. EIGRP (Enhanced Interior Gateway Routing Protocol)

We implemented EIGRP as a more advanced alternative to RIP.

* **Autonomous System (AS):** All routers were assigned the same AS number to establish adjacency.
* **Convergence:** Observed faster convergence times compared to RIP.

## Verification

To ensure the configurations were successful, the following steps were taken:

1. **Ping Test:** Successful pings between PCs in different networks (e.g., PC0 in Network A to PC2 in Network C).
---

# Lab 3(C): Dynamic Routing with OSPF (Single Area)

## Overview

This lab demonstrates the configuration of **Open Shortest Path First (OSPF)**, a Link-State routing protocol. Unlike RIP or EIGRP, OSPF uses the Shortest Path First (SPF) algorithm to build a complete map of the network topology, ensuring high efficiency and fast convergence in complex environments.

## Network Topology

To study OSPF behavior in its purest form, this topology eliminates switches and uses direct cabling:

* **3 Routers:** Interconnected via **Serial DCE** cables (Red cables with clock symbols).
* **3 PCs:** Each PC is connected directly to its respective Router’s GigabitEthernet port using a **Copper Cross-Over** cable (Black dashed line).
* **Clock Rate:** Since Serial DCE cables are used, clocking was manually configured on the DCE side of each link.

## Key Configurations

### 1. Router-to-Router (Serial DCE)

The routers communicate over a  subnet.

* **Note:** The `clock rate 64000` command was applied to the DCE interface to synchronize data transmission.

### 2. Router-to-PC (Direct Cross-Over)

Because there are no switches, a **Cross-Over cable** is required to connect the Router's NIC to the PC's NIC. This simulates a direct point-to-point connection between a gateway and a host.

### 3. OSPF Protocol Setup

We utilized **OSPF Process ID 1** and placed all networks into **Area 0** (the backbone area).

```bash
Router(config)# router ospf 1
Router(config-router)# network 192.168.1.0 0.0.0.255 area 0
Router(config-router)# network 10.0.0.0 0.0.0.3 area 0

```

* **Wildcard Masks:** Used `0.0.0.255` for LANs and `0.0.0.3` for Serial links to precisely define participating interfaces.

## Verification & Troubleshooting

The following commands were used to verify that the Link-State Database (LSDB) was synchronized:

* **`show ip ospf neighbor`**: Confirmed that routers established Full Adjacencies.
* **`show ip route`**: Verified that routes learned via OSPF are marked with the code **`O`**.
* **`ping`**: Tested end-to-end connectivity from PC0 to PC2 across multiple router hops.

---
