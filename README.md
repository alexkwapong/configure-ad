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

- Step 1
- Step 2
- Step 3
- Step 4

<h2>Deployment and Configuration Steps</h2>

<p>


Step 1: Log into Azure --> search "virtual machines" --> click "create azure virtual machine" to create VM#1. Name this first virtual machine "DC-1" using your current region --> set the image type as "Windows Server 2022" (effectively making it a domain for the lab) --> Set username and password --> create VM #2 --> title it "Client-1" (repeat the same steps used to create VM#1 except for the image type select "Windows 10 pro" since this VM will be the employees'/ cleints' computer).</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Step 2: Go to DC-1's network settings --> select networking --> click the hyperlink next to "network interface" --> "IP Configurations" --> "ipconfig1" --> change the assignment from dynamic to static (this ensures DC-1's IP address will not change) --> check the NIC settings to make sure both VMs are on the same "Vnet". This will ensure both VMs can communicate & connect with each other later in this lab.</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Step 3: Remote Desktop into DC-1 via windows firwall security settings --> Advanced settings --> inbound/outbound rules to allow "IPV4 permissions" on DC-1's Firewall. This will open the firewall for connectivity after DC-1 is converted into a domain.</p>
<br />
Step 4: Ensure communication between both VMs via perpetual ping using cmd:ping -t (Ip Address).

Step 5: Install "Active Directory" on DC-1. Set up DC-1 as a new domain.
Step 6: Remote Desktop into DC-1 to create two "Organzational Units" (OU), one titled "Admins" and another titled "Employees" within Active Directory.
Step 7: Change Client-1's "DNS settings" in Azure to match the same private IP Address as DC-1 via network settings in DC-1. Go into Client-1's network settings --> Network Interface (NIC) --> DNS server --> custom DNS settings --> add DC-1's private IP Address as the DNS server to connect to for Client-1. Restart Client-1 to flush the DNS cache --> change Client-1 to the same domain as DC-1 via "about PC" --> rename this PC advanced --> type DC-1's domain name under the "domain section" --> create a new OU named "_clients".

Step 8: Use Remote Desktop in the system settings to allow domain users access for all non-admin users on Client-1 VM under "user accounts" --> "select users that can remotely access this PC" --> click "add" and type in "domain users".

Step 9: Use a random account generating script to create at least 100 users for this lab. Upload script via "Powershell ISE" (run as administrator) to Client-1. This will create 100 new users with random names. This is done to simulate employees within the company.

Step 10: Log into any newly generated user account on Client-1 VM. The login attempt with the user's name & generic password should be successful. That is the conclusion of this lab.
