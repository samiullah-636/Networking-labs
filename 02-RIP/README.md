# RIP (Routing Information Protocol) Labs

## Overview
RIP is a **distance-vector routing protocol** that uses hop count as its metric. It's one of the oldest routing protocols and great for understanding dynamic routing fundamentals.

## Key Concepts Covered
- Distance Vector Routing
- Hop Count Metric (Max 15 hops)
- RIPv1 vs RIPv2 Differences
- Classful vs Classless Routing
- Automatic Summarization
- RIPv2 Authentication (MD5)

## Labs in This Section

| Lab Name | Description |
|----------|-------------|
| [RIPv1 Basic](./ripv1-basic/) | Configuring RIPv1 (Classful) |
| [RIPv2 Basic](./ripv2-basic/) | Configuring RIPv2 (Classless) |
| [RIPv2 Authentication](./ripv2-authentication/) | Securing RIP with MD5 |

## RIP Versions Comparison

| Feature | RIPv1 | RIPv2 |
|---------|-------|-------|
| **Classful/Classless** | Classful | Classless |
| **Subnet Mask** | Not included | Included in updates |
| **Broadcast/Multicast** | 255.255.255.255 | 224.0.0.9 |
| **Authentication** |  No |  Yes (MD5) |
| **VLSM Support** |  No |  Yes |

## Prerequisites
- Static Routing concepts
- Basic IP Addressing
- Cisco Packet Tracer installed