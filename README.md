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

[pic 3.5]
<br><br>

- Click the dropdown for `Forest: mydomain.com` → Then for `Domains` → Then for `mydomains.com` → Select `Default Domain Policy`.

[pic 3.6]

- Right click `Default Domain Policy` and select `Edit`.
- Click the dropdown for `Computer Configuration` → `Policies` → `Windows Settings` → `Security Settings` → `Account Policies` → then click `Account Lockout Policy`.
- Double click `Account lockout threshold` → Set the number to five → Click `Apply` → Click `OK` → Click `OK` again.

[pic 3.7]

---

### Step 2 - Force Update for Group Policy on Client VM
(why)

First, logon to Client VM using the Admin user account.

- From the start menu open `Command Prompt` and type `gpupdate /force`.

[pic 3.8]
<br><br>

- Logout of the Client VM

---

### Step 3 - Dealing With Account Lockouts
(common it support)

Next, lets attempt to logon to the Client VM using one of the Employee User accounts you just created but used the **wrong** password 5+ times to simulate an account lockout.

[pic 3.9]
<br><br>

Return to you DC-1 VM open Active Directory Users and Computers

Select the user with the account lockout and click the `Account` tab and view that the account is locked out.

[pic 4.0]
<br><br>

- Unlock the account by checking the box → Click `Apply` → Click `OK`.
- Attempt to Remote Desktop into the Client VM unsing the correct password → Note that the unlocking the account was successful.
***To reset the users password right click on their name and select `Reset Password`, you can also unlock the account from here.***

---

### Step 4 - Disable Accounts within Active Directory

Choose one of the employee users you created and disable their account. It can be the same one you just used for the password lockout or another user.

- Right click the users name and select `Disable Account`.
- Note the small down arrow next to their icon now.

[pic 4.1]
<br><br>

- Attempt to logon to the Client VM using the disabled users account and note the error message.

[pic 4.2]
