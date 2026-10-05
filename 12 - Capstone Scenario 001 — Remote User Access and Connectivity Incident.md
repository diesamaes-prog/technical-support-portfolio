# Capstone Scenario 001 — Remote User Access and Connectivity Incident

## Extended Description

A remote employee contacted the Service Desk because they were unable to access several corporate services from their Windows workstation. The user reported that Outlook was repeatedly requesting authentication, Microsoft Teams was showing as disconnected, and the corporate VPN was failing to establish a connection.

The user confirmed that their home Internet connection was working and that public websites could be accessed normally. Because multiple corporate services were affected simultaneously, the incident required a structured troubleshooting approach covering network connectivity, DNS resolution, authentication, Microsoft 365, VPN configuration, and the Windows workstation.

The incident was treated as a single-user Service Desk incident and investigated using an ITIL/ITSM-based troubleshooting workflow. Each troubleshooting step was documented with its findings before moving to the next layer.

## User Report

> "My Internet is working, but I can't connect to the VPN. Outlook keeps asking for my password and Teams says I'm offline."

## Environment

* **Device:** Windows workstation
* **Operating System:** Windows 10/11
* **Connection:** Home Internet
* **Applications:** Outlook, Microsoft Teams
* **Services:** Microsoft 365, Corporate VPN
* **Identity:** Microsoft 365 / Entra ID
* **Support Level:** L1/L2 Service Desk
* **Affected Users:** 1
* **Work Arrangement:** Remote

## Incident Categorization

**Category:** Network / Remote Access / Microsoft 365

**Type:** Incident

**Impact:** Single user

**Urgency:** High

**Priority:** P2 — High

The incident was assigned a high priority because the user was unable to access multiple corporate services required to perform normal work activities.

---

# Investigation

## 1. Verify Physical and Internet Connectivity

The user confirmed that the workstation was connected to the home network.

Public websites were accessible normally.

**Finding:** The workstation had general Internet connectivity. The issue was not caused by a complete loss of network access.

## 2. Verify IP Configuration

The workstation was checked for a valid IPv4 configuration, subnet information, default gateway, and DNS configuration.

The workstation had a valid network configuration.

**Finding:** No local IP configuration problem was identified.

## 3. Test Default Gateway

Connectivity to the local network gateway was tested.

The gateway responded successfully.

**Finding:** The workstation could communicate with the local network and gateway.

## 4. Test Internet Connectivity

Connectivity to a known public IP address was tested without relying on DNS.

The test was successful.

**Finding:** Internet connectivity was available at the IP level.

## 5. Test DNS Resolution

DNS resolution was tested against a public domain.

The hostname resolved successfully.

**Finding:** DNS resolution was functioning correctly.

## 6. Test HTTPS Connectivity

TCP connectivity to HTTPS port 443 was tested.

The connection was successful.

**Finding:** The workstation could establish outbound HTTPS connections. No general firewall or Internet connectivity problem was identified.

## 7. Test Microsoft 365 Web Access

The user attempted to access Microsoft 365 through a web browser.

The user successfully authenticated using the current credentials and accessed Outlook on the web.

**Finding:** The Microsoft 365 account and credentials were valid. The issue was isolated to the local desktop applications and VPN connection.

## 8. Verify Account Status

The user's identity account was checked through the appropriate administrative tools.

The account was enabled and there was no indication of an account lockout.

**Finding:** No account-level authentication problem was identified.

## 9. Investigate Outlook Authentication

Outlook continued displaying authentication prompts despite successful Microsoft 365 web authentication.

Windows Credential Manager was reviewed.

Outdated Microsoft 365 authentication credentials associated with a previous password were identified.

**Finding:** Stale locally cached credentials were preventing Outlook from establishing a new authenticated session.

## 10. Investigate VPN Connection

The VPN client was restarted and the connection was attempted again.

The VPN continued to fail.

The VPN profile was reviewed and found to contain an outdated configuration.

**Finding:** The workstation was using an obsolete VPN profile.

---

# Root Cause

Two related local configuration issues were identified:

1. **Outdated Microsoft 365 credentials** stored in Windows Credential Manager were causing repeated Outlook authentication prompts.

2. **An outdated VPN configuration profile** was preventing the workstation from establishing the corporate VPN connection.

The user's Internet connection, DNS resolution, Microsoft 365 account, and general network connectivity were functioning normally.

---

# Resolution

The obsolete Microsoft 365 credentials were removed from Windows Credential Manager.

Outlook was restarted and the user authenticated using the current Microsoft 365 credentials. MFA was completed successfully.

The outdated VPN profile was then removed and replaced with the current approved corporate VPN configuration.

The VPN client was restarted and the user successfully established the corporate VPN connection.

---

# Verification

The following services were tested after the changes:

* Internet connectivity
* DNS resolution
* Microsoft 365 web access
* Outlook authentication
* Outlook mailbox synchronization
* Microsoft Teams connectivity
* Corporate VPN connection
* Internal corporate resources

The user successfully authenticated to Microsoft 365, Outlook synchronized normally, Teams returned to an online state, and the VPN connected successfully.

The user confirmed that required corporate applications and resources were accessible and that normal work could resume.

**Result:** Full service restoration confirmed.

---

# ITIL/ITSM Handling

### Incident Management

The issue was handled as an incident because previously available corporate services were unavailable to the user.

### Categorization

**Network → Remote Access → VPN / Microsoft 365 → Authentication**

### Priority

**P2 — High**

The priority reflected the user's inability to access multiple services required for normal business operations.

### Troubleshooting

Troubleshooting progressed from basic connectivity to application and authentication layers:

**Network → IP Configuration → Gateway → Internet → DNS → HTTPS → Microsoft 365 → Identity → Outlook → VPN**

This approach prevented unnecessary escalation and isolated the problem to local authentication and VPN configuration.

### Escalation

No escalation was required after the root causes were identified and resolved using standard Service Desk procedures.

### Documentation

The ticket documented:

* User symptoms
* Business impact
* Environment
* Category and priority
* Troubleshooting steps
* Findings
* Root cause
* Resolution
* Verification
* User confirmation
* Closure status

---

# Knowledge Base Opportunities

The incident identified two reusable Knowledge Base procedures:

1. **Outlook repeatedly prompts for Microsoft 365 credentials after a password change.**
2. **Corporate VPN connection fails because of an outdated VPN profile.**

Both procedures can be documented separately to reduce troubleshooting time for future incidents.

---

# Final Ticket Notes

**Issue:** Remote user unable to access corporate VPN and experiencing repeated Outlook authentication prompts.

**Impact:** Single remote user unable to access multiple corporate services required for work.

**Root Cause:** Stale Microsoft 365 credentials stored locally and an outdated VPN configuration profile.

**Resolution:** Removed obsolete credentials, reauthenticated Microsoft 365, replaced the outdated VPN profile, and re-established the corporate VPN connection.

**Verification:** Outlook, Teams, Microsoft 365, VPN, and required corporate resources were successfully tested.

**Escalation:** Not required.

**User Confirmation:** User confirmed that normal work activities could resume.

**Status:** Resolved / Closed

## Capstone Skills Demonstrated

* Windows troubleshooting
* TCP/IP troubleshooting
* DNS troubleshooting
* Network connectivity analysis
* HTTPS connectivity testing
* VPN troubleshooting
* Microsoft 365 support
* Outlook troubleshooting
* Identity and authentication
* MFA
* Credential Manager
* Entra ID concepts
* ITIL Incident Management
* Incident categorization
* Priority assessment
* Root Cause Analysis
* Knowledge Base development
* Technical documentation
* User communication
* L1/L2 troubleshooting methodology

