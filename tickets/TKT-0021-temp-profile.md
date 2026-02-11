# TKT-0021 – Temporary Profile Issue (itp-user01)

## Issue Overview
User itp-user01 reported that after logging in, their desktop appeared reset, and personal files were missing. The environment did not retain changes after logout. Investigation confirmed Windows was loading a temporary profile instead of the user’s original profile.

System Details:
Device: ITP-ENDPOINT-01
OS: Windows 11 Enterprise Evaluation
Account Type: Local Standard User

---

## Symptoms
- Default desktop and Start menu
- Missing user files and settings
- Changes did not persist after logout

Command output confirmed temporary profile usage:

echo %USERPROFILE%
C:\Users\TEMP

Evidence:
../evidence/screenshots/temp-profile/temp-userprofile-path.png
../evidence/screenshots/temp-profile/desktop-reset.png

---

## Investigation

Profile directory review at:
C:\Users

Findings:
- Original profile renamed: itp-user01.old
- Temporary profile folder created: TEMP

Evidence:
../evidence/screenshots/temp-profile/users-folder-temp.png

Event Viewer Analysis:
Event Viewer → Windows Logs → Application  
Source: User Profile Service

Findings:
- Errors indicating Windows could not load the local user profile
- System logged the user into a temporary profile

Evidence:
../evidence/screenshots/temp-profile/user-profile-service-error.png

Full log:
../evidence/logs/eventviewer-exports/temp-profile-user-profile-service.evtx

---

## Root Cause
The user profile directory name did not match the path configured in the Windows ProfileList registry. Because the expected directory (C:\Users\itp-user01) was unavailable, Windows failed to load the original profile and created a temporary profile.

---

## Resolution
1. Logged in as local administrator (itp-admin01)
2. Renamed profile directory:
   C:\Users\itp-user01.old → C:\Users\itp-user01
3. Verified registry mapping at:
   HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\ProfileList
   ProfileImagePath = C:\Users\itp-user01
4. Removed temporary profile folder:
   C:\Users\TEMP
5. Logged in as affected user to confirm profile loaded correctly

---

## Verification

Confirmed active profile path:

echo %USERPROFILE%
C:\Users\itp-user01

User logged out and back in multiple times. Profile loaded correctly and persisted.

Evidence:
../evidence/screenshots/temp-profile/profile-restored.png
../evidence/screenshots/temp-profile/users-folder-after-fix.png

---

## Impact
- Single user affected
- Temporary loss of access to user environment
- No data loss (original profile preserved and restored)

---

## Key Takeaways
- Temporary profiles commonly result from profile directory or registry mismatches
- Event Viewer (User Profile Service) is critical for diagnosing profile load failures
- Always preserve original user data before performing profile recovery
