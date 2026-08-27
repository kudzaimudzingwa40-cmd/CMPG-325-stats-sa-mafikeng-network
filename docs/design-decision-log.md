# Design Decision Log

Project name: **Stats SA Mafikeng Field Office (Mahikeng)**

## Purpose

This log records the main design decisions for the Milestone 1 review. It is written so the reviewer can see not only what was chosen, but why it fits the client scenario.

## Decisions

| Decision | Choice | Justification |
| --- | --- | --- |
| Network structure | Core/access topology | A small field office needs a clean and manageable structure. One core switch and several access switches are enough for Packet Tracer and realistic for a branch office. |
| Internet edge | R1 edge router | NAT belongs at the boundary between the private office network and the outside network. This also makes the assigned NAT challenge easy to demonstrate. |
| Internal routing | SW-CORE Layer 3 switch | Keeping inter-VLAN routing on the core switch makes internal traffic efficient and keeps R1 focused on WAN/NAT. |
| VLAN segmentation | Separate VLANs by function | Management, servers, users, wireless, printers, and CCTV have different security needs. VLANs keep those roles clear. |
| CCTV design | Dedicated CCTV VLAN and access switch | The brief specifically says CCTV cameras must be added and their traffic segmented. A separate VLAN and switch area make that requirement visible and testable. |
| NVR placement | NVR in server VLAN | The NVR is a server-type device and should live with controlled services, while cameras remain in the CCTV VLAN. |
| Admin security | Management VLAN plus SSH | The design responds to the previous unauthorized-change incident by limiting device administration paths. |
| Addressing method | VLSM from `172.30.56.0/23` | VLSM gives enough addresses to bigger user groups while preserving spare space. |
| Guest/training access | Separate limited VLAN | Temporary wireless users should not share the same space as staff systems. |
| Printers | Separate small VLAN | Printers are shared devices and should be reachable by users without being placed directly in user VLANs. |

## Alternatives Considered

| Alternative | Reason not selected |
| --- | --- |
| One flat LAN | Too weak for security, does not properly segment CCTV, and would score poorly against the topology and design criteria. |
| Router-on-a-stick for all VLANs | Valid for small labs, but SW-CORE inter-VLAN routing is cleaner and more scalable for this field-office design. |
| CCTV cameras in the server VLAN | Easier to configure, but it does not satisfy the segmentation requirement clearly. |
| NAT on an internal Layer 3 switch | Less appropriate because the router is the natural inside/outside boundary in Packet Tracer. |
| One large `/24` for users | Wastes address space and does not show efficient VLSM planning. |

## Human Design Notes

The design keeps the office understandable. A technician should be able to look at the topology and know where to check first: user issue at the access switch, inter-VLAN issue at SW-CORE, internet issue at R1, camera issue in VLAN 80, and device-login issue in VLAN 10. That kind of clarity matters in a government office where the network must be supportable after the initial setup.
