# Technical Report: Stats SA Mafikeng Field Office Network

**Module:** CMPG 325 — Computer Networks  
**Student:** Kudzai Mudzingwa  
**Client scenario:** Stats SA Mafikeng Field Office, Mahikeng, North West, South Africa  
**Implementation platform:** Cisco Packet Tracer 9.x  
**Report date:** 16 October 2026  
**Primary implementation file:** StatsSA-Mafikeng-Network.pkt

> **Evidence statement.** This report consolidates the project documentation and test results recorded in this repository. Packet Tracer was not independently run during preparation of this report. Results below are reported as observed in the existing project records; outstanding checks are identified rather than presented as completed.

## Executive summary

This project models a small Stats SA field-office network with separate business, guest, CCTV, and infrastructure-management segments. A Cisco 2911 router (R1) provides router-on-a-stick routing across seven VLANs and acts as the simulated edge for network address translation and policy enforcement. A Cisco 2960 core switch connects two 2960 access switches, which serve six representative endpoints and an external test server. Guest and CCTV access-control lists (ACLs) are intended to restrict access to protected internal networks while preserving permitted external connectivity. Infrastructure management uses VLAN 99, and SSH provides remote access to the core switch.

The repository records successful management reachability, an SSH session to SW1-Core, Guest and CCTV gateway reachability, Guest/CCTV access to the external test server, denial of Guest/CCTV traffic to the Admin endpoint, and NAT/ACL counters. Four dynamic NAT translations and 12 NAT hits were recorded. These are simulation results, not production service-level measurements. The evidence record does not include a dedicated inter-VLAN test capture, a final routing-table capture, or captured DHCP verification. The NAT-inside documentation also needs reconciliation for VLAN 99 before the final demonstration.

## 1. Purpose, scope, and design objectives

The purpose is to demonstrate a manageable and segmented branch-office network using Packet Tracer. The design covers representative endpoint connectivity, VLAN separation, inter-VLAN routing, restricted Guest/CCTV policy, simulated external access, and secure switch management. The boundary is a teaching simulation: it is not a validated production deployment or a complete as-built record for a real site.

The design objectives are to:

1. Separate Administration, Field, Finance, Human Resources, Guest, CCTV, and network-management traffic.
2. Route traffic between VLANs at a controlled Layer 3 boundary.
3. Restrict Guest and CCTV access to protected internal networks while allowing the recorded external test path.
4. Provide a dedicated management subnet and demonstrate SSH administration.
5. Maintain reviewable addressing, topology, and test records, with observed results distinguished from outstanding evidence.

## 2. Requirements and acceptance status

| ID | Requirement | Design / implementation | Recorded status |
|---|---|---|---|
| R01 | Separate business and security functions | VLANs 10, 20, 30, 40, 50, 60, and 99 | Implemented in the documented topology; configuration evidence should be included in the final capture set. |
| R02 | Route permitted traffic between VLANs | Router-on-a-stick on R1 | Architecture is documented; a dedicated inter-VLAN evidence capture remains outstanding. |
| R03 | Provide controlled external connectivity | PAT/NAT through R1 to the simulated external network | Four dynamic translations and 12 hits were recorded; Guest and CCTV reached the external test server. |
| R04 | Isolate Guest users | GUEST-ISOLATION ACL | Guest-to-Admin traffic was blocked; Guest gateway and external-server access succeeded. Other protected destinations were not individually listed as tested. |
| R05 | Isolate CCTV | CCTV-ISOLATION ACL | CCTV-to-Admin traffic was blocked; CCTV gateway and external-server access succeeded. Other protected destinations were not individually listed as tested. |
| R06 | Provide infrastructure management | VLAN 99 and switch management IPs | PC-Admin reached the three documented switch management addresses. |
| R07 | Use secure remote administration | SSH to SW1-Core | A successful PC-Admin SSH session to SW1-Core is recorded. |
| R08 | Maintain reviewable technical evidence | Documentation and evidence register | Partially captured; DHCP, dedicated inter-VLAN, and final routing-table captures remain outstanding. |

“Implemented” describes the design recorded in the project files; it does not mean every possible traffic path has been tested. Acceptance should be based on the evidence actually demonstrated and submitted.

## 3. Network architecture and topology

The topology follows a compact hierarchical pattern:

**External test server → R1 (Cisco 2911) → SW1-Core (Cisco 2960) → SW2-Access and SW3-Access (Cisco 2960).**

