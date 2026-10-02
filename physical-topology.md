# Physical Topology

## Implemented Layout

The Packet Tracer implementation uses a compact hierarchical topology suitable for a small branch/field-office simulation.

```text
External-Test-Server
        |
       R1
        |
    SW1-Core
     /     \
SW2-Access  SW3-Access
 /  |  \     /  |  \
Admin Field Finance HR Guest CCTV
```

## Device Inventory

| Device | Model / type | Role |
| --- | --- | --- |
| R1 | Cisco 2911 | Inter-VLAN routing, ACL enforcement, NAT/PAT edge |
| SW1-Core | Cisco 2960-24TT | Core aggregation and trunk distribution |
| SW2-Access | Cisco 2960-24TT | Admin, Field, Finance access |
| SW3-Access | Cisco 2960-24TT | HR, Guest, CCTV access |
| External-Test-Server | Packet Tracer Server-PT | Simulated external connectivity target |
| PC-Admin | PC-PT | Administration and management test host |
| PC-Field | PC-PT | Field endpoint |
| PC-Finance | PC-PT | Finance endpoint |
| PC-HR | PC-PT | HR endpoint |
| PC-Guest | PC-PT | Restricted guest endpoint |
| PC-CCTV | PC-PT | Restricted CCTV endpoint |

## Confirmed Access-Port Mapping

| Access switch | Port | Endpoint |
| --- | --- | --- |
| SW2-Access | Fa0/2 | PC-Admin |
| SW2-Access | Fa0/3 | PC-Field |
| SW2-Access | Fa0/4 | PC-Finance |
| SW3-Access | Fa0/2 | PC-HR |
| SW3-Access | Fa0/3 | PC-Guest |
| SW3-Access | Fa0/4 | PC-CCTV |

R1's internal trunk uses `GigabitEthernet0/1`. The final topology screenshot shows the required links active.

## Cabling and Link Roles

- Endpoint-to-switch connections are Ethernet access links.
- SW2-Access and SW3-Access uplinks to SW1-Core are 802.1Q trunks.
- SW1-Core to R1 carries the VLAN trunk required for router-on-a-stick.
- R1 to External-Test-Server represents the external/WAN-side test segment.

## Deployment Considerations

A real site should document exact patch-panel, rack, switch-port, cable-ID, power/UPS, and physical-security details. Production access switches should also be selected according to PoE, port-density, redundancy, and environmental requirements rather than solely Packet Tracer availability.
