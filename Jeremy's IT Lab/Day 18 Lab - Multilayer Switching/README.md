# Day 18 Lab

## Overview
This lab focuses on **inter-VLAN routing using a Layer 3 (multilayer) switch**.

![Topology](topology.png)

## Key Activities
- Enable **Layer 3 routing** on the multilayer switch.
- Create **SVIs (Switch Virtual Interfaces)** for each VLAN and assign IP addresses.
- Verify inter-VLAN communication by testing connectivity between hosts in different VLANs.

![Layer3-SW](configs-layer3-sw.png)

## Commands to remember
On the multilayer switch:<br>
`ip routing`

interface vlan 10  
ip address 192.168.10.1 255.255.255.0  
no shutdown  

interface vlan 20  
ip address 192.168.20.1 255.255.255.0  
no shutdown  

Source: https://www.youtube.com/watch?v=MQcCr3QW1vE&list=PLxbwE86jKRgMpuZuLBivzlM8s2Dk5lXBQ&index=34