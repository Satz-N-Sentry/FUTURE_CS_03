# FUTURE_CS_03 — API Security Risk Analysis

![Target](https://img.shields.io/badge/Target-OWASP%20crAPI-blue?style=flat-square)
![Domain](https://img.shields.io/badge/Domain-API%20Security-critical?style=flat-square)
![Tool](https://img.shields.io/badge/Tool-Postman-orange?style=flat-square&logo=postman)
![Framework](https://img.shields.io/badge/Framework-MITRE%20ATT%26CK-red?style=flat-square)

9 vulnerabilities across 4 OWASP API Top 10 categories — all mapped to CVE and MITRE ATT&CK.

## Author

**Satheesh Nithiananthan** (CyberLycan) — SAIZERO Ground Zero Defence 🐺

## Target

| Field | Details |
|---|---|
| App | OWASP crAPI |
| URL | `http://localhost:8888` |
| Auth | JWT Bearer (RS256) |
| Scope | Local Docker — Educational only |

## Findings

| # | Finding | OWASP | Severity |
|---|---|---|---|
| 01 | JWT Role in Payload + No MFA | API2:2023 | 🔴 HIGH |
| 02 | Excessive Data Exposure — PII | API3:2023 | 🟠 MEDIUM |
| 03 | BOLA — GPS Location Leaked | API1:2023 | 🚨 CRITICAL |
| 04 | No Rate Limiting on Login | API4:2023 | 🔴 HIGH |
| 05 | MFA Not Enforced | API2:2023 | 🔴 HIGH |
| 06 | Missing CSP Header | API8:2023 | 🔴 HIGH |
| 07 | CORS Wildcard (`*`) | API8:2023 | 🔴 HIGH |
| 08 | Server Version Disclosed | API8:2023 | 🟡 LOW |
| 09 | Weak Email Token — No Expiry | API2:2023 | 🔴 HIGH |

## Key Finding — BOLA (CRITICAL)
```
GET /identity/api/v2/vehicle/{uuid}/location
Authorization: Bearer [User A Token]

→ Returns GPS + name + email of ANY user. No ownership check.
```

## Tools

`Postman` `jwt.io` `Mailhog` `Browser DevTools` `Docker`

## Tags

`APISecurity` `OWASP` `crAPI` `BOLA` `JWT` `Postman` `MITRE` `CyberSecurity`
