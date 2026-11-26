# NAT and PAT Labs

Two Packet Tracer labs on the same topology: a LAN behind a NAT router, 3 other routers running OSPF, and 2 servers. Open with Packet Tracer 8.2.2 or newer.

| File | What is configured |
|---|---|
| `lab10-dynamic-nat.pkt` | Dynamic NAT. Inside LAN 192.168.1.0/24, pool `a` of 170.160.1.1 to 170.160.1.4, standard ACL 1 selects the inside hosts, default route out. |
| `lab11-pat.pkt` | PAT. Same inside LAN, pool `aa` with the single address 170.160.1.1, `ip nat inside source list 2 pool aa overload`. |

## What I practiced
- `ip nat inside` and `ip nat outside` on the interfaces
- A NAT pool and an ACL that selects traffic to translate
- The `overload` keyword for PAT
- OSPF between the other routers and a default route on the NAT router
