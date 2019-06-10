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

- The user who creates the Instant Bloomberg connector in Step 2 (and who downloads the public keys and IP address in Step 1) must be assigned the Mailbox Import Export role in Exchange Online. This is required to access the **Archive third-party data** page in the Security & Compliance Center. By default, this role isn't assigned to any role group in Exchange Online. You can add the Mailbox Import Export role to the Organization Management role group in Exchange Online. Or you can create a new role group, assign the Mailbox Import Export role, and then add the appropriate users as members. For more information, see the  [Create role groups](https://docs.microsoft.com/Exchange/permissions-exo/role-groups#create-role-groups) or [Modify role groups](https://docs.microsoft.com/Exchange/permissions-exo/role-groups#modify-role-groups) sections in the article "Manage role groups in Exchange Online".

## Step 1: Obtain SSH and PGP public keys and IP address

The step is to object public keys for Secure Shell (SSH) and Pretty Good Privacy (PGP). You'll use these keys in Step 2 to configure the Bloomberg SFTP site to allow the connector that you create in Step 3 to connect to the SFTP site and transfer the Instant Bloomberg chat data to Office 365 mailboxes. You also obtain an IP address in this step, which you when configuring the Bloomberg FTP site in Step 2.

1. 


## Step 2: Configure the Bloomberg SFTP site so Office 365 can connect to it



## Step 2: Create an Instant Bloomberg connector



## Step 5:




(From website: 
Communication is powerful with Instant Bloomberg, the leading chat tool used by the global financial community. Completely integrated with the Bloomberg Terminal, our unique chat-parsing technology lets you capture chat text, incorporate crucial deal details and send them directly to your trading platform. All chats are archived and auditable, enabling you to meet compliance requirements. You can share screens, data sets, charts or Excel files through Instant Bloomberg to collaborate quickly and easily with colleagues and trading partners.)

While market participants rely on the security, stability and consistency of the Instant Bloomberg chat service to view securities, share information and engage in trade negotiations, compliance officers want a better way to manage these communications.

"The SSH protocol (also referred to as Secure Shell) is a method for secure remote login from one computer to another. It provides several alternative options for strong authentication, and it protects the communications security and integrity with strong encryption. It is a secure alternative to the non-protected login protocols (such as telnet, rlogin) and insecure file transfer methods (such as FTP). "