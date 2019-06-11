---
title: "Set up a connector to archive Instant Bloomberg data in Office 365 (Preview)"
ms.author: markjjo
author: markjjo
manager: laurawi
ms.date: 
audience: Admin
ms.topic: article
ms.service: O365-seccomp
localization_priority: Normal
ms.collection: M365-security-compliance
description: "Administrators can set up a native connector to import data from the Instant Bloomberg chat tool into Office 365. This lets you archive data from third-party data sources in Office 365 so you can use compliance features such as legal hold, content search, and retention policies to manage your organization's third-party data."
---

# Set up a connector to archive Instant Bloomberg data in Office 365 (Preview)

The connector feature to archive Instant Bloomberg data in Office 365 is in Preview.

Use a native connector in the Security & Compliance Center in Office 365 to import and archive financial services chat data from [Instant Bloomberg](https://www.bloomberg.com/professional/product/collaboration/) collaboration tool. After you set up and configure a connector, it connects to your organization's Instant Bloomberg account (on a daily basis), converts the content of chat messages to an email message format, and then imports those items to mailboxes in Office 365.

After Instant Bloomberg data is imported and located in user mailboxes, you can user Office 365 compliance features such as Litigation Hold, Content Search, In-Place Archiving, Auditing, and Office 365 retention policies to Instant Bloomberg data. For example, you can search third-party data using Content Search or associate it with a custodian in an Advanced eDiscovery case. Using sample connectors to import and archive Twitter data in Office 365 can help your organization stay compliant with government and regulatory policies.

> [!NOTE]
> At this time, Instant Bloomberg chat messages that are archived in mailboxes won’t be monitored by supervision policies in Office 365.

## Overview of archiving Instant Bloomberg data

The following overview explains the implementation process of archiving Instant Bloomberg chat data in Office 365. Note that many of the implementation steps are external to Office 365 and must be completed before you can create the Instant Bloomberg connector in the Security & Compliance Center.


## Before you begin

- You need to subscribe to [Blooomberg Anywhere](https://www.bloomberg.com/professional/product/remote-access/?bbgsum-page=DG-WS-PROF-PROD-BBA). This is required so that you can log in to Bloomberg Anywhere to access the Bloomberg SFTP site that you have to set up and configure.

- You need to set up a Bloomberg SFTP (Secure file transfer protocol) site. After working with Bloomberg to set up the SFTP site, data from Instant Bloomberg will be uploaded to the SFTP site on a daily basis. The connector you create in Step 2 connects to this SFTP site and transfers the chat data to Office 365 mailboxes. SFTP also encrypts the Instant Bloomberg chat data that is sent to Office 365 mailboxes during the transfer process.

    For information about Bloomberg SFTP (also called *BB-SFTP*):

    - See the "SFTP Connectivity Standards" document at [Bloomberg Support](https://www.bloomberg.com/professional/support/documentation/).
    
    - Contact [Bloomberg customer support](https://service.bloomberg.com/portal/sessions/new?utm_source=bloomberg-menu&utm_medium=csc).

    After you work with Bloomberg to set up an SFTP site, Bloomberg will provide some information to you after you respond to the Bloomberg implemenation email message. Save a copy of the following information. You'll use it to set up a connector in Step 3.

    - Firm code

    - Password for SFTP site

    - URL for Bloomberg SFTP site (for example, sftp.bloomberg.com)

    - SFTP port number

- The user who creates the Instant Bloomberg connector in Step 2 (and who downloads the public keys and IP address in Step 1) must be assigned the Mailbox Import Export role in Exchange Online. This is required to access the **Archive third-party data** page in the Security & Compliance Center. By default, this role isn't assigned to any role group in Exchange Online. You can add the Mailbox Import Export role to the Organization Management role group in Exchange Online. Or you can create a new role group, assign the Mailbox Import Export role, and then add the appropriate users as members. For more information, see the  [Create role groups](https://docs.microsoft.com/Exchange/permissions-exo/role-groups#create-role-groups) or [Modify role groups](https://docs.microsoft.com/Exchange/permissions-exo/role-groups#modify-role-groups) sections in the article "Manage role groups in Exchange Online".

## Step 1: Obtain SSH and PGP public keys and IP address

The first step is to obtain a copy of the public keys for Secure Shell (SSH) and Pretty Good Privacy (PGP). You'll use these keys in Step 2 to configure the Bloomberg SFTP site to allow the connector (that you create in Step 3) to connect to the SFTP site and transfer the Instant Bloomberg chat data to Office 365 mailboxes. You also obtain an IP address in this step, which you use when configuring the Bloomberg SFTP site.

1.  Go to <https://protection.office.com> and then click **Data governance \> Import** and then click **Archive third-party data**.

2. On the **Archive third-party data** page, click **Add a connector**, and then click **Instant Bloomberg**.

3. On the **Terms of service** page, click **Accept**.

4. On the **Add credentials for Bloomberg SFTP site** under step 1, click **Download public keys and IP address**.

5. Save a copy of the Keys.txt file to your local computer. This file contains the following three items:

   - SSH public key

   - PGP public key

   - IP address: 40.124.28.216

6. Click **Cancel** to close the wizard. You'll come back to this wizard in Step 3 to create the connector.

## Step 2: Configure the Bloomberg SFTP site so Office 365 can connect to it

The next step is to use the SSH and PGP public keys and the IP address that you obtained in Step 1 to configure SSH authentication and PGP encryption for the Bloomberg SFTP site. This will allow the Instant Bloomberg connector that you create in Step 3 to connect to the Bloomberg SFTP site and transfer Instant Bloomberg data to Office 365. Contact [Bloomberg customer support](https://service.bloomberg.com/portal/sessions/new?utm_source=bloomberg-menu&utm_medium=csc) if you need assitance setting this up.

1. Log in to the Bloomberg CCNS control panel using an account for your organization.

2. Go to CCNS and click the ****Public Keys** tab.

3. To enable SSH authentication, click **Add**.

4. In the **Add Public Key** window, click the **Key Type** dropdown list, and then click **Login**.

5. Copy the entire SSH public key (all characters between, but not including, the double quotation marks) that you downloaded in Step 1, paste it in this field, and then click **Submit**.
 
    For example, you would copy the following SSH public key:

    ```
    ssh-rsa AAAAB3NzaC1yc2EAAAABIwAAAQEA1dxAyc0JzCmc5NzgyzRYhnj3FGHK5Kd9T2cwZNkmL/9nFhQupQor081rmuw9gACAmeot7y+V/fmijo/q4rxDe3Auu3hfLl1NpWlIssQJHzycms8zimtdQcXbMKwDQOnRthpEocF5ySs76KE72vaYQJTvclAamWWq0D75SUmXDFFr7afvEy57F7KgMD1ecg6lH7q8seSKbiiWxX1Ul0kL15fzpUyhjDP41owb1XC/dF7fJwAmCO1+HZfDLEp62q4tnApLpdd92KoR41LZTryO5dICKhk+S+JxPLkksxL0wm5YevOr2n4ScuRdsBV8mWKZ1Xw+cOss9O6L7cCcEiB3Ow==
    ```

6. To enable PGP encryption, click **Add** again on the **Public Keys** tab, click the **Key Type** dropdown list, and this time click **Encryption**.

7. Copy the entire PGP public key (all characters between, but not including, the double quotation marks) that you downloaded in Step 1, paste it in this field, and then click **Submit**. 

    For example, you would copy the following PGP public key:

    ```
    -----BEGIN PGP PUBLIC KEY BLOCK-----\nVersion: BCPG C# v1.7.4137.9688\n\nmQENBFz+6UQBCACKC4ilYoVOP5b/F0CO+oQYbag79Ov4NZxM4EKW51lUAvKNExRM\nc1C/gwXm8bghht8GEODckXXqx8qSSXUEeA/ROweXNtD1u1kn7PgYEFUeD/qE739m\nm5lxXF9Vod26AtKQ9Y1EvYoQEltwztAaXg8K8LQzB+tzN079d1cxM5tbiRQLttAh\nOt5amLXuINt8+dWyNas3DfgIBUmwfkwCbUO0ElrIhvvO3A85K97SX9Q6Py0SkfkK\nQpnULuhdjSm+7k7qlVMf0s8e/9jUXYKbMFkxlOoMq052vV0l0VQNSeuKoC+m6+LT\nEPab89AMt6S4Ujum9wTUy1eWNx9vV0y/w8N7ABEBAAG0JDM5MjM4ZTg3LWI1YWIt\nNGVmNi1hNTU5LWFmNTRjNmIwN2I0MokBHAQQAQIABgUCXP7pRAAKCRAJQdjaG//S\nCy70B/wKrR2CcqtZx56yrGJFfVy3niEt16VEA3xJM3D9nX0gmgo85Nh5gkiY3ahH\nnNEmgW5vlCM1gcgFeoZWe8A80G4QoabslSUzLbq9HsHOOAQApsfhrhXpylrAVa4n\nI53XUOxWdOTa4xsOob8hSRADqJbwHPOsoAr2A87TvZ9LSi2Mii5omeTq416CLnoS\nPBAEhelZm+ruy5JhzA1yXvWYFH08wNqSHO3bskdES2yW5SyQmYlcoEztWE0Q0Z+G\nZT3kOa/W2MbcZovFCQIfqhwVfXtIzx5uYUmxgk5cFKUJJMlO0AZK/HwM22xuuIWe\ndMa6OMo/n8tvEBxrLQMdVPlz+hZ6\n=AwmP\n-----END PGP PUBLIC KEY BLOCK-----\n
    ```

## Step 3: Create an Instant Bloomberg connector



## Step 5:




(From website: 
Communication is powerful with Instant Bloomberg, the leading chat tool used by the global financial community. Completely integrated with the Bloomberg Terminal, our unique chat-parsing technology lets you capture chat text, incorporate crucial deal details and send them directly to your trading platform. All chats are archived and auditable, enabling you to meet compliance requirements. You can share screens, data sets, charts or Excel files through Instant Bloomberg to collaborate quickly and easily with colleagues and trading partners.)

While market participants rely on the security, stability and consistency of the Instant Bloomberg chat service to view securities, share information and engage in trade negotiations, compliance officers want a better way to manage these communications.

"The SSH protocol (also referred to as Secure Shell) is a method for secure remote login from one computer to another. It provides several alternative options for strong authentication, and it protects the communications security and integrity with strong encryption. It is a secure alternative to the non-protected login protocols (such as telnet, rlogin) and insecure file transfer methods (such as FTP). "