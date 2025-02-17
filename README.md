<p align="center">
<img src="https://github.com/user-attachments/assets/212f28e4-27b8-46f3-8b80-118a6616ea4a"/>
</p>

<h1>Practicing DNS within Azure VMs</h1>
This article describes the steps taken when practicing DNS in a Virtual Machine using Azure.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- DNS Manager
- PowerShell

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
**A-Record Steps**

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

**local DNS cache Steps**
<p>
<img src="https://github.com/user-attachments/assets/eced10e0-67f4-4ce1-9955-954f7474c897"/>
</p>
<p>
To continue where I left off, I returned to the Domain Controller and changed "wire's" IP address from the Domain Controller's IP to 8.8.8.8. I then attempted to ping "wire" again, and received a response. 
</p>
<br />

<p>
<img src="https://github.com/user-attachments/assets/eced10e0-67f4-4ce1-9955-954f7474c897"/>
<img src="https://github.com/user-attachments/assets/9dec7e74-4938-450e-876e-72fb9ce273f9"/>
</p>
<p>
To continue where I left off, I returned to the Domain Controller and changed "wire's" IP address from the Domain Controller's IP to 8.8.8.8. I then attempted to ping "wire" again, and received a response. 
</p>
<br />


<p>
<img src="https://github.com/user-attachments/assets/b595c05d-b17f-4388-9bd5-c36f258ff34d"/>
</p>
<p>
This happened because the computer had previously cached the IP address from an external source (in this case, the Domain Controller). When the IP address is changed, the cached DNS entry needs to be flushed to reflect the new address, which I did using ipconfig /flushdns. To verify that the cache was cleared, I ran ipconfig /displaydns, and no entries were found.
</p>
<br />

![image]()

<p>
<img src="https://github.com/user-attachments/assets/49e3a968-4b27-461a-a226-1b6273e6ea50"/>
</p>
Lastly, I attempted to ping "wire" again, and it worked. I then checked its IP address by running ipconfig /displaydns in PowerShell, and confirmed that the IP had successfully changed from 10.0.0.4 to 8.8.8.8!
</p>
<br />
