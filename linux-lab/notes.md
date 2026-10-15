# Linux Lab Notes

## Status
Complete (April 2026)

## What Was Done
- Ubuntu 22.04 LTS installed in VirtualBox (2048MB RAM, 25GB disk)
- Static IP 192.168.10.20 on the labnet internal network
- DNS pointed at 192.168.10.10 (Windows Server); verified with dig and nslookup
- Full bidirectional connectivity with the Windows nodes verified by ping, including by hostname

## Commands Used
- ip addr — confirmed IP assignment
- ping — verified connectivity to server and clients
- dig — verified DNS resolution against the lab.local zone
- traceroute — traced paths between nodes

Full chronological log: ../lab-setup-log.md
