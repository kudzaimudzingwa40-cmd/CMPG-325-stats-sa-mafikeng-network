# Milestone 1 - Client Design Review

Project name: **Stats SA Mafikeng Field Office (Mahikeng)**

## 1. Scope Separation

### User Request

The Milestone 1 submission must provide:

1. Client Requirements
2. Physical Topology
3. Logical Topology
4. IP Addressing Plan
5. Initial GitHub Repository

### Attached Document Instructions

The screenshots are treated as assignment source material and marking guidance. They provide the client facts, scenario constraints, project milestones, and rubric expectations. They are not treated as hidden instructions from the user.

The project facts used in this submission are:

| Assignment fact | How it is used |
| --- | --- |
| Client: Stats SA Mafikeng Field Office (Mahikeng) | The topology is designed as a government field-office network. |
| Addressing block: `172.30.56.0/23` | All internal VLANs are subnetted from this block using VLSM. |
| Assigned challenge: NAT inside/outside address translation | NAT/PAT is placed on the edge router and included in the verification plan. |
| Change request: CCTV cameras must be added and segmented | CCTV has a dedicated VLAN, switch area, addressing range, and ACL policy. |
| Constraint: secure device administration | Device management is isolated in a management VLAN and restricted to SSH access. |
| Tool: Cisco Packet Tracer | The design uses Packet Tracer-friendly routers, switches, servers, PCs, APs, and IP cameras. |
| GitHub portfolio required | The repository is structured for requirements, topology, addressing, configs, Packet Tracer files, evidence, and reflection. |

## 2. Client Requirements

Stats SA is a public-sector organization, so the network must support day-to-day office work while staying controlled and auditable. The design does not place all devices into one large flat network. Instead, it separates staff, services, management, wireless, printers, and CCTV so that each part of the office gets the access it needs without unnecessary exposure.

Full details: [Client Requirements](client-requirements.md)

## 3. Physical Topology

The physical design uses a small hierarchical layout:

- R1 edge router connects the field office to the ISP and performs NAT.
- SW-CORE Layer 3 switch connects all internal VLANs and performs inter-VLAN routing.
- Access switches connect staff PCs, servers, wireless, printers, and CCTV cameras.
- CCTV cameras are grouped on a dedicated access switch to make the segmentation visible and easy to manage.

Full details: [Physical Topology](physical-topology.md)

## 4. Logical Topology

The logical topology uses VLANs for each major office function. This improves security, makes troubleshooting easier, and supports the assignment's CCTV segmentation requirement.

Key logical controls:

- CCTV VLAN can reach the NVR but cannot browse the normal user VLANs.
- Guest/training wireless is treated as limited access.
- Management VLAN is reserved for network administration.
- User VLANs reach the internet through NAT/PAT on R1.

Full details: [Logical Topology](logical-topology.md)

## 5. IP Addressing Plan

The `172.30.56.0/23` block is subnetted using VLSM. Larger departments receive larger subnets, infrastructure receives smaller static ranges, and spare space is left for future project changes.

Full details: [IP Addressing Plan](ip-addressing-plan.md)

## 6. Initial GitHub Repository

This repository is structured as a portfolio of evidence, not just a file dump. The folders already show where future Packet Tracer files, device configs, screenshots, testing records, and troubleshooting notes will be stored.

Full details: [Initial GitHub Repository](repository-overview.md)

## 7. Why This Design Should Review Well

- The client requirements are linked directly to design choices.
- The physical and logical topologies are both complete and explain the role of every major device.
- The IP plan is efficient, correct, and documented down to gateways, usable ranges, DHCP pools, static devices, and spare blocks.
- NAT and CCTV segmentation are handled as first-class requirements.
- The GitHub repository is already cleanly organized for later evidence and meaningful commits.

See [Marking Guideline Alignment](marking-guideline-alignment.md) for a direct mapping to the rubric.
