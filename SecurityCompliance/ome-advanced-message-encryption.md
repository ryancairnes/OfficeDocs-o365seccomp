---
title: "Office 365 Advanced Message Encryption"
ms.author: krowley
author: kccross
manager: laurawi
ms.audience: Admin
ms.topic: conceptual
ms.service: O365-seccomp
localization_priority: Normal
ms.date: 4/30/2019
ms.collection: 
- Strat_O365_IP
- M365-security-compliance
search.appverid:
- MET150
description: "Advanced Message Encryption in Office 365 helps organizations meet their compliance obligations by enabling admins to expire and revoke access through a Office 365 web portal to encrypted emails."
---

# Office 365 Advanced Message Encryption

Office 365 Advanced Message Encryption is available on top of Office 365 Message Encryption in certain subscriptions. Advanced Message Encryption is included in [Microsoft 365 Enterprise E5](https://www.microsoft.com/microsoft-365/enterprise/home), Office 365 Enterprise E5, and Office 365 Education A5. If your organization has an Office 365 subscription that does not include Office 365 Advanced Message Encryption, you can purchase Advanced Message Encryption as an add-on with E5 Compliance of the Advanced Compliance SKU.

This article is part of a larger series of articles about [Office 365 Message Encryption](ome.md).

Advanced Message Encryption in Office 365 helps customers meet compliance obligations that require more flexible controls over external recipients and their access to encrypted emails. With Advanced Message Encryption in Office 365, you can control sensitive emails shared outside the organization with automatic policies. You configure these policies to identify sensitive information types such as PII, Financial, or Health IDs, or you can use keywords to enhance protection. Once you've configured the policies, you pair policies with a custom branded email templates and then add an expiration date for additional control for emails that fit the policy. Additionally, admins can further control encrypted emails accessed externally through a secure web portal by revoking access to the mail at any time.

You can only set an expiration for and revoke emails  sent to external recipients.

With Office 365 Advanced Message Encryption, any time you apply custom branding, the Office 365 applies the wrapper to email that fits the mail flow rule to which you apply the template. In addition, expiration can only be used if custom branding is used. You can only revoke messages that are received through the portal.

## Get started with Office 365 Advanced Message Encryption

The following topics describe how you set up and use Advanced Message Encryption.

Your organization must have a subscription that includes Office 365 Advanced Message Encryption. For detailed information about supported subscriptions, see the [Message policy and compliance service description](https://docs.microsoft.com/en-us/office365/servicedescriptions/exchange-online-service-description/message-policy-and-compliance).

Set up the new Office 365 Message Encryption capabilities if they are not already set up to leverage Advanced Message Encryption capabilities which provide added protection on top of encrypted messages shared externally. If you do not have Office 365 Message Encryption set up, see [Set up new Office 365 Message Encryption capabilities](set-up-new-message-encryption-capabilities.md).

[Set an expiration date for email encrypted by Office 365 Advanced Message Encryption](ome-advanced-expiration.md). Control sensitive emails shared outside the organization with automatic policies that enhance protection by expiring access through a secure web portal to encrypted emails.

[Revoke email encrypted by Office 365 Advanced Message Encryption](revoke-ome-encrypted-mail.md). Control sensitive emails shared outside the organization and enhance protection by revoking access through a secure web portal to encrypted emails.  