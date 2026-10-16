# INSET Video Demonstration Script — Stats SA Mafikeng Network

**Target length:** about 17 minutes (within the requested 15–20 minute window)  
**Presenter:** Kudzai Mudzingwa  
**Project:** CMPG 325 — Stats SA Mafikeng Field Office Network  
**Use with:** StatsSA-Mafikeng-Network.pkt in Cisco Packet Tracer 9.x

## Before recording

- Open the saved Packet Tracer file and confirm it loads. Save a backup copy first.
- Arrange the Packet Tracer window so device labels and links are readable. Close unrelated windows and notifications.
- Prepare the PC-Admin, PC-Guest, and PC-CCTV test endpoints; the external server is 203.0.113.10.
- If you rerun tests, record the actual result on screen. Do not narrate an expected outcome as if it happened.
- The project notes say DHCP, a dedicated inter-VLAN evidence capture, and a final routing-table screenshot are outstanding. Do not claim these were verified unless you capture them now.
- Confirm whether VLAN 99 is configured as NAT-inside. The written addressing plan and general NAT wording are not fully consistent on that detail.
- Hide or replace any reusable lab credentials before recording. Do not show passwords in the video.

## Timed script

### 0:00–0:55 — Opening and project identification

**On screen:** Show the project title, then the Packet Tracer workspace with the complete topology visible.

**Say:**

“Hello, my name is Kudzai Mudzingwa, and this is my CMPG 325 Computer Networks demonstration. I will present a simulated network for the Stats SA Mafikeng Field Office in Mahikeng. I will explain the design, show how the departments and restricted devices are separated, and walk through the recorded connectivity and security checks.

“This is a Cisco Packet Tracer simulation, not a live Stats SA production network. I will distinguish what the project records as tested from items that still need evidence. The main design goal is to give the office separate network zones, maintain controlled communication, and provide manageable infrastructure without treating Guest or CCTV devices as trusted business endpoints.”

### 0:55–2:15 — Requirements and scenario

**On screen:** Point to the six user/security endpoints and the three network devices. Briefly show the repository’s client-requirements document if available in another window.

**Say:**

“The scenario represents a small field office with Administration, Field, Finance, and Human Resources users, together with Guest access and CCTV devices. Network infrastructure has its own management segment. This separation is useful because each group has a different purpose and does not need identical access to every other group.

“The project requirements focus on four outcomes. First, separate these functions into VLANs. Second, route traffic through a controlled Layer 3 device. Third, restrict Guest and CCTV traffic from protected internal networks while allowing the project’s permitted external test path. Fourth, manage the switches through a dedicated management network and use SSH for remote administration.

“The implementation also records address planning and verification evidence. I will show the recorded results and identify the checks that still need to be captured, rather than overstate what was tested.”

### 2:15–3:40 — Topology walkthrough

**On screen:** Trace the topology from the External-Test-Server to R1, then to SW1-Core, then to SW2-Access and SW3-Access. Zoom in enough to show labels and active links.

**Say:**

“Starting on the external side, this Packet Tracer server is the deterministic test destination at 203.0.113.10. R1 is a Cisco 2911. It is the central routing and policy point, and it provides the simulated edge connection. SW1-Core is the aggregation switch. It connects the two access switches, SW2-Access and SW3-Access.

“SW2 serves the Administration, Field, and Finance representative PCs. SW3 serves Human Resources, Guest, and CCTV. The endpoint links are access links, while the switch uplinks and the router-to-core connection carry the VLAN traffic over trunks. The router’s internal trunk is documented on GigabitEthernet zero slash one; its external interface is GigabitEthernet zero slash zero.

“This layout is intentionally compact for a lab. A real site would need rack, cabling, power, redundancy, and capacity details that Packet Tracer does not establish here.”

### 3:40–5:10 — VLAN and addressing plan

**On screen:** Show the addressing plan document or a readable table. Return to Packet Tracer and point out the departmental endpoints.

**Say:**

“The design uses seven VLANs. VLAN 10 is Administration, VLAN 20 is Field, VLAN 30 is Finance, VLAN 40 is Human Resources, VLAN 50 is Guest, VLAN 60 is CCTV, and VLAN 99 is infrastructure management. Each documented internal VLAN has a separate slash-24 network and a gateway ending in dot one.

