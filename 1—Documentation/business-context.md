# Business Context (Fictional Ramp Office)

This design supports a mid-size Ramp office with the following requirements:

## Users / Segments
- **Engineering (VLAN 30):** dev workstations, internal tooling access, broader east-west access
- **Finance (VLAN 20):** accounting operations; requires stricter segmentation due to sensitive workflows
- **HR (VLAN 10):** People Ops endpoints and HR systems access
- **Guest (VLAN 40):** visitor and contractor Wi-Fi; must not access internal resources

## Network Priorities
- High availability for user default gateways
- Secure isolation of Guest traffic
- Restricted access between Finance and Engineering
- Centralized routing at distribution with predictable L2 behavior (STP root placement)
- Simple, testable internet access through NAT at the edge
