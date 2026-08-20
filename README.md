# 🛡️ Enterprise Network Simulation

Full implementation of Project Security's [E101: From Initial Access to 
Breached](https://projectsecurity.io/) — a self-hosted 
lab that simulates a small business network end-to-end: identity and 
domain services, workstations, a SIEM, and a guided attack/defense cycle 
against the environment once it's built.

---

## 🎯 What this project covers

The lab is built in three broad phases:

1. **🏗️ Build the network** — provision every VM, stand up Active Directory, 
   DNS, DHCP, a corporate server, and a SIEM (Wazuh) for monitoring.
2. **💥 Break it** — deliberately misconfigure part of the environment and 
   run a guided attack chain against it (phishing → credential theft → 
   lateral movement → domain compromise).
3. **📝 Document it** — write up what was built, what the attack looked like, 
   and what the corresponding detection/defense would be.

---

## 🌐 Network

- **Type:** Isolated NAT network, VirtualBox (`project-x-nat`)
- **Range:** `10.0.0.0/24`
- **Usable range:** `10.0.0.1 – 10.0.0.254`
- **DHCP dynamic scope:** `10.0.0.100 – 10.0.0.200`

---

## 🖥️ Hosts

| Host | IP | Role |
|---|---|---|
| project-x-dc | 10.0.0.5 | Domain Controller — AD, DNS, DHCP, SSO |
| project-x-admin (corp-svr) | 10.0.0.8 | Corporate Server |
| project-x-sec-box | 10.0.0.10 | Dedicated Security Server |
| project-x-sec-work | 10.0.0.103 / dynamic | Security Playground (Security Onion) |
| project-x-win-client | 10.0.0.100 / dynamic | Windows Workstation |
| project-x-linux-client | 10.0.0.101 / dynamic | Linux Desktop Workstation |
| attacker | dynamic | Attacker environment (Kali) |

---

## 💻 Virtual machines

| VM | OS | Specs | Storage |
|---|---|---|---|
| project-x-dc | Windows Server 2025 | 2 vCPU / 4096 MB | 50 GB |
| project-x-win-client | Windows 11 Enterprise | 2 vCPU / 4096 MB | 80 GB |
| project-x-linux-client | Ubuntu 22.04 Desktop | 1 vCPU / 2048 MB | 80 GB |
| project-x-sec-work | Security Onion | 1 vCPU / 2048 MB | 55 GB |
| project-x-sec-box | Ubuntu 22.04 Desktop | 2 vCPU / 4096 MB | 80 GB |
| project-x-corp-svr | Ubuntu Server 22.04 | 1 vCPU / 2048 MB | 25 GB |
| project-x-attacker | Kali Linux 2024.2 | 1 vCPU / 2048 MB | 55 GB |

Hypervisor: VirtualBox (alternative: VMware Workstation Pro).

---

## 🗺️ Build order

1. ⚙️ Provision VMs (hypervisor setup)
2. 🏢 AD Server — Windows Server 2025
3. 🖱️ Workstations — Windows 11, Ubuntu Desktop
4. 🗄️ Corporate Server — Ubuntu Server
5. 📧 Email Server — MailHog
6. 🧅 Security Onion workstation
7. 🔐 Security Server — Ubuntu Server
8. 📊 SIEM — Wazuh setup
9. 🎭 Configure a vulnerable environment
10. ⚔️ Run the cyber attack simulation

---

## 🧰 Tools

**Enterprise / defense**
- 🏢 Active Directory — identity, users, group policy
- 📊 Wazuh — SIEM: log analysis, intrusion detection, vulnerability detection
- 📧 MailHog — fake SMTP server for email testing

**Offense**
- 🐚 Evil-WinRM — remote Windows management / post-exploitation
- 🔨 Hydra — brute-force / credential attacks
- 📋 SecLists — wordlists for recon and exploitation
- 🌐 NetExec — lateral movement / remote execution
- 🖥️ XFreeRDP — remote desktop access for post-exploitation

---

## 🎓 Objective

Build a realistic (if small-scale) enterprise network, understand how its 
pieces depend on each other (AD, DNS, DHCP, SIEM), then attack it the way 
a real breach would unfold, and document both the attack and how it 
would've been caught or prevented.

---

## 📈 Progress

Currently connecting and provisioning workstations to the AD server.

| Phase | Status |
|---|---|
| Provision VMs | ✅ Done |
| AD Server (DC, DNS, DHCP) | ✅ Done |
| Windows 11 Workstation | 🟡 In progress |
| Ubuntu Desktop Workstation | 🟡 In progress |
| Corporate Server | ⬜ Not started |
| Email Server (MailHog) | ⬜ Not started |
| Security Onion | ⬜ Not started |
| Security Server | ⬜ Not started |
| SIEM (Wazuh) | ⬜ Not started |
| Vulnerable Environment Config | ⬜ Not started |
| Attack Simulation | ⬜ Not started |

**Writeups:** See [`/writeups`](writeups) for detailed entries as the build progresses.

---

## 📚 Reference

Course: [Project Security — E101](https://projectsecurity.io/)