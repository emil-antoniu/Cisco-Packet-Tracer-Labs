# Day 20 Lab

## Overview
This lab focuses on **analyzing Spanning Tree Protocol (STP)** behavior in a switched network.

![Topology](./topology.png)

## Key Activities
- Examine the network topology and calculate which switch becomes the **root bridge** by comparing bridge priorities and MAC addresses.
- Identify the **root ports** on non-root switches by determining which interface provides the lowest path cost to the root bridge.
- Determine the **designated port** for each network segment (the port that forwards traffic toward the root).
- Identify any **non-designated ports** that are placed in a blocking state to prevent Layer 2 loops.
- Observe STP output fields such as **Root ID**, **Bridge ID**, port roles, port states, and path costs.

![SW1](./sw1.png)
![SW2](./sw2.png)
![SW3](./sw3.png)
![SW4](./sw4.png)

## Commands to remember

`show spanning-tree detail`/`summary`

Source: https://www.youtube.com/watch?v=Ev9gy7B5hx0&list=PLxbwE86jKRgMpuZuLBivzlM8s2Dk5lXBQ&index=38