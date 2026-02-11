# TKT-0021 – User Logged Into Temporary Profile

## Summary
User reported that their desktop environment appeared reset and personal files were missing after signing in. The issue was caused by Windows loading a temporary profile instead of the user’s original profile.

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

echo %USERPROFILE%
- Result showed: C:\Users\TEMP

Evidence:
- [Temporary profile path confirmation](../evidence/screenshots/temp-profile/temp-userprofile-path.png)
- [Default desktop after temporary profile login](../evidence/screenshots/temp-profile/desktop-reset.png)

---

## Investigation

### Profile Folder State
Reviewed:

C:\Users
Findings:
- Original profile folder renamed (`itp-user01.old`)
- Temporary profile folder created (`TEMP`)

Evidence:
- [Users directory showing TEMP profile](../evidence/screenshots/temp-profile/users-folder-temp.png)

---

### Event Viewer Analysis
Location:

Windows Logs → Application
Source: User Profile Service
Findings:
- Errors indicating failure to load local user profile
- System logged the user into a temporary profile

Evidence:
- [User Profile Service error in Event Viewer](../evidence/screenshots/temp-profile/user-profile-service-error.png)
- Full log export: [Event Viewer Export Log](../evidence/logs/eventviewer-exports/temp-profile-user-profile-service.evtx)

---

## Root Cause
The original user profile directory name did not match the path referenced in the ProfileList registry entry. Because the expected profile directory (`C:\Users\itp-user01`) was unavailable, Windows failed to load the profile and created a temporary profile.

---

## Resolution

Actions performed:

1. Logged in as local administrator (`itp-admin01`)
2. Renamed original profile folder:

C:\Users\itp-user01.old → C:\Users\itp-user01
3. Verified registry path: HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\ProfileList
ProfileImagePath = C:\Users\itp-user01

4. Removed temporary profile folder (`C:\Users\TEMP`)
5. Logged in as the affected user to validate profile loading

---

## Verification

### Profile Path
Command:

echo %USERPROFILE%
Result: C:\Users\itp-user01


Evidence:
- [Profile restored confirmation (USERPROFILE output)](../evidence/screenshots/temp-profile/profile-restored.png)

---

### Persistence Test
- User logged out and back in multiple times
- Profile loaded each session

### Final Folder State
Evidence:
- [Users directory after profile restoration](../evidence/screenshots/temp-profile/users-folder-after-fix.png)

---

## Impact
- Single user affected
- Temporary loss of access to the user environment
- No data loss (original profile preserved and restored)

---

## Lessons / Prevention
- Profile folder changes or corruption can cause Windows to load temporary profiles
- Verify ProfileList registry mappings and directory consistency during troubleshooting
- Always preserve original user data before making profile changes
