# Azure-AD-Connect-Synchronization-with-On-Premises-Active-Directory-Project

# Project Overview

This project demonstrates the synchronization of an on-premises Active
Directory (AD) with Azure Active Directory (Azure AD) using Azure AD
Connect. The goal is to allow seamless integration and user management
between on-premises and cloud environments.

## Architecture Overview

### Infrastructure Setup

- **Azure Virtual Network** with two Virtual Machines (VMs):

  1.  **VM 1: Domain Controller (DC)** – Hosts the on-premises Active
      Directory.

  2.  **VM 2: Azure AD Connect** – Handles synchronization between the
      on-premises AD and Azure AD.

- **Domain Name**: clouddirectory.solutions.

- **Microsoft Entra User** **with Global Admin permission:**
  Entraconnect-user

- **Users Migrated**: UserL, UserM, UserP, and UserV.

**Architecture Diagram**

Diagram displaying Azure Virtual Network, VMs, and their connectivity.

![image1](https://github.com/user-attachments/assets/822dc6a0-c485-4be0-9cce-55ea2c163ecf)


## Creating a User with Global Administrator Permission in Azure Portal

### Sign in to Azure Portal

- Go to [Azure Portal](https://portal.azure.com).

- Log in with your Azure account credentials.

![image2](https://github.com/user-attachments/assets/ad3f45d4-e3a0-49a4-91fb-f2555c08e9ea)


### Navigate to Microsoft Entra ID

- In the left-hand menu, select Microsoft Entra ID.

![image3](https://github.com/user-attachments/assets/05df2835-6fcf-4370-bc8e-c03606b7e836)

- If it’s not visible, click More Services and search for Azure Active
  Directory.

### Add a New User

- Under the Manage section, click Users.

> <img src="./media/image4.png" style="width:2.86599in;height:2.86739in"
> alt="A screen shot of a black background Description automatically generated" />

- Click + New user at the top.

![image4](https://github.com/user-attachments/assets/8492d470-9ed7-4cf6-aa85-3664bcdb0db2)


### Fill in User Details

- Select Create user.

- Enter the following details:

  - User principle name:Entraconnect-user

  - Display name: Entraconnect-user

- Set an Initial Password (Azure generates one automatically, but you
  can change it).Ensure to keep it

![image5](https://github.com/user-attachments/assets/248cfc8a-de01-4bac-864d-d4097a563272)


- Click Create**.**

### Assign Global Administrator Role

- Select Assigment.

- Click Add role in the lower pane.

- Search for Global Administrator and select it.

![image7](https://github.com/user-attachments/assets/eb1b1393-f209-4ef6-ba32-bd17f4bff1d5)


- Click review+create.

![image8](https://github.com/user-attachments/assets/3a38766a-9d88-4fba-855e-970383bb6532)


### Verify Role Assignment

- Go back to the user profile and ensure the Global Administrator role
  is listed under Assigned roles.

![image9](https://github.com/user-attachments/assets/296abc6a-5a5e-4b40-b4fe-74e5ac3659cb)


## Setting up the Domain Controller

### Create an Azure Virtual Machine(DomainControllerVm)

1.  Log in to the **Azure Portal**.

2.  Navigate to **Virtual Machines** and click **+ Create**.

3.  Fill in the required details: Resource Group, VM Name, Region, and
    Image (Windows Server 2019).

4.  Configure the network settings and create the VM.

Azure VM creation wizard for the DomainControllerVm

![image10](https://github.com/user-attachments/assets/0f8b581a-fed3-4e51-9d51-9dce95f0ec11)


### Install Active Directory Domain Services (AD DS)

Log on to the DomainControllerVm by downloading the RDP file.

Open **Server Manager**.

Click **Add Roles and Features**.

![image11](https://github.com/user-attachments/assets/c67cbecf-8d42-4d38-b53d-df6b9fdadc96)

Click on Next ( No configuration change is requided)

![image12](https://github.com/user-attachments/assets/afbcce9f-3f48-4539-bc0c-462261995cf4)

Select role-based or feature -based installation. Click on Next.

![image13](https://github.com/user-attachments/assets/490a4549-5a97-4e89-9d07-fd28b9a0f38b)


Click on Next ( No configuration change is requided)

![image14](https://github.com/user-attachments/assets/a77ead6d-1a78-404c-be2c-f4424788ae62)

Select Active Directory Domain Services and proceed with installation.

![image15](https://github.com/user-attachments/assets/3c3de0c3-b353-4e22-b890-9208ec3b571c)

Click on Add Features

![image16](https://github.com/user-attachments/assets/5c118c13-241b-410b-ae83-4c9c094ee3c3)

Select Active Directory Domain Services

![image17](https://github.com/user-attachments/assets/c495dbff-58b4-467e-86f3-e737c5d3a1cd)

Click on Next ( No configuration change is requided)

![image18](https://github.com/user-attachments/assets/5758c2d7-d703-4c78-9cc6-9bb5728ba43d)

Click on Next ( No configuration change is requided)

![image19](https://github.com/user-attachments/assets/ad278e0f-cd18-45b5-83ed-c1b21b897e6f)

Click on Install to commence installation.

![image20](https://github.com/user-attachments/assets/6a7f5fbe-f8a7-4082-a3d7-80fad598a816)

Promote the server to a **Domain Controller**

![image21](https://github.com/user-attachments/assets/63eb32b3-35b4-4b88-9650-91a327b7f58b)

Add a new forest and input the domain name **clouddirectory.solutions**

![image22](https://github.com/user-attachments/assets/021f5ac8-7c70-4dae-abfd-09c76bc4e7c5)

Create a Password for the domain.

![image23](https://github.com/user-attachments/assets/1b04a972-7a5d-4b87-af9b-e391eedc463f)


Click on Next ( No configuration change is requided)

![image24](https://github.com/user-attachments/assets/cf04e0e3-58a0-4640-9443-f8d4df895bcf)


Click on Next ( No configuration change is requided)

![image25](https://github.com/user-attachments/assets/097cb317-91aa-43e3-a259-12d2702877fe)


Click on Next ( No configuration change is requided)

![image26](https://github.com/user-attachments/assets/b4731de7-9c4c-41cc-89ef-3719d3ac2421)


Click on Next ( No configuration change is requided)

![image27](https://github.com/user-attachments/assets/e41a16d9-9085-4436-8f73-0436c822b910)


Click on install to commence installation. The DomainControllerVm will
reboot to apply the new setting.

![image28](https://github.com/user-attachments/assets/207503bd-a7ef-4079-9c8e-9e66a768e470)


Server Manager displaying the new computer name and domain name.

![image29](https://github.com/user-attachments/assets/2f296731-fe04-414a-a3f7-37d69c99542b)


### Create Users in Active Directory

Click on Tools and Open Active Directory Users and Computers.

![image30](https://github.com/user-attachments/assets/81f40b3d-846c-40d3-ba4b-4f64f8997673)


Right-click on the domain (clouddirectory.solutions) and select New \>
User

![image31](https://github.com/user-attachments/assets/0772c314-e0f1-4ff3-8590-ae363a75794a)


UserL setup. Click Next

![image32](https://github.com/user-attachments/assets/11aacf5e-bf9d-40a1-b767-f1aa5e162d29)


Set passwords and enable the accounts

![image33](https://github.com/user-attachments/assets/f7231ec8-6fc8-4f79-bae7-79de5613c1de)


Create the following users the same way.(UserM,UserP,UserV)

![image34](https://github.com/user-attachments/assets/9f08f19b-a2ed-4103-9bee-c7c54bb95d81)


User properties showing group memberships and details.

![image35](https://github.com/user-attachments/assets/2b873206-8d9e-47fa-96e8-962a9bf838cb)


Add this UserL to member of Domain Admins and Enterprise Admins.

![image36](https://github.com/user-attachments/assets/27808198-9385-4814-9721-6a870cacadad)


### Configure DNS Settings

Locate the **Private IP** of the Domain Controller from the default
Azure Portal and copy the private IP address of the DomainControllerVm.

![image37](https://github.com/user-attachments/assets/a5b7e28a-b28b-43a1-9e33-c9d305ef65dd)


Click on the Vitual network/subnet of the DomainControllerVm.

![image38](https://github.com/user-attachments/assets/d16386f7-e887-471c-984d-41be893d0ed8)


Scroll down to DNS servers and paste the private IP address and click on
save.

![image39](https://github.com/user-attachments/assets/a6525b32-716a-4e01-99ac-8cf75ac9cb85)


Restart the DomainControllerVm to apply to setting.

![image40](https://github.com/user-attachments/assets/7d59dc58-74e0-4642-894f-13d0e5df43b2)


## Setting up Azure AD Connect Server

### Create the Second Azure VM

Follow the same steps as in **Step 1** to create the second VM.

Azure VM creation wizard for the EntraconnectVm.

![image41](https://github.com/user-attachments/assets/2380fdc7-2f9f-428c-aa07-54d0532300af)


### Join the Machine to the Domain via Server Manager

Log in to the second VM (Entraconnectvm).

Launch Server Manager from the taskbar or Start menu.

![image42](https://github.com/user-attachments/assets/607ebf1e-88d1-4e4a-b0e9-4259dcf5a53c)


In Server Manager, click on Local Server from the left pane. Locate the
Computer name field and click the hyperlink (e.g., "WORKGROUP").

![image43](https://github.com/user-attachments/assets/7c2cde6a-b574-45e2-a3b1-c405fb6eb9e8)


Open System Properties. In the System Properties window, click the
Change button.

![image44](https://github.com/user-attachments/assets/223b9916-c36d-4575-abe6-b156ca63d2ab)


Under the Member of section, select Domain.

Enter the domain name: clouddirectory.solutions.

Ensure the DomainControllerVm is on before clicking OK.

![image45](https://github.com/user-attachments/assets/a2afd71a-2623-44bc-87af-0cc50d3a1c99)


### Authenticate Credentials

Provide domain administrator credentials (e.g.,
<userL@clouddirectory.solutions>). Since the User has the necessary
permissions.

Click OK.

![image46](https://github.com/user-attachments/assets/b848fe1a-76b8-4492-8502-7a5866d60fa6)


When prompted, restart the server to complete the domain join process.

EntraconnectVm joined to the cloddirectory.solutions domain.

![image47](https://github.com/user-attachments/assets/5201d3bd-2e86-459b-850f-9c4d967e26a2)


### Configure TLS 1.2 on the System

Azure AD Connect requires **TLS 1.2** for secure communication. Update
the registry as follows:

1.  Log in to the second VM (Entraconnectvm).

2.  Open **Registry Editor** (Run \> regedit).

![image48](https://github.com/user-attachments/assets/3473adf2-9125-4d46-89bb-952f53678e5d)


3.  Navigate to the following paths and create the required keys:

    - HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\\NETFramework\v4.0.30319.

![image](https://github.com/user-attachments/assets/7afd9c57-c24e-45b0-974c-256dffb18328)



1.  Right-click in the right pane, select **New \> DWORD (32-bit)
    Value**, and create:

    1.  **SchUseStrongCrypto** (DWORD) with value **1**.

![image](https://github.com/user-attachments/assets/e3c89e60-8248-4762-a0d8-d02e4417839a)


2.  **SystemDefaultTlsVersions** (DWORD) with value 1.

![image](https://github.com/user-attachments/assets/a85a7aff-6126-41c6-ab88-3cecec6d66bc)


- HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\\NETFramework\v4.0.30319

  1.  Right-click in the right pane, select **New \> DWORD (32-bit)
      Value**, and create:

      1.  **SystemDefaultTlsVersions**: Set the value to 1.

![image](https://github.com/user-attachments/assets/ed82e02f-082e-410b-8257-90602e526e67)


2.  **SchUseStrongCrypto**: Set the value to 1.

![image](https://github.com/user-attachments/assets/c86e1f43-27cc-4577-865f-e1ee57a81890)


- HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols

![image](https://github.com/user-attachments/assets/2942a9c8-c04b-4a40-9eda-52b7f4f5d2aa)


1.  Right-click on **Protocols**, select **New \> Key**, and name it TLS
    1.2.

![image](https://github.com/user-attachments/assets/88a3d99e-416f-470b-a784-d129b7155020)

2.  Right-click on TLS 1.2, select New \> Key, and name it Server

3.  Select the Server key and right-click in the right pane to create:

    1.  Enabled: Set the value to 1.

![image](https://github.com/user-attachments/assets/d1ce7cc6-adde-4899-bf6a-b159420280b0)

2.  DisabledByDefault: Set the value to 0.

![image](https://github.com/user-attachments/assets/9334c89e-894c-4f18-ab97-6aa059eb4a83)


4.  In the TLS 1.2 key, right-click on it and select New \> Key, and
    name it Client

5.  Select the Client key and right-click in the right pane to create:

    1.  Enabled: Set the value to 1.

![image](https://github.com/user-attachments/assets/25669700-816a-41df-a605-6633bf4092ca)

2.  DisabledByDefault: Set the value to 0.

![image](https://github.com/user-attachments/assets/f23a674a-594f-4b8b-b128-a577a91e3e88)

4.  Restart the computer.

### Install Microsoft Entra Connect

1.  Log in to the second VM (Entraconnectvm).

2.  Download Microsoft Entra Connect from the **Microsoft Download
    Center**.

![image60](https://github.com/user-attachments/assets/63983af5-a307-4563-b2b8-0c343b623516)


3.  Launch the installer and select **Express Settings**.

![image61](https://github.com/user-attachments/assets/9d152d91-2a3f-49e5-b6a4-4f775d83e9ae)


4.  Sign in with Azure Global Admin and on-premises AD credentials.

![image62](https://github.com/user-attachments/assets/f5e36c92-ffb3-4395-8c19-98ea89ff1ad7)

>
![image63](https://github.com/user-attachments/assets/de344a3c-8c27-4aaf-840f-9f0bcbe123bc)


5.  Complete the installation process by click on next.

![image64](https://github.com/user-attachments/assets/e34bde07-f669-4e7d-936e-9ec8cdf58cb4)

>
![image65](https://github.com/user-attachments/assets/9544bf0b-a983-46f1-9b51-cc9734ab09a7)


## Verify Synchronization

1.  Log in to the **Azure Portal**.

2.  Navigate to **Azure Active Directory \> Users**.

3.  Confirm that users (UserL, UserM, UserP, and UserV) appear in the
    Azure AD directory with the attribute **Directory synced: Yes**.

![image66](https://github.com/user-attachments/assets/36304dcb-3bfd-4e51-989b-3eacf9314daa)

>
> Microsoft Azure portal for UserL
>
![image67](https://github.com/user-attachments/assets/84c1d10a-001b-4d7f-95ca-b1f910f77ef3)

>
> Microsoft Azure portal for UserM
>
![image68](https://github.com/user-attachments/assets/e73a1f1a-4da6-496d-8b33-b01c8fd1fa00)


# Conclusion

In this project, we successfully deployed a hybrid identity
infrastructure by integrating an on-premises Active Directory with Azure
Active Directory using Microsoft Entra Connect. The setup included the
creation of virtual machines, installation and configuration of Active
Directory Domain Services (AD DS), enabling TLS 1.2 for secure
communication, and synchronizing identities with Azure AD.

Key highlights include:

1.  Setting up a primary domain controller with Active Directory Domain
    Services.

2.  Adding users to the Active Directory and assigning roles.

3.  Installing and configuring Microsoft Entra Connect for
    synchronization.

4.  Creating a Global Administrator account in Azure for identity
    management.

5.  Configuring TLS 1.2 to ensure secure communication between services.

**Enhancing Security with Multi-Factor Authentication (MFA)**

To further enhance security, it is highly recommended to enable
Multi-Factor Authentication (MFA) for all administrative and user
accounts. MFA adds an extra layer of protection by requiring users to
verify their identity through multiple forms of authentication.

**Further Reading and Resources**

For additional information and step-by-step guides, refer to the
following Microsoft documentation:

- [Microsoft Entra Connect Installation
  Guide](https://learn.microsoft.com/en-us/azure/active-directory/hybrid/how-to-connect-install)

- [Enable Multi-Factor Authentication in
  Azure](https://learn.microsoft.com/en-us/azure/active-directory/authentication/concept-mfa-howitworks)

- [Managing Users in Azure Active
  Directory](https://learn.microsoft.com/en-us/azure/active-directory/fundamentals/add-users)

- [Active Directory Domain Services
  Overview](https://learn.microsoft.com/en-us/windows-server/identity/ad-ds/ad-ds-overview)

By implementing the steps outlined in this project and leveraging the
additional security features, organizations can establish a robust and
secure identity management solution suitable for hybrid environments.
