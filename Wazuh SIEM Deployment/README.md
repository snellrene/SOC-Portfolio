# Wazuh SIEM Deployment Lab

## Overview

This project documents the deployment of a Security Information and Event Management (SIEM) platform using Wazuh on Ubuntu Server 24.04 LTS.

The goal of this lab was to build a Security Operations Centre (SOC) environment capable of collecting, monitoring, and analysing endpoint security events.

## Objectives

- Deploy Ubuntu Server 24.04 LTS in VirtualBox
- Install and configure Wazuh SIEM
- Configure network connectivity between the SIEM and endpoint
- Deploy a Windows 11 Wazuh Agent
- Validate communication between endpoint and manager
- Prepare the environment for security investigations and threat detection

## Lab Architecture

```text
Windows 11 Endpoint (SOC-WIN11)
            │
            │ Wazuh Agent
            ▼
Ubuntu Server 24.04 LTS
(Wazuh Manager, Indexer, Dashboard)
            │
            ▼
Wazuh Dashboard
```

## Technologies Used

- Wazuh 4.8.2
- Ubuntu Server 24.04 LTS
- Windows 11
- VirtualBox
- OpenSSH
- Linux CLI

## Environment Configuration

### Wazuh Server

| Component | Configuration |
|------------|------------|
| Hostname | wazuh-server |
| Operating System | Ubuntu Server 24.04.5 LTS |
| Memory | 4 GB |
| CPU | 2 vCPU |
| Disk | 60 GB |
| Network | Bridged Adapter |

### Endpoint

| Component | Configuration |
|------------|------------|
| Hostname | SOC-WIN11 |
| Operating System | Windows 11 |
| Agent Version | 4.8.2 |

## Deployment Process

### 1. Ubuntu Server Installation

- Created a dedicated Ubuntu Server 24.04 LTS virtual machine
- Configured CPU, memory and storage resources
- Enabled OpenSSH during installation
- Applied system updates

### 2. Wazuh Installation

Installed the following components using the official Wazuh installation script:

- Wazuh Manager
- Wazuh Indexer
- Wazuh Dashboard

### 3. Network Configuration

Changed VirtualBox network settings from NAT to Bridged Adapter to allow direct access to the Wazuh Dashboard from the host system.

### 4. Windows Agent Deployment

- Generated a Windows agent deployment package,
- Installed the Wazuh Agent on Windows 11,
- Connected the agent to the Wazuh Manager,
- Verified successful enrolment and communication

### Results:
Successfully deployed a fully functional SIEM environment.

Validated:
- Wazuh dashboard accessibility,
- Agent registration,
- Endpoint communication,
- Security event collection readiness

### Screenshots
<img width="944" height="769" alt="Ubuntu   Wazuh installed" src="https://github.com/user-attachments/assets/c80610a7-c716-4338-aa51-e6d595ce3767" />

<img width="1659" height="1022" alt="Wazuh running" src="https://github.com/user-attachments/assets/6d3f7375-7fbc-4f3e-9d6c-89d8ea96eb9c" />

<img width="1909" height="742" alt="Agent Enrolled   connected" src="https://github.com/user-attachments/assets/33216713-908b-404b-a944-6b00fae72198" />





