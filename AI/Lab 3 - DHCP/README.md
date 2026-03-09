🧪 **Lab 3: DHCP Server and Dynamic Host Configuration**

---

🏢 **Scenario:**
You work for a small company that recently expanded and added a "Research" department. Manually assigning IP addresses to devices has become inefficient. Your task is to set up a centralized DHCP server to dynamically assign IP addresses to client devices. You will also ensure that key devices (such as servers) retain manually assigned static IPs.


---

📦 **Topology Overview:**

- 1 Router (Router0)
- 1 Switch (Switch0)
- 4 PCs (PC1, PC2, PC3, PC4)

---

🏗️ **Step-by-Step Objectives:**

🔹 1. VLAN Configuration
- No new VLANs needed for this lab (assume all devices are in VLAN1).

🔹 2. Static IP Address Assignment
- Assign Router0's LAN interface a static IP address: `192.168.50.1/24`.

🔹 3. DHCP Server Setup on Router
- Create a DHCP pool named "Research_Pool".
- Network: `192.168.50.0/24`
- Default Gateway: `192.168.50.1`
- DNS Server: `8.8.8.8`
- Exclude the following addresses from being assigned:
  - `192.168.50.1` (router)
  - `192.168.50.2` (future file server)
  - `192.168.50.3` (future printer)

🔹 4. Switch Setup
- Configure necessary port settings (default access ports for PCs).
- Connect Router0 to Switch0.

🔹 5. PC Configuration
- Configure PC1, PC2, PC3, and PC4 to obtain an IP address dynamically (DHCP).


---

🔐 **Restrictions (Real-World Constraints):**

- No static IPs are allowed for end-user PCs.
- Switch ports must be administratively enabled.
- Router must have a banner warning about unauthorized access.


---

✅ **How to Test:**

- On each PC, verify that it has received an IP address in the `192.168.50.x` range.
- Confirm that none of the excluded addresses (`.1`, `.2`, `.3`) are given to any PC.
- Ping the default gateway (`192.168.50.1`) from each PC.
- Use the following router commands:
  - `show ip dhcp binding` (to view DHCP leases)
  - `show running-config` (to verify DHCP pool and exclusions)


---

⚠️ **Common Mistakes to Avoid:**
- Forgetting to `ip dhcp excluded-address` before defining the pool.
- Typing errors in the network, gateway, or DNS server address.
- PCs still being set to static IPs accidentally.


---
