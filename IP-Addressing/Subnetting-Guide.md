# Subnetting Guide

Subnetting is one of the most fundamental skills in networking.  
It allows you to divide a larger network into smaller, logical segments — improving performance, organization, and security.

A lot of people struggle with subnetting at first, but once you learn the patterns, it becomes predictable and even enjoyable.  
This guide focuses on simple explanations, repeatable methods, and exam-style thinking.

---

## 📌 What Subnetting Actually Is

Subnetting is the process of taking a single IP network and splitting it into multiple smaller networks.

For example:

`192.168.1.0/24`  
can be split into:
- 192.168.1.0/26  
- 192.168.1.64/26  
- 192.168.1.128/26  
- 192.168.1.192/26  

This gives four smaller subnets instead of one big subnet.

---

## 🧩 Key Concepts You Must Know

### **1. Network Bits vs Host Bits**
IPv4 address = 32 bits  
Subnet mask decides how many bits are used for:
- **Network**
- **Host**

Example:  
`255.255.255.0` = `/24`  
Means:
- 24 network bits  
- 8 host bits  

If we “borrow” bits from the host side, we create more subnets.

---

### **2. Borrowed Bits**
Borrowing bits increases the number of subnets and decreases hosts per subnet.

Formula:
- **Number of subnets = 2^borrowed_bits**
- **Hosts per subnet = 2^host_bits − 2**

Example:  
Borrow 2 bits from /24:
- New mask: /26  
- Subnets = 2² = 4  
- Hosts = 2⁶ − 2 = 62 hosts per subnet  

---

### **3. CIDR Slash Notation (/25, /26, /27…)**
CIDR (/ notation) is simply a shorthand for subnet masks.

Examples:
- /24 = 255.255.255.0  
- /25 = 255.255.255.128  
- /26 = 255.255.255.192  
- /27 = 255.255.255.224  
- /28 = 255.255.255.240  

You do NOT need to memorize masks — you only need the pattern.

---

### **4. The “Magic Number” Trick**
Magic number = the block size in the last octet.

Formula:
`256 − subnet_mask_value = block size`


Example:  
Mask = 255.255.255.192 → last octet = 192  
Block size = 256 − 192 = **64**

Subnets:  
0, 64, 128, 192

---

## 🌐 Real-World Example

You are given the network:

`192.168.10.0/24`

You need **4 subnets**.

Borrow 2 bits → /26  
Subnets:

- 192.168.10.0 – 63  
- 192.168.10.64 – 127  
- 192.168.10.128 – 191  
- 192.168.10.192 – 255  

Each subnet has:
- 62 usable hosts  
- A network ID  
- A broadcast address  

This is exactly the type of question Network+ asks.

---

# 🧮 Step-by-Step Subnetting Method (My Personal Method)

Here’s the method I always use during exams:

---

## **Step 1 — Identify the original network**
Example: `192.168.50.0/24`

---

## **Step 2 — Identify how many subnets or hosts you need**

If question says:
- “Need 120 hosts” → work from host bits  
- “Need 8 subnets” → work from borrowed bits  

---

## **Step 3 — Apply formulas**

### ✔ If subnets needed:
2^n ≥ required subnets  
Find n.

### ✔ If hosts needed:
2^h − 2 ≥ required hosts  
Find h.

---

## **Step 4 — Determine new mask**
Old mask + borrowed bits = new mask (/24 → /26)

---

## **Step 5 — Find block size (magic number)**
256 − subnet_mask_value

---

## **Step 6 — List subnets**
Start at 0, add block size each time.

---

## **Step 7 — Identify network ID, usable range, broadcast**

Example for block size = 64:
- Network ID: 192.168.10.64  
- First host: 192.168.10.65  
- Last host: 192.168.10.126  
- Broadcast: 192.168.10.127

---

# 🔧 Subnetting Troubleshooting Tips

If something isn’t working, I check:

### ✔ Host mask mismatch  
Two devices in same subnet *act* like they’re in different networks.

### ✔ Misconfigured gateway  
Great IP, wrong gateway → no external access.

### ✔ Overlapping subnets  
Common error in poorly designed networks.

### ✔ Wrong borrowed-bit calculation  
Subnet size too small → devices can’t fit.

### ✔ Broadcast mismatch  
Especially causes problems in routing and DHCP.

---

# 🎯 Network+ Exam Tips

- Memorize private IP ranges → subnetting frequently appears with these.  
- Know how to calculate number of hosts quickly.  
- Be able to identify valid vs invalid subnets (exam loves this).  
- Know the difference between network ID, usable range, broadcast.  
- APIPA questions usually hint at DHCP/subnet issues.  
- Classful addressing appears in trick questions.  

### The exam LOVES questions like:

> “Two hosts: 192.168.2.50 and 192.168.3.50 need to communicate without a router. Which mask works?”

Answer → **255.255.254.0** (/23)

---

# 📚 How I Study Subnetting

Subnetting becomes easy once you stop memorizing and start pattern-recognition:

- Practice converting masks to slash notation  
- Solve fast block-size questions  
- Write binary for a few examples  
- Draw subnet tables  
- Use Packet Tracer to simulate different subnets  
- Do 10 quick subnetting drills per day — it builds speed  

This is the #1 skill for Network+ exam speed.

---

# 🧩 Quick Review Questions

**1. How many subnets does borrowing 3 bits from /24 create?**  
→ 2³ = **8 subnets**

**2. How many hosts does a /26 support?**  
→ 2⁶ − 2 = **62 hosts**

**3. What is the block size for 255.255.255.224?**  
→ 256 − 224 = **32**

**4. Is 192.168.1.130 valid in the subnet 192.168.1.128/26?**  
→ Yes (usable range: 129–190)

**5. What is the broadcast of 10.0.8.0/21?**  
→ 10.0.15.255

---

# ✅ Summary

Subnetting allows you to divide networks into structured, efficient segments.  
By understanding network/host bits, CIDR notation, magic numbers, and subnet ranges, you can quickly identify valid subnets and design scalable networks.

Subnetting becomes easy with practice — and it is one of the most important skills for both real-life networking and the Network+ exam.
