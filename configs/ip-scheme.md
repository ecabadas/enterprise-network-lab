# Network IP Scheme

## Lab Network
- Network Address: 192.168.10.0
- Subnet Mask: 255.255.255.0
- CIDR: /24
- Internal Network Name: labnet
- DNS Zone: lab.local (Phase 2)
- DHCP Scope: 192.168.10.50 – 192.168.10.100 (Phase 2)

## Host Table
| Hostname        | Role              | IP Address    | Type   |
|-----------------|-------------------|---------------|--------|
| WinServer2022   | DNS + DHCP Server | 192.168.10.10 | Static |
| Ubuntu2204      | Linux Client      | 192.168.10.20 | Static |
| Win10Client     | Windows Client    | DHCP Assigned | Dynamic|

## Adapter Configuration
| VM            | Adapter 1 | Adapter 2     |
|---------------|-----------|---------------|
| WinServer2022 | NAT       | Internal (labnet) |
| Ubuntu2204    | Internal (labnet) | — |
| Win10Client   | Internal (labnet) | — |
