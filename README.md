FUTURE_CS_03 — API Security Risk Analysis
SAIZERO — Ground Zero Defence
Every shadow has a hunter 🐺
![OWASP crAPI](https://img.shields.io/badge/Target-OWASP%20crAPI-blue?style=flat-square)
![API Security](https://img.shields.io/badge/Domain-API%20Security-critical?style=flat-square)
![Postman](https://img.shields.io/badge/Tool-Postman-orange?style=flat-square&logo=postman)
![MITRE ATT&CK](https://img.shields.io/badge/Framework-MITRE%20ATT%26CK-red?style=flat-square)
![Future Interns](https://img.shields.io/badge/Program-Future%20Interns%202026-darkblue?style=flat-square)
API Security Risk Analysis on OWASP crAPI — 9 vulnerabilities across 4 OWASP API Top 10 categories, mapped to CVE and MITRE ATT&CK.
---
Author
Satheesh Nithiananthan (CyberLycan)
SAIZERO — Ground Zero Defence | github.com/Satz-N-Sentry
---
Target
Field	Details
Application	OWASP crAPI (Completely Ridiculous API)
Base URL	`http://localhost:8888`
Services	`/identity`, `/community`, `/workshop`
Auth	JWT Bearer Token (RS256)
Scope	Local Docker — Educational only
---
Findings
#	Finding	OWASP	Severity
01	JWT Role in Payload + No MFA	API2:2023	🔴 HIGH
02	Excessive Data Exposure — PII + Financial	API3:2023	🟠 MEDIUM
03	BOLA — Vehicle GPS Location Leaked	API1:2023	🚨 CRITICAL
04	No Rate Limiting on Login	API4:2023	🔴 HIGH
05	MFA Not Enforced	API2:2023	🔴 HIGH
06	Missing Content-Security-Policy Header	API8:2023	🔴 HIGH
07	CORS Wildcard (`*`)	API8:2023	🔴 HIGH
08	Server Version Disclosed	API8:2023	🟡 LOW
09	Weak Email Token — No Expiry	API2:2023	🔴 HIGH
---
Key Finding — BOLA (CRITICAL)
```http
GET /identity/api/v2/vehicle/{uuid}/location
Authorization: Bearer [User A Token]

200 OK → returns GPS location + full name + email of any user
```
Any authenticated user can retrieve another user's real-time GPS location using their vehicle UUID. No ownership check. Physical safety risk.
---
MITRE ATT&CK Mapping
Finding	CVE	MITRE
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
Tools
Tool	Purpose
Postman	API testing, header inspection
Browser DevTools	Endpoint discovery
jwt.io	JWT decoding
Mailhog	Email token capture
Docker	Run crAPI locally
---
OWASP Coverage
Category	Status
API1 — BOLA	✅ CRITICAL
API2 — Broken Authentication	✅ HIGH
API3 — Excessive Data Exposure	✅ MEDIUM
API4 — Rate Limiting	✅ HIGH
API8 — Security Misconfiguration	✅ HIGH / LOW
---
Repo Structure
```
FUTURE_CS_03/
├── evidence/
│   └── FUTURE_CS_03_Evidence/
├── screenshots/
│   ├── finding_01_login_token.png
│   ├── finding_02_jwt_decoded.png
│   ├── finding_03_excessive_data.png
│   ├── finding_04_bola_location.png
│   ├── finding_05_no_rate_limit.png
│   ├── finding_06_security_headers.png
│   ├── finding_07_cors_wildcard.png
│   ├── finding_09_mfa_disabled.png
│   └── finding_10_email_token.png
├── reports/
│   └── SAIZERO_API_Security_Report.pdf
└── README.md
```
---
`APISecurity` `OWASP` `crAPI` `BOLA` `JWT` `Postman` `MITRE` `FutureInterns` `CyberSecurity` `BlueTeam`
