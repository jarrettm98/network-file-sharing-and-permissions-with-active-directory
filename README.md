<p align="center">
<img src="https://i.imgur.com/Q3YpjDD.png" alt="AD Logo"/>
</p>

<h1>Network File Sharing and Permissions with Active Directory</h1>
This is a tutorial on how to set file sharing and manage access permissions with Active Directory. You should not start this tutorial until you have completed the previous tutorial on how to set up Active Directory and create users. Click this link for the tutorial.

https://github.com/jarrettm98/install-active-directory-create-users

<h2>Technologies Used</h2>

- Microsoft Azure
- Remote Desktop
- Active Directory

<h2>Operating Systems Used</h2>

- Windows Server 2022
- Windows 10

<h2>Prerequisites</h2>

- Create Domain Controller and Client Virtual Machines
- Enable ICMPv4 rules with Windows Defender
- Installing Active Directory
- Create Domain Admin
- Set Client DNS Settings to Domain Controller Private IP Address
- Set up Remote Connection for Domain Users
- Create Domain Users

<h2>Step 1: Set up Network File Sharing Access</h2>

First, log into the Domain Controller with the domain admin account.

![image](https://github.com/jarrettm98/network-file-sharing-and-permissions-with-active-directory/assets/140662793/8bcc72cc-1846-461f-8d0d-7eb44925160a)

Next, log into the Client with one of the domain users created in the last tutorial.

![image](https://github.com/jarrettm98/network-file-sharing-and-permissions-with-active-directory/assets/140662793/87733a8a-c3dc-4110-a523-f45d8760eded)

On the Domain Controller, go to the C:\ drive and create four folders ("read-access", "write-access", "no-access", and "accounting")

![image](https://github.com/jarrettm98/network-file-sharing-and-permissions-with-active-directory/assets/140662793/b9cabc44-3409-4cb8-ba41-c2b4be78f7b2)

Once they are created, highlight the "read-access" folder, then right-click it. Click on properties. Go to the "Sharing" tab and click "Share..."

Now in the text bar type "Domain Users" and click "Add." Leave "Permission Level" as Read and click "Share."

![image](https://github.com/jarrettm98/network-file-sharing-and-permissions-with-active-directory/assets/140662793/bce6a285-2ebe-4f0f-8bdd-70f8fc75a6c0)

Now do the same with "write-access" except choose "Read/Write" Permission Level.

![image](https://github.com/jarrettm98/network-file-sharing-and-permissions-with-active-directory/assets/140662793/1b5ed7a6-06ee-4897-b99d-05da769279d6)

For the "no-access" folder, instead of adding "Domain Users", add "Domain Admins" and give them the "Read/Write" Permission Level. Click the Share button.

![image](https://github.com/jarrettm98/network-file-sharing-and-permissions-with-active-directory/assets/140662793/b8cfb8df-c187-450d-889e-4b275fdb26f4)

The "accountants" folder will be set up later with Active Directory.

Now, go to the Client VM. Open the Run dialog box by holding the Windows key then press "R". in the text box type "\\dc-1" (This should be the name of the Domain Controller just in case you named yours differently)

![image](https://github.com/jarrettm98/network-file-sharing-and-permissions-with-active-directory/assets/140662793/93345914-00ee-4f44-8fae-641a45bfb095)

The folders created on the Domain Controller should all show up. A normal domain user should be able to read any files in "read-access." They should be able to create a file in "write-access". They should not be able to access the "no-access" folder.

![image](https://github.com/jarrettm98/network-file-sharing-and-permissions-with-active-directory/assets/140662793/83272589-6756-4b5d-8ae2-625bbd4775ad)

![image](https://github.com/jarrettm98/network-file-sharing-and-permissions-with-active-directory/assets/140662793/72d55e42-76f8-4875-9530-5063c4371445)

![image](https://github.com/jarrettm98/network-file-sharing-and-permissions-with-active-directory/assets/140662793/1822d959-e239-4130-9063-955ffc74187c)

![image](https://github.com/jarrettm98/network-file-sharing-and-permissions-with-active-directory/assets/140662793/b69d8d5e-128c-40d8-800a-511fdbdca3ef)

<h2>Step 2: Set up Permission Access with Active Directory</h2>

Go back to the Domain Controller. Now go to Server Manager>Tools>Active Directory Users and Computers. In the domain container, create a "Security Group" and name it "ACCOUNTANTS"

![image](https://github.com/jarrettm98/network-file-sharing-and-permissions-with-active-directory/assets/140662793/6804d1d9-5666-426b-9679-42a5459e51c6)

Now, go the accounting folder created, right-click it, then click on Properties. Go to the Sharing tab and click Share... Type "ACCOUNTANTS" in the text bar and click Add. Give it a Read/Write Permission level then click Share.

![image](https://github.com/jarrettm98/network-file-sharing-and-permissions-with-active-directory/assets/140662793/e357f3d4-ac13-458d-a903-caa6ecb35c71)

In Active Directory Users and Computers, find the domain user that is currently logged in and right-click the user. Next, click Properties.

![image](https://github.com/jarrettm98/network-file-sharing-and-permissions-with-active-directory/assets/140662793/9251f4c5-c2ec-4b0f-89ea-2e1f676d5f09)

Click the "Member Of" tab, then click "Add".

![image](https://github.com/jarrettm98/network-file-sharing-and-permissions-with-active-directory/assets/140662793/cd49e12d-45b3-4008-be7f-2820c32b6be4)

Type "ACCOUNTANTS" and click "Check Names". Click OK. Now click "Apply".

![image](https://github.com/jarrettm98/network-file-sharing-and-permissions-with-active-directory/assets/140662793/dcf37e92-1c90-47a1-9d81-3c99aaa01085)

Now go to the Client and try to access the accounting folder. It should still refuse access.

![image](https://github.com/jarrettm98/network-file-sharing-and-permissions-with-active-directory/assets/140662793/8e3d776b-d608-4d52-94a6-07101bcf74ab)

A simple relog should fix this. Log back into the same domain user granted access to the Accountants Security Group and accountants folder.

Open the Run dialog box by holding the Windows key then press "R". in the text box type "\\dc-1" to access the network files again.

Now the accounting folder should be accessible. Create a file to see the write access as well.

![image](https://github.com/jarrettm98/network-file-sharing-and-permissions-with-active-directory/assets/140662793/1f6441d0-fbc1-4622-b825-0d08d24a2262)

Congrats! You completed this tutorial. Hope you learned more about Network File Sharing and Permissions given by Active Directory.
