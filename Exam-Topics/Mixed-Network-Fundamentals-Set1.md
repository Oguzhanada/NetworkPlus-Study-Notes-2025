# Mixed Network Fundamentals – Exam Question Set 1

These notes are based on a set of practice questions I solved.  
I wrote them in a way that helps me quickly review the logic behind each answer, not just memorize them.  
They cover topics like cabling, QoS, OSI layers, secure protocols, subnetting, cloud models, and general network design.

---

## 1. Plenum-Rated Cable and Building Codes

When cabling runs through **air-handling spaces** (like above a dropped ceiling used for ventilation), building codes require **plenum-rated cable**.

**Key points I keep in mind:**

- Plenum cable uses **fire-resistant materials**.
- Produces minimal toxic smoke during a fire.
- Approved specifically for **air circulation spaces** (CMP-rated).
- Prevents hazardous fumes from spreading through HVAC systems.

**Why not PVC or standard CAT6?**

- PVC produces toxic fumes and thick smoke.
- CAT6 only tells me the performance category, not the fire rating.

**DAC cables** are just short, pre-terminated switch-to-switch links—not for building infrastructure.

**Exam tip:**  
If I see *“air-handling space”* or *“above ceiling tiles”*, the correct answer is always plenum-rated cable.

---

## 2. QoS (Quality of Service) for Real-Time Traffic

Scenario: VoIP and video calls break during peak congestion.  
To fix this, the network must **prioritize real-time traffic**.

**QoS helps by:**

- Assigning traffic priorities.
- Guaranteeing bandwidth for time-sensitive flows.
- Reducing jitter, delay, and packet loss.
- De-prioritizing bulk traffic like file transfers.

**Not QoS:**

- TTL → hop limit  
- CDN → content distribution  
- VPN → secure tunneling  

**Exam tip:**  
If the question mentions VoIP/video vs email/file transfers, the answer is QoS.

---

## 3. OSI Layer for Encryption/Decryption – Presentation Layer (L6)

If encrypted data arrives but can't be interpreted, the issue is at the **Presentation layer**.

This layer is responsible for:

- Encryption/decryption  
- Compression  
- Encoding/format translation  
- Making sure data is usable by the Application layer  

**Other layers:**

- L7 → services and protocols  
- L5 → session control  
- L4 → segmentation, ports, reliability  

**Exam tip:**  
Keywords like *encryption*, *encoding*, *formatting* → Layer 6.

---

## 4. Replacing Telnet with SSH

Telnet (port 23) sends all data—including passwords—in plaintext.  
The secure replacement is **SSH (port 22)**.

**Why SSH:**

- Encrypts the entire session  
- Protects credentials  
- Standard for secure remote device administration  

**Other protocols:**

- SMTP (25) → email  
- SNMP (161/162) → monitoring  
- HTTP (80) → also plaintext  

**Exam tip:**  
“Remote access in plaintext” or “port 23” → SSH.

---

## 5. Choosing an RFC1918 Range for ~500 Devices

For ~500 hosts, the best option is **192.168.0.0/23**.

- /23 gives **512 total** addresses (510 usable)
- Fits the requirement without wasting space

**Other choices:**

- /24 → 254 hosts → too small  
- 172.16.0.0/16 → way too large  
- 10.0.0.0/8 → extremely oversized  

**Exam tip:**  
“Most appropriate” means *enough IPs, but not excessive waste*.

---

## 6. Creating Four Equal Subnets from a /24

Given: `172.16.20.0/24`  
Needed: **4 equal subnets**

- Borrow 2 bits → `/26`
- Each /26 = **62 usable hosts**

Subnets become:

- 172.16.20.0/26  
- 172.16.20.64/26  
- 172.16.20.128/26  
- 172.16.20.192/26  

**Exam tip:**  
4 equal-sized subnets from /24 → always `/26`.

---

## 7. Multicast for One-to-Many Delivery

If many users must receive **the same data at the same time**, multicast is the efficient option.

**Multicast strengths:**

- One stream → many receivers  
- Works across multiple segments  
- Saves bandwidth  
- Ideal for streaming/video/software distribution  

**Why not others:**

- Unicast → one-to-one  
- Broadcast → local subnet only  
- Anycast → sent to the nearest receiver only  

**Exam tip:**  
“Same data to many users across segments” → multicast.

---

## 8. Zero Trust Architecture (ZTA)

Requirement: **Identity-based access** and **consistent security policies regardless of user location**.

Zero Trust principles:

- Never trust by default  
- Always verify identity  
- Least privilege  
- Same security whether local or remote  

**Why others don't fit:**

- SD-WAN → WAN optimization  
- VXLAN → L2 over L3 tunneling  
- IaC → automation approach  

**Exam tip:**  
If security is based on *identity* rather than *network location*, the answer is ZTA.

---

## 9. Spine-and-Leaf for East–West Traffic

Data centers need fast **east–west** (server ↔ server) communication.

**Spine-and-Leaf provides:**

- Predictable low-latency paths  
- Max two hops anywhere in the fabric  
- High availability  
- Easy horizontal scaling  

Other topologies fall short:

- Three-tier → optimized for north–south  
- Star/hub → bottleneck at the hub  
- Point-to-point → not scalable  

**Exam tip:**  
“Data center” + “east-west traffic” → spine-and-leaf.

---

## 10. PaaS – Managing Only Apps and Data

Requirement:  
Company wants to manage **applications + data only**, not infrastructure or OS.

This matches **PaaS**.

**Provider manages:**

- Servers  
- Storage  
- Networking  
- OS  
- Runtime  

**Customer manages:**

- App code  
- Application data  

**Why not others:**

- IaaS → OS and runtime are customer-managed  
- SaaS → even the app is provider-managed  
- NaaS → only network services  

**Exam tip:**  
“Only manage applications and data” → PaaS.

---

## Quick Review Questions

1. Required cable type for air-handling spaces? → **Plenum-rated cable**  
2. How to prioritise VoIP/video? → **QoS**  
3. Which OSI layer handles encryption/encoding? → **Layer 6 – Presentation**  
4. Secure replacement for Telnet (23)? → **SSH (22)**  
5. Best private range for ~500 hosts? → **192.168.0.0/23**  
6. 4 subnets from /24 → mask? → **/26**  
7. Efficient one-to-many traffic? → **Multicast**  
8. Identity-based security model? → **Zero Trust**  
9. Best topology for east–west traffic? → **Spine-and-Leaf**  
10. Cloud model where I manage only apps/data? → **PaaS**

---

These notes help me quickly review why each answer is correct and remind me of the patterns that tend to repeat in Network+ questions.
