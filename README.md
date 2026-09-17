# Stats SA Mafikeng Field Office Network Design

Professional Cisco Packet Tracer network design for the **Stats SA Mafikeng Field Office (Mahikeng)**.

| Item | Detail |
| --- | --- |
| Prepared by | Kudzai Mudzingwa |
| Project | CMPG 325 Computer Networks |
| Client | Stats SA Mafikeng Field Office |
| Location | Mahikeng, North West, South Africa |
| Assigned feature | NAT inside/outside address translation (PAT overload) |
| Security enhancement | CCTV VLAN segmentation and protected device administration |
| Internal address block | `172.30.66.0/23` |
| Simulation platform | Cisco Packet Tracer |
| Repository status | Submission package |

## Submission Items

### 1. Working Packet Tracer file
The final `.pkt` simulation file should be stored in the repository as:

`packet-tracer/StatsSA-Mafikeng-Network.pkt`

> GitHub's text-file API used for this repository cannot upload binary Packet Tracer files. The `.pkt` must therefore be uploaded from Cisco Packet Tracer/Git locally. The configuration and verification requirements are documented in `testing-evidence.md`.

### 2. Assigned feature implemented — NAT/PAT
The assigned feature is **NAT inside/outside address translation** on R1.

Required implementation:

```text
Inside LAN:       172.30.66.0/23
R1 inside:        172.30.67.114/30
R1 outside:       203.0.113.2/30
NAT type:         PAT overload
NAT ACL:          permit 172.30.66.0 0.0.1.255
External target:  198.51.100.10
```

Example R1 configuration:

```cisco
access-list 1 permit 172.30.66.0 0.0.1.255

interface GigabitEthernet0/0
 ip address 172.30.67.114 255.255.255.252
 ip nat inside
 no shutdown

interface GigabitEthernet0/1
 ip address 203.0.113.2 255.255.255.252
 ip nat outside
 no shutdown

ip nat inside source list 1 interface GigabitEthernet0/1 overload
ip route 172.30.66.0 255.255.254.0 172.30.67.113
ip route 0.0.0.0 0.0.0.0 203.0.113.1
```

### 3. Testing evidence
The required evidence is documented in **testing-evidence.md**. Packet Tracer screenshots should show successful connectivity and NAT translation rather than only configuration.

Minimum evidence:
- End device receives a valid DHCP address.
- Internal host can ping its VLAN gateway.
- Internal host can reach `198.51.100.10`.
- R1 `show ip nat translations` displays translations.
- R1 `show ip nat statistics` confirms inside/outside operation.
- `show ip route` confirms the internal and default routes.
- CCTV host can reach the NVR while CCTV-to-user traffic is restricted.
- SSH management is reachable only from an authorized management host.

### 4. Updated GitHub portfolio
The repository contains:
- `README.md` — project overview and submission checklist.
- `client-requirements.md` — client and technical requirements.
- `physical-topology.md` — physical design and device inventory.
- `logical-topology.md` — VLANs, routing, NAT, and security policy.
- `ip-addressing-plan.md` — VLSM addressing and static/DHCP allocation.
- `testing-evidence.md` — practical test procedure and evidence checklist.
- `packet-tracer/` — location reserved for the final `.pkt` file.

## Repository Structure

```text
.
|-- README.md
|-- client-requirements.md
|-- physical-topology.md
|-- logical-topology.md
|-- ip-addressing-plan.md
|-- testing-evidence.md
`-- packet-tracer/
    `-- StatsSA-Mafikeng-Network.pkt   # upload from Packet Tracer
```

## Design Summary
The network uses a Layer 3 core switch for inter-VLAN routing and an edge router for the WAN/NAT boundary. VLANs separate management, servers, administration, field operations, GIS/statistics, guest/training wireless, printers, and CCTV.

CCTV is isolated in VLAN 80, while management access is protected through VLAN 10 and SSH. PAT on R1 provides controlled external connectivity for internal private addresses.

## Submission Status
| Requirement | Repository status |
| --- | --- |
| Client requirements | Complete |
| Physical topology | Complete |
| Logical topology | Complete |
| IP addressing plan | Complete |
| Assigned NAT/PAT feature specification | Complete |
| Testing procedure/evidence template | Complete |
| Packet Tracer `.pkt` | **Requires local Packet Tracer upload** |