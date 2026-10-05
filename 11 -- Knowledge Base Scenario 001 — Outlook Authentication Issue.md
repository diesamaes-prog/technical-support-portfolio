# Knowledge Base Scenario 001 — Outlook Authentication Issue

## Extended Description

A user contacted the Service Desk because Microsoft Outlook repeatedly prompted for their Microsoft 365 password and would not maintain a connected status. The user confirmed that Internet access was working normally and that other websites could be accessed without interruption.

The issue affected the Outlook desktop application on a Windows workstation. The user was unable to reliably access their corporate mailbox through Outlook, which prevented normal email communication.

The Service Desk investigated the issue by validating network connectivity, Microsoft 365 web access, account authentication, and the local Outlook authentication state.

## User Report

> "Outlook keeps asking me for my password. I enter it, but it asks again and Outlook stays disconnected."

## Environment

* **Operating System:** Windows 10/11
* **Application:** Microsoft Outlook Desktop
* **Service:** Microsoft 365 Email
* **Support Level:** L1 Service Desk
* **Affected Users:** 1

## Incident Categorization

**Category:** Application Support / Microsoft 365 / Outlook

**Type:** Incident

**Impact:** Single user

**Urgency:** Medium

**Priority:** P3 — Medium

The incident affected the user's ability to use corporate email, but other workstation functions and Internet access remained available.

## Initial Assessment

The user confirmed that:

* Internet access was working.
* Other websites were accessible.
* The issue was isolated to Outlook.
* The problem began after the user's Microsoft 365 password had been changed.
* Outlook repeatedly requested authentication.

The initial assessment indicated that the problem was more likely related to local authentication credentials or cached authentication data than to a general network outage.

## Troubleshooting

### 1. Verify Internet Connectivity

The user successfully accessed public websites.

**Finding:** Internet connectivity was working normally.

### 2. Test Microsoft 365 Web Access

The user signed in to Microsoft 365 through a web browser using the updated password.

The user successfully accessed Outlook on the web.

**Finding:** The Microsoft 365 account and new password were valid. The issue was isolated to the Outlook desktop application.

### 3. Verify Account Status

The account was checked through the available identity-management tools.

The account was enabled and there was no indication of an account lockout.

**Finding:** No account-level issue was identified.

### 4. Restart Outlook

Outlook was completely closed and restarted.

The application continued requesting the user's previous credentials.

**Finding:** Restarting Outlook did not resolve the issue.

### 5. Remove Outdated Cached Credentials

Windows Credential Manager was reviewed.

Outdated Microsoft 365/Outlook credentials associated with the previous password were identified.

The obsolete credentials were removed according to the standard Service Desk troubleshooting procedure.

### 6. Reauthenticate Outlook

Outlook was reopened after the cached credentials were removed.

The application prompted the user to authenticate again.

The user entered the current Microsoft 365 credentials and successfully completed MFA.

**Result:** Outlook authenticated successfully.

## Root Cause

The issue was caused by **outdated cached Microsoft 365 authentication credentials stored on the Windows workstation after the user's password change**.

Outlook continued attempting to authenticate using previously stored credentials, resulting in repeated password prompts and preventing the application from maintaining a connected session.

## Resolution

The obsolete Microsoft 365 credentials were removed from Windows Credential Manager.

Outlook was restarted and the user authenticated using the current Microsoft 365 credentials.

MFA authentication was completed successfully.

The Outlook client established a new authenticated session with Microsoft 365.

## Verification

The following checks were completed:

* Outlook displayed a connected status.
* The user's mailbox loaded successfully.
* New messages synchronized correctly.
* The user successfully sent an email.
* The user successfully received an email.
* Repeated password prompts no longer appeared.
* Microsoft 365 web access remained functional.

**Result:** Service fully restored.

## Knowledge Base Article

### Title

**Outlook Repeatedly Prompts for Microsoft 365 Credentials After Password Change**

### Symptoms

Users may experience:

* Repeated Outlook password prompts.
* Outlook displaying a disconnected status.
* Authentication failures after changing a Microsoft 365 password.
* Outlook working through the browser but not through the desktop client.

### Resolution

1. Confirm Internet connectivity.
2. Test Microsoft 365 authentication through the browser.
3. Verify the account is active and not locked.
4. Close Outlook completely.
5. Review Windows Credential Manager.
6. Remove obsolete Microsoft 365/Outlook credentials.
7. Restart Outlook.
8. Authenticate using the current credentials.
9. Complete MFA.
10. Confirm mailbox synchronization and send/receive functionality.

### Escalation

Escalation was **not required** in this case because the issue was resolved through standard L1 troubleshooting.

## Final Ticket Notes

**Issue:** Outlook repeatedly requesting Microsoft 365 credentials after password change.

**Impact:** Single user unable to maintain an authenticated Outlook session.

**Root Cause:** Outdated cached credentials stored locally on the Windows workstation.

**Resolution:** Removed obsolete credentials and reauthenticated Outlook using the current Microsoft 365 credentials.

**Verification:** Outlook connected successfully, mailbox synchronization was restored, and the user successfully sent and received email.

**Escalation:** Not required.

**Status:** Resolved / Closed

## ITIL/ITSM Alignment

The incident was handled using standard Incident Management practices:

* Incident identified and logged.
* Appropriate category and priority assigned.
* User impact documented.
* Troubleshooting actions recorded.
* Findings documented after each diagnostic step.
* Root cause identified.
* Service restored.
* Resolution verified with the user.
* Knowledge Base documentation created to support future incidents.

**Final Outcome:** The user's Outlook service was fully restored and the documented resolution can be reused by Service Desk analysts for similar authentication incidents.

