# Suspicious DNS Activity Investigation & Incident Response

## Project Overview
This project demonstrates a beginner-level Security Operations Center (SOC) investigation using Wireshark and Kali Linux. The goal was to generate controlled DNS query activity, capture the network traffic, and investigate repeated DNS requests.

## Objectives
- Generate controlled DNS queries in a lab environment.
- Capture DNS traffic using Wireshark.
- Identify repeated queries with changing subdomain names.
- Analyze DNS requests and responses.
- Document findings and recommend SOC investigation steps.

## Tools Used
- Kali Linux
- Wireshark
- `nslookup`
- DNS
- UDP port 53

## Investigation Process
1. Generated DNS lookup requests for test subdomains under `example.com`.
2. Captured network traffic using Wireshark.
3. Applied the display filter `dns.qry.name contains "test-"`.
4. Examined DNS query names, source and destination IP addresses, record types, and responses.
5. Saved the packet capture and screenshot as evidence.
6. Prepared an investigation report with observations and recommended response actions.

## Key Observations
- Repeated DNS queries used changing subdomain names.
- The Kali Linux machine sent DNS requests to its configured resolver.
- Both A (IPv4) and AAAA (IPv6) queries were observed.
- Some responses contained zero answer records.

## Security Analysis
Repeated DNS queries with changing subdomain names can be a reason for further investigation in a real environment. Similar patterns may occur in DNS tunneling or command-and-control activity, but they are not proof of malicious behavior by themselves.

The traffic in this project was intentionally generated for learning purposes. No real malware or confirmed attack was identified.

## Evidence
- `evidence/suspicious-dns-test.pcapng` — packet capture for further analysis.
- `evidence/dns-query-pattern.png` — screenshot of the observed DNS query pattern.
- `reports/investigation-report.md` — investigation findings and recommended SOC response steps.

## Recommended SOC Response
- Preserve the original packet capture.
- Investigate the endpoint and process that generated the DNS queries.
- Review query frequency, domain patterns, and DNS responses.
- Correlate network findings with endpoint and security logs.
- Use threat-intelligence sources when investigating genuine suspicious domains.
- Escalate only when supporting evidence justifies it.

## Conclusion
This lab demonstrates basic DNS traffic capture, investigation, evidence preservation, and incident documentation. The observed pattern was simulated for educational purposes, and malicious activity was not confirmed.

**Disclaimer:** This project is for educational purposes only. All testing was performed in a controlled lab environment.
