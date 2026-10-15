# Windows Lab Notes

## Status
Complete (April 2026)

## What Was Done
- Windows 10 Pro installed in VirtualBox (4096MB RAM, 40GB disk)
- Migrated from a temporary static IP to DHCP; received 192.168.10.50 from the TechCore-Office scope
- DNS resolution verified with nslookup against all lab.local host records
- ICMPv4 inbound firewall rule enabled (blocked by default on Windows)

## Commands Used
- ipconfig /all — confirmed DHCP lease and DNS server
- ipconfig /release and ipconfig /renew — tested lease renewal
- nslookup — verified DNS resolution
- ping — verified connectivity by IP and hostname

Full chronological log: ../lab-setup-log.md
