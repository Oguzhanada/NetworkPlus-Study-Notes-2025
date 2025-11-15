# Layer 3 — Network Layer (OSI)

Layer 3 is where **routing**, **logical addressing (IP)**, and **path selection** happen.  
Compared to Layer 1 and 2, this layer decides *where* data should go across different networks.

If Layer 2 delivers frames inside a LAN,  
Layer 3 delivers packets **between** networks.

This is one of the most important layers for the Network+ exam.

---

## 🌍 What Layer 3 Does

The Network layer is responsible for:

- IP addressing (IPv4 and IPv6)
- Routing packets between networks
- Selecting the best path (metrics, routing decisions)
- Fragmentation / MTU checks
- Logical network segmentation
- Handling unreachable networks (ICMP messages)

**Core Layer 3 Protocols:**
- **IPv4**
- **IPv6**
- **ICMP** (ping, destination unreachable)
- **ARP** (between L2/L3 boundary)
- **Routing protocols** (OSPF, RIP, BGP, EIGRP)

---

## 🧭 IP Addressing (The Heart of Layer 3)

Layer 3 uses **logical addresses** (IP addresses) to identify devices.

### IPv4 Example:
`192.168.1.10/24`

Includes:
- Network portion  
- Host portion  
- Subnet mask  
- Broadcast address  

### IPv6 Example:
`2001:db8:abcd::1/64`

IPv6 solves IPv4 exhaustion and simplifies routing with more hierarchical addressing.

---

## 🧭 Routers at Layer 3

Routers are the main devices that operate at this layer.

What a router does:
1. Looks at the **destination IP** inside a packet  
2. Checks its **routing table**  
3. Chooses the best route  
4. Forwards the packet to the next hop  
5. Drops it & sends ICMP if no route exists  

Routers **do not** forward broadcast frames — switches do.

---

## 📝 The Routing Table

A routing table contains:

- Destination network  
- Next-hop IP  
- Outgoing interface  
- Metric (cost of the path)  
- Administrative Distance (trust level of the route)  
- Route type (static, connected, learned by protocol)

Example entry:
- 10.10.10.0/24 via 192.168.1.1, GigabitEthernet0/1

If no match is found → router uses the **default route** (`0.0.0.0/0`).  
If default route doesn’t exist → packet is dropped.

---

## 📡 Routing Methods

### **1. Static Routing**
- Manually configured  
- Zero overhead  
- Good for small networks  
- Not scalable  

### **2. Dynamic Routing**
Routers learn networks automatically:
- **OSPF** (Link-state)  
- **RIPv2** (Distance vector)  
- **EIGRP** (Cisco hybrid)  
- **BGP** (Internet backbone)

Dynamic protocols:
- Adjust when links fail  
- Share route updates  
- Provide load balancing  

---

## 🧩 Layer 3 Packet Structure

An IPv4 packet contains:

- Version  
- Header Length  
- Total Length  
- TTL  
- Source IP  
- Destination IP  
- Protocol (TCP/UDP/ICMP)  
- Payload  

Key exam point:  
Layer 3 uses **packets** (not frames, not segments).

---

## ⚠️ Common Layer 3 Issues

These are problems I see often in labs and real networks:

- Wrong default gateway  
- Incorrect subnet mask  
- Missing route on router  
- Overlapping subnets  
- Routing loop  
- Asymmetric routing  
- TTL expired  
- Incorrect static route  

Example:  
If I can ping the gateway but not beyond, the routing table is usually wrong.

---

## 🧪 How I Troubleshoot Layer 3 Problems

My personal process:

### **1. Check IP + Subnet Mask**
If mask is wrong → device will think it’s on the wrong network.

### **2. Check Default Gateway**
Most “I can only ping local devices” issues come from this.

### **3. Ping Step-by-Step**
- Ping own IP  
- Ping gateway  
- Ping next hop  
- Ping destination  

Where ping fails tells me which hop is broken.

### **4. Check Routing Table**
