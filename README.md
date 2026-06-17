**Splunk Enterprise Tier 1 SOC 20 Security Event Monitoring Lab**

**Overview**

This lab was designed to simulate the daily responsibilities of a Tier 1 Security Operations Center (SOC) Analyst using Splunk Enterprise. The project consists of twenty security event datasets representing common enterprise security telemetry sources, including authentication logs, firewall events, web server activity, DNS queries, VPN access logs, Windows security events, endpoint security alerts, and network traffic data.

To create a realistic SOC environment, all datasets were custom-generated using Python scripts. The Python-based log generator was used to produce structured security events that simulate real-world enterprise activity and common security monitoring scenarios. Generating the datasets programmatically provided complete control over the event content while ensuring that each dataset contained sufficient data for meaningful Splunk analysis and investigation.

After generating the datasets, each log file was ingested into Splunk Enterprise and assigned to its appropriate index based on the security domain it represented. The datasets were then analyzed using Splunk Search Processing Language (SPL) to perform statistical investigations and event analysis.

The primary objective of this lab is to develop practical experience with log ingestion, indexing, event monitoring, and statistical analysis using Splunk Enterprise. Unlike dashboard-focused projects, this lab intentionally emphasizes raw event analysis and SPL-based investigations. No dashboards, visualizations, panels, reports, alerts, lookups, or correlation searches were used. Instead, the focus remained on understanding security events, identifying patterns and trends, and developing the search and analysis skills commonly used by Tier 1 SOC analysts during daily monitoring and triage activities.

For example, the Failed Login Attempts dataset was ingested into the authentication index and analyzed using SPL to count failed password attempts by source IP address and user account. Similar statistical investigations were performed across all twenty security event datasets, allowing the analyst to practice working with multiple security data sources commonly found in enterprise environments.\
\
**\
Security Event Categories**

This lab covers the following twenty security monitoring scenarios:

1.  Failed Login Attempts

2.  Successful Logins

3.  Top Source IP Addresses

4.  Top Destination IP Addresses

5.  Firewall Blocked Traffic

6.  Firewall Allowed Traffic

7.  HTTP 404 Errors

8.  HTTP 500 Errors

9.  DNS Query Monitoring

10. VPN Login Activity

11. After-Hours Login Detection

12. New User Account Creation

13. User Account Lockouts

14. Disabled Account Usage

15. Antivirus Detections

16. Top Talkers by Bandwidth

17. Critical Security Events

18. Most Active Hosts

19. Login Failures by User

20. Event Counts by Sourcetype

**Skills Practiced**

Throughout this lab, the following skills were developed and reinforced:

- Python log generation and dataset creation

- Security data engineering fundamentals

- Splunk Enterprise administration

- Log ingestion and indexing

- Search Processing Language (SPL)

- Statistical analysis using SPL commands

- Security event monitoring

- Authentication analysis

- Firewall traffic analysis

- DNS activity investigation

- VPN monitoring and access analysis

- Windows security event analysis

- Endpoint security monitoring

- Network traffic analysis

- Security operations workflows

- Event triage and investigation

- Threat detection fundamentals

- SOC Tier 1 analyst methodologies

- Security telemetry analysis

- Log source management and organization

**Outcome**

Upon completion of this lab, the analyst gained hands-on experience creating realistic security datasets using Python, ingesting multiple log sources into Splunk Enterprise, and performing statistical investigations using SPL. The project provided practical exposure to authentication monitoring, firewall analysis, web log investigation, DNS monitoring, VPN activity analysis, Windows security events, endpoint security alerts, and network traffic analysis.

By working directly with raw security events rather than dashboards or visualizations, the lab strengthened the analyst's ability to interpret log data, identify security-relevant activity, and perform the types of investigations commonly conducted within a Security Operations Center. The completed project serves as a foundational SOC monitoring portfolio piece and prepares the analyst for more advanced Tier 2 activities such as threat hunting, incident response, malware analysis, persistence detection, and adversary behavior investigations.\
\
**1. Python script file** (**generate_tier1_soc_datasets.py)**

**2. Terminal execution showing the datasets being created**

**3. The folder containing the 20 generated datasets**

**4. Splunk ingestion**\

**5. Splunk searches and results**




