<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Configure Group Policy and Practicing Workflows Inside Active Directory</h1>

This tutorial covers configuring **Group Policy** and praciticg basic workflows within AD DS.

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Command Prompt

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (22H2)

<h2>Prerequisite</h2>

Open and log in to Azure: [https://azure.microsoft.com/](https://azure.microsoft.com/)

## Table of Contents
- [Step 1 - Configure Account Lockouts in Group Policy Management](#step-1---configure-account-lockouts-in-group-policy-management)
- [Step 2 - Force Update for Group Policy on Client VM](#step-2---force-update-for-group-policy-on-client-vm)
- [Step 3 - Dealing With Account Lockouts](#step-3---dealing-with-account-lockouts)
- [Step 4 - Disable Accounts within Active Directory](#step-4---disable-accounts-within-active-directory)


---

### Step 1 - Configure Account Lockouts in Group Policy Management
(gpo is..)


First, logon to DC-1 using your Admin User account.

- Right click the start menu select `Run` → Type `gpmc.msc` → Click `OK`.

<img width="395" height="192" alt="3 5 group policy run" src="https://github.com/user-attachments/assets/c4510259-c0db-4123-a450-a27f46d02a10" />
<br><br>

- Click the dropdown for `Forest: mydomain.com` → Then for `Domains` → Then for `mydomains.com` → Select `Default Domain Policy`.

<img width="942" height="581" alt="3 6 default domian policy" src="https://github.com/user-attachments/assets/78e16f67-2ca6-42fa-a06a-c3257ac7a780" />
<br><br>

- Right click `Default Domain Policy` and select `Edit`.
- Click the dropdown for `Computer Configuration` → `Policies` → `Windows Settings` → `Security Settings` → `Account Policies` → then click `Account Lockout Policy`.
- Double click `Account lockout threshold` → Set the number to five → Click `Apply` → Click `OK` → Click `OK` again.

<img width="1073" height="738" alt="3 7 account lockout attempts" src="https://github.com/user-attachments/assets/56fbd688-01f8-474f-998a-36166f6cd246" />

---

### Step 2 - Force Update for Group Policy on Client VM
(why)

First, logon to Client VM using the Admin user account.

- From the start menu open `Command Prompt` and type `gpupdate /force`.

<img width="1138" height="234" alt="3 8 gpupdate" src="https://github.com/user-attachments/assets/e76ced04-e740-4085-8dbb-1802cc9ce7b7" />
<br><br>

- Logout of the Client VM.

---

### Step 3 - Dealing With Account Lockouts
(common it support)

Next, lets attempt to logon to the Client VM using one of the Employee User accounts you just created but used the **wrong** password 5+ times to simulate an account lockout.

<img width="557" height="491" alt="3 9 locked out" src="https://github.com/user-attachments/assets/0e80dd39-7739-4844-84f8-7341a54f3356" />
<br><br>

Return to you DC-1 VM open Active Directory Users and Computers

Select the user with the account lockout and click the `Account` tab and view that the account is locked out.

<img width="408" height="552" alt="4 0 locked out" src="https://github.com/user-attachments/assets/871fa517-ef81-41f6-9603-7d2fa72ddf0c" />
<br><br>

- Unlock the account by checking the box → Click `Apply` → Click `OK`.
- Attempt to Remote Desktop into the Client VM unsing the correct password → Note that the unlocking the account was successful.
***To reset the users password right click on their name and select `Reset Password`, you can also unlock the account from here.***

---

### Step 4 - Disable Accounts within Active Directory

Choose one of the employee users you created and disable their account. It can be the same one you just used for the password lockout or another user.

- Right click the users name and select `Disable Account`.
- Note the small down arrow next to their icon now.

<img width="347" height="423" alt="4 1 disable acct" src="https://github.com/user-attachments/assets/0a8c3622-13a7-47b4-8d56-e751534c1016" />
<br><br>

- Attempt to logon to the Client VM using the disabled users account and note the error message.

<img width="557" height="486" alt="4 2 disabled" src="https://github.com/user-attachments/assets/09d57648-0732-4e47-9abf-46b4f3b06df9" />
