# Stats SA Mafikeng Field Office — Network Implementation

Cisco Packet Tracer implementation for the **Stats SA Mafikeng Field Office (Mahikeng)**, prepared as part of CMPG 325 Computer Networks.

## Project Summary

| Item | Implementation |
| --- | --- |
| Prepared by | Kudzai Mudzingwa |
| Client | Stats SA Mafikeng Field Office |
| Site | Mahikeng, North West, South Africa |
| Platform | Cisco Packet Tracer 9.x |
| Architecture | Router-on-a-stick with one core switch and two access switches |
| Edge router | Cisco 2911 (R1) |
| Switching | Cisco 2960 core/access switches |
| External test network | `203.0.113.0/24` |
| Management network | `192.168.99.0/24` |
| Security controls | Guest isolation, CCTV isolation, SSH management |
| Internet simulation | PAT/NAT overload through R1 |

## Implemented Topology

The final Packet Tracer implementation contains R1, SW1-Core, SW2-Access, SW3-Access, an external test server, and six representative endpoint systems: Admin, Field, Finance, HR, Guest, and CCTV.

R1 provides 802.1Q subinterfaces and default gateways for the internal VLANs. SW1-Core aggregates the two access switches, while SW2 and SW3 place endpoints into their assigned access VLANs.

## Implemented Addressing

| VLAN | Function | Subnet | Gateway |
| ---: | --- | --- | --- |
| 10 | Administration | `192.168.10.0/24` | `192.168.10.1` |
| 20 | Field | `192.168.20.0/24` | `192.168.20.1` |
| 30 | Finance | `192.168.30.0/24` | `192.168.30.1` |
| 40 | HR | `192.168.40.0/24` | `192.168.40.1` |
| 50 | Guest | `192.168.50.0/24` | `192.168.50.1` |
| 60 | CCTV | `192.168.60.0/24` | `192.168.60.1` |
| 99 | Network management | `192.168.99.0/24` | `192.168.99.1` |
| — | External test network | `203.0.113.0/24` | R1: `203.0.113.1` |

The external test server is `203.0.113.10`.

## Security and Network Services

**Inter-VLAN routing.** R1 uses router-on-a-stick subinterfaces on `GigabitEthernet0/1` for VLANs 10, 20, 30, 40, 50, 60, and 99.

**NAT/PAT.** Internal VLAN subinterfaces are NAT-inside interfaces and `GigabitEthernet0/0` is the NAT-outside interface. PAT provides translated connectivity to the simulated external network.

**Guest isolation.** The `GUEST-ISOLATION` ACL prevents VLAN 50 from initiating traffic to protected internal and management networks while allowing permitted external traffic.

**CCTV isolation.** The `CCTV-ISOLATION` ACL prevents VLAN 60 from initiating traffic to user and management networks while allowing permitted external traffic.

**Secure management.** SW1-Core, SW2-Access, and SW3-Access use VLAN 99 management addresses. SSH was configured for administrative access.

## Verification Status

Only results actually observed during Packet Tracer testing are reported here.

| Control / test | Observed result |
| --- | --- |
| Management reachability | PC-Admin successfully reached `192.168.99.2`, `.3`, and `.4` |
| SSH management | Successful PC-Admin SSH session to SW1-Core |
| Guest gateway | `192.168.50.1`: 4/4 replies |
| Guest → Admin | Blocked: 100% packet loss |
| Guest → external server | `203.0.113.10`: 4/4 replies |
| CCTV gateway | `192.168.60.1`: 4/4 replies |
| CCTV → Admin | Blocked: 100% packet loss |
| CCTV → external server | `203.0.113.10`: 4/4 replies |
| NAT statistics | 4 dynamic translations and 12 hits observed |
| ACL counters | Guest and CCTV deny/permit counters incremented during testing |
| Final topology | Required devices present with active links |

DHCP, a dedicated inter-VLAN evidence capture, and a final routing-table screenshot were not captured during the recorded evidence session and are therefore not represented as verified evidence.

## Repository Structure

```text
.
├── README.md
├── SUBMISSION.md
├── client-requirements.md
├── physical-topology.md
├── logical-topology.md
├── ip-addressing-plan.md
├── testing-evidence.md
├── packet-tracer/
│   └── StatsSA-Mafikeng-Network.pkt
└── evidence/
    └── README.md
```

## Operational Notes

The Packet Tracer file is the authoritative implementation artifact. The Markdown files document the implemented design, test scope, and evidence status. Before using this design outside a simulation environment, replace laboratory credentials, use organization-approved IP addressing, define production firewall policy, implement centralized AAA/logging, and validate availability and capacity requirements.

## Review

See `SUBMISSION.md` for the handover summary and `testing-evidence.md` for the verification procedure and evidence register.
