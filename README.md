<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Computer)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Step 1: Create the Domain Controller Virtual Machine.
- Step 2: Set the Domain Controller's NIC Private IP address to "static."
- Step 3: Create the Client Virtual Machine.
- Step 4: Install Active Directory.
- Step 5: Create an Admin and Normal User Account in Active Directory.
- Step 6: Join Client-1 to your domain (mydomain.com).
- Step 7: Set up Remote Desktop for non-administrative users on Client-1.

<h2>Deployment and Configuration Steps</h2>

<p>
<img src="https://i.imgur.com/HTro8P8.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Step 1: Create the Domain Controller Virtual Machine. In Microsoft Azure create a Windows Server 2022 named "DC-1". Note the Resource Group and Virtual Network (Vnet) that get created at this time.  You will need this information when setting up the Client VM.
</p>
<br />

<p>
<img src="https://i.imgur.com/xxMIkIr.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Step 2: Set the Domain Controller's NIC Private IP address to "static." 
</p>
<br />

<p>
<img src="https://i.imgur.com/sh1nDTF.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Step 3: Create the Client Virtual Machine. In Microsoft Azure, create the Client VM (Windows 10) named "Client-1". Use the same Resource Group and Vnet that were created in Step 1 for the Domain Controller VM.
</p>
<br />

<p>
<img src="https://i.imgur.com/cbMk5r3.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Step 4: Install Active Directory. Login to DC-1 and install Active Directory Domain services.  Promote DC-1 to a Domain Controller: Set up a new forest as mydomain.com. Restart the computer and log back into DC-1 as user: mydomain.com/freeuser.
</p>
<br />

<p>
<img src="https://i.imgur.com/xo2Z5de.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Step 5: Create an Admin and Normal User Account in Active Directory. In Active Directory Users and Computers (ADUC), create two new organizational units: _EMPLOYEES and _ADMINS.  Create a new employee name "Jane Doe" with the username of "jane_admin."  Add jane_admin to the "Domains Admins" Security Group. Log back in as "mydomain.com\jane_admin".
</p>
<br />


<p>
<img src="https://i.imgur.com/kK3tIM2.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Step 6: Join Client-1 to your domain (mydomain.com). From the Azure Portal, set Client-1's DNS settings to the DC"s Private IP Address. In this case, the private IP address is 10.0.0.4. From the Azure portal restart Client-1. Login to Client-1 (via Remote Desktop) as the original admin and joinit to the domain.  This is done from "settings" -> "about" -> "rename".  (The computer will restart.)
</p>
<br />


<p>
<img src="https://i.imgur.com/uddYDcJ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Step 7: Set up Remote Desktop for non-administrative users on Client-1. Log into Client-1 as mydomain.com\jane_admin and open System properties. Click "Remote Desktop" and allow "domain users" access to remote desktop.  You can now log into Client-1 as a normal, non-administrative user now.
</p>
<br />


