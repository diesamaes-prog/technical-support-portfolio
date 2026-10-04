# MS365 Incident 004 — Outlook Repeated Sign-In Prompt

## Issue

User reports that Outlook opens normally, but repeatedly prompts for Microsoft 365 credentials. The user enters valid credentials, but the sign-in prompt appears again. The issue prevents Outlook from maintaining an authenticated session and accessing the user's mailbox normally.

**Affected user:** Single workstation
**Application:** Microsoft Outlook / Microsoft 365
**Operating System:** Windows 10/11

---

## Initial Symptom

The user reports that Outlook continuously requests authentication even after entering valid Microsoft 365 credentials.

The user confirms that the credentials are correct and that the account can be accessed through the Microsoft 365 web portal.

---

## Investigation

The first step is to verify whether the Microsoft 365 account itself is accessible.

The user signs in to the Microsoft 365 portal through a web browser and successfully authenticates. This indicates that the account credentials are valid and that the issue is not caused by an incorrect password.

The next step is to verify whether the workstation has general Internet connectivity. The workstation is connected to the network and can access external websites normally.

The issue is then isolated to the Outlook desktop application.

Windows Credential Manager is checked for stored Microsoft 365 or Office credentials that may be causing an authentication conflict. Existing Microsoft Office-related credentials are identified.

The affected Outlook session is closed before removing outdated Office-related credentials. This is done carefully because removing credentials may require the user to authenticate again.

After the outdated credentials are removed, Outlook is reopened and the user is prompted to authenticate again.

The user enters their Microsoft 365 credentials and completes the authentication process.

Outlook successfully establishes the account session without repeatedly requesting credentials.

---

## Root Cause

The issue was caused by stale or conflicting Microsoft 365 authentication credentials stored on the Windows workstation.

The Microsoft 365 account itself was valid, but Outlook was unable to maintain the authenticated session using the existing cached credentials.

---

## Resolution

Outlook was closed and the affected Microsoft Office credentials were removed from Windows Credential Manager.

Outlook was then reopened and the user authenticated again using their valid Microsoft 365 credentials.

The new authentication session was established successfully and Outlook stopped repeatedly prompting for credentials.

No password reset or account replacement was required.

---

## Verification Results

```text
Microsoft 365 web authentication:
Successful. User was able to sign in to the Microsoft 365 portal.

Internet connectivity:
Successful. Workstation had normal Internet access.

Outlook authentication:
Successful. User authenticated successfully after removing stale credentials.

Outlook mailbox access:
Successful. Outlook maintained the authenticated session and accessed the mailbox normally.

Repeated sign-in prompt:
No longer occurring after reauthentication.

User confirmation:
User confirmed that Outlook was working normally.
```

---

## Evidence

Recommended screenshots for the GitHub portfolio:

```text
04-MS365/
└── troubleshooting-cases/
    └── 001-outlook-repeated-signin/
        ├── README.md
        └── evidence/
            ├── 01-office-portal-signin.png
            ├── 02-credential-manager.png
            ├── 03-outlook-signin.png
            ├── 04-outlook-authenticated.png
            └── 05-mailbox-access.png
```

**Important:** redact your personal email address, account name, tenant information, tokens, phone numbers, and any other private information before uploading screenshots.

---

## Final Ticket Notes

**Issue:** Outlook repeatedly prompted the user for Microsoft 365 credentials.

**Initial symptom:** User entered valid credentials, but Outlook repeatedly requested authentication.

**Affected user:** Single workstation.

**Investigation:** Microsoft 365 web authentication, Internet connectivity, Outlook authentication, and Windows Credential Manager were checked.

**Root Cause:** Stale or conflicting Microsoft 365 authentication credentials stored on the Windows workstation.

**Resolution:** Outdated Office-related credentials were removed from Windows Credential Manager and Outlook was reauthenticated.

**Verification:** User successfully authenticated to Microsoft 365, Outlook maintained the session, and mailbox access was restored without additional sign-in prompts.

**Status:** Resolved.


