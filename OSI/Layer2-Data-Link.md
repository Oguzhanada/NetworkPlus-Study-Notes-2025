# Layer 2 — Data Link Layer (OSI)

Layer 2 is where frames, MAC addresses, and switching come into play.  
If Layer 1 is the road wires, connectors, and signals, then Layer 2 is the system that decides **which direction on the road the traffic should go** on a local network.

This layer is critical because most LAN issues (especially VLAN problems and switching problems) start here.

---

## 🔍 What Layer 2 Actually Does

The Data Link layer is responsible for:

- Creating **frames**  
- Using **MAC addresses** to forward frames  
- Handling **error detection** (CRC)  
- Managing **VLAN tags** (802.1Q)  
- Building and maintaining **MAC address tables**  
- Providing **reliable local delivery** inside the same LAN segment  

Layer 2 does NOT understand IP addresses, routing, or ports — that’s Layer 3 and above.

Its job is:  
> “Deliver frames within the same Layer 2 domain.”

---

## 🧩 Sublayers of Layer 2

Layer 2 is split into two sublayers:

### **1. LLC (Logical Link Control)**
- Controls communication with upper layers  
- Handles flow control  
- Manages error checking  
- Identifies which protocol (IP, ARP, IPv6) is inside the frame  

### **2. MAC (Media Access Control)**
- Responsible for physical addressing  
- Determines how frames get onto the medium  
- Manages MAC addresses and access to the network  
- Performs CSMA/CD (legacy Ethernet)  

Most Network+ exam questions about Layer 2 refer to the **MAC sublayer**.

---

## 🔢 MAC Addresses (What I Must Remember)

A MAC address is:
- **48-bit**
- **Hexadecimal**
- Assigned to NIC by manufacturer
- Unique on the local network

Format:  
`AA:BB:CC:DD:EE:FF`

The first 3 bytes = **OUI** (vendor ID)  
The last 3 bytes = device-specific identifier

Layer 2 uses MAC addresses to forward frames inside the same network segment.

---

## 🧱 Switches at Layer 2

Switches are the main devices operating at Layer 2.  
They maintain a **MAC address table** to know which port a device lives on.

### How a switch learns MACs:
1. Reads the **source MAC** of incoming frames  
2. Records the MAC and port  
3. Builds a table that maps MAC → Port  

### How a switch forwards:
- If destination MAC is known → **unicast** frame  
- If unknown → **flood** frame  
- If broadcast → send to all ports except incoming  
- If multicast → processed based on IGMP/registered groups  

---

## 🏷 VLAN Tags (802.1Q)

VLANs are a **Layer 2 segmentation method**.

Layer 2 frames can include a VLAN tag:
- Identifies the VLAN ID (1–4094)
- Added only on **trunk ports**
- Not present on access ports

VLANs create separate broadcast domains.

Example:  
VLAN 10 and VLAN 20 cannot talk without a router or Layer 3 switch.

---

## 📉 Layer 2 Error Detection (CRC)

Layer 2 performs **error detection**, not correction.

- CRC = Cyclic Redundancy Check  
- It checks frame integrity  
- If the CRC doesn’t match → frame is dropped  

A high CRC count usually means:
- Bad cable  
- Interference  
- Duplex mismatch  
- Damaged NIC  

---

## 🌐 Layer 2 Addressing and Frame Structure

A standard Ethernet frame includes:

- Destination MAC  
- Source MAC  
- Optional 802.1Q VLAN tag  
- EtherType (IPv4, ARP, IPv6)  
- Payload  
- FCS (Frame Check Sequence)

Remember:  
Layer 2 only cares about **MAC + Frames**.

---

## ⚠️ Common Layer 2 Issues

These are frequent real-world problems:

- Wrong VLAN assignment  
- Trunk port missing VLANs  
- Duplicate MAC addresses  
- MAC table overflow  
- STP blocking  
- Switch loops  
- CRC errors  
- Duplex mismatches (Half vs Full)  

If pings fail only between specific VLANs → check Layer 2.

---

## 🧪 How I Troubleshoot Layer 2 Issues

My personal checklist:

1. **Check VLANs**  
   - Is the port in the correct VLAN?  
   - Does the switch trunk allow that VLAN?

2. **Verify MAC address table**  

-show mac address-table
- Is the destination MAC learned on the expected port?

3. **Look for loops**  
- STP blocking?  
- Ports flapping?

4. **Check duplex settings**  
- Auto/auto is usually safe  
- Mismatched duplex causes CRC errors

5. **Examine trunk ports**  
- Native VLAN mismatches are common

6. **Check for MAC flapping**
- Could indicate switching loops or bad cabling

---

## 🎯 Network+ Exam Tips

- Know the purpose of **LLC vs MAC sublayers**  
- Understand how switches learn MAC addresses  
- VLANs = Layer 2 segmentation  
- 802.1Q = VLAN tagging standard  
- STP prevents loops (Layer 2!)  
- Most LAN issues are Layer 2 issues  
- CRC errors = Layer 1/2 problem  
- Duplex mismatch → slow network  

The exam *loves* asking questions about VLANs and switch behavior.

---

## 👨‍🏫 Example Scenario (Memory Aid)

**Scenario:**  
Two computers in the same office cannot ping each other, but they both ping the internet.

**My thought process:**  
- If both can reach the router, Layer 3 is OK  
- If they can’t reach each other, they’re probably in **different VLANs**

This is almost always a Layer 2 misconfiguration.

---

## 📝 How I Study This Topic

To understand Layer 2 deeply, I like to:

- Draw simple switch diagrams  
- Practice tagging/untagging VLANs  
- Play with trunk/access ports in Packet Tracer  
- Check MAC tables regularly  
- Force duplex mismatches to see real errors  

Hands-on practice makes Layer 2 much easier to remember.

---

## 🧩 Quick Review Questions

**1. Which OSI layer uses MAC addresses?**  
→ Layer 2.

**2. What does a switch do if a destination MAC is unknown?**  
→ Floods the frame.

**3. What protocol adds VLAN tags to frames?**  
→ 802.1Q.

**4. What is CRC used for?**  
→ Error detection.

---

## ✅ Summary

Layer 2 is where switches, MAC addresses, VLANs, and frame forwarding live.  
Most LAN problems — especially VLAN issues, MAC conflicts, and duplex mismatches — come from this layer.

Mastering Layer 2 makes troubleshooting faster and helps build a strong foundation for the exam.
