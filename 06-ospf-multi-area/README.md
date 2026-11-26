# OSPF Multi-Area (8 routers)
Eight routers (R1 to R8) running OSPF process 1 across five areas. This folder holds the GNS3 project file `ospf.gns3` and the startup configurations in [`configs/`](configs/). The configs were read from the files only. Running state (neighbors, routing tables) was not captured, so nothing here claims the lab was verified live.

## Areas and links
| Area | Routers | Network |
|---|---|---|
| 0 (backbone) | R1, R2, R4, R6 | 10.100.1.0/24 (FastEthernet) |
| 23 | R2, R3 | 10.23.1.0/24 |
| 45 | R4, R5 | 10.45.1.0/24 |
| 67 | R6, R7 | 10.67.1.0/24 |
| 78 | R7, R8 | 10.78.1.0/24 |

## What the configs show
- OSPF is enabled per interface (`ip ospf 1 area N`) and each router has a router-id set (R1 1.1.1.1 up to R8 8.8.8.8).
- R2, R4 and R6 each have one interface in area 0 and one in another area (23, 45 and 67), so they sit on the area borders.
- R1 is in area 0 only. It has `redistribute static metric-type 1 subnets` and four static routes to Null0 (172.31.0.0/24, 172.31.1.0/24, 172.31.2.0/24, 172.31.3.0/24), so those prefixes are injected into OSPF as external type 1 routes.
- R7 connects area 67 (to R6) and area 78 (to R8).

## Observation: area 78
Area 78 connects to the rest of the network only through R7, and R7 has no interface in area 0. There is no `virtual-link` in any of the configs. In standard OSPF an area must attach to area 0 (directly or through a virtual link), so area 78 as configured is not attached to the backbone. This is an observation from the startup configs. Whether routes reach area 78 in the running lab was not tested here.

## Notes and limits
- Startup configurations only. Neighbor states, routing tables and reachability tests are not shown.
- No passwords or keys are set in the configs.
