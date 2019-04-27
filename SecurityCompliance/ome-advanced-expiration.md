---
title: "Office 365 Advanced Message Encryption - message expiration"
ms.author: krowley
author: kccross
manager: laurawi
ms.date: 4/30/2019
ms.audience: Admin
ms.topic: conceptual
ms.service: O365-seccomp
localization_priority: Normal
search.appverid:
- MET150
ms.assetid: f87cb016-7876-4317-ae3c-9169b311ff8a
description: "With Office 365 Advanced Message Encryption capabilities on top of Office 365 Message Encryption (OME), you can extend your email security by setting an expiration date on emails through a custom branded template."
---

# Office 365 Advanced Message Encryption - message expiration

Office 365 Advanced Message Encryption is available additions to Office 365 Message Encryption in certain subscriptions. Advanced Message Encryption is included in [Microsoft 365 Enterprise](https://www.microsoft.com/microsoft-365/enterprise/home), Office 365 Enterprise E5, and Office 365 Education A5. If your organization has an Office 365 subscription that does not include Office 365 Advanced Message Encryption, you can potentially purchase Advanced Message Encryption as an add-on. For more information, see [Carolyn/Samson, I need a page](https://products.office.com/) and the [Message Policy and Compliance](https://docs.microsoft.com/en-us/office365/servicedescriptions/exchange-online-service-description/message-policy-and-compliance). Make sure your organization is using the latest version of Office 365 ProPlus on Windows or Mac to take full advantage of Advanced Message Encryption.

You can use message expiration on emails that your users send to recipients who use the OME Portal to access encrypted emails. Recipients outside of Office 365 are directed to the OME Portal when they receive encrypted email. In addition, you can force recipients in other Office 365 organizations to use the OME portal to view and reply to encrypted emails sent by your organization by using Windows Powershell. For information on how to do this, see [Ensure all external recipients use the OME Portal to read encrypted mail](manage-office-365-message-encryption.md#ensure-all-external-recipients-use-the-ome-portal-to-read-encrypted-mail).

Control encrypted emails accessed externally through a secure web portal by setting an expiration date and revoking access at any time.

As an O365 global administrator, when you apply your company branding to customize the look of your Office 365 organization's email messages, you can also specify an expiration for these email messages. With Office 365 Advanced Message Encryption, you can create multiple templates for encrypted emails originating from your organization. Using a template, you can control how long recipients have access to mail sent by your users.

When an end user receives mail that has an expiration date set, the user  sees the expiration date in the wrapper email. If a user tries to open an expired mail, an error appears in the OME portal.

## Create a custom branding template by using PowerShell

1. [Connect to Exchange Online PowerShell](https://docs.microsoft.com/en-us/powershell/exchange/exchange-online/connect-to-exchange-online-powershell/connect-to-exchange-online-powershell) using an account with global administrator permissions in your Office 365 tenant.

2. Run the New-OMEConfiguration cmdlet.

     ```powershell
     New-OMEConfiguration -Identity "Expire in 7 days" ExternalMailExpiryInDays 7
     ```

Where:

- Identity is the name of the custom template.

- ExternalMailExpiryInDays identifies the number of days you want recipients to be able to keep mail before it expires. You can use any value between 1 to 730 days.

## More information about Office 365 Advanced Message Encryption

- [Office 365 Advanced Message Encryption capabilities](ome-version-comparison.md#office-365-advanced-message-encryption-capabilities)
- [Office 365 Advanced Message Encryption - email revocation](revoke-ome-encrypted-mail.md)
- 