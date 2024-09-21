# Building a SOC + Honeynet in Azure (Live Traffic)
![Cloud Honeynet / SOC](https://github.com/user-attachments/assets/c92aa085-b3d1-4440-b5d0-a1b10d89a1f4)


## Introduction

In this project, I set up a mini Honeynet in Azure and gathered log data from multiple sources into a Log Analytics workspace. From there, Microsoft Sentinel was utilized to generate attack maps, trigger alerts, and create incidents. I monitored specific security metrics in the unsecured environment over a 24-hour period, implemented security controls to strengthen the system, measured the metrics for another 24 hours, and then presented the findings below. 

The metrics we will show are:
- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

## Architecture Before Hardening / Security Controls
![Architecture Diagram](https://i.imgur.com/aBDwnKb.jpg)

## Architecture After Hardening / Security Controls
![Architecture Diagram](https://i.imgur.com/YQNa9Pp.jpg)

The architecture of the mini honeynet in Azure consists of the following components:

- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (2 windows, 1 linux)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel

For the "BEFORE" metrics, all resources were initially deployed and fully exposed to the internet. The Virtual Machines had unrestricted Network Security Groups and firewalls, and all other resources were accessible via public endpoints without the use of Private Endpoints.

For the "AFTER" metrics, I tightened the Network Security Groups by blocking all traffic except for my admin workstation. Additionally, all other resources were secured using their built-in firewalls and Private Endpoints.

## Attack Maps Before Hardening / Security Controls
![NSG Allowed Inbound Malicious Flows](https://github.com/user-attachments/assets/967a0155-53ae-4b3f-93db-e7f87e7ba230)</br>
![Linux Syslog Auth Failures](https://github.com/user-attachments/assets/3f56192a-a3fa-4b33-a03f-9a57b10a6729)<br>
![Windows RDP/SMB Auth Failures](https://github.com/user-attachments/assets/5fcadae6-2e18-4524-8375-30f6138d1842)<br>

## Metrics Before Hardening / Security Controls

The table below presents the metrics we recorded in our unsecured environment over a 24-hour period:
Start Time 2024-09-18 00:37:27
Stop Time 2024-09-19T00:37:27

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 22513
| Syslog                   | 7712
| SecurityAlert            | 0
| SecurityIncident         | 188
| AzureNetworkAnalytics_CL | 2056

## Attack Maps Before Hardening / Security Controls

```All map queries actually returned no results due to no instances of malicious activity for the 24 hour period after hardening.```

## Metrics After Hardening / Security Controls

The table below presents the metrics we collected in our environment over the next 24 hours, following the implementation of security controls:
Start Time 2024-09-20T16:38:57
Stop Time	2024-09-21T16:38:57

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 2549
| Syslog                   | 0
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

## Conclusion

In this project, a mini honeynet was set up in Microsoft Azure, with log sources feeding into a Log Analytics workspace. Microsoft Sentinel was used to generate alerts and incidents based on the collected logs. Security metrics were tracked both before and after applying security controls to the environment. Importantly, there was a significant decrease in security events and incidents following the implementation of the security measures, highlighting their effectiveness.

It is worth noting that if the resources within the network were heavily utilized by regular users, it is likely that more security events and alerts may have been generated within the 24-hour period following the implementation of the security controls.
