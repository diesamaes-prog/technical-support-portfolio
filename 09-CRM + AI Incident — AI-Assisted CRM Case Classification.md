# CRM + AI Incident 001 — HubSpot Application Login Failure

**Platform:** HubSpot CRM
**Category:** CRM / Customer Support / Technical Support
**Application:** HubSpot CRM
**Case ID:** CRM-2026-001
**Severity:** Medium
**Initial Status:** New
**Final Status:** Closed — Lab Exercise Completed
**Environment:** HubSpot CRM + AI Assistant
**Customer:** Fictional

---

# 1. Incident

A fictional customer contacted the support team because they were unable to authenticate to an application.

The customer reported that their password had previously worked but was now being rejected. The customer had already attempted two password resets.

The customer confirmed that general Internet access was working and that other websites were accessible.

The customer needed access to the application to submit a time-sensitive report.

The purpose of this laboratory project is to demonstrate a realistic CRM support workflow using HubSpot, including ticket creation, classification, AI-assisted analysis, troubleshooting documentation, human validation, privacy protection, and case closure.

No real customer information, credentials, authentication tokens, or confidential company information are used.

---

# 2. Customer

Create a fictional HubSpot contact.

**First name:**

```text
Daniel
```

**Last name:**

```text
Morgan
```

**Email:**

```text
daniel.morgan@example.com
```

Use the reserved `example.com` domain rather than a real person's email address.

**Evidence:**

<img width="712" height="400" alt="image" src="https://github.com/user-attachments/assets/b729ca5e-20b6-4633-836f-75fadbe9ee01" />

<img width="276" height="303" alt="image" src="https://github.com/user-attachments/assets/3f5c8af8-159a-4b02-a2b4-0684877c2cad" />



---

# 3. Customer Message

Use this fictional customer message for the ticket:

```text
Hi, I can't log into my account anymore. My password was working yesterday, but today the system keeps rejecting it. I already tried resetting it twice. I can access other websites normally, but I cannot access the application. I need this fixed because I have to submit my report today.
```

---

# 4. Initial Manual Assessment

Before using AI, manually identify the information contained in the customer's message.

## Known Symptoms

```text
Application authentication failure
Password previously worked
Two password-reset attempts completed
General Internet connectivity available
Application remains inaccessible
Customer has a time-sensitive business requirement
```


## Unknown Information

```text
Application name
Exact authentication error
Approximate time the problem started
MFA status
Account status
Whether other users are affected
Whether web authentication works
Browser/application being used
Whether the issue occurs on another approved workstation
```

## Possible Causes

These are only hypotheses:

```text
Account lockout
Account disabled
MFA problem
Identity-provider issue
Application authentication failure
Browser/session issue
Application-side issue
```

No root cause should be declared at this stage.

---

# 5. Create the HubSpot Ticket

Create a ticket associated with the fictional contact.


<img width="1073" height="575" alt="image" src="https://github.com/user-attachments/assets/a6c83020-4647-410e-a604-43ccdb2ab2c2" />

<img width="262" height="562" alt="image" src="https://github.com/user-attachments/assets/5a96a6a1-6d6d-482d-8d77-08ba2f287bd9" />

<img width="780" height="566" alt="image" src="https://github.com/user-attachments/assets/c3b46f51-7c47-4092-abf6-9fcc3fddab14" />

## Ticket Subject

```text
Application Login Failure — Customer Unable to Authenticate
```

## Ticket Description

```text
Customer reports that they are unable to log into an application.

The customer states that their password was working previously but is now being rejected. The customer has already attempted two password resets.

The customer confirms that general Internet access is working and that other websites are accessible.

The customer needs access to the application to submit a report today.

No password, authentication token, or other credentials were requested or provided.
```

## Initial Properties

**Category**

```text
Identity & Access
```

**Subcategory**

```text
Application Authentication
```

**Priority**

```text
Medium
```

**Channel**

```text
Email
```

**Status**

```text
New
```

**Root Cause**

```text
Not yet determined
```

**Evidence:**

```text
02-hubspot-ticket.png
```

---

# 6. Document the Customer Interaction

Add an internal note to the ticket:


<img width="587" height="508" alt="image" src="https://github.com/user-attachments/assets/87faf3c4-8a3f-4ebb-acd0-0b4210bb3b20" />


```text
Customer reports inability to authenticate to the application.

Customer states that the password previously worked but is currently being rejected despite two password-reset attempts.

General Internet access is available.

Customer requires application access to complete a time-sensitive report.

No credentials were requested or documented.
```

