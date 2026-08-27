# Client Requirements

Project: **Stats SA Mafikeng Field Office Network Design**

| Item | Detail |
| --- | --- |
| Prepared by | Kudzai Mudzingwa |
| Client | Stats SA Mafikeng Field Office |
| Site | Mahikeng |
| Design status | In progress |
| Internal address block | `172.30.66.0/23` |
| Network feature | NAT inside/outside address translation |
| Security enhancement | Segmented CCTV network and protected device administration |
| Simulation platform | Cisco Packet Tracer |

## Business Context

The Stats SA Mafikeng Field Office requires a secure and reliable branch-office network that supports daily administration, field-data processing, statistical analysis, shared office services, printing, wireless access, and site monitoring.

The design separates business functions into dedicated VLANs instead of placing all devices on a flat network. This improves security, reduces unnecessary broadcast traffic, simplifies troubleshooting, and gives the office a clear structure for growth and operational support.

## Stakeholders

| Stakeholder | Network need |
| --- | --- |
| Office management | Reliable connectivity for administration and service delivery. |
| Field operations staff | Stable access to data-capture systems, shared services, printing, and internet resources. |
| GIS and statistics analysts | A dedicated user segment with dependable access to internal services and external resources. |
| Security staff | CCTV monitoring through an approved NVR viewing workflow. |
| Network administrator | Controlled management access to routers, switches, and infrastructure devices. |
| Office visitors and trainees | Limited wireless access separated from internal office resources. |

## Design Scope

| Area | Design position |
| --- | --- |
| LAN architecture | Core/access topology with one Layer 3 core switch and dedicated access switches. |
| WAN edge | Edge router providing the boundary between the internal LAN and outside network. |
| Addressing | VLSM design using the assigned `172.30.66.0/23` block. |
| Segmentation | VLANs for management, servers, administration, field operations, analysts, guest wireless, printers, and CCTV. |
| Security | SSH administration, management VLAN isolation, CCTV traffic control, and guest wireless restrictions. |
| Services | DHCP, DNS, file/application services, NVR services, printing, and NAT/PAT. |

## Functional Requirements

| ID | Priority | Requirement | Design response | Business value |
| --- | --- | --- | --- | --- |
| CR-01 | Critical | Provide stable LAN connectivity for the field office. | Deploy a core/access topology with a Layer 3 core switch and separate access switches. | Gives the office a reliable and supportable network foundation. |
| CR-02 | Critical | Separate office departments and device types. | Use VLANs for management, servers, administration, field operations, analysts, guest wireless, printers, and CCTV. | Reduces unnecessary exposure between business areas. |
| CR-03 | Critical | Support internal office services. | Place DHCP, DNS, file/application, and NVR services in a controlled server VLAN. | Keeps core services reachable while maintaining network order. |
| CR-04 | Critical | Provide controlled external connectivity. | Use NAT/PAT on the edge router for inside-to-outside translation. | Allows internal users to access outside resources without exposing private addressing. |
| CR-05 | Critical | Add CCTV camera support. | Place IP cameras in a dedicated CCTV VLAN connected through a CCTV access switch. | Supports site monitoring without mixing camera traffic with office users. |
| CR-06 | Critical | Segment CCTV traffic. | Permit CCTV-to-NVR traffic and block camera-initiated access to normal user VLANs. | Protects office devices and limits unnecessary cross-network movement. |
| CR-07 | Critical | Protect network device administration. | Restrict router, switch, and AP management to VLAN 10 with SSH access. | Reduces the risk of unauthorized configuration changes. |
| CR-08 | Critical | Use the assigned address block efficiently. | Apply VLSM with documented gateways, DHCP pools, static addresses, and spare ranges. | Provides clear capacity planning and avoids address waste. |
| CR-09 | High | Keep the design practical for Cisco Packet Tracer. | Use supported routers, multilayer switches, access switches, servers, PCs, APs, printers, and IP cameras. | Makes the design directly implementable in the selected simulation platform. |
| CR-10 | High | Maintain a professional repository record. | Keep the repository limited to the completed design files with clear naming and consistent formatting. | Makes the design package easy to review and maintain. |

## Non-Functional Requirements

| Area | Requirement | Design response |
| --- | --- | --- |
| Security | Administration access is restricted to authorized sources. | Management traffic is isolated in VLAN 10 and protected with SSH. |
| Reliability | Routing and internet access have clear points of control. | SW-CORE handles internal routing, while R1 handles NAT and outside connectivity. |
| Manageability | Device roles, VLANs, and addresses are easy to identify. | Consistent naming is used across all design documents. |
| Scalability | The office can grow without redesigning the full network. | Spare address space is reserved and documented in the IP plan. |
| Auditability | The design can be reviewed against business and security needs. | Requirements, topology, and addressing are documented in separate design files. |

## Security Requirements

| Control area | Requirement | Design response |
| --- | --- | --- |
| Device administration | Use secure management access for routers and switches. | SSH is used instead of Telnet, with management access restricted to VLAN 10. |
| Credentials | Protect privileged device access. | Local credentials and enable access are secured with encrypted passwords. |
| Management reachability | Limit who can administer infrastructure devices. | Only authorized administrator hosts are permitted to access device management services. |
| CCTV isolation | Prevent camera traffic from reaching normal user segments. | VLAN 80 is dedicated to CCTV and controlled with ACL policy. |
| NVR access | Allow approved CCTV recording and viewing. | Cameras communicate with the NVR, and the authorized security workstation can access CCTV services. |
| Guest access | Keep temporary users away from internal resources. | Guest/training wireless is placed in a restricted VLAN with limited internal access. |
| Internet access | Hide internal office addressing from the outside network. | NAT/PAT translates inside addresses on the edge router. |

## Completion Statement

The client requirements are complete and are aligned with the physical topology, logical topology, and IP addressing plan in this repository.
