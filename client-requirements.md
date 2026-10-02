# Client and Technical Requirements

## Objective

Provide a segmented, manageable field-office network that separates business functions, protects guest and CCTV traffic, supports secure infrastructure administration, and provides controlled external connectivity.

## Implemented Requirements

| ID | Requirement | Implementation | Verification |
| --- | --- | --- | --- |
| R01 | Separate business/security functions | VLANs 10, 20, 30, 40, 50, 60 and 99 | Topology/configuration |
| R02 | Route permitted traffic between VLANs | R1 router-on-a-stick | Dedicated evidence screenshot outstanding |
| R03 | Provide controlled external connectivity | NAT/PAT through R1 | Verified: dynamic translations and 12 hits |
| R04 | Isolate guest users from protected networks | GUEST-ISOLATION ACL | Verified behavior and ACL counters |
| R05 | Isolate CCTV from user/management networks | CCTV-ISOLATION ACL | Verified behavior and ACL counters |
| R06 | Provide infrastructure management network | VLAN 99 | Verified switch reachability |
| R07 | Use secure remote administration | SSH | Verified to SW1-Core |
| R08 | Maintain reviewable technical evidence | Evidence register and screenshots | Partially captured |

## Functional Scope

The implemented topology supports representative Administration, Field, Finance, HR, Guest, and CCTV endpoints. R1 provides the VLAN gateways and policy boundary. The switch hierarchy provides core/access connectivity, while the external server provides a deterministic target for NAT and permitted-connectivity testing.

## Security Requirements

- Guest and CCTV endpoints must not initiate traffic to protected business/management subnets.
- Permitted Guest/CCTV external traffic must continue to function.
- Network infrastructure must use a dedicated management subnet.
- Remote switch administration must use SSH rather than Telnet.
- NAT/PAT must hide internal addressing when traffic traverses the simulated external boundary.

## Non-Functional Requirements

**Maintainability:** consistent device naming, VLAN numbering, and documentation.

**Auditability:** observed test results are separated from expected results; uncollected evidence is explicitly identified.

**Security:** laboratory credentials are not suitable for production and must be replaced before deployment.

**Scalability:** production sizing should account for actual staff count, cameras, wireless clients, printers, growth, redundancy, and WAN capacity.

## Assumptions and Limitations

This repository represents a Cisco Packet Tracer simulation, not an as-built production deployment. It does not model enterprise identity services, high availability, centralized logging/SIEM, production firewall inspection, wireless security architecture, QoS, UPS/power engineering, or physical cabling records.

## Acceptance Position

Guest isolation, CCTV isolation, external reachability, NAT/PAT operation, management reachability, and an authorized SSH session were observed. DHCP, dedicated inter-VLAN, and routing-table evidence captures remain outstanding and must not be reported as verified until captured.
