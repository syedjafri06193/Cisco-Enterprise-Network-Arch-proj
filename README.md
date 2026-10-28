# Ramp Enterprise Network Design (Cisco-Style Architecture)

This repository contains a Cisco-style enterprise campus network design for a fictional mid-size Ramp office environment supporting Finance operations, Engineering teams, HR, and guest access. The design focuses on segmentation, high availability, loop prevention, and secure internet edge connectivity.

## Objectives
- Segment users by business function (HR, Finance, Engineering, Guest)
- Provide resilient default gateways (HSRP)
- Prevent L2 loops (Rapid-PVST)
- Enable inter-VLAN routing at the distribution layer (SVIs)
- Enforce policy with ACLs
- Provide secure internet access via NAT (PAT)
- Document IP/subnet plan and operational validation steps
- Deliver a reproducible diagram (draw.io)

## Skills Demonstrated
- VLAN / VTP
- STP (Rapid-PVST)
- HSRP
- ACLs
- NAT
- IP Addressing & Subnetting
- Enterprise Network Design + Documentation

---

## Topology (Campus Model)
- **Distribution Layer:** 2x L3 switches (DIST1, DIST2)
- **Access Layer:** 2x L2 switches (ACCESS1, ACCESS2)
- **Internet Edge:** 1x router (EDGE1) for NAT + upstream routing
- **Redundancy**
  - HSRP VIP per VLAN across DIST1/DIST2
  - STP root controlled at distribution

---

## VLANs
| VLAN | Name        | Purpose |
|------|-------------|---------|
| 10   | RAMP-HR     | People Ops / HR workstations |
| 20   | RAMP-FIN    | Finance/Accounting endpoints |
| 30   | RAMP-ENG    | Engineering workstations |
| 40   | RAMP-GUEST  | Guest Wi-Fi / contractor BYOD |
| 99   | RAMP-MGMT   | Network device management |
| 999  | NATIVE-DROP | Native/unused VLAN for trunks |

---

## IP Plan (Summary)
| VLAN | Subnet           | HSRP VIP Gateway |
|------|------------------|------------------|
| 10   | 10.10.10.0/24    | 10.10.10.1 |
| 20   | 10.10.20.0/24    | 10.10.20.1 |
| 30   | 10.10.30.0/24    | 10.10.30.1 |
| 40   | 10.10.40.0/24    | 10.10.40.1 |
| 99   | 10.10.99.0/24    | 10.10.99.1 |

Transit:
- DIST1 ↔ EDGE1: 10.255.1.0/30
- DIST2 ↔ EDGE1: 10.255.2.0/30
- DIST1 ↔ DIST2: 10.255.10.0/30

---

## Documentation

All documentation lives in [`1—Documentation/`](1—Documentation/README.md):
business context, IP plan, VLAN/VTP plan, STP/HSRP design, security ACLs,
NAT and internet edge, the validation checklist and the change log.

---

## Policy Highlights
- Guest VLAN is **internet-only** (blocked from RFC1918 internal ranges)
- Finance VLAN is **restricted** (blocked from Engineering VLAN)
- HR VLAN is **open baseline** (can be tightened further if needed)

---

## How to Use
- Load configs from `configs/` into Packet Tracer / GNS3 / EVE-NG.
- Open diagram: `diagrams/ramp-enterprise-network.drawio`
- Validate using: [`1—Documentation/validation-checklist.md`](1—Documentation/validation-checklist.md)

---

## Project Deliverables
- Configs (DIST/ACCESS/EDGE)
- Subnetting + IP plan
- VLAN/VTP plan
- STP + HSRP design
- ACL design
- NAT edge design
- Diagram
- Validation checklist

---

