# WAN Throughput Degradation — UCG-Max (INC-2026-001)

**Status:** Resolved with vendor-prescribed workaround. Waiting on permanent fix.
**Vendor ticket:** Ubiquiti Support #6043461
**Dates:** October 8–13, 2026

## Summary

After cutting over to a Ubiquiti Cloud Gateway Max, wired downloads collapsed whenever the WAN port was left on auto-negotiation. The link trained at 2.5 GbE without issue — negotiation was succeeding, but the gateway was not forwarding at anything close to line rate. Two weeks of structured testing isolated the problem to the gateway's 2.5G forwarding path, and Ubiquiti's dev team used my test data to prescribe a fix that restored full throughput.

## Confirmed Observations

- Gateway: Ubiquiti Cloud Gateway Max, base model (no storage)
- ISP: Xfinity 1.2 Gbps plan; modem: Arris Surfboard S33 (2.5 GbE port) → gateway WAN (2.5 GbE port)
- Hardware acceleration ON, flow control ON, LAN ports on auto-negotiation throughout all tests
- WAN on **auto-negotiation**: wired downloads collapsed
  - Speedtest.net: ~80–170 Mbps down
  - LibreSpeed CLI: ~78–114 Mbps down
  - Upload: ~40 Mbps (normal — degradation was download-direction only)
- WAN **forced to 1 Gbps full duplex**: wired downloads recovered to ~940–950 Mbps
- The issue was present **before** a firmware update done at support's request, so it was not caused by that update

## What I Ruled Out (and How)

Every test was run on the same computer against the same test servers, changing one variable at a time:

| Suspect | Test | Result |
|---|---|---|
| Bad Ethernet cable | Two different cables, identical collapse | Ruled out |
| Bad LAN port | Two different gateway LAN ports, identical collapse | Ruled out |
| In-wall wiring | Direct short cable vs. in-wall office run, identical collapse | Ruled out |
| Test machine | All runs on the same computer | Ruled out |
| Negotiation failure | Dashboard showed the link training at 2.5 GbE | Ruled out — the link came up fine |
| Firmware regression | Issue predated the 6.0.11 update done at support's request | Ruled out |

## Key Findings (the Ones That Pointed Somewhere)

1. **The link trained at 2.5 GbE cleanly.** This was the big one. Auto-negotiation was not failing — the gateway and modem agreed on 2.5G without trouble, and then forwarding collapsed anyway. That moved the suspect list from the physical link to the forwarding path.
2. **Two measurement tools disagreed with each other.** Speedtest.net and LibreSpeed CLI differed by up to 4x under the same condition. A simple link-speed cap would constrain both roughly equally. The divergence pointed at a per-flow problem (loss, reordering, or CPU-bound forwarding), not a speed ceiling.
3. **Wireless beat wired on the same machine.** Under auto-negotiation, the same computer got ~500–740 Mbps over Wi-Fi but only ~80–170 Mbps wired. Same WAN condition, same machine — the difference was in the path, which further implicated the gateway's wired forwarding path rather than the WAN link itself.
4. **Disabling hardware acceleration restored speeds** (but spiked CPU and raised security concerns, so I reverted it). That the problem could be worked around either by changing negotiation mode or by disabling offload helped separate a PHY problem from a driver/offload problem.
5. **Community corroboration.** Independent UCG-Max owners across different ISPs (Xfinity, Spectrum, FTTH) and modem brands reported the same symptom and the same workaround (manually locking WAN speed). No ISP- or modem-specific pattern — which pointed at the gateway, not my modem or ISP.

## Hypotheses I Considered (All Unverified — I Never Claimed More Than the Data Showed)

- **Marginal 2.5GBASE-T link** producing errors — weakened when the link trained at full 2.5G
- **Firmware/driver issue in the 2.5G forwarding path** — best fit for the evidence
- **Flow-control / pause-frame interaction** — possible, never confirmed
- **A traffic rule silently disabling hardware offload** — a known independent cause of similar symptoms on this hardware; cheap to check, never confirmed
- **Modem/ISP-side issue** — no supporting evidence; forcing the gateway port changed the outcome, which implicated the gateway side

## Working With Ubiquiti Support

I opened ticket #6043461 with structured data instead of a vague complaint: controlled benchmarks in a table, the full list of ruled-out variables, the anomalous findings, and three specific diagnostic questions (known issues in the 2.5G/offload path, which counters distinguish PHY vs. driver problems, and how to confirm offload is actually active beyond the UI toggle).

Their dev team reviewed the data and prescribed:

1. Update to UniFi OS 6.0.12 Early Access (the 6.0.11 build I was on did not fix it)
2. Keep hardware acceleration ON, WAN and test LAN ports on auto-negotiation
3. Run three runtime commands over SSH targeting the packet-processing path:

```
echo 'add eth4 switch0' > /proc/sys/ppe/ppe_drv/lpbk_buffer_map
echo 'add switch0 eth4' > /proc/sys/ppe/ppe_drv/lpbk_buffer_map
echo 1 > /sys/kernel/debug/ecm/ecm_db/defunct_all
```

(`eth4` is the WAN port on this hardware. These commands are runtime-only and are lost on reboot.)

## Verification (October 13, 2026)

Applied the prescription in a maintenance window with local access available, then re-ran the same tests:

| Test | Before | After |
|---|---|---|
| Speedtest.net down | ~80–170 Mbps | ~950 Mbps |
| LibreSpeed CLI down | ~78–114 Mbps | ~855–865 Mbps |

WAN port back on auto-negotiation, hardware acceleration on, stable since.

## Current Status

- Running the vendor-prescribed fix. Throughput is stable.
- The three commands do not survive a reboot — I reapply them after restarts.
- Ubiquiti is working on a permanent fix. I decided to keep the gateway.
- If the fix ever stops working, the fallback is the known-good workaround: force the WAN port to 1 Gbps full duplex.

## What This Taught Me

- Change one variable at a time and write down every result. Memory is not data.
- When two tools disagree, the disagreement is evidence. Don't average it away.
- A workaround is an observed result, not a root cause. Keep those separate or you'll stop investigating too early.
- Vendors move faster when you bring structured data and a specific question.
- Correlation is not causation: the forced-1G workaround "fixing" speeds never proved the link was the problem — and it wasn't.
