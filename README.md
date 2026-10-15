# Cybersecurity Threat Monitoring Dashboard

## Project Overview
This project demonstrates security monitoring and log analysis using Splunk Enterprise. I analyzed simulated Windows security events to identify failed login attempts, examine suspicious source IP addresses, and visualize authentication activity.

## Tools and Technologies
- Splunk Enterprise (SIEM)
- Search Processing Language (SPL)
- Windows Security Event Logs (simulated)
- GitHub

## Security Investigation
I uploaded a CSV dataset containing 10 simulated Windows authentication events into Splunk.

**Findings:**
- Total authentication events: 10
- Failed login attempts: 6
- Successful logins: 4
- Highest number of failed logins: 5 from IP address `203.0.113.25`
- Windows Event ID 4625 was used to identify failed authentication attempts.

The repeated failures from one IP address demonstrate a pattern worth investigating for possible brute-force activity. These simulated events do not independently establish a real attack.

## Splunk Queries

**Failed Login Attempts by IP**
```spl
index=cybersecurity_lab EventCode=4625
| stats count as Failed_Attempts by Source_IP
| sort - Failed_Attempts
```

**Successful vs Failed Logins**
```spl
index=cybersecurity_lab
| stats count by Status
```

**Failed Login Attempts Over Time**
```spl
index=cybersecurity_lab EventCode=4625
| timechart span=1m count as Failed_Attempts
```

## Dashboard Visualizations
The dashboard includes:
1. Failed Login Attempts by IP — Bar Chart
2. Successful vs Failed Logins — Pie Chart
3. Failed Login Attempts Over Time — Line Chart

![Cybersecurity Threat Monitoring Dashboard](Cybersecurity-%20Threat-%20Monitoring.png)

## Skills Demonstrated
- Security event monitoring
- SIEM log ingestion and analysis
- SPL query development
- Authentication failure investigation
- Security dashboard creation
- Identifying suspicious login patterns

## Conclusion
This hands-on project strengthened my understanding of how security analysts use Splunk to investigate authentication events, identify potentially suspicious activity, and communicate findings through dashboards.

## How to Reproduce This Project

1. Download `windows_security_lab.csv` from this repository.
2. Open Splunk Enterprise.
3. Navigate to Settings > Add Data > Upload.
4. Upload the CSV file.
5. Select the `cybersecurity_lab` index and verify the timestamps and CSV fields are parsed correctly.
6. Run the SPL queries documented above.
7. Recreate the bar chart, pie chart, and line chart.
