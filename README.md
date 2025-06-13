<table>
  <tr>
    <td>
      <img width="1000" alt="ADS1" src="https://github.com/user-attachments/assets/6764e034-271e-4809-8e91-bb25dba7ba17" />
    </td>
    <td>
      <img width="1000" alt="ADS2" src="https://github.com/user-attachments/assets/2dfb8569-f306-4f94-a01a-6790869d3475" />
    </td>
  </tr>
</table>

<h1>Creating Active Directory Infrastructure in the Cloud (Azure)</h1>
This tutorial outlines the creation of an Active Directory infrastructure within Azure. We will use this build to deploy and configure Active Directory in a future project. <br />

<h2>⚠️ Prerequisite</h2>

- [Creating Virtual Machines in the Cloud](https://github.com/jeffersonshue/configure-ad)
<p>(Reference this project for help creating Virtual Manchines if needed.)</p>

<h2>💻 Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>👨‍💻 Operating Systems Used </h2>

- macOS Sequoia
- Windows Server 2022
- Windows 10 (21H2)


<h2>⚙️ Deployment and Configuration Steps</h2>

<p>
<img width="800" alt="AD7" src="https://github.com/user-attachments/assets/ed0e23c0-b02a-4363-a979-aa40e6dfd400" />


</p>

<p>
- In Azure, create a new Resource Group and two Virtual Machines. Ensure the VMs are in the same Virtual Network and Location (Region). 
<p>- Name the first VM "dc-1" (Domain Controller), set the image to Windows Server 2022, and at least (2 vcpus, 8 GiB memory) for size.</p>
<p>- Name the second VM "client-1", set the image to Windows 10, and at least (2 vcpus, 8 GiB memory) for size.</p>
<br />

<p>
<img width="800" alt="AD8" src="https://github.com/user-attachments/assets/9d2d73d9-a901-47a3-8b09-e173b228f2e7" />
</p>


<p>
- From Virtual machines, click on DC-1 and select Network settings. Then, click on Network interface / IP configuration as shown in Figure 2.
</p>
<br />

<p>
<img width="850" alt="AD10" src="https://github.com/user-attachments/assets/7b9c9a6f-525a-4bcb-a713-8985c93d2361" />
<p>

- In IP configurations, locate and click on "ipconfig". Under Private IP address settings, change Allocation to "Static". Click Save.
<p>- We set the Private IP to Static because we do not want this IP address to change.
</p>
<br />

<p>
<img width="850" alt="AD14" src="https://github.com/user-attachments/assets/d0c58bc4-f43e-4997-aeb9-2e38acf83bec" />
 </p>

<p>
- Minimize Azure for now and hop over to Remote Desktop (Windows) or Windows App (MacOS). Use dc-1's Public IP address and create a new RDP connection.
<p>- Once logged into dc-1, right-click the Start Menu and open Run. Type in wf.msc and click OK.</p>
<p>- This will open the firewall settings for dc-1. Server manager should open automatically if you're on the domain controller server.</p>
</p>
<br />

<p> <img width="1000" alt="AD15" src="https://github.com/user-attachments/assets/d1785d71-ecc3-4d75-85e5-45bc6492f565" />
</p>

  -Select Windows Defender Firewall Properties. Then for Domain, Private, and Public Profiles, change Firewall state to Off. (You will need to do this for each tab). Click Apply and then OK to save the changes.
</p>
<br />

<p> <img width="1000" alt="AD18" src="https://github.com/user-attachments/assets/81e76271-ddf1-424c-b633-a9221cc40bc0" />
</p>

  - Head back to Azure and go to Virtual machines. Click on client-1. Select Network settings and then Network inferace / IP configuration. 
</p>
<p>
  - Select DNS servers. Click Custom and enter dc-1's Private IP under DNS Server.
</p>
<br />

<p>
<img width="850" alt="AD22" src="https://github.com/user-attachments/assets/593d9a4a-af1f-4196-84da-4f9f1904767d" />
 </p>

<p>
- Since we changed the DNS Server for client-1, we need to restart the VM. Go back to the Virtual machines main screen and restart client-1.  
</p>
<p>- Check the box next to client-1, click Restart, and tell Azure Yes.</p>
<br />

<p>
<img width="850" alt="AD23" src="https://github.com/user-attachments/assets/abe07877-230d-43fd-9678-57fce300ed30" />
 </p>
<p>
- Once client-1 finishes restarting, grab your notes with the Public IP adrresses, and use client-1's Public IP to login using RDP.</p>
<p>-After you get logged in to client-1, open up PowerShell. </p>
<br />

<p>
<img width="850" alt="AD24" src="https://github.com/user-attachments/assets/fb7e0ea1-3cba-459d-a6b4-f2f9350ff25f" />
 </p>
<p>
- From PowerShell, we are going to test our connection from client-1 to dc-1 (Our Server) with command ping 10.0.0.4 and press enter. This shows us that both VMs are on the same Virtual Network and we disabled dc-1's firewall correctly.
</p>
<br />

<p>
<img width="850" alt="AD25" src="https://github.com/user-attachments/assets/4fce9965-3fbb-4541-a4f6-fcce4c33dfad" />
 </p>
<p>
- Now for our final step, we will make sure the DNS Server of client-1 is set to dc-1's Private IP address. In PowerShell use the command ipconfig /all and press enter. 
</p>
<br />

<h2> Conclusion</h2>

<p>
This concludes our project. We have successfully built the infrastructure we need for Active Directory in Azure.
</p>
<br />
