# IP Addressing Troubleshooting Guide

Most network problems begin with addressing issues.  
Incorrect masks, wrong gateways, duplicate IPs, or DNS errors can break communication instantly.  
Knowing how to troubleshoot IP addressing step-by-step is one of the most valuable skills for both the Network+ exam and real-world work.

This guide summarizes how I diagnose IP problems in a clear, reliable, repeatable way.

---

# 📌 The Big Picture

When IP communication fails, the issue usually comes from:

1. Wrong IP address  
2. Wrong subnet mask  
3. Wrong default gateway  
4. DHCP failure (APIPA)  
5. DNS issues  
6. Duplicate IP address  
7. Wrong static configuration  
8. IPv6 misconfiguration (prefix, RA, ND)  

By checking these in order, you can solve 90% of network issues quickly.

---

# 🧩 Common IPv4 Addressing Issues & Fixes

## ✔ 1. Wrong IP Address
A device assigned to the wrong network will not communicate with local hosts.

Example:  
You expect: `192.168.1.x`  
But device has: `192.168.2.x`

**Fix:** Assign correct IP, check DHCP scope, verify VLAN.

---

## ✔ 2. Wrong Subnet Mask
Mask determines which devices are “local.”  
A wrong mask makes devices think they’re on different networks.

Example:  
- Host A: 192.168.1.50 /24  
- Host B: 192.168.1.60 /16  

Host B thinks Host A is local, Host A thinks B is remote → one-way communication issues.

**Fix:** Match subnet masks on all local hosts.

---

## ✔ 3. Wrong Default Gateway
Device can talk locally but not outside its subnet.

Symptoms:
- Ping gateway fails  
- Internet unreachable  
- “No route to host” errors

**Fix:**  
- Set gateway to the router IP in the same subnet  
- Ensure gateway’s interface is up

---

## ✔ 4. DHCP Problems → APIPA
If a system cannot reach the DHCP server, it assigns itself:

`169.254.x.x`

Symptoms:
- Local communication only if other APIPA devices exist  
- No internet  
- Router unreachable  

**Fix:**  
- Check DHCP server  
- Check scopes  
- Check VLAN  
- Ensure DHCP relay is configured if needed  
- Check switch port (blocked, wrong VLAN)

---

## ✔ 5. Duplicate IP Address
Happens when two devices use the same static IP.

Symptoms:
- IP conflict warnings  
- Random disconnects  
- ARP table instability  
- Flapping connectivity  

**Fix:**  
- Identify duplicate  
- Use DHCP reservation  
- Assign unique static IPs  
- Clear ARP cache

---

## ✔ 6. DNS Issues
Device can reach IPs but not domain names.

Example:
`ping 8.8.8.8` → works  
`ping google.com` → fails

**Fix:**  
- Set correct DNS server  
- Check DNS service  
- Try `nslookup`  
- Ensure router passes DNS traffic

---

## ✔ 7. Wrong Static Configuration
Wrong:
- IP  
- Mask  
- Gateway  
- DNS  
breaks communication.

**Fix:**  
- Cross-check addressing plan  
- Match gateway with network ID  
- Ensure DNS is reachable  
- Avoid typos (common!)

---

# 🧩 IPv6 Addressing Issues & Fixes

### ✔ Link-Local Only (fe80::)
Means device did NOT receive a global unicast address.

**Fix:**  
- Ensure RAs are being sent  
- Check router's IPv6 config  
- Verify DHCPv6 if used  

---

### ✔ Duplicate Address Detection (DAD) Failure
IPv6 prevents duplicate addresses automatically.

**Fix:**  
- Reassign IPv6 address  
- Check ND table  
- Fix misconfigured static addresses  

---

### ✔ ICMPv6 Blocked
IPv6 **depends** on ICMPv6 (for SLAAC, ND, RS/RA).  
Blocking it breaks all IPv6 communication.

**Fix:**  
- Allow ICMPv6 in firewall  
- Ensure Neighbor Discovery messages pass

---

### ✔ Wrong Prefix Length
Most enterprise networks use `/64`.  
Using anything else breaks SLAAC.

**Fix:**  
- Set prefix to /64 unless there is a specific design reason

---

# 🔧 Step-by-Step Troubleshooting Workflow (My Personal Method)

This is the exact flow I use in interviews and real jobs:

---

## **Step 1 → Check local IP configuration**
Commands:
- Windows: `ipconfig`  
- Linux/macOS: `ip a`

Verify:
- IP  
- Mask  
- Gateway  
- DNS  
- DHCP vs static

---

## **Step 2 → Ping yourself**
`ping 127.0.0.1`  
If this fails → NIC or OS issue.

---

## **Step 3 → Ping your own IP**
Confirms interface is functioning.

---

## **Step 4 → Ping default gateway**
If gateway unreachable → local network issue.

---

## **Step 5 → Ping remote IP**
If external unreachable but gateway reachable → routing issue.

---

## **Step 6 → Test DNS**
`ping 8.8.8.8`  
`ping google.com`

If IP works but name doesn’t → DNS problem.

---

## **Step 7 → Check ARP or ND**
IPv4:
`arp -a`

IPv6:
`ip neigh`

Incorrect entries mean MAC resolution problems.

---

## **Step 8 → Check switch port / VLAN**
Symptoms of wrong VLAN:
- DHCP not working  
- Can’t reach gateway  
- Can only reach devices in same VLAN  

---

# 🎯 Network+ Exam Tips

These appear VERY often:

- APIPA = DHCP failure  
- “Can ping IP but not name” = DNS problem  
- Wrong mask = weird communication issues  
- Wrong gateway = no internet  
- Duplicate IP = instability  
- Link-local only = IPv6 misconfigured or missing RA  
- “Which device assigns IPs?” → DHCP server  
- “Which port does DHCP use?” → UDP 67/68  
- “Which protocol maps IP to MAC?” → ARP

If you see 169.254.x.x → answer is ALWAYS “DHCP unreachable”.

---

# 📚 How I Study IP Troubleshooting

My routine:

- Break networks on purpose in lab  
- Practice with DHCP on/off  
- Manually misconfigure masks to see symptoms  
- Use Wireshark to watch ARP and ND  
- Try IPv6 SLAAC and observe RAs  
- Solve 5–10 quick troubleshooting questions daily  

Hands-on training builds intuition faster than memorizing theory.

---

# 🧩 Quick Review Questions

**1. What does an APIPA address indicate?**  
→ DHCP server unreachable.

**2. A device can ping IPs but not domain names. What failed?**  
→ DNS.

**3. Two hosts can’t communicate even though they’re in the same /24. Why?**  
→ Different subnet masks.

**4. IPv6 device only has fe80::. Why?**  
→ No RA / no global unicast prefix.

**5. Cannot reach gateway but can reach local devices. Cause?**  
→ Wrong gateway or gateway down.

---

# ✅ Summary

IP addressing issues are among the most common network problems.  
By checking the basics — IP, mask, gateway, DNS, ARP/ND, DHCP — you can pinpoint failures quickly and systematically.

Mastering this flow makes both the exam and real-world troubleshooting much easier.