“For example, Administration uses 192.168.10.0 slash 24, with gateway 192.168.10.1. Guest uses 192.168.50.0 slash 24, with gateway 192.168.50.1. CCTV uses 192.168.60.0 slash 24, and its gateway is 192.168.60.1. Management uses 192.168.99.0 slash 24. The switches use management addresses 192.168.99.2, .3, and .4.

“The external test segment is 203.0.113.0 slash 24, with R1 at 203.0.113.1 and the server at 203.0.113.10. This address range is used as a simulation and documentation test network, not as proof of an Internet connection.”

### 5:10–6:35 — Switching and trunks

**On screen:** Select SW1-Core, SW2-Access, and SW3-Access. If the CLI is available, show VLAN membership and trunk state. Suggested checks: show vlan brief and show interfaces trunk.

**Say:**

“The access switches assign each endpoint port to its functional VLAN. The uplinks aggregate multiple VLANs between the access layer and SW1-Core, and the link from SW1-Core to R1 carries the VLANs needed for router-on-a-stick routing.

“When I show the switch command output, I am looking for two things: the VLANs exist and the endpoint-facing ports are assigned to the intended VLANs; and the uplinks are operating as trunks. If a result is missing or differs from the design, I will pause and correct the project before claiming it passed. The documentation records the endpoint port mapping: Fa0/2 through Fa0/4 on SW2 for Admin, Field, and Finance, and the same access-port range on SW3 for HR, Guest, and CCTV.”

### 6:35–8:05 — Router-on-a-stick routing

**On screen:** Select R1. Show the interface summary and relevant subinterfaces if visible. Suggested checks: show ip interface brief and show ip route. Do not expose credentials.

**Say:**

“R1 uses one physical internal connection with 802.1Q subinterfaces for the VLAN gateways. That design is called router-on-a-stick. The switch forwards tagged VLAN traffic to R1, and the router uses the subinterface for the matching VLAN to route traffic according to the configured policy.

“The project documentation lists gateways for VLANs 10, 20, 30, 40, 50, 60, and 99. The route table should include the connected VLAN networks when the relevant interfaces are up. I am showing the current Packet Tracer state here, rather than relying only on the design document.

“One evidence item still noted as outstanding is a final routing-table capture. If I capture it during this recording, I will save the screenshot and add it to the evidence register. A topology diagram alone is not enough to prove that the routing table was correct at test time.”

### 8:05–9:25 — Guest and CCTV security policy

**On screen:** Show the ACL configuration and counters on R1, if available. Suggested check: show access-lists. Avoid exposing passwords or unrelated configuration.

**Say:**

“Guest and CCTV are treated as restricted zones. The documented GUEST-ISOLATION ACL is intended to prevent Guest VLAN 50 from initiating traffic to protected internal and management networks while allowing the permitted external path. The CCTV-ISOLATION ACL applies a similar policy to VLAN 60.

“The recorded behavioral checks are specific: PC-Guest and PC-CCTV could reach their own gateways and the external test server, but could not reach the Admin endpoint at 192.168.10.21. The ACL permit and deny counters also increased during testing. These observations support the tested paths. They do not, by themselves, prove every protocol or every internal destination was tested. I will keep that distinction clear in the report and evidence register.”

### 9:25–10:35 — NAT and external test path

**On screen:** Show R1 NAT configuration and statistics. Suggested checks: show ip nat translations and show ip nat statistics. Confirm whether VLAN 99 is NAT-inside before discussing that interface.

**Say:**

“R1 provides the project’s simulated edge translation. The documentation identifies GigabitEthernet zero slash zero as outside and records dynamic translations after internal traffic reached the external test server. The reported result was four dynamic translations and 12 hits. The Guest and CCTV PCs each recorded four replies from 203.0.113.10.

“There is one documentation detail I am checking: the IP plan lists VLAN subinterfaces .10 through .60 as NAT-inside, while other wording refers more generally to the internal VLAN interfaces. I will verify whether management VLAN 99 is included in the actual configuration and make the documents match. I will not claim that management traffic is translated unless the configuration and test show it.”

### 10:35–11:40 — Management plane and SSH

**On screen:** Show VLAN 99 switch management addresses and the recorded PC-Admin SSH session to SW1-Core. If rerunning SSH, keep the password hidden.

**Say:**

“VLAN 99 separates switch management from user endpoint networks. The documented switch addresses are 192.168.99.2 for SW1-Core, .3 for SW2-Access, and .4 for SW3-Access. The recorded test from PC-Admin reached all three management addresses. The project also records a successful SSH session from PC-Admin to SW1-Core.

