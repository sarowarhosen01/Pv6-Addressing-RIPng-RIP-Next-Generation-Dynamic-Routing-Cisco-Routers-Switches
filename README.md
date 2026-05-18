# IPv6 Static Routing Implementation

**A Cisco Packet Tracer Project**

![Network Topology](topology.png)  
*(Add a screenshot of your Packet Tracer topology here)*

## Project Overview

This project implements IPv6 static routing across a multi-router topology. It demonstrates manual route configuration for IPv6 networks, enabling communication between different LAN segments without dynamic routing protocols.

**Objectives:**
- Design and configure IPv6 addressing scheme
- Configure IPv6 on router interfaces
- Implement static routes for full network reachability
- Verify connectivity and routing tables
- Document topology, addressing, and configurations

## Network Topology

**Devices:**
- 3 x Routers (e.g., 2911 or 4331 series)
- 2-3 x Layer 2 Switches
- 4-6 x PCs (for testing)

**Topology Description:**
- **R1** connected to LAN1 and to R2
- **R2** connected to R1 and R3 (backbone)
- **R3** connected to R2 and LAN2/LAN3
- PCs connected via switches to respective routers

*(Insert detailed topology diagram here - export from Packet Tracer)*

### Network Topology Table

| Device | Interface     | Connected To     | Purpose                  |
|--------|---------------|------------------|--------------------------|
| R1     | GigabitEthernet0/0 | Switch1 (LAN1)  | User LAN                 |
| R1     | Serial0/0/0   | R2 Serial0/0/0  | Inter-router link        |
| R2     | Serial0/0/0   | R1              | Inter-router link        |
| R2     | Serial0/0/1   | R3              | Inter-router link        |
| R3     | GigabitEthernet0/0 | Switch2 (LAN2) | User LAN                 |
| R3     | GigabitEthernet0/1 | (Optional LAN3)| Additional segment       |
| PC1    | NIC           | Switch1          | End device (LAN1)        |
| PC2    | NIC           | Switch2          | End device (LAN2)        |

## IP Addressing Table

| Device | Interface              | IPv6 Address                  | Prefix | Default Gateway (for PCs) |
|--------|------------------------|-------------------------------|--------|---------------------------|
| R1     | G0/0                   | 2001:db8:1::1/64             | /64    | -                         |
| R1     | S0/0/0                 | 2001:db8:12::1/64            | /64    | -                         |
| R1     | Loopback0              | 2001:db8:11::1/128           | /128   | -                         |
| R2     | S0/0/0                 | 2001:db8:12::2/64            | /64    | -                         |
| R2     | S0/0/1                 | 2001:db8:23::1/64            | /64    | -                         |
| R3     | S0/0/1                 | 2001:db8:23::2/64            | /64    | -                         |
| R3     | G0/0                   | 2001:db8:3::1/64             | /64    | -                         |
| PC1    | NIC                    | 2001:db8:1::10/64            | /64    | 2001:db8:1::1             |
| PC2    | NIC                    | 2001:db8:3::10/64            | /64    | 2001:db8:3::1             |

*(Update this table with your actual addresses from the .pkt file)*

## Configuration Highlights

### 1. Enable IPv6 Routing
```cisco
Router(config)# ipv6 unicast-routing
