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

## Client Context

This field office needs a network that can support ordinary office work, data capture, statistics/GIS work, shared services, printing, and site security. Because it is a government office, the design should be predictable and easy to audit. A flat network would be quick to draw, but it would not be suitable here because CCTV, guest access, servers, and network administration should not all share the same broadcast and security space.

The design therefore uses VLANs, routing controls, NAT, and a dedicated management area. That gives the client a network that is still realistic for Packet Tracer, but strong enough to explain and defend during the project review.

## Functional Requirements

| ID | Requirement | Design Response | Reason |
| --- | --- | --- | --- |
| CR-01 | Provide stable LAN connectivity for the field office. | Use a core/access topology with one Layer 3 core switch and separate access switches. | Keeps the design simple, scalable, and easy to troubleshoot. |
| CR-02 | Separate different office functions. | Create VLANs for management, servers, administration, field operations, analysts, wireless, printers, and CCTV. | Limits unnecessary traffic and supports role-based access. |
| CR-03 | Support core services. | Include DHCP, DNS, file/application services, and NVR services. | Provides the services a working office network normally needs. |
| CR-04 | Allow office users to reach external services. | Use NAT/PAT on the edge router for inside-to-outside translation. | Meets the assigned NAT challenge and gives realistic internet access. |
| CR-05 | Add CCTV cameras. | Place cameras in a dedicated CCTV VLAN connected through a CCTV access switch. | Makes the change request visible in the topology and easy to verify. |
| CR-06 | Segment CCTV traffic. | Permit CCTV-to-NVR traffic and deny CCTV access to normal user VLANs. | Protects office users and prevents camera traffic from spreading through the LAN. |
| CR-07 | Secure device administration. | Use a management VLAN, SSH, encrypted passwords, and access restrictions. | Responds directly to the unauthorized-change incident in the brief. |
| CR-08 | Use the assigned IP block properly. | Apply VLSM to `172.30.56.0/23` with gateways, DHCP pools, static ranges, and spare blocks. | Shows efficient planning and supports future expansion. |
| CR-09 | Produce a working Packet Tracer implementation later. | Use Packet Tracer-compatible routers, switches, servers, PCs, APs, and IP cameras. | Keeps the design practical for the next milestones. |
| CR-10 | Maintain a professional GitHub portfolio. | Store the design, diagrams, configs, Packet Tracer files, and evidence in organized folders. | Matches the portfolio-of-evidence requirement from the marking guide. |

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
