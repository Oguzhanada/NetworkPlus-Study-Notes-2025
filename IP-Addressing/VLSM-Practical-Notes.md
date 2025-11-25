# VLSM Practical Notes

VLSM (Variable Length Subnet Masking) allows you to create subnets of different sizes within the same network.  
Instead of carving every subnet into equal pieces, VLSM lets you design networks based on real requirements.

This is one of the most useful skills in real-world networking and a frequent topic on the Network+ exam.

---

# 📌 What VLSM Actually Is

VLSM is subnetting done more than once.

Example:
Start with a /24 → Subnet into smaller pieces → Take one piece → Subnet it again → Repeat as needed.

This produces:
- A subnet for 50 hosts  
- Another for 20 hosts  
- Another for 6 hosts  
- Another for 2 hosts  

All from the same original network.

---

# 🧩 Key Concepts

### **1. Subnets Do Not Have to Be Equal**
VLSM lets you create:
- A large subnet (e.g., /26)
- Medium subnet (/27)
- Several small subnets (/29, /30)

### **2. Always Assign the Largest Subnets First**
This ensures you don’t paint yourself into a corner.

Order of operations:
1. Largest host requirement  
2. Second largest  
3. Continue downward  
4. Leave small leftovers at the end  

### **3. You Must Avoid Overlapping Subnets**
Each subnet must be calculated carefully so addresses do NOT conflict.

### **4. Same Base Network, Multiple Prefixes**
Example:
All subnets come from 192.168.50.0/24 but have different masks:
- /26  
- /27  
- /28  
- /30  

---

# 🧮 Step-by-Step VLSM Example (Most Useful Section)

You are given:

**Base network:**  
`192.168.10.0/24`

**Requirements:**  
- Subnet A: 50 hosts  
- Subnet B: 20 hosts  
- Subnet C: 10 hosts  
- Subnet D: 2 hosts

---

## ✔ Step 1 — Sort by size (largest first)

| Subnet | Needed Hosts |
|--------|--------------|
| A | 50 |
| B | 20 |
| C | 10 |
| D | 2 |

---

## ✔ Step 2 — Find the correct prefix (mask) for each

### Subnet A (50 hosts)
Need: at least 50  
2^6 = 64 → usable 62  
Mask = /26

### Subnet B (20 hosts)
2^5 = 32 → usable 30  
Mask = /27

### Subnet C (10 hosts)
2^4 = 16 → usable 14  
Mask = /28

### Subnet D (2 hosts)
2^2 = 4 → usable 2  
Mask = /30

---

## ✔ Step 3 — Assign subnets in order

Start from: **192.168.10.0**

### **Subnet A (/26 → block size 64)**
- Network: 192.168.10.0  
- Range: 192.168.10.1 – 62  
- Broadcast: 192.168.10.63  

Next available: **192.168.10.64**

---

### **Subnet B (/27 → block size 32)**
- Network: 192.168.10.64  
- Range: 192.168.10.65 – 94  
- Broadcast: 192.168.10.95  

Next available: **192.168.10.96**

---

### **Subnet C (/28 → block size 16)**
- Network: 192.168.10.96  
- Range: 192.168.10.97 – 110  
- Broadcast: 192.168.10.111  

Next available: **192.168.10.112**

---

### **Subnet D (/30 → block size 4)**
- Network: 192.168.10.112  
- Range: 192.168.10.113 – 114  
- Broadcast: 192.168.10.115  

Next available: **192.168.10.116**

---

# 📋 Final VLSM Table

| Subnet | Mask | Network | First Host | Last Host | Broadcast |
|--------|------|----------|------------|-----------|-----------|
| A | /26 | 192.168.10.0 | .1 | .62 | .63 |
| B | /27 | 192.168.10.64 | .65 | .94 | .95 |
| C | /28 | 192.168.10.96 | .97 | .110 | .111 |
| D | /30 | 192.168.10.112 | .113 | .114 | .115 |

This structure avoids all overlap and fits perfectly into the /24 base network.

---

# 🔧 Troubleshooting VLSM Problems

If a VLSM design fails, the cause is usually:

### ✔ Overlapping subnets  
Ranges accidentally collide.

### ✔ Wrong host calculations  
Forgetting the −2 rule for usable hosts.

### ✔ Not sorting by size  
Starting with small subnets first wastes space.

### ✔ Incorrect block size  
Misreading /27 vs /28 can break configurations.

### ✔ Misaligned networks  
Summaries must start on proper boundaries:  
e.g., /27 must start at multiples of 32.

---

# 🎯 Network+ Exam Tips

The exam loves VLSM questions such as:

- “Create the smallest subnet that supports X hosts.”  
- “Which mask provides at least 50 hosts?”  
- “Given a base network, create multiple subnet sizes.”  
- “Which subnets fit inside a /24 without overlap?”  

Most common trick:
> Giving two host requirements that cannot fit inside the wrong prefix.

Example:
50 hosts cannot fit into /27 → maximum is 30 usable.

---

# 📚 How I Study VLSM

My personal method:

- Always list biggest subnets first  
- Use a table or scratch paper  
- Memorize block sizes for /26–/30  
- Practice 3–5 VLSM problems per day  
- Recalculate ranges in my head to build speed  

Once you do VLSM a few times, the logic becomes second nature.

---

# 🧩 Quick Review Questions

**1. Which prefix supports 20 hosts?**  
→ /27 (30 usable)

**2. Which prefix supports exactly 2 hosts?**  
→ /30

**3. Why start with the largest subnet first?**  
→ Prevent overlap and conserve address space.

**4. What is the block size of /28?**  
→ 16

**5. What happens if two VLSM subnets overlap?**  
→ Routing and addressing fail; devices pick wrong networks.

---

# ✅ Summary

VLSM allows you to create subnets of different sizes based on actual host requirements.  
By sorting subnets from largest to smallest, calculating correct masks, and assigning spaces carefully, you can build efficient, clean, and scalable network designs.

Understanding VLSM is essential for both subnetting mastery and real-world network engineering.
