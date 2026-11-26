# Extended ACL Lab

`lab08-extended-acl.pkt`: 3 routers running OSPF (area 0), 3 switches, 2 PCs and a server at 20.0.0.2. Open with Packet Tracer 8.2.2 or newer.

## What is configured
- ACL 101 is applied inbound on the 30.0.0.0/8 LAN interface. It denies ICMP echo from host 30.0.0.3 to the server 20.0.0.2 and permits everything else.
- ACL 100 is also written (denies HTTP from host 30.0.0.2 to the server) but is not applied to an interface in this file.

## What I practiced
- Extended ACL syntax with `deny` and `permit ip any any`
- Applying an ACL inbound on an interface
