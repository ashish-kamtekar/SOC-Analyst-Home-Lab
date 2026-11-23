# Project 03 – Port Scan Detection & Investigation

## Overview
This project demonstrates the identification and investigation of network reconnaissance activity using Kali Linux, Nmap, tcpdump, Wireshark, and Splunk.

A controlled port scan was performed against a lab target to generate network connection activity. The captured traffic was analyzed to identify the source IP, target IP, attempted ports, and connection patterns.

## Objective
- Understand network reconnaissance activity.
- Identify potential port scanning.
- Analyze source and destination IP addresses.
- Identify targeted ports.
- Investigate connection attempts using Splunk.
- Understand how SOC analysts investigate suspicious network activity.

## Lab Environment

- Kali Linux – Scanner
- Kali Linux – Target
- Splunk – SIEM
- Nmap – Network scanning
- tcpdump – Packet capture
- Wireshark – Packet analysis

## Investigation Workflow

1. Identified the target IP address.
2. Generated controlled port scan activity.
3. Captured network traffic using tcpdump.
4. Analyzed packet activity using Wireshark.
5. Imported structured connection data into Splunk.
6. Analyzed source IPs and targeted ports.
7. Created SPL queries to identify potential scanning activity.
8. Documented investigation findings.

## Detection Logic

The detection identifies source IP addresses attempting connections to multiple unique destination ports.

A high number of unique destination ports within a short timeframe may indicate network reconnaissance.

## Key Skills

- Network traffic analysis
- Port scan investigation
- TCP fundamentals
- Nmap
- tcpdump
- Wireshark
- Splunk
- SPL
- Source IP investigation
- SOC investigation methodology

## Disclaimer

All testing was conducted within a controlled lab environment using systems owned or authorized for testing.
