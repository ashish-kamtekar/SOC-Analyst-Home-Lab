# Incident Report – Failed Login Followed by Successful Login

## 1. Incident Overview

**Incident Name:** Failed Login Followed by Successful Authentication  
**Incident Type:** Suspicious Authentication Activity  
**Severity:** Medium – Lab Classification  
**Status:** Investigated  
**SIEM:** Splunk  
**Log Source:** Linux SSH Authentication Logs  
**Environment:** Controlled Home Lab

## 2. Incident Summary

Multiple failed SSH authentication attempts followed by a successful login were generated and investigated in a controlled lab environment.

The objective was to analyze the authentication sequence and understand how this pattern may indicate potential password guessing or account compromise.

## 3. Lab Environment

| System | Role |
|---|---|
| Kali Linux 1 | Source / Attacker Simulation |
| Kali Linux 2 | Target |
| Splunk | SIEM |

## 4. Investigation

The investigation was performed using Linux authentication logs collected in Splunk.

The following activities were performed:

- Searched for failed and successful SSH authentication events.
- Identified the source IP address.
- Identified the targeted username.
- Counted failed authentication attempts.
- Reviewed authentication events chronologically.
- Investigated the failed-login-to-success pattern.

## 5. Findings

The lab activity demonstrated multiple failed authentication attempts followed by a successful login.

This pattern is consistent with suspicious authentication activity and may indicate password guessing.

However, the authentication sequence alone does not prove unauthorized access or account compromise.

## 6. Security Risk

If observed in a production environment, this activity could indicate:

- Password guessing.
- SSH brute-force attempts.
- Unauthorized access attempts.
- Potential account compromise.

The risk would depend on the account's privileges, source IP, timing, and activity following authentication.

## 7. Recommended Response

- Validate the alert using authentication logs.
- Identify the source IP and targeted account.
- Confirm the chronological sequence of failed and successful authentication.
- Review subsequent user activity.
- Investigate suspicious commands, processes, network connections, and privilege changes.
- Escalate suspected compromise according to incident response procedures.
- Apply containment actions only when authorized.

## 8. Severity Assessment

**Assigned Severity: Medium (Lab Classification)**

The activity was classified as medium because repeated authentication failures followed by a successful login warrant investigation.

Account compromise was not confirmed, and post-login malicious activity was not established during this exercise.

## 9. Conclusion

This investigation demonstrated how a SOC analyst can use Splunk to analyze SSH authentication events, identify repeated failures, investigate successful authentication, and build an event timeline.

It reinforced the importance of correlating authentication events and validating suspicious activity before declaring an incident confirmed.

## 10. MITRE ATT&CK Mapping

| Technique | ID | Relevance |
|---|---|---|
| Brute Force | T1110 | Repeated attempts to obtain access using guessed credentials |
| Password Guessing | T1110.001 | Repeated password attempts against an account |

These techniques are relevant to the simulated activity. The lab does not establish that an actual attacker compromised the system.

## 11. Tools Used

- Kali Linux
- Splunk Enterprise
- Splunk Universal Forwarder
- SSH
- Linux Authentication Logs
- SPL

## 12. Disclaimer

This investigation was conducted in a controlled home lab using virtual machines for educational purposes only. No production systems were involved.
