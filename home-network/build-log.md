# Build Log

| Date | What happened |
|---|---|
| Late Sep 2026 | Purchased the Ubiquiti Cloud Gateway Max. Plan: replace the ISP-provided gateway with my own modem + gateway and rebuild the home network properly segmented. |
| Oct 7, 2026 | Installed the patch panel and terminated the in-wall Ethernet drops. Physical layer done. |
| Oct 8, 2026 | Cutover day. Swapped in the Arris S33 modem and the UCG-Max. Expected a smooth switchover. Immediately noticed wired download speeds were far below the 1.2 Gbps plan. Opened incident INC-2026-001 and started structured troubleshooting instead of guessing. |
| Oct 9, 2026 | Controlled testing: confirmed the collapse on WAN auto-negotiation and the recovery on forced 1 Gbps. Ran community research, found corroborating cases across ISPs and modems, posted findings on r/Ubiquiti. Opened Ubiquiti support ticket #6043461 with structured data. |
| Oct 10, 2026 | Full A/B session on one test machine: cables, LAN ports, and the in-wall run all ruled out. Key finding: the WAN link trains at 2.5 GbE cleanly — negotiation succeeds, forwarding collapses. |
| Oct 12, 2026 | Ubiquiti's dev team reviewed my test data and prescribed a fix: update to UniFi OS 6.0.12 Early Access plus targeted runtime commands. |
| Oct 13, 2026 | Applied the prescription in a maintenance window. Verified: ~950 Mbps down on Speedtest.net, ~855-865 on LibreSpeed, WAN back on auto-negotiation. Decided to keep the gateway. Fix is runtime-only (reapplied after reboots); waiting on a permanent fix from Ubiquiti. |

## Current State

- Gateway stable on the dev-team fix, monitoring ongoing
- Known limitation: the three runtime commands must be reapplied after any reboot
- Next: IoT/guest VLAN segmentation, remote-access VPN, small home server
