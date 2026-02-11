# TKT-0021 – User Logged Into Temporary Profile

## Summary
User reported that their desktop environment appeared reset and personal files were missing after signing in. Issue was caused by Windows loading a temporary profile instead of the user’s original profile.

---

## Environment
- Device: ITP-ENDPOINT-01
- OS: Windows 11 Enterprise Evaluation
- User: itp-user01
- Account Type: Local Standard User

---

## User Reported Symptoms
- Default desktop and Start menu after login
- User data appeared missing
- Environment did not persist after logout

---

## Initial Triage
- Confirmed user successfully authenticated
- Verified abnormal profile behavior after login
- Checked active profile path using:

