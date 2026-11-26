# Network Infrastructure Using VoIP and IoT System (Graduation Project, team project)
Faculty of Engineering, Tanta University, Electronics and Communications Engineering, 2026.
Tool: Cisco Packet Tracer 8.2.2.

## What the file contains (counted from the saved configuration)
- 7 routers (4 Cisco 2811, 3 Cisco 2911), 4 multilayer switches (3560-24PS), 13 access switches (2960-24TT), 12 access points
- 17 PCs, 1 laptop, 1 tablet, 9 printers, 10 Cisco IP phones, 7 servers
- 11 microcontroller boards with sensors and actuators (cameras, RFID readers, door locks, fire sprinklers, sirens, lights, air conditioners)

## What was configured
- 19 VLAN interfaces on the multilayer switches (VLAN 1, 10, 19, 20, 30, 40, 50, 60, 70, 80, 90, 100, 111, 200, 210, 220, 230, 240, 250), 802.1Q trunks
- OSPF process 1, area 0, across routers and multilayer switches
- HSRP gateway redundancy: 16 groups on 4 multilayer switches
- Rapid PVST spanning tree
- DHCP relay for the VLANs
- Cisco IP telephony (telephony-service) on 2 routers with 10 phones and 32 extensions
- 7 named extended ACLs separating camera, RFID and fire-system VLANs
- HQ to Branch site-to-site tunnel protected by IPsec (AES-256, SHA, ACL-defined traffic)
- SSH version 2 on 12 devices

## Files
The project file is not uploaded yet.

## Not claimed here
Port Security, AAA, NAT and VLSM are not in this file.
