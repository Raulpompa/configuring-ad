<p align="center">
<img src="https://i.imgur.com/cvTElbW.png" alt="ad logo"/>
</p>
<h1>Creating Users, Group Policy, and Managing Accounts in Azure</h1>
<h2>Description</h2>
<p>This project will showcase how to set up Remote Desktop access for standard (non-admin) users, automate the process of creating user accounts using PowerShell, and handle group policy management. I’ll also explore account lockout scenarios and log monitoring to reflect real-world IT challenges. Come along as I explore Active Directory deployment and strengthen system administration skills!</p>

<h2>Environments and Utilities Used</h2>

- Microsoft Azure
- Virtual Machines
- Remote Desktop Connection
- Active Directory

<h2>Operating Systems Used</h2>

- Windows Server
- Windows 10

<h2>Implementation Process</h2>
<p>
  <p>Begin by accessing Client-1 via Remote Desktop Connection, logging in as the domain administrator (jane_admin).</p>
<img src="https://i.imgur.com/fUaub8X.png" alt="client-1 rdp"/>
</p>
<p>
  <p>To enable Remote Desktop access for standard (non-admin) users, right-click the Start button and select System. On the right-hand panel, click Remote Desktop, then choose Select users that can remotely access this PC.</p> 
<img src="https://i.imgur.com/e1FrSIv.png" alt="rdp non-admin"/>
</p>
<p>
  <p>Click on "Domain Users," then select "Check Names," and press "OK" twice. Now, all users in the domain are granted Remote Desktop access to this client.</p>
<img src="https://i.imgur.com/Wd3CIH5.png"  alt="grant rdp access"/>
</p>
<p>
  <p>Next, we’ll use PowerShell to create multiple user accounts. Begin by logging into the Domain Controller (DC) with our admin account, jane_admin.</p>
<img src="https://i.imgur.com/fuJPIpe.png" alt="login to DC-1 PS"/>
</p>
<p>
  <p>After logging in, launch PowerShell ISE with administrative privileges and create a new script file to begin.</p> 
<img src="https://i.imgur.com/EL25wsH.png" alt="open ISE powershell on admin"/>
</p>
<p>
  <p>Press Ctrl + S and save the file using the following naming convention:</p>
<img src="https://i.imgur.com/2V0Ympj.png"  alt="save file as create-users"/>
</p>
<p>
  <p>Now, paste the user creation script into the top section of the PowerShell ISE window, then click the "Run" button (the green play icon) located on the top toolbar.</p>
<img src="https://i.imgur.com/7rA8h71.png" alt="paste script and run"/>
</p>
<p>
  <p>PowerShell will execute the script, automatically generating random user accounts and placing them in the Organizational Unit (OU) we previously created called "_EMPLOYEES." To verify, open "Active Directory Users and Computers," navigate to mydomain.com > _EMPLOYEES, and you'll see the new users listed. Choose one of these accounts, then log into client-1 using that username and the default password set by the script: "Password1."</p> 
<img src="https://i.imgur.com/kFSt9Dx.png" alt="creating users using powershell"/>
</p>
<p>
  <p>Now, sign out of Jane's account on client-1 to proceed with logging in as one of the newly created users.</p>
<img src="https://i.imgur.com/OQzv1sP.png"  alt="sgin out of Client-1"/>
</p>
<p>
  <p>Log back into client-1 using one of the newly created user accounts. Be sure to specify the domain context by entering the username in this format: mydomain.com\username.</p>
<img src="https://i.imgur.com/8in1qqN.png" alt="log in with created user"/>
</p>
<p>
  <p>Once logged in, open File Explorer and navigate to C: > Users. You’ll see a folder for the current user, as well as folders for any other users who have previously signed into this client. However, you won’t be able to open those other folders, since standard users don’t have the necessary permissions to access them.</p> 
<img src="https://i.imgur.com/cJo9O5L.png" alt="file explorer"/>
</p>
<p>
  <p>Now, log out of this user account, as we’ll be configuring an account lockout Group Policy next. After setting the policy, we’ll test it by attempting to lock this user out through repeated failed login attempts.</p>
<img src="https://i.imgur.com/oQkHCth.png"  alt="user lockout"/>
</p>
<p>
  <p>Return to the Domain Controller (DC), right-click the Start button, select Run, then type gpmc.msc and press Enter to open the Group Policy Management Console.</p>
<img src="https://i.imgur.com/4eTkbX9.png" alt="open gpm console"/>
</p>
<p>
  <p>In the Group Policy Management Console, go to Domains > mydomain.com, and click on Default Domain Policy.</p> 
<img src="https://i.imgur.com/78L2XDo.png" alt="configuring domain policy"/>
</p>
<p>
  <p>Under Computer Configuration, expand Policies > Windows Settings > Security Settings, then select Account Lockout Policy to view and configure the lockout settings.</p>
<img src="https://i.imgur.com/YaqtFnG.png"  alt="configure lockout settings"/>
</p>
<p>
  <p>Next, double-click "Account lockout threshold", set it to 5 invalid login attempts, and then click Apply to save the setting.</p>
<img src="https://i.imgur.com/izwmTil.png" alt="5 login attempts"/>
</p>
<p>
  <p></p> 
<img src="https://i.imgur.com/09yJRI9.png" alt="5"/>
</p>
<p>
  <p>To confirm the change, go back to the Group Policy settings, scroll down, and look under the Account Lockout Policy section. You should see that the Account lockout threshold is now set to 5 invalid attempts.</p>
<img src="https://i.imgur.com/psPJj4R.png"  alt="policy check"/>
</p>
<p>
  <p>Although the policy will update automatically over time, you can force it to apply right away. Sign into client-1 using the admin account, open the Command Prompt, and type: gpupdate /force, then press Enter. This will refresh the Group Policy settings on the client.</p>
<img src="https://i.imgur.com/MqsAORu.png" alt="gpupdate/force"/>
</p>
<p>
  <p></p> 
<img src="https://i.imgur.com/GRSEAhc.jpeg" alt="command prompt"/>
</p>
<p>
  <p></p>
<img src=""  alt=""/>
</p>
<p>
  <p></p>
<img src="" alt=""/>
</p>
<p>
  <p></p> 
<img src="" alt=""/>
</p>
<p>
  <p></p>
<img src=""  alt=""/>
</p>
<p>
  <p></p>
<img src="" alt=""/>
</p>
<p>
  <p></p> 
<img src="" alt=""/>
</p>
<p>
  <p></p>
<img src=""  alt=""/>
</p>
<p>
  <p></p>
<img src="" alt=""/>
</p>
<p>
  <p></p> 
<img src="" alt=""/>
</p>
<p>
  <p></p>
<img src=""  alt=""/>
</p>
