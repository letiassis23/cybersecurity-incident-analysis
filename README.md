# Cybersecurity Incident Analysis – DNS Failure Investigation

## Overview

This project documents the investigation of a network connectivity issue using packet analysis with **tcpdump**. The incident involved failed DNS requests caused by an unreachable UDP port 53, preventing users from accessing a website.

The analysis follows a structured incident response process, including traffic inspection, protocol identification, root cause analysis, and recommendations for remediation.

---

## Scenario

Users reported that they were unable to access the website **www.yummyrecipesforme.com** and received the error message **"Destination Port Unreachable."**

Network traffic was captured using **tcpdump** to determine the cause of the incident.

---

## Objectives

- Analyze captured network traffic.
- Identify the network protocols involved.
- Determine the source of the connectivity issue.
- Produce a cybersecurity incident report.
- Recommend possible remediation steps.

---

## Skills Demonstrated

- Network Traffic Analysis
- TCP/IP Fundamentals
- DNS Troubleshooting
- ICMP Error Analysis
- Packet Inspection
- Cybersecurity Incident Reporting
- Root Cause Analysis

---

## Tools Used

- tcpdump
- DNS
- UDP
- ICMP

---

## Repository Structure

```
.
├── README.md
├── incident-report.md
├── tcpdump-analysis.md
└── screenshots/
```

---

## Key Findings

- DNS requests were sent using UDP port 53.
- The DNS server returned ICMP **"UDP Port 53 Unreachable"** messages.
- The website could not be reached because the domain name could not be resolved into an IP address.
- The most likely cause was that the DNS service was unavailable, misconfigured, or blocked.
