# Building a SOC + Honeynet in Azure (Live Traffic)
![Cloud Honeynet / SOC](https://i.imgur.com/NQMrqma.jpg)

## Introduction

In this project, I created a mini honeynet in Azure, integrating various log sources into a Log Analytics workspace. Microsoft Sentinel was then utilized to develop attack maps, trigger alerts, and generate incidents. Initially, security metrics were measured in the unsecured environment over a 24-hour period. After applying security controls to strengthen the environment, metrics were measured again for another 24 hours. The results, showcasing the effectiveness of the implemented security controls, are detailed below. The metrics presented include:

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- nsg-malicious-allowed-in (Malicious Flows allowed into our honeynet)

## Architecture Before Hardening / Security Controls
![Architecture Diagram](https://i.imgur.com/LSgw8bs.jpg)

## Architecture After Hardening / Security Controls
![Architecture Diagram](https://i.imgur.com/3r2MzHr.jpg)

The architecture of the mini honeynet in Azure is composed of the following elements:

- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (2 windows, 1 linux)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel

BEFORE Metrics: Initially, all resources were deployed with internet exposure. The Virtual Machines had their Network Security Groups and built-in firewalls completely open, and all other resources had public endpoints visible to the internet, with no use of Private Endpoints.

AFTER Metrics: Network Security Groups were hardened by blocking ALL traffic with the exception of my admin workstation, and all other resources were protected by their built-in firewalls as well as Private Endpoint

## Attack Maps Before Hardening / Security Controls
![NSG Allowed Inbound Malicious Flows](https://i.imgur.com/w7XWaMA.png)<br>
![Linux Syslog Auth Failures](https://i.imgur.com/aJcuG83.png)<br>
![MySQL Auth Failures](https://i.imgur.com/rk49fP4.png)<br>
![Windows RDP/SMB Auth Failures](https://i.imgur.com/vcbX86e.png)<br>

## Metrics Before Hardening / Security Controls

The information below displays the metrics recorded in our insecure environment over a 24-hour period:

Start Time: 5/30/2024 19:39:11

Stop Time: 5/31/2024 19:39:11

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 18599
| Syslog                   | 8470
| SecurityAlert            | 2
| SecurityIncident         | 136
| NSG Inbound Malicious Allowed | 1129

## Attack Maps Before Hardening / Security Controls

```Map queries returned no results due to the absence of malicious activity in the 24-hour period following the hardening process.```

## Metrics After Hardening / Security Controls

The table below displays the metrics recorded in our environment for another 24 hours, following the implementation of security controls:


Start Time 6/9/2024 20:32:45


Stop Time	6/10/2024 20:32:45

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 9497
| Syslog                   | 1
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

## Conclusion

For this project, I designed a mini honeynet in Microsoft Azure, integrating log sources into a Log Analytics workspace. Microsoft Sentinel was utilized to generate alerts and incidents from these logs. Initial metrics were recorded in an unsecured environment, followed by additional metrics taken after implementing security controls. The results showed a significant reduction in security events and incidents, demonstrating the effectiveness of the security measures.

It is also important to note that if network resources had been heavily used by regular users, more security events and alerts might have been generated within the 24-hour period following the implementation of the security controls.
