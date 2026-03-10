# Day 24 Lab

## Overview
This lab focuses on configuring **floating static routes**, which act as backup routes when the primary route becomes unavailable. A floating static route is created by assigning a **higher administrative distance (AD)** than the preferred route, ensuring it is only installed in the routing table if the primary route fails.

![Topology](./topology)

## Key Activities
- Configure **floating static routes** with a higher administrative distance to act as backup routes.

## Commands to remember

ip route <destination-network> <mask> <next-hop-ip>  

ip route <destination-network> <mask> <next-hop-ip> <administrative-distance>  

Source: https://www.youtube.com/watch?v=KuKC0G3LZc8&list=PLxbwE86jKRgMpuZuLBivzlM8s2Dk5lXBQ&index=50