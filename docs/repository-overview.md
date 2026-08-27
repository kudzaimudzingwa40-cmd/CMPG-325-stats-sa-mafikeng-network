# Initial GitHub Repository

## Purpose

This repository is the project portfolio for the Stats SA Mafikeng Field Office network design. It is organized so a reviewer can follow the design decisions, implementation files, evidence, and final testing record.

## Current Milestone 1 Contents

| Path | Purpose |
| --- | --- |
| `README.md` | Repository landing page and project summary. |
| `SUBMISSION_CHECKLIST.md` | Milestone 1 review checklist. |
| `docs/client-requirements.md` | Client requirements and design response. |
| `docs/physical-topology.md` | Physical network topology and device roles. |
| `docs/logical-topology.md` | VLANs, routing, NAT, and security policy. |
| `docs/ip-addressing-plan.md` | VLSM addressing plan for `172.30.56.0/23`. |
| `docs/diagrams/` | Mermaid diagram source files for topology diagrams. |
| `packet-tracer/` | Placeholder for the Packet Tracer `.pkt` file in later milestones. |
| `configs/` | Placeholder for exported router and switch configurations. |
| `evidence/` | Placeholder for screenshots, test evidence, and verification notes. |

## Recommended Repository Workflow

1. Keep one GitHub repository for the whole project.
2. Commit each meaningful milestone update with a clear message.
3. Store the Packet Tracer file in `packet-tracer/`.
4. Store exported router/switch configs in `configs/`.
5. Store ping tests, NAT tests, VLAN tests, and screenshots in `evidence/`.
6. Keep documentation updated whenever the topology or addressing plan changes.

## Suggested Initial Commands

```bash
git status
git add .
git commit -m "Add milestone 1 client design review"
git remote add origin https://github.com/<username>/cmpg325-stats-sa-mafikeng-field-office.git
git push -u origin main
```

