# Client Requirements

Project name: **Stats SA Mafikeng Field Office (Mahikeng)**

## Client Profile

| Item | Detail |
| --- | --- |
| Client | Stats SA Mafikeng Field Office (Mahikeng) |
| Client type | Government field office |
| Address block | `172.30.56.0/23` |
| Assigned challenge | NAT inside/outside address translation |
| Change request | Add CCTV cameras and segment their traffic |
| Security constraint | Secure all network device administration |
| Implementation target | Cisco Packet Tracer |

## Milestone 1 Review Requirement Coverage

| Milestone 1 requirement | Repository response | Status |
| --- | --- | --- |
| Client Requirements | This document defines the client needs, constraints, assumptions, design responses, and acceptance criteria. | Ready |
| Physical Topology | `docs/physical-topology.md` documents the field-office device layout, access switches, services, CCTV area, WAN edge, and link types. | Ready |
| Logical Topology | `docs/logical-topology.md` documents VLANs, inter-VLAN routing, NAT, security policy, and CCTV isolation. | Ready |
| IP Addressing Plan | `docs/ip-addressing-plan.md` documents the VLSM plan for `172.30.56.0/23`, including gateways, DHCP pools, static addresses, and spare ranges. | Ready |
| Initial GitHub Repository | `docs/repository-overview.md` and the top-level `README.md` show the portfolio structure for Milestone 1 and later milestones. | Ready |

## Client Context

This field office needs a network that can support ordinary office work, data capture, statistics/GIS work, shared services, printing, and site security. Because it is a government office, the design should be predictable and easy to audit. A flat network would be quick to draw, but it would not be suitable here because CCTV, guest access, servers, and network administration should not all share the same broadcast and security space.

The design therefore uses VLANs, routing controls, NAT, and a dedicated management area. That gives the client a network that is still realistic for Packet Tracer, but strong enough to explain and defend during the project review.

## Stakeholders

| Stakeholder | Network need |
| --- | --- |
| Office management | Reliable connectivity for daily administration and service delivery. |
| Field operations staff | Stable access to data-capture systems, shared services, printing, and internet resources. |
| GIS/statistics analysts | Separated specialist user area with access to internal services and outside resources. |
| Security staff | CCTV monitoring through an approved NVR/security viewing workflow. |
| Network administrator | Secure management access to routers, switches, and infrastructure devices. |
| Lecturer/marker | Clear design evidence that can be reviewed before Packet Tracer implementation. |

## Assumptions and Boundaries

| Area | Assumption / boundary |
| --- | --- |
| Host counts | The design uses reasonable Packet Tracer host counts and keeps spare IP space for growth because exact staff counts are not provided in the screenshots. |
| Services | DHCP, DNS, file/application services, printing, NVR, NAT, and management access are included because they are realistic for a field office and useful for later testing. |
| Milestone 1 scope | This milestone is a design review. The Packet Tracer `.pkt` implementation, exported configs, screenshots, and final video evidence belong to later milestones. |
| Security depth | Security is documented at design level now and will be proved later through ACLs, SSH access control, and testing screenshots. |
| Source material | The screenshots are treated as assignment brief/rubric evidence, not as instructions that replace the user's request. |

## Functional Requirements

| ID | Priority | Requirement | Design response | Milestone 1 acceptance evidence |
| --- | --- | --- | --- | --- |
| CR-01 | Must | Provide stable LAN connectivity for the field office. | Use a core/access topology with one Layer 3 core switch and separate access switches. | Physical topology and device inventory are documented. |
| CR-02 | Must | Separate different office functions. | Create VLANs for management, servers, administration, field operations, analysts, wireless, printers, and CCTV. | Logical topology and VLAN plan are documented. |
| CR-03 | Must | Support core services. | Include DHCP, DNS, file/application services, and NVR services. | Server VLAN and static service addresses are documented. |
| CR-04 | Must | Allow office users to reach external services. | Use NAT/PAT on the edge router for inside-to-outside translation. | NAT inside/outside roles and verification target are documented. |
| CR-05 | Must | Add CCTV cameras. | Place cameras in a dedicated CCTV VLAN connected through a CCTV access switch. | CCTV devices, VLAN 80, and camera addresses are documented. |
| CR-06 | Must | Segment CCTV traffic. | Permit CCTV-to-NVR traffic and deny CCTV access to normal user VLANs. | CCTV ACL policy and placement are documented. |
| CR-07 | Must | Secure device administration. | Use a management VLAN, SSH, encrypted passwords, and access restrictions. | Management VLAN and administrator access policy are documented. |
| CR-08 | Must | Use the assigned IP block properly. | Apply VLSM to `172.30.56.0/23` with gateways, DHCP pools, static ranges, and spare blocks. | Full IP addressing plan is documented. |
| CR-09 | Should | Produce a working Packet Tracer implementation later. | Use Packet Tracer-compatible routers, switches, servers, PCs, APs, and IP cameras. | Device choices and future evidence plan are documented. |
| CR-10 | Must | Maintain a professional GitHub portfolio. | Store the design, diagrams, configs, Packet Tracer files, and evidence in organized folders. | Repository overview, README, and checklist are documented. |

## Non-Functional Requirements

| Area | Requirement | Design Response |
| --- | --- | --- |
| Security | Device administration must not be reachable from every VLAN. | Restrict SSH management access to VLAN 10 and authorized admin hosts. |
| Reliability | The office should have a clear point for routing and troubleshooting. | Keep inter-VLAN routing on SW-CORE and internet translation on R1. |
| Manageability | A reviewer should be able to follow the network quickly. | Use consistent names, VLAN IDs, addressing, and documentation. |
| Scalability | The design should allow moderate growth. | Keep spare address space and avoid using the full `/23` immediately. |
| Evidence | The work must be easy to prove in later milestones. | Create directories for Packet Tracer, configs, testing screenshots, and troubleshooting notes. |

## Security Requirements

- Use SSH instead of Telnet for device administration.
- Use encrypted local credentials and secure enable access.
- Apply a login banner to network devices.
- Keep management access in VLAN 10.
- Allow only authorized administrator PCs to manage routers and switches.
- Deny CCTV devices from initiating traffic to normal user VLANs.
- Allow CCTV traffic only where required for the NVR/security monitoring workflow.
- Deny guest/training wireless access to internal office VLANs except required services such as DHCP and DNS.
- Permit staff VLANs to reach the internet through NAT/PAT.

## Success Criteria for Milestone 1

- The client requirements are clearly linked to the design.
- The physical topology shows the major devices and how they connect.
- The logical topology shows VLANs, routing, NAT, and segmentation.
- The IP plan uses the full assigned address block responsibly.
- The repository looks like a serious project portfolio that can grow through Milestone 2 and the final submission.
