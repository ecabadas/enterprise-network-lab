# Troubleshooting Log

Real issues encountered during the virtual lab build and how they were resolved.

## Resolved Issues

| File | Problem | Root Cause |
|---|---|---|
| fault1-wrong-dns-server.md | nslookup timeouts; hostname resolution failing while ping by IP worked | Workstation DNS pointed at a nonexistent host (192.168.10.99) |
| fault2-dhcp-scope-exhausted.md | Workstation pulled an APIPA address (169.254.x.x), no connectivity | DHCP scope narrowed to a single already-leased address |
| icmp-firewall-fix.md | 100% packet loss between Ubuntu and Windows Server | Windows Defender Firewall blocking ICMP by default |
| win10-icmp-firewall-fix.md | 100% packet loss to the Windows 10 client | Same default ICMP block on Windows 10 |

## Packet Analysis

| File | Subject |
|---|---|
| wireshark-dns-analysis.md | DNS query and response pair captured in Wireshark: the Phase 2 DNS server resolving a client lookup, matched by transaction ID, RCODE 0 |

## Tools Used

ping, ipconfig /all, nslookup, dig, DHCP management console, Windows Defender Firewall with Advanced Security, Wireshark

## Goal

Demonstrate practical troubleshooting skills in a simulated enterprise network environment.
