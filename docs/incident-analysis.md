# Incident Analysis Report — TechPay Solutions
## Date: August 10, 2026

## Executive Summary
Splunk SIEM analysis of TechPay security logs identified 
3 critical security incidents requiring immediate investigation:
1. Brute force attacks from Russia and China
2. Suspected account takeover — ana.martinez (China)
3. Suspected account takeover — maria.garcia (Russia)

---

## Incident 1 — Brute Force Attacks

### Detection Query
```spl
source="techpay-security-logs.csv" status="failed"
| stats count by source_ip, country
| where count > 3
```

### Findings
| Source IP | Country | Failed Attempts |
|---|---|---|
| 45.33.32.156 | Russia (RU) | 6 |
| 103.21.244.0 | China (CN) | 5 |
| 91.108.4.0 | Ukraine (UA) | 3 |

### Analysis
Three separate IPs launched coordinated login attempts 
against the TechPay portal between 09:12 and 15:30. 
The pattern is consistent with credential stuffing or 
brute force attacks targeting employee accounts.

### MITRE ATT&CK
- **Tactic**: Credential Access
- **Technique**: T1110 — Brute Force

### Recommended Actions
- Block IPs: 45.33.32.156, 103.21.244.0, 91.108.4.0
- Enable account lockout after 5 failed attempts
- Enforce MFA for all accounts immediately

---

## Incident 2 — Account Takeover: ana.martinez

### Timeline
| Time | Event | Details |
|---|---|---|
| 02:33:15 | Login success | From China (185.220.101.45) |
| 02:33:45 | Data access | customer-database |
| 02:34:12 | Data access | customer-database |
| 02:34:55 | **Data export** | customer-database ⚠️ |

### Analysis
ana.martinez logged in from China at 02:33 AM — outside 
business hours and from an unusual country. The account 
immediately accessed and exported customer database data. 
This is consistent with an account takeover followed by 
data exfiltration.

### MITRE ATT&CK
- **Tactic**: Initial Access → Collection → Exfiltration
- **Technique**: T1078 Valid Accounts → T1530 Data from Cloud Storage

### GDPR Impact
- **Art. 33** — Personal data breach notification to AEPD 
  required within 72 hours
- **Art. 34** — Affected customers may need to be notified
- Data exported: customer database (PII + financial data)

### Recommended Actions
- Immediately disable ana.martinez account
- Investigate what data was exported
- Preserve logs as legal evidence
- Notify DPO — potential GDPR breach
- Assess AEPD notification requirement

---

## Incident 3 — Account Takeover: maria.garcia

### Timeline
| Time | Event | Details |
|---|---|---|
| 23:15:22 | Login success | From Russia (77.88.55.66) |
| 23:16:00 | Data access | compliance-reports |
| 23:17:30 | **Data export** | compliance-reports ⚠️ |
| 23:18:00 | Data access | customer-database |

### Analysis
maria.garcia (Compliance Officer) logged in from Russia 
at 11:15 PM and exported compliance reports before 
accessing the customer database. This is highly suspicious 
given the geographic anomaly and after-hours timing.

### MITRE ATT&CK
- **Tactic**: Initial Access → Collection → Exfiltration
- **Technique**: T1078 Valid Accounts → T1530 Data from Cloud Storage

### GDPR Impact
- **Art. 33** — Compliance reports may contain personal data
- **Art. 9** — If health data included, stricter notification rules
- Potential insider threat or compromised credentials

### Recommended Actions
- Immediately disable maria.garcia account
- Review what compliance reports were exported
- Investigate if credentials were phished
- Notify DPO and CISO immediately
- Consider law enforcement notification

---

## Overall Risk Assessment

| Incident | Severity | GDPR Impact | Action Required |
|---|---|---|---|
| Brute Force RU/CN | High | None yet | Block IPs, enforce MFA |
| Account Takeover + Exfiltration (ana) | Critical | Art. 33 breach | Disable account, notify AEPD |
| Account Takeover + Exfiltration (maria) | Critical | Art. 33 breach | Disable account, notify AEPD |

## GDPR Breach Notification Timeline
```
Incident detected: August 10, 2026 at 23:18
        ↓
DPO notified: August 10, 2026 (immediately)
        ↓
Internal assessment: August 11, 2026 (24 hours)
        ↓
AEPD notification deadline: August 13, 2026 (72 hours)
        ↓
Affected individuals notified: TBD (if high risk)
```