“SSH is preferable to Telnet for remote device administration because it provides an encrypted management session. The evidence specifically records SSH to SW1-Core. Unless I show a separate successful session to the other access switches, I will not claim that their SSH access was independently tested.”

### 11:40–14:20 — Connectivity and policy test demonstration

**On screen:** If conducting live tests, open the PC command prompts in turn. Show the source device and destination as you test. Use the saved results as a reference, but narrate the on-screen result. Suggested pings: Guest to 192.168.50.1, Guest to 192.168.10.21, Guest to 203.0.113.10; then CCTV to 192.168.60.1, CCTV to 192.168.10.21, CCTV to 203.0.113.10. If short on time, show the recorded evidence and say it is previously recorded rather than live.

**Say:**

“I am testing the Guest endpoint first. The expected and previously recorded result to the Guest gateway, 192.168.50.1, is four replies. The test to the Admin endpoint, 192.168.10.21, should be denied by the Guest policy; the recorded test showed 100 percent loss. The external test server at 203.0.113.10 should remain reachable; the recorded result was four replies.

“Now I am using the same pattern for CCTV. The recorded result to the CCTV gateway, 192.168.60.1, was four replies. Access from CCTV to the Admin endpoint was blocked, with 100 percent loss. The external test server remained reachable, again with four replies.

“As I demonstrate, I will allow the result to finish and leave it visible long enough to read. If a result differs from the record, I will state what happened, save the actual output, and investigate it. I will not silently edit the result or present an expected response as an observed one.”

### 14:20–15:35 — Evidence and remaining checks

**On screen:** Show the testing-evidence.md table and repository evidence folder. Show the two screenshot files only after checking what each depicts.

**Say:**

“The repository contains the Packet Tracer file, design and addressing documents, a test register, and two screenshots. The screenshot filenames are generic, so before final submission I will confirm what each image shows, rename them descriptively, and link them from the evidence register.

“The project notes three evidence items as outstanding: DHCP verification, a dedicated inter-VLAN evidence capture, and a final routing-table screenshot. I will either capture these before submission or label them as not captured. I will not describe DHCP as working solely because the addressing plan says endpoints are DHCP-capable. Likewise, the router-on-a-stick design is documented, but a dedicated inter-VLAN test result still needs to be shown.”

### 15:35–16:35 — Limitations and practical meaning

**On screen:** Show the report’s limitations section, then return to the topology.

**Say:**

“This project demonstrates core networking concepts in a controlled simulator: VLAN segmentation, routed VLAN gateways, traffic policy, address translation, and a management network. It does not establish that a production deployment is ready. A real site would still need approved IP addressing, capacity and availability planning, production firewall policy, centralized authentication and logging, configuration backups, physical cabling records, and operational change control.

“The test server is a deterministic lab endpoint, not a public Internet service. The results are useful for the project’s defined paths, but they should not be generalized beyond what was actually tested.”

### 16:35–17:30 — Conclusion

**On screen:** Show the full topology one final time. Leave the project name and complete network visible for the closing.

**Say:**

“To conclude, the Stats SA Mafikeng field-office simulation separates seven network functions across dedicated VLANs and uses R1 for inter-VLAN routing, access-control enforcement, and simulated NAT/PAT. The recorded tests show management reachability, an SSH session to SW1-Core, Guest and CCTV gateway and external connectivity, blocked Guest/CCTV access to the Admin endpoint, and NAT and ACL counters.

“The final improvements are to reconcile the VLAN 99 NAT documentation, capture the outstanding DHCP, inter-VLAN, and routing-table evidence where applicable, and label the screenshots clearly. Thank you for watching my CMPG 325 network demonstration.”

## Optional evidence capture checklist

- Show VLAN membership and trunk state on the switches.
- Show R1 interface status and the final route table.
- Confirm the actual NAT inside/outside interfaces, especially whether VLAN 99 is included.
- Capture the Guest and CCTV gateway, Admin-denial, and external-server tests with the source endpoint visible.
- Capture NAT translations/statistics and ACL counters after generating test traffic.
- Capture DHCP only if configured and successfully tested; show the lease details.
- Save each screenshot with a descriptive filename and add it to evidence/README.md or testing-evidence.md.
- Keep raw credentials out of screenshots and the public recording.
