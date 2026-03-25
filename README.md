# Network-Forensics-Lab

## Overview:
The goal of this lab is to analyze a PCAP file using Wireshark and identify suspicious activity on a compromised web server. Lab done through CyberDefenders.

### Objectives:
- Identify the IP addresses in the PCAP file and determine traffic patterns.
- Detect initial access, execution, and reverse shell communication.
- Uncover what the threat actor was after.

| Tool                                         | Purpose        |
|-----------------------------------------------|----------------------------|
| Wireshark | Analyze the network traffic |
| PCAP File | File used |

### Scenario:
A suspicious file was identified on a companies web server within the intranet. This caused for concern and determination to scan the network traffic to prepare a PCAP file. From there, the use of Wireshark allowed for the examination of the network traffic to identify any anomolies.

<img width="1298" height="714" alt="image" src="https://github.com/user-attachments/assets/26eabe08-e042-4ca8-b3b7-ef4c502e42c1" />

Able to identify two IP addresses. Using a web search, I can see that the IPv4 address 117.x.x.x is located in an area that is geo blocked.

<img width="774" height="172" alt="image" src="https://github.com/user-attachments/assets/255eb759-5c73-4f00-a90b-33a84c53f45c" />

Scanning the details, I find POST activity coming from the attacker machine. From there I follow the TCP stream to determine the path.

POST Activity:
<img width="1008" height="156" alt="image" src="https://github.com/user-attachments/assets/497d9daf-8439-462b-b9f5-df7ec10dffe5" />

TCP Stream:
<img width="975" height="725" alt="image" src="https://github.com/user-attachments/assets/ac405867-1923-470c-b85b-be62905bcbbc" />

Curl command:
<img width="975" height="1259" alt="image" src="https://github.com/user-attachments/assets/99a367f6-6e7b-4723-92fb-b8ec0b6f6049" />

### Conclusions Found:
- See that there is a PHP file uploaded followed by a netcat connection to port 8080.
- Followed by a CURL command to extract a password file.
- Using this information helps to enhance an incident response plan and action.

