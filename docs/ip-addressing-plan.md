# IP Addressing Plan

Assigned block: `172.30.56.0/23`

Usable range: `172.30.56.1` to `172.30.57.254`

## Addressing Rules

- The first usable address in each VLAN is the default gateway.
- Infrastructure devices and servers use static addresses.
- User devices use DHCP.
- CCTV cameras may use static addresses or DHCP reservations.
- Spare ranges are intentionally left for later expansion.

## Internal VLAN Addressing

| VLAN | Name | Subnet | Gateway | DHCP / Host Allocation | Notes |
| --- | --- | --- | --- | --- | --- |
| 10 | Network Management | `172.30.56.0/27` | `172.30.56.1` | Static: `172.30.56.2-172.30.56.30` | Router, switches, AP management. |
| 20 | Servers and Core Services | `172.30.56.32/27` | `172.30.56.33` | Static: `172.30.56.34-172.30.56.62` | DHCP/DNS, file/app server, NVR. |
| 30 | Administration and Reception | `172.30.56.64/26` | `172.30.56.65` | DHCP: `172.30.56.80-172.30.56.120` | Admin, reception, security viewing PC. |
| 40 | Field Operations / Data Capture | `172.30.56.128/25` | `172.30.56.129` | DHCP: `172.30.56.140-172.30.56.240` | Largest user group. |
| 50 | GIS / Statistical Analysis | `172.30.57.0/26` | `172.30.57.1` | DHCP: `172.30.57.10-172.30.57.55` | Analyst workstations. |
| 60 | Training / Guest Wi-Fi | `172.30.57.64/27` | `172.30.57.65` | DHCP: `172.30.57.70-172.30.57.90` | Internet-only or limited access. |
| 70 | Printers and Shared Devices | `172.30.57.96/28` | `172.30.57.97` | Static: `172.30.57.98-172.30.57.110` | Printers and shared office devices. |
| 99 | Core-to-Edge Transit | `172.30.57.112/30` | N/A | SW-CORE: `172.30.57.113`; R1 inside: `172.30.57.114` | Routed internal transit. |
| 80 | CCTV Cameras | `172.30.57.128/27` | `172.30.57.129` | Cameras: `172.30.57.130-172.30.57.149` | Segmented CCTV camera VLAN. |
| Spare | Future small VLAN | `172.30.57.160/27` | TBD | Reserved | Future services or department. |
| Spare | Future expansion | `172.30.57.192/26` | TBD | Reserved | Growth capacity. |

## Key Static Addresses

| Device / Service | IP Address | VLAN |
| --- | --- | --- |
| SW-CORE management | `172.30.56.2` | 10 |
| R1 management/inside reference | `172.30.56.3` | 10 |
| SW-ADMIN management | `172.30.56.4` | 10 |
| SW-OPS management | `172.30.56.5` | 10 |
| SW-SERVICES management | `172.30.56.6` | 10 |
| SW-CCTV management | `172.30.56.7` | 10 |
| DHCP/DNS server | `172.30.56.34` | 20 |
| File/application server | `172.30.56.35` | 20 |
| CCTV NVR | `172.30.56.40` | 20 |
| Security viewing workstation | `172.30.56.66` | 30 |

## Simulated Outside Network

These outside addresses are for Packet Tracer simulation only and are not part of the assigned internal block.

| Link / Device | Addressing |
| --- | --- |
| ISP-to-R1 WAN subnet | `203.0.113.0/30` |
| ISP router | `203.0.113.1` |
| R1 outside interface | `203.0.113.2` |
| Example external test server | `198.51.100.10` |

## NAT Summary

- Inside local network: `172.30.56.0/23`
- Inside global address: R1 outside interface `203.0.113.2`
- Translation type: PAT/overload
- Expected test: inside PCs should ping or access the simulated external server through R1 NAT.

## Growth Capacity

The design leaves `172.30.57.160/27` and `172.30.57.192/26` unused for future departments, extra cameras, additional servers, or revised client requirements.

