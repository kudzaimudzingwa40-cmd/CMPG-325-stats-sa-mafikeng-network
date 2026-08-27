# IP Addressing Plan

Project: **Stats SA Mafikeng Field Office Network Design**

Prepared by: **Kudzai Mudzingwa**

Status: **Complete**

Assigned block: `172.30.56.0/23`

Usable range: `172.30.56.1` to `172.30.57.254`

Total usable internal host addresses: 510

## Addressing Method

The address plan uses VLSM so that larger user groups receive larger subnets and infrastructure networks receive smaller, controlled ranges. The plan keeps the first usable address as the default gateway in each VLAN, reserves low addresses for infrastructure, and uses DHCP for ordinary user devices.

This approach is efficient because it does not waste a full `/24` on every department, while still reserving growth space for planned network expansion.

## Internal VLAN Addressing

| VLAN | Name | Subnet | Mask | Usable host range | Broadcast | Gateway | Capacity | Allocation |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 10 | Network Management | `172.30.56.0/27` | `255.255.255.224` | `172.30.56.1-172.30.56.30` | `172.30.56.31` | `172.30.56.1` | 30 hosts | Static infrastructure |
| 20 | Servers and Core Services | `172.30.56.32/27` | `255.255.255.224` | `172.30.56.33-172.30.56.62` | `172.30.56.63` | `172.30.56.33` | 30 hosts | Static servers |
| 30 | Administration and Reception | `172.30.56.64/26` | `255.255.255.192` | `172.30.56.65-172.30.56.126` | `172.30.56.127` | `172.30.56.65` | 62 hosts | DHCP users plus security viewer |
| 40 | Field Operations / Data Capture | `172.30.56.128/25` | `255.255.255.128` | `172.30.56.129-172.30.56.254` | `172.30.56.255` | `172.30.56.129` | 126 hosts | Largest DHCP user pool |
| 50 | GIS / Statistical Analysis | `172.30.57.0/26` | `255.255.255.192` | `172.30.57.1-172.30.57.62` | `172.30.57.63` | `172.30.57.1` | 62 hosts | DHCP specialist users |
| 60 | Training / Guest Wi-Fi | `172.30.57.64/27` | `255.255.255.224` | `172.30.57.65-172.30.57.94` | `172.30.57.95` | `172.30.57.65` | 30 hosts | Controlled DHCP wireless |
| 70 | Printers and Shared Devices | `172.30.57.96/28` | `255.255.255.240` | `172.30.57.97-172.30.57.110` | `172.30.57.111` | `172.30.57.97` | 14 hosts | Static printers |
| 99 | Core-to-Edge Transit | `172.30.57.112/30` | `255.255.255.252` | `172.30.57.113-172.30.57.114` | `172.30.57.115` | Point-to-point | 2 hosts | SW-CORE to R1 |
| 80 | CCTV Cameras | `172.30.57.128/27` | `255.255.255.224` | `172.30.57.129-172.30.57.158` | `172.30.57.159` | `172.30.57.129` | 30 hosts | Cameras and CCTV devices |
| Spare | Transit spare 1 | `172.30.57.116/30` | `255.255.255.252` | `172.30.57.117-172.30.57.118` | `172.30.57.119` | TBD | 2 hosts | Reserved |
| Spare | Transit spare 2 | `172.30.57.120/30` | `255.255.255.252` | `172.30.57.121-172.30.57.122` | `172.30.57.123` | TBD | 2 hosts | Reserved |
| Spare | Transit spare 3 | `172.30.57.124/30` | `255.255.255.252` | `172.30.57.125-172.30.57.126` | `172.30.57.127` | TBD | 2 hosts | Reserved |
| Spare | Reserved small VLAN | `172.30.57.160/27` | `255.255.255.224` | `172.30.57.161-172.30.57.190` | `172.30.57.191` | Reserved | 30 hosts | Reserved |
| Spare | Reserved expansion block | `172.30.57.192/26` | `255.255.255.192` | `172.30.57.193-172.30.57.254` | `172.30.57.255` | Reserved | 62 hosts | Reserved |

## DHCP Pool Plan

| VLAN | DHCP pool | Default gateway | DNS server | Excluded / static range |
| --- | --- | --- | --- | --- |
| 30 | `172.30.56.80-172.30.56.120` | `172.30.56.65` | `172.30.56.34` | `172.30.56.65-172.30.56.79`, `172.30.56.121-172.30.56.126` |
| 40 | `172.30.56.140-172.30.56.240` | `172.30.56.129` | `172.30.56.34` | `172.30.56.129-172.30.56.139`, `172.30.56.241-172.30.56.254` |
| 50 | `172.30.57.10-172.30.57.55` | `172.30.57.1` | `172.30.56.34` | `172.30.57.1-172.30.57.9`, `172.30.57.56-172.30.57.62` |
| 60 | `172.30.57.70-172.30.57.90` | `172.30.57.65` | `172.30.56.34` | `172.30.57.65-172.30.57.69`, `172.30.57.91-172.30.57.94` |

## Static Address Plan

| Device / Service | IP address | VLAN | Notes |
| --- | --- | --- | --- |
| SW-CORE management | `172.30.56.2` | 10 | Core switch management IP. |
| R1 management reference | `172.30.56.3` | 10 | Used if a dedicated management interface is simulated. |
| SW-ADMIN management | `172.30.56.4` | 10 | Access switch management. |
| SW-OPS management | `172.30.56.5` | 10 | Access switch management. |
| SW-SERVICES management | `172.30.56.6` | 10 | Access switch management. |
| SW-CCTV management | `172.30.56.7` | 10 | CCTV access switch management. |
| Wireless AP management | `172.30.56.8` | 10 | Managed from VLAN 10. |
| DHCP/DNS server | `172.30.56.34` | 20 | DHCP scopes and DNS. |
| File/application server | `172.30.56.35` | 20 | Simulated office services. |
| CCTV NVR | `172.30.56.40` | 20 | Receives camera traffic. |
| Security viewing workstation | `172.30.56.66` | 30 | Authorized to view NVR. |
| Printer 1 | `172.30.57.98` | 70 | Static printer. |
| Printer 2 | `172.30.57.99` | 70 | Static printer. |
| Camera 1 | `172.30.57.130` | 80 | Static or DHCP reservation. |
| Camera 2 | `172.30.57.131` | 80 | Static or DHCP reservation. |
| Camera 3 | `172.30.57.132` | 80 | Static or DHCP reservation. |
| Camera 4 | `172.30.57.133` | 80 | Static or DHCP reservation. |

## Core-to-Edge Transit

| Device | Interface role | IP address |
| --- | --- | --- |
| SW-CORE | Routed transit to R1 | `172.30.57.113/30` |
| R1 | NAT inside interface | `172.30.57.114/30` |

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
| Inside local network | `172.30.56.0/23` |
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
