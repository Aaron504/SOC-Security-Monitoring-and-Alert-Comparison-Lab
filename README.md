# SOC Security Monitoring and Alert Comparison Lab
<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

In this lab, I monitored security events and incidents across multiple data sources, including SecurityEvent, Syslog, SecurityAlert, SecurityIncident, and AzureNetworkAnalytics_CL. The environment was observed for 24 hours, during which I collected and analyzed alerts and incidents. After securing the environment, I allowed another 24-hour observation period and compared the number and severity of alerts before and after implementing the security measures. This lab demonstrates my ability to monitor security events, respond to incidents, and evaluate the effectiveness of security hardening in a SOC environment.




<h2>Environments and Technologies Used</h2>

- Virtual Machines (Windows & Linux)
- Network Security Groups (NSGs)
- Azure Monitor / Network Watcher
- Log Analytics Workspace
- Microsoft Sentinel
- Kusto Query Language (KQL)

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Phase 1: Vulnerable VM Deployment
- Phase 2: 24-Hour Threat Window
- Phase 3: Hardening & Remediation
- Phase 3: Post-Remediation Analysis

<h2>Deployment and Configuration Steps</h2>

Phase 1: Vulnerable Deployment
Deployed VMs with:
- Open ports: SSH (22), RDP (3389), SMB (445)
- Outdated software and missing patches
- Default or weak credentials (e.g., admin/admin123)
- Enabled NSG flow logs and packet capture

![Screenshot 2025-05-11 172608](https://github.com/user-attachments/assets/f040f719-9afa-48a5-ab47-60cc08ade35f)
![Screenshot 2025-05-11 172957](https://github.com/user-attachments/assets/23449c7f-022e-4f3e-ba9f-fd5d6fb23b54)

Phase 2: 24-Hour Threat Window

After deploying the vulnerable virtual machines in various global Azure regions, the environment was left completely exposed for 24 hours with no security controls in place. During this time, Microsoft Sentinel collected telemetry data using NSG flow logs and syslog messages. The findings were mapped visually using built-in geolocation queries.

![Screenshot 2024-10-16 173122](https://github.com/user-attachments/assets/8f1ce94e-80eb-4ddb-8b89-99bb5a890daa)
![Screenshot 2024-10-16 173234](https://github.com/user-attachments/assets/f9769dfa-b839-4ab9-b32f-0e870018d340)
![Screenshot 2024-10-16 173327](https://github.com/user-attachments/assets/b434a1c4-2a04-4701-89be-85f06d25e078)
![Screenshot 2025-05-11 174914](https://github.com/user-attachments/assets/cc517fff-1947-4504-9bdd-ef613508458a)

 Key Observations:
- Over 1,000+ RDP and SSH brute-force attempts were detected in less than a day
- Multiple cities had more than 400 failed login attempts
- NSG misconfigurations led to 930+ confirmed malicious flows reaching target VMs
- Attack traffic originated from over 25 countries, including those commonly associated with botnet infrastructure
- All traffic was collected passively, with no bait interaction — confirming the high-risk profile of publicly exposed VMs

Phase 3: Hardening & Remediation
Applied:
- OS updates and patching
- Strong password policies
- Disabled unnecessary ports/services
- Configured NSGs to allow only whitelisted IPs
- Account lockout (Windows)

![Screenshot 2025-05-11 175821](https://github.com/user-attachments/assets/15edb757-ca1a-43f3-a28d-a7e76e04f562)









