# windows-wazuh-detection-lab-
# Windows Detection & Incident Response Lab

A personal cybersecurity lab built to develop practical skills in security monitoring, detection engineering, incident investigation, and DFIR.

The lab is built around a small Active Directory environment with Windows telemetry collected through Sysmon and Wazuh. The environment will progressively be expanded with MITRE ATT&CK simulations, custom detections, network monitoring, endpoint hunting, and Microsoft security tooling.

## Current Status

🟢 **Core telemetry pipeline operational**

- Proxmox VE — operational
- Windows Server 2022 / `DC01` — operational
- Windows 11 / `WIN11-CL01` — operational
- Wazuh Manager & Dashboard — operational
- Wazuh agents — connected
- Sysmon — installed
- Sysmon telemetry — confirmed in Wazuh
- Windows Security telemetry — confirmed in Wazuh

### Evidence

Both Windows endpoints are actively connected to Wazuh.
<img width="2505" height="644" alt="wazuh-agents-connected" src="https://github.com/user-attachments/assets/5003a32c-e8eb-463a-90cb-dec424afce40" />


A Sysmon Event ID 1 (Process Create) event generated on `WIN11-CL01` was successfully received by Wazuh.

<img width="2506" height="1216" alt="wazuh-sysmon-event-id-1" src="https://github.com/user-attachments/assets/654b1727-2f05-4f11-b835-a2fb240bc61e" />


Detailed validation and supporting evidence can be found in [Pipeline Validation](validation/03-pipeline-validation.md).

## Architecture
                    ┌─────────────────────┐
                    │      Proxmox        │
                    │   Dell Latitude     │
                    │       5490          │
                    └──────────┬──────────┘
                               │
             ┌─────────────────┼─────────────────┐
             │                 │                 │
             ▼                 ▼                 ▼
       ┌───────────┐     ┌─────────────┐   ┌─────────────┐
       │   DC01    │     │ WIN11-CL01  │   │   WAZUH01   │
       │ Windows   │     │ Windows 11  │   │   Debian    │
       │ Server    │     │ Sysmon      │   │   Wazuh     │
       │ AD DS     │     │             │   │   Manager   │
       └─────┬─────┘     └──────┬──────┘   │  Dashboard  │
             │                  │          └──────┬──────┘
             │                  │                 │
             └───────────  Wazuh Agents ──────────┘

## Telemetry Pipeline

The current telemetry flow is:

Windows Activity<br>
       ↓<br>
Windows Event Logs / Sysmon<br>
       ↓<br>
Wazuh Agent<br>
       ↓<br>
Wazuh Manager<br>
       ↓<br>
Wazuh Dashboard<br>
       ↓<br>
Detection & Investigation<br>

The pipeline has been validated using a controlled `ipconfig /all`
execution. Sysmon Event ID 1 was generated on `WIN11-CL01` and
successfully received by Wazuh.

See [Pipeline Validation](validation/03-pipeline-validation.md) for
the detailed test and supporting evidence.
               `    
