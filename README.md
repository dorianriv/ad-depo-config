<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Project Logo"/>
</p>

<h1>Active Directory Deployment and Configuration – Phase 2</h1>

<p>
Building on the previous project that set up our simulated AD environment, this phase focuses on deploying and configuring Active Directory. We’ll install Active Directory Domain Services (AD DS), create a forest, set up an admin user, join the client machine to the domain, and enable Remote Desktop for domain users. This forms the core of our domain-based network.
</p>

<h2>Overview</h2>

<p>
We’re now working with:

- <strong>DC-1</strong> (Windows Server 2022): Will be promoted to Domain Controller  
- <strong>Client-1</strong> (Windows 10): Will join the domain and test user access

By the end of this phase, we’ll have a working domain and a management-ready AD environment.
</p>

<h2>Key Objectives</h2>

<h3>Active Directory Installation</h3>
- Install AD DS on DC-1 via Server Manager

<h3>Forest and Domain Setup</h3>
- Create a new Active Directory forest

<h3>Admin Account Setup</h3>
- Create and manage admin-level user accounts to control and maintain the Active Directory environment

<h3>Domain Join</h3>
- Join Client-01 to the domain and confirm it can communicate with the Domain Controller

<h3>Remote Desktop Access</h3>
- Configure RDP access for domain users

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)  
- Active Directory Domain Services  
- Remote Desktop  
- Windows Firewall

<h2>Operating Systems Used</h2>

- Windows Server 2022  
- Windows 10 (21H2)

<h2>Configuration Steps</h2>

<h3>&#9312; Install Active Directory on DC-1</h3>

- In the Server Manager dashboard, click Add roles and features, and continue the setup

![screenshot 1](https://github.com/user-attachments/assets/c9d73107-6bf5-4cea-9917-a3cdb4e7be0a)

- Select Active Directory Domain Services and finish the installation 

<h3>&#9313; Promote DC-1 to Domain Controller</h3>

- Once the installation is done, notice the flag on the top right of the Server Manager
- Click on the flag and promote DC-1 to Domain Controller

![screenshot 2](https://github.com/user-attachments/assets/e961eec5-c5ec-45ad-8e1e-87a0f256098a)

- We will now add a new Forest and set the Root domain name to "mydomain.com"

![screenshot 3](https://github.com/user-attachments/assets/d913a844-abbd-4f59-ac5d-c891db61b3af)

- Finish the setup and restart DC-1
- Log back in with "your username"@mydomain.com

<h3>&#9314; Create an Admin User</h3>

- Once DC-1 has rebooted, click on Tools and select Active Directory Users and Computers
- Right click on mydomain.com and select New and click on Organizational Unit

![screenshot 4](https://github.com/user-attachments/assets/925a6fa0-03c3-41e1-b707-9bff845242c3)

- We will be creating an OU named_EMPLOYEES and _ADMINS

![screenshot 5](https://github.com/user-attachments/assets/dce76947-c0e8-4a78-95bb-c0ff6a83a2cb)

- Right click on Users and create a new user named Jane Doe with the username jane_admin

![screenshot 6](https://github.com/user-attachments/assets/21658183-7416-4206-ab05-efa0990fcbfb)

- Now we will turn Jane Doe into an admin by right-clicking her name and adding her to the "Domain Admins" Security Group

![screenshot 7](https://github.com/user-attachments/assets/36cb5e70-b71a-45fa-880b-3974360ad14b)

- Log out of DC-1 and log back in with Jane Doe's credentials

![screenshot 8](https://github.com/user-attachments/assets/bf3b2bad-d0cf-46e1-a688-ba7a48334605)

<h3>&#9315; Join Client-1 to the Domain</h3>

<p>For Client-1 to join the domain, we must first set its DNS server as DC-1's private address.</p>

- In the Azure Portal, select Client-1 -> Networking -> Network interface and click on DNS servers

![screenshot 9](https://github.com/user-attachments/assets/d57bf1de-c2b9-4a1e-834c-a1f24e8d2897)

- Select a custom DNS server and type in the private IP address of DC-1 and restart Client-1

![screenshot 10](https://github.com/user-attachments/assets/af3c5369-7c89-4842-8c18-eed9ea168dbf)

- Now log back into Client-1 using your original admin credentials (labuser). Click Start and go to Settings -> Rename this PC (advanced) -> Change and add "mydomain.com" and log in with the admin credentials previously created (jane_admin)

![screenshot 11](https://github.com/user-attachments/assets/2f9d3e20-01c4-4e4c-9dba-56edd5f58471)

- Once Client-1 has been added, the VM will restart 

<h3>&#9316; Enable RDP for Domain Users</h3>

- Log back into Client-1 using jane_admin and open Settings -> Remote Desktop -> User Accounts and click “Select users that can remotely access this PC”
- Add Domain Users

![screenshot 12](https://github.com/user-attachments/assets/612b0026-a3c9-478c-b3ee-d2191f7beb7f)

- This will allow normal users to log in to Client-1

<h2>Final Thoughts</h2>

<p>
We’ve now fully deployed and configured Active Directory. With a new forest, a working domain, and both admin and client machines properly integrated, we’re ready for the next step: creating users and groups in Active Directory. Phase 3 will cover that in detail.
</p>
