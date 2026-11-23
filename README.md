# SOC Analyst Home Lab

## About This Repository

This repository contains my hands-on cybersecurity labs and SOC Analyst practice projects. I am building practical experience in security monitoring, SIEM investigation, log analysis, threat detection, and incident response.

My primary focus is understanding how a Level 1 SOC Analyst investigates suspicious activity, validates security alerts, analyzes logs, and escalates potential incidents.

## Tools & Technologies

- Splunk SIEM
- Kali Linux
- Linux Authentication Logs
- SSH
- SPL (Splunk Search Processing Language)
- VMware Workstation
- Networking Fundamentals

## Lab Environment

My home lab consists of:

- Kali Linux – Attack Simulation
- Kali Linux – Target Machine and Log Generation
- Splunk – Security Log Monitoring and Investigation

## Practical Labs

### 01. SSH Brute-Force Detection Using Splunk

- Simulated SSH authentication failures in a controlled lab environment.
- Monitored Linux authentication logs.
- Forwarded authentication events to Splunk.
- Identified repeated failed login attempts.
- Extracted source IP addresses.
- Investigated suspicious authentication activity using SPL.

**Skills:** SIEM Monitoring, Log Analysis, SPL, SSH Authentication, Incident Investigation

## Upcoming Labs

- Failed Logins Followed by Successful Authentication
- Port Scan Detection
- Linux Suspicious Activity Investigation
- Windows Security Event Analysis
- IOC Investigation and Threat Intelligence
- Security Incident Reporting

## Disclaimer

All practical activities documented in this repository are performed in my own isolated lab environment for educational purposes.


## Completed Projects

### 1. SSH Brute Force Detection Using Splunk
- Simulated SSH authentication failures in a controlled lab.
- Forwarded Linux authentication logs to Splunk.
- Investigated failed login attempts using SPL.
- Identified source IP addresses and repeated authentication failures.

[View Project](./01-SSH-Brute-Force-Detection/)



### 2. Failed Login Followed by Successful Login Investigation

- Investigated repeated SSH authentication failures followed by successful authentication.
- Analyzed source IP addresses and targeted usernames.
- Built authentication timelines using Splunk.
- Correlated failed and successful login events using SPL.
- Evaluated potential account compromise and documented SOC response recommendations.

[View Project](./02-Failed-Login-Success-Investigation/)



### 3. Port Scan Detection & Investigation

- Generated controlled port scanning activity against a lab target using Nmap.
- Captured network traffic using tcpdump.
- Analyzed TCP connection attempts and packets using Wireshark.
- Identified source IPs, destination IPs, and targeted ports.
- Analyzed connection activity using Splunk.
- Created SPL queries to identify potential port scanning patterns.

[View Project](./03-Port-Scan-Detection/)
