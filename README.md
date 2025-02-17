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

<h2>High-Level Practice Steps</h2>

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

<h2>Practice Steps</h2>

<p>
<img src="https://github.com/user-attachments/assets/f07458f3-deca-4bda-b99c-4857555ef490"/>
</p>
<p>
For this repository, the first step I took was logging into both the Domain Controller and Client-1 (Windows 10 VM) as jane_admin. I then opened PowerShell and attempted to ping "wire." After a few seconds, I received an error message stating that there was no entity called "wire."
</p>
<br />

<p>
<img src="https://github.com/user-attachments/assets/6dcbaba5-3f3c-42f3-b5db-5fcd8f3ee59f"/>
</p>
<p>
Since "wire" didn’t exist yet, I decided to create it on the Domain Controller. First, I opened DNS Manager and navigated to the Forward Lookup Zone, where my domain name was located. I then right-clicked on the domain and created a new Host (A) Record called "wire," mapping it to the Domain Controller's private IP address.
</p>
<br />

<p>
<img src="https://github.com/user-attachments/assets/0b664de4-8c76-4e51-8074-f1d32bf807e1"/>
<img src="https://github.com/user-attachments/assets/6505174e-671a-4c94-b689-37bac70b3290"/>
</p>
<p>
Returning to Client-1, I attempted to ping "wire" again, and this time it was successful. I also ran nslookup to check the result, and sure enough, the Domain Controller's IP address was displayed as "wire's" IP.
</p>
<br />
