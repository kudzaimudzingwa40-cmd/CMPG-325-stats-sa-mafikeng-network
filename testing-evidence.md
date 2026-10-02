# Network Testing and Verification

## Test Results

| Test | Source / component | Destination / check | Result |
| --- | --- | --- | --- |
| Management connectivity | PC-Admin | SW1-Core 192.168.99.2 | Successful |
| Management connectivity | PC-Admin | SW2-Access 192.168.99.3 | Successful |
| Management connectivity | PC-Admin | SW3-Access 192.168.99.4 | Successful |
| SSH management | PC-Admin | SW1-Core | Successful login |
| Guest gateway | PC-Guest | 192.168.50.1 | 4/4 replies |
| Guest isolation | PC-Guest | Admin 192.168.10.21 | Blocked, 100% loss |
| Guest external access | PC-Guest | 203.0.113.10 | 4/4 replies |
| CCTV gateway | PC-CCTV | 192.168.60.1 | 4/4 replies |
| CCTV isolation | PC-CCTV | Admin 192.168.10.21 | Blocked, 100% loss |
| CCTV external access | PC-CCTV | 203.0.113.10 | 4/4 replies |
| NAT/PAT statistics | R1 | Translation statistics | 4 dynamic translations, 12 hits |
| Guest ACL | R1 | GUEST-ISOLATION | Deny and permit counters recorded |
| CCTV ACL | R1 | CCTV-ISOLATION | Deny and permit counters recorded |

## NAT/PAT Verification

R1 identified GigabitEthernet0/0 as the outside interface and the internal VLAN subinterfaces on GigabitEthernet0/1 as inside interfaces. NAT statistics displayed four dynamic translations and 12 hits after traffic was generated toward the external test server.

## Guest Network Security

The Guest host successfully reached its default gateway and the external test server. Traffic from the Guest VLAN to the Administration network was denied. The GUEST-ISOLATION ACL recorded matches for both denied internal traffic and permitted traffic.

## CCTV Network Security

The CCTV host successfully reached its default gateway and the external test server. Traffic from the CCTV VLAN to the Administration network was denied. The CCTV-ISOLATION ACL recorded matches for both denied internal traffic and permitted traffic.

## Infrastructure Management

PC-Admin successfully reached the three switch management addresses on VLAN 99. SSH access to SW1-Core was also successfully established, demonstrating remote administrative access through the management network.

## Test Conclusion

The recorded tests demonstrate that the implemented security policies behave as designed: restricted VLANs retain required gateway/external connectivity while access to protected internal networks is denied. NAT/PAT and infrastructure management were also demonstrated during verification.
