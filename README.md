<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Create folders: "read-access", "write-access", "no-access", "accounting"
- Set permissions for the "Domain-Users" group
- Attempt to access file share as a normal User
- Create an "accountants" folder for Security Group and configure permissions

<h2>Actions and Observations</h2>

<p>
  
![image](https://github.com/CopaceticWill/azure-network-protocols/assets/137100082/d02e909f-6177-43b3-b681-f39d888dc912)
</p>
<p>
In this step, I created sample file shares with various permissions
  
  - Connect/log into DC-1 as your domain admin account (mydomain.com\user_admin)
  - Connect/log into Client-1 as a normal user (mydomain\<someuser>)
  - On DC-1, on the C:\ drive, create 4 folders: “read-access”, “write-access”, “no-access”, “accounting”
  - Set the following permissions (share the folder) for the “Domain Users” group:
  - Folder: “read-access”, Group: “Domain Users”, Permission: “Read”
  - Folder: “write-access”,  Group: “Domain Users”, Permissions: “Read/Write”
  - Folder: “no-access”, Group: “Domain Admins”, “Permissions: “Read/Write”

</p>
<br />

<p>

![image](https://github.com/CopaceticWill/azure-network-protocols/assets/137100082/8a72cd75-1923-419a-8776-90525193f5ab)
</p>
<p>
In this step, I created an “ACCOUNTANTS” Security Group, assign permissions, and test access
  
  - Back to DC-1, in Active Directory, and create a security group called “ACCOUNTANTS”
  - On the “accounting” folder I created earlier, I set the following permissions:
      - Folder: “accounting”, Group: “ACCOUNTANTS”, Permissions: “Read/Write”
  - On Client-1, as  <someuser>, I tried to access the accountant's folder. It failed. 
  - I logged out of Client-1 as  <someuser>
  - On DC-1, I make <someuser> a member of the “ACCOUNTANTS”  Security Group
  - I signed back into Client-1 as <someuser> and tried to access the “accounting” share in \\DC-1\ as <someuser> and access is now granted
                                                                                                      
</p>
<br />

