# ARP and Neighbor Discovery

ARP (for IPv4) and Neighbor Discovery (for IPv6) are essential protocols that map IP addresses to MAC addresses.  
Without them, devices wouldn’t know *where* to send frames on the local network.

Even though ARP and ND serve the same purpose, they operate differently and appear frequently in Network+ questions.

This note explains both technologies in a simple, practical way.

---

# 📌 Why We Need ARP and ND

Devices communicate using:
- **IP addresses at Layer 3**
- **MAC addresses at Layer 2**

Before sending a frame on the local network, a device must find the **MAC address** of the destination.

This is where ARP (IPv4) and ND (IPv6) come in.

---

# 🧩 ARP (Address Resolution Protocol) — IPv4

ARP maps IPv4 addresses to MAC addresses.

### ✔ ARP Request (Broadcast)
Device sends:
> “Who has 192.168.1.50? Tell 192.168.1.10.”

Sent to: **FF:FF:FF:FF:FF:FF**

### ✔ ARP Reply (Unicast)
The owner replies:
> “192.168.1.50 is at AA:BB:CC:DD:EE:FF.”

### ✔ ARP Cache
Devices store mappings temporarily in an ARP table.

Command examples:
- `arp -a` (Windows, macOS)
- `ip neigh` (Linux)

---

## 🌐 Gratuitous ARP

A device sends an ARP request for **its own IP**.

Used for:
- Duplicate IP detection  
- Updating other devices’ ARP tables  
- Failover / HA systems (VRRP, HSRP)

---

## 🔥 ARP Spoofing/Poisoning

ARP is insecure — there is no authentication.  
Attackers can send fake ARP replies to redirect traffic.

Example:
- Attacker pretends to be the gateway  
- Victim sends traffic to attacker  
- MitM attack begins  

Security solutions:
- Dynamic ARP inspection (DAI)  
- Port security  
- Static ARP entries  

---

# 🧩 Neighbor Discovery (ND) — IPv6

IPv6 replaces ARP with a more advanced system: **ICMPv6 Neighbor Discovery**.

ND handles:
- MAC address resolution  
- Router discovery  
- Prefix discovery  
- Duplicate address detection (DAD)  
- Neighbor unreachability detection  

---

## ✔ Neighbor Solicitation (NS)
Equivalent of ARP Request (but NOT broadcast).  
Sent to a **multicast** address.

Example:
> “Who has fe80::2aa? Tell fe80::1?”

---

## ✔ Neighbor Advertisement (NA)
Equivalent of ARP Reply.  
Device responds with its MAC address.

---

## ✔ Router Solicitation (RS)
Host asks routers for configuration info.

---

## ✔ Router Advertisement (RA)
Routers provide:
- Prefixes  
- Gateway info  
- DNS servers (optional)  
- SLAAC details  

This is how IPv6 devices autoconfigure themselves.

---

## ✔ Duplicate Address Detection (DAD)

IPv6 checks if an address is already in use **before** assigning it.  
If a conflict is found, the address is not used — preventing collisions.

---

## ✔ No Broadcast in IPv6

Unlike ARP, ND **never** uses broadcast.  
Everything is done through multicast.

This reduces unnecessary LAN traffic.

---

# 🌐 Real-World Example

### IPv4 Example (ARP)
Laptop → wants to reach 192.168.1.20  
Laptop ARPs:  
“Who has 192.168.1.20?”  
Server replies with its MAC.  
Laptop stores entry in ARP cache.

### IPv6 Example (ND)
Laptop → sends Neighbor Solicitation (NS)  
Target: fe80::5  
Server responds with Neighbor Advertisement (NA)  
Laptop stores entry in the neighbor table.

---

# 🔧 Troubleshooting Tips

### ✔ For IPv4:
- Check ARP table: `arp -a`
- Clear ARP cache if entries are wrong
- Look for ARP flooding → possible spoofing
- If gateway can't be reached → ARP may be failing

### ✔ For IPv6:
- Check neighbor table: `ip neigh`
- Make sure ICMPv6 is NOT blocked
- RS/RA messages must pass for SLAAC
- DAD failures indicate address conflicts

### Common symptoms:
- “Cannot reach gateway”
- “Intermittent connectivity”
- Wrong MAC address resolution
- Devices randomly become unreachable

---

# 🎯 Network+ Exam Tips

You will definitely see:

- “What protocol maps IPv4 addresses to MAC addresses?” → **ARP**  
- “What protocol does IPv6 use instead of ARP?” → **Neighbor Discovery**  
- “Which IPv6 message handles router autoconfiguration?” → **RA (Router Advertisement)**  
- “Which mechanism detects IPv6 duplicates?” → **DAD**  
- “What replaces broadcast in IPv6?” → **Multicast**

The exam also likes to test ARP poisoning.

---

# 📚 How I Study This Topic

My strategy:

- Compare ARP vs ND side-by-side  
- Practice ARP commands on real machines  
- Watch RS/RA messages in Wireshark  
- Clear ARP cache and observe new entries  
- Experiment with IPv6 link-local communication  

Hands-on practice makes ARP and ND extremely easy to understand.

---

# 🧩 Quick Review Questions

**1. What does ARP do?**  
→ Maps IPv4 addresses to MAC addresses.

**2. What ICMPv6 message replaces ARP Request?**  
→ Neighbor Solicitation.

**3. What message IPv6 hosts use to discover routers?**  
→ Router Solicitation + Router Advertisement.

**4. Does IPv6 use broadcast?**  
→ No — only multicast.

**5. What is ARP spoofing?**  
→ Attacker sends fake ARP replies to redirect traffic.

---

# ✅ Summary

ARP and Neighbor Discovery are essential for local communication.  
IPv4 uses ARP with broadcasts, while IPv6 uses a more efficient, secure-by-design method with multicast and ICMPv6.

Understanding how both protocols work — and how they fail — is critical for troubleshooting and for the Network+ exam.
