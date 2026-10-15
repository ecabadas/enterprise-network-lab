# Screenshots

## Phase 1 - VM Setup & Network Configuration
| File | Description |
|------|-------------|
| 01-winserver-network-adapter_NAT.png.png | Windows Server NAT adapter config |
| 02-winserver-network-adapter_Internal.png.png | Windows Server internal labnet adapter config |
| 03-win10-network-adapter.png.png | Win10 client internal adapter config |
| 04-ubuntu-network-adapter.png.png | Ubuntu internal adapter config |
| 05-server-manager-dashboard.png.png | Windows Server Manager dashboard |
| 06-winserver-static-ip.png.png | Windows Server static IP configuration |
| 07-ubuntu-static-ip.png.png | Ubuntu static IP configuration |
| 08-ping-ubuntu-to-server.png.png | Successful ping from Ubuntu to Windows Server |
| 09-ping-server-to-ubuntu.png.png | Successful ping from Windows Server to Ubuntu |
| 10-icmpv4-firewall-rule-enabled.png.png | ICMPv4 inbound rule enabled on Windows Server |
| 11-win10-static-ip.png.png | Win10 static IP configuration |
| 12-ping-win10-to-server.png.png | Successful ping from Win10 to Windows Server |
| 13-ping-win10-to-ubuntu.png.png | Successful ping from Win10 to Ubuntu |
| 14-ping-server-to-win10.png.png | Successful ping from Windows Server to Win10 |
| 15-ping-ubuntu-to-win10.png.png | Successful ping from Ubuntu to Win10 |

## Phase 2 - DNS & DHCP Configuration
| File | Description |
|------|-------------|
| 16-dns-dhcp-roles-selected.png | DNS and DHCP roles selected in Server Manager |
| 17-dns-dhcp-install-success.png | DNS and DHCP installation success confirmation |
| 18-dhcp-scope-created.png | TechCore-Office DHCP scope created |
| 19-dns-zone-created.png | lab.local DNS forward lookup zone created |
| 20-dns-host-records.png | DNS host records for all three machines |
| 21-dns-nslookup-server.png | nslookup resolving server.lab.local |
| 22-dns-nslookup-ubuntu.png | nslookup resolving ubuntu.lab.local |
| 23-dns-nslookup-win10client.png | nslookup resolving win10client.lab.local |
| 24-win10-dhcp-lease.png | Windows 10 DHCP lease from server |
| 25-win10-nslookup-server.png | Win10 nslookup resolving server.lab.local |
| 26-win10-nslookup-ubuntu.png | Win10 nslookup resolving ubuntu.lab.local |
| 27-win10-nslookup-win10client.png | Win10 nslookup resolving win10client.lab.local |
| 28-ubuntu-dig-server.png | Ubuntu dig resolving server.lab.local |
| 29-ubuntu-dig-ubuntu.png | Ubuntu dig resolving ubuntu.lab.local |
| 30-ubuntu-dig-win10.png | Ubuntu dig resolving win10client.lab.local |
| 31-win10-ping-hostname.png | Win10 ping by hostname server.lab.local |
| 32-ubuntu-ping-server-hostname.png | Ubuntu ping by hostname server.lab.local |
| 33-ubuntu-ping-ubuntu-hostname.png | Ubuntu ping by hostname ubuntu.lab.local |
| 34-ubuntu-ping-win10-hostname.png | Ubuntu ping by hostname win10client.lab.local |

## Phase 3 - Troubleshooting & Packet Capture
| File | Description |
|------|-------------|
| 35-wireshark-dns-query.png | Wireshark capture of DNS query packet |
| 36-wireshark-dns-response.png | Wireshark capture of DNS response packet |
