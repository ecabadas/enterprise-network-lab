# Enterprise Network Lab — TechCore Solutions

## Overview
Designed and deployed a small office network for a simulated 
10-person IT consulting firm (TechCore Solutions) using Windows 
Server, Windows 10, and Ubuntu Linux in a virtualized environment. 
The goal was to eliminate manual IP configuration and implement 
centralized DNS and DHCP services across the office network.

## Business Problem
The office had no centralized IP management or internal DNS. 
Devices were manually configured, causing address conflicts and 
making it difficult to locate machines by hostname. This lab 
documents the planning, implementation, and verification of a 
solution using Windows Server 2022.

## Environment
- Hypervisor: VirtualBox 7.x
- Host OS: Windows 11
- Internal Network: labnet (192.168.10.0/24)

## Network Machines
| Hostname | OS | Role | IP |
|---|---|---|---|
| WinServer2022 | Windows Server 2022 | DNS + DHCP Server | 192.168.10.10 (static) |
| Win10Client | Windows 10 Pro | Employee workstation | DHCP assigned |
| Ubuntu2204 | Ubuntu 22.04 LTS | Secondary workstation | 192.168.10.20 (static) |

## What Was Implemented
- Virtualized office network using VirtualBox internal networking
- Static IP addressing on server and Linux nodes
- Windows Server configured as DHCP server for workstation 
  IP assignment
- Windows Server configured as DNS server with internal 
  zone (lab.local)
- ICMPv4 firewall rule enabled to allow network diagnostics
- Verified full connectivity across all three nodes

## Troubleshooting Documented
- Resolved ICMP blocked by Windows Firewall default rules
- Diagnosed and fixed VM boot failure caused by incorrect 
  boot order and graphics controller settings
- Verified DNS resolution and DHCP lease assignment

## Tools Used
| Tool | Purpose |
|---|---|
| ping | Verified connectivity between nodes |
| tracert / traceroute | Traced network path between machines |
| ipconfig / ip addr | Confirmed IP assignments |
| nslookup / dig | Verified DNS resolution |
| Wireshark | Captured and analyzed DNS query packets |

## Security Notes
- Windows Server firewall configured to allow only necessary 
  inbound ICMP traffic
- All VMs isolated on internal network with no external 
  exposure except server NAT adapter
- DHCP scope limited to defined range to prevent unauthorized 
  IP assignment

## Project Status
- [x] Phase 1 — VM setup and network configuration
- [x] Phase 2 — DNS and DHCP configuration
- [ ] Phase 3 — Troubleshooting and Wireshark packet capture

## Documentation
- Network topology diagram: network-diagrams/lab-topology.png
- IP scheme: configs/ip-scheme.md
- Lab log: lab-setup-log.md
- Screenshots: screenshots/
- Troubleshooting notes: troubleshooting/
