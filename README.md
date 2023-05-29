<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Video Demonstration</h2>

- ### [YouTube: How to Deploy on-premises Active Directory within Azure Computer](https://www.youtube.com/watch?v=Tz5W5h5U81g)

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

<p>
<img src="https://i.imgur.com/5rrTKOO.png" height="100%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<p>
8. Login to DC-1 and install Active Directory Domain Services.
</p>
<br />

<p>
<img src="https://i.imgur.com/p64caNH.png" height="100%" width="100%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/gezRyBb.png" height="100%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<p>
9. Promote as a DC: Setup a new forest as mydomain.com (can be anything, just remember what it is).
</p>
<br />

<p>
<img src="https://i.imgur.com/xDfi2PT.png" height="100%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<p>
10. Restart and then log back into DC-1 as user: mydomain.com\labuser. Though in my case I just have to type labuser since I am on Linux Mint using a third party RDP software.
</p>
<br />

<p>
<img src="https://i.imgur.com/zcnoImF.png" height="100%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<p>
11. In Active Directory Users and Computers (ADUC), create an Organizational Unit (OU) called “_EMPLOYEES”
</p>
<br />

<p>
<img src="https://i.imgur.com/JIVxqTy.png" height="100%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<p>
12. Create a new OU named “_ADMINS”
</p>
<br />

<p>
<img src="https://i.imgur.com/dA6CqgJ.png" height="100%" width="100%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/KsuC0xR.png" height="100%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<p>
13. Create a new employee named “Jane Doe” (same password) with the username of “jane_admin”
</p>
<br />

<p>
<img src="https://i.imgur.com/u7EeM6F.png" height="100%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<p>
14. Add jane_admin to the “Domain Admins” Security Group
</p>
<br />

<p>
<img src="https://i.imgur.com/Jia3NyJ.png" height="100%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<p>
15. Log out/close the Remote Desktop connection to DC-1 and log back in as “mydomain.com\jane_admin”. 
16. Use jane_admin as your admin account from now on fo DC-1.
</p>
<br />

<p>
<img src="https://i.imgur.com/8sRTeXZ.png" height="100%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<p>
17. From the Azure Portal, set Client-1’s DNS settings to the DC’s Private IP address.
</p>
<br />

<p>
<img src="https://i.imgur.com/2NJcpwV.png" height="100%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<p>
18. From the Azure Portal, restart Client-1.
</p>
<br />

<p>
<img src="https://i.imgur.com/e2HjyPd.png" height="100%" width="100%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/BMf5gfk.png" height="100%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<p>
19. Login to Client-1 (Remote Desktop) as the original local admin (labuser) and join it to the domain (computer will restart)
</p>
<br />

<p>
<img src="https://i.imgur.com/7Zn9SFq.png" height="100%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<p>
20. Login to the Domain Controller (Remote Desktop) and verify Client-1 shows up in Active Directory Users and Computers (ADUC) inside the “Computers” container on the root of the domain
</p>
<br />

<p>
<img src="https://i.imgur.com/Iv3lNWw.png" height="100%" width="100%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/FV7Agcl.png" height="100%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<p>
21. Create a new OU named “_CLIENTS” and drag Client-1 into there
</p>
<br />

<p>
<img src="https://i.imgur.com/H9Qn46M.png" height="100%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<p>
22. Log into Client-1 as mydomain.com\jane_admin and open system properties.
23. Click “Remote Desktop”
</p>
<br />

<p>
<img src="https://i.imgur.com/4PD2hT3.png" height="100%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<p>
24. Allow “domain users” access to remote desktop
</p>
<br />

<p>
<img src="https://i.imgur.com/v3Uq8gx.png" height="100%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<p>
25. You can now log into Client-1 as a normal, non-administrative user now.
</p>
<br />

<p>
<img src="https://i.imgur.com/aJ7WEpC.png" height="100%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<p>
26. Login to DC-1 as jane_admin
</p>
<br />

<p>
<img src="https://i.imgur.com/CnVShsu.png" height="100%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<p>
27. Open PowerShell_ise as an administrator.
</p>
<br />

<p>
<img src="https://i.imgur.com/ricgzsG.png" height="100%" width="100%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/cM7J7iB.png" height="100%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<p>
28. Create a new File and paste the contents of the script into it (https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1)
</p>
<br />

<p>
<img src="https://i.imgur.com/krfgwLy.png" height="100%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<p>
29. Run the script and observe the accounts being created.
</p>
<br />

<p>
<img src="https://i.imgur.com/tmBrshE.png" height="100%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<p>
30. When finished, open ADUC and observe the accounts in the appropriate OU.
</p>
<br />

<p>
<img src="https://i.imgur.com/IaO3moT.png" height="100%" width="100%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/b0BslfF.png" height="100%" width="100%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/rGJp9eM.png" height="100%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<p>
31. Attempt to log into Client-1 with one of the accounts (take note of the password in the script).
</p>
<br />

This concludes the implementation of on-premises Active Directory within Azure Virtual Machines.
