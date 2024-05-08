<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Create Two Virtual Machines In Azure (Domain Controller [DC] & Client-1)
- Install Active Directory On DC & "Join" Client-1 To DC
- Create User Accounts On DC Using Powershell Script
- Create Folders & Share Over Network

<h2>Deployment and Configuration Steps</h2>

<p>
<img src="https://github.com/zjmassie/configure-ad/assets/139398375/1f9b8e15-8037-498e-9a66-37bd18e0d903"/>
</p>

- Setup resources in Azure
- Create Domain Controller VM (DC-1)
- Set DC's NIC Private IP address to be "static"
- Create client VM using Windows 10 (Client-1)
- Make sure both VMs are on the same virtual network
</p>
<br />

<p>
<img src="https://github.com/zjmassie/configure-ad/assets/139398375/6e143d2d-6a3d-4e91-801f-5268fd21c13f"/>
</p>

- Check connectivity b/w client & Domain Controller
- Login to Client-1 using Remote Desktop
- Ping DC-1 using private IP (ping -t for infinite ping)
- Login to Domain Controller & enable ICMPv4 on local Windows Firewall
- Check back in on Client-1 to see the ping go through
</p>
<br />

<p>
<img src="https://github.com/zjmassie/configure-ad/assets/139398375/b42e68b9-30b6-4c3c-9ccd-46d1a28879ec"/>
<img src="https://github.com/zjmassie/configure-ad/assets/139398375/6ebc2586-3054-41d9-a513-e8778bcac896"/>

</p>

- Install Active Directory
- Login to DC-1 & install Active Directory Domain Services
- Setup new forest as mydomain.com
- Restart & then log back into DC-1 as user: mydomain.com/labuser
</p>
<br />

<p>
<img src="https://github.com/zjmassie/configure-ad/assets/139398375/499d2905-4316-4a97-a984-e5bf4e29e773"/>
<img src="https://github.com/zjmassie/configure-ad/assets/139398375/1cf50940-fc6f-448f-bf4b-a8749d0da8da"/>
<img src="https://github.com/zjmassie/configure-ad/assets/139398375/08cbb572-e9fe-4779-8b03-87eab061afde"/>
<img src="https://github.com/zjmassie/configure-ad/assets/139398375/cd2a1b95-99a0-49d4-b035-4de58103160e"/>

</p>

- Create admin & normal user account in Active Directory
- In AD Users & Computers, make an Organizational Unit (_EMPLOYEES)
- Create another Organizational Unity (_ADMINS)
- Create new employee name (can be "jane doe" or personal name) w/the username "jane_admin"
- Add jane_admin to "Domain Admins" Security Group
- Close Remote Desktop connection to DC-1
- Log back in as "mydomain.com\jane_admin"
- User jane_admin as main account
</p>
<br />

<p>
<img src="https://github.com/zjmassie/configure-ad/assets/139398375/784577da-2536-4f6a-844e-3f030f6d6ae5"/>

</p>

- In Azure Portal, set Client-1's DNS settings to the DC's private IP address
- Restart Client-1 in Azure Portal
- Login to DC via Remote Desktop to make sure Client-1 Shows up in Active Directory Users & Computers
</p>
<br />

<p>
<img src="https://github.com/zjmassie/configure-ad/assets/139398375/68631c85-ee94-4f0f-90a4-79b5730d74d6"/>
<img src="https://github.com/zjmassie/configure-ad/assets/139398375/6fb07b33-bf60-4955-b6e5-17b9447fa4a2"/>

</p>

- Log into Client-1 as mydomain.com\jane_admin (or whatever name you used) & open system properties
- Select "Remote Desktop"
- Allow "domain users" access to remote desktop
</p>
<br />

<p>
<img src="https://github.com/zjmassie/configure-ad/assets/139398375/709fb9f2-0af7-4b2c-83ae-0dca33229e09"/>
<img src="https://github.com/zjmassie/configure-ad/assets/139398375/fcfba95a-e38a-4388-850a-a87ea932a1e1"/>

</p>

- Login to DC-1 as jane_admin
- Open Powershell_ISE as administrator
- Create new file and run script to generate names and create users
- Attempt to log into Client-1 with one of the accounts created

Excelsior! Thou hast completed thine quest.
