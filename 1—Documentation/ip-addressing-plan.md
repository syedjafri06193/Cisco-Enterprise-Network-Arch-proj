# IP Addressing & Subnetting Plan

## VLAN Subnets
- VLAN 10 (RAMP-HR):    10.10.10.0/24   VIP: 10.10.10.1
- VLAN 20 (RAMP-FIN):   10.10.20.0/24   VIP: 10.10.20.1
- VLAN 30 (RAMP-ENG):   10.10.30.0/24   VIP: 10.10.30.1
- VLAN 40 (RAMP-GUEST): 10.10.40.0/24   VIP: 10.10.40.1
- VLAN 99 (RAMP-MGMT):  10.10.99.0/24   VIP: 10.10.99.1
- VLAN 999: Native/unused (no SVI)

## Device Management (examples)
- DIST1 mgmt:   10.10.99.11/24
- DIST2 mgmt:   10.10.99.12/24
- ACCESS1 mgmt: 10.10.99.21/24
- ACCESS2 mgmt: 10.10.99.22/24

## Transit Links (/30)
- DIST1 ↔ EDGE1: 10.255.1.0/30  (DIST1 .1 / EDGE1 .2)
- DIST2 ↔ EDGE1: 10.255.2.0/30  (DIST2 .1 / EDGE1 .2)
- DIST1 ↔ DIST2: 10.255.10.0/30 (DIST1 .1 / DIST2 .2)

## Internet (example ISP)
- EDGE1 outside: 203.0.113.2/30
- ISP next hop:  203.0.113.1
