# Network Forensics Lab

## Overview

Analysis of a PCAP file using Wireshark to investigate suspicious activity 
on a compromised web server. Lab completed through CyberDefenders.

| Tool | Purpose |
|------|---------|
| Wireshark | Network traffic analysis and packet inspection |
| PCAP File | Captured network traffic from compromised web server |

---

## Objectives

- Identify and profile IP addresses within the PCAP file to determine 
traffic patterns and anomalies.
- Detect initial access, execution methods, and reverse shell communication.
- Trace the attack chain to uncover the threat actor's objective and 
exfiltrated data.

---

## Scenario

A suspicious file was identified on a company's web server within the 
corporate intranet, triggering a network traffic capture for analysis. 
Using Wireshark, the PCAP file was examined to identify anomalies, 
trace attacker behavior, and document indicators of compromise.

---

## Investigation

**Step 1 — IP Address Identification**

Two IP addresses were identified within the PCAP file. A geo-lookup 
confirmed that the external IPv4 address 117.x.x.x originated from 
a geo-blocked region, establishing it as the likely attacker machine.

<img width="1298" height="714" alt="image" src="https://github.com/user-attachments/assets/26eabe08-e042-4ca8-b3b7-ef4c502e42c1" />

**Step 2 — Anomalous Traffic Detection**

Further analysis revealed a PHP file upload followed by a netcat 
connection to port 8080, indicating remote code execution and 
reverse shell establishment by the attacker.

<img width="774" height="172" alt="image" src="https://github.com/user-attachments/assets/255eb759-5c73-4f00-a90b-33a84c53f45c" />

**Step 3 — HTTP POST Activity Analysis**

Filtering for HTTP POST requests exposed active communication from 
the attacker machine. Following the TCP stream confirmed the attack 
path and revealed the commands being executed on the compromised server.

POST Activity:
<img width="1008" height="156" alt="image" src="https://github.com/user-attachments/assets/497d9daf-8439-462b-b9f5-df7ec10dffe5" />

TCP Stream:
<img width="975" height="725" alt="image" src="https://github.com/user-attachments/assets/ac405867-1923-470c-b85b-be62905bcbbc" />

**Step 4 — Credential Exfiltration**

A curl command was identified within the TCP stream, used to extract 
a sensitive password file from the compromised web server confirming 
data exfiltration as the threat actor's primary objective.

Curl Command:
<img width="975" height="1259" alt="image" src="https://github.com/user-attachments/assets/99a367f6-6e7b-4723-92fb-b8ec0b6f6049" />

---

## Findings & Recommendations

| Finding | Detail |
|---------|--------|
| Initial Access | Remote code execution via PHP file upload from geo-blocked IP |
| Persistence | Reverse shell established via netcat on port 8080 |
| Exfiltration | Password file extracted using curl command via HTTP POST |

**Recommended Detection Improvements:**
- Implement geo-blocking rules to restrict traffic from high-risk regions
- Alert on outbound netcat connections and unexpected port 8080 activity
- Monitor for curl commands executing against sensitive file paths
- Create SIEM detection rules for PHP file uploads on web servers

---

## Skills Demonstrated

`Network Forensics` `PCAP Analysis` `Wireshark` `Threat Detection` 
`Incident Response` `IOC Documentation` `Attack Chain Analysis`
