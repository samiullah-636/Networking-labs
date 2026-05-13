# Static Routing Labs

## Overview
Static routing involves manually configuring routes on a router. It is best suited for small networks where the path is fixed.

## Labs

| Lab Name | Description |
|----------|-------------|
| [Basic Static Routing](./basic-static/) | Configuring static routes between routers |
| [Recursive Static Route](./recursive-static/) | Using next-hop IP for routing |
| [Floating Static Route](./floating-static/) | Backup routes with higher AD |
| [Summary Static Route](./summary-static/)  | Route summarization for optimization |

## Prerequisites
- Basic understanding of IP Addressing
- Basic understanding of static route
- Cisco Packet Tracer installed

## Key Commands

Static route
```bash
ip route [network] [mask] [next-hop]
```

Verification
```bash
show ip route
```
