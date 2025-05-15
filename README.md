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

![screenshot 1](https://github.com/user-attachments/assets/684fe051-e393-478c-9660-f3e7b0b17170)

- Select Active Directory Domain Services and finish the installation 

<h3>&#9313; Promote DC-1 to Domain Controller</h3>

- Once the installation is done, notice the flag on the top right of the Server Manager
- Click on the flag and promote DC-1 to Domain Controller

![screenshot 2](https://github.com/user-attachments/assets/3adb15a5-3c33-499a-8cad-0189a917509b)

- We will now add a new Forest and set the Root domain name to "mydomain.com"

![screenshot 3](https://github.com/user-attachments/assets/e314682b-fa8a-4dce-8cd5-aef2ac665ab8)

- Finish the setup and restart DC-1
- Log back in with "your username"@mydomain.com

<h3>&#9314; Create an Admin User</h3>

- Once DC-1 has rebooted, click on Tools and select Active Directory Users and Computers
- Right click on mydomain.com and select New and click on Organizational Unit

![screenshot 4](https://github.com/user-attachments/assets/e014fa30-747c-454e-ba40-71be6f1e0b2d)

- We will be creating an OU named_EMPLOYEES and _ADMINS

![screenshot 5](https://github.com/user-attachments/assets/3c8e514b-66c7-411d-8960-c2063a83d0bb)

- Right click on Users and create a new user named Jane Doe with the username jane_admin

![screenshot 6](https://github.com/user-attachments/assets/8c763704-53c5-468d-9eb2-96551e7594a3)

- Now we will turn Jane Doe into an admin by right-clicking her name and adding her to the "Domain Admins" Security Group

![screenshot 7](https://github.com/user-attachments/assets/4b75aef0-1e81-4d9f-9e68-fa147408f631)

- Log out of DC-1 and log back in with Jane Doe's credentials

![screenshot 8](https://github.com/user-attachments/assets/abcf7cc6-809f-422a-b193-abe047ed39aa)

<h3>&#9315; Join Client-1 to the Domain</h3>

<p>For Client-1 to join the domain, we must first set its DNS server as DC-1's private address.</p>

- In the Azure Portal, select Client-1 -> Networking -> Network interface and click on DNS servers

![screenshot 9](https://github.com/user-attachments/assets/85bcf242-3b33-4a93-b792-56bf32024ea4)

- Select a custom DNS server and type in the private IP address of DC-1 and restart Client-1

![screenshot 10](https://github.com/user-attachments/assets/91d8bac3-c52f-4b60-abc5-74942c672ee8)

- Now log back into Client-1 using your original admin credentials (labuser). Click Start and go to Settings -> Rename this PC (advanced) -> Change and add "mydomain.com" and log in with the admin credentials previously created (jane_admin)

![screenshot 11](https://github.com/user-attachments/assets/4092a5ca-00e6-4ccb-9565-06618ce0e0f9)

- Once Client-1 has been added, the VM will restart 

<h3>&#9316; Enable RDP for Domain Users</h3>

- Log back into Client-1 using jane_admin and open Settings -> Remote Desktop -> User Accounts and click “Select users that can remotely access this PC”
- Add Domain Users

![screenshot 12](https://github.com/user-attachments/assets/4e557f2b-be64-45d1-862b-0d0a21c0625f)

- This will allow normal users to log in to Client-1

<h2>Final Thoughts</h2>

<p>
We’ve now fully deployed and configured Active Directory. With a new forest, a working domain, and both admin and client machines properly integrated, we’re ready for the next step: creating users and groups in Active Directory. Phase 3 will cover that in detail.
</p>
