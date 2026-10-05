# ITIL/ITSM Incident 001 — VPN Connection Failure

## Incident

A remote user reported that they were unable to connect to the corporate VPN. The user's Internet connection was working normally, but the VPN client failed during connection.

The user needed VPN access to reach internal applications and shared corporate resources.

## User Report

> "My Internet is working, but I can't connect to the company VPN. The VPN keeps failing when I try to sign in."

## Environment

* Device: Windows workstation
* Connection: Home Internet
* VPN Client: Corporate VPN client
* Support Level: L1 Service Desk
* Service: Remote Access / VPN
* Affected Users: 1

## Categorization

**Category:** Network / Remote Access / VPN

**Type:** Incident

**Impact:** Single user

**Urgency:** High

**Priority:** P2 — High

The priority was assigned based on the user's inability to access required corporate resources while confirming that the issue was isolated to a single workstation.

## Initial Assessment

The user confirmed that normal Internet access was available.

Websites and other public Internet services were accessible, indicating that the workstation had general network connectivity.

The issue appeared to be isolated to the corporate VPN connection.

## Troubleshooting

### 1. Verify Internet Connectivity

The user confirmed that normal websites could be accessed.

**Finding:** General Internet connectivity was available.

### 2. Verify VPN Credentials

The user confirmed that the correct corporate credentials were being used.

There was no indication of an expired password or account lockout.

**Finding:** Authentication credentials were not identified as the cause.

### 3. Restart VPN Client

The VPN client was completely closed and restarted.

The user attempted to establish the VPN connection again.

**Result:** The VPN connection continued to fail.

### 4. Verify Local Network Configuration

The workstation was checked for a valid IP configuration, default gateway, and DNS configuration.

The workstation had a valid network configuration.

**Finding:** No local IP configuration issue was identified.

### 5. Test Local Network Connectivity

The default gateway was reachable and the workstation had normal Internet connectivity.

**Finding:** The problem was not caused by a basic local network or Internet connectivity failure.

### 6. Check VPN Configuration

The VPN connection profile was reviewed.

The VPN client was using an outdated VPN profile containing an incorrect VPN gateway configuration.

The profile was removed and recreated using the current corporate VPN configuration.

## Root Cause

The incident was caused by an **outdated VPN configuration profile** on the user's workstation.

The workstation itself had normal network connectivity, but the VPN client was attempting to establish the corporate connection using an obsolete VPN gateway configuration.

## Resolution

The outdated VPN profile was removed from the workstation.

The current corporate VPN configuration was deployed and configured in the VPN client.

The VPN client was restarted and the user attempted to connect again.

The VPN connection was established successfully.

## Verification

After the VPN connection was established, the following were verified:

* VPN client displayed a connected status.
* The workstation received the expected VPN connection information.
* Internal corporate resources were accessible.
* Internal applications could be reached.
* The user confirmed that they could resume normal work.

**Result:** Service restored successfully.

## ITIL/ITSM Handling

### Incident Management

The issue was handled as an incident because the primary objective was to restore a previously available service: remote VPN access.

### Categorization

The incident was categorized as:

**Network → Remote Access → VPN**

### Prioritization

The incident was assigned **P2 — High** because the user could not access required corporate resources, while the issue remained limited to a single user.

### SLA Management

The ticket was monitored against the applicable response and resolution targets.

Troubleshooting actions and timestamps were documented throughout the incident.

### Escalation

L1 troubleshooting was performed first.

Because the initial client restart and connectivity checks did not resolve the issue, the VPN configuration was investigated further. No Network Operations escalation was required after the outdated profile was identified and corrected.

### Documentation

The ticket was updated with:

* User-reported symptoms
* Business impact
* Category and priority
* Troubleshooting performed
* Findings
* Root cause
* Resolution
* Verification
* Final user confirmation

## Final Ticket Notes

**Issue:** User unable to connect to corporate VPN.

**Impact:** Single remote user unable to access internal corporate resources.

**Root Cause:** Outdated VPN configuration profile containing an obsolete VPN gateway configuration.

**Resolution:** Removed outdated VPN profile and configured the current corporate VPN profile.

**Verification:** VPN connection established successfully and internal resources were accessible.

**Status:** Resolved / Closed

**Closure:** User confirmed that VPN access was restored and normal work could resume.

