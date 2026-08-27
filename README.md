# Stats SA Mafikeng Field Office (Mahikeng)

CMPG 325 Computer Networks individual project portfolio for the client design review.

This repository is prepared for **Milestone 1 - Client Design Review**. I used the attached project brief and marking guideline screenshots as the assignment source material, then separated those instructions from the actual submission items required for this milestone.

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

## Milestone 1 Review Pack

The required Milestone 1 items are ready in this repository:

1. [Client Requirements](docs/client-requirements.md)
2. [Physical Topology](docs/physical-topology.md)
3. [Logical Topology](docs/logical-topology.md)
4. [IP Addressing Plan](docs/ip-addressing-plan.md)
5. [Initial GitHub Repository](docs/repository-overview.md)

I also added supporting review evidence so the marker can quickly see how the submission lines up with the rubric:

- [Milestone 1 Client Design Review](docs/milestone-1-client-design-review.md)
- [Marking Guideline Alignment](docs/marking-guideline-alignment.md)
- [Design Decision Log](docs/design-decision-log.md)
- [Testing and Evidence Plan](docs/testing-and-evidence-plan.md)

## Design Summary

Stats SA needs a field-office network that is reliable, easy to support, and careful with security. The design therefore uses a simple core/access layout: an edge router for the ISP and NAT boundary, a Layer 3 core switch for inter-VLAN routing, and access switches for office users, services, wireless, printers, and CCTV.

The CCTV change request is handled as a real design requirement, not as an add-on. Cameras sit in their own VLAN, their traffic is kept away from normal users, and only the NVR/security workflow is allowed. Device administration is also separated into a management VLAN so router and switch access is not exposed to every office subnet.

## Repository Structure

```text
.
|-- README.md
|-- SUBMISSION_CHECKLIST.md
|-- configs/
|   `-- README.md
|-- docs/
|   |-- client-requirements.md
|   |-- design-decision-log.md
|   |-- ip-addressing-plan.md
|   |-- logical-topology.md
|   |-- marking-guideline-alignment.md
|   |-- milestone-1-client-design-review.md
|   |-- physical-topology.md
|   |-- repository-overview.md
|   |-- testing-and-evidence-plan.md
|   `-- diagrams/
|       |-- logical-topology.mmd
|       `-- physical-topology.mmd
|-- evidence/
|   `-- README.md
`-- packet-tracer/
    `-- README.md
```

## GitHub Setup

The local repository is already initialized on branch `main`. Add the actual GitHub remote URL that matches the project name you created on GitHub, then push:

```bash
git remote add origin https://github.com/<username>/<your-github-repository-name>.git
git push -u origin main
```
