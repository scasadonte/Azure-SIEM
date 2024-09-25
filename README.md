
# Introduction

I set up a mini-security operations center (honeynet) on Microsoft Azure in this project. After configuring multiple insecure VMs and services on Azure, I directed the VMs and services' security and event logs to be forwarded to Azure's Log Analytics Workspace to be processed by the platform's native SIEM, Microsoft Sentinel. I configured Sentinel to record incidents and trigger events, using live traffic data to generate attack maps based on the attackers' geographic location. After configuring the network and resources, I monitored the vulnerable network for 24 hours. After analyzing and documenting the results, I secured the VMs and network per Nist 800-53, at which point I monitored the network for another 24 hours to observe the differences. 

# Network Topology
![AzureMap](https://github.com/user-attachments/assets/348d83c7-6c8b-4054-9c00-e059305402b7)

When configuring the network, the following data was used:
* Syslog (Linux VM)
* SecurityEvents (Windows VM)
* SecurityAlert (Log Analytics Alerts)
* SecurityIncident (Incidents recorded by Microsoft Sentinel)
* AzureNetworkAnalytics_CL (Malicious Flows from the Internet)

# Before Securing Environment

For the project's initial phase, I deliberately made the system insecure by configuring the Network Security Groups and firewalls of both VMs to allow all incoming traffic. Additionally, I deployed resources such as the Key Vault and Storage Account with public endpoints, exposing them to the Internet.

<img width="1274" alt="Screenshot 2024-09-22 at 5 52 07 PM" src="https://github.com/user-attachments/assets/538b432d-b604-4666-9047-9cbc32711d8e">

<img width="1173" alt="Screenshot 2024-09-22 at 5 52 31 PM" src="https://github.com/user-attachments/assets/8a2e3343-ed8d-4846-8290-f6fcd60cb035">

<img width="1001" alt="Screenshot 2024-09-22 at 5 53 03 PM" src="https://github.com/user-attachments/assets/71140477-ecc5-436b-bcc2-d01f9ff5d24d">

<br></br>

![image](https://github.com/user-attachments/assets/eaa53b45-79ec-4840-9740-cf1a1de8df3f)

These are the metrics gathered after running the vulnerable network for 24 hours.

# After Securing Environment

To enhance the network security, I reconfigured the Network Security Groups to block all incoming traffic except for authorized users based on the documented results. I also secured the network resources by placing them within a new private network and setting up private endpoints for all resources. As an additional measure, I implemented a new Network Security Group to block all traffic except for resources located within the VLAN. This ensured that the resources could still forward logs and interact with other resources within the network while no longer being exposed to the Internet.

<br>

![image](https://github.com/user-attachments/assets/12a06aaa-05a1-44ea-88bf-edeca7229af8)

These are the metrics gathered after running the secure network for 24 hours. 

# Conclusion

In this project, I learned to leverage Microsoft Azure's native resources to set up and configure a Mini-Security operations center via their SIEM and Microsoft Sentinel. By doing this project, I learned how to configure these resources, forward their logs to the Log Analytics Workspace, and Set up the SIEM to monitor live traffic while recording incidents and security events. I also learned how to harden the system, isolate critical resources, and remediate vulnerabilities through best practices, as published in NIST 800-53. These changes yielded a positive effect, as it can be seen in the recorded metrics that the number of events and incidents was reduced dramatically. In the future, I would like to do this project again and further explore the capabilities of Microsoft Sentinel. 








