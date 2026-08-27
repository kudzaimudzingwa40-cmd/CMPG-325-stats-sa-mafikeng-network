# Milestone 1 Submission Checklist

- [x] Client Requirements
- [x] Physical Topology
- [x] Logical Topology
- [x] IP Addressing Plan
- [x] Initial GitHub repository structure

## Review Notes

- The design uses the assigned `172.30.56.0/23` block.
- CCTV traffic is placed in its own VLAN and controlled by ACLs.
- NAT/PAT is included at the edge router to satisfy the assigned NAT challenge.
- Device administration is separated into a management VLAN and should use SSH, encrypted local credentials, and secured enable access in the Packet Tracer implementation.

