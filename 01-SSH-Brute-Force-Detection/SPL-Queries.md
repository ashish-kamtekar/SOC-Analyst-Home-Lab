# SPL Queries – SSH Brute Force Detection

This document contains the Splunk Search Processing Language (SPL) queries used during my SSH brute-force detection lab.

The objective is to analyze Linux authentication logs, identify repeated failed login attempts, extract source IP addresses, and identify targeted usernames.

---

## 1. Search for Failed SSH Login Attempts

### Objective
Identify failed SSH authentication attempts collected from Linux authentication logs.

### SPL Query

```spl
index=main "Failed password"
```

### Analysis
This query searches the `main` index for events containing the phrase `Failed password`, which is commonly found in Linux SSH authentication failure logs.

---

## 2. Identify Source IP Addresses

### Objective
Extract source IP addresses and count the failed login attempts originating from each IP.

### SPL Query

```spl
index=main "Failed password"
| rex "from (?<src_ip>\d{1,3}(?:\.\d{1,3}){3})"
| stats count by src_ip
| sort -count
```

### Analysis
- `rex` extracts the source IP address from the authentication event.
- `stats count by src_ip` counts the events associated with each IP.
- `sort -count` sorts the results in descending order.

---

## 3. Identify Targeted Usernames

### Objective
Identify usernames targeted during failed SSH authentication attempts.

### SPL Query

```spl
index=main "Failed password"
| rex "Failed password for (invalid user )?(?<username>\S+)"
| stats count by username
| sort -count
```

### Analysis
- `rex` extracts the username from the authentication log.
- `stats count by username` counts the attempts against each username.
- This helps identify accounts receiving repeated authentication attempts.

---

## 4. Detect IP Addresses with 5 or More Failed Attempts

### Objective
Identify source IP addresses associated with five or more failed authentication attempts within the selected search time range.

### SPL Query

```spl
index=main "Failed password"
| rex "from (?<src_ip>\d{1,3}(?:\.\d{1,3}){3})"
| stats count as failed_attempts by src_ip
| where failed_attempts >= 5
| sort -failed_attempts
```

### Analysis
- Extracts source IP addresses.
- Counts failed authentication attempts for each source.
- Filters IP addresses with five or more failed attempts.
- Sorts the results by attempt count.

**Note:** The threshold of five attempts is used for this lab demonstration. This query counts events within the selected Splunk time range. It does not independently enforce a five-minute detection window.

---

## 5. SOC Analyst Investigation

After identifying suspicious authentication activity, a SOC analyst should:

1. Identify the source IP address.
2. Identify the targeted username.
3. Review the number and timing of failed login attempts.
4. Check for successful logins following the failed attempts.
5. Review other activities associated with the source IP and account.
6. Determine whether the activity is suspicious or legitimate.
7. Escalate potential compromise according to the incident response procedure.

---

## 6. Detection Limitations

- Five failed attempts alone do not confirm a brute-force attack.
- Legitimate users may occasionally fail authentication multiple times.
- This query does not automatically correlate failed logins with successful logins.
- The detection threshold depends on the selected time range.
- In a production environment, time-based correlation, baselines, alert tuning, and additional investigation would be required.

---

## 7. Learning Outcomes

Through these SPL queries, I practiced:

- Searching Linux authentication events in Splunk.
- Extracting fields using `rex`.
- Identifying source IP addresses.
- Analyzing targeted usernames.
- Counting authentication failures.
- Filtering suspicious activity using thresholds.
- Performing basic SIEM investigation and alert triage.

---

## Disclaimer

These queries were developed and tested in a controlled home lab for educational purposes. They are intended for learning basic SIEM detection and investigation techniques.
