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
show ip route

### **5. Use Traceroute**
Find the hop where packet disappears.

### **6. Check ACLs / firewalls**
Routing might be correct, but traffic blocked.

---

## 🎯 Network+ Exam Tips

- Know the difference between **routing vs switching**  
- Understand how default gateways work  
- Recognize common routing problems  
- Understand static vs dynamic routing  
- ICMP roles (ping, unreachable, TTL exceeded)  
- Path selection concepts like metrics and AD  
- CIDR + subnetting (heavily tested)  

The exam loves questions like:
> “Host A can reach Host B’s network but Host B cannot reach Host A.”

(Solution: missing return route)

---

## 👨‍🏫 Realistic Scenario (Memory Anchor)

**Scenario:**  
A user can access local servers but not anything on the internet.

My thought process:
1. They can reach LAN resources → Layer 2 OK  
2. They can’t go outside → Layer 3 problem  
3. Check their gateway → wrong  
4. Fix gateway → internet restored  

Simple but extremely common.

---

## 📝 How I Study This Layer

My approach:
- Draw small topologies and practice routing flow  
- Manually calculate subnets  
- Practice traceroute analysis  
- Build static and OSPF labs in Packet Tracer  
- Break routes on purpose to see real errors  

The more routing failures I see, the easier this layer becomes.

---

## 🧩 Quick Review Questions

**1. What device operates at Layer 3?**  
→ Router.

**2. What does a router do if no route matches a packet?**  
→ Drops packet (or uses default route).

**3. What protocol reports “Destination Unreachable”?**  
→ ICMP.

**4. Difference between static and dynamic routing?**  
→ Static is manual, dynamic is learned automatically.

**5. What does TTL prevent?**  
→ Routing loops.

---

## ✅ Summary

Layer 3 connects different networks, assigns IP addressing, and handles packet routing.  
Without this layer, communication would be limited to a single LAN.  
A strong understanding of Layer 3 is essential for troubleshooting, exams, and real-world networking.

