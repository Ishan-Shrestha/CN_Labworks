# CN_Labworks

---

# Lab 03: Dynamic Routing Configurations (RIP & EIGRP)

## 📌 Overview

This lab focuses on implementing dynamic routing protocols within a complex network topology. We explored two primary Distance Vector protocols: **RIP (Routing Information Protocol)** and **EIGRP (Enhanced Interior Gateway Routing Protocol)** to enable communication across multiple subnets.

## 🛠️ Network Topology

The setup consists of the following components for each model:

* **3 Routers:** Serving as the Layer 3 gateways.
* **3 Switches:** Providing Layer 2 connectivity for each local network.
* **3 PCs:** End devices used to verify end-to-end connectivity.
* **1 Laptop:** Used specifically in the RIP configuration to perform **Console Configuration** on Router 0.

## 🚀 Key Configurations

### 1. RIP (Routing Information Protocol)

In this section, we configured RIP to allow routers to share their routing tables automatically.

* **Console Access:** Router 0 was configured using a Laptop via a **Console Cable** to simulate a real-world physical connection.
* **Routing Table:** Used `router rip` and `network` commands to advertise subnets.

### 2. EIGRP (Enhanced Interior Gateway Routing Protocol)

We implemented EIGRP as a more advanced alternative to RIP.

* **Autonomous System (AS):** All routers were assigned the same AS number to establish adjacency.
* **Convergence:** Observed faster convergence times compared to RIP.

## 🧪 Verification

To ensure the configurations were successful, the following steps were taken:

1. **Ping Test:** Successful pings between PCs in different networks (e.g., PC0 in Network A to PC2 in Network C).

## 📂 Files in this Repository

* `RIP.pkt`: The Packet Tracer file for the RIP setup.
* `EIGRP.pkt`: The Packet Tracer file for the EIGRP setup.

---