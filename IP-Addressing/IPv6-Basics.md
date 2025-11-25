# IPv6 Basics

IPv6 was created to solve a simple but critical problem:  
**the world is running out of IPv4 addresses.**

With billions of devices coming online, IPv6 provides a massively larger address space, improved network capabilities, and a more modern design.  
Even though many organizations still rely on IPv4, IPv6 is becoming increasingly common in enterprise networks, cloud services, and ISPs.

This note explains the fundamentals of IPv6 in a clear, practical way.

---

## 📌 What IPv6 Is

IPv6 is a **128-bit addressing system**, written in hexadecimal and separated by colons.

Example:  
`2001:0db8:85a3:0000:0000:8a2e:0370:7334`

128 bits = **8 groups**, each group containing 16 bits.

Compared to IPv4’s 32-bit system, IPv6 provides more than enough addresses for the foreseeable future.

---

## 🧩 Key Concepts

### **1. Hexadecimal Format**
IPv6 uses hex because binary would be too long and decimal wouldn’t make sense.

Each group (called a *hextet*) represents 16 bits:
`2001 : 0db8 : 0000 : 0000 : 02aa : fff0 : 0120 : 0e1b`

---

### **2. Zero Compression and Shortening Rules**

IPv6 allows you to shorten addresses for readability:

#### ✔ Drop leading zeros:
`02aa` → `2aa`

#### ✔ Use :: to replace one consecutive block of zeros:
`2001:db8:0:0:0:0:2aa:1`  
becomes  
`2001:db8::2aa:1`

⚠ **:: can only appear once** in an address.

---

### **3. Types of IPv6 Addresses**

| Type | Starts With | Purpose |
|------|--------------|--------------|
| **Global Unicast** | 2000::/3 | Public, routable |
| **Link-Local** | fe80::/10 | Required on every interface; non-routable |
| **Unique Local (ULA)** | fc00::/7 | Private IPv6 (similar to RFC1918) |
| **Multicast** | ff00::/8 | Replaces broadcast |
| **Loopback** | ::1 | IPv6 loopback |
| **Unspecified** | :: | “No address” placeholder |

IPv6 **does not use broadcast**, only multicast.

---

### **4. IPv6 Configuration Methods**

- **SLAAC (Stateless Address Autoconfiguration)**  
  Device autogenerates its IPv6 address from router advertisements (RAs).

- **DHCPv6**  
  Similar to DHCP but for IPv6, provides additional options.

- **Static IPv6**  
  Manually assigned.

Most modern devices prefer SLAAC unless DHCPv6 is explicitly used.

---

### **5. ICMPv6 and Neighbor Discovery (ND)**

IPv6 replaces ARP with **Neighbor Discovery (ND)**:
- Router Solicitation (RS)
- Router Advertisement (RA)
- Neighbor Solicitation (NS)
- Neighbor Advertisement (NA)

ICMPv6 is essential — blocking it breaks IPv6.

---

## 🌐 Real-World Example

A typical enterprise network might provide IPv6 like this:

- Global unicast for servers:  
  `2001:db8:4422:10::20`
- Link-local for router interfaces:  
  `fe80::1`
- Clients receiving SLAAC-based addresses:
  `2001:db8:4422:10:abcd:12ff:fe45:7720`

Routers advertise:
- Prefix: `2001:db8:4422:10::/64`
- Default gateway info
- DNS server via RA or DHCPv6

Clients configure themselves automatically — no need for NAT.

---

## 🔧 Troubleshooting IPv6 Issues

### ✔ Link-Local only address (fe80::)
Device didn’t receive a global unicast prefix → check RAs or DHCPv6.

### ✔ Duplicate Address Detection failure
IPv6 performs DAD; if conflict detected, address is not assigned.

### ✔ ICMPv6 blocked
Neighbor Discovery fails → no communication.

### ✔ Missing default gateway
Device can talk locally but not outside subnet.

### ✔ Wrong prefix length
IPv6 heavily relies on /64 for SLAAC — other values can break auto config.

---

## 🎯 Network+ Exam Tips

- Link-local always starts with **fe80::**  
- ::1 is the IPv6 loopback  
- **No broadcast** in IPv6 → multicast instead  
- SLAAC uses **Router Advertisements (RAs)**  
- IPv6 addresses can be shortened but **:: only once**  
- ICMPv6 is critical (ND, RS/RA, etc.)  
- 128-bit addressing = huge space  

Many exam questions revolve around recognizing:
- Address types  
- Shortened address validity  
- SLAAC behavior  
- Link-local troubleshooting  

---

## 📚 How I Study This Topic

To understand IPv6, I like to:

- Practice expanding and compressing IPv6 addresses  
- Configure SLAAC on a lab router and watch RS/RA messages  
- Compare IPv4 ARP vs IPv6 ND  
- Ping using link-local addresses with the interface ID  
- Draw different IPv6 address types (global, ULA, link-local)  

Hands-on practice makes IPv6 feel simple instead of intimidating.

---

## 🧩 Quick Review Questions

**1. How many bits does an IPv6 address have?**  
→ 128 bits

**2. What prefix do link-local addresses use?**  
→ fe80::/10

**3. What replaces broadcast in IPv6?**  
→ Multicast

**4. What is the IPv6 loopback address?**  
→ ::1

**5. Can :: appear twice in an IPv6 address?**  
→ No — only once.

---

## ✅ Summary

IPv6 offers a modern, scalable, and flexible addressing system that solves the limitations of IPv4.  
Understanding its structure, address types, ND behavior, and shortening rules is essential for both real-world networking and the Network+ exam.

This file sets a strong base for deeper topics like **CIDR, VLSM, subnetting, and IPv6 routing**.

