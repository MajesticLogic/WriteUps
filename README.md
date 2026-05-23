# 📁 WriteUps

> Penetration test reports, CTF write-ups, and security research by **William Mackins**
>
> [![LinkedIn](https://img.shields.io/badge/LinkedIn-william--mackins-0A66C2?style=flat&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/william-mackins/)
> ![Platform](https://img.shields.io/badge/Platform-HackTheBox-9FEF00?style=flat&logo=hackthebox&logoColor=black)
> ![TLP](https://img.shields.io/badge/Classification-TLP%3ACLEAR-green?style=flat)

---

## 📖 About

This repository contains detailed penetration test reports and security research write-ups. Each report documents the full attack chain — from initial reconnaissance through to post-exploitation — along with risk-rated findings, evidence, and remediation guidance.

Reports follow a professional format aligned with industry standards (PTES) and include both a Markdown version for easy reading on GitHub and a formatted PDF for distribution.

---

## 📂 Write-Ups

| # | Target | Platform | Severity | Techniques | Report |
|---|--------|----------|----------|------------|--------|
| 01 | [MonitorsFour](#monitorsfour) | HackTheBox | 🔴 Critical | IDOR · RCE · Container Escape | [.md](./MonitorsFour_PenTest_Report.md) · [.pdf](./MonitorsFour_PenTest_Report.pdf) |

---

## MonitorsFour

**Platform:** HackTheBox &nbsp;|&nbsp; **Type:** Black-Box Penetration Test &nbsp;|&nbsp; **Rating:** 🔴 Critical

A three-stage attack chain achieving full Windows host compromise from an unauthenticated starting position.

### Attack Chain

```
[Unauthenticated]
      │
      ▼
  IDOR — /user?token=0
  Mass credential disclosure (MD5 hashes)
      │
      ▼
  CVE-2025-24367 — Cacti 1.2.28 RCE
  Authenticated → www-data shell (Docker container)
      │
      ▼
  CVE-2025-9074 — Docker Desktop Unauthenticated API
  Container escape → C:\ mount → root flag
```

### Findings Summary

| ID | Finding | Severity | CVSS |
|----|---------|----------|------|
| F-01 | IDOR in `/user` API Endpoint — Credential Disclosure | 🟠 High | 8.6 |
| F-02 | Cacti 1.2.28 Remote Code Execution (CVE-2025-24367) | 🔴 Critical | 9.8 |
| F-03 | Docker Desktop Unauthenticated API Access (CVE-2025-9074) | 🔴 Critical | 9.3 |

### Key Techniques
- Insecure Direct Object Reference (IDOR) / boundary-condition bypass
- Server-side command injection via Cacti Graph Template (CVE-2025-24367)
- Docker Engine API abuse for privileged container creation and host filesystem mount (CVE-2025-9074)
- MD5 hash cracking via rainbow table lookup

📄 [Read the full report →](./MonitorsFour_PenTest_Report.md)

---

## 🛠️ Tools Referenced

| Tool | Use |
|------|-----|
| [Nmap](https://nmap.org/) | Port & service scanning |
| [FFUF](https://github.com/ffuf/ffuf) | Virtual-host & directory fuzzing |
| [CrackStation](https://crackstation.net/) | Hash cracking |
| [CVE-2025-24367 PoC](https://github.com/TheCyberGeek/CVE-2025-24367-Cacti-PoC) | Cacti RCE exploit |
| curl / Netcat | Docker API interaction & reverse shells |

---

## 📜 Methodology

All assessments follow the [Penetration Testing Execution Standard (PTES)](http://www.pentest-standard.org/):

1. **Reconnaissance** — passive & active information gathering
2. **Enumeration** — service fingerprinting, subdomain & endpoint discovery
3. **Exploitation** — vulnerability exploitation using PoCs and manual techniques
4. **Post-Exploitation** — privilege escalation, lateral movement, persistence
5. **Reporting** — risk-rated findings with remediation guidance

---

## ⚠️ Disclaimer

All targets documented in this repository are either lab environments (HackTheBox, TryHackMe, etc.) or systems for which explicit written authorization was obtained prior to testing. This content is published for **educational purposes only**. Do not attempt to reproduce these techniques against systems you do not own or have permission to test.

---

## 📬 Contact

**William Mackins**
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-0A66C2?style=flat&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/william-mackins/)
