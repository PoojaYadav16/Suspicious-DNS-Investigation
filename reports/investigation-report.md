# Suspicious DNS Activity Investigation & Incident Response

## 1. Project Overview

Objective: Generate controlled DNS test traffic, capture it with Wireshark, and investigate the observed DNS query pattern using a SOC-style workflow.

Environment: Kali Linux running in a VMware virtual machine.

Tools: Wireshark, `nslookup`, Kali Linux terminal.

## 2. Lab Details

- Source IP: `192.168.6.128`
- DNS resolver: `192.168.6.2`
- DNS protocol port: `53`
- Test domain: `example.com`
- Traffic type: Controlled, simulated DNS activity

## 3. Test Activity

The following command generated repeated DNS lookup attempts with changing subdomain names:

`for i in $(seq 1 20); do nslookup "test-$i.example.com" 192.168.6.2; sleep 1; done`

The test generated names such as `test-1.example.com`, `test-2.example.com`, and subsequent numbered names.

## 4. Evidence Collection

- Captured network traffic on interface `eth0` using Wireshark.
- Applied the display filter `dns.qry.name contains "test-"`.
- Observed DNS queries and corresponding responses.
- Identified A queries for IPv4 addresses and AAAA queries for IPv6 addresses.
- Saved a packet capture and a screenshot of the DNS traffic pattern.

## 5. Observations

- Multiple DNS queries used changing test subdomain names.
- The queries were sent from `192.168.6.128` to DNS resolver `192.168.6.2`.
- Some inspected responses had reply code `No error (0)` but contained zero answer records.
- A and AAAA queries were observed.
- The displayed packet count varied according to the active display filter and capture contents.

## 6. Security Analysis

Repeated DNS queries with unusual or changing subdomain names can be a reason for further investigation. Some malware uses DNS tunneling or DNS for command-and-control communication.

However, this lab traffic was generated intentionally by the analyst. The use of changing names alone does not confirm DNS tunneling, malware, or a security incident.

The test domain is reserved for documentation, and the observed traffic is simulated test activity rather than evidence of a real compromise.

## 7. Recommended SOC Response

1. Preserve the original packet capture and screenshots.
2. Identify the source host and the process responsible for DNS requests.
3. Review query frequency, domain patterns, response codes, and record types.
4. Enrich suspicious domains using approved threat-intelligence sources when investigating real incidents.
5. Correlate DNS events with endpoint logs and other network evidence.
6. Escalate and contain a host only when additional evidence supports a real threat.
7. Document the findings and clearly distinguish confirmed facts from assumptions.

## 8. Conclusion

This project demonstrates a basic SOC investigation workflow: generating controlled test traffic, capturing DNS packets, filtering relevant events, inspecting query and response details, preserving evidence, and documenting findings.

Final assessment: Simulated DNS pattern observed. Malicious activity was not confirmed.
