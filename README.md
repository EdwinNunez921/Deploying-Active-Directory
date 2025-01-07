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

<h2>Deployment and Configuration Steps</h2>

<h2>Step 1: Install Active Directory Domain Services on DC-1</h2>

<p>
<img src="https://github.com/user-attachments/assets/6ed319e8-1ba6-4947-8b05-08d10c6d8824" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
RDP into DC-1.

Click on the Windows icon in the lower-left corner.

Select Server Manager.

In Server Manager, click Add roles and features.

Click Next until you reach Server Roles.

Enable Active Directory Domain Services.

Click Add Features.

Click Next until you reach the Confirmation page.

Check the Restart box, then click Yes.

Click Install to begin the installation process.
</p>
<br />

<h2>Step 2: Promote DC-1 to a Domain Controller</h2>

<p>
<img src="https://github.com/user-attachments/assets/da0f5b42-f7fe-4fd1-b3e6-2d6e94a13242" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
In Server Manager, click the flag in the upper-right corner.

Select Promote this server to a domain controller.

In the new window that appears, select Add a new forest.

Name the forest mydomain.com, then click Next.

Fill out the Password field, then click Next.

Uncheck Create DNS delegation, then click Next.

Continue clicking Next until you see the Install button light up.

Click Install to begin the promotion process.

The server will automatically restart and log you out.

Log back in using mydomain.com\username (e.g., mydomain.com\labuser).
</p>
<br />

<h2>Step 3: Create Organizational Units in Active Directory</h2>

<p>
<img src="https://github.com/user-attachments/assets/afb82a76-3a01-4a3f-ba6f-b023d9105827" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Once logged into DC-1, click the Search bar and type Active Directory Users and Computers.

Expand mydomain.com.

Right-click mydomain.com, hover over New, and then select Organizational Unit.

Type _EMPLOYEES URGENT (case-sensitive) and click OK.

Create another Organizational Unit called _ADMINS (all caps, with the underscore).

Right-click mydomain.com and click Refresh.
</p>
<br />

<h2>Step 4: Create a User in the _ADMINS Folder</h2>

<p>
<img src="https://github.com/user-attachments/assets/b6e21f03-a21c-4424-867a-17d7b9b4ecd1" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Navigate to the _ADMINS folder in Active Directory Users and Computers.

Right-click the _ADMINS folder, hover over New, and select User.

Enter the following details:

First name: Jane
Last name: Doe
User logon name: jane_admin
Click Next.

Set the Password.

Deselect User must change password at next login.

Select Password never expires (for the sake of the lab, not practical in real scenarios).

Click Next, then click Finish.
</p>
<br />

<h2>Step 5: Add the User to the Domain Admins Group</h2>

<p>
<img src="https://github.com/user-attachments/assets/0717a231-b344-4d28-a976-aaa410747dec" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Right-click the user jane_admin that we just created.

Click Properties.

Navigate to the Members Of tab.

Click Add.

Type Domain Admins.

Click Check Names to verify the group.

Click OK.

Click Apply, then click OK to finalize.
</p>
<br />

<h2>Step 6: Connect Client-1 to the Domain</h2>

<p>
<img src="https://github.com/user-attachments/assets/dec62f67-681a-4769-9925-75c29611abdf" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
On DC-1, right-click the Windows icon in the lower-left corner and select Run.

Type logoff, then press Enter to log off.

Reconnect to DC-1, but log in as mydomain.com\jane_admin (e.g., mydomain.com\jane_admin).

Once logged in to DC-1, switch to Microsoft Azure and connect to Client-1 using the credentials you set up for the VM.

On Client-1, right-click the Windows icon and select System.

In the System window, click About.

Click Rename this PC (Advanced).

Under the Computer Name tab, click Change.

Select Domain and type mydomain.com, then click OK.

When prompted, log in with:

Username: mydomain.com\jane_admin
Password: The password you set for jane_admin.
Minimize the System window (it may pop up behind the confirmation dialog).

Click OK, and the computer will restart to apply the changes.
</p>
<br />

<h2>Step 7: Organize Client Machines in Active Directory</h2>

<p>
<img src="https://github.com/user-attachments/assets/a5713e87-2d15-47c8-b1ca-3b20c8a3142c" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Log back into DC-1.

Use the Search bar on the left-hand side and type Active Directory Users and Computers.

Expand mydomain.com.

Right-click mydomain.com, hover over New, and select Organizational Unit.

Name the Organizational Unit _CLIENTS (case-sensitive), then click OK.

Click on Computers in the left-hand menu.

Drag Clients into the _CLIENTS Organizational Unit.

When prompted, click Yes to confirm.

Right-click mydomain.com and select Refresh.
</p>
<br />
