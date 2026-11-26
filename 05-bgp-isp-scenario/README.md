# BGP ISP Scenario (GNS3)
A provider network (AS500) with two upstream ISPs and one customer. This folder holds the GNS3 project file `practical-scenario.gns3` and the startup configurations of the 7 routers in [`configs/`](configs/). The configs were read from the files only. Running state (neighbor status, routing tables) was not captured, so nothing here claims the lab was verified live.

## Topology
| Router | AS | Role |
|---|---|---|
| R1, R2, R3, R4 | 500 | Provider core |
| ISP1 | 200 | Upstream ISP, peers with R1 |
| ISP2 | 300 | Upstream ISP, peers with R2 |
| Cust1 | 64512 | Customer (private AS), peers with R3 |

## What the configs show
**Inside AS500**
- OSPF process 1, area 0, enabled per interface on the core links and on each router's Loopback10 (hello 1 s, dead 3 s on the serial links). R1 and R2 use `default-information originate always`.
- iBGP between all four core routers, using Loopback10 addresses (R1 1.1.1.1, R2 2.2.2.2, R3 3.3.3.3, R4 4.4.4.4). Only R1 and R2 have `next-hop-self`.
- R1 and R2 each advertise 150.1.0.0/30 (the R3 to Cust1 link) with a `network` statement.

**Towards the ISPs**
- R1 to ISP1 (AS200) and R2 to ISP2 (AS300): eBGP between loopbacks with `ebgp-multihop 2` on both ends, and `remove-private-as` on R1 and R2. Each pair has two static routes to the peer loopback, one per serial link.
- ISP1 and ISP2 use `redistribute connected` through a route-map (zz on ISP1, xx on ISP2) that permits only the three /24 loopback networks (ISP1: 100.1.1.0, 100.2.2.0, 100.3.3.0; ISP2: 200.1.1.0, 200.2.2.0, 200.3.3.0) via access list 1 and denies the rest.

**Towards the customer**
- R3 to Cust1 (AS64512): eBGP over the 150.1.0.0/30 link with a neighbor password (redacted in the published files) and `default-originate`. Cust1 advertises 150.1.1.0/24.
- R3 applies route-map `aa` outbound to Cust1. Its permit clause matches access list 10, and **access list 10 is not defined in R3's startup config** (only access list 1 exists, permitting 0.0.0.0). What the route-map does in practice was not tested here.

## Notes and limits
- Several neighbor descriptions in the configs are copy-pasted or misspelled (for example, R1 labels its neighbors 3.3.3.3 and 4.4.4.4 as `CONNECTION_TO_R2`, and R2 has `CONNECTOIN_TO_ISP2`). They are labels only and do not change behaviour.
- Startup configurations only. Neighbor states, learned routes and best-path results are not shown.
- Neighbor passwords were removed before publishing (`<REDACTED>`).
