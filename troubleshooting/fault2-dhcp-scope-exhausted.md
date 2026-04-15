# Fault 2 — DHCP Scope Exhaustion

## Environment
TechCore Solutions office network — Win10Client workstation

## Symptom
- ipconfig /renew returned blank response
- ipconfig /all showed APIPA address 169.254.38.166
- Device had no network connectivity
- Could not reach any network resources

## Root Cause
DHCP scope was limited to a single IP address
(192.168.10.50) which was already leased to another
device (Ubuntu2204). No addresses were available
for new lease requests.

## Diagnosis Steps
1. Ran ipconfig /renew — blank response, no IP assigned
2. Ran ipconfig /all — identified 169.254.x.x APIPA
   address confirming DHCP failure
3. Checked DHCP console on Windows Server — confirmed
   scope end address was set to 192.168.10.50 with
   only one available address already leased

## Fix
Expanded DHCP scope end address from 192.168.10.50
back to 192.168.10.100 on Windows Server DHCP console.
Ran ipconfig /release and ipconfig /renew on Win10Client.

## Result
Win10Client received new lease 192.168.10.51.
Full network connectivity restored.

## Real World Context
DHCP scope exhaustion occurs in enterprise environments
when IP pools are too small for the number of devices,
or when stale leases are not cleared. A 169.254.x.x
APIPA address is the key diagnostic indicator — it
immediately tells you the device cannot reach a DHCP
server or the scope is full. First step is always to
check available addresses in the DHCP console.
