# Issue: Ping blocked to Windows 10 Client

## Symptom
Ping from Ubuntu to Win10Client (192.168.10.30) returned 
100% packet loss despite successful pings to Windows Server.

## Cause
Windows 10 blocks ICMP (ping) traffic by default via 
Windows Defender Firewall — same default behavior as 
Windows Server.

## Fix
1. Opened Windows Defender Firewall → Advanced Settings
2. Inbound Rules → find "File and Printer Sharing 
   (Echo Request - ICMPv4-In)"
3. Right click → Enable Rule

## Result
Ping from Ubuntu to Win10Client restored.
4/4 packets received, 0% loss.

## Note
This is default Windows behavior — ICMP is blocked 
out of the box on all Windows machines. Self reminder to always check 
firewall rules before assuming a network connectivity issue.
