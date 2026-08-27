# Marking Guideline Alignment

Project name: **Stats SA Mafikeng Field Office (Mahikeng)**

## Purpose

This file shows how the Milestone 1 submission has been prepared to target the higher bands of the marking guideline. It does not guarantee a mark, because the final score depends on the marker and later Packet Tracer evidence, but it makes the design choices visible and easy to assess.

## Client Requirements and Network Design

| Excellent rubric expectation | Where this submission addresses it |
| --- | --- |
| Exceptional understanding of client requirements | `docs/client-requirements.md` explains the government field-office context, the operational groups, CCTV change request, NAT challenge, and administration security issue. |
| Topology is well-designed, complete, and appropriate | `docs/physical-topology.md` and `docs/logical-topology.md` show a complete core/access design with edge routing, VLANs, services, CCTV, printers, wireless, and test network. |
| IP addressing is efficient, correct, and fully documented | `docs/ip-addressing-plan.md` includes subnet, mask, usable range, broadcast, gateway, capacity, DHCP pools, static addresses, NAT wildcard, and spare blocks. |
| Design decisions are clearly justified | `docs/design-decision-log.md` explains why each major design choice was made and how it responds to the scenario. |

## Packet Tracer Implementation Readiness

| Excellent rubric expectation | Prepared evidence |
| --- | --- |
| Correct device selection and configuration plan | `docs/physical-topology.md` lists Packet Tracer-friendly device types and roles. |
| Network operates as required | `docs/testing-and-evidence-plan.md` defines the tests to prove DHCP, VLAN routing, NAT, CCTV segmentation, and management security. |
| Core services considered | VLAN 20 is reserved for DHCP, DNS, file/app, and NVR services. |
| No major reliability or performance issues | The design avoids a flat network, centralizes routing, and documents ACL placement. |

## Assigned Networking Feature / Technical Challenge

| Requirement | Evidence in this repository |
| --- | --- |
| NAT inside/outside address translation | `docs/logical-topology.md` and `docs/ip-addressing-plan.md` identify NAT inside and outside interfaces, NAT scope, public simulation address, and verification target. |
| Explanation of why NAT is used | `docs/logical-topology.md` explains PAT overload for shared outside access. |
| Verification plan | `docs/testing-and-evidence-plan.md` lists pings/web tests and `show ip nat translations`. |

## GitHub Portfolio of Evidence

| Excellent rubric expectation | Repository response |
| --- | --- |
| Repository is well structured and professional | README, checklist, docs, diagrams, configs, packet-tracer, and evidence folders are created. |
| Evidence is easy to navigate | `docs/repository-overview.md` describes where each evidence type belongs. |
| Meaningful commit history | The repository contains Milestone 1 documentation commits; future milestone commits should be added as work continues. |
| Excellent documentation | The repository contains separate, readable documents for requirements, topology, addressing, testing, design decisions, and rubric alignment. |

## Important Next Steps for 90 Percent Plus Final Portfolio Quality

- Build the Packet Tracer file exactly from the physical and logical design.
- Export router and switch configurations into `configs/`.
- Capture evidence screenshots into `evidence/`.
- Commit each meaningful change with a clear message.
- Show NAT translations, CCTV ACL results, DHCP leases, VLAN routing, and secured SSH administration in the final evidence.
