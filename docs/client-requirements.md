# Client Requirements

## Client Profile

| Item | Detail |
| --- | --- |
| Client | Stats SA Mafikeng Field Office (Mahikeng) |
| Industry | Government |
| Address block | `172.30.56.0/23` |
| Assigned challenge | NAT inside/outside address translation |
| Change request | CCTV cameras added; CCTV traffic must be segmented |
| Security constraint | Secure all network device administration |
| Implementation target | Cisco Packet Tracer |

## Requirements

| ID | Requirement | Design Response |
| --- | --- | --- |
| CR-01 | Provide reliable LAN connectivity for the field office. | Use a core switch with access switches for departments and services. |
| CR-02 | Support government office functions without mixing all devices into one flat network. | Use VLANs for administration, operations, analysts, servers, printers, guest/training wireless, CCTV, and management. |
| CR-03 | Provide basic network services. | Provide DHCP per user VLAN, DNS for internal name resolution, and static addressing for infrastructure and servers. |
| CR-04 | Allow internal users to reach external services. | Configure NAT/PAT on the edge router from `172.30.56.0/23` to the simulated ISP-facing address. |
| CR-05 | Add CCTV cameras while keeping camera traffic segmented. | Create a dedicated CCTV VLAN and restrict it using ACLs so cameras communicate only with the NVR/security services. |
| CR-06 | Secure device administration. | Use a management VLAN, SSH access, encrypted credentials, secure enable access, login banners, and access restrictions. |
| CR-07 | Use the assigned address block efficiently. | Subnet `172.30.56.0/23` using VLSM with room for growth. |
| CR-08 | Produce a testable Packet Tracer design. | Use Packet Tracer-supported routers, Layer 3 switches, access switches, servers, PCs, wireless APs, and IP cameras. |
| CR-09 | Keep design evidence organized in GitHub. | Store requirements, topologies, IP plan, configs, Packet Tracer files, and evidence in this repository. |

## Security and Access Requirements

- Administrative access must be available only through the management VLAN.
- Use SSH instead of Telnet.
- Encrypt stored device passwords.
- Use role-appropriate VLAN access ports on access switches.
- Deny CCTV devices from initiating traffic to normal user VLANs.
- Deny guest/training wireless from internal networks except required services such as DHCP and DNS.
- Permit office users to reach shared services and the internet through NAT.

## Review Questions

- Confirm the expected number of PCs, cameras, printers, and servers for the final Packet Tracer topology.
- Confirm whether guest/training wireless is required or should be removed.
- Confirm whether the NVR should remain in the server VLAN or move to a dedicated security server VLAN.

