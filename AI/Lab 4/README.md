🧪 **Lab 4: Redundant Switch Topology with STP and Port Security**

---

## 🏢 Scenario
You are a network engineer for a growing office that now wants **network redundancy** to prevent outages. You are tasked with creating a redundant switched network that prevents broadcast storms or loops using **Spanning Tree Protocol (STP)**.

To improve security, you will also configure **Port Security** on the access ports to limit unauthorized devices from accessing the LAN.

---

## 🖥️ Devices Required in Packet Tracer
- 2 Switches (Switch0, Switch1)
- 1 Router (Router0)
- 4 PCs (PC1–PC4)

---

## 🗺️ Topology Overview
- Switch0 and Switch1 are connected to each other
- Switch0 connects to PC1 and PC2
- Switch1 connects to PC3 and PC4
- Router0 is connected to Switch0 (trunk port)

---

## 🧩 Objectives

### 🔹 1. VLAN Configuration
- Create VLAN10 (Sales) and VLAN20 (Engineering)
- Assign:
  - PC1, PC2 → VLAN10 (on Switch0)
  - PC3, PC4 → VLAN20 (on Switch1)

### 🔹 2. STP Redundancy Setup
- Connect Switch0 ↔ Switch1 with 2 crossover links
- Observe how STP blocks one redundant port to prevent loops
- Use `show spanning-tree` to confirm port states

### 🔹 3. Port Security
- Enable port security on all PC-facing switch ports:
  - Limit to 1 MAC address
  - Enable sticky MAC
  - Set violation mode to `restrict`

Example (for Fa0/1):
```bash
interface Fa0/1
 switchport mode access
 switchport port-security
 switchport port-security maximum 1
 switchport port-security mac-address sticky
 switchport port-security violation restrict
```

### 🔹 4. Router-on-a-Stick for Inter-VLAN Routing
- Create subinterfaces on Router0 for VLAN10 and VLAN20:
```bash
interface g0/0.10
 encapsulation dot1Q 10
 ip address 192.168.10.1 255.255.255.0

interface g0/0.20
 encapsulation dot1Q 20
 ip address 192.168.20.1 255.255.255.0
```
- Configure trunk port between Router0 and Switch0

### 🔹 5. IP Addressing
Assign static IPs:

| Device   | IP Address         | VLAN     |
|----------|--------------------|----------|
| PC1      | 192.168.10.10/24   | VLAN10   |
| PC2      | 192.168.10.11/24   | VLAN10   |
| PC3      | 192.168.20.10/24   | VLAN20   |
| PC4      | 192.168.20.11/24   | VLAN20   |

---

## 🔐 Restrictions
- Only 1 MAC per port is allowed (port security)
- Switches must connect redundantly (STP will manage loops)
- No physical connections between PCs of different VLANs

---

## ✅ Testing
1. **Basic Connectivity:**
   - PC1 ↔ PC2 should ping
   - PC3 ↔ PC4 should ping
2. **VLAN Isolation:**
   - PC1 ↔ PC3 should fail (before router setup)
   - After router setup: PC1 ↔ PC3 should ping
3. **Port Security:**
   - Try moving a PC to a different port; verify port security restricts access
4. **STP:**
   - Use `show spanning-tree` on switches to confirm one port is blocked for redundancy

---

## 🧠 Notes
- STP prevents loops by blocking one of the redundant links
- Port Security ensures only authorized PCs are used
- Router-on-a-stick enables inter-VLAN communication over a single trunk link

---
