# Scenario Overview — TechPay Solutions Splunk SIEM Lab

## Company Profile
- **Name**: TechPay Solutions S.L.
- **Sector**: Financial Technology (Fintech)
- **Employees**: 50
- **Location**: Barcelona, Spain
- **Services**: Digital payment processing, peer-to-peer 
  transfers, virtual card issuing

## SIEM Context
TechPay uses Splunk Enterprise as its SIEM solution to 
monitor and analyze security events across all systems. 
The SOC team uses SPL (Search Processing Language) to 
detect threats and investigate incidents in real time.

## Log Sources Analyzed
| Source | Data Type | Events |
|---|---|---|
| techpay-portal | Authentication logs | Login attempts |
| customer-database | Access logs | Data access and exports |
| payment-gateway | Transaction logs | Payment processing |
| entra-id | Identity logs | Privilege changes |
| compliance-reports | Access logs | Report access |

## Threat Scenarios Investigated
| Scenario | MITRE Tactic | Severity |
|---|---|---|
| Brute force from RU/CN/UA | Credential Access | High |
| Account takeover — ana.martinez | Initial Access | Critical |
| Data exfiltration — customer DB | Exfiltration | Critical |
| Account takeover — maria.garcia | Initial Access | Critical |
| Data exfiltration — compliance | Exfiltration | Critical |
| Privilege change — admin | Privilege Escalation | Medium |

## Regulatory Context
| Regulation | SIEM Relevance |
|---|---|
| GDPR Art. 32 | Security monitoring obligation |
| GDPR Art. 33 | Breach detection enables 72h notification |
| NIS2 Art. 21 | Incident detection and response |
| DORA Art. 17 | ICT-related incident reporting |