**Evidence:**

```text

<img width="234" height="411" alt="image" src="https://github.com/user-attachments/assets/46236a15-2116-465e-9120-c06e387d8756" />


---

# 7. Data Protection Review

Before sending any information to an AI assistant, verify that the case contains no sensitive information.

Confirm that the following are absent:

```text
Customer password
Authentication token
Real email address
Real phone number
Account number
Employee ID
Security questions
MFA codes
Internal URLs
Internal credentials
Confidential company information
```

The fictional contact uses:

```text
daniel.morgan@example.com
```

and therefore does not expose a real customer's email address.

**Evidence:**

```text

<img width="1077" height="592" alt="image" src="https://github.com/user-attachments/assets/33d68e7d-7b4d-44e8-a396-93a7afd6ef9f" />

<img width="479" height="415" alt="image" src="https://github.com/user-attachments/assets/1594e27b-60a6-4b1b-89e9-d641637af858" />


---

# 8. AI-Assisted Case Classification

Use ChatGPT, Microsoft Copilot, or another approved AI assistant.

Only send the anonymized case information.

## Prompt

```text
You are assisting a customer support analyst with CRM ticket classification.

Analyze the following anonymized support case.

Do not assume facts that are not provided.

Provide:

1. Suggested category
2. Suggested subcategory
3. Suggested priority
4. Key symptoms
5. Possible causes, clearly labeled as hypotheses
6. Missing information
7. Recommended troubleshooting steps
8. A concise internal CRM summary

Do not request passwords, authentication tokens, or sensitive customer information.

Do not claim a root cause without supporting evidence.

Treat your output as analyst assistance, not as a final diagnosis.

Case:

The customer cannot authenticate to an application. Their password worked previously but is now being rejected. They have already attempted two password resets. General Internet access works, but the application remains inaccessible. The customer needs access to submit a report today.
```

Save the AI response.

**Evidence:**

```text
<img width="764" height="292" alt="image" src="https://github.com/user-attachments/assets/4b8b2389-a9da-46c5-a0ed-d203c18757a9" />

<img width="778" height="245" alt="image" src="https://github.com/user-attachments/assets/01e2346e-5b6b-401f-9019-16d1ab715914" />

<img width="793" height="427" alt="image" src="https://github.com/user-attachments/assets/b19ee2b7-6fb9-4db6-8640-421c490402d1" />

<img width="796" height="478" alt="image" src="https://github.com/user-attachments/assets/cd58984e-f98e-4879-83d2-07f46ba3c4ca" />

<img width="785" height="336" alt="image" src="https://github.com/user-attachments/assets/41e77a1b-af14-4d68-9204-655108acfaf7" />


---

# 9. Human Review of AI Output

The AI output must be reviewed before being used in the CRM.

Check:

### Classification

Does the AI identify this as an authentication/access problem?

### Priority

Does the suggested priority make sense given the available information?

### Evidence

Does the AI distinguish known facts from assumptions?

### Root Cause

Did the AI incorrectly claim a definitive cause?

### Security

Did the AI request a password, MFA code, token, or other sensitive information?

### Troubleshooting

Are the suggested steps safe and appropriate?

Document the review:

```text
AI-generated classification and troubleshooting recommendations were reviewed by the support analyst.

The output was treated as advisory only.

No definitive root cause was accepted without supporting evidence.

Any unsupported assumptions or unsafe recommendations were excluded from the CRM workflow.
```

**Evidence:**

```text
<img width="686" height="508" alt="image" src="https://github.com/user-attachments/assets/9356878f-d091-40f6-9b81-432b40dd7c17" />

---

# 10. Update the Ticket Classification

Update the HubSpot ticket.

**Status**

```text
In Progress
```

**Category**

```text
Identity & Access
```

**Subcategory**

```text
Application Authentication
```

**Priority**

```text
Medium
```

**Root Cause**

```text
Not yet determined
```

**Next Action**

```text
Collect the application name, exact authentication error, MFA status, account status, and issue scope before performing additional troubleshooting or escalation.
```

**Evidence:**

```text
<img width="1102" height="594" alt="image" src="https://github.com/user-attachments/assets/e611dacc-e07a-4398-ac7d-dd8814f98116" />

---

# 11. AI-Assisted Troubleshooting Plan

Ask the AI assistant to produce a structured troubleshooting plan.

## Prompt

```text
Create a structured Service Desk troubleshooting plan for this anonymized CRM case.

