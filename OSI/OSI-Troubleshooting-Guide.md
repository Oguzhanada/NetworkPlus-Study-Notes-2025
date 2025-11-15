# OSI Troubleshooting Guide

One of the easiest ways to troubleshoot networks is by thinking in OSI layers.  
Instead of guessing, I move step-by-step from the Physical layer upward, or from the Application layer downward, depending on where the issue appears.

This guide summarizes how I troubleshoot each OSI layer in real environments and how it applies to the Network+ exam.

---

# 🔽 Bottom-Up Troubleshooting (Layer 1 → Layer 7)

I use this method when **nothing works** or connectivity is completely down.

### Great for:
- No link/no connection
- Hardware failures
- Physical cable or Wi-Fi problems

---

# 🔼 Top-Down Troubleshooting (Layer 7 → Layer 1)

I use this method when **specific applications fail** but the network works.

### Great for:
- DNS issues
- Email not sending
- Website down
- Application errors

---

# 🧩 Layer-by-Layer Troubleshooting

Below is how I diagnose issues at each OSI layer, with exam-focused examples.

---

# 🟪 Layer 1 — Physical Layer

### **Symptoms**
- No link light  
- Cable unplugged/damaged  
- Wi-Fi signal weak  
- Interference  
- Bad connectors  
- SFP module failure  
- Speed/duplex mismatch symptoms

### **Checks**
- Replace cable  
- Try another port  
- Check link LEDs  
- Test with cable tester  
- Check maximum cable distance (100m for copper)

### **Network+ Hint**
Layer 1 problems are VERY common exam questions.

---

# 🟦 Layer 2 — Data Link Layer

### **Symptoms**
- Wrong VLAN  
- Trunk misconfiguration  
- STP blocking  
- MAC table issues  
- CRC errors  
- Duplicate MAC addresses  
- Framing errors

### **Checks**
- Confirm VLAN assignment  
- Check if VLAN allowed on trunk  
- Check MAC table:
- show mac address-table
- Look for port flapping  
- Inspect duplex settings (common cause of CRC errors)

### **Network+ Hint**
If devices are in the same subnet but can’t reach each other → **Layer 2 issue**.

---

# 🟩 Layer 3 — Network Layer

### **Symptoms**
- Wrong gateway  
- No route  
- Overlapping subnets  
- Routing loops  
- Ping fails beyond local network  
- Traceroute stops mid-path

### **Checks**
- Verify IP + subnet mask  
- Check default gateway  
- Check routing table:
- show ip route
- Ping gateway → next hop → remote host  
- Look for asymmetric routing

### **Network+ Hint**
If you can ping locally but not beyond → **Layer 3**.

---

# 🟧 Layer 4 — Transport Layer

### **Symptoms**
- Application slow  
- Port blocked  
- Packet loss  
- Jitter/latency issues  
- Connection reset  
- TCP retransmissions  
- UDP traffic dropping

### **Checks**
- Test port accessibility:
- telnet <ip> <port>
- Check firewall rules  
- Test packet loss (ping)  
- Test latency (ping)  
- Examine TCP/UDP behavior

### **Network+ Hint**
If VoIP is choppy → UDP (Layer 4).

---

# 🟨 Layer 5 — Session Layer

### **Symptoms**
- Random disconnects  
- VPN session drops  
- RDP logouts  
- “Session expired” messages  
- Authentication token failures

### **Checks**
- Check timeout settings  
- Inspect session logs  
- Monitor stability of connection (Layer 3/4)  
- Check application idle timers

### **Network+ Hint**
Session = maintaining communication.

---

# 🟦 Layer 6 — Presentation Layer

### **Symptoms**
- SSL/TLS errors  
- “Connection not private”  
- Corrupted file received  
- Encoding issues (weird characters)  
- JSON/XML parsing failures

### **Checks**
- Check certificates  
- Validate TLS version  
- Check encoding formats  
- Test with plain text tools  
- Ensure compression/encoding correct

### **Network+ Hint**
Encryption lives at **Layer 6**.

---

# 🟪 Layer 7 — Application Layer

### **Symptoms**
- Website won't load  
- DNS not resolving  
- Email not sending  
- HTTP errors (404, 500, 403)  
- API failures  
- Application server misconfig

### **Checks**
- Check DNS: - Test using `curl`  
- Review application logs  
- Verify correct ports (80, 443, 25, 53, etc.)  
- Check credentials/authentication

### **Network+ Hint**
If you can ping by IP but not hostname → **Layer 7 (DNS)**.

---

# 🧭 Putting It All Together — Real Troubleshooting Flow

**Scenario:**  
A user says: “I can connect to Wi-Fi but websites do not load.”

My OSI workflow:

### Layer 1  
Wi-Fi signal strong → OK  

### Layer 2  
Wireless authentication successful → OK  

### Layer 3  
Can they ping gateway? → Yes  
Can they ping 8.8.8.8? → Yes  

### Layer 4  
TCP/UDP fine → OK  

### Layer 7  
DNS failing → Aha  
User can reach IPs but not domain names → **DNS issue**  

Problem solved with a simple DNS fix.

---

# 👨‍🏫 Another Example (Common in Exams)

**Scenario:**  
Workstations in the same VLAN cannot ping each other.

- IPs correct? → Yes  
- Gateway irrelevant (same VLAN)  
- VLAN assignment? → Wrong  
- Layer 2 issue  

Correct answer: **Data Link layer (Layer 2)**.

---

# 🧠 My Personal Study Strategy

To master OSI troubleshooting, I:

- Associate each layer with specific symptoms  
- Memorize what each device does (router, switch, NIC)  
- Practice “OSI mapping” on every problem  
- Review exam-style questions  
- Rebuild failed topologies in Packet Tracer  
- Use Wireshark to see what layer each protocol belongs to  

Over time, OSI-based thinking becomes instinctive.

---

# 🧩 Quick Review Questions

**1. A user cannot reach the default gateway. Which layer is likely failing?**  
→ Layer 3.

**2. CRC errors are found on a switch port. What layer is affected?**  
→ Layer 1/2.

**3. DNS is unreachable, but IP pings work. Which layer?**  
→ Layer 7.

**4. SSL certificate error appears in browser. Which layer?**  
→ Layer 6.

**5. Two hosts in same subnet cannot reach each other. Which layer?**  
→ Layer 2.

---

# ✅ Summary

This OSI troubleshooting guide ties symptoms to the correct layer, making it easier to isolate network problems quickly.  
Whether in an exam or real environment, thinking layer-by-layer gives structure and clarity to complex issues.

Master this flow → troubleshooting becomes predictable.

