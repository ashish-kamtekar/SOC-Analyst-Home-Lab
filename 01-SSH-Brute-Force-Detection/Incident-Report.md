# Incident Report: SSH Brute Force Detection

## 1. Incident Overview

**Incident Name:** SSH Brute Force Detection  
**Incident Type:** Suspicious Authentication Activity  
**Severity:** Medium (Lab Classification)  
**Status:** Investigated  
**SIEM Tool:** Splunk  
**Log Source:** Linux Authentication Logs  
**Environment:** Controlled Home Lab

---

## 2. Objective

The objective of this investigation was to identify repeated SSH authentication failures, analyze the source IP address, identify targeted usernames, and understand how a SOC analyst investigates potential brute-force activity.

---

## 3. Lab Environment

| System | Role | Technology |
|---|---|---|
| Machine 1 | Attacker / Log Generator | Kali Linux |
| Machine 2 | Target | Kali Linux |
| Machine 3 | SIEM | Splunk |

---

## 4. Detection Details

Multiple failed SSH authentication attempts were generated against the target Linux machine in a controlled lab environment.

The authentication logs were collected and forwarded to Splunk for investigation.

The following indicators were analyzed:

- Repeated failed authentication attempts
- Source IP address
- Targeted username
- Number of failed login attempts
- Authentication activity during the selected time range

---

## 5. Investigation Process

The investigation was performed using Splunk Search & Reporting.

### Step 1: Identify Failed SSH Logins

Searched Splunk for failed SSH authentication events.

### Step 2: Identify Source IP

Extracted the source IP address associated with the failed authentication attempts.

### Step 3: Analyze Attempt Count

Counted failed authentication attempts from each source IP to identify repeated activity.

### Step 4: Identify Targeted Username

Analyzed usernames associated with failed authentication attempts.

### Step 5: Assess the Activity

Reviewed the authentication events to determine whether the activity was consistent with password-guessing or brute-force behavior.

---

## 6. Findings

- Multiple failed SSH authentication attempts were observed.
- The source IP address responsible for the attempts was identified.
- Targeted usernames were analyzed.
- The activity was consistent with SSH password-guessing behavior within the lab.
- No production systems were involved in this exercise.

Repeated failed authentication attempts alone do not confirm successful account compromise.

---

## 7. Recommended Response

If similar activity were detected in a production environment, the SOC analyst should:

1. Validate the alert and confirm the affected system.
2. Identify the source IP and targeted account.
3. Check whether a successful login occurred after the failed attempts.
4. Review the account's activity for suspicious actions.
5. Monitor the source IP for additional attempts.
6. Escalate suspected compromise according to the incident response procedure.
7. Apply blocking or account security measures only when authorized.

---

## 8. MITRE ATT&CK Mapping

| Technique | ID | Description |
|---|---|---|
| Brute Force | T1110 | Attempting to gain access by guessing credentials |
| Password Guessing | T1110.001 | Repeatedly attempting passwords against an account |

---

## 9. Tools Used

- Kali Linux
- Splunk Enterprise
- Splunk Universal Forwarder
- SSH
- Linux Authentication Logs
- SPL (Search Processing Language)

---

## 10. Conclusion

This lab demonstrated how repeated SSH authentication failures can be detected and investigated using Splunk.

The investigation involved analyzing authentication logs, identifying source IP addresses, counting failed login attempts, and evaluating suspicious login behavior.

This exercise helped develop practical skills in log analysis, SIEM investigation, detection logic, and basic SOC alert triage.

---

## Disclaimer

This investigation was conducted in a controlled virtual lab environment for educational purposes only. All activities were performed against systems owned and managed for testing.
