# Testing Evidence — Stats SA Mafikeng Field Office

## Purpose
This document records the tests required to demonstrate that the Cisco Packet Tracer implementation works. Capture screenshots from Packet Tracer after each successful test and place them in `evidence/`.

## Test Matrix
| ID | Test | Expected result | Evidence to capture |
| --- | --- | --- | --- |
| T01 | DHCP on VLAN 30/40/50/60 | Client receives an address from the correct subnet and gateway. | PC IP Configuration screen |
| T02 | Default gateway | Client successfully pings its VLAN gateway. | Command Prompt ping output |
| T03 | Inter-VLAN routing | Authorized client reaches an internal service/NVR. | Ping or application test |
| T04 | NAT connectivity | Internal client reaches external test server `198.51.100.10`. | Ping output |
| T05 | NAT translation | R1 shows an active inside-local to inside-global translation. | `show ip nat translations` |
| T06 | NAT statistics | R1 reports NAT inside/outside interfaces and translations. | `show ip nat statistics` |
| T07 | Routing table | SW-CORE has connected VLAN routes and a default route to R1; R1 has a return route to `172.30.66.0/23`. | `show ip route` |
| T08 | CCTV isolation | CCTV camera can reach the NVR, but camera traffic to normal user VLANs is denied by policy. | Successful NVR test + denied test |
| T09 | Guest isolation | Guest/training client reaches permitted internet resources but cannot reach protected internal VLANs. | Ping/test results |
| T10 | SSH management | Authorized management host can SSH to infrastructure; unauthorized user VLAN cannot. | SSH session + failed attempt |

## NAT/PAT Verification
On R1, run:

```text
show ip interface brief
show ip route
show ip nat translations
show ip nat statistics
```

From an internal client, generate traffic to the external test server:

```text
ping 198.51.100.10
```

Then run `show ip nat translations` again. The evidence should show the internal address translated to the R1 outside address `203.0.113.2`.

## Suggested Evidence Filenames
```text
evidence/
├── 01-dhcp-vlan40.png
├── 02-gateway-ping.png
├── 03-inter-vlan-routing.png
├── 04-external-connectivity.png
├── 05-nat-translations.png
├── 06-nat-statistics.png
├── 07-routing-table.png
├── 08-cctv-acl-test.png
├── 09-guest-isolation.png
└── 10-ssh-management.png
```

## Evidence Quality Requirements
- Include the Packet Tracer topology in at least one screenshot.
- Keep the command window visible when CLI verification is required.
- Ensure IP addresses and device names are readable.
- Do not submit simulated results that were not actually observed.
- Record any failed test and the corrective action before taking the final screenshot.

## Final Review Checklist
- [ ] `.pkt` opens successfully in Cisco Packet Tracer.
- [ ] All links required by the topology are up.
- [ ] VLANs and gateways are configured.
- [ ] DHCP clients receive correct addresses.
- [ ] Inter-VLAN routing works where permitted.
- [ ] NAT inside/outside is configured on R1.
- [ ] External connectivity works.
- [ ] NAT translations are visible on R1.
- [ ] CCTV ACL restrictions work.
- [ ] Guest restrictions work.
- [ ] SSH management works from an authorized host.
- [ ] Evidence screenshots are added to `evidence/`.