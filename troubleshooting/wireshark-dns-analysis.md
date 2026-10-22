# DNS Query and Response Packet Analysis (Wireshark)

Phase 3 evidence for the enterprise-network-lab: a live DNS lookup captured on the wire, showing the lab's Windows Server DNS role answering a client query.

## What was captured

Two screenshots from a Wireshark session on the lab network:

- `35-wireshark-dns-query.png` - the outbound DNS query (Frame 9, 76 bytes)
- `36-wireshark-dns-response.png` - the inbound DNS response (Frame 10, 92 bytes)

The exchange is between the DHCP-assigned workstation at 192.168.10.50 and the lab DNS server at 192.168.10.10 (Windows Server 2022, DNS + DHCP roles from Phase 2). Both MAC addresses carry the 08:00:27 OUI, which is VirtualBox's, consistent with the lab's virtualized environment.

## Packet 1: the query

| Layer | Observed value |
|---|---|
| Frame | 9, 76 bytes on the wire |
| Ethernet II | Src 08:00:27:f6:7b:6e (destination clipped in the capture) |
| IPv4 | Src 192.168.10.50, Dst 192.168.10.10 |
| UDP | Src port 51961, Dst port 53 |
| DNS | Transaction ID 0x0004; Flags 0x0100 (standard query, recursion desired); Questions: 1; Answer RRs: 0; Authority RRs: 0; Additional RRs: 0 |

Reading it: the workstation asks the server to resolve one hostname. Port 53 is DNS. The source port 51961 is an ephemeral port the client picked so it can match the reply to this specific lookup. The transaction ID 0x0004 tags this question; the response must carry the same ID. Flags 0x0100 is a standard query with recursion desired, meaning the client is asking the server to do the full lookup work.

## Packet 2: the response

| Layer | Observed value |
|---|---|
| Frame | 10, 92 bytes on the wire |
| Ethernet II | Src 08:00:27:16:e1:5c (destination clipped in the capture) |
| IPv4 | Src 192.168.10.10, Dst 192.168.10.50 |
| UDP | Src port 53, Dst port 51961 |
| DNS | Transaction ID 0x0004; Flags 0x8580 (standard query response, no error); Questions: 1; Answer RRs: 1; Authority RRs: 0; Additional RRs: 0 |

Reading it: the server answered with one record and no error. Three things prove this response belongs to the query above: the transaction ID 0x0004 matches, the ports are reversed exactly (53 to 51961), and the IP addresses are reversed exactly. Flags 0x8580 breaks down as response (not a query), recursion desired echoed back, recursion available, and RCODE 0, which means the name resolved successfully. No NXDOMAIN, no server failure.

## What this proves about the lab

- The DNS server role deployed in Phase 2 is live and resolving names for lab clients, not just installed.
- The full round trip works: query leaves the client, reaches 192.168.10.10, and a valid answer returns.
- The 16-byte growth from query (76) to response (92) is the answer record payload coming back.

## Known gaps in these captures

- The Queries subtree is collapsed in the query screenshot, so the exact hostname asked for is not visible.
- The Answers subtree is cut off at the bottom of the response screenshot, so the resolved IP address and TTL are not visible.
- The packet list pane, hex pane, and display filter are not in either crop.

Suggested follow-up: re-run the lookup with a `dns` display filter, expand the DNS tree fully (Queries and Answers), and capture the packet list pane as well. That would pin the hostname and the returned address to the evidence above.

## Files

- `screenshots/35-wireshark-dns-query.png`
- `screenshots/36-wireshark-dns-response.png`
