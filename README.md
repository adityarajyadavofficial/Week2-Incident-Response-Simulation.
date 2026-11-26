# Virtual Security Incident Response Simulation

**Week 2 Task – Cybersecurity Internship (YuvaIntern)**
**Author:** Aditya Raj

## Overview
This project simulates a full security incident response in an isolated virtual lab. A Linux web server (Metasploitable 2 + DVWA) is breached by a simulated attacker, and the incident is handled end-to-end using the **NIST SP 800-61** incident response lifecycle. The project includes a complete Incident Response Plan and a Post-Incident Analysis Report.

**Incident ID:** INC-2026-001 (simulated) | **Severity:** Critical

## 📄 Report
- [View report (PDF)](Week2_Incident_Response_Report_Aditya_Raj.pdf) – opens directly in the browser
- [Download report (DOCX)](Week2_Incident_Response_Report_Aditya_Raj.docx)

## Lab Environment
| System | IP | Role |
|---|---|---|
| Attacker (Kali Linux) | 192.168.56.110 | Simulated threat actor |
| SRV-WEB01 (Metasploitable 2) | 192.168.56.102 | Compromised web server |
| SIEM (Wazuh + rsyslog) | 192.168.56.105 | Log collection and alerting |
| IR Workstation | 192.168.56.120 | Analysis and forensics |

![Environment and Attack Path](images/fig1.png)

## Incident Summary
The attacker scanned the server, exploited **SQL injection** to steal credentials, reused a password to log in via **SSH**, uploaded a **PHP web shell**, escalated to **root** through unrestricted sudo, added persistence (hidden UID-0 user + cron reverse shell) and **exfiltrated a 48 MB database dump**. A Wazuh alert detected the breach the next morning.

![Incident Timeline](images/fig3.png)

## Frameworks Used
- **NIST SP 800-61** – Incident response lifecycle
- **SANS PICERL** – Practical response checklist
- **MITRE ATT&CK** – Mapping of 10 attacker techniques
- **NIST CSF 2.0** – Proposed security framework improvements

![NIST IR Lifecycle](images/fig2.png)

## Response Phases
| Phase | Key actions |
|---|---|
| Detection & Analysis | Alert triage, log analysis, IOC extraction, ATT&CK mapping, scope determination |
| Containment | Network isolation, attacker IP blocked, VM snapshot and disk image with SHA-256 hashes |
| Eradication | Web shell, backdoor user and cron job removed; root causes fixed |
| Recovery | Rebuilt from clean image, verified backup restored, re-scan, 72-hour monitoring |
| Post-Incident | Root cause analysis, 12 security gaps, lessons learned, recommendations |

## Response Metrics
| Metric | Time |
|---|---|
| Time to Detect | 6.4 hours |
| Time to Contain | 25 minutes |
| Time to Eradicate | 4.4 hours |
| Time to Recover | 9.3 hours |

![Response Metrics](images/fig4.png)

## Key Recommendations
1. Fix SQL injection with prepared statements and deploy a WAF
2. Enforce strong unique passwords, MFA and SSH key-based login
3. Remove unrestricted sudo rights (least privilege)
4. Default-deny egress firewall rules
5. Real-time web log monitoring and file-integrity monitoring
6. Formal IR plan with regular tabletop exercises and tested backups

![Security Gaps](images/fig5.png)

## Repository Structure
```
├── README.md
├── Week2_Incident_Response_Report_Aditya_Raj.pdf
├── Week2_Incident_Response_Report_Aditya_Raj.docx
└── images/   (diagrams and charts)
```

## Disclaimer
This is a training exercise performed only on intentionally vulnerable virtual machines in an isolated network. All data used is synthetic.
