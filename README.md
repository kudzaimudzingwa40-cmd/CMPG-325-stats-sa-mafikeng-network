# Stats SA Mafikeng Field Office Network Design

Professional network design package for the Stats SA Mafikeng Field Office in Mahikeng.

| Item | Detail |
| --- | --- |
| Prepared by | Kudzai Mudzingwa |
| Design status | Complete |
| Project stage | Client Design Review |
| Client | Stats SA Mafikeng Field Office |
| Location | Mahikeng |
| Project reference | CMPG 325 Computer Networks |
| Internal address block | `172.30.56.0/23` |
| Simulation platform | Cisco Packet Tracer |

## Executive Summary

This design provides a secure, structured network for a government field office that supports administration, field operations, statistical analysis, shared services, printing, wireless access, CCTV monitoring, and controlled internet access.

The proposed architecture uses an edge router for the WAN and NAT boundary, a Layer 3 core switch for inter-VLAN routing, and dedicated access switches for users, services, printers, wireless, and CCTV. CCTV traffic is isolated in its own VLAN, while device administration is protected through a dedicated management VLAN and SSH-based access control.

## Design Package Contents

| Document | Purpose |
| --- | --- |
| [client-requirements.md](client-requirements.md) | Defines the business, operational, security, and technical requirements for the field-office network. |
| [physical-topology.md](physical-topology.md) | Presents the physical network layout, device inventory, cabling approach, and equipment roles. |
| [logical-topology.md](logical-topology.md) | Defines VLANs, routing, NAT, security zones, and traffic-control policy. |
| [ip-addressing-plan.md](ip-addressing-plan.md) | Provides the complete VLSM addressing plan for the assigned `172.30.56.0/23` network. |
| [README.md](README.md) | Confirms the initial GitHub repository structure and completed design package status. |

## Architecture Overview

- Core/access topology for a clean and supportable field-office network.
- VLAN separation for management, servers, administration, field operations, analysts, guest wireless, printers, and CCTV.
- NAT/PAT on the edge router for internal-to-external address translation.
- Dedicated CCTV network segment with controlled access to the NVR.
- Dedicated management segment for router, switch, and access point administration.
- Reserved address capacity for controlled growth.

## Repository Structure

```text
.
|-- README.md
|-- client-requirements.md
|-- physical-topology.md
|-- logical-topology.md
`-- ip-addressing-plan.md
```

## Repository Status

| Item | Status |
| --- | --- |
| Repository URL | [CMPG-325-stats-sa-mafikeng-network](https://github.com/kudzaimudzingwa40-cmd/CMPG-325-stats-sa-mafikeng-network) |
| Branch | `main` |
| Visible repository files | Five design files |
| Documentation status | Complete |
