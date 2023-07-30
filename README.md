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

- Setup Resources in Azure
- Ensure Connectivity between the client and Domain Controller
- Install Active Directory
- Create an Admin and Normal User Account in AD
- Join Client-1 to your domain (mydomain.com)
- Setup Remote Desktop for non-administrative users on Client-1
- Create a bunch of additional users and attempt to log into client-1 with one of the users

<h2>Deployment and Configuration Steps</h2>
<p align="center">
Set up Resources in Azure
<p> Create the Domain Controller VM (Windows Server 2022) named “DC-1”
<img src="https://imgur.com/q1s2Z1j.png" height="50%" width="50%" alt="Disk Sanitization Steps"/><p>
<p> 
Create the Client VM (Windows 10) named “Client-1”
<p>
<img src="https://imgur.com/la5JukB.png" height="50%" width="50%" alt="Disk Sanitization Steps"/>
<p>
Set Domain Controller’s NIC Private IP address to be static
<p> DC-1 VM > Networking > Network Interface > IP Configuration
  
<img src="https://imgur.com/VtpsKIZ.png" height="50%" width="50%" alt="Disk Sanitization Steps"/></p>
</p>
</p>
<p align="center">
Ensure Connectivity between the client and Domain Controller
<p>Login to Client-1 with Remote Desktop and ping DC-1’s private IP address with ping -t <ip address> (perpetual ping)
<p>
<img src="https://imgur.com/PqzV5uT.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>
</p>
<p>
Login to the Domain Controller and enable ICMPv4 on the local windows Firewall
<p>

<img src="https://imgur.com/mOid39W.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>
<p>

Check back at Client-1 to see the ping succeed
<p>
<img src="https://imgur.com/L0mS7Go.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>
</p>

<p align="center">
Install Active Directory
<p> Login to DC-1 and install Active Directory Domain Services

<p>
<img src="https://imgur.com/OzIcXK5.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>
<p>
Promote as a Domain Controller
<p>
<img src="https://imgur.com/4mv0SQJ.png" height="100%" width="100%" alt="Disk Sanitization Steps"/>
<p>
Setup a new forest as mydomain.com (can be anything, just remember what it is)
<p>
<img src="https://imgur.com/YQsYsTo.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<p>
Restart and then log back into DC-1 as user: mydomain.com\labuser
<p>
<img src="https://imgur.com/miWH0Na.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>
</p>
<p align="center">
Create an Admin and Normal User Account in Active Directory
<p> Active Directory Users and Computers (ADUC), create an Organizational Unit (OU) called “_EMPLOYEES” & "ADMINS"
<p>
<img src="https://imgur.com/S5GKLdP.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>
<img src="https://imgur.com/S2WYvhP.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>
<p>
Create a new employee named “Jane Doe” (same password) with the username of “jane_admin”
<p>
<img src="https://i.imgur.com/ZgLdkVO.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>
<p>
Add jane_admin to the “Domain Admins” Security Group
<p>
<img src="https://i.imgur.com/nq2xZzz.png" height="70%" width="70%" alt="Disk Sanitization Steps"/>
<p>
Log out/close the Remote Desktop connection to DC-1 and log back in as “mydomain.com\jane_admin”
<p>
<img src="https://imgur.com/UztSnn7.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<p>
  
</p>
<br />
<p align="center">
Join Client-1 to your domain (mydomain.com)
<p> From the Azure Portal, set Client-1’s DNS settings to the DC’s Private IP address
<p>
<img src="https://imgur.com/AgZ9aTI.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<p> From the Azure Portal, restart Client-1
<p> Login to Client-1 (Remote Desktop) as the original local admin (labuser) and join it to the domain (computer will restart)  
<p>
<img src="https://imgur.com/TlFHF7T.png" height="40%" width="40%" alt="Disk Sanitization Steps"/>

<p>
Login to the Domain Controller (Remote Desktop) and verify Client-1 shows up in Active Directory Users and Computers (ADUC) inside the “Computers” container on the root of the domain
<p> Create a new OU named “_CLIENTS” and drag Client-1 into there
<p>
<img src="https://imgur.com/l2FNctc.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>




<p align="center">
Setup Remote Desktop for non-administrative users on Client-1





<p align="center">
Create a bunch of additional users and attempt to log into client-1 with one of the users
