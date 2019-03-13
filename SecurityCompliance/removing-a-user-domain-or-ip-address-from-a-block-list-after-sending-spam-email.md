---
title: "Removing a user from the restricted users portal after sending spam email"
ms.author: tracyp
author: MSFTTracyP
manager: laurawi
ms.date: 03/12/2019
ms.audience: ITPro
ms.topic: article
f1_keywords:
- 'ms.exch.eac.ActionCenter.Restricted.Users.RestrictedUsers'
ms.service: O365-seccomp
ms.custom: TN2DMC
localization_priority: Normal
search.appverid:
- MET150
ms.assetid: 712cfcc1-31e8-4e51-8561-b64258a8f1e5
ms.collection:
- M365-security-compliance
description: "If a user continuously sends emails from Office 365 that are classified as spam, they will be restricted from sending any more messages."
---

# Removing a user from the restricted users portal after sending spam email

If a user continuously sends emails from Office 365 that are classified as spam, they will be restricted from sending any more messages outbound. The user will be listed in the service as a bad outbound sender and will receive a Non-Delivery Report (NDR) that states:

- Your message couldn't be delivered because you weren't recognized as a valid sender. The most common reason for this is that your email address is suspected of sending spam and it's no longer allowed to send messages outside of your organization. Contact your email admin for assistance. Remote Server returned '550 5.1.8 Access denied, bad outbound sender'

## What do you need to know before you begin?
<a name="sectionSection0"> </a>

Estimated time to complete: 5 minutes
  
You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Anti-spam entry in the [Feature Permissions in Exchange Online](http://technet.microsoft.com/library/15073ce1-0917-403b-8839-02a2ebc96e16.aspx) topic.

The following procedure can also be performed via remote PowerShell. Use the Get-BlockedSenderAddress cmdlet to get the list of restricted users and Remove-BlockedSenderAddress to remove the restriction. To learn how to use Windows PowerShell to connect to Exchange Online, see [Connect to Exchange Online PowerShell](https://go.microsoft.com/fwlink/p/?linkid=396554).

## Remove restrictions for a blocked Office 365 email account

You complete this task in the Office 365 Security & Compliance Center (SCC). [Go to the Office 365 Security & Compliance Center](go-to-the-securitycompliance-center.md) for more details about SCC. You need to be in the **Organization Management** or the **Security Administrator** role group in order to perform these functions. [Go to Permissions in the Office 365 Security & Compliance Center](permissions-in-the-security-and-compliance-center.md) for more details about SCC role groups.

1. Using a work or school account that has Office 365 global administrator privileges, sign into the Office 365 Security and Compliance Center and in the list on the left, expand **Threat Management**, choose **Review**, and then choose **Restricted Users**.
    
    > [!TIP]
    > To go directly to the **Restricted Users** page (formerly known as the Action Center) in the Security &amp; Compliance Center, use this URL: > [https://protection.office.com/#/restrictedusers](https://protection.office.com/?hash=/restrictedusers)

2. This page will contain the list of users that have been blocked from sending mail to outside of your organization.  Find the user you wish to remove restrictions on and then click on **Unblock**.

3. A fly-out will go into the details about the account whose sending is restricted. You should go through the recommendations to ensure you're taking the proper actions in case the account is actually compromised. Click **Next** when done.

4. The next screen has recommendations to help prevent future compromise. Enabling multi-factor authentication (MFA) and changing the passwords are a good defense. Click **Unblock user** when done.

5. Click **Yes** to confirm the change.

    > [!NOTE]
    > It may take up to 30 minutes before restrictions are removed. 

## Making sure admins are alerted when this happens

The tenant admins will also receive an alert stating that the user has been restricted from sending any more outbound messages. It is a default alert that is provided for all tenants and is listed in the SCC Alert policies page, titled "User restricted from sending email". Go to [Alert policies in the Office 365 Security & Compliance Center](https://docs.microsoft.com/en-us/office365/securitycompliance/alert-policies) for more information on the alert.

## For more information

[Responding to a compromised email account](responding-to-a-compromised-email-account.md)

[Understanding the User restricted from sending email alert](https://docs.microsoft.com/en-us/office365/securitycompliance/alert-policies)

[High-risk delivery pool for outbound messages](high-risk-delivery-pool-for-outbound-messages.md)

[Permissions in the Office 365 Security & Compliance Center](permissions-in-the-security-and-compliance-center.md)
