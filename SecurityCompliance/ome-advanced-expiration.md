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
description: "with Office 365 Advanced Message Encryption capabilities on top of Office 365 Message Encryption, you can extend your email security by setting an expiration date on emails through a custom branded template."
---

# Office 365 Advanced Message Encryption - message expiration

Office 365 Advanced Message Encryption is available in Office 365 Message Encryption. Advanced Message Encryption is included in subscriptions, such as [Microsoft 365 Enterprise](https://www.microsoft.com/microsoft-365/enterprise/home), Office 365 Enterprise E5, Office 365 Education A5, etc. If your organization has an Office 365 subscription that does not include Office 365 Advanced Message Encryption, you can potentially purchase Advanced Message Encryption as an add-on. For more information, see [Carolyn/Samson, I need a page](https://products.office.com/TBD) and the [Office 365 CORRECT Service Description](https://docs.microsoft.com/office365/servicedescriptions/TBD). Make sure your organization is using the latest version of Office 365 ProPlus on Windows to take full advantage of Advanced Message Encryption.

**I need the M365 equivalent, not EOP or EXO** As an Administrator, when you apply your company branding to customize the look of your organization's Office 365 Message Encryption email messages, you can also specify an expiration for these email messages. You can create multiple templates for encrypted emails originating from your organization. Using these templates, you can control how long recipients have access to mail sent by your users.

When an end user receives mail that has an expiration date set, they will see that expiration date in the wrapper email. If a user tries to open an expired mail, they receive an error in the OME portal. **CAROLYN! SAMSON! what if they are using OMEv2 and have a seamless experience and therefore, NO wrapper mail and no portal?**

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

- 