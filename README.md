# Wazuh SIEM Windows Monitoring Lab

## Overview

This project demonstrates the deployment of a `Wazuh SIEM` environment to monitor, detect, and track security events originating from a Windows endpoint. The lab simulates a credential `brute-force` attack against a Windows 11 virtual machine and uses Wazuh's default detection rules to monitor failed logons and trigger high-severity alert escalations.

## Lab Architecture & Environment

**SIEM Manager**: Ubuntu Server (hosted on VMware Workstation) running Wazuh Manager.
**Endpoint Agent**: Windows 11 Virtual Machine running the Wazuh Agent.
**Hypervisor**: VMware Workstation.

## Project Objectives

Deploy and configure a centralized Wazuh SIEM server on Ubuntu.

Install, register, and verify the Wazuh agent on a Windows 11 endpoint.

Simulate an authentic security incident (Windows account brute-force / failed logons via Event ID 4625).

Verify log ingestion, dashboard visibility, and default rule escalation logic (Level 5 baseline to Level 10 high severity).

## Implementation Steps & Methodology

1. **Environment Deployment**

Wazuh Manager Setup: Deployed an Ubuntu Server VM, updated system packages, and installed the Wazuh central components.

Agent Enrollment: Downloaded and installed the Wazuh agent on the Windows 11 VM, configuring it to communicate securely with the Ubuntu Manager via the manager IP address. Verified active agent status in the Wazuh web dashboard.

2. **Attack Simulation**

To generate realistic telemetry for Windows authentication failures, a simulated brute-force attack was performed on the Windows 11 endpoint:

Utilized the command prompt (cmd) and the runas utility to intentionally execute commands with invalid credentials repeatedly.

This generated a burst of Windows Security Event logs corresponding to Event ID 4625 (An account failed to log on).

3. **Log Ingestion & Rule Escalation**

**Baseline Detection** (Level 5): The Wazuh agent captured the Windows Security event logs and forwarded them to the manager, triggering Wazuh's default low-to-medium severity alerts (Level 5) for individual failed logon attempts.

**Rule Escalation** (Level 10): As the frequency and volume of Event ID 4625 occurrences increased within the configured time window, Wazuh's built-in correlation rules automatically escalated the activity to Level 10 (High Severity), flagging it as a potential brute-force attack.

## Evidence & Screenshots

Can be found in the `screenshots` folder.
