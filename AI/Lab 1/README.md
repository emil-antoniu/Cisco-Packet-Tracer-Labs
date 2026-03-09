# 🧪 Lab: Small Business Network Setup (CCNA Fundamentals)

## 🏢 Scenario:
You are a network technician hired by a small company to set up their internal LAN and basic routing between departments. The company has two departments:

- **Sales**
- **Engineering**

Each department must be placed in its own VLAN, and devices must not be able to communicate across VLANs unless routed via a router. You’ll use a router-on-a-stick setup to enable inter-VLAN communication.

## 📦 Topology Overview
You will need the following devices in Packet Tracer:

- 1 Router (e.g., Router0)
- 1 Switch (e.g., Switch0)
- 4 PCs (2 per department: PC1, PC2 in Sales, PC3, PC4 in Engineering)

## 🏗️ Step-by-Step Objectives

### 🔹 1. VLAN Configuration
- Create VLAN10 for Sales
- Create VLAN20 for Engineering
- Assign the correct ports to each VLAN:
  - PC1 and PC2 → VLAN10
  - PC3 and PC4 → VLAN20

### 🔹 2. IP Addressing
Assign static IPs:

| Device | IP Address | VLAN | Port |
|:------:|:----------:|:----:|:----:|
| PC1 | 192.168.10.10/24 | VLAN10 | Fa0/1 |
| PC2 | 192.168.10.11/24 | VLAN10 | Fa0/2 |
| PC3 | 192.168.20.10/24 | VLAN20 | Fa0/3 |
| PC4 | 192.168.20.11/24 | VLAN20 | Fa0/4 |
| Router (subinterfaces) | 192.168.10.1/24 (G0/0.10), 192.168.20.1/24 (G0/0.20) | — | Trunk |

### 🔹 3. Switch Setup
- Configure a trunk link from Switch0 to Router0 (Fa0/5)
- Configure the access ports accordingly
- Set native VLAN to 99 (simulate custom setup)

### 🔹 4. Router Setup (Router-on-a-Stick)
Create subinterfaces on the router:

```bash
interface g0/0.10
  encapsulation dot1Q 10
  ip address 192.168.10.1 255.255.255.0

interface g0/0.20
  encapsulation dot1Q 20
  ip address 192.168.20.1 255.255.255.0

interface g0/0.99
  encapsulation dot1Q 99 native
```

## 🔐 Restrictions (Real-World Constraints)
- You are not allowed to use DHCP — IPs must be manually configured.
- VLANs must be clearly named (e.g., `name Sales`, `name Engineering`).
- Trunking must not use default native VLAN 1.
- No direct physical connections between devices of different departments (Sales ↔ Engineering).
- Switch must use descriptive port descriptions.

## ✅ How to Test
Once you've finished setting everything up:

**Ping tests:**
- PC1 ↔ PC2 should succeed
- PC3 ↔ PC4 should succeed
- PC1 ↔ PC3 should fail before router is set up
- After router setup, PC1 ↔ PC3 should succeed

**Verification commands:**
- Use `show vlan brief` on the switch to verify correct port assignments.
- Use `show ip interface brief` on the router to verify subinterface configuration.
- Use `ping` and `tracert` from PCs to ensure correct routing.

