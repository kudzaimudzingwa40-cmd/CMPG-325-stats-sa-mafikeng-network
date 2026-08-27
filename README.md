# CMPG 325 Network Design - Stats SA Mafikeng Field Office

Initial repository for the CMPG 325 client design review milestone.

## Milestone 1 Review Pack

This repository contains the review materials requested for Milestone 1:

1. Client requirements
2. Physical topology
3. Logical topology
4. IP addressing plan
5. Initial GitHub repository structure

The source assignment screenshots were used only as project constraints and marking context. The actual deliverable scope is the Milestone 1 client design review requested above.

## Project Facts Used

- Client: Stats SA Mafikeng Field Office (Mahikeng)
- Industry: Government
- Assigned addressing block: 172.30.56.0/23
- Assigned networking challenge: NAT inside/outside address translation
- Change request: CCTV cameras must be added and their traffic must be segmented
- Security constraint: device administration must be secured
- Tooling target: Cisco Packet Tracer

## Repository Structure

```text
.
|-- README.md
|-- SUBMISSION_CHECKLIST.md
|-- configs/
|-- docs/
|   |-- client-requirements.md
|   |-- ip-addressing-plan.md
|   |-- logical-topology.md
|   |-- milestone-1-client-design-review.md
|   |-- physical-topology.md
|   |-- repository-overview.md
|   `-- diagrams/
|       |-- logical-topology.mmd
|       `-- physical-topology.mmd
|-- evidence/
`-- packet-tracer/
```

## Suggested GitHub Repository Name

`cmpg325-stats-sa-mafikeng-field-office`

After creating the GitHub repository, add it as the remote:

```bash
git remote add origin https://github.com/<username>/cmpg325-stats-sa-mafikeng-field-office.git
git branch -M main
git push -u origin main
```

