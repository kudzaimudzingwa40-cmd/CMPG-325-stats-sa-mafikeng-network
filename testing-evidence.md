# Verification and Evidence Register

## Purpose

This document defines the acceptance checks for the Packet Tracer implementation and records only outcomes actually observed during the test session. Screenshots belong in `evidence/`.

## Acceptance Matrix

| ID | Verification | Expected result | Observed status |
| --- | --- | --- | --- |
| T01 | DHCP addressing | Endpoint receives an address and gateway from the correct VLAN | **Evidence not captured** |
| T02 | Default gateway | Endpoint reaches its VLAN gateway | **Observed** for Guest and CCTV |
| T03 | Inter-VLAN routing | Authorized business VLAN traffic routes successfully | **Dedicated evidence not captured** |
| T04 | External connectivity | Permitted internal endpoint reaches `203.0.113.10` | **Observed** from Guest and CCTV |
| T05 | NAT translation | R1 creates dynamic translations for permitted outbound traffic | **Observed** |
| T06 | NAT statistics | Correct inside/outside roles and non-zero hits/translations | **Observed: 4 dynamic translations, 12 hits** |
| T07 | Routing table | Connected VLAN routes and required external reachability are present | **Final screenshot not captured** |
| T08 | CCTV isolation | CCTV reaches its gateway/external target but not Admin | **Observed** |
| T09 | Guest isolation | Guest reaches its gateway/external target but not Admin | **Observed** |
| T10 | SSH management | Authorized administrator establishes SSH management session | **Observed** |
| T11 | Management reachability | Admin host reaches all switch management addresses | **Observed** |
| T12 | ACL enforcement | Guest/CCTV ACL counters increment for test traffic | **Observed** |

## Observed Results

### Guest isolation

- `192.168.50.1`: 4/4 replies, 0% loss.
- Admin host `192.168.10.21`: blocked, 100% loss.
- External server `203.0.113.10`: 4/4 replies, 0% loss.

### CCTV isolation

- `192.168.60.1`: 4/4 replies, 0% loss.
- Admin host `192.168.10.21`: blocked, 100% loss.
- External server `203.0.113.10`: 4/4 replies, 0% loss.

### NAT/PAT

R1 reported:

- outside interface: `GigabitEthernet0/0`;
- inside interfaces: `GigabitEthernet0/1.10` through `.60`;
- 4 dynamic translations; and
- 12 NAT hits.

### ACL enforcement

`GUEST-ISOLATION` recorded four matches on the deny rule toward the Admin subnet and eight matches on the final permit rule. `CCTV-ISOLATION` recorded the same observed deny/permit match counts.

### Management

PC-Admin successfully reached switch management addresses `192.168.99.2`, `192.168.99.3`, and `192.168.99.4`. An authorized SSH session to SW1-Core was also observed.

## Recommended Evidence Filenames

```text
evidence/
├── 01-dhcp-addressing.png
├── 02-gateway-ping.png
├── 03-inter-vlan-routing.png
├── 04-external-connectivity.png
├── 05-nat-translations.png
├── 06-nat-statistics.png
├── 07-routing-table.png
├── 08-cctv-acl-test.png
├── 09-guest-isolation.png
├── 10-ssh-management.png
├── 11-management-reachability.png
├── 12-final-topology.png
└── 13-acl-counters.png
```

## Verification Commands

On R1:

```text
show ip interface brief
show ip route
show ip nat translations
show ip nat statistics
show ip access-lists
show ip interface g0/1.50
show ip interface g0/1.60
```

From endpoints, use `ipconfig` and `ping` to validate addressing, gateways, permitted paths, and deliberately denied paths.

## Evidence Standard

Evidence must show an actual Packet Tracer result, not an expected or fabricated outcome. A failed/blocked ping is valid evidence only where the security policy explicitly requires that path to be denied. Configuration output should be paired with behavioral testing where practical.
