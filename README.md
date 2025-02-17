<p align="center">
<img src="https://github.com/user-attachments/assets/212f28e4-27b8-46f3-8b80-118a6616ea4a"/>
</p>

<h1>Practicing DNS within Azure VMs</h1>
This article describes the steps taken when practicing DNS in a Virtual Machine using Azure.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

**A-Record Steps**
- Logged into both the Windows 10(Client-1) and Windows Server(Domain Controller) Virtual Machines as an admin([Click here to find out more about how these were made](https://github.com/JheovauhniThompson1/AD-config))
- Attempted to ping "Wire" from Client-1 and observed the result
- Created a A-record in Domain Controller called "wire"
- Went back to Client-1 and tried pinging "wire" again.

**local DNS cache Steps**
- Went back to Domain Controller and changed wire's record addresss to 8.8.8.8
- Went back to Client-1 and attempted to ping wire
- Observed the local cache(using ipconfig/displaydns)
- Flushed the current DNS cache in Client-1
- Attempted to ping wire again

<h2>Deployment and Configuration Steps</h2>

<p>
<img src="https://github.com/user-attachments/assets/9cc56003-0803-47c8-958b-7b5991f7109f"/>
</p>
<p>
During the osTicket Project, I had an issue in which I was fully locked out of all of my accounts, including the admin account. To resolve this, I had to enter MySQL and run code under "Query" to change my admin password.
</p>
<br />

<p>
<img src="https://github.com/user-attachments/assets/fbd73c85-dfbf-4adc-b746-dd76819d70c3"/>
</p>
<p>
Lastly, I went into the "ost_staff" table to update the Agent's passwords' manually. This can be done by double clicking the "passwd" field. The password entered is encrypted and translates to "welcome".
</p>
<br />

