# Wireshark_analysis_SYNflood_attack
Network Security Incident Analysis | SYN Flood &amp; IP Spoofing > Technical analysis of a denial-of-service (DoS) incident using network traffic inspection with Wireshark. Includes root cause diagnosis and mitigation strategies such as SYN Cookies and firewall filtering.
# Incident Analysis: SYN Flood & IP Spoofing Attack

This repository documents the technical analysis and resolution of a cybersecurity incident that impacted the availability of a corporate web server.

## Scenario Overview
An automated monitoring alert was triggered due to a **Connection Timeout** error on the company's web server (`192.0.2.1`). Initial investigation revealed that the server was overwhelmed by an unusual volume of TCP traffic, preventing legitimate users and employees from accessing sales promotions.

## Technical Diagnosis
After inspecting network logs using Wireshark, a **SYN Flood** attack was identified. The attacker exploited the TCP protocol mechanics as follows:

1. **Massive SYN Requests**: The source flooded the destination with connection requests.
2. **Half-Open Connections**: The server responded with `SYN-ACK`, but the attacker never sent the final `ACK`. This left connections "half-open," consuming the server's memory resources.
3. **Resource Exhaustion**: The server's backlog reached capacity, leading to `HTTP 504 Gateway Time-out` errors and `[RST, ACK]` reset packets as the server struggled to protect itself.



## Mitigation & Response
To restore service and harden the infrastructure, the following actions were taken:
* **IP Blocking**: Identified and blocked the persistent attacking IP `203.0.113.0` in the firewall once the initial spoofing ceased.
* **Firewall Rate Limiting**: Configured limits on the number of simultaneous "half-open" connections allowed.
* **SYN Cookies**: Recommended enabling SYN Cookies to validate connections without pre-allocating memory resources.

## Repository Files
* [Cybersecurity_incident_report.docx](./Cybersecurity%20incident%20report.docx) - Detailed diagnosis and remediation plan.
* [Wireshark_TCP_HTTP_log.pdf](./Wireshark%20TCP_HTTP%20log%20-%20TCP%20log.pdf) - The packet capture analyzed during the incident.
* [How_to_read_Wireshark_log.pdf](./How%20to%20read%20a%20Wireshark%20TCP_HTTP%20log.pdf) - Technical reference for interpreting TCP flags.
---
*This project is part of my cybersecurity analysis portfolio, demonstrating skills in incident response and network traffic analysis.*
