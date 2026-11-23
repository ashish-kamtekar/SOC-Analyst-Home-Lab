# Incident Report – Port Scan Detection

## Incident Overview

| Field | Details |
|---|---|
| Incident Name | Port Scan Detection |
| Incident Type | Network Reconnaissance |
| Severity | Medium – Lab Classification |
| Status | Investigated |
| Environment | Controlled SOC Home Lab |
| Tools | Nmap, tcpdump, Wireshark, Splunk |

## Summary

During lab testing, network connection attempts were generated from a scanning machine against a target machine.

Network traffic was captured and analyzed to identify the source IP, destination IP, targeted ports, and connection patterns.

The connection data was analyzed in Splunk to identify the source responsible for generating multiple connection attempts.

## Indicators Observed

- Multiple connection attempts from a single source.
- Connections directed toward multiple destination ports.
- Rejected connection attempts.
- Network reconnaissance behavior.

## Investigation

1. Identified the scanning source IP.
2. Identified the target IP.
3. Reviewed the network connection activity.
4. Analyzed packet traffic.
5. Identified the targeted ports.
6. Reviewed connection counts using Splunk.
7. Used SPL to identify sources targeting multiple ports.

## Findings

The activity demonstrated a pattern consistent with network port scanning.

Port scanning is commonly used during reconnaissance to identify accessible services and potential attack surfaces.

No successful exploitation was established through this investigation alone.

## Recommended Response

- Verify whether the scan was authorized.
- Identify the source system and its owner.
- Review firewall and endpoint logs.
- Investigate any subsequent suspicious activity.
- Block the source IP if malicious activity is confirmed and blocking is authorized.
- Continue monitoring the target system.

## Conclusion

The practical demonstrated how a SOC analyst can investigate network reconnaissance activity using packet capture, traffic analysis, and SIEM queries.

The investigation highlights the importance of identifying suspicious connection patterns before further attack activity occurs.
