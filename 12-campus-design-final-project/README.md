# Campus Network Final Project

`final-project.pkt`: a small campus network in Packet Tracer. Open with Packet Tracer 8.2.2 or newer.

## What is in the file
- 2 routers, 3 multilayer switches and 4 access switches, OSPF area 0 between them.
- 3 VLANs (10, 20, 30), trunks to the access switches.
- Two multilayer switches share each VLAN gateway with HSRP (groups 10, 20, 30: 192.168.1.1, 192.168.2.1, 192.168.3.1).
- DHCP server at 200.200.200.4, reached with `ip helper-address` on the VLAN interfaces.
- An extended ACL `isolation_printer0` on VLAN 10: only 192.168.1.0/24 can reach the printer at 192.168.1.15.
- 6 PCs, 4 servers, 3 printers, 3 access points and a few IoT devices.

## What I practiced
- VLANs and trunks, inter-VLAN routing on multilayer switches
- HSRP for the default gateway
- DHCP relay
- A named extended ACL