| **\#** | **Dataset File**           | **Splunk Index** |
|--------|----------------------------|------------------|
| 1      | Failed_logins.log          | auth             |
| 2      | successful_logins.log      | auth             |
| 3      | top_source_ips.log         | network          |
| 4      | top_destination_ips.log    | network          |
| 5      | firewall_blocked.log       | firewall         |
| 6      | Firewall_allowed.log       | Firewall         |
| 7      | http_404.log               | web              |
| 8      | http_500.log               | web              |
| 9      | dns_queries.log            | dns              |
| 10     | vpn_logins.log             | vpn              |
| 11     | after_hours_logins.log     | auth             |
| 12     | new_users.log              | windows          |
| 13     | account_lockouts.log       | windows          |
| 14     | disabled_account_usage.log | windows          |
| 15     | antivirus_detections.log   | endpoint         |
| 16     | bandwidth_top_talkers.log  | network          |
| 17     | critical_events.log        | security         |
| 18     | active_hosts.log           | security         |
| 19     | login_failures_by_user.log | auth             |
| 20     | sourcetype_count.log       | security         |


Please refer to images # 1, 2, and 3 in the repository.

**Note:** This repository contains one security event investigation from the Splunk Enterprise Tier 1 SOC 20 Security Event Monitoring Lab series. For the remaining security event investigations, please refer to the corresponding repositories in this project collection.

**Top Source IP Addresses Event**

Dataset: top_source_ips.log\
Index:network\
Sourcetype: top_source_ips

This dataset focuses on identifying the **most active source IP addresses** generating network traffic.

**SOC Objective**

Identify:

Most active source IPs\
Potential scanners\
Suspicious hosts\
High-volume traffic generators\
Systems requiring further investigation

Please refer to image # 4 in the repository.

**1. Confirm Dataset Ingestion**

index=network sourcetype=top_source_ips\
\| stats count by source index sourcetype

Purpose: Verify the dataset was ingested correctly.

Please refer to image # 5 in the repository.

**2. View Raw Events**

index=network sourcetype=top_source_ips\
\| table \_time src_ip dest_ip bytes

Purpose: Review the raw network communications.

Which IP initiated traffic?\
Traffic was initiated by several source IP addresses, including **123.123.123.123**, **10.0.0.20**, **10.0.0.15**, **192.168.1.50**, **10.0.0.10**, and **88.88.88.88**.\
\
Where was it sent?\
The traffic was sent to multiple destination IP addresses, including **192.168.1.10**, **192.168.1.20**, **172.16.1.5**, **45.33.32.156**, and **8.8.8.8**.\
\
How much data was transferred?\
Individual network events transferred varying amounts of data. In the displayed results, transferred data ranged from **474 bytes** to **8,231 bytes** per event.\
\
Network traffic was initiated by multiple source IP addresses and sent to several destination IP addresses. The observed source IPs included 123.123.123.123, 10.0.0.20, 10.0.0.15, 192.168.1.50, 10.0.0.10, and 88.88.88.88. Traffic was directed toward destination IPs such as 192.168.1.10, 192.168.1.20, 172.16.1.5, 45.33.32.156, and 8.8.8.8. The amount of data transferred varied between events, ranging from 474 bytes to 8,231 bytes in the displayed results.

Please refer to image # 6 and 7 in the repository.

**3. Top Source IP Addresses**

index=network sourcetype=top_source_ips\
\| stats count by src_ip\
\| sort -count

Purpose: Identify the most active source IPs.

Which **source IP addresses** are generating the most network events?\
\
The source IP addresses **10.0.0.20** and **192.168.1.50** generated the highest number of network events, with **12 events each**. They were followed by **88.88.88.88** with **10 events**, **10.0.0.10** and **10.0.0.15** with **9 events each**, and **123.123.123.123** with **8 events**.

Please refer to image # 8 in the repository.

**4. Total Bytes Sent by Source IP**

index=network sourcetype=top_source_ips\
\| stats sum(bytes) as total_bytes by src_ip\
\| sort -total_bytes

Purpose: Find which IP addresses or system transferred the most data.

Which IP addresses consumed the most bandwidth?\
\
The source IP address **88.88.88.88** consumed the most bandwidth, transferring a total of **52,249 bytes**. It was followed by **10.0.0.20** with **51,637 bytes**, **10.0.0.10** with **44,568 bytes**, **192.168.1.50** with **43,481 bytes**, **123.123.123.123** with **40,912 bytes**, and **10.0.0.15** with **39,500 bytes**.

