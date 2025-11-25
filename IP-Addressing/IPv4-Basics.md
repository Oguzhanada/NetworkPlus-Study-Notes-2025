# IPv4 Basics

IPv4 is the foundation of most modern networks.  
Even as IPv6 adoption grows, IPv4 remains everywhere — home networks, enterprise environments, cloud providers, and even many legacy systems.

Understanding IPv4 means understanding how devices identify each other, how networks are divided, and how routing decisions are made.

This note summarizes IPv4 in a simple, practical, exam-focused way.

---

## 📌 What IPv4 Is

IPv4 is a **32-bit addressing system** used to identify devices on a network.  
It represents addresses in dotted decimal format:

Example:  
`192.168.1.10`

32 bits = 4 octets (each 0–255):
`192 . 168 . 1 . 10`


Each octet = 8 bits.

---

## 🧩 Key Concepts

### **1. IPv4 Address Structure**
Every IPv4 address is made of:
- **Network portion** (which network the host belongs to)
- **Host portion** (specific device inside that network)

The subnet mask determines the boundary.

---

### **2. Public vs Private IPv4**

**Private IP ranges** (RFC 1918):

- 10.0.0.0 – 10.255.255.255  
- 172.16.0.0 – 172.31.255.255  
- 192.168.0.0 – 192.168.255.255  

These are used internally, never on the internet.

**Public IPs** → Routable on the internet.

---

### **3. Special IPv4 Address Types**
- **Loopback:** 127.0.0.1  
- **APIPA:** 169.254.0.0/16  
- **Broadcast:** 255.255.255.255  
- **Network address:** (host bits = all 0s)  
- **Directed broadcast:** (host bits = all 1s)

---

### **4. Binary Representation**
IPv4 uses binary underneath:

Example:  
`192` → `11000000`

Binary is essential for subnetting and CIDR calculations.

---

### **5. Classful Addressing (Legacy but exam-relevant)**

| Class | First Octet Range | Default Mask |
|-------|--------------------|---------------|
| A | 1–126 | /8 |
| B | 128–191 | /16 |
| C | 192–223 | /24 |

You’ll still see this in Network+ questions.

---

## 🌐 Real-World Example

Imagine a home network:

- Router LAN IP: `192.168.1.1`
- Laptop: `192.168.1.50`
- Phone: `192.168.1.60`
- Subnet mask: `255.255.255.0`

All devices share the same **/24** network:

`192.168.1.0 – 192.168.1.255`

They communicate locally because:
- Network portion is identical  
- Only host portion differs  

If one device had `192.168.2.50`, it would **not** communicate without a router.

---

## 🔧 Troubleshooting IPv4 Issues

When IPv4 breaks, these are the most common problems:

### ✔ Wrong subnet mask  
Devices fall into different networks accidentally.

### ✔ Wrong default gateway  
You can ping local devices but not the internet.

### ✔ Duplicate IP address  
Two hosts fighting over the same IP → unstable network.

### ✔ APIPA (169.254.x.x)  
DHCP unreachable or misconfigured.

### ✔ DNS misconfigured  
You can ping IPs but not domain names.

### ✔ Wrong static configuration  
Mask, gateway, DNS mismatch.

Whenever IPv4 behaves strangely, I always start by checking the basics:

`ipconfig` / `ifconfig` / `ip a`

---

## 🎯 Exam Tips (Network+)  

- Know private IP ranges — very often tested.  
- Recognize APIPA (169.254.x.x) and what it means (DHCP failure).  
- Classful addressing questions appear frequently.  
- Understand the structure: Network vs Host bits.  
- Know the purpose of loopback (127.0.0.1).  
- DHCP misconfig → APIPA.  
- Subnet masks change the network portion, not the IP itself.

---

## 📚 How I Study This Topic

To really understand IPv4, I usually:

- Convert a few decimal numbers to binary by hand  
- Practice identifying network/host portions  
- Look at real device configs (router, PC, VM)  
- Draw simple network diagrams  
- Play with DHCP and static IPs in a lab  
- Troubleshoot broken IP setups on purpose  

Seeing IPv4 in actual networks makes the theory stick.

---

## 🧩 Quick Review Questions

**1. How many bits does an IPv4 address contain?**  
→ 32 bits

**2. What IP range is APIPA?**  
→ 169.254.0.0/16

**3. Which IP class covers 192.x.x.x?**  
→ Class C

**4. Which IP is loopback?**  
→ 127.0.0.1

**5. Private IP range that starts with 172?**  
→ 172.16.0.0 – 172.31.255.255

---

## ✅ Summary

IPv4 is a 32-bit addressing scheme used across almost all networks today.  
Understanding how IPv4 is structured — public vs private, binary format, special addresses, subnetting basics — is essential for both the Network+ exam and real-world troubleshooting.

This file sets the foundation for the next topics: Subnetting, CIDR, VLSM, and IPv6.

