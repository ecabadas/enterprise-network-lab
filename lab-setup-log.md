# Lab Setup Log
## A chronological log of all work completed on this project.

## April 10, 2026 — Phase 1: VM Setup & Network Configuration

### Environment Setup
- Downloaded and installed VirtualBox
- Downloaded Windows Server 2022 Evaluation ISO
- Downloaded Ubuntu 22.04 LTS ISO
- Downloaded Windows 10 Pro ISO

### Virtual Machine Creation
- Created WinServer2022 VM (4096MB RAM, 50GB disk)
- Created Ubuntu2204 VM (2048MB RAM, 25GB disk)
- Created Win10Client VM (4096MB RAM, 40GB disk)
- Configured network adapters for all three VMs

### Operating System Installation
- Installed Windows Server 2022 Desktop Experience
- Installed Ubuntu 22.04 LTS
- Installed Windows 10 Pro

### Network Configuration
- Assigned static IP 192.168.10.10 to Windows Server
- Assigned static IP 192.168.10.20 to Ubuntu
- Assigned static IP 192.168.10.30 to Win10Client (temporary)
- Enabled ICMPv4 inbound rule on Windows Server firewall
- Enabled ICMPv4 inbound rule on Windows 10 firewall

### Verification
- Win10 → Windows Server: 4/4 packets, 0% loss
- Win10 → Ubuntu: 4/4 packets, 0% loss
- Server → Win10: 4/4 packets, 0% loss
- Ubuntu → Win10: 4/4 packets, 0% loss
- Full three-way connectivity confirmed across all nodes

### Issues Encountered
- Win10 VM displayed green/orange screen on first boot
  - Resolved by correcting boot order (Optical first), 
    setting video memory to 128MB, graphics controller to VMSVGA
- Windows Server blocked ICMP by default
  - Resolved by enabling ICMPv4 inbound rule in Windows 
    Defender Firewall Advanced Settings
- Windows 10 blocked ICMP by default
  - Resolved by enabling ICMPv4 inbound rule in Windows 
    Defender Firewall Advanced Settings
- Win10 mouse not captured in VirtualBox
  - Resolved after VM resume on following session

---

## April 13, 2026 — Phase 2: DNS & DHCP Configuration

### Roles Installed
- Installed DHCP Server role on WinServer2022 via Server Manager
- Installed DNS Server role on WinServer2022 via Server Manager
- Completed DHCP post-install configuration and authorized server
- Restarted DHCP service to apply security group changes

### DHCP Configuration
- Created new scope named TechCore-Office
- Scope range: 192.168.10.50 — 192.168.10.100
- Subnet mask: 255.255.255.0
- Default gateway: 192.168.10.10
- Lease duration: 8 hours
- Activated scope immediately after creation

### DNS Configuration
- Created forward lookup zone: lab.local
- Created host (A) records for all three machines:
  - server.lab.local → 192.168.10.10
  - ubuntu.lab.local → 192.168.10.20
  - win10client.lab.local → 192.168.10.30

### Verification — Windows Server
- nslookup server.lab.local → resolved 192.168.10.10
- nslookup ubuntu.lab.local → resolved 192.168.10.20
- nslookup win10client.lab.local → resolved 192.168.10.30

### Verification — Windows 10
- Switched from static IP to DHCP
- Received IP 192.168.10.50 from TechCore-Office scope
- DHCP server identified as 192.168.10.10
- nslookup server.lab.local → resolved 192.168.10.10
- nslookup ubuntu.lab.local → resolved 192.168.10.20
- nslookup win10client.lab.local → resolved 192.168.10.30
- ping server.lab.local → 4/4 packets, 0% loss

### Verification — Ubuntu
- Configured /etc/resolv.conf to use 192.168.10.10 as DNS
- dig server.lab.local → resolved 192.168.10.10
- dig ubuntu.lab.local → resolved 192.168.10.20
- dig win10client.lab.local → resolved 192.168.10.30
- ping server.lab.local → 4/4 packets, 0% loss
- ping ubuntu.lab.local → 4/4 packets, 0% loss
- ping win10client.lab.local → 4/4 packets, 0% loss

### Issues Encountered
- Windows Server nslookup initially queried Comcast DNS
  instead of local server
  - Resolved by setting preferred DNS to 192.168.10.10
    on the labnet adapter
- Ubuntu ignored DHCP-assigned DNS server due to local
  resolver override
  - Resolved by manually editing /etc/resolv.conf and
    adding nameserver 192.168.10.10
- Windows 10 had second network adapter using Comcast DNS
  - Resolved by disabling the non-labnet adapter

---

## April 14, 2026 — Phase 3: Troubleshooting & Packet Capture
*(upcoming)*

---
