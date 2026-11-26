# BGP Lab (GNS3 2.2.59)
- 5 Cisco 7200 routers (Dynamips, IOS c7200-adventerprisek9-mz.124-24.T5), 5 serial links
- Three autonomous systems: AS1 (ISP1), AS100 (E1, EX, E2) and AS2 (ISP2)
- ISP1 is dual-linked to E1; E1 - EX - E2 forms the AS100 core; ISP2 connects to E2
- Startup configurations of all five routers are in [`configs/`](configs/)
- Screenshot (`screenshots/show-ip-bgp.jpg`): ISP1 log line "BGP-5-ADJCHANGE: neighbor 3.3.3.3 Up" and `show ip bgp` on ISP1 listing its own locally originated networks (1.1.1.1/32, 10.1.1.0/30, 10.1.1.4/30 and four 180.x.x.0/24 networks)

## Design (from the configs)
- **AS100 (E1, EX, E2)** runs iBGP. E1 and E2 peer with EX and use `next-hop-self`. OSPF process 1 (area 0) is enabled on the internal links 128.107.1.0/24 and 128.107.2.0/24, and E1 and E2 use `default-information originate always`.
- **ISP1 (AS1) to E1 (AS100)**: eBGP between loopbacks (ISP1 Loopback1 1.1.1.1, E1 Loopback3 3.3.3.3) with `ebgp-multihop`. Two static routes on each side (one per serial link) provide reachability to the peer loopback.
- **ISP1 outbound policy**: ISP1 uses `redistribute connected` and a route-map `isp1` on its outbound updates to E1. The route-map denies the prefixes matched by access list 1 (1.1.1.1/32, 10.1.1.0/30 and 10.1.1.4/30, the loopback and the links between ISP1 and E1) and permits everything else.
- **E2 (AS100) to ISP2 (AS2)**: eBGP over the directly connected 192.168.1.0/30 link. ISP2 originates 200.0.0.0.