R1 connects to the core through an 802.1Q trunk on GigabitEthernet0/1. R1 subinterfaces provide the VLAN gateways. GigabitEthernet0/0 connects to the simulated external test segment. SW1-Core aggregates the access switches; access ports place endpoints into their assigned VLANs. The Packet Tracer scenario contains PC-Admin, PC-Field, PC-Finance, PC-HR, PC-Guest, PC-CCTV, and an External-Test-Server.

| Device | Model / type | Role |
|---|---|---|
| R1 | Cisco 2911 | VLAN gateways, inter-VLAN routing, ACL policy boundary, simulated NAT/PAT edge |
| SW1-Core | Cisco 2960-24TT | Core aggregation and trunk distribution |
| SW2-Access | Cisco 2960-24TT | Administration, Field, and Finance endpoints |
| SW3-Access | Cisco 2960-24TT | HR, Guest, and CCTV endpoints |
| External-Test-Server | Packet Tracer Server-PT | Deterministic target on the simulated external segment |

Recorded access-port assignments are Fa0/2–Fa0/4 on SW2-Access for Admin, Field, and Finance, and Fa0/2–Fa0/4 on SW3-Access for HR, Guest, and CCTV respectively. The project documentation reports active links in the final topology. Exact rack, patch-panel, cable-ID, and physical-site details are outside this simulation's scope.

## 4. VLAN and IP addressing plan

All listed internal VLANs use a /24 subnet with mask 255.255.255.0. The plan uses private IPv4 address space; the external test range is a documentation/simulation network.

| VLAN | Function | Subnet | Default gateway |
|---:|---|---|---|
| 10 | Administration | 192.168.10.0/24 | 192.168.10.1 |
| 20 | Field | 192.168.20.0/24 | 192.168.20.1 |
| 30 | Finance | 192.168.30.0/24 | 192.168.30.1 |
| 40 | Human Resources | 192.168.40.0/24 | 192.168.40.1 |
| 50 | Guest | 192.168.50.0/24 | 192.168.50.1 |
| 60 | CCTV | 192.168.60.0/24 | 192.168.60.1 |
| 99 | Infrastructure management | 192.168.99.0/24 | 192.168.99.1 |

| Infrastructure / test endpoint | Address | Purpose |
|---|---|---|
| SW1-Core | 192.168.99.2 | Switch management |
| SW2-Access | 192.168.99.3 | Switch management |
| SW3-Access | 192.168.99.4 | Switch management |
| PC-Admin | 192.168.10.21 | Address recorded during Guest/CCTV isolation testing |
| R1 external interface | 203.0.113.1 | Simulated external-side address |
| External-Test-Server | 203.0.113.10 | Permitted external connectivity test target |

The addressing plan labels business endpoints DHCP-capable, but the evidence record does not confirm DHCP service or lease acquisition. It must not be presented as verified unless tested and captured.

## 5. Routing, switching, and security design

### 5.1 VLAN switching and inter-VLAN routing

The switches use access ports for endpoint attachment and 802.1Q trunks for uplinks. SW1-Core aggregates SW2-Access and SW3-Access. R1 uses subinterfaces on GigabitEthernet0/1 to act as the default gateway for VLANs 10, 20, 30, 40, 50, 60, and 99. This router-on-a-stick design centralizes routing and policy at R1 while carrying multiple VLANs over the router-to-switch link.

A dedicated packet-level inter-VLAN test capture is still required. Before claiming full inter-VLAN acceptance, demonstrate at least one permitted business-VLAN path and one intentionally restricted path, and record the source, destination, result, and relevant policy.

### 5.2 Guest and CCTV access control

The documented GUEST-ISOLATION policy restricts Guest VLAN 50 from protected internal and management networks while permitting the external test path. The CCTV-ISOLATION policy similarly restricts CCTV VLAN 60 from user and management networks while permitting the external test path. Recorded behavior confirms that each restricted endpoint could reach its gateway and the external test server but could not reach PC-Admin at 192.168.10.21. The recorded result therefore demonstrates the tested paths; it is not proof that every protected destination or every protocol was tested.

### 5.3 NAT/PAT

R1 provides the simulated edge translation service. The documentation identifies GigabitEthernet0/0 as NAT outside and records four dynamic translations and 12 hits after external test traffic. Guest and CCTV external-server pings are also recorded as successful.

**Configuration detail to reconcile before final submission:** the IP addressing plan names R1 subinterfaces .10 through .60 as NAT inside, while broader wording elsewhere refers to internal VLAN subinterfaces without stating whether management VLAN 99 is included. Confirm the actual R1 running configuration in Packet Tracer, then align the README and addressing plan to it. Do not claim management VLAN NAT behavior unless it is shown and tested.

