# Failed Login Followed by Successful Login Investigation

## Project Overview

This project demonstrates the investigation of repeated SSH authentication failures followed by a successful login using Splunk SIEM.

The objective was to analyze authentication events, identify the source IP and targeted username, correlate failed and successful authentication activity, and understand how a SOC analyst investigates potential account compromise.

## Scenario

Multiple failed SSH authentication attempts were followed by a successful login.

This behavior can indicate password guessing or potential account compromise. However, repeated authentication failures followed by a successful login do not automatically confirm malicious activity.

## Lab Architecture

| Machine | Role |
|---|---|
| Kali Linux 1 | Source / Attacker Simulation |
| Kali Linux 2 | Target System |
| Splunk | SIEM and Log Analysis |

## Tools Used

- Kali Linux
- Splunk Enterprise
- Splunk Universal Forwarder
- SSH
- Linux Authentication Logs
- SPL

## Investigation Objectives

- Identify failed SSH authentication attempts.
- Identify successful authentication events.
- Extract source IP addresses.
- Identify targeted usernames.
- Analyze authentication event timelines.
- Correlate failed and successful login activity.
- Assess the possibility of account compromise.

## Investigation Process

1. Generated failed SSH authentication attempts.
2. Performed a successful SSH login in the controlled lab.
3. Monitored authentication logs on the target machine.
4. Investigated events in Splunk.
5. Extracted source IP addresses and usernames.
6. Reviewed the chronological authentication sequence.
7. Evaluated the suspicious activity.
8. Documented investigation findings and recommended actions.

## Detection Logic

The investigation focused on identifying authentication activity involving:

- Three or more failed login attempts.
- At least one successful login.
- The same source IP address.
- The same targeted username.

This logic was used as an investigative filter in the lab and is not a production-ready detection rule.

## Investigation Findings

The lab generated multiple failed SSH authentication attempts followed by a successful login.

This activity demonstrated a suspicious authentication pattern that requires further investigation.

Authentication events alone cannot confirm whether the successful login was malicious.

## Recommended SOC Response

- Validate the authentication events.
- Identify the source IP and account.
- Review the authentication timeline.
- Investigate activity following successful login.
- Check for privilege escalation or suspicious processes.
- Escalate suspected compromise.
- Apply containment actions according to organizational procedures.

## Learning Outcomes

- Authentication log analysis.
- Splunk event investigation.
- SPL field extraction.
- Source IP investigation.
- Username analysis.
- Event timeline creation.
- Failed and successful authentication correlation.
- Basic SOC alert triage.
- Incident assessment and escalation.

## Disclaimer

This project was conducted in a controlled home lab using personally managed virtual machines for educational purposes. No production systems were involved.
