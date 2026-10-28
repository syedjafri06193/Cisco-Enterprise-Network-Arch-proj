# Validation Checklist

## VLAN / Trunking
- show vlan brief
- show interfaces trunk

## STP
- show spanning-tree vlan 10
- show spanning-tree vlan 20
Confirm DIST1 is root for VLANs 10, 30 and 99 and DIST2 is root for VLANs 20
and 40 — matching the HSRP active switch for each VLAN.

## HSRP
- show standby brief
Confirm correct active/standby per VLAN.

## Failover
- Shut DIST1 Gi1/0/48 (uplink to EDGE1)
- show standby brief on DIST2: active for every VLAN
- From an HR host (VLAN 10): reach the internet. EDGE1's floating static
  (AD 10) via DIST2 carries the return traffic: `show ip route 10.10.10.0`
- No shut Gi1/0/48: DIST1 preempts back for VLANs 10, 30, 99

## Inter-VLAN Routing
- Ping HR ↔ Engineering (allowed by baseline)
- Ping Finance → Engineering (should fail due to ACL)

## Guest Policy
- From Guest host: ping internal 10.10.20.x (should fail)
- From Guest host: reach internet (should succeed with NAT)

## NAT (EDGE1)
- show ip nat translations
- show ip nat statistics
