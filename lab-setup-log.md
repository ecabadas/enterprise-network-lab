## April 10–11, 2026 — Phase 1: VM Setup & Network Configuration

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

## April 11, 2026 — Phase 2: DNS & DHCP Configuration
*(in progress)*

---

## April 12, 2026 — Phase 3: Troubleshooting & Packet Capture
*(upcoming)*
