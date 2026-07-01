# Project 3 — Attack Simulation & Detection with Wazuh

## Objective

Simulate real-world attack techniques on a Windows 10 endpoint, capture the resulting alerts in Wazuh, and map detected activity to the MITRE ATT&CK framework. Document findings for SOC analyst portfolio evidence.

---

## Lab Environment

| Component | Details |
|---|---|
| SIEM / Detection Platform | Wazuh 4.x |
| Wazuh Server IP | 192.168.1.48 |
| Windows 10 Endpoint IP | 192.168.1.65 |
| Wazuh Agent Service | WazuhSvc |
| Host Machine | Alienware Desktop — Windows 11, VirtualBox |

---

## Attacks Simulated

### 1. Brute Force / Failed Login Attempts
- **Method:** Ran repeated `net use` commands against localhost with intentionally wrong credentials
- **Command used:**
```cmd
net use \\localhost\IPC$ wrongpassword123 /user:Administrator
```
- **Goal:** Generate Windows Event ID 4625 (Logon Failure) to trigger authentication failure alerts in Wazuh

---

### 2. Network Reconnaissance (Port Scan)
- **Method:** Ran an nmap SYN scan from the Wazuh Server against the Windows 10 Endpoint
- **Command used:**
```bash
sudo nmap -sS 192.168.1.65
```
- **Goal:** Simulate external recon activity and test whether Wazuh captures network scanning behavior

---

## Wazuh Alerts Captured

| Rule ID | Description |
|---|---|
| 60104 | Windows Audit Failure Event |
| 60105 | Windows Logon Failure |

**Last 24 Hours Summary:**
- Total Alerts: 119+
- Authentication Failures: 3 (confirmed Event ID 4625)
- Medium Severity Alerts: 142
- Low Severity Alerts: 324

---

## MITRE ATT&CK Mapping

| Technique | Technique ID | Tactic | Alert Count | Source |
|---|---|---|---|---|
| Valid Accounts | T1078 | Defense Evasion, Persistence, Privilege Escalation, Initial Access | 36 | Failed login simulation |
| Domain Policy Modification | T1484 | Defense Evasion, Privilege Escalation | 1 | Windows policy event |
| Sudo and Sudo Caching | T1548.003 | Privilege Escalation, Defense Evasion | 1 | Wazuh Server activity |

---

## Screenshots

> Add screenshots to a `/screenshots` folder in this repo and reference them below.

| Screenshot | Description |
|---|---|
| `screenshots/agent-active.png` | Wazuh dashboard showing Win10-Endpoint Active (1) |
| `screenshots/threat-hunting-dashboard.png` | Threat Hunting dashboard with alert counts |
| `screenshots/mitre-tactics.png` | Top 10 MITRE ATT&CKs panel showing Valid Accounts (36) |
| `screenshots/nmap-scan.png` | nmap -sS scan output from Wazuh Server terminal |
| `screenshots/failed-logins-cmd.png` | net use command generating failed login attempts |

---

## Key Takeaways

- Wazuh successfully detected brute force login attempts via Windows Event ID 4625 and mapped them to **T1078 (Valid Accounts)**
- nmap recon scan confirmed the endpoint was reachable and generated network-level activity visible in Wazuh
- Windows Firewall filtered all 1000 ports during the SYN scan — realistic behavior in a hardened environment
- MITRE ATT&CK integration in Wazuh automatically categorized detected techniques without manual tagging

---

## Tools Used

- Wazuh SIEM (open source)
- nmap 7.98
- Windows Command Prompt (`net use`)
- VirtualBox (bridged networking)
- MITRE ATT&CK Framework

---

## Status

- [x] Agent confirmed Active in Wazuh dashboard
- [x] Failed login attacks simulated and detected
- [x] nmap recon scan executed
- [x] Alerts captured in Threat Hunting
- [x] MITRE ATT&CK techniques mapped
- [ ] Screenshots uploaded to `/screenshots`
- [ ] README pushed to GitHub