Please refer to image # 9 in the repository.

**5. Source IP to Destination Mapping**

index=network sourcetype=top_source_ips\
\| stats count by src_ip dest_ip\
\| sort -count

Purpose: Identify communication relationships.\
\
Which source IP and destination IP pairs communicate most frequently?\
\
The most frequent communication pair was **10.0.0.20 → 8.8.8.8**, generating **6 network events**. The next most active pair was **88.88.88.88 → 192.168.1.10** with **5 events**, followed by **192.168.1.50 → 45.33.32.156** with **4 events**.

Please refer to image # 10 in the repository.

**6. Unique Destinations Per Source**

index=network sourcetype=top_source_ips\
\| stats dc(dest_ip) as unique_destinations by src_ip\
\| sort -unique_destinations

Purpose: Identify scanning behavior.

Is one source IP contacting many different destinations?

No. The source IP addresses displayed similar communication patterns. Five source IPs each contacted five unique destination IP addresses, while one source IP contacted four unique destinations. No single source IP demonstrated significantly higher destination diversity than the others.

Please refer to image # 11 in the repository.


**7. Average Bytes Per Source**

index=network sourcetype=top_source_ips\
\| stats avg(bytes) as average_bytes by src_ip\
\| sort -average_bytes

Purpose: Identify unusually large transfers.

Which IP addresses have the largest average traffic size (bytes)?\
\
The source IP address **88.88.88.88** had the largest average traffic size at **5,224.9 bytes per event**. It was followed by **123.123.123.123** with **5,114 bytes**, **10.0.0.10** with **4,952 bytes**, **10.0.0.15** with **4,388.89 bytes**, **10.0.0.20** with **4,303.08 bytes**, and **192.168.1.50** with **3,623.42 bytes**.\

Please refer to image # 12 in the repository.


**8. Top Talkers Summary**

index=network sourcetype=top_source_ips\
\| stats count sum(bytes) as total_bytes by src_ip\
\| sort -total_bytes

Purpose: Combine event volume and bandwidth.

Which source IPs are both active and transferring significant amounts of data?

The source IP addresses **88.88.88.88** and **10.0.0.20** were the most notable in the dataset. **88.88.88.88** generated **10 network events** and transferred **52,249 bytes**, while **10.0.0.20** generated **12 network events** and transferred **51,637 bytes**. These source IP addresses demonstrated both high activity and large data transfer volumes.

Please refer to image # 13 in the repository.

**9. Unique Destination Analysis**
\
index=network sourcetype=top_source_ips\
\| stats dc(dest_ip) as unique_destinations by src_ip\
\| where unique_destinations \>= 3\
\| sort -unique_destinations

Purpose: Identify source IP addresses that communicate with multiple destination IPs and understand network communication patterns.\
\
Which source IP addresses communicated with the greatest number of unique destination IP addresses?\
\
10.0.0.10, 10.0.0.15, 123.123.123.123, 192.168.1.50, and 88.88.88.88 communicated with the greatest number of unique destination IP addresses, with 5 destinations each**.**

\**
Five source IP addresses (10.0.0.10, 10.0.0.15, 123.123.123.123, 192.168.1.50, and 88.88.88.88) each communicated with 5 unique destination IP addresses. One source IP (10.0.0.20) communicated with 4 unique destination IP addresses. The communication patterns were relatively uniform across the dataset, and no source IP demonstrated unusually high destination diversity.

Please refer to image # 14 in the repository.

**10. Executive Summary**

index=network sourcetype=top_source_ips\
\| stats dc(src_ip) as unique_sources dc(dest_ip) as unique_destinations sum(bytes) as total_bytes count as total_connections

Purpose: Provide a high-level overview for reporting.


How many unique source IPs, unique destination IPs, total bytes transferred, and total network connections were observed?

| **Metric**                | **Value** |
|---------------------------|-----------|
| Unique Source IPs         | 6         |
| Unique Destination IPs    | 5         |
| Total Bytes Transferred   | 272,347   |
| Total Network Connections | 60        |

The dataset contains 6 unique source IP addresses communicating with 5 unique destination IP addresses. A total of 60 network connections were recorded, transferring 272,347 bytes of data.

Please refer to image # 15 in the repository.




