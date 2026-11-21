# SPL Queries – Failed Login and Successful Login Investigation

## 1. Search Failed and Successful Authentication Events

```spl
index=main ("Failed password" OR "Accepted password")
```

**Purpose:** Identify SSH authentication failures and successful logins.

---

## 2. Authentication Timeline

```spl
index=main ("Failed password" OR "Accepted password")
| rex "from (?<src_ip>\d{1,3}(?:\.\d{1,3}){3})"
| rex "(Failed password|Accepted password) for (invalid user )?(?<username>\S+)"
| eval auth_status=if(match(_raw,"Failed password"),"FAILED","SUCCESS")
| table _time src_ip username auth_status _raw
| sort _time
```

**Purpose:** Build a chronological timeline of failed and successful authentication events.

---

## 3. Source IP Analysis

```spl
index=main ("Failed password" OR "Accepted password")
| rex "from (?<src_ip>\d{1,3}(?:\.\d{1,3}){3})"
| stats count by src_ip
| sort -count
```

**Purpose:** Identify IP addresses generating authentication events.

---

## 4. Username Analysis

```spl
index=main ("Failed password" OR "Accepted password")
| rex "(Failed password|Accepted password) for (invalid user )?(?<username>\S+)"
| stats count by username
| sort -count
```

**Purpose:** Identify usernames associated with authentication attempts.

---

## 5. Failed Login Count by Source IP

```spl
index=main "Failed password"
| rex "from (?<src_ip>\d{1,3}(?:\.\d{1,3}){3})"
| stats count as failed_attempts by src_ip
| sort -failed_attempts
```

**Purpose:** Count failed authentication attempts by source IP.

---

## 6. Failed Logins Followed by Successful Authentication — Investigative Filter

```spl
index=main ("Failed password" OR "Accepted password")
| rex "from (?<src_ip>\d{1,3}(?:\.\d{1,3}){3})"
| rex "(Failed password|Accepted password) for (invalid user )?(?<username>\S+)"
| eval auth_status=if(match(_raw,"Failed password"),"FAILED","SUCCESS")
| stats
    count(eval(auth_status="FAILED")) as failed_attempts
    count(eval(auth_status="SUCCESS")) as successful_logins
    min(_time) as first_seen
    max(_time) as last_seen
    by src_ip username
| where failed_attempts >= 3 AND successful_logins >= 1
| convert ctime(first_seen) ctime(last_seen)
| sort -failed_attempts
```

**Purpose:** Identify source IP and username combinations with three or more failures and at least one success during the selected time range.

**Limitation:** This query does not guarantee that the success occurred after the failures. Verify event order using the timeline query. This is an investigative query, not a production-ready chronological detection.

---

## Investigation Notes

Authentication events should be correlated with other available telemetry before declaring an account compromised.

A successful login following repeated failures may be suspicious, but could also be caused by a legitimate user repeatedly entering an incorrect password.

Additional investigation should include source reputation, account ownership, successful login time, process activity, network connections, and actions performed after authentication.

---

## Disclaimer

All queries were created and tested for educational purposes in a controlled home lab.
