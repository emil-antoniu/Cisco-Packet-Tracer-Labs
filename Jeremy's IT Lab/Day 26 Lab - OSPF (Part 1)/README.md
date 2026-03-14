# Day 26 Lab

## Overview
This lab walks us through configuring OSPF.

![Topology](./images/topology.png)

## Key Activities
- Configure all routers within the same OSPF area.
- Configure loopbacks as a best practice for router ID selection.
- Understand that OSPF is a link-state routing protocol, meaning that each router shares and builds the same map of the network.

## Configurations

### Step 1 - Static IPs
```R1
R1(config)#hostname R1

R1(config)#interface gigabitEthernet 0/0
R1(config-if)#ip address 10.0.12.1 255.255.255.252

R1(config)#interface fastEthernet 1/0
R1(config-if)#ip address 10.0.13.1 255.255.255.252

R1(config)#interface gigabitEthernet 3/0
R1(config-if)#ip address 203.0.113.1 255.255.255.252
```
![R1 Config 1](./images/r1-conf-1.png)

```R2
R2(config)#hostname R2

R2(config)#interface gigabitEthernet 0/0
R2(config-if)#ip address 10.0.12.2 255.255.255.252

R2(config)#interface fastEthernet 1/0
R2(config-if)#ip address 10.0.24.1 255.255.255.252
```
![R2 Config 2](./images/r2-conf-1.png)
```R3
R3(config)#hostname R3

R3(config)#interface fastEthernet 1/0
R3(config-if)#ip address 10.0.13.2 255.255.255.252

R3(config)#interface fastEthernet 2/0
R3(config-if)#ip address 10.0.34.1 255.255.255.252
```
![R3 Config 1](./images/r3-conf-1.png)
```R4
R4(config)#hostname R4

R4(config)#interface fastEthernet 1/0
R4(config-if)#ip address 10.0.24.2 255.255.255.252

R4(config)#interface fastEthernet 2/0
R4(config-if)#ip address 10.0.34.2 255.255.255.252

R4(config)#interface gigabitEthernet 0/0
R4(config-if)#ip address 192.168.4.254 255.255.255.0
```
![R4 Config 1](./images/r4-conf-1.png)

### Step 2 - Loopback interfaces
```R1
R1(config)#interface loopback 0
R1(config-if)#ip address 1.1.1.1 255.255.255.255
```

```R2
R2(config)#interface loopback 0
R2(config-if)#ip address 2.2.2.2 255.255.255.255
```

```R3
R3(config)#interface loopback 0
R3(config-if)#ip address 3.3.3.3 255.255.255.255
```

```R4
R4(config)#interface loopback 0
R4(config-if)#ip address 4.4.4.4 255.255.255.255
```

### Step 3 - Configure OSPF
```R1
R1(config)#router ospf 1

R1(config-router)#network 10.0.12.0 0.0.0.3 area 0
R1(config-router)#network 10.0.13.0 0.0.0.3 area 0
R1(config-router)#network 1.1.1.1 0.0.0.0 area 0

R1(config-router)#passive-interface loopback 0
```
![R1 Config 3](./images/r1-conf-3.png)
```R2
R2(config)#router ospf 2

R2(config-router)#network 10.0.12.0 0.0.0.3 area 0
R2(config-router)#network 10.0.24.0 0.0.0.3 area 0
R2(config-router)#network 2.2.2.2 0.0.0.0 area 0

R2(config-router)#passive-interface loopback 0
```
![R2 Config 3](./images/r2-conf-3.png)
```R3
R3(config)#router ospf 3

R3(config-router)#network 10.0.13.0 0.0.0.3 area 0
R3(config-router)#network 10.0.34.0 0.0.0.3 area 0
R3(config-router)#network 3.3.3.3 0.0.0.0 area 0

R3(config-router)#passive-interface loopback 0
```
![R3 Config 3](./images/r3-conf-3.png)
```R4
R4(config)#router ospf 4

R4(config-router)#network 10.0.24.0 0.0.0.3 area 0
R4(config-router)#network 10.0.34.0 0.0.0.3 area 0
R4(config-router)#network 4.4.4.4 0.0.0.0 area 0
R4(config-router)#network 192.168.4.0 0.0.0.255 area 0

R4(config-router)#passive-interface loopback 0
R4(config-router)#passive-interface gigabitEthernet 0/0
```
![R4 Config 3](./images/r4-conf-3.png)

### Step 4 - Configure R1 as ASBR
```R1
R1(config-router)#default-information originate

R1(config)#ip route 0.0.0.0 0.0.0.0 203.0.113.2
```

### Step 5 - Check routing talbes
![R2 Routes](./images/r2-routes.png)
![R3 Routes](./images/r3-routes.png)
![R4 Routes](./images/r4-routes.png)

Source: https://www.youtube.com/watch?v=LeLRWjfylcs&list=PLxbwE86jKRgMpuZuLBivzlM8s2Dk5lXBQ&index=54