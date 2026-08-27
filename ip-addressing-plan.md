# IP Addressing Plan

Project: **Stats SA Mafikeng Field Office Network Design**

Prepared by: **Kudzai Mudzingwa**

Status: **Complete**

Assigned block: `172.30.66.0/23`

Usable range: `172.30.66.1` to `172.30.67.254`

Total usable internal host addresses: 510

## Addressing Method

The address plan uses VLSM so that larger user groups receive larger subnets and infrastructure networks receive smaller, controlled ranges. The plan keeps the first usable address as the default gateway in each VLAN, reserves low addresses for infrastructure, and uses DHCP for ordinary user devices.

This approach is efficient because it does not waste a full `/24` on every department, while still reserving growth space for planned network expansion.

## Internal VLAN Addressing

| VLAN | Name | Subnet | Mask | Usable host range | Broadcast | Gateway | Capacity | Allocation |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 10 | Network Management | `172.30.66.0/27` | `255.255.255.224` | `172.30.66.1-172.30.56.30` | `172.30.66.31` | `172.30.66.1` | 30 hosts | Static infrastructure |
| 20 | Servers and Core Services | `172.30.66.32/27` | `255.255.255.224` | `172.30.66.33-172.30.56.62` | `172.30.66.63` | `172.30.66.33` | 30 hosts | Static servers |
| 30 | Administration and Reception | `172.30.66.64/26` | `255.255.255.192` | `172.30.66.65-172.30.56.126` | `172.30.66.127` | `172.30.66.65` | 62 hosts | DHCP users plus security viewer |
| 40 | Field Operations / Data Capture | `172.30.66.128/25` | `255.255.255.128` | `172.30.66.129-172.30.56.254` | `172.30.66.255` | `172.30.66.129` | 126 hosts | Largest DHCP user pool |
| 50 | GIS / Statistical Analysis | `172.30.67.0/26` | `255.255.255.192` | `172.30.67.1-172.30.57.62` | `172.30.67.63` | `172.30.67.1` | 62 hosts | DHCP specialist users |
| 60 | Training / Guest Wi-Fi | `172.30.67.64/27` | `255.255.255.224` | `172.30.67.65-172.30.57.94` | `172.30.67.95` | `172.30.67.65` | 30 hosts | Controlled DHCP wireless |
| 70 | Printers and Shared Devices | `172.30.67.96/28` | `255.255.255.240` | `172.30.67.97-172.30.57.110` | `172.30.67.111` | `172.30.67.97` | 14 hosts | Static printers |
| 99 | Core-to-Edge Transit | `172.30.67.112/30` | `255.255.255.252` | `172.30.57.113-172.30.67.114` | `172.30.67.115` | Point-to-point | 2 hosts | SW-CORE to R1 |
| 80 | CCTV Cameras | `172.30.67.128/27` | `255.255.255.224` | `172.30.67.129-172.30.57.158` | `172.30.67.159` | `172.30.67.129` | 30 hosts | Cameras and CCTV devices |
| Spare | Transit spare 1 | `172.30.67.116/30` | `255.255.255.252` | `172.30.67.117-172.30.57.118` | `172.30.67.119` | TBD | 2 hosts | Reserved |
| Spare | Transit spare 2 | `172.30.67.120/30` | `255.255.255.252` | `172.30.67.121-172.30.57.122` | `172.30.67.123` | TBD | 2 hosts | Reserved |
| Spare | Transit spare 3 | `172.30.67.124/30` | `255.255.255.252` | `172.30.67.125-172.30.57.126` | `172.30.67.127` | TBD | 2 hosts | Reserved |
| Spare | Reserved small VLAN | `172.30.67.160/27` | `255.255.255.224` | `172.30.67.161-172.30.57.190` | `172.30.67.191` | Reserved | 30 hosts | Reserved |
| Spare | Reserved expansion block | `172.30.67.192/26` | `255.255.255.192` | `172.30.67.193-172.30.67.254` | `172.30.67.255` | Reserved | 62 hosts | Reserved |

