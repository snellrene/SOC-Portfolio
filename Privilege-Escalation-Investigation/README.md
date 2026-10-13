# Privilege Escalation Investigation

## Overview
This project demonstrates the detection and investigation of a privilege escalation scenario using Wazuh SIEM.
The objective was to create a local user account, add that account to the local Administrators group, analyse the resulting security alerts, and assess the potential security impact.

## Objectives
- Generate a privilege escalation event
- Detect account manipulation activity
- Detect administrator group modifications
- Investigate alerts using Wazuh SIEM
- Perform risk assessment
- Document findings and recommendations

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
```

## Scenario

A new local user account was created and subsequently granted administrative privileges.
This simulated a privilege escalation attack path commonly used by threat actors to obtain elevated access within a compromised environment.

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

## Skills Demonstrated

### SOC Skills

- SIEM Monitoring
- Alert Triage
- Threat Detection
- Incident Investigation
- Event Correlation
- MITRE ATT&CK Mapping

### Security Skills

- Privilege Escalation Detection
- Windows Security Monitoring
- Identity and Access Management
- Risk Assessment
- Security Reporting

## Evidence

### User Creation Event

<img width="706" height="635" alt="Test user creation" src="https://github.com/user-attachments/assets/e4e651de-3b56-4f97-bdc3-a7568d5ea887" />

### User Added To Administrators Group

<img width="891" height="298" alt="Test user administrator confirm" src="https://github.com/user-attachments/assets/3f8e0574-eeac-4ddd-8c6c-f35addcd3c06" />

### Wazuh Alert - Rule 60154

<img width="1909" height="897" alt="Wazuh-Threat-Hunting" src="https://github.com/user-attachments/assets/c335c474-745c-48f0-bbea-8be4d7858978" />

## Lessons Learned
Privilege escalation activity generates multiple security events rather than a single alert.
By correlating account creation, account modification and privileged group membership changes, a SOC analyst can identify suspicious privilege escalation behaviour and assess its potential impact.
Monitoring privileged group changes is a critical detection capability because elevated privileges are a common objective for attackers.

### Wazuh Report

[wazuh-alert-report.pdf](https://github.com/user-attachments/files/33360652/wazuh-alert-report.pdf)

