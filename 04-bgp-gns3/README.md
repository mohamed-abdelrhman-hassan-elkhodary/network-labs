# BGP Lab (GNS3 2.2.59)
- 5 Cisco 7200 routers (Dynamips, IOS c7200-adventerprisek9-mz.124-24.T5), 5 serial links
- Three autonomous-system groups drawn on the topology: AS1, AS2 and AS100
- ISP1 is dual-linked to E1; E1 - EX - E2 forms a transit path; ISP2 connects to E2
- Screenshot (`screenshots/show-ip-bgp.jpg`): ISP1 log line "BGP-5-ADJCHANGE: neighbor 3.3.3.3 Up" and `show ip bgp` listing the networks ISP1 originates (1.1.1.1/32, 10.1.1.0/30, 10.1.1.4/30 and four 180.x.x.0/24 networks)

## Not shown yet
Routes learned from another AS and best-path selection.

## Design goal (configs not included in this repo)
The internal networks run an internal routing protocol, and BGP runs toward the ISP. Redistribution with route-maps is used to control which routes are advertised. The router configurations are not part of this repo, so this is the intended design and is not shown by the files here.
