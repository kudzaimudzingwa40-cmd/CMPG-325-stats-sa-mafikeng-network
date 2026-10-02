# CMPG 325 Project Submission

## Stats SA Mafikeng Field Office Network

**Student:** Kudzai Mudzingwa  
**Module:** CMPG 325 Computer Networks  
**Client:** Stats SA Mafikeng Field Office, Mahikeng  
**Platform:** Cisco Packet Tracer

## Project Overview

This project implements a segmented field-office network using VLANs, router-on-a-stick inter-VLAN routing, NAT/PAT, access-control lists and SSH management. The topology separates Administration, Field, Finance, Human Resources, Guest and CCTV traffic and provides a dedicated management VLAN for network infrastructure.

## Deliverables

| Deliverable | Project evidence |
| --- | --- |
| Packet Tracer implementation | packet-tracer/StatsSA-Mafikeng-Network.pkt |
| Client requirements | client-requirements.md |
| Physical topology | physical-topology.md |
| Logical topology | logical-topology.md |
| IP addressing plan | ip-addressing-plan.md |
| Testing and verification | testing-evidence.md and evidence/ |
| GitHub portfolio | This repository |

## Implemented Features

The implementation includes seven VLANs, 802.1Q trunking, router-on-a-stick routing on R1, NAT/PAT for external connectivity, Guest and CCTV isolation ACLs, VLAN 99 infrastructure management, and SSH remote administration.

## Verification Summary

| Test area | Recorded result |
| --- | --- |
| Management reachability | PC-Admin reached SW1-Core, SW2-Access and SW3-Access management addresses |
| SSH management | PC-Admin established an SSH session to SW1-Core |
| Guest gateway | Successful |
| Guest to Admin | Blocked as required |
| Guest to external server | Successful |
| CCTV gateway | Successful |
| CCTV to Admin | Blocked as required |
| CCTV to external server | Successful |
| NAT/PAT | Four dynamic translations and 12 hits observed |
| ACL enforcement | Guest and CCTV ACL permit/deny counters incremented |

## Conclusion

The project demonstrates VLAN segmentation, controlled routing, edge address translation and access-control enforcement in a Cisco Packet Tracer environment. The implementation provides a clear separation between normal business users, restricted Guest/CCTV networks and infrastructure management while retaining permitted external connectivity.
