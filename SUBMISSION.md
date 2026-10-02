# Implementation Handover and Submission Record

## System

**Stats SA Mafikeng Field Office Network — Cisco Packet Tracer implementation**

Prepared by **Kudzai Mudzingwa** for CMPG 325 Computer Networks.

## Deliverables

| Deliverable | Status | Notes |
| --- | --- | --- |
| Packet Tracer implementation | Available | Final working file: `StatsSA-Mafikeng-Network.pkt` |
| Network design documentation | Complete | Physical, logical, requirements, and addressing documents included |
| NAT/PAT implementation | Verified | Dynamic translations and non-zero NAT hits observed |
| Guest isolation | Verified | Internal Admin access blocked; gateway/external access observed |
| CCTV isolation | Verified | Internal Admin access blocked; gateway/external access observed |
| SSH management | Verified | Authorized SSH session to SW1-Core observed |
| Management reachability | Verified | SW1/SW2/SW3 management IPs reachable from PC-Admin |
| DHCP evidence screenshot | Not captured | Do not represent as verified evidence |
| Dedicated inter-VLAN screenshot | Not captured | Do not represent as verified evidence |
| Routing-table screenshot | Not captured | Do not represent as verified evidence |

## Implemented Network

R1 operates as the routing and NAT boundary. `GigabitEthernet0/1` carries the internal 802.1Q VLANs and `GigabitEthernet0/0` connects to the simulated external network. The design uses VLANs 10–60 for business/security functions and VLAN 99 for infrastructure management.

The external validation host is `203.0.113.10`. R1 uses `203.0.113.1` on its external interface.

## Acceptance Evidence

The evidence register in `evidence/README.md` records what was observed during the test session. Recorded results include:

- successful management reachability to all three switches;
- successful SSH access from PC-Admin to SW1-Core;
- successful Guest and CCTV default-gateway connectivity;
- enforced Guest and CCTV isolation from the Admin VLAN;
- successful Guest and CCTV connectivity to the external test server;
- active NAT/PAT with four dynamic translations and 12 observed hits; and
- ACL counters showing actual Guest/CCTV permit and deny matches.

## Known Evidence Gaps

The implementation should not be described as having complete acceptance evidence until the following screenshots are captured:

1. DHCP lease/address configuration;
2. a dedicated authorized inter-VLAN connectivity test; and
3. the final routing table.

These are evidence gaps, not claims of test failure.

## Handover Notes

This is a simulation/academic implementation. Before production deployment, complete a formal security review, replace laboratory credentials, use approved enterprise addressing and WAN services, implement centralized authentication and logging, establish configuration backup/version control, and perform resilience/capacity testing.
