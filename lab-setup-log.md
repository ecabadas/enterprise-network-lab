# Virtual Lab Setup Log
Enterprise Network Configuration & Troubleshooting Lab

## Overview
This document tracks the step-by-step setup of a virtualized enterprise-style network environment using VirtualBox. The lab includes a Windows Server, Windows 10 client, and Ubuntu 24.04 Linux VM.

---

## Phase 1: Environment Preparation

### Completed Actions
- Installed Oracle VirtualBox on host machine (Lenovo ThinkPad X1 Carbon)
- Downloaded required ISO files:
  - Windows Server ISO
  - Windows 10 Client ISO
  - Ubuntu 24.04 ISO

---

## Phase 2: Virtual Machine Creation

### Virtual Machines Created
- Windows Server VM
- Windows 10 Client VM
- Ubuntu Linux VM

### Configuration Steps
For each VM:
- Created new virtual machine shell in VirtualBox
- Assigned appropriate OS type and version
- Allocated system resources (RAM and CPU)
- Created virtual hard disks (VDI, dynamically allocated)

---

## Phase 3: Network Configuration

### Windows Server VM
- Adapter 1: NAT (for external internet access if needed)
- Adapter 2: Internal Network (labnet)

### Windows 10 Client VM
- Adapter 1: Internal Network (labnet)

### Ubuntu VM
- Adapter 1: Internal Network (labnet)

### Network Notes
- Internal Network name standardized as: `labnet`
- This network is intended to simulate an isolated enterprise environment
- NAT adapter on Windows Server allows optional external connectivity for updates or package installs

---

## Phase 4: ISO Attachment

### Completed Actions
- Attached Windows Server ISO to Windows Server VM storage controller
- Attached Windows 10 ISO to Windows 10 VM storage controller
- Attached Ubuntu 24.04 ISO to Ubuntu VM storage controller

---

## Phase 5: Documentation

### Evidence Collected
- Screenshots of:
  - VM creation process
  - Network adapter configuration
  - Storage/ISO attachment setup

---

## Current Status
- Virtual machines created and configured
- Network segmentation implemented (Internal Network: labnet)
- Installation phase pending (OS setup not yet completed)

---

## Next Steps
- Install operating systems on all virtual machines
- Verify IP addressing and network connectivity
- Begin ping testing between systems
- Document troubleshooting scenarios
