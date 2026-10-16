# Evidence Register

This directory contains the Packet Tracer screenshots currently available. The supplied attachment and the repository file  StatsSA-Mafikeng-Network.pkt were byte-for-byte identical when checked (SHA-256: 1846678dcb4c2435c53dafe48535db552dd1e7c47ff97ff0d68433ad6f987db4). No new simulator screenshots or test results were generated while preparing this register; the Packet Tracer application is not available in this environment.

## Existing screenshots

| Screenshot | What it visibly shows | Limitation |
|---|---|---|
| [Existing topology view](existing-topology-view.png) | Packet Tracer logical workspace with the router, switches, endpoints, and external server. | The title bar shows  project.pkt, not the submitted filename. The Server–R1 link indicator appears red. Reopen the submitted file, confirm the link state, and recapture before using this as final topology evidence. |
| [Management and SSH session](management-ssh-session.png) | PC-Admin ping output to 192.168.99.4 and a later SW1-Core CLI prompt. | Failed login/timeout attempts appear before the prompt. Recapture a clean successful SSH session for presentation. This image does not show DHCP, inter-VLAN routing, or the routing table. |

The test record separately reports results for management reachability, SSH, Guest/CCTV restrictions, external reachability, and NAT/ACL counters. Those written records are not substitutes for screenshots of the corresponding Packet Tracer outputs. See [testing-evidence.md](../testing-evidence.md).

## Final evidence to capture in Packet Tracer

Use the saved  StatsSA-Mafikeng-Network.pkt file. Save screenshots directly into this directory with clear names. Do not mark a test verified in the report until its actual output has been captured.

| Suggested filename | Capture | Minimum content to show |
|---|---|---|
|  01-final-topology.png | Logical workspace after reopening the submitted file | Device names and all required links visibly up; the Packet Tracer title/file name should identify the submitted file. |
|  02-vlans-and-trunks.png | Switch CLI:  show vlan brief and  show interfaces trunk | VLAN membership and active trunk links relevant to VLANs 10, 20, 30, 40, 50, 60, and 99. |
|  03-router-interfaces-routes.png | R1 CLI:  show ip interface brief and  show ip route | Router subinterfaces, status, and connected VLAN routes. |
|  04-inter-vlan-test.png | PC-Admin to a real endpoint in another business VLAN | Show the actual source/destination addresses (use  ipconfig to identify endpoint addressing) and successful host-to-host ping replies. A ping to a gateway alone is not host-to-host inter-VLAN evidence. |
|  05-guest-cctv-policy.png | Guest and CCTV test outputs plus R1 ACL counters | Show the tested gateway/external paths succeeding, the tested Admin path being denied, and  show access-lists counters. State only the destinations actually tested. |
|  06-nat-verification.png | R1 after external test traffic:  show ip nat translations and  show ip nat statistics | Active translations and counters. Check the actual NAT-inside subinterfaces, including whether VLAN 99 is included, before reconciling the report. |
|  07-ssh-management.png | PC-Admin SSH session to SW1-Core | Successful prompt with no password or credential visible; avoid showing earlier failed attempts. |
|  08-dhcp-lease.png | DHCP lease output, only if DHCP is configured and required | Client lease details and, where useful, the router's DHCP binding. Do not claim DHCP is working without this observation. |

The project documents identify DHCP, dedicated inter-VLAN evidence, and a final routing-table capture as outstanding. The technical report also flags a VLAN 99 NAT-inside discrepancy that must be checked against R1's actual configuration before submission.
