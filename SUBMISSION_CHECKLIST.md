# Milestone 1 Submission Checklist

Project name: **Stats SA Mafikeng Field Office (Mahikeng)**

## Required Items

- [x] Client Requirements - `docs/client-requirements.md`
- [x] Physical Topology - `docs/physical-topology.md`
- [x] Logical Topology - `docs/logical-topology.md`
- [x] IP Addressing Plan - `docs/ip-addressing-plan.md`
- [x] Initial GitHub Repository - `docs/repository-overview.md`

## Marking Guideline Readiness

- [x] Client needs are explained in the context of a government field office.
- [x] The design uses a complete physical and logical topology, not only a device list.
- [x] VLANs are matched to real office functions: management, servers, administration, field operations, analysts, wireless, printers, and CCTV.
- [x] The assigned `172.30.56.0/23` block is fully subnetted with gateways, DHCP/static ranges, capacity, and spare space.
- [x] NAT inside/outside translation is included at the edge router with a clear verification plan.
- [x] CCTV traffic is segmented and controlled by ACL policy.
- [x] Device administration is secured through a dedicated management VLAN and SSH-based access.
- [x] The GitHub repository is organized for evidence, configs, Packet Tracer files, and future testing screenshots.
- [x] Supporting files explain the design decisions and link the work back to the rubric.

## Final Checks Before Upload

- [x] GitHub remote URL is configured: `https://github.com/kudzaimudzingwa40-cmd/CMPG-325-stats-sa-mafikeng-network.git`
- [x] Local branch `main` tracks `origin/main`.
- [ ] Confirm that GitHub renders the Mermaid diagrams inside the topology Markdown files.
- [ ] Confirm the repository is visible to the marker, or make it public/private with lecturer access as required.
- [ ] Confirm the repository name shown on GitHub matches the lecturer's naming requirement.
- [ ] Upload or submit the GitHub link according to the eFundi milestone instructions.
