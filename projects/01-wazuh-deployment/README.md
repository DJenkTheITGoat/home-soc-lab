# Project 1: Wazuh SIEM Deployment

## Overview
Stood up a Wazuh 4.9.2 all-in-one deployment on Ubuntu 26.04 as the foundation of my home SOC lab. This deployment includes the Wazuh Manager, Indexer, and Dashboard running on a single VM.

## Architecture
- **Host:** Alienware desktop (Windows 11, 16GB RAM, 24 logical processors)
- **Hypervisor:** Oracle VirtualBox 7.x
- **VM:** Ubuntu 26.04 LTS, 6GB RAM, 3 vCPU, 50GB disk
- **Network:** NAT adapter (default)
- **Wazuh version:** 4.9.2

## Steps Taken
1. Installed VirtualBox on the Windows host and confirmed CPU virtualization (VT-x) was enabled in BIOS.
2. Created a new VM and installed Ubuntu 26.04 from ISO.
3. Installed `curl` via `apt`, which was missing from the minimal Ubuntu install.
4. Downloaded the Wazuh all-in-one installer:
5. Hit a hardware requirements error on first run — the script flagged the VM as below minimum specs. Powered the VM off, increased RAM from 4GB to 6GB and CPU cores from 2 to 3 in VirtualBox settings.
6. Re-ran the installer:
7. Installer completed in ~18 minutes. Captured the admin credentials from the final summary.
8. Logged into the dashboard at `https://localhost` via Firefox inside the VM, accepted the self-signed cert, and confirmed all modules load.

## Validation
Verified all three Wazuh services are active and running via systemd:
- `wazuh-manager.service` — active (running)
- `wazuh-indexer.service` — active (running)
- `wazuh-dashboard.service` — active (running)

Dashboard reachable at `https://localhost:443` with admin credentials.

## Troubleshooting Notes
- **curl not installed by default:** Ubuntu 26.04 minimal ships without curl. Resolved with `sudo apt install curl -y`.
- **Hardware minimum error:** Wazuh installer enforces 4GB RAM / 2 CPU. Linux reports slightly less than allocated, so the check failed at 4GB. Bumping to 6GB and 3 CPU resolved it and gave better performance.
- **Shutdown inhibited by GNOME session:** `sudo shutdown now` was blocked by an active user session. Used `sudo systemctl poweroff -i` to force a clean shutdown.

## Skills Demonstrated
- Linux server administration (Ubuntu, apt, systemd)
- SIEM deployment (Wazuh Manager, Indexer, Dashboard architecture)
- VirtualBox VM provisioning and hardware allocation
- Troubleshooting installation errors against vendor documentation
- Self-signed TLS handling

## Screenshots
See [`/screenshots`](./screenshots/) for visual evidence of the deployment.

## Next Steps
Project 2: Deploy a Wazuh agent to a Windows endpoint and validate log ingestion.
