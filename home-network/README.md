# Home Network Build

## TL;DR

I replaced my ISP-provided gateway with my own modem and a Ubiquiti Cloud Gateway Max, expecting a straightforward cutover. Instead, the new gateway immediately showed a WAN throughput bug: with the WAN port on auto-negotiation, wired downloads collapsed to a fraction of my plan speed. I spent two weeks methodically isolating the problem, ruled out every other variable one by one, worked with Ubiquiti support using my test data, and their dev team used my findings to prescribe a fix. It worked. I am now running stable while waiting on a permanent fix.

**Bottom line:** 1.2 Gbps plan. Was getting ~80-170 Mbps wired on auto-negotiation. Now getting ~950 Mbps.

## The Build

- **Modem:** Arris Surfboard S33 (DOCSIS 3.1, 2.5 GbE port) — replaced the ISP gateway
- **Gateway:** Ubiquiti Cloud Gateway Max (UCG-Max) — router, firewall, and UniFi controller
- **Distribution:** PoE switch feeding a patch panel and in-wall Ethernet drops
- **Wireless:** UniFi access point, segmented SSIDs on separate VLANs
- **Power:** core network on a UPS so the modem, gateway, and switch stay up through outages

Full inventory and topology: [topology.md](topology.md)
Build timeline: [build-log.md](build-log.md)

## The Problem

Day one, the numbers did not add up. With the gateway's WAN port on auto-negotiation, wired download speeds collapsed:

| Condition | Speedtest.net | LibreSpeed CLI |
|---|---|---|
| WAN auto-negotiation, wired | ~80-170 Mbps | ~78-114 Mbps |
| WAN forced to 1 Gbps full duplex, wired | ~940-950 Mbps | ~855-865 Mbps |

Upload was normal (~40 Mbps) in both cases. The link itself trained at 2.5 GbE without any trouble — negotiation was succeeding, but forwarding was collapsing.

Full troubleshooting write-up: [troubleshooting/wan-throughput-degradation.md](troubleshooting/wan-throughput-degradation.md)

## How I Worked the Problem

1. **Isolated the variable.** A/B tested WAN auto-negotiation vs. forced 1 Gbps with everything else held constant.
2. **Ruled out the obvious, with evidence.** Two different Ethernet cables, two different LAN ports, the in-wall run, and the test machine itself — every test run on the same computer, same servers. All ruled out.
3. **Read the anomalies.** Two speed-test tools disagreed with each other by 4x under the same condition, which pointed at a per-flow forwarding problem rather than a link-speed ceiling. Wireless on the same machine outperformed wired, which pointed at the path, not the WAN link.
4. **Did the research.** Found corroborating cases across ISPs and modem brands, all converging on the same workaround. Posted my own findings and data for the community.
5. **Worked the vendor ticket properly.** Opened Ubiquiti support ticket #6043461 with structured test data, controlled benchmarks, and specific diagnostic questions instead of "internet slow, please help."
6. **Ran the dev team's prescription.** Their engineers used my data to prescribe a firmware update plus targeted runtime commands. I applied them in a maintenance window, re-tested, and confirmed the fix.

## Result

- Speedtest.net: ~950 Mbps down (was ~80-170)
- LibreSpeed CLI: ~855-865 Mbps down (was ~78-114)
- WAN port back on auto-negotiation, hardware acceleration on
- Stable since October 13, 2026

The fix involves runtime commands that do not survive a reboot, so I reapply them after restarts. Ubiquiti is working on a permanent fix. I decided to keep the gateway.

## What I Learned

- Test one variable at a time and write down every result. Memory is not data.
- When two measurement tools disagree, the disagreement itself is evidence — don't average them away.
- A workaround is an observed result, not a root cause. Don't confuse the two.
- Vendors move faster when you hand them structured data and a clear question instead of a complaint.

## What's Next

- Monitoring throughput stability over time
- Waiting on Ubiquiti's permanent fix
- Planned: segmented VLANs for IoT and guest, a VPN for remote access, and a small home server (AdGuard Home, VPN, game server)

---

**A note on privacy:** anything that could identify my home network — public IP addresses, MAC addresses, Wi-Fi network names, passwords — has been obscured or replaced with placeholders throughout this repo. The gear, the tests, and the results are all real. I just did not want to publish anything someone could use to find or reach my network.
