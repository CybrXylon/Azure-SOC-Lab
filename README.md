# Building a SOC + Honeynet in Azure (Live Traffic)
![image](https://github.com/CybrXylon/Azure-SOC-Lab/assets/150117045/c366eb73-e467-4128-8f3d-f64c6614ffb3)



## Introduction

In this project, I build a mini honeynet in Azure and ingest log sources from various resources into a Log Analytics workspace, which is then used by Microsoft Sentinel to build attack maps, trigger alerts, and create incidents. I measured some security metrics in the insecure environment for 24 hours, apply some security controls to harden the environment, measure metrics for another 24 hours, then show the results below. The metrics we will show are:

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

## Architecture Before Hardening / Security Controls
![image](https://github.com/CybrXylon/Azure-SOC-Lab/assets/150117045/ce59703d-1f4e-4980-a419-66e01765c572)


## Architecture After Hardening / Security Controls
![image](https://github.com/CybrXylon/Azure-SOC-Lab/assets/150117045/f68a3571-9aa0-4560-9f22-cb8813a2a92d)


The architecture of the mini honeynet in Azure consists of the following components:

- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (2 windows, 1 linux)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel

For the "BEFORE" metrics, all resources were originally deployed, exposed to the internet. The Virtual Machines had both their Network Security Groups and built-in firewalls wide open, and all other resources are deployed with public endpoints visible to the Internet; aka, no use for Private Endpoints.

For the "AFTER" metrics, Network Security Groups were hardened by blocking ALL traffic with the exception of my admin workstation, and all other resources were protected by their built-in firewalls as well as Private Endpoint

## Attack Maps Before Hardening / Security Controls\
![MySQL Auth Failures]![Screenshot 2023-12-14 153415](https://github.com/CybrXylon/Azure-SOC-Lab/assets/150117045/377ef4cd-ef5e-4348-9064-1c5ad401c36b)<br>

![NSG Allowed Inbound Malicious Flows]![Screenshot 2023-12-14 153620](https://github.com/CybrXylon/Azure-SOC-Lab/assets/150117045/8ded24e6-b865-4136-a272-d1b6dda0ed0b)
<br>
![Linux Syslog Auth Failures]![Screenshot 2023-12-14 153921](https://github.com/CybrXylon/Azure-SOC-Lab/assets/150117045/d1aee7c3-b2b9-4503-99b1-4c77dda66e9b)<br>
![Windows RDP/SMB Auth Failures]![Screenshot 2023-12-14 154044](https://github.com/CybrXylon/Azure-SOC-Lab/assets/150117045/bd64395b-841c-4abd-b1f3-0ab771bc3344)<br>

## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:
Start Time 2023-12-13T23:21:00.0492444Z
Stop Time 2023-12-14T23:21:00.0492444Z

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 41246
| Syslog                   | 40706
| SecurityAlert            | 13
| SecurityIncident         | 547
| AzureNetworkAnalytics_CL | 2671

## Attack Maps Before Hardening / Security Controls

![image](https://github.com/CybrXylon/Azure-SOC-Lab/assets/150117045/ebb3eea6-266b-415e-adad-9dbbfefcbc34)


## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:
Start Time 2023-12-17T04:51:24.8386067Z
Stop Time	2023-12-17T04:51:24.8386067Z

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 8995
| Syslog                   | 1665
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

## Conclusion

In this project, a mini honeynet was constructed in Microsoft Azure and log sources were integrated into a Log Analytics workspace. Microsoft Sentinel was employed to trigger alerts and create incidents based on the ingested logs. Additionally, metrics were measured in the insecure environment before security controls were applied, and then again after implementing security measures. It is noteworthy that the number of security events and incidents were drastically reduced after the security controls were applied, demonstrating their effectiveness.

It is worth noting that if the resources within the network were heavily utilized by regular users, it is likely that more security events and alerts may have been generated within the 24-hour period following the implementation of the security controls.
