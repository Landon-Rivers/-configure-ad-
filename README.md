<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Video Demonstration</h2>

- ### [YouTube: How to Deploy on-premises Active Directory within Azure Compute](https://www.youtube.com)

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

<p>
<img src="https://i.imgur.com/ZKYSmVQ.png" height="100%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<p>
1. Create the Domain Controller VM (Windows Server 2022) named “DC-1”
</p>
<br />

<p>
<img src="https://i.imgur.com/M1d9yCa.png" height="100%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<p>
2. Set Domain Controller’s NIC Private IP address to be static
</p>
<br />

<p>
<img src="https://i.imgur.com/aGzcXMU.png" height="100%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<p>
3. Create the Client VM (Windows 10) named “Client-1”. Use the same Resource Group 
</p>
<br />

<p>
<img src="https://i.imgur.com/yEb5vK3.png" height="100%" width="100%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/6KdZKMT.png" height="100%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<p>
4. Ensure that both VMs are in the same Vnet.
</p>
<br />

<p>
<img src="https://i.imgur.com/X874OHd.png" height="100%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<p>
5. Login to Client-1 with Remote Desktop and ping DC-1’s private IP address with ping -t <ip address> (perpetual ping)
</p>
<br />

<p>
<img src="https://i.imgur.com/Z3m4Sjp.png" height="100%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<p>
6. Login to the Domain Controller and enable ICMPv4 in on the local windows Firewall
</p>
<br />

<p>
<img src="https://i.imgur.com/Zrr5dL6.png" height="100%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<p>
7. Check back at Client-1 to see the ping succeed
</p>
<br />

