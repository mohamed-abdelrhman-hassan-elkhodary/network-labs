# OSPF Areas, Stub, NSSA and Redistribution (Packet Tracer)

`ospf-areas.pkt`: 7 routers (R1 to R7). Open with Packet Tracer 8.2.2 or newer. A GNS3 multi-area lab is in `06-ospf-multi-area`.

## What is configured
- OSPF process 1 with router IDs 1.1.1.1 to 5.5.5.5, enabled per interface (`ip ospf 1 area N`).
- Area 0 on R2, R3 and R4 links, area 2 on R1 and R2 as a stub area, area 1 on R4 and R5 as an NSSA.
- R3 redistributes RIP into OSPF and OSPF into RIP, to a RIP network (192.168.1.0 to 192.168.4.0, loopbacks on R6). R5 redistributes its RIP network (192.168.5.0, with R7) into OSPF.

## What I practiced
- Multiple areas, stub and NSSA area types
- Redistribution between RIP and OSPF
