# Security ACLs

## Guest (VLAN 40) — Internet Only
Inbound on VLAN 40 SVI:
- Deny access to RFC1918 internal ranges (10/8, 172.16/12, 192.168/16)
- Permit all else (internet)

## Finance (VLAN 20) — Restricted East/West
Inbound on VLAN 20 SVI:
- Deny Finance → Engineering subnet (VLAN 30)
- Permit other traffic (internet + allowed internal)

## HR (VLAN 10) — Baseline
Inbound on VLAN 10 SVI:
- Permit HR → any (baseline; can be tightened to only approved services)

## Known gaps

**DHCP.** The design has no DHCP service (no pools, no `ip helper-address`).
When one is added, note that `GUEST_IN` (and any SVI ACL that ends in an
implicit deny) will drop DHCP DISCOVER/REQUEST packets, because they are sent
from `0.0.0.0`, which none of the entries match. Add, before the deny lines:

```
ip access-list extended GUEST_IN
 permit udp host 0.0.0.0 eq bootpc host 255.255.255.255 eq bootps
```

**Management plane.** The configs set no device authentication. Before
deploying, on every device:

```
service password-encryption
enable secret <secret>
username netadmin privilege 15 secret <secret>
ip domain-name ramp.example
crypto key generate rsa modulus 2048
ip ssh version 2
line vty 0 15
 login local
 transport input ssh
```

and restrict VTY access to the management VLAN (99) with an `access-class`.

**VTP.** The VTP password is stored in clear text and both distribution
switches are VTP servers. Consider VTP version 3 (primary server and hidden
password) or transparent mode, so a switch with a higher revision number
cannot overwrite the VLAN database.
