# IP Addressing Plan

## Scope

This document records the addressing used by the **implemented Packet Tracer topology**. It supersedes earlier conceptual/VLSM addressing drafts.

## Production-Like Addressing Model

| VLAN | Function | Network | Default gateway | Addressing |
| ---: | --- | --- | --- | --- |
| 10 | Administration | `192.168.10.0/24` | `192.168.10.1` | Endpoint addressing / DHCP-capable |
| 20 | Field | `192.168.20.0/24` | `192.168.20.1` | Endpoint addressing / DHCP-capable |
| 30 | Finance | `192.168.30.0/24` | `192.168.30.1` | Endpoint addressing / DHCP-capable |
| 40 | Human Resources | `192.168.40.0/24` | `192.168.40.1` | Endpoint addressing / DHCP-capable |
| 50 | Guest | `192.168.50.0/24` | `192.168.50.1` | Restricted user network |
| 60 | CCTV | `192.168.60.0/24` | `192.168.60.1` | Restricted security-device network |
| 99 | Infrastructure management | `192.168.99.0/24` | `192.168.99.1` | Static management addressing |

All internal networks use mask `255.255.255.0`.

## Infrastructure Addresses

| Device | Address | Purpose |
| --- | --- | --- |
| R1 VLAN 10 gateway | `192.168.10.1` | Administration gateway |
| R1 VLAN 20 gateway | `192.168.20.1` | Field gateway |
| R1 VLAN 30 gateway | `192.168.30.1` | Finance gateway |
| R1 VLAN 40 gateway | `192.168.40.1` | HR gateway |
| R1 VLAN 50 gateway | `192.168.50.1` | Guest gateway |
| R1 VLAN 60 gateway | `192.168.60.1` | CCTV gateway |
| R1 VLAN 99 gateway | `192.168.99.1` | Management gateway |
| SW1-Core | `192.168.99.2` | Switch management |
| SW2-Access | `192.168.99.3` | Switch management |
| SW3-Access | `192.168.99.4` | Switch management |

PC-Admin was observed as `192.168.10.21` during Guest/CCTV isolation testing.

## External Test Network

| Item | Address |
| --- | --- |
| Network | `203.0.113.0/24` |
| R1 external interface | `203.0.113.1` |
| External test server | `203.0.113.10` |

The `203.0.113.0/24` block is used here as a documentation/test network for the simulation.

## NAT Classification

- R1 `GigabitEthernet0/0`: NAT outside.
- R1 `GigabitEthernet0/1.10`–`.60`: NAT inside.
- PAT/NAT overload is used for permitted internal-to-external traffic.
- During verification, R1 reported four dynamic translations and 12 hits.

## Address Management Guidance

For a real deployment, addresses should be allocated from the organization's approved IPAM plan. Infrastructure addresses should be reserved/static, user endpoints should use controlled DHCP scopes, and management addressing should be reachable only from authorized administration networks.
