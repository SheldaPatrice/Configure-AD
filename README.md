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

- Step 1: Set Up Resources in Azure
  
- Step 2: Create the Domain Controller VM (Windows Server 2022) named "DC-1"
  
- Step 3: Set Domain Controller's NIC Private IP Address to be Static

- Step 4: Create the Client VM (Windows 10) named "Client-1"

- Step 5: Ensure Both VMs Are in the Same Vnet

- Step 6: Ensure Connectivity Between Client and Domain Controller

- Step 7: Install Active Directory

- Step 8: Create Admin and Normal User Accounts in AD

- Step 9: Join Client-1 to Your Domain (mydomain.com)

- Step 10: Organize Client-1

- Step 11: Set Up Remote Desktop for Non-Administrative Users on Client-1

- Step 12: Create Additional Users

<h2>Deployment and Configuration Steps</h2>

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

****Set Up Resources in Azure:****

   - Go to the Azure Portal (https://portal.azure.com/).
  
   - Follow Azure's guided process to create a Resource Group and a Virtual Network (Vnet). Remember the names of these resources.

**Create the Domain Controller VM (Windows Server 2022) named "DC-1":**
   - In Azure Portal:
        - Navigate to "Virtual Machines."
        - Click "Add" to create a new virtual machine.
        - Choose "Windows Server 2022" as the OS. Name it "DC-1."
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
  
****Set Domain Controller's NIC Private IP Address to be Static:****

- In the Azure Portal, go to "DC-1" settings.

- Find the network interface card (NIC) settings.

- Set the private IP address to be static.

**Create the Client VM (Windows 10) named "Client-1":**

  - Use the same Resource Group and Vnet from Step 1.a.

**Ensure Both VMs Are in the Same Vnet:**

   - Confirm that both "DC-1" and "Client-1" are in the same Virtual Network.
     
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
  
**Ensure Connectivity Between Client and Domain Controller:**

- Log in to "Client-1" using Remote Desktop.

- Open Command Prompt and ping "DC-1's" private IP address using: ping -t <ip address>

- On "DC-1," enable ICMPv4 in the Windows Firewall settings.

- Check if the ping from "Client-1" succeeds.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
  
****Install Active Directory:****

- Log in to "DC-1" and install "Active Directory Domain Services."

- Promote it as a new forest, e.g., "mydomain.com" (you can choose a different name).

- After the promotion, restart "DC-1" and log back in as "mydomain.com\labuser."

****Create Admin and Normal User Accounts in AD:****

- In "Active Directory Users and Computers" (ADUC), create an OU named "_EMPLOYEES."

- Create another OU named "_ADMINS."

- Create a user named "Jane Doe" with the username "jane_admin" in the "_ADMINS" OU.

- Add "jane_admin" to the "Domain Admins" Security Group.

- Log out and log back in as "mydomain.com\jane_admin" for administrative tasks.

</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

  **Join Client-1 to Your Domain (mydomain.com):**

- In the Azure Portal, set "Client-1's" DNS settings to "DC's" Private IP address.

- Restart "Client-1" from the Azure Portal.

- Log in to "Client-1" as the original local admin ("labuser") and join it to the domain. The computer will restart.

**Organize Client-1:**

- Log in to the Domain Controller using Remote Desktop.

- In ADUC, verify that "Client-1" appears under "Computers" in the root of the domain.

- Optionally, create an OU named "_CLIENTS" and move "Client-1" there for organization.

**Set Up Remote Desktop for Non-Administrative Users on Client-1:**

- Log into "Client-1" as "mydomain.com\jane_admin."

- Open system properties and click "Remote Desktop."

- Allow "domain users" access to remote desktop.
  
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

  **Create Additional Users:**

- Log in to "DC-1" as "jane_admin."

- Open PowerShell ISE as an administrator.

- Paste the contents of this script (https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1) into a new file.

- Run the script to create user accounts.

- In ADUC, observe the accounts in the appropriate OU.

- Attempt to log into "Client-1" with one of the newly created accounts.

- Optionally, create an OU named "_CLIENTS" and move "Client-1" there for organization.

</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

**Set Up Remote Desktop for Non-Administrative Users on Client-1:**

- Log into "Client-1" as "mydomain.com\jane_admin."

- Open system properties and click "Remote Desktop."

- Allow "domain users" access to remote desktop.

**Create Additional Users:**

- Log in to "DC-1" as "jane_admin."

- Open PowerShell ISE as an administrator.

- Paste the contents of this script (https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1) into a new file.

- Run the script to create user accounts.

- In ADUC, observe the accounts in the appropriate OU.

- Attempt to log into "Client-1" with one of the newly created accounts.




