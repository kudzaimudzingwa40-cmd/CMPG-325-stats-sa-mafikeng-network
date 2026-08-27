# Testing and Evidence Plan

Project name: **Stats SA Mafikeng Field Office (Mahikeng)**

## Purpose

Milestone 1 is mainly a design review, but the project brief also expects the final network to be tested and supported by evidence. This plan lists the proof that should be captured when the Packet Tracer implementation is built.

## Required Evidence

| Test area | Evidence to capture | Expected result |
| --- | --- | --- |
| Basic device setup | Screenshot or exported configs for device names, VLANs, IPs, and interfaces | Devices match the documented topology and IP plan. |
| DHCP | PC addressing screenshot and DHCP server scopes | User PCs receive correct IP, gateway, and DNS values. |
| Inter-VLAN routing | Ping tests between permitted VLANs | Allowed VLANs can reach required internal services. |
| NAT challenge | `show ip nat translations` and internal-to-external test | Internal `172.30.56.0/23` hosts translate through R1 outside address. |
| CCTV segmentation | Ping/traffic tests from CCTV VLAN to NVR and user VLANs | Cameras can reach NVR, but cannot reach normal user VLANs. |
| Guest/training isolation | Ping tests from guest VLAN to internal VLANs and outside test server | Guest VLAN is blocked from internal networks but can reach allowed outside access. |
| Management security | SSH test from authorized admin host and failed access from normal user VLAN | Device administration is restricted. |
| Printer access | User-to-printer test | Staff VLANs can reach shared printers where allowed. |
| Troubleshooting record | Notes on issues fixed during build | Reviewer can see the design was tested and corrected. |

## Suggested Packet Tracer Commands and Checks

| Device | Command / check | Purpose |
| --- | --- | --- |
| R1 | `show ip interface brief` | Confirm inside and outside interfaces are up. |
| R1 | `show ip route` | Confirm default route and inside return path. |
| R1 | `show ip nat translations` | Prove NAT/PAT is working. |
| R1 | `show ip nat statistics` | Show NAT activity and interface roles. |
| SW-CORE | `show vlan brief` | Confirm VLANs exist. |
| SW-CORE | `show ip interface brief` | Confirm SVI gateways are up. |
| SW-CORE | `show ip route` | Confirm inter-VLAN routing and default route. |
| Access switches | `show interfaces trunk` | Confirm trunk links to SW-CORE. |
| Access switches | `show interfaces status` | Confirm endpoints are connected to correct access ports. |

## Evidence Folder Plan

Store screenshots and notes in `evidence/` using clear names:

```text
evidence/
|-- 01-dhcp-vlan30-admin.png
|-- 02-dhcp-vlan40-field-operations.png
|-- 03-inter-vlan-server-access.png
|-- 04-nat-translations-r1.png
|-- 05-cctv-to-nvr-allowed.png
|-- 06-cctv-to-user-vlan-denied.png
|-- 07-management-ssh-authorized.png
|-- 08-management-ssh-unauthorized-denied.png
`-- troubleshooting-notes.md
```

## Final Demo Talking Points

- Explain why VLANs were used instead of a flat LAN.
- Show how the CCTV change request was handled.
- Show the NAT inside and outside interfaces on R1.
- Show one successful internal-to-external test and the NAT translation entry.
- Show one successful CCTV-to-NVR test and one denied CCTV-to-user test.
- Explain how device administration is protected after the unauthorized-change incident.
