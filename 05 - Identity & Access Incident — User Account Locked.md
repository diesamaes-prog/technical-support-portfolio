# Identity & Access Incident 005 — User Account Locked

## Issue

The user reports being unable to authenticate to their Windows workstation and access Microsoft 365 resources. The user reports that the account appears to be locked even though they believe they are using the correct credentials.

**Affected user:** Single workstation / user account
**Issue type:** Identity & Access
**Environment:** Windows / Microsoft 365 / Enterprise Identity

---

## Initial Symptom

The user reports that authentication attempts are unsuccessful and that access to the account is unavailable.

The user states that they are using their expected credentials. The issue is treated as an identity and access problem rather than a general hardware or network issue.

---

# Investigation

## Step 1 — Identify the Current Windows User

The current Windows account is identified to establish which local user account is being used on the workstation.

The following commands are used:

```cmd
whoami
whoami /user
```

The output is reviewed to identify the username and associated security identifier (SID).

### Evidence

<img width="587" height="233" alt="image" src="https://github.com/user-attachments/assets/3a44d0cc-1e70-40d8-b8b0-ca6a9b61a685" />

---

## Step 2 — Verify Local Account Status

The local Windows account configuration is reviewed to determine whether the account is active, disabled, or subject to a local account restriction.

The following command can be used:

```cmd
net user
```

The specific user account can then be reviewed with:

```cmd
net user <username>
```

The account status and available account information are reviewed.

### Evidence

**Screenshot:**

<img width="857" height="374" alt="image" src="https://github.com/user-attachments/assets/46f07de6-4c27-413b-919b-20b56f5f81a6" />


---

## Step 3 — Check for Authentication or Account-Related Events

Windows Event Viewer is reviewed for authentication-related events that could help identify failed logon attempts or account problems.

Open:

```text
Event Viewer
→ Windows Logs
→ Security
```

Relevant authentication events are reviewed, particularly failed logon events.

The investigation should focus on identifying:

* Failed authentication attempts
* Logon failures
* Account-related errors
* Time of the failed attempt
* Authentication source, when available

### Evidence

**Screenshot:**


---

## Step 4 — Check Network Connectivity

Before investigating an authentication problem further, basic network connectivity is verified.

Run:

```cmd
ipconfig
```

Then test the local network connection using the default gateway identified in the output:

```cmd
ping <default-gateway>
```

This determines whether the workstation can communicate with the local network.

### Evidence

**Screenshot:**

---

<img width="482" height="450" alt="image" src="https://github.com/user-attachments/assets/77f75c90-0bde-4f1c-bf89-726a5df479c9" />


Step 5 — Check Microsoft 365 Authentication

Open a browser and go to:

https://www.office.com

Sign in using the Microsoft 365 account associated with the incident.

The purpose of this test is to determine whether the account can authenticate successfully through the web or whether authentication is failing across multiple services.

Evidence

Screenshot:

<img width="444" height="481" alt="image" src="https://github.com/user-attachments/assets/fc93ec75-ee6a-4e5d-966f-80bf8fa9884c" />


[INSERT EVIDENCE HERE]

Security: Redact your email address and any other personal or organizational information before uploading the screenshot.

Step 6 — Investigate the Lockout Source

In a real enterprise environment, the account status and authentication logs would be reviewed through the organization's identity-management platform.

Possible sources include:

Active Directory

Domain Controller Security logs

Microsoft Entra ID

Microsoft 365 sign-in logs

Identity and Access Management platform

The investigation should determine whether repeated authentication attempts originated from:

The user's workstation

A mobile device

A VPN client

A mapped network resource

Outlook or another application

A saved or outdated credential

Another workstation or device

Evidence

Screenshot:
<img width="411" height="556" alt="image" src="https://github.com/user-attachments/assets/2bbdd876-7853-4934-9bf5-b43fa306ea0f" />


Lab note: If you do not have access to an enterprise AD/Entra environment, mark this as Simulated Enterprise Investigation rather than creating fabricated evidence.

Step 7 — Unlock the Account

Once the account lockout is confirmed, an authorized administrator would unlock the account using the organization's approved identity-management procedure.

Do not intentionally lock your personal Microsoft or Windows account to reproduce this step.

Evidence

Screenshot:

<img width="1332" height="651" alt="image" src="https://github.com/user-attachments/assets/333bb39c-1b44-43a2-8c0c-910ce360b3bc" />


If this is simulated:

[SIMULATED STEP — Enterprise identity-management platform required]

Step 8 — Reauthenticate

After the account has been unlocked, the user attempts to authenticate again using the current credentials.

The authentication process is monitored to confirm that the user can establish a successful session.

Evidence

Screenshot:

<img width="1357" height="637" alt="image" src="https://github.com/user-attachments/assets/db1f0eb5-f6e6-4af3-9cac-b66281cce21b" />


Step 9 — Verify Microsoft 365 Access

The user accesses Microsoft 365 again and verifies that the required services are available.

The user confirms that authentication remains active and that the previous authentication problem is no longer occurring.

## Investigation Results

**Account identification:**
The current Windows user account was identified using `whoami` and `whoami /user`. The username and associated SID were confirmed from the local workstation.

**Account status:**
The local account was reviewed using `net user <username>`. The account was confirmed as active and not disabled at the local Windows level.

**Authentication events:**
Windows Security logs were reviewed for authentication-related events. The investigation focused on failed logon events, including the account involved, logon type, failure reason, workstation name, and source information when available. No enterprise Active Directory or Entra ID lockout event could be verified because this workstation is not connected to an enterprise identity environment.

**Network connectivity:**
Network connectivity was verified successfully. The workstation had network connectivity and was able to communicate with the local gateway, indicating that the authentication issue was not caused by a basic network connectivity failure.

**Microsoft 365 authentication:**
Microsoft 365 web authentication was tested through the Office portal. The user was able to authenticate successfully, confirming that the Microsoft 365 account credentials were accepted by the service.

**Lockout source:**
No definitive enterprise lockout source could be identified in this standalone lab environment. The available local Windows evidence did not provide sufficient information to attri


Screenshot:
<img width="663" height="610" alt="image" src="https://github.com/user-attachments/assets/e2d4bdf6-bd5b-4923-9119-9dfb6954418e" />

**Issue:**
User unable to authenticate because of an apparent account-lockout condition.

**Initial symptom:**
Authentication attempts were unsuccessful and access to required resources was unavailable.

**Affected user:**
Single workstation / user account.

**Investigation:**
User identity and local account status were verified. Windows Security authentication events were reviewed for failed authentication activity. Network connectivity was confirmed, including communication with the local gateway. Microsoft 365 web authentication was tested successfully. Potential lockout sources were investigated using the available local Windows Security logs.

The workstation was operating as a standalone lab environment and was not connected to an enterprise Active Directory or Entra ID environment. Therefore, an actual enterprise account-lockout event or Domain Controller source

Evidence Folder

05-Identity-Access/
└── troubleshooting-cases/
    └── 001-account-lockout/
        ├── README.md
        └── evidence/
            ├── 01-account-identity.png
            ├── 02-account-status.png
            ├── 03-authentication-event.png
            ├── 04-network-connectivity.png
            ├── 05-microsoft365-authentication.png
            ├── 06-lockout-source.png
            ├── 07-account-unlocked.png
            ├── 08-authentication-success.png
            ├── 09-microsoft365-access.png
            └── 10-final-verification.png

