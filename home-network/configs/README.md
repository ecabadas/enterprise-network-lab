# Configs

I don't publish my actual device configurations verbatim — they contain network-specific details I don't put online (see the privacy note in the [home network README](../README.md)).

What I can say about the approach:

- **Gateway:** UniFi controller-managed. WAN on auto-negotiation with hardware acceleration on (per the vendor fix documented in [troubleshooting/wan-throughput-degradation.md](../troubleshooting/wan-throughput-degradation.md)). LAN segmented into VLANs for main, IoT, and guest traffic.
- **Wireless:** Separate SSIDs mapped to separate VLANs.
- **DNS/DHCP:** Served by the gateway per-VLAN.
- **Backups:** Console backups taken before any firmware change or maintenance window.

If a sanitized config export becomes useful for a specific write-up, it will go here with all identifying values replaced.
