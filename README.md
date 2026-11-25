# Sysmon Configuration (Schema v4.90)

A detection-engineered Sysmon configuration designed to capture high-fidelity Windows endpoint telemetry for threat hunting, incident response, and SIEM alerting while keeping host resource overhead low.

## Key Features
- **Modern Schema (`4.90`):** Supports Sysmon 15+ event types and rule-group logic.
- **MITRE ATT&CK Tagging:** Embeds technique IDs directly into `RuleName` fields for streamlined SIEM alerting and triage.
- **Expanded Telemetry:**
  - **Event ID 22 (`DnsQuery`):** Captures outbound DNS requests while filtering routine Microsoft/OS chatter.
  - **Event ID 25 (`ProcessTampering`):** Detects process hollowing and herpaderping.
  - **Event ID 26 (`FileDeleteDetected`):** Logs deletion of executables, scripts, and `.evtx` logs without disk-bloat archiving.
  - **Event ID 17/18 (`PipeEvent`):** Alerts on default Cobalt Strike, PsExec, and lateral movement named pipes.
- **LOLBin & Credential Access Coverage:** Monitors high-risk scripting engines, Living-off-the-Land binaries (`mshta`, `rundll32`, `regsvr32`, `certutil`, `bitsadmin`), LSASS process access (`ID 10`), and persistence registry keys (`ID 12–14`).
- **Dual Hashing & Low Overhead:** Captures `SHA256` and `IMPHASH` while disabling endpoint reverse-DNS lookups (`DnsLookup=False`) to minimize host network chatter.

## Quick Install
Run from an elevated PowerShell prompt:
```powershell
.\Sysmon64.exe -accepteula -i sysmonconfig-improved.xml
