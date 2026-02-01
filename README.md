# Windows User & Profile Troubleshooting Lab

## Overview
This project demonstrates hands-on Windows endpoint troubleshooting skills commonly required in **IT Analyst / Tier 1–2 support roles**.  
The focus is on diagnosing and resolving **user logon, profile, and permissions-related issues** using structured troubleshooting, log analysis, and clear ticket documentation.

The lab simulates real-world helpdesk scenarios such as temporary profiles, corrupted user profiles, and login failures, with emphasis on **root cause analysis, remediation, and verification**.

---

## Objectives
- Troubleshoot Windows user login and profile issues
- Analyze Event Viewer logs to identify root causes
- Repair or rebuild corrupted local user profiles
- Validate fixes through repeatable verification steps
- Document incidents using professional IT ticket formats

---

## Environment
- **Operating System:** Windows 10/11 (Virtual Machine)
- **User Types:** Local admin and standard users
- **Tools Used:**
  - Windows Event Viewer
  - Local Users & Groups
  - File Explorer (`C:\Users`)
  - Registry Editor (read-only where applicable)
  - Virtualization snapshots for rollback

---

## Tickets Included
Each issue is documented as an individual ticket to mirror real IT workflows.

| Ticket ID | Scenario |
|---------|---------|
| TKT-0021 | User logged into a temporary profile |
| TKT-0022 | Corrupted local user profile prevents sign-in |
| TKT-0023 | Login failure caused by profile or permission issues |
| TKT-0024 | User unable to sign in due to system or policy misconfiguration |

Ticket writeups include:
- User-reported symptoms
- Initial triage steps
- Evidence (logs and screenshots)
- Root cause analysis
- Remediation steps
- Verification of successful resolution

---

## Repository Structure
```text
windows-user-profile-troubleshooting/
├─ README.md
├─ tickets/
│ ├─ TKT-0021-temp-profile.md
│ ├─ TKT-0022-profile-corruption.md
│ ├─ TKT-0023-permissions-login-failure.md
│ └─ TKT-0024-user-cannot-signin.md
├─ evidence/
│ ├─ screenshots/
│ │ ├─ temp-profile/
│ │ ├─ profile-service/
│ │ ├─ permissions/
│ │ └─ event-viewer/
│ └─ logs/
│ └─ eventviewer-exports/
├─ templates/
│ ├─ ticket-template.md
│ └─ rca-template.md
└─ changelog.md
