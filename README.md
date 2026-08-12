# windows-wazuh-detection-lab-
Windows Detection & Incident Response Lab

A personal cybersecurity lab built to develop practical skills in security monitoring, detection engineering, incident investigation and DFIR using a combination of open-source security tooling and Microsoft technologies.
The lab is intentionally built from the ground up to provide visibility into Windows endpoint and Active Directory activity and to allow controlled adversary simulations using MITRE ATT&CK techniques.

Current Status

🟢 Core telemetry pipeline operational

Proxmox VE — operational
Windows Server 2022 / DC01 — operational
Windows 11 / WIN11-CL01 — operational
Wazuh Manager & Dashboard — operational
Wazuh agents — connected
Sysmon — installed
Sysmon telemetry — confirmed in Wazuh
Windows Security telemetry — confirmed in Wazuh

### Evidence
Both Windows endpoints are actively connected to Wazuh:
<img width="2505" height="644" alt="wazuh-agents-connected" src="https://github.com/user-attachments/assets/4cda72e5-1838-4b9b-a126-7fa99b68a0ec" />

The telemetry pipeline has also been validated from the Windows endpoint through Sysmon and into Wazuh:
<img width="2506" height="1216" alt="wazuh-sysmon-event-id-1" src="https://github.com/user-attachments/assets/719ec592-e4b6-44db-8e16-0278deafbeca" />

Current Architecture:
            ┌─────────────────────┐ 
            │ Proxmox             │ 
            │ Dell Latitude 5490  │ 
            │                     │ 
            └──────────┬──────────┘ 
                       │ 
      ┌────────────────┼─────────────────┐ 
      │                │                 │ 
      ▼                ▼                 ▼ 
┌───────────┐   ┌─────────────┐ ┌─────────────┐ 
│ DC01      │   │ WIN11-CL01  │ │ WAZUH01     │ 
│ Windows   │   │ Windows 11  │ │ Debian      │ 
│ Server    │   │ Sysmon      │ │ Wazuh       │ 
│ AD DS     │   │             │ │ Manager     │ 
└─────┬─────┘   └──────┬──────┘ │ Dashboard   │ 
      │                │        └──────┬──────┘
      │                │               │ 
└─────┬─────┘    └─────┬─────┘   └─────┬─────┘
      └────────── Wazuh Agents ────────┘
<img width="470" height="364" alt="image" src="https://github.com/user-attachments/assets/b77d16ec-df9d-4c69-9e06-4f4f358d3d27" />

Objective
The initial objective is to build a functioning Windows security telemetry pipeline before introducing adversary simulation.
The intended pipeline is:

Windows Activity
      ↓
Windows Event Logs / Sysmon
      ↓
Wazuh Agent
      ↓
Wazuh Manager
      ↓
Wazuh Dashboard
      ↓
Detection & Investigation

The lab will progressively be expanded with:
MITRE ATT&CK adversary simulations
Custom Wazuh detection rules
Network telemetry
Suricata / Zeek
Velociraptor
DFIR investigations
Detection tuning and false-positive analysis
Microsoft security tooling where practical
Phase 1 — Core Infrastructure
Proxmox

Proxmox VE is running on a dedicated Dell Latitude 5490.

The host provides the virtualization layer for the Windows and security infrastructure.

Current resources
Resource	Specification
CPU	Intel Core i5-8250U
RAM	32 GB
Storage	1 TB SSD
Hypervisor	Proxmox VE
Phase 2 — Active Directory
DC01

DC01 runs Windows Server 2022 and provides the Active Directory environment for the lab.

Current functionality:
Active Directory Domain Services
Domain authentication
Windows 11 domain joining
Centralized Windows configuration
Phase 3 — Windows Endpoint
WIN11-CL01

WIN11-CL01 is the primary Windows endpoint used for security testing.

The endpoint currently has:
Wazuh Agent
Sysmon
Windows Security auditing
Domain membership

This machine will later be used for controlled MITRE ATT&CK simulations.

Phase 4 — Wazuh
WAZUH01

Wazuh Manager and Dashboard are running on a dedicated Debian VM.
Both Windows systems have successfully connected to the Wazuh Manager.

Agent status
Host	OS	Wazuh Agent	Status
DC01	Windows Server 2022	Yes	🟢 Connected
WIN11-CL01	Windows 11	Yes	🟢 Connected
Phase 5 — Sysmon Telemetry Validation

Sysmon has been installed on the Windows endpoints and configured to generate Windows telemetry relevant to security investigation.

The telemetry has been successfully confirmed in Wazuh.

Validation:
A controlled process execution was performed on the Windows endpoint.

Expected flow:
Process execution
      ↓
Sysmon
      ↓
Windows Event Log
      ↓
Wazuh Agent
      ↓
Wazuh Manager
      ↓
Wazuh Dashboard
Result

🟢 PASS — Sysmon telemetry is successfully reaching Wazuh.

This confirms that the basic endpoint telemetry pipeline is operational.

Evidence

Screenshots and relevant event examples are stored under:

/screenshots/telemetry/
Current Milestone
🟢 Pipeline Green

The initial infrastructure and telemetry pipeline has been successfully validated.

The lab can now:

Generate Windows activity.
Capture activity through Sysmon and Windows Security Logs.
Forward the telemetry through the Wazuh agents.
Ingest the telemetry into Wazuh.
Display and investigate the resulting events.

The next phase is to introduce controlled MITRE ATT&CK / Atomic Red Team activity and determine which events are generated, which are detected automatically, and where detection gaps exist.

Roadmap
Phase 1 — Infrastructure

🟢 Proxmox
🟢 Active Directory
🟢 Windows endpoint
🟢 Wazuh
🟢 Sysmon telemetry

Phase 2 — Detection Engineering

⬜ Atomic Red Team
⬜ Wazuh detection rules
⬜ MITRE ATT&CK mapping
⬜ False-positive analysis
⬜ Detection tuning

Phase 3 — Network Visibility

⬜ Suricata / Zeek
⬜ Network telemetry
⬜ Endpoint + network correlation

Phase 4 — DFIR

⬜ Velociraptor
⬜ Endpoint hunting
⬜ Evidence collection
⬜ Incident investigation

Phase 5 — Advanced Testing

⬜ Attack chains
⬜ Detection coverage analysis
⬜ Additional adversary emulation

Phase 6 — Microsoft Security Stack

⬜ KQL
⬜ Microsoft Sentinel
⬜ Defender integration
