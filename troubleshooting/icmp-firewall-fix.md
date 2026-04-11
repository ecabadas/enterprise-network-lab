# Issue: Ping blocked between VMs

## Symptom
Ping from Ubuntu to Windows Server returned 100% packet loss
despite correct IP configuration on both VMs.

## Cause
Windows Server blocking ICMP (ping) traffic by default via 
Windows Defender Firewall.

## Fix
1. Open Windows Defender Firewall → Advanced Settings
2. Inbound Rules → find "File and Printer Sharing (Echo Request - ICMPv4-In)"
3. Right click → Enable Rule

## Result
Bidirectional ping restored. 4/4 packets received, 0% loss.
