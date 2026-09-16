# Splunk SIEM Log Analysis Lab — TechPay Solutions

## Project Overview
This project simulates a SOC analyst investigation using 
Splunk Enterprise to analyze security logs for a fictional 
fintech company — TechPay Solutions S.L. It covers data 
ingestion, SPL threat detection queries, incident analysis 
and GDPR breach assessment.

## What This Project Covers
- Security log ingestion and parsing in Splunk
- 5 SPL detection queries for real threat scenarios
- Identification of 3 critical security incidents
- MITRE ATT&CK framework mapping
- GDPR Art. 33 breach notification assessment
- SOC analyst incident investigation workflow

## Threats Detected
| Threat | Source | Severity | MITRE |
|---|---|---|---|
| Brute Force | Russia, China, Ukraine | High | T1110 |
| Account Takeover + Exfiltration | China (ana.martinez) | Critical | T1078, T1530 |
| Account Takeover + Exfiltration | Russia (maria.garcia) | Critical | T1078, T1530 |
| After-hours access | Multiple | Medium | T1078 |

## SPL Queries
| Query | File | Purpose |
|---|---|---|
| Brute Force Detection | brute-force-detection.spl | Detect failed login patterns |
| Unusual Country Login | unusual-country-login.spl | Detect geographic anomalies |
| Data Exfiltration | data-exfiltration.spl | Detect unauthorized exports |
| Privilege Change | privilege-change.spl | Detect role assignments |
| Event Summary | event-summary.spl | Executive overview |

## Key Finding — GDPR Breach
Two data exfiltration incidents triggered GDPR Art. 33 
breach notification obligations:
- Customer database exported from China
- Compliance reports exported from Russia
- AEPD notification deadline: 72 hours from detection

## Tools & Technologies
- Splunk Enterprise (local installation)
- SPL (Search Processing Language)
- CSV log ingestion
- Splunk Dashboard

## GDPR Compliance Connection
| Article | Splunk Function |
|---|---|
| Art. 32 — Security | Continuous log monitoring |
| Art. 33 — Breach notification | Incident detection enables 72h response |
| Art. 5(1)(f) — Integrity | Audit trail of all data access |

## Related Projects
- [Microsoft Sentinel Lab](https://github.com/Andrea1864/siem-microsoft-sentinel)
- [TechPay GDPR ROPA](https://github.com/Andrea1864/gdpr-ropa-fintech)
- [Azure Policy Lab](https://github.com/Andrea1864/azure-policy-defender-cloud)

## Author
Andrea Castillo — Law Graduate | Cybersecurity & GRC Specialist  