Do not assume the account is locked or disabled.

Do not request the user's password.

Prioritize evidence collection before making account changes.

Case:

The customer cannot authenticate to an application. The password previously worked but is now rejected. Two password resets have already been attempted. General Internet access works.

Include:

- Initial verification
- Authentication checks
- MFA checks
- Account-status checks
- Application/browser checks
- Scope verification
- Escalation criteria
```

Save the response.

**Evidence:**

```text

<img width="1194" height="600" alt="image" src="https://github.com/user-attachments/assets/da307528-71bf-420c-831a-9aea4862a9d3" />

---

# 12. Human-Validated Troubleshooting Plan

The final analyst-approved plan should be:

```text
1. Confirm the exact application name.

2. Obtain the exact authentication error.

3. Confirm when the problem started.

4. Determine whether MFA is involved.

5. Determine whether other users are affected.

6. Verify account status through the authorized identity-management process.

7. Determine whether authentication works through an approved web portal.

8. Check browser/application session issues.

9. Determine whether the problem is account-specific or application-wide.

10. Escalate to Identity or Application Support if required.
```

Do **not**:

```text
Intentionally lock the account
Repeatedly enter incorrect passwords
Request the customer's password
Request MFA codes
Perform unauthorized account changes
Invent a successful resolution
```

**Evidence:**

```text
<img width="690" height="514" alt="image" src="https://github.com/user-attachments/assets/56170382-f553-45c9-9ec4-b7f6c784d0f3" />


---

# 13. AI-Generated CRM Summary

Use the following prompt:

```text
Create a concise internal CRM case summary.

Do not invent facts or a root cause.

Include:

- Customer-reported issue
- Known troubleshooting information
- Current classification
- Missing information
- Recommended next action

Case:

Customer cannot authenticate to an application. Password previously worked but is now rejected. Two password resets have already been attempted. General Internet access works. Application name and exact error message have not yet been provided.
```

The resulting summary should communicate:

```text
Customer reports inability to authenticate to an application. Password previously worked but is currently rejected despite two password-reset attempts. General Internet connectivity is available.

Classification: Identity & Access / Application Authentication

Priority: Medium

Root cause has not been established.

Next action: Obtain the application name and exact authentication error, confirm MFA status, verify account status through the authorized identity-management process, and determine whether the issue affects only this user or multiple users.
```

**Evidence:**

```text

<img width="1143" height="600" alt="image" src="https://github.com/user-attachments/assets/f93e22db-30f3-426e-b08e-59e3b39be56a" />


---

# 14. Add the Validated Summary to HubSpot

Add an internal ticket note:

```text
AI-assisted analysis was used to support ticket classification and summarization.

The customer reports application authentication failure despite two password-reset attempts. General Internet connectivity is available.

Current classification: Identity & Access / Application Authentication.

Root cause has not been established.

Additional authentication and application information is required before further action or escalation.
```

---

# 15. Simulated Investigation

This is where we maintain technical honesty.

We do **not** have access to:

* The customer's identity platform
* The application's backend
* The customer's actual account
* Production authentication logs

Therefore, we do not pretend to perform an account unlock or application-side repair.

Document:

```text
The investigation could not establish a definitive technical root cause because the laboratory environment does not provide access to the customer's identity platform or application backend.

The case was therefore documented as requiring additional information and appropriate escalation.
```

---

# 16. AI Hallucination Test

Create a second AI test.

Give the AI only:

```text
The customer cannot log into the application.
```

Ask:

```text
What is the root cause?
```

The purpose is to determine whether the AI recognizes insufficient evidence.

If the AI suggests:

```text
Account locked
Incorrect password
MFA failure
Application outage
```

those are **hypotheses**, not confirmed causes.

The analyst conclusion should be:

```text
The AI suggested possible causes, but the available evidence was insufficient to establish a definitive root cause.

Unsupported conclusions were rejected.

The case remains in an investigation state pending additional evidence.
```

**Evidence:**

```text

<img width="343" height="474" alt="image" src="https://github.com/user-attachments/assets/f1feb482-810f-4e6c-aebf-5b995f0270ef" />


---

# 17. Privacy Validation

Before completing the project, verify:

```text
[✓] Fictional customer
[✓] No real email address
[✓] No password
[✓] No authentication token
[✓] No MFA code
[✓] No account number
[✓] No employee ID
[✓] No internal credentials
[✓] No confidential company information
[✓] AI received anonymized information
```

**Evidence:**

```text
<img width="750" height="241" alt="image" src="https://github.com/user-attachments/assets/7b2a738d-6a9b-4ceb-9b0a-9643c53c7592" />

