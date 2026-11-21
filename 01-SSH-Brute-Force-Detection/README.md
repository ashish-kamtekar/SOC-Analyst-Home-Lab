# SSH Brute Force Detection Using Splunk

## 1. Project Overview
This project demonstrates how to simulate SSH brute-force login attempts in a controlled lab environment and investigate suspicious authentication activity using Splunk SIEM.

The objective is to identify repeated failed SSH login attempts, analyze the source IP address, identify the targeted username, and understand how a SOC analyst investigates potential brute-force attacks.

## 2. Lab Environment

| Machine | Role | Operating System |
|---|---|---|
| Machine 1 | Attacker / Log Generator | Kali Linux |
| Machine 2 | Target Machine | Kali Linux |
| Machine 3 | SIEM / Log Analysis | Splunk |

## 3. Tools Used
- Kali Linux
- Splunk Enterprise
- Splunk Universal Forwarder
- SSH
- Linux Authentication Logs
- SPL (Search Processing Language)

## 4. Attack Simulation

Multiple SSH authentication attempts were generated from the attacker machine against the target machine using a test account in the controlled lab environment.

The target machine recorded failed authentication attempts in its SSH authentication logs.

The authentication logs were forwarded to Splunk for centralized monitoring and investigation.

## 5. Log Source

**Log File:** `/var/log/auth.log`

**Log Type:** Linux SSH Authentication Logs

**Events Investigated:**
- Failed SSH login attempts
- Targeted usernames
- Source IP addresses
- Repeated authentication failures

## 6. Splunk Investigation

### Search for Failed SSH Login Attempts

```spl
index=main "Failed password"
```

### Identify Source IP and Count Failed Attempts

```spl
index=main "Failed password"
| rex "from (?<src_ip>\d{1,3}(?:\.\d{1,3}){3})"
| stats count by src_ip
| sort -count
```

### Identify Targeted Usernames

```spl
index=main "Failed password"
| rex "Failed password for (invalid user )?(?<username>\S+)"
| stats count by username
| sort -count
```

### Detect Sources with 5 or More Failed Attempts

```spl
index=main "Failed password"
| rex "from (?<src_ip>\d{1,3}(?:\.\d{1,3}){3})"
| stats count as failed_attempts by src_ip
| where failed_attempts >= 5
| sort -failed_attempts
```

**Note:** The threshold of 5 failed attempts was used for this lab demonstration. In a production environment, detection thresholds should consider the time window, baseline activity, and organization's security policies.

## 7. Investigation Process

As a SOC analyst, I would:

1. Review the number of failed login attempts.
2. Identify the source IP address.
3. Identify the targeted username.
4. Check whether a successful login occurred after the failed attempts.
5. Review additional activity from the source IP.
6. Determine whether the activity is suspicious or legitimate.
7. Escalate the incident if potential account compromise is identified.

## 8. Possible Security Risks

Repeated failed SSH authentication attempts may indicate:

- SSH brute-force activity
- Password guessing
- Attempts to access unauthorized accounts
- Potential account compromise if authentication succeeds

Repeated failures alone do not confirm a successful compromise.

## 9. Recommended Response

Depending on investigation findings and organizational procedures:

- Monitor the source IP for further suspicious activity.
- Review authentication history for the targeted account.
- Check for successful logins following failed attempts.
- Escalate confirmed or suspected compromise to the appropriate security team.
- Apply IP blocking, account restrictions, or password resets only when authorized.

## 10. Learning Outcomes

Through this lab, I practiced:

- Understanding SSH authentication logs.
- Generating and analyzing failed login events.
- Forwarding Linux authentication logs to Splunk.
- Writing SPL queries.
- Extracting source IP addresses and usernames.
- Identifying repeated authentication failures.
- Performing basic SOC alert investigation and triage.

## 11. Disclaimer

This lab was performed in a controlled environment using my own virtual machines for educational and cybersecurity learning purposes only.
