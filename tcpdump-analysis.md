# TCPDump Analysis

## Objective

The objective of this analysis is to investigate why users were unable to access the website **www.yummyrecipesforme.com** by examining the network traffic captured with `tcpdump`.

---

## Scenario

Users reported receiving the error message:

> Destination Port Unreachable

A packet capture was performed to identify where the communication failed.

---

## Packet Analysis

### Step 1 — DNS Request

The client sent a DNS query to resolve the domain name.

Example:

```text
192.51.100.15 > 203.0.113.2.domain: UDP
```

**Analysis**

- Source IP: `192.51.100.15`
- Destination IP: `203.0.113.2`
- Protocol: UDP
- Destination Port: 53 (DNS)

This indicates that the client attempted to contact the DNS server to obtain the IP address of the requested website.

---

### Step 2 — ICMP Response

The DNS server responded with the following error:

```text
ICMP
udp port 53 unreachable
```

**Analysis**

The ICMP message indicates that the destination host could not deliver the packet because UDP port **53** was unreachable.

Possible reasons include:

- DNS service stopped
- Firewall blocking UDP port 53
- DNS server misconfiguration

---

### Step 3 — Impact

Since the DNS query failed, the browser could not resolve the domain name.

Without an IP address, the HTTPS connection could never be established.

```
Browser
        │
        ▼
DNS Query (UDP 53)
        │
        ▼
ICMP Port Unreachable
        │
        ▼
No DNS Resolution
        │
        ▼
Website Unavailable
```

---

## Protocols Identified

| Protocol | Purpose |
|----------|---------|
| UDP | Transported the DNS request |
| DNS | Domain name resolution |
| ICMP | Returned the network error message |

---

## Root Cause

Based on the packet capture, the failure occurred during the DNS resolution process.

The ICMP message **"UDP port 53 unreachable"** strongly suggests that the DNS service was unavailable or inaccessible.

---

## Conclusion

The tcpdump analysis shows that the communication failed before any HTTPS connection was established.

The DNS server could not process requests on UDP port 53, preventing the client from resolving the domain name and accessing the website.
