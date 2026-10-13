# Privilege Escalation Investigation

## Overview
This project demonstrates the detection, investigation, containment, and remediation of a privilege escalation event using Wazuh SIEM.

The objective was to simulate a common attacker technique by creating a local user account and granting administrative privileges. The resulting security events were detected by Wazuh, investigated through Threat Hunting, assessed for risk, and remediated using standard security response procedures.

## Objectives
- Generate a privilege escalation event
- Detect account manipulation activity
- Detect administrator group modifications
- Investigate alerts using Wazuh SIEM
- Perform risk assessment
- Document findings and recommendations
- Perform containment and remediation
- Document the incident lifecycle

## Lab Environment

### SIEM Platform
- Wazuh 4.8.2

### Endpoint
- Windows 11
- Agent Name: SOC-WIN11

### Detection Sources
- Windows Security Logs
- Wazuh Agent
- Wazuh Manager

## Lab Architecture

```text
SOC-WIN11
      │
      │ Wazuh Agent
      ▼
Wazuh Manager
      │
      ▼
Wazuh Dashboard
      │
      ▼
Privilege Escalation Detection
      │
      ▼
Threat Hunting & Investigation
```

## Scenario

A new local user account was created and subsequently granted administrative privileges.
This simulated a privilege escalation attack path where an attacker attempts to gain elevated permissions to perform administrative actions within an environment.

## Activity Performed

### Step 1 – Create New User using powershell

```powershell
net user test-user1 xxxxxxxxxxx /add
```

### Step 2 – Add User to Administrators Group

```powershell
net localgroup Administrators test-user1 /add
```
### Step 3 – Verify Membership

```powershell
net localgroup Administrators
```

Verification confirmed:

```text
test-user1
```
was successfully added to the local Administrators group.

## Detection Results

### User Account Events

| Rule ID | Description | Severity |
|----------|-------------|----------|
| 60109 | User account enabled or created | 8 |
| 60110 | User account changed | 8 |

### Group Membership Events

| Rule ID | Description | Severity |
|----------|-------------|----------|
| 60170 | Users group changed | 5 |
| 60154 | Administrators group changed | 12 |

## MITRE ATT&CK Mapping

| Technique | Description |
|------------|------------|
| T1098 | Account Manipulation |
| T1484 | Domain or Group Policy Modification |

## Investigation Process

### Alert Analysis

Wazuh generated several alerts related to account creation, account modification and group membership changes.
The most critical alert observed was:

```text
Administrators group changed
Rule ID: 60154
Severity: 12
MITRE Technique: T1484
```
PowerShell verification confirmed that the account had been successfully granted administrative privileges.

### Evidence Reviewed

- User account creation events
- User account modification events
- Users group modification events
- Administrators group modification events
- Local administrator membership verification

## Findings

The SIEM successfully detected the complete privilege escalation chain:

1. Local user account creation
2. User account modification
3. Users group modification
4. Administrators group modification

The account was successfully granted administrative privileges.
The highest severity alert generated was:

```text
Administrators group changed
Rule ID: 60154
Severity Level: 12
```

This activity would be considered high risk in a production environment because unnecessary administrative privileges could be used to:

- Disable security controls
- Install malicious software
- Create persistence mechanisms
- Access sensitive system resources
- Modify system configurations

## Risk Assessment

### Risk Level

High

### Impact

- Privilege Escalation
- Unauthorised Administration
- Persistence
- Security Control Bypass
- Increased Attack Surface

## Recommendations

- Monitor local administrator group changes.
- Review privileged account memberships regularly.
- Implement Privileged Access Management (PAM).
- Configure real-time alerts for privileged group modifications.
- Apply least privilege principles.
- Remove unnecessary local administrator accounts.

## Evidence

### User Creation Event

<img width="706" height="635" alt="Test user creation" src="https://github.com/user-attachments/assets/e4e651de-3b56-4f97-bdc3-a7568d5ea887" />

### User Added To Administrators Group

<img width="891" height="298" alt="Test user administrator confirm" src="https://github.com/user-attachments/assets/3f8e0574-eeac-4ddd-8c6c-f35addcd3c06" />

### Wazuh Alert - Rule 60154

<img width="1909" height="897" alt="Wazuh-Threat-Hunting" src="https://github.com/user-attachments/assets/c335c474-745c-48f0-bbea-8be4d7858978" />

### Wazuh Alert Report

[wazuh-alert-report.pdf](https://github.com/user-attachments/files/33360652/wazuh-alert-report.pdf)


### Containment Actions
Following detection, remediation actions were performed.

## Remove Administrative Privileges
net localgroup Administrators test-user1 /delete
Verification:

net localgroup Administrators
Confirmed the account was no longer a member of the Administrators group.

## Disable the Account
net user test-user1 /active:no
Verification:

net user test-user1

Confirmed:

Account active               No

<img width="767" height="772" alt="image" src="https://github.com/user-attachments/assets/b715d1e7-4680-4a6b-bda9-9df045280660" />

### Remediation Outcome
_Before Remediation_
- User account created
- User account modified
- User added to Administrators group
- Elevated privileges granted

_After Remediation_
- Administrative access removed
- Account disabled
- Privilege escalation contained

## Skills Demonstrated

### SOC Skills

- SIEM Monitoring
- Alert Triage
- Threat Detection
- Incident Investigation
- Event Correlation
- MITRE ATT&CK Mapping
- Incident Response

### Security Skills

- Privilege Escalation Detection
- Windows Security Monitoring
- Identity and Access Management
- Risk Assessment
- Security Reporting

## Lessons Learned
Privilege escalation activity generates multiple security events rather than a single alert.
By correlating account creation, account modification and privileged group membership changes, a SOC analyst can identify suspicious privilege escalation behaviour and assess its potential impact.
Monitoring privileged group changes is a critical detection capability because elevated privileges are a common objective for attackers.


