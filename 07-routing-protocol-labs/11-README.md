# Routing Protocol Labs

Four small Packet Tracer labs, one routing method each. Open with Packet Tracer 8.2.2 or newer.

| File | What is configured |
|---|---|
| `lab04-static-routing.pkt` | 3 routers in a triangle, each with a LAN (DHCP pools on the routers). Static routes to the other two LANs, with a route through each neighbor. |
| `lab05-rip.pkt` | 5 routers in a ring, 2 LANs with DHCP. RIP version 2 on every router. |
| `lab06-eigrp.pkt` | Same topology as lab 5. EIGRP AS 1 on every router with `auto-summary`. The RIP v2 config from lab 5 is still on the routers too, so both protocols are configured. One router link is shut down. |
| `lab07-ospf-broadcast.pkt` | 3 routers on one shared 10.0.0.0/8 broadcast segment through a switch, OSPF process 1, all in area 0. Two LANs with DHCP. |

## What I practiced
- Static routes and a second path per destination
- RIP v2 with `network` statements
- EIGRP with `router eigrp 1` and `network` statements
- OSPF on a broadcast segment

## Notes
- Addressing uses classful-looking ranges (10.0.0.0/8, 11.0.0.0/8 and so on) to keep the labs simple.
- Lab 6 is lab 5 with EIGRP added, so it still has the RIP config under it.
