<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Video Demonstration</h2>


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell
- Active Directory

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)
<h2>Objectives </h2>

- Install Active Directory
- Create a Domain Admin user within the domain
- Join Client-1 to your domain (mydomain.com)
- Setup Remote Desktop for non-administrative users on Client-1
- Create additional users and attempt to log into client-1 with one of the users

<h2>Install Active Directory</h2>

<p>
First we will set up our DC-1 VM as our Domain Controller and install active directory in it.
</p>

<p>
  
  ****![image](https://github.com/user-attachments/assets/e4fb3d13-bfdd-4d46-bc8e-0c773341c25d)

</p>
