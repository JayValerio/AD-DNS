<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory DNS(Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines and Observing DNS addressing and functions.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory
- DNS

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)
<h2>Objectives </h2>

- Observe DNS addressing and functions.

<h2>A-Record</h2>

<p>
An A-record (Address Record) maps a domain name to its corresponding IPv4 address, allowing browsers to find and connect to the correct server. Lets log into our Azure machines and look at how it works.
</p>

<p>
  
  ![image](https://github.com/user-attachments/assets/a8fc2436-86ce-42c8-91bd-86bf2a405b9c)
</p>
<p>
  Now on our Domain Controller lets open up powershell and "ping mainframe", notice how the request cannot be found.
</p>
<p>
  
  ![image](https://github.com/user-attachments/assets/6969c2ee-b9eb-4f15-b0bf-2f8d856e9860)

</p>

<p>
  now lets also "nslookup mainframe" and notice how this also fails.
</p>

<p>
  
  ![image](https://github.com/user-attachments/assets/71804348-d2e2-4a88-9a09-07adb597bd72)

</p>
<p>
  Now that we have established that 'mainframe' does not exist on our Domain Controller we will make an "A-Record" and have mainframe point to our DC IP address.
</p>
<p>
  On our DNS server, open 'administrative tools' and find 'DNS'. Here we open the dropdown for 'DC-1' and 'alphadomain.com'. Here we will see the different A-Records recorded in the cache.
</p>
<p>

  ![image](https://github.com/user-attachments/assets/cd41fa2c-04bc-4902-b7da-0b172744a45b)

</p>















