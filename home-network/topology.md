# Network Topology & Inventory

## Topology

```
                    Xfinity coax
                         |
              Arris Surfboard S33
            (DOCSIS 3.1 modem, 2.5 GbE port)
                         |  Cat6
              Ubiquiti Cloud Gateway Max
        (gateway, firewall, UniFi controller)
                         |  LAN
                   PoE switch
                    /        \
        Patch panel           UniFi access point
       (in-wall drops)        (segmented wireless)
        /      \
   Office    Other rooms
```

Physical path: ISP coax → modem → gateway WAN (2.5 GbE) → gateway LAN → PoE switch → patch panel → room drops; access point powered via PoE.

## Inventory

| Device | Model | Role |
|---|---|---|
| Modem | Arris Surfboard S33 | DOCSIS 3.1 modem, 2.5 GbE uplink |
| Gateway | Ubiquiti Cloud Gateway Max (base, no storage) | Router, firewall, UniFi controller host |
| Switch | 8-port PoE switch | LAN distribution, AP power |
| Access point | UniFi AP | Wireless coverage |
| Patch panel | 12-port Cat6 | Terminates in-wall drops |
| UPS | APC Back-UPS (600VA) | Battery backup for modem, gateway, and switch |

## Segmentation

- Separate SSIDs on separate VLANs for main, IoT, and guest traffic (VLAN IDs and subnets obscured)
- Wired drops home-run to the patch panel

## Notes

- IP addresses, MAC addresses, and wireless network names are obscured in this repo (see the privacy note in the [README](README.md)).
- Firmware versions change over time; the versions in effect during the throughput investigation are documented in [troubleshooting/wan-throughput-degradation.md](troubleshooting/wan-throughput-degradation.md).
