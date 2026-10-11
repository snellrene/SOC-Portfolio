# Failed Login Investigation

## Overview

This project demonstrates the detection and investigation of Windows authentication failures using Wazuh SIEM. The objective was to generate failed login attempts on a monitored Windows 11 endpoint, analyse the resulting alerts, and document the investigation process from a SOC analyst perspective.

## Objectives

- Generate failed authentication events
- Detect Windows security events using Wazuh
- Investigate Event ID 4625 alerts
- Assess security impact
- Document findings and recommendations

## Lab Environment

### SIEM Platform
- Wazuh 4.8.2

### Endpoint
- Windows 11
- Agent Name: SOC-WIN11

### Detection Method
- Windows Security Logs
- Wazuh Agent
- Wazuh Manager

## Lab Architecture

```text
Windows 11 Endpoint (SOC-WIN11)
            │
            │ Wazuh Agent
            ▼
Wazuh Manager
            │
            ▼
Wazuh Dashboard
            │
            ▼
Security Alert Investigation
```

## Scenario

Multiple failed login attempts were intentionally generated on the Windows endpoint to simulate suspicious authentication activity. The Wazuh agent collected the security events and forwarded them to the Wazuh Manager, where security alerts were generated for investigation.

## Alert Summary

| Field | Value |
|---------|---------|
| Alert Count | 4 |
| Rule ID | 60122 |
| Severity | Level 5 |
| Endpoint | SOC-WIN11 |
| Alert Type | Authentication Failure |

### Alert Description

```text
Logon failure - Unknown user or bad password
```

## Investigation Process

### Step 1 – Generate Failed Login Attempts

Multiple incorrect passwords were entered on the Windows endpoint.

### Step 2 – Review Security Alerts

Opened the Wazuh Dashboard and navigated to:

```text
Threat Hunting
```

Reviewed authentication-related alerts.

### Step 3 – Analyse Alert Data

Reviewed:

- Alert description
- Timestamp
- Rule ID
- Severity
- Endpoint information

### Step 4 – Determine Impact

Confirmed that the activity was generated during authorised lab testing.

No evidence of account compromise was identified.

## Findings

Wazuh successfully detected and recorded multiple authentication failures.

The failed login attempts generated Rule ID 60122 alerts and were assigned a Severity Level of 5.

The alerts originated from the monitored endpoint SOC-WIN11.

No successful logins were observed following the failed authentication attempts.

## Risk Assessment

### Severity

Medium (Level 5)

### Potential Impact

- Password guessing attacks
- Brute-force attempts
- Credential stuffing attacks
- Unauthorised access attempts

### Likelihood

Low

The activity was generated intentionally during testing.

## MITRE ATT&CK Mapping

| Technique | Description |
|------------|------------|
| T1078 | Valid Accounts |
| T1531 | Account Access Related Activity |

## Recommendations

- Monitor repeated authentication failures.
- Implement account lockout policies.
- Enforce multi-factor authentication.
- Investigate failed logins from unfamiliar systems or locations.
- Review authentication logs regularly.

## Skills Demonstrated

### SOC Skills

- SIEM Monitoring
- Security Alert Analysis
- Authentication Failure Investigation
- Incident Triage
- Windows Security Event Analysis

### Security Skills

- Threat Detection
- Log Analysis
- MITRE ATT&CK Mapping
- Security Monitoring

### Documentation Skills

- Incident Reporting
- Evidence Collection
- Risk Assessment
- Security Recommendations

## Screenshots

### Dashboard Overview

Screenshots


