# Lab Setup Log

A chronological log of all work completed on this project.

---

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
- Enabled ICMPv4 inbound rule on Windows Server firewall
- *(pending - Win10 VM network configuration)*

### Verification
- Confirmed bidirectional ping between Windows Server and Ubuntu
- 0% packet loss on all connectivity tests
- *(pending - Win10 VM bidirectional ping communication)*

### Issues Encountered
- Win10 VM displayed green/orange screen on first boot
- Resolved by adjusting boot order, video memory to 128MB,
  and graphics controller to VMSVGA
- Windows Server blocked ICMP by default
- Resolved by enabling ICMPv4 inbound rule in Windows Defender 
  Firewall Advanced Settings

---

## April 11, 2026 — Phase 2: DNS & DHCP Configuration
*(in progress)*

---

## April 12, 2026 — Phase 3: Troubleshooting & Packet Capture
*(upcoming)*
