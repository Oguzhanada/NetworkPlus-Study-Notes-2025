# CIDR and Slash Notation

CIDR (Classless Inter-Domain Routing) is one of the most important concepts in modern networking.  
Instead of using rigid class-based addressing (Class A, B, C), CIDR gives us flexible, efficient, and scalable IP addressing.

CIDR is expressed using **slash notation** (also called prefix length):  
- `/24`  
- `/27`  
- `/30`  
- etc.

If subnetting is the “how much space do I need?” question,  
then **CIDR is the “how efficiently can I represent this network?”** answer.

---

# 📌 Why CIDR Exists

Before CIDR, networks used Class A/B/C boundaries:

- Class A → /8  
- Class B → /16  
- Class C → /24  

This caused huge waste.  
Example:  
Needing only 300 hosts forced you to use a Class B network (65,534 hosts).

CIDR fixed this by allowing ANY prefix length (from /1 to /32).

---

# 🧩 Understanding Slash Notation (/ notation)

Slash notation simply tells you **how many bits represent the network portion** of an IP address.

Examples:

- `/24` = 255.255.255.0  
- `/25` = 255.255.255.128  
- `/26` = 255.255.255.192  
- `/27` = 255.255.255.224  
- `/28` = 255.255.255.240  

The remaining bits belong to hosts.

---

# 🎯 CIDR Conversion Table (Most Common Prefixes)

| Prefix | Mask | Hosts |
|--------|--------------|--------|
| /24 | 255.255.255.0 | 254 |
| /25 | 255.255.255.128 | 126 |
| /26 | 255.255.255.192 | 62 |
| /27 | 255.255.255.224 | 30 |
| /28 | 255.255.255.240 | 14 |
| /29 | 255.255.255.248 | 6 |
| /30 | 255.255.255.252 | 2 |
| /32 | Single host route | 1 |

You **don’t** memorize all masks — you memorize the PATTERN.

---

# 🧮 How to Read / Write CIDR Prefixes

## ✔ Step 1 — Look at the prefix length  
Example: `/27`  
Means:
- 27 network bits  
- 5 host bits  

## ✔ Step 2 — Convert to a mask  
Host bits = 5 → 2⁵ = 32 addresses  
Mask = 256 − 32 = 224  
Final mask = **255.255.255.224**

## ✔ Step 3 — Identify the block size  
Block size = 256 − mask_octet  
Block for /27 = 32  
Subnets:

0, 32, 64, 96, 128, 160, 192, 224

---

# 🌐 Real-World Example

An ISP assigns you:

`203.0.113.64/28`

/28 = 16 addresses  
Range breakdown:

- Network ID: 203.0.113.64  
- First Host: 203.0.113.65  
- Last Host: 203.0.113.78  
- Broadcast: 203.0.113.79  

As a network engineer, you might assign:
- Firewall → .65  
- Switch → .66  
- Router → .67  
- Remaining hosts → .68 – .78

CIDR lets you design networks efficiently without wasting space.

---

# 🧠 What CIDR Really Solves

### ✔ 1. IP address waste  
CIDR prevents using a huge block when a small one is enough.

### ✔ 2. Routing table size  
CIDR allows **route summarization**, reducing router workloads.

### ✔ 3. Flexible subnet design  
You can choose ANY prefix length based on actual needs.

---

# 🧩 Route Summarization (Supernetting)

CIDR can combine contiguous networks into a single larger network.

Example:

- 192.168.4.0/24  
- 192.168.5.0/24  
- 192.168.6.0/24  
- 192.168.7.0/24  

All share the first 22 bits.

Summarized route = **192.168.4.0/22**

Routers love summarized routes — it reduces routing table entries.

---

# 🔧 Troubleshooting Tips

CIDR problems often appear as:

### ✔ Wrong mask → Wrong subnet  
Device falls into the wrong broadcast domain.

### ✔ Misaligned summaries  
Route summarization must be aligned (e.g., /22 starts at multiples of 4).

### ✔ Overlapping networks  
CIDR must avoid overlap or routing loops can occur.

### ✔ Host prefix too small  
Example: /29 supports only 6 hosts. Not enough → devices fail to get IP.

---

# 🎯 Network+ Exam Tips

You will definitely see:

- “Which mask corresponds to /26?”  
- “How many hosts does /30 support?”  
- “Which CIDR block summarizes these networks?”  
- “Given an IP and prefix, find broadcast/network ID.”  
- “Choose the right / notation for number of subnets.”

Most common trick:
> Two hosts must communicate without a router — which mask works?

Think: **Make the subnet bigger** (e.g., /23, /22).

---

# 📚 How I Study This Topic

To master CIDR, I usually:

- Practice converting masks to / notation  
- Memorize common prefix lengths (/24–/30)  
- Summarize multiple networks to one prefix  
- Break down complex IP ranges  
- Draw quick subnet tables  

CIDR becomes intuitive with repetition.

---

# 🧩 Quick Review Questions

**1. What is the mask for /26?**  
→ 255.255.255.192

**2. How many hosts does /29 support?**  
→ 6 usable hosts

**3. What is the summary of 10.10.0.0/24 – 10.10.3.0/24?**  
→ 10.10.0.0/22

**4. Block size for 255.255.255.224?**  
→ 32

**5. What prefix has 128 hosts?**  
→ /25

---

# ✅ Summary

CIDR gives us flexible and efficient IP subnetting.  
It replaces rigid class-based networks, reduces waste, and simplifies routing through route summarisation.

Slash notation (/25, /26, /27…) is the key to understanding modern IPv4 network design.

Learning CIDR makes subnetting faster, routing cleaner, and exam questions easier.
