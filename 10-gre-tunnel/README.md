# GRE Tunnel Lab

`gre-tunnel.pkt`: three routers named `hq`, `isp` and `branch`. Open with Packet Tracer 8.2.2 or newer.

## What is configured
- `hq` (11.0.0.2/24) and `branch` (11.1.0.2/24) each have a default route to the `isp` router.
- A GRE tunnel (`Tunnel1`) between hq and branch: 192.168.1.1/30 and 192.168.1.2/30, source is the WAN interface, destination is the other router's WAN address.
- Each side has a loopback (1.1.1.1 and 2.2.2.2). OSPF area 0 runs over the tunnel and advertises the loopbacks.

## What I practiced
- Tunnel source and destination
- Running a routing protocol over a tunnel between two sites that only reach each other through an ISP
