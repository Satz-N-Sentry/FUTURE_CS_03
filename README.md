FUTURE_CS_03 — API Security Risk Analysis Report
SAIZERO — Ground Zero Defence
Every shadow has a hunter 🐺
---
Overview
This repository contains a professional API Security Risk Analysis conducted
as part of the Future Interns Cybersecurity Internship 2026.
The assessment targeted OWASP crAPI (Completely Ridiculous API) — an
intentionally vulnerable API platform built by OWASP specifically for
API security learning and testing.
9 confirmed vulnerabilities were identified across 4 OWASP API Security
Top 10 categories, with full CVE and MITRE ATT&CK framework mapping.
---
Target API
Field	Details
Application	OWASP crAPI (Completely Ridiculous API)
Base URL	http://localhost:8888
Services	/identity, /community, /workshop
Auth Method	JWT Bearer Token (RS256)
Assessment Type	Read-Only API Security Risk Analysis
Scope	Local Docker deployment — Educational only
---
Findings Summary
#	Finding	OWASP	Severity
01	JWT Token — Role in Payload + No MFA	API2:2023	HIGH
02	Excessive Data Exposure — PII + Financial	API3:2023	MEDIUM
03	BOLA — Vehicle GPS Location Leaked	API1:2023	CRITICAL
04	No Rate Limiting on Login Endpoint	API4:2023	HIGH
05	MFA Not Required — Single Factor Only	API2:2023	HIGH
06	Missing Content-Security-Policy Header	API8:2023	HIGH
07	CORS Wildcard (*) Misconfiguration	API8:2023	HIGH
08	Server Version Disclosed	API8:2023	LOW
09	Weak Email Change Token — No Expiry	API2:2023	HIGH
---
Key Finding — BOLA (CRITICAL)
```
Endpoint: GET /identity/api/v2/vehicle/{uuid}/location
Authorization: Bearer \[User A Token]

Response 200 OK:
{
  "carId": "5204faf7-2b4c-4909-a801-f86f772362be",
  "vehicleLocation": {
    "latitude": "38.206348",
    "longitude": "-84.270172"
  },
  "fullName": "usera",
  "email": "usera@test.com"
}
```
Any authenticated user can retrieve the real-time GPS location of any
other user by supplying their vehicle UUID. No ownership verification
is performed. Physical safety risk — not just a data breach.
---
CVE & MITRE ATT&CK References
Finding	CVE	MITRE ATT&CK
JWT / MFA	CVE-2022-21449, CWE-287	T1552.004, T1078
Excessive Data	CVE-2019-14234, CWE-213	T1530, T1213
BOLA GPS	CVE-2021-20114, CWE-639	T1083, T1530
Rate Limiting	CVE-2019-19781, CWE-307	T1110, T1110.001
MFA Missing	CWE-308, CWE-287	T1078, T1556
CSP Missing	CVE-2016-5088, CWE-1021	T1059.007, T1185
CORS Wildcard	CVE-2018-1000007, CWE-942	T1539, T1185
Server Version	CWE-200	T1592, T1590
Weak Token	CVE-2020-14179, CWE-640	T1110.003, T1078
---
Tools Used
Tool	Purpose
Postman	API request crafting, response analysis, header inspection
Browser DevTools	Network traffic monitoring, endpoint discovery
jwt.io	JWT token decoding and algorithm analysis
Mailhog	Email token capture and expiry verification
Docker	Running OWASP crAPI locally
Git	Version control
GitHub	Repository hosting for submission
---
Methodology
Setup — Deploy crAPI via Docker, create two test accounts
Reconnaisance — Map all API endpoints via documentation and DevTools
Authentication Testing — JWT analysis, brute force, MFA check
Authorization Testing — BOLA via UUID manipulation across accounts
Data Exposure — Response field analysis against minimum necessary
Header Inspection — Security headers via Postman response tab
CORS Testing — Forged Origin header testing
Email Flow — Token capture via Mailhog, entropy and expiry analysis
Documentation — Map to OWASP API Top 10, CVE, MITRE ATT&CK
---
OWASP API Security Top 10 Coverage
Category	Status
API1:2023 — Broken Object Level Authorization	✅ Found — CRITICAL
API2:2023 — Broken Authentication	✅ Found — HIGH
API3:2023 — Broken Object Property Level Auth	✅ Found — MEDIUM
API4:2023 — Unrestricted Resource Consumption	✅ Found — HIGH
API5:2023 — Broken Function Level Authorization	Not in scope
API6:2023 — Unrestricted Access to Sensitive Flows	Not in scope
API7:2023 — Server Side Request Forgery	Not in scope
API8:2023 — Security Misconfiguration	✅ Found — HIGH/LOW
API9:2023 — Improper Inventory Management	Not in scope
API10:2023 — Unsafe Consumption of APIs	Not in scope
---
Repository Structure
```
FUTURE\\\_CS\\\_03/
├── evidence/FUTURE\\\_CS\\\_03\\\_Evidence



├── screenshots/
│   ├── finding\\\_01\\\_login\\\_token.png
│   ├── finding\\\_02\\\_jwt\\\_decoded.png
│   ├── finding\\\_03\\\_excessive\\\_data.png
│   ├── finding\\\_04\\\_bola\\\_location.png
│   ├── finding\\\_05\\\_no\\\_rate\\\_limit.png
│   ├── finding\\\_06\\\_security\\\_headers.png
│   ├── finding\\\_07\\\_cors\\\_wildcard.png
│   ├── finding\\\_09\\\_mfa\\\_disabled.png
│   └── finding\\\_10\\\_email\\\_token.png
├── reports/
│   └── SAIZERO\\\_API\\\_Security\\\_Report.pdf
└── README.md

```
\---

```

\---

## Assessor

**Satheesh Nithiananthan** (CyberLycan)
