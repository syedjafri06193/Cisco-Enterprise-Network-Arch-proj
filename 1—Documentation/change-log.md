# Change Log

## v1.1
- STP root per VLAN now matches the HSRP active switch (DIST1: 10,30,99;
  DIST2: 20,40); previously DIST1 was root for every VLAN
- HSRP tracking decrement 20 → 30, so an uplink failure drops the active
  switch below the standby instead of tying with it
- EDGE1: floating static return routes (AD 10) via the other distribution
  switch, so return traffic survives a distribution switch or uplink failure
- Validation checklist: failover test

## v1.0
- Implemented VLAN segmentation + VTP domain
- Rapid-PVST root design at distribution
- HSRP VIPs for all VLANs with load distribution
- ACLs for Guest isolation + Finance segmentation
- NAT overload at the edge
- Added draw.io diagram and validation checklist
