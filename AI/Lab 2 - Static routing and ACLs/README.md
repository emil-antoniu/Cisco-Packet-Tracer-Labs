# 🧪 Lab 2: Inter-Branch Routing with Access Control (CCNA Fundamentals)

## 🏢 Scenario
You work for a company that has two small branches: **Branch A** and **Branch B**.
Each branch has its own router and internal PCs. You need to set up communication between the branches **using static routing**.
Additionally, management requests that **only Branch A should initiate pings to Branch B**, but not the other way around.
You'll enforce this using an **Access Control List (ACL)**.


## 🛋 Topology Overview
You will need the following devices in Packet Tracer:

- 2 Routers (e.g., RouterA and RouterB)
- 2 Switches (SwitchA and SwitchB)
- 4 PCs (2 per branch)


```
[PC1]---[SwitchA]---[RouterA]---[RouterB]---[SwitchB]---[PC3]
[PC2]                                                   [PC4]
```


## 🛠️ Step-by-Step Objectives

### 🔹 1. Basic Device Setup
- Assign hostnames to each device (RouterA, RouterB, SwitchA, SwitchB).


### 🔹 2. IP Addressing Plan

| Device        | Interface  | IP Address         | Subnet Mask       |
|---------------|------------|--------------------|-------------------|
| RouterA (LAN) | G0/0        | 10.10.10.1          | 255.255.255.0     |
| RouterA (WAN) | G0/1        | 192.168.1.1         | 255.255.255.252   |
| RouterB (WAN) | G0/1        | 192.168.1.2         | 255.255.255.252   |
| RouterB (LAN) | G0/0        | 10.20.20.1          | 255.255.255.0     |
| PC1           | NIC         | 10.10.10.10         | 255.255.255.0     |
| PC2           | NIC         | 10.10.10.11         | 255.255.255.0     |
| PC3           | NIC         | 10.20.20.10         | 255.255.255.0     |
| PC4           | NIC         | 10.20.20.11         | 255.255.255.0     |

- Default gateways:
  - PC1 & PC2: `10.10.10.1`
  - PC3 & PC4: `10.20.20.1`


### 🔹 3. Switch Setup
- Connect PCs to Switches.
- Connect Switches to Router LAN interfaces.
- No VLAN configuration needed (flat network per branch).


### 🔹 4. Router Configuration
- Configure IP addresses on all router interfaces.
- Set up static routes:

  - On RouterA:
    - Route to 10.20.20.0/24 via 192.168.1.2

  - On RouterB:
    - Route to 10.10.10.0/24 via 192.168.1.1

- Bring up interfaces if shut down.


### 🔹 5. Implement Access Control (ACL)
- Configure an ACL on **RouterB** to **block ICMP echo requests** (ping) **coming from 10.20.20.0/24 to 10.10.10.0/24**.
- Apply the ACL **inbound** on RouterB's LAN interface (G0/0).
- Allow other traffic.


## 🔐 Restrictions (Real-World Constraints)
- No dynamic routing protocols (no RIP, OSPF, EIGRP).
- Only **static routing** allowed.
- All device hostnames must be properly configured.
- Add descriptions to router interfaces.
- Use a numbered ACL (not a named ACL).


## ✅ How to Test

- **Ping tests:**
  - PC1 → PC3: **should succeed**
  - PC3 → PC1: **should fail** (due to ACL)

- **Other tests:**
  - PC1 → PC2: should succeed
  - PC3 → PC4: should succeed

- **Show commands:**
  - Use `show ip route` on both routers to verify static routes.
  - Use `show access-lists` and `show running-config` to verify ACL.
  - Use `ping` and `tracert` from PCs.


---
