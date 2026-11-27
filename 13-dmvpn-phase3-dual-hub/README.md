# Dual-hub DMVPN Phase 3 (GNS3)
A DMVPN with two hubs and two spokes, EIGRP over the tunnel, and IPsec protection on the tunnel interface. Built and tested in GNS3 2.2.59 on Dynamips (c7200, IOS 12.4(24)T5). This is a lab, not a production design.

Files: the GNS3 project and everything else in `Dmvpn.zip`, the startup configs of the five routers in [`configs/`](configs/), and three terminal screenshots (the `.jpg` files in this folder).

## Topology
| Router | Role | Tunnel0 | NBMA (physical) | Loopback10 |
|---|---|---|---|---|
| R1 | Hub | 10.0.0.1 | 15.0.0.1 | 1.1.1.1 |
| R3 | Hub | 10.0.0.2 | 25.0.0.2 | 2.2.2.2 |
| R4 | Spoke | 10.0.0.3 | 35.0.0.3 | 3.3.3.3 |
| R2 | Spoke | 10.0.0.4 | 45.0.0.4 | 4.4.4.4 |
| Internet | Underlay router | none | 15.0.0.5, 25.0.0.5, 35.0.0.5, 45.0.0.5 | none |

Each of the four routers connects to the Internet router over its own serial link (15/25/35/45.0.0.0/8) and has a FastEthernet LAN behind it (192.168.1.0 to 192.168.4.0, /24). The Internet router only carries those links. Hostnames in the configs are the names above.

## What the configs show
- **DMVPN Phase 3.** All four routers use `tunnel mode gre multipoint` with NHRP network-id 1234. The hubs have `ip nhrp redirect`. The spokes have `ip nhrp shortcut`.
- **Two hubs.** Each spoke lists both hubs as `ip nhrp nhs` (10.0.0.1 and 10.0.0.2) with static NHRP and multicast maps to both.
- **EIGRP 100** over the tunnel network (10.0.0.0/24), loopbacks and LANs. The hubs have `no ip split-horizon eigrp 100`.
- **IPsec.** ISAKMP policy 10 (3DES, MD5, pre-shared key, group 2), transform set ABC (`esp-3des esp-sha-hmac`, transport mode), and `tunnel protection ipsec profile IPROF` on Tunnel0 of all four routers.
- **Underlay.** Each router has a default route out of its serial interface.

## What was verified in the running lab
- **Hub R1 (`show dmvpn`).** Both spokes are registered as dynamic peers, 10.0.0.3 and 10.0.0.4, state UP ([screenshot](r1-show-dmvpn-and-isakmp-sa%5B1%5D.jpg)).
- **Hub R1 (`show crypto isakmp sa`).** Four ISAKMP SAs, all `QM_IDLE` and `ACTIVE` (same screenshot).
- **Spoke to spoke (R4 to R2).** `traceroute 4.4.4.4 source 3.3.3.3` from R4. The first run goes through the hubs (10.0.0.1 and 10.0.0.2) in 2 hops. The second run goes straight to 10.0.0.4 in 1 hop, so the NHRP shortcut formed ([screenshot](r4-traceroute-to-4.4.4.4-shortcut%5B1%5D.jpg)).
- **R3 to R2.** `traceroute 4.4.4.4 source 2.2.2.2` from R3 reaches 10.0.0.4 in 1 hop ([screenshot](r3-traceroute-to-4.4.4.4%5B1%5D.jpg)). R3 is a hub, so this is hub to spoke.

Only R1's DMVPN and ISAKMP tables were captured. The same outputs on R2, R3 and R4 were not.

## Known limits
- **The two hubs are not registered with each other.** On R1, the entry for R3 (10.0.0.2) shows state `NHRP` with up/down time `never` and the `S` (static) flag. Neither hub has an `ip nhrp nhs` line for the other hub. The spokes use both hubs.
- **R1's LAN is not advertised.** R1's EIGRP does not include 192.168.1.0, unlike the other routers.
- **Lab security settings.** The pre-shared key is in the startup configs in plain text (`cisco123`), and 3DES with MD5 is old. Fine for a lab, not for real use.
- Routing tables on the spokes and the NHRP cache after the shortcut were not captured.
