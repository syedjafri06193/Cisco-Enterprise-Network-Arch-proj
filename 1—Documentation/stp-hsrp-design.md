# STP + HSRP Design

## STP (Rapid-PVST)
- DIST1: root primary for VLANs 10,30,99; secondary for 20,40
- DIST2: root primary for VLANs 20,40; secondary for 10,30,99
- PortFast + BPDU Guard enabled on edge access ports

The STP root for each VLAN is the switch that is HSRP-active for it. If the
two disagree, an access switch's uplink to the active gateway can be the
blocked one, and that VLAN's traffic reaches its gateway the long way —
through the root, the other access switch, and back up.

## HSRP (Gateway Redundancy)
HSRP VIPs:
- VLAN 10: 10.10.10.1
- VLAN 20: 10.10.20.1
- VLAN 30: 10.10.30.1
- VLAN 40: 10.10.40.1
- VLAN 99: 10.10.99.1

Load distribution:
- DIST1 active: VLAN 10,30,99
- DIST2 active: VLAN 20,40

Tracking:
- Each distribution switch tracks its edge uplink (Gi1/0/48) and lowers its
  priority by 30 if the uplink fails: 110 → 80, below the standby's 90, so
  the standby takes over (both sides preempt). A decrement of 20 would only
  reach 90 — a tie, settled by the higher interface IP rather than by design.
