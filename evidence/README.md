# Testing Evidence

Place the actual Cisco Packet Tracer screenshots for the tests in `../testing-evidence.md` in this folder.

## Required filenames

| File | Evidence required | Current observed status |
| --- | --- | --- |
| `01-dhcp-vlan40.png` | DHCP client address and gateway | Screenshot still needed |
| `02-gateway-ping.png` | Successful client-to-default-gateway ping | Observed during testing; clean evidence screenshot still needed |
| `03-inter-vlan-routing.png` | Authorized inter-VLAN connectivity | Screenshot still needed |
| `04-external-connectivity.png` | Successful internal client to external test server | Observed to 203.0.113.10 |
| `05-nat-translations.png` | `show ip nat translations` | Observed active translations on R1 |
| `06-nat-statistics.png` | `show ip nat statistics` | Observed: 4 dynamic translations, 12 hits |
| `07-routing-table.png` | Routing table | Screenshot still needed |
| `08-cctv-acl-test.png` | CCTV gateway permitted, Admin blocked, external permitted | Observed: gateway 0% loss; Admin 100% loss; external 0% loss |
| `09-guest-isolation.png` | Guest gateway permitted, Admin blocked, external permitted | Observed: gateway 0% loss; Admin 100% loss; external 0% loss |
| `10-ssh-management.png` | Authorized SSH management session | Observed from PC-Admin to SW1-Core |

## Additional useful evidence

- `11-management-reachability.png` — PC-Admin successfully pinged SW1/SW2/SW3 management addresses `192.168.99.2`, `.3`, and `.4`.
- `12-final-topology.png` — final Packet Tracer topology with required links visible.
- `13-acl-counters.png` — R1 `show ip access-lists` showing GUEST-ISOLATION and CCTV-ISOLATION match counters.

## Evidence integrity

Only screenshots of results actually observed in Packet Tracer should be uploaded. Do not mark DHCP, routing-table, or inter-VLAN evidence complete until the corresponding final screenshot has been captured.
