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
  DNS is a hierarchical naming system that translates human-readable domain names (like example.com) into IP addresses (like 192.0.2.1) used by computers to identify each other on a network. It enables users to access websites using easy-to-remember names instead of numerical IP addresses, acting as the "phonebook" of the internet.
</p>
An A-record (Address Record) maps a domain name to its corresponding IPv4 address, allowing browsers to find and connect to the correct server. Lets log into our Azure machines and look at how it works.
</p>

<p>
  
  ![image](https://github.com/user-attachments/assets/a8fc2436-86ce-42c8-91bd-86bf2a405b9c)
</p>
<p>
  Now on our Client-1 VM lets open up powershell and "ping mainframe", notice how the request cannot be found.
</p>
<p>
  
  ![image](https://github.com/user-attachments/assets/6969c2ee-b9eb-4f15-b0bf-2f8d856e9860)

</p>

<p>
  now lets "nslookup mainframe" and notice how this also fails.
</p>

<p>
  
  ![image](https://github.com/user-attachments/assets/71804348-d2e2-4a88-9a09-07adb597bd72)

</p>
<p>
  Now that we have established that 'mainframe' does not point towards any IP address on our VNET, we will make an "A-Record" and have 'mainframe' point to our VM machine, DC-1's, IP address.
</p>
<p>
  On our DC-1 VM, open windows 'administrative tools' and find 'DNS'. Here we open the dropdown for 'DC-1' and 'alphadomain.com'. Here we will see the different A-Records recorded in the cache.
</p>
<p>

  ![image](https://github.com/user-attachments/assets/cd41fa2c-04bc-4902-b7da-0b172744a45b)

</p>
<p>
  Now lets create an A-record with the hostname "mainframe", this A record will point towards our DC-1 IP Address. In this example that would be 10.1.0.4
</p>
<p>
  
  ![image](https://github.com/user-attachments/assets/11a7ae04-0ef3-4df7-8707-f2debf6c4683)

</p>
<p>
  Right click 'alphadomain.com' then select 'New Host(A or AAA)...' and add the A-record 'mainframe' with the IP Address '10.1.0.4'. Adding a Pointer Record allows us to reverse look up this A-record.
</p>
<p>
  
  ![image](https://github.com/user-attachments/assets/0e66a074-b99e-44f9-ac66-77504afde86d)

</p>
<p>
  Now we can 'ping mainframe' in client-1 and it will show the ping from the IP Address for DC-1.
</p>
<p>

  ![image](https://github.com/user-attachments/assets/f3115cbd-1d9e-49ae-8071-434c43c05eaa)

</p>
<p>
  The A-Record for mainframe can be changed to point towards any IP Address we choose, We can change it to google.com IP Address with a couple of extra steps. Lets go back into DC-1 DNS Manager, change 'mainframe' IP Address to '8.8.8.8', This is google.com's IP Address.
  
</p>
<p>
  
  ![image](https://github.com/user-attachments/assets/59a6c802-2e28-468c-a0a1-8f1c620451df)

</p>
<p>
  Now lets go into Client-1 and observe the changes.
</p>
<p>
  
  ![image](https://github.com/user-attachments/assets/0ba13cbc-7216-48d5-a878-205f8032c77c)


</p>
<p>
  You'll notice the IP Address has not changed and that is because when DNS tries to resolve the host name it checks the 'cache' first then 'Local Host File' then it will check the DNS Server for the IP Address. Since mainframe was already in the 'cache' as 10.1.0.4 that is what we are seeing in powershell. To fix this issue we simply push the command 'ipconfig /flushdns' and this will flush the cache. Note that this can only be done if you are running powershell as an administrator.
</p>
<p>

  ![image](https://github.com/user-attachments/assets/bdaa0c75-2747-4e7d-83e8-1de27f6bb1ef)

</p>
<p>
  Now that we have flushed the cache, lets ping mainframe again and observe those changes.
</p>
<p>
  
  ![image](https://github.com/user-attachments/assets/3a1de6a3-795d-4e4b-942c-37c492510862)

</p>
<p>
  Another tool in DNS is CNAME, A CNAME record (Canonical Name record) maps one domain name to another, allowing multiple domains to point to the same server or service.
</p>
<p>
  Lets go back to DC-1 DNS Manager, right click 'alphadomain.com' and select 'New Alias (CNAME)...'. Lets name this 'Cash' and map it to 'google.com'
<p>
  
  ![image](https://github.com/user-attachments/assets/47723204-744d-4e53-9dfe-1fda3fd1d9be)

</p>
<p>
  Back in client-1 lets ping Cash and observe as it points towards google.com.
</p>
<p>
  
  ![image](https://github.com/user-attachments/assets/d16cb454-c59f-4b77-98e4-d29725b9de1a)

</p>