---

# 18. Final HubSpot Ticket

The completed ticket should contain:

```text
Case ID:
CRM-2026-001

Subject:
Application Login Failure — Customer Unable to Authenticate

Customer:
Daniel Morgan

Category:
Identity & Access

Subcategory:
Application Authentication

Priority:
Medium

Channel:
Email

Status:
In Progress

Known Symptoms:
Application authentication failure
Password previously worked
Two password-reset attempts
General Internet access available

Root Cause:
Not determined

AI Assistance:
Used for classification, troubleshooting planning,
and CRM summarization

Human Validation:
Completed

Next Action:
Obtain application name, exact authentication error,
MFA status, account status, and issue scope.

Escalation:
Identity/Application Support if required.

Customer Data:
Fictional/anonymized.
```

**Evidence:**

```text
13-final-hubspot-ticket.png
```

---

# 19. Close the Laboratory Case

Because we did **not** actually fix the fictional customer's authentication problem, do not falsely claim that the technical issue was resolved.

For the portfolio, close the exercise as:

```text
Status:
Closed
```

Add an internal note:

```text
Laboratory exercise completed.

The underlying customer authentication issue was not technically resolved because the laboratory environment does not provide access to the customer's identity platform or application backend.

The case was successfully classified, documented, analyzed with AI assistance, validated by the support analyst, and prepared for appropriate escalation.
```

**Evidence:**

```text
<img width="687" height="513" alt="image" src="https://github.com/user-attachments/assets/c2320903-063e-40b9-8857-ffd7de29dfdb" />

<img width="688" height="582" alt="image" src="https://github.com/user-attachments/assets/6f608bd2-69ae-4f23-83b7-f3b321234a5f" />


---

# 20. Final Investigation Results

The fictional customer case was created and managed within HubSpot CRM.

The ticket was classified as **Identity & Access / Application Authentication** with **Medium** priority.

AI was used to assist with case classification, troubleshooting planning, and CRM summarization.

AI-generated output was reviewed by the support analyst before being incorporated into the CRM workflow.

The available information was insufficient to establish a definitive root cause.

Potential causes included account status, MFA, identity-provider authentication, application-side authentication, or browser/session issues.

No customer credentials or sensitive information were entered into the AI assistant.

The underlying authentication problem was not technically resolved because the laboratory environment does not provide access to the production identity platform or application backend.

The exercise demonstrated the complete CRM case-management workflow from customer contact through classification, AI assistance, human validation, documentation, and closure.

---

# 21. Root Cause

**Not determined.**

There is insufficient evidence to establish whether the problem originated from the customer's account, authentication service, MFA, application, or browser/session.

---

# 22. Resolution

No technical change was performed.

The case was classified and documented for appropriate follow-up.

The recommended next action is to obtain:

* Application name
* Exact authentication error
* MFA status
* Account status
* Issue scope
* Application/browser information

---

# 23. Verification

The following were successfully demonstrated:

* HubSpot contact creation
* HubSpot ticket creation
* Ticket classification
* Priority assignment
* Customer interaction documentation
* AI-assisted classification
* AI-assisted troubleshooting
* AI-generated CRM summary
* Human validation of AI output
* AI hallucination testing
* Data anonymization
* Privacy validation
* Escalation criteria
* Case documentation
* Ticket closure

---

# 24. Final Ticket Notes

```text
CRM-2026-001

Customer reported inability to authenticate to an application. Customer stated that the password previously worked but is currently rejected despite two password-reset attempts. General Internet access is available.

Case classified as Identity & Access / Application Authentication with Medium priority.

AI assistance was used to support case classification, troubleshooting planning, and case summarization. AI output was reviewed and validated by the support analyst before being incorporated into the CRM record.

No real customer credentials or personally identifiable information were provided to the AI assistant.

Root cause was not established because insufficient technical information was available.

Recommended next action is to obtain the application name, exact authentication error, MFA status, account status, and issue scope before performing additional troubleshooting or escalation.

Status: Closed — Lab Exercise Completed.

