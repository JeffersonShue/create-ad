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

- [Creating Virtual Machines in the Cloud](https://github.com/joshuaheck1/VM-creation)
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
<img width="800" alt="AD7" src="https://github.com/user-attachments/assets/3324e347-dda1-4ace-bb71-5417daaa7673" />

</p>

<p>
- In Azure, create a new Resource Group and two Virtual Machines. Ensure the VMs are in the same Virtual Network and Location (Region). Reference the project above in Prerequisites if you need a quick reminder.
<p>- Name the first VM "DC-1" (Domain Controller), set the image to Windows Server 2022, and at least (2 vcpus, 8 GiB memory) for size.</p>
<p>- Name the second VM "Client-1", set the image to Windows 10, and at least (2 vcpus, 8 GiB memory) for size.</p>
<p>- This would be a good time to note the Public IP addresses of both VMs and the Private IP for DC-1. We will need them later for RDP.</p>
<br />

<p>
<img width="800" alt="AD8" src="https://github.com/user-attachments/assets/77d02814-7bb0-4f8e-a1f9-1ee2e5598dfc" />
</p>

<p>
- From Virtual machines, click on DC-1 and select Network settings. Then, click on Network interface / IP configuration as shown in Figure 2.
</p>
<br />

<p>
<img width="850" alt="AD10" src="https://github.com/user-attachments/assets/cc03b9ca-0954-4762-a004-75a2908508f4" />
<p>
- In IP configurations, locate and click on "ipconfig1". Under Private IP address settings, change Allocation to "Static". Click Save. (Note the Private IP while we're here if you forgot earlier).
<p>- We set the Private IP to Static because we do not want this IP address to change. Dynamic = Constantly changing and Static = Stay same. DC-1 will be our Server for upcoming AD Projects. 
</p>
<br />

<p>
<img width="850" alt="AD11" src="https://github.com/user-attachments/assets/0cb1a9c1-0f68-4030-8383-b0add4594a84" />
 </p>
<p>
-You will be back in the IP configurations screen after clicking Save. Here, we can confirm our changes were saved by looking next to the Private IP address.
</p>
<br />

<p>
<img width="850" alt="AD14" src="https://github.com/user-attachments/assets/5eef23b7-ecfb-4b1c-aa60-8dc9a5d20d6d" />
 </p>
<p>
- Minimize Azure for now and hop over to Remote Desktop (Windows) or Windows App (MacOS). Use DC-1's Public IP address and create a new RDP connection.
<p>- Once logged into DC-1, right-click the Start Menu and open Run. Type in wf.msc and click OK.</p>
<p>- This will open the firewall settings for DC-1. (NOTE: Server Manager Dashboard should showing once logged into DC-1. If not, or if Windows is showing as normal, there is an issue. Make sure you are in the right VM and/or check Azure to verify the DC-1 VM was setup correctly).</p>
</p>
<br />

<table>
  <tr>
    <td>
      <img width="1000" alt="AD15" src="https://github.com/user-attachments/assets/bb4d885d-527a-4e07-9882-d9ab13889204" />
    </td>
    <td>
      <img width="1000" alt="AD16" src="https://github.com/user-attachments/assets/2ce39e9f-e408-4ccf-8c6e-abf9ec8e22b2" />
    </td>
  </tr>
</table>
<p>
  -Select Windows Defender Firewall Properties. Then for Domain, Private, and Public Profiles, change Firewall state to Off. (You will need to do this for each tab). Click Apply and then OK to save the changes.
</p>
<br />

<table>
  <tr>
    <td>
      <img width="1000" alt="AD18" src="https://github.com/user-attachments/assets/86c1c816-3a80-4687-a39f-cb723df05860" />
    </td>
    <td>
      <img width="1000" alt="AD19" src="https://github.com/user-attachments/assets/2341ccd3-6165-48a1-8663-f1c2a1f08629" />
    </td>
  </tr>
</table>
<p>
  - Head back to Azure and go to Virtual machines. Click on Client-1. Select Network settings and then Network inferace / IP configuration. See Figure 8.
</p>
<p>
  - Select DNS servers. Click Custom and enter DC-1's Private IP under DNS Server.(Good thing we noted the IPs earlier.😁) Click Save. See Figure 9.
</p>
<br />

<p>
<img width="850" alt="AD22" src="https://github.com/user-attachments/assets/07428d49-90b7-4573-b1f4-a4441a1e794e" />
 </p>
<p>
- Since we changed the DNS Server for Client-1, we need to restart the VM. Run,🏃‍♂️, back to the Virtural machines main screen and restart Client-1.  
</p>
<p>- Check the box next to Client-1, click Restart, and tell Azure Yes.</p>
<br />

<p>
<img width="850" alt="AD23" src="https://github.com/user-attachments/assets/abe07877-230d-43fd-9678-57fce300ed30" />
 </p>
<p>
- Once Client-1 finishes restarting, grab your notes with the Public IP adrresses, and use Client-1's Public IP to login using RDP. (Don't forget username and password.) 😉</p>
<p>-After you get logged in to Client-1, open up PowerShell. </p>
<br />

<p>
<img width="850" alt="AD24" src="https://github.com/user-attachments/assets/fb7e0ea1-3cba-459d-a6b4-f2f9350ff25f" />
 </p>
<p>
- From PowerShell, we are going to test our connection from Client-1 to DC-1 (Our Server) with command ping 10.0.0.4 and press enter. This shows us that both VMs are on the same Virtual Network and we disabled DC-1's firewall correctly.
</p>
<br />

<p>
<img width="850" alt="AD25" src="https://github.com/user-attachments/assets/4fce9965-3fbb-4541-a4f6-fcce4c33dfad" />
 </p>
<p>
- Now for our final act of the eveving, we will make sure the DNS Server of Client-1 is set to DC-1's Private IP address. In PowerShell use the command ipconfig /all and press enter. 🪄 Abracadabra and there it is folks! 
</p>
<br />

<h2>✅ Conclusion</h2>

<p>
This concludes our project. We have successfully built the infrastructure we need for Active Directory in Azure. We will use this build to complete a few more AD projects. Next, we will deploy Active Directory. Isn't Cloud Computing cool? Don't forget to Stop (turn off) the VMs in Azure. As always, Thank You for your time and viewing this Project. We'll see you on the next one! 😎      
</p>
<br />
