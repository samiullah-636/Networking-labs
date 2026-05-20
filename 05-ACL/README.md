# Access Control Lists (ACL) Labs

## Overview
ACLs are used to filter network traffic based on defined rules. They can permit or deny packets based on source/destination IP, protocol type, port numbers, and more. ACLs are essential for network security and traffic management.

## Key Concepts Covered
- Standard ACL (Source IP only)
- Extended ACL (Source, Destination, Protocol, Port)

## Labs in This Section

| Lab Name | Difficulty | Description |
|----------|------------|-------------|
| [Standard ACL](./standard-acl/) | Filtering based on source IP only |
| [Extended ACL](./extended-acl/) | Filtering based on IP, protocol, ports |

## ACL Types Comparison

| Feature | Standard ACL | Extended ACL |
|---------|--------------|--------------|
| **Filter Based On** | Source IP only | Source + Dest IP + Protocol + Port |
| **Number Range** | 1-99, 1300-1999 | 100-199, 2000-2699 |
| **Placement** | Near Destination | Near Source |
| **Use Case** | Simple filtering | Advanced security |

## Prerequisites
- IP Addressing & Subnetting
- Static/Dynamic Routing
- Cisco Packet Tracer installed