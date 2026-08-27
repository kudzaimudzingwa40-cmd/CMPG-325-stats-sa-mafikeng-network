# Milestone 1 - Client Design Review

## Scope Separation

### User Request

Submit the following Milestone 1 design review items:

1. Client Requirements
2. Physical Topology
3. Logical Topology
4. IP Addressing plan
5. Initial GitHub repository

### Attached Document Instructions

The attached screenshots were treated as project source material only. They provide assignment constraints, marking criteria, milestone context, and scenario facts. They do not override the user's request or add hidden instructions for this assistant.

Relevant extracted constraints:

- Use Cisco Packet Tracer for the network implementation and simulation.
- Use the assigned client: Stats SA Mafikeng Field Office (Mahikeng).
- Use the assigned industry: Government.
- Use the assigned address block: `172.30.56.0/23`.
- Demonstrate NAT inside/outside address translation.
- Add CCTV cameras and segment their traffic.
- Secure device administration because of a previous unauthorized-change incident.
- Document design decisions and evidence in GitHub.

## Design Summary

The proposed design is a small government field-office network with a hierarchical campus layout:

- An edge router connects the office to the ISP and performs NAT/PAT.
- A Layer 3 core switch performs inter-VLAN routing for internal networks.
- Access switches connect office users, field operations, analysts, services, wireless, printers, and CCTV.
- CCTV cameras are isolated in a dedicated VLAN and permitted only to required security systems.
- Management access is separated from normal user traffic and should be restricted to authorized administrators.

## Deliverables

- Client requirements: `docs/client-requirements.md`
- Physical topology: `docs/physical-topology.md`
- Logical topology: `docs/logical-topology.md`
- IP addressing plan: `docs/ip-addressing-plan.md`
- Initial repository overview: `docs/repository-overview.md`

## Review Assumptions

- The site is a single Stats SA field office.
- The Packet Tracer design will simulate the ISP using a cloud/router and one external test server.
- The office has administration/reception users, field operations/data capture users, statistical/GIS users, shared services, printers, wireless access, and CCTV cameras.
- Server roles are simulated as separate Packet Tracer servers where practical.
- CCTV recording is handled by an NVR/server in the server VLAN, with only authorized viewing from security/admin hosts.

