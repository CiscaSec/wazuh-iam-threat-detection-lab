# wazuh-iam-threat-detection-lab
Hands-on IAM threat detection lab using Wazuh and Windows Security event logs.
# Wazuh IAM Threat Detection Lab

## Overview

This project extends my home cybersecurity lab to explore **Identity and Access Management (IAM) threat detection** using Wazuh and Windows Security event logs.

The objective was to monitor Windows authentication activity, detect failed logon attempts, and identify changes to local user accounts through security events collected from a Windows 11 endpoint.

## Lab Environment

- **SIEM:** Wazuh
- **Endpoint:** Windows 11
- **Wazuh Manager:** Ubuntu Linux virtual machine
- **Log Source:** Windows Security Event Logs
- **Virtualization:** VMware Workstation

This project builds on my existing Wazuh lab, which also includes Sysmon, File Integrity Monitoring (FIM), VirusTotal integration, and Atomic Red Team testing.

## Detection Scenarios

| Event ID | Activity | Result |
|---|---|---|
| 4624 | Successful logon | Observed in Wazuh |
| 4625 | Failed logon | Detected by Wazuh |
| 4720 | Local user account created | Observed in Wazuh |
| 4732 | Member added to a security-enabled local group | Not yet validated |
| 4738 | User account changed | Not yet validated |

## Key Findings

### 1. Failed Logon Detection — Event ID 4625

Generated a failed logon event on the Windows 11 endpoint and searched for it in Wazuh.

Wazuh generated the alert **"Logon Failure - Unknown user or bad password"**.

- **Rule ID:** 60122
- **Severity level:** 5
- **Purpose:** Identify failed authentication attempts that may warrant further investigation.

Repeated failed logons can indicate password guessing or brute-force activity. A single failure does not establish malicious activity.

### 2. Successful Logon Monitoring — Event ID 4624

Confirmed that successful Windows logon events were visible in Wazuh.

Monitoring successful authentication alongside failures can help analysts investigate authentication patterns and identify potentially suspicious activity.

### 3. Local User Account Creation — Event ID 4720

Created a test local user account in the Windows lab and confirmed that the corresponding account-creation event was visible in Wazuh.

Unexpected account creation can indicate unauthorized account provisioning or persistence, depending on the surrounding evidence.

## Investigation Approach

For each validated scenario, I:

1. Generated or identified the relevant Windows security event.
2. Searched for the event in Wazuh Threat Hunting.
3. Reviewed the event details and associated alert information.
4. Recorded the observed result and identified scenarios requiring further validation.

## Skills Demonstrated

- Wazuh SIEM monitoring and event investigation
- Windows Security Event Log analysis
- Authentication monitoring
- IAM-related security event analysis
- Local account activity monitoring
- Security alert triage and documentation
- Hands-on virtual lab development

## Limitations and Next Steps

This is a controlled home lab, not a production environment. The validated scenarios demonstrate event collection and investigation; they do not establish that every IAM-related attack can be detected.

Planned improvements include:

- Validate local group membership changes (Event ID 4732).
- Validate user account modification events (Event ID 4738).
- Investigate repeated failed logons and suspicious authentication patterns.
- Explore custom Wazuh rules and correlation logic.
- Document additional test cases and their detection results.

## Repository Evidence

Screenshots documenting validated detection scenarios will be available in the `screenshots/` directory.

## Disclaimer

All testing was conducted in an isolated, authorized home lab using test accounts and virtual machines. This project is intended for cybersecurity learning and defensive security research.
