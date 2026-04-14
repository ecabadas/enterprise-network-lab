# Fault 1 — Wrong DNS Server IP

## Environment
TechCore Solutions office network — Win10Client workstation

## Symptom
- nslookup timed out with no response
- ping server.lab.local failed with "could not find host"
- ping 192.168.10.10 still succeeded

## Root Cause
DNS server IP manually set to 192.168.10.99 — 
a nonexistent host on the network. All DNS queries 
were sent to an address with no responding service.

## Diagnosis Steps
1. Ran nslookup server.lab.local — repeated timeouts
2. Ran ping server.lab.local — hostname not resolved
3. Ran ping 192.168.10.10 — succeeded, confirming
   network connectivity was intact
4. Ran ipconfig /all — identified incorrect DNS server
   192.168.10.99 under ethernet adapter settings

## Fix
Changed preferred DNS server from 192.168.10.99 
back to 192.168.10.10 (Windows Server) in 
IPv4 adapter settings.

## Result
nslookup server.lab.local resolved correctly.
Hostname ping restored. 0% packet loss.

## Real World Context
From what I've learned, this is a common issue in enterprise
environments, usually caused by a manually misconfigured workstation
or an incorrect DNS server IP in the DHCP scope. A key indicator is
that ping by IP works, while ping by hostname fails, which points to
a DNS issue rather than general network connectivity.
