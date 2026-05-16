# RIPv2 Basic Configuration Lab

## Overview
In this lab, we configure **RIPv2** - the enhanced version of RIP. RIPv2 is a **classless** routing protocol that includes subnet masks in updates and supports VLSM.

## Objectives
- [ ] Configure IP addresses on all interfaces
- [ ] Configure RIPv2 with classless routing
- [ ] Disable automatic summarization
- [ ] Verify VLSM support

## Topology
![Topology](topology.png)

## IP Addressing Table

| Device | Interface | IP Address    | Subnet Mask     | Clock Rate |
|--------|-----------|---------------|-----------------|------------|
| R0    | Se0/3/0   | 30.30.30.1    | 255.255.255.252 | 64000          |
| R0    | Se0/3/1  | 40.40.40.1    | 255.255.255.252 | 64000          |
| R1    | Se0/3/0   | 40.40.40.2    | 255.255.255.252 | -          |
| R2    | Se0/3/0   | 20.20.20.1      | 255.255.255.252 | 64000      |
| R2     | Fa0/0     | 10.10.10.1      | 255.255.255.248 | -          |
| R3     | Se0/3/0     | 30.30.30.2      | 255.255.255.252 | -          |
| R3     | Se0/3/1     | 20.20.20.2   | 255.255.255.252   | -          |
| R3     | Se0/0/0     | 130.130.130.2   | 255.255.255.252   | -          |
| R3     | Se0/0/1     | 160.160.160.2   | 255.255.255.252   | 64000          |
| R4     | Se0/3/0     | 130.130.130.1   | 255.255.255.252   | 64000          |
| R4     | Se0/3/1     | 220.220.220.1   | 255.255.255.252   | 64000          |
| R5     | Se0/3/0     | 160.160.160.1   | 255.255.255.252   | -          |
| R6     | Se0/3/0     | 220.220.220.2   | 255.255.255.252   | -          |
| R6     | Fa0/0     | 192.168.1.1   | 255.255.255.240   | -          |

## Configuration Steps

### Step 1: Basic Interface Configuration
```bash
R1(config)# interface FastEthernet0/0
R1(config-if)# ip address 192.168.1.1 255.255.255.0
R1(config-if)# no shutdown
```

### Step 2: Enable RIP Routing
**On Router-0:**
```bash
Router-0(config)#router rip
Router-0(config-router)#version 2
Router-0(config-router)#network 40.40.40.0
Router-0(config-router)#network 30.30.30.0
Router-0(config-router)#no auto-summary
Router-0(config-router)#exit
```

**On Router-01:**
```bash
Router-1(config)#router rip
Router-1(config-router)#version 2
Router-1(config-router)#network 40.40.40.0
Router-1(config-router)#no auto-summary
Router-1(config-router)#exit
```

**On Router-02:**
```bash
Router-2(config)#router rip
Router-2(config-router)#version 2
Router-2(config-router)#net 20.20.20.0
Router-2(config-router)#net 10.10.10.0
Router-2(config-router)#no auto-summary
Router-2(config-router)#exit
```

**On Router-03:**
```bash
Router-3(config)#router rip
Router-3(config-router)#version 2
Router-3(config-router)#net 20.20.20.0
Router-3(config-router)#net 30.30.30.0
Router-3(config-router)#net 160.160.160.0
Router-3(config-router)#net 130.130.130.0
Router-3(config-router)#no auto-summary
Router-3(config-router)#exit
```

**On Router-04:**
```bash
Router-4(config)#router rip
Router-4(config-router)#version 2
Router-4(config-router)#net 130.130.0.0
Router-4(config-router)#net 220.220.220.0
Router-4(config-router)#no auto-summary
Router-4(config-router)#exit
```

**On Router-05:**
```bash
Router-5(config)#router rip
Router-5(config-router)#version 2
Router-5(config-router)#net 160.160.160.0
Router-5(config-router)#no auto-summary
Router-5(config-router)#exit
```

**On Router-06:**
```bash
Router-6(config)#router rip
Router-6(config-router)#version 2
Router-6(config-router)#network 220.220.220.0
Router-6(config-router)#net 192.168.1.0
Router-6(config-router)#no auto-summary
Router-6(config-router)#exit
```

### Step 3: Verification
**Checking Routing Table**
```bash
ROUTER-0#show ip route

     10.0.0.0/29 is subnetted, 1 subnets
R       10.10.10.0/29 [120/2] via 30.30.30.2, 00:00:29, Serial0/3/0
     20.0.0.0/30 is subnetted, 1 subnets
R       20.20.20.0/30 [120/1] via 30.30.30.2, 00:00:29, Serial0/3/0
     30.0.0.0/8 is variably subnetted, 2 subnets, 2 masks
C       30.30.30.0/30 is directly connected, Serial0/3/0
L       30.30.30.1/32 is directly connected, Serial0/3/0
     40.0.0.0/8 is variably subnetted, 2 subnets, 2 masks
C       40.40.40.0/30 is directly connected, Serial0/3/1
L       40.40.40.1/32 is directly connected, Serial0/3/1
     130.130.0.0/30 is subnetted, 1 subnets
R       130.130.130.0/30 [120/1] via 30.30.30.2, 00:00:29, Serial0/3/0
     160.160.0.0/30 is subnetted, 1 subnets
R       160.160.160.0/30 [120/1] via 30.30.30.2, 00:00:29, Serial0/3/0
     192.168.1.0/28 is subnetted, 1 subnets
R       192.168.1.0/28 [120/3] via 30.30.30.2, 00:00:29, Serial0/3/0
     220.220.220.0/30 is subnetted, 1 subnets
R       220.220.220.0/30 [120/2] via 30.30.30.2, 00:00:29, Serial0/3/0
```
Look for R (RIP) entries in the table.
> **Note:** Subnet masks are preserved (VLSM supported!).


**RIP Protocol Info**
```bash
Router-0#show ip protocols
Routing Protocol is "rip"
Sending updates every 30 seconds, next due in 12 seconds
Invalid after 180 seconds, hold down 180, flushed after 240
Outgoing update filter list for all interfaces is not set
Incoming update filter list for all interfaces is not set
Redistributing: rip
Default version control: send version 2, receive 2
  Interface             Send  Recv  Triggered RIP  Key-chain
  Serial0/3/0           22
  Serial0/3/1           22
Automatic network summarization is not in effect
Maximum path: 4
Routing for Networks:
	30.0.0.0
	40.0.0.0
Passive Interface(s):
Routing Information Sources:
	Gateway         Distance      Last Update
	30.30.30.2           120      00:00:06
Distance: (default is 120)
```
**Test Connectivity**
```bash
Router-0>ping 192.168.1.3

Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 192.168.1.3, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 3/12/31 ms
```
Success rate should be 100% (5/5).

> **Note:** Full device configurations are available inside the `.pkt` file.

> Key commands are documented above for quick review.

## Troubleshooting Tips
No routes learned? Check `network` statements match classful network addresses.

Subnets missing in updates? Ensure `no auto-summary` is configured under router rip.

Version mismatch? Verify all routers are configured with `version 2`.

Updates not sending? Check if interface is set to `passive-interface`.

Route unreachable? Hop count exceeded 15 (RIP maximum limit).

## Files
- [RIPv2.pkt](RIPv2.pkt) - Open this in Packet Tracer to view full configs
- [topology.png](topology.png) - Network Diagram
