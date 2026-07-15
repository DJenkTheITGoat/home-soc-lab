# Home SOC Lab

A self-hosted security operations lab I built to practice detection engineering, log analysis, and incident response while pursuing my Cybersecurity degree and CompTIA Security+.

> **Why this repo exists:** I'm an early-career cybersecurity student building practical SOC analyst skills. This lab is where I generate attacks, watch them fire alerts, and learn to investigate them — the same workflow a Tier 1 analyst does daily.

---

## 🎯 Goals

- Build a working SIEM/EDR pipeline from scratch
- Generate and detect common attack techniques (mapped to MITRE ATT&CK)
- Practice the full alert → triage → investigation → writeup loop
- Document every project so the learning sticks

---

## 🖥️ Lab Environment

| Component | Role | Specs |
|---|---|---|
| Host machine | Hypervisor | Alienware desktop, 16GB RAM, 24 logical processors |
| Hypervisor | VM platform | Oracle VirtualBox 7.x |
| Wazuh Manager | SIEM + XDR server | Ubuntu 26.04, 6GB RAM, 3 vCPU, 50GB disk |
| Windows 10 Endpoint | Victim host | Active ✅|
| Kali Linux | Attacker box | Planned |

---

## 📂 Projects

### ✅ Project 1: Wazuh SIEM Deployment
**Status:** Complete
**What I did:** Stood up a Wazuh 4.9.2 all-in-one deployment on Ubuntu 26.04, including the Wazuh Manager, Indexer, and Dashboard. Verified all services are active and the web UI is accessible.
**Skills demonstrated:** Linux server administration, SIEM deployment, service management with systemd, self-signed TLS, troubleshooting installation errors
**Writeup:** [`/projects/01-wazuh-deployment/`](./projects/01-wazuh-deployment/)

 ### ✅  Project 2: Wazuh Agent Deployment (Windows Endpoint)
**Status:** Complete 
**What I did:** Deployed a Wazuh agent to a Windows 10 endpoint, configured agent-to-manager communication, validated log ingestion, and analyzed CIS benchmark results. 
**Writeup:** [/projects/02-agent-deployment/](projects/02-agent-deployment/)

### ✅  Project 3: Detecting Common Attacks

**Status:** Complete **What I did:** Simulated brute-force login attempts using `net use` on a Windows 10 endpoint and ran an nmap SYN scan from the Wazuh Server. Captured alerts in Wazuh Threat Hunting, identified Windows Logon Failure events (rule 60122), and mapped detected activity to MITRE ATT&CK techniques including T1078 (Valid Accounts). **Skills demonstrated:** Attack simulation, log analysis, MITRE ATT&CK mapping, Wazuh alert triage. **Writeup:** [projects/03-attack-simulation](projects/03-attack-simulation)

✅  Project 4: Active Directory Lab & Kerberoasting

**Status:** Complete **What I did:** Built a Windows Server 2022 Domain Controller from scratch, configured the jenkslab.local domain (NetBIOS: JENKSLAB), created domain user accounts, and simulated a Kerberoasting attack by registering an SPN (HTTP/jenkslab.local) on the jsmith account and requesting an RC4-HMAC Kerberos service ticket. Mapped the attack to MITRE ATT&CK T1558.003. **Skills demonstrated:** Active Directory administration, domain controller setup, Kerberos authentication, offensive security simulation, MITRE ATT&CK mapping. **Writeup:** [projects/04-active-directory](projects/04-active-directory)

---

## 🧠 Skills Built

- **SIEM:** Wazuh 4.9.2
- **OS:** Ubuntu 26.04, Linux CLI fundamentals
- **Virtualization:** VirtualBox VM creation, hardware allocation, networking
- **Service management:** systemd, journalctl
- **Documentation:** Markdown, GitHub workflow

---

## 📚 In Parallel

- **Studying:** CompTIA Security+ (SY0-701)
- **Practicing:** TryHackMe SOC Level 1 path (planned), LetsDefend investigations (planned)
- **Degree:** Cybersecurity, in progress

---

*Last updated: May 2026. This is a living lab — projects get added as I build them.*
