# Stats SA Mafikeng Field Office (Mahikeng)

CMPG 325 Computer Networks individual project portfolio for **Milestone 1 - Client Design Review**.

This repository intentionally contains only the five items requested for Milestone 1. The attached project brief and marking guideline screenshots were treated as assignment source material, not as extra user instructions or extra deliverables.

## Project Details

| Item | Detail |
| --- | --- |
| Project name | Stats SA Mafikeng Field Office (Mahikeng) |
| Course | CMPG 325 - Computer Networks |
| Project ID | CMPG325-2026-097 |
| Client | Stats SA Mafikeng Field Office (Mahikeng) |
| Client type | Government field office |
| Assigned address block | `172.30.56.0/23` |
| Assigned networking challenge | NAT inside/outside address translation |
| Client change request | Add CCTV cameras and segment CCTV traffic |
| Design constraint | Secure all device administration |
| Simulation tool | Cisco Packet Tracer |

## Milestone 1 Deliverables

| No. | Required item | File |
| --- | --- | --- |
| 1 | Client Requirements | [client-requirements.md](client-requirements.md) |
| 2 | Physical Topology | [physical-topology.md](physical-topology.md) |
| 3 | Logical Topology | [logical-topology.md](logical-topology.md) |
| 4 | IP Addressing Plan | [ip-addressing-plan.md](ip-addressing-plan.md) |
| 5 | Initial GitHub Repository | [README.md](README.md) |

No Packet Tracer file, configuration exports, evidence screenshots, or final video files are included in this milestone because those belong to later project stages.

## Design Summary

Stats SA needs a field-office network that is reliable, easy to support, and careful with security. The design therefore uses a simple core/access layout: an edge router for the ISP and NAT boundary, a Layer 3 core switch for inter-VLAN routing, and access switches for office users, services, wireless, printers, and CCTV.

The CCTV change request is handled as a real design requirement, not as an add-on. Cameras sit in their own VLAN, their traffic is kept away from normal users, and only the NVR/security workflow is allowed. Device administration is also separated into a management VLAN so router and switch access is not exposed to every office subnet.

## Repository Structure

```text
.
|-- README.md
|-- client-requirements.md
|-- physical-topology.md
|-- logical-topology.md
`-- ip-addressing-plan.md
```

## GitHub Repository Status

| Item | Status |
| --- | --- |
| Repository URL | [CMPG-325-stats-sa-mafikeng-network](https://github.com/kudzaimudzingwa40-cmd/CMPG-325-stats-sa-mafikeng-network) |
| Remote name | `origin` |
| Active branch | `main` |
| Portfolio status | Limited to the five Milestone 1 deliverables |

Before submission, open the GitHub link and confirm that the repository shows only these five files and that the Markdown topology diagrams render correctly. Then submit the GitHub repository link on eFundi according to the Milestone 1 instructions.

Useful local checks:

```bash
git status --short --branch
git log --oneline --decorate -5
```