Note: The underlying authentication issue was not technically resolved in the laboratory environment.
```

---

# 25. GitHub Evidence Structure

Use this structure:

```text
technical-support-portfolio/
│
└── 09-CRM-AI/
    │
    ├── README.md
    │
    └── troubleshooting-cases/
        │
        └── 001-hubspot-application-login/
            │
            ├── README.md
            │
            └── evidence/
                │
                ├── 01-hubspot-contact.png
                ├── 02-hubspot-ticket.png
                ├── 03-ticket-classification.png
                ├── 04-data-protection.png
                ├── 05-ai-classification.png
                ├── 06-ai-human-validation.png
                ├── 07-ticket-classification.png
                ├── 08-ai-troubleshooting-plan.png
                ├── 09-human-validated-troubleshooting.png
                ├── 10-ai-crm-summary.png
                ├── 11-ai-hallucination-test.png
                ├── 12-privacy-validation.png
                ├── 13-final-hubspot-ticket.png
                └── 14-closed-ticket.png
```

---

# 26. README — Project Description

Use this for the individual project README:

```text
CRM + AI Incident 001 — HubSpot Application Login Failure

## Overview

Hands-on HubSpot CRM laboratory demonstrating customer-support ticket management, application authentication troubleshooting, AI-assisted case classification, AI-assisted troubleshooting, human validation, data anonymization, and CRM documentation.

## Scenario

A fictional customer reported that they could no longer authenticate to an application. The customer's password had previously worked, but authentication attempts were being rejected despite two password-reset attempts.

General Internet connectivity was available.

## Tools

- HubSpot CRM
- ChatGPT / AI assistant
- Windows workstation
- GitHub

## Workflow

Customer Contact
→ CRM Ticket
→ Manual Assessment
→ AI Classification
→ Human Validation
→ Troubleshooting Plan
→ CRM Documentation
→ AI Summary
→ Privacy Validation
→ Case Closure

## Classification

Category: Identity & Access

Subcategory: Application Authentication

Priority: Medium

## Root Cause

Not determined.

The available evidence was insufficient to establish a definitive technical root cause.

## AI Usage

AI was used to assist with:

- Ticket classification
- Troubleshooting planning
- Case summarization
- Identification of missing information

AI-generated output was manually reviewed before being incorporated into the CRM workflow.

## Security

No real customer information, passwords, authentication tokens, MFA codes, or confidential company information were used.

All customer information was fictional and anonymized.

## Key Lesson

AI can improve support productivity, but AI-generated recommendations must be validated by a human analyst before they become technical conclusions or customer-facing actions.

## Disclaimer

This is a simulated laboratory project created for professional portfolio purposes. It does not represent professional use of HubSpot for a real employer or customer.
```

---

# 27. Skills Demonstrated

This project demonstrates:

* HubSpot CRM
* CRM ticket management
* Customer Service
* Technical Support
* Identity & Access
* Application troubleshooting
* Ticket classification
* Priority management
* AI-assisted support
* Prompt engineering
* AI output validation
* AI hallucination awareness
* Human-in-the-loop AI
* Data anonymization
* Customer-data protection
* Case summarization
* Troubleshooting documentation
* Escalation logic
* Case lifecycle management
* Knowledge documentation

---

# 28. How to Describe It in an Interview

Be completely transparent:

> “I built a hands-on HubSpot CRM laboratory project where I created fictional customer contacts and support tickets, classified an application authentication issue, used AI to assist with case classification and troubleshooting, and then manually validated the AI output before documenting it in the CRM. I also included a hallucination test and data-protection controls to demonstrate that I understand the limitations of AI in customer support.”

If they ask:

**“Did you use HubSpot professionally?”**

Answer:

> “Not professionally yet. I used HubSpot hands-on as part of a technical-support portfolio project to gain practical CRM and ticket-management experience.”

That answer is much stronger than pretending you used it at a previous employer.

---

## Final project flow

```text
FICTIONAL CUSTOMER
       │
       ▼
HUBSPOT CONTACT
       │
       ▼
SUPPORT TICKET
       │
       ▼
MANUAL ASSESSMENT
       │
       ▼
AI CLASSIFICATION
       │
       ▼
HUMAN VALIDATION
       │
       ▼
TROUBLESHOOTING PLAN
       │
       ▼
CRM DOCUMENTATION
       │
       ▼
AI SUMMARY
       │
       ▼
PRIVACY VALIDATION
       │
       ▼
ROOT CAUSE: NOT DETERMINED
       │
       ▼
CLOSED — LAB EXERCISE COMPLETED
```

This is the version I would use for your portfolio because it demonstrates **actual HubSpot usage + CRM case management + tech**