## DHCP Pool Plan

| VLAN | DHCP pool | Default gateway | DNS server | Excluded / static range |
| --- | --- | --- | --- | --- |
| 30 | `172.30.66.80-172.30.66.120` | `172.30.66.65` | `172.30.66.34` | `172.30.66.65-172.30.66.79`, `172.30.66.121-172.30.66.126` |
| 40 | `172.30.66.140-172.30.66.240` | `172.30.66.129` | `172.30.66.34` | `172.30.66.129-172.30.66.139`, `172.30.66.241-172.30.66.254` |
| 50 | `172.30.67.10-172.30.67.55` | `172.30.67.1` | `172.30.66.34` | `172.30.67.1-172.30.67.9`, `172.30.67.56-172.30.67.62` |
| 60 | `172.30.67.70-172.30.67.90` | `172.30.67.65` | `172.30.66.34` | `172.30.67.65-172.30.67.69`, `172.30.67.91-172.30.67.94` |

## Static Address Plan

| Device / Service | IP address | VLAN | Notes |
| --- | --- | --- | --- |
| SW-CORE management | `172.30.66.2` | 10 | Core switch management IP. |
| R1 management reference | `172.30.66.3` | 10 | Used if a dedicated management interface is simulated. |
| SW-ADMIN management | `172.30.66.4` | 10 | Access switch management. |
| SW-OPS management | `172.30.66.5` | 10 | Access switch management. |
| SW-SERVICES management | `172.30.66.6` | 10 | Access switch management. |
| SW-CCTV management | `172.30.66.7` | 10 | CCTV access switch management. |
| Wireless AP management | `172.30.66.8` | 10 | Managed from VLAN 10. |
| DHCP/DNS server | `172.30.66.34` | 20 | DHCP scopes and DNS. |
| File/application server | `172.30.66.35` | 20 | Simulated office services. |
| CCTV NVR | `172.30.66.40` | 20 | Receives camera traffic. |
| Security viewing workstation | `172.30.66.66` | 30 | Authorized to view NVR. |
| Printer 1 | `172.30.67.98` | 70 | Static printer. |
| Printer 2 | `172.30.67.99` | 70 | Static printer. |
| Camera 1 | `172.30.67.130` | 80 | Static or DHCP reservation. |
| Camera 2 | `172.30.67.131` | 80 | Static or DHCP reservation. |
| Camera 3 | `172.30.67.132` | 80 | Static or DHCP reservation. |
| Camera 4 | `172.30.67.133` | 80 | Static or DHCP reservation. |

## Core-to-Edge Transit

| Device | Interface role | IP address |
| --- | --- | --- |
| SW-CORE | Routed transit to R1 | `172.30.67.113/30` |
| R1 | NAT inside interface | `172.30.67.114/30` |

## Simulated Outside Network

These outside addresses are for Packet Tracer simulation only. They are not part of the assigned internal address block.

| Device / link | Addressing |
| --- | --- |
| ISP-to-R1 WAN subnet | `203.0.113.0/30` |
| ISP router | `203.0.113.1` |
| R1 outside interface | `203.0.113.2` |
| External test server | `198.51.100.10` |

## NAT Addressing Summary

| Item | Value |
| --- | --- |
| Inside local network | `172.30.66.0/23` |
| NAT wildcard | `0.0.1.255` |
| Inside global address | R1 outside interface `203.0.113.2` |
| Translation type | PAT/overload |
| Expected verification | Internal PC reaches `198.51.100.10`; R1 shows active NAT translations. |

## Why the Addressing Plan Is Efficient

- Large groups receive large subnets: field operations gets a `/25`, while admin and analysts get `/26` networks.
- Infrastructure networks are smaller and controlled: management and servers use `/27` networks.
- Printers use a `/28` because they do not need many addresses.
- The routed link between SW-CORE and R1 uses a `/30`, which is appropriate for two interfaces.
- CCTV receives its own `/27`, enough for the baseline cameras and planned expansion.
- All remaining address space is documented as spare, so there are no unexplained gaps in the assigned block.
