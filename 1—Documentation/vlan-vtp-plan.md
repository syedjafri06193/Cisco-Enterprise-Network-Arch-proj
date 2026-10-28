# VLAN & VTP Plan

## VLAN Database
- 10 RAMP-HR
- 20 RAMP-FIN
- 30 RAMP-ENG
- 40 RAMP-GUEST
- 99 RAMP-MGMT
- 999 NATIVE-DROP

## VTP
Domain: RAMP-CAMPUS
Password: vtpRAMP!
Version: 2

Roles:
- DIST1: VTP Server
- DIST2: VTP Server
- ACCESS1/2: VTP Client

Notes:
- VLAN 999 is used as the native VLAN on trunks.
- Trunks explicitly configured; DTP disabled (nonegotiate).