### 5.4 Infrastructure management

VLAN 99 uses 192.168.99.0/24. The three switches have documented management addresses from .2 through .4. PC-Admin reached all three addresses, and a successful SSH session to SW1-Core is recorded. The evidence specifically confirms the SW1-Core SSH session; equivalent SSH access to SW2-Access and SW3-Access should only be claimed if separately demonstrated.

## 6. Verification results

The following table reproduces the recorded outcomes in the repository's test register. They were not rerun while preparing this report.

| Test | Recorded outcome | Interpretation |
|---|---|---|
| PC-Admin to SW1-Core management address | Successful | Management reachability demonstrated for SW1-Core. |
| PC-Admin to SW2-Access management address | Successful | Management reachability demonstrated for SW2-Access. |
| PC-Admin to SW3-Access management address | Successful | Management reachability demonstrated for SW3-Access. |
| PC-Admin SSH to SW1-Core | Successful session | SSH administration demonstrated for SW1-Core. |
| PC-Guest to 192.168.50.1 | 4/4 replies | Guest gateway reachable. |
| PC-Guest to PC-Admin, 192.168.10.21 | Blocked; 100% loss | Guest-to-Admin restriction observed. |
| PC-Guest to 203.0.113.10 | 4/4 replies | Guest external test path allowed. |
| PC-CCTV to 192.168.60.1 | 4/4 replies | CCTV gateway reachable. |
| PC-CCTV to PC-Admin, 192.168.10.21 | Blocked; 100% loss | CCTV-to-Admin restriction observed. |
| PC-CCTV to 203.0.113.10 | 4/4 replies | CCTV external test path allowed. |
| R1 NAT statistics | Four dynamic translations; 12 hits | NAT/PAT activity observed during testing. |
| Guest and CCTV ACL counters | Permit and deny counters incremented | Both policy paths recorded matching traffic. |
| DHCP, dedicated inter-VLAN capture, final routing-table screenshot | Not captured in the evidence session | Outstanding; do not mark as verified. |

## 7. Limitations, risks, and recommended completion work

1. **Close the evidence gaps.** Capture DHCP only if it is part of the intended implementation; capture a permitted inter-VLAN test, a final routing table, and the relevant VLAN/trunk and ACL/NAT state. Save screenshots with descriptive names and note the test, endpoint, and outcome.
2. **Resolve the VLAN 99 NAT-inside discrepancy.** Check the Packet Tracer router configuration and make the source documents agree with it.
3. **Broaden policy validation.** The recorded Guest/CCTV denial tests target PC-Admin. If the requirement is isolation from all protected zones, test each relevant destination or document a justified representative test plus inspection of the ACL statements and counters.
4. **Label evidence clearly.** The repository has two screenshots with generic names, Screenshot (79).png and Screenshot (99).png. Confirm what each image demonstrates, rename them accordingly, and reference them from the evidence register. Do not infer their contents from their filenames.
5. **Treat the project as a simulation.** The repository does not establish production readiness. A real deployment would need approved IPAM, requirements-based capacity and availability design, validated firewall rules, credential replacement, centralized AAA and logging, configuration backup, physical cabling records, and change control.
6. **Use a controlled demo environment.** Reopen the saved .pkt file before recording, verify the Packet Tracer version, save a backup, and avoid exposing reusable passwords or personal information in the recording.

## 8. Conclusion

The recorded Packet Tracer project demonstrates a segmented field-office design with seven VLANs, router-on-a-stick routing, Guest and CCTV access-control policies, simulated external connectivity through NAT/PAT, and a dedicated management VLAN with SSH access to the core switch. The existing results support the specific management, gateway, Guest/CCTV-to-Admin, external-test, NAT-counter, and ACL-counter claims listed in this report. They do not establish unrecorded DHCP behavior, a dedicated inter-VLAN test result, final routing-table state, or production suitability.

The most important pre-submission actions are to reconcile VLAN 99 NAT documentation, capture the outstanding evidence, and clearly label the existing screenshots. This keeps the portfolio technically defensible.

## Project references

- [Project overview and verification summary](README.md)
- [Client and technical requirements](client-requirements.md)
- [Physical topology](physical-topology.md)
- [Logical topology](logical-topology.md)
- [IP addressing plan](ip-addressing-plan.md)
- [Testing and verification register](testing-evidence.md)
- [Evidence register](evidence/README.md)
- [Packet Tracer implementation](StatsSA-Mafikeng-Network.pkt)
