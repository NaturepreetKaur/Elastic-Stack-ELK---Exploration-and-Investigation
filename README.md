# Elastic Stack (ELK)
## Overview
The Elastic Stack, commonly known as ELK, is a collection of tools used to collect, process, search, analyze, and visualize data and logs.
The stack consists of three main components:
        **Elasticsearch**– Stores, indexes, and searches data.
        **Logstash** – Collects and processes data from different sources.
        **Kibana** – Provides dashboards and visualizations for analyzing data.
## Log Exploration

Kibana Discover provides an interactive interface for searching and
analyzing data stored in Elasticsearch.
In this view, I explored collected log events, examined event fields,
filtered data, and used the timeline to understand activity over a
selected period.

This demonstrates how Kibana can turn raw log data into searchable
information that can support security monitoring and investigation.
<img width="1146" height="587" alt="elk1" src="https://github.com/user-attachments/assets/8dd914eb-3a2e-490e-b65e-1bcf704a627f" />
## VPN Connection Monitoring

This Kibana visualization demonstrates how network connection data can be explored over time. I used fields such as timestamp, action, company, and port to visualize VPN-related activity. From a SOC perspective, this type of visualization can help identify unusual connection patterns, failed attempts, and activity that may require further investigation.
<img width="1361" height="641" alt="elk2" src="https://github.com/user-attachments/assets/08613aa2-6a94-4e67-8fef-d0552adbffee" />
## Filtering VPN Activity by Source Country
Applied a geographic filter in Kibana to isolate VPN connection events originating from England.This filtering helps a SOC analyst narrow down large volumes of security telemetry and focus on a specific source for further investigation.

As a SOC Analyst;

1) Filtered vpn_connections data by Source Country: England
2) Analyzed VPN connection activity over time
3) Used event volume to identify activity patterns and potential anomalies
4) Provides a starting point for further correlation with source IPs, users, authentication events, and timestamps
<img width="1360" height="594" alt="elk3" src="https://github.com/user-attachments/assets/bcd39745-ce19-447b-a1b4-3ddd44c17e81" />

## Query-Based Event Filtering
Applied a structured query in Kibana to isolate VPN connection events associated with a specific source IP address and user account.

Query: sourceip: 238.163.231.224 AND UserName: "Suleman"
The query returned 46 matching events, providing a focused dataset for further analysis.

As a SOC Analyst;

1) Correlated source IP and user identity within VPN telemetry.
2) Examined the event timeline to identify connection patterns and frequency.
3) Reviewed associated attributes including action, port, protocol, and source country.
4) Reduced the investigation scope from broader VPN telemetry to username and sourceip specific activity.
5) Established a focused dataset for subsequent event correlation and investigation.
<img width="1351" height="527" alt="elk4" src="https://github.com/user-attachments/assets/aa2f0c8b-dc6f-440f-a150-1ba97090e8ac" />

## VPN Activity Analysis & User-Based Event Correlation
The Kibana visualization was configured to analyze VPN connection activity over time using a stacked bar chart.

Analysis performed;
- Visualized the number of VPN connection events across 12-hour time intervals.
- Broke down event volume by top usernames to identify which accounts generated the highest activity.
- Reviewed supporting telemetry fields including source IP, source country, action, protocol, and port.
- Used the visualization to establish a baseline of user activity and identify unusual spikes or changes in authentication/VPN activity.
- This view can support SOC triage by helping analysts pivot from overall event volume to specific user accounts and their associated network activity.

<img width="1366" height="592" alt="elk5" src="https://github.com/user-attachments/assets/e61f644c-55d3-4142-abf3-c449ccec66ff" />

## Protocol Distribution Analysis Using Kibana

Analyzed VPN connection telemetry indexed in Elasticsearch using Kibana aggregation and visualization capabilities.

- Aggregated events by `protocol` to establish a network activity baseline.
- Correlated protocol distribution with `username` using Top Values aggregation.
- Used record-count aggregation to quantify VPN connection activity.
- TCP represented approximately 79.99% of observed events in the dataset.
- Reviewed lower-volume protocol activity as a starting point for further event correlation and investigation.
<img width="1357" height="590" alt="6" src="https://github.com/user-attachments/assets/d636523f-86bd-494f-b8c5-1e53b38a857c" />

## Source IP–Based VPN Event Analysis
The visualization uses Kibana to isolate VPN connection events associated with a specific source IP while excluding an internal/private address.

Analysis Performed;

- Applied a source-country/source-IP filter to narrow the VPN telemetry.
- Excluded `172.20.10.191` from the dataset to reduce internal or non-relevant traffic.
- Focused analysis on source IP `69.208.133.98`.
- Visualized event count over 12-hour time intervals using a vertical bar chart.
- Observed sustained event activity across the selected time periods rather than a single isolated event.
- This provides a focused dataset for further investigation of the source IP across related fields such as `username`, `protocol`, `port`, `action`, and `timestamp`.

<img width="1361" height="541" alt="7" src="https://github.com/user-attachments/assets/60c998cc-fd9a-4d4a-bd58-b1254da4331a" />
