---
title: "Office 365 Message Encryption version comparison"
ms.author: krowley
author: kccross
manager: laurawi
ms.audience: Admin
ms.topic: conceptual
ms.service: O365-seccomp
localization_priority: Normal
search.appverid:
- MET150
description: "Helps explain the differences in the features delivered with different versions of Office 365 Message Encryption as well as how the two continue to work together."
---

# Compare versions of OME

This article compares legacy Office 365 Message Encryption to the new OME capabilities. The new capabilities are a merger and newer version of both the OME and Information Rights Management (IRM). We'll also cover how the two can coexist in your Office 365 organization.

||
|:-----|
|This article is part of a larger series of articles about Office 365 Message Encryption. This article is intended for administrators and ITPros. If you're just looking for information on sending or receiving an encrypted message, see the list of articles in [Office 365 Message Encryption (OME)](ome.md) and locate the article that best fits your needs. |
||

## Side-by-side comparison of features and capabilities

|                                   |Old features       |                   |New features              |
|-----------------------------------|-------------------|-------------------|--------------------------|
|**Capability**                     | **Legacy OME**    | **IRM**           | **New OME capabilities** |
|*Sending an encrypted mail*        |Through Exchange mail flow rules|End-user initiated from Outlook desktop or Outlook on the Web; or through Exchange mail flow rules|End-user initiated from Outlook desktop, Outlook for Mac, or Outlook on the Web; through Exchange Transport Rules and Office 365 Data Loss Prevention (DLP)|
|*Rights management template*       |   N/A      |Do Not Forward option and custom templates|Do Not Forward option, Encrypt-Only option, and custom templates|
|*Recipient type*                   |Internal and external recipients|Internal recipients only         |Internal and external recipients|
|*Experience for internal recipient*|Recipients receive an HTML message, which they download and open in a web browser or mobile app|Native inline experience in Outlook clients|Native inline experience for Office 365 recipients. All other recipients can read message from OME portal (no download or app required).|
|*Experience for external recipient*|Recipients receive an HTML message, which they download and open in a web browser or mobile app|N/A|Native inline experience for Office 365 recipients. All other recipients can read message from OME portal (no download or app required).|
|*Attachment permissions*           |No restrictions on attachments|Attachments are protected|Attachments are protected for the Do Not Forward option and custom templates. Admins can choose whether attachments for the Encrypt-Only option are protected or not.|
|*Bring your own key (BYOK) support*|None                |None               |BYOK supported          |
||

## Advantages of using the new OME capabilities over legacy OME

The new capabilities provide the following advantages:

- Ability to use Encrypt-Only (which enables secure collaboration), Do Not Forward, as well as custom restrictions.
- Senders can send mail encrypted with the new capabilities manually from Outlook Desktop, Outlook for Mac and Outlook on the web clients.
- Office 365 recipients get to use an inline experience in supported Outlook clients. Alternatively, admins can choose to show Office 365 recipients a branded experience.
- Accounts outside of Office 365, such as Gmail, Yahoo, and Microsoft accounts, are federated with the OME portal, which provides a better user experience for these recipients. All other identities use a one-time pass code to access encrypted messages.
- Admins can customize branding, and create multiple branding templates.
- Admins can revoke emails encrypted with the new capabilities.
- The new capabilities provide detailed usage reports through the Security &amp; Compliance Center.

## Coexistence of legacy OME and the new capabilities in the same tenant

You can use both legacy OME and the new capabilities in the same tenant. As an administrator, you do this by choosing which version of OME you want to use when you create your mail flow rules.

- To specify the legacy version of OME, use the Exchange mail flow rule action “Apply the previous version of OME”.
- To specify the new capabilities, use the Exchange mail flow rule action “Apply Office 365 Message Encryption and rights protection”.

Users can also send mail encrypted with the new capabilities manually from Outlook Desktop, Outlook for Mac and Outlook on the web clients.

## Migrating from legacy OME to the new capabilities

Even though both versions of OME can co-exist, we highly recommend that you edit your old mail flow rules that use the rule action "Apply the previous version of OME" to use the new capabilities by specifying the mail flow rule action “Apply Office 365 Message Encryption and rights protection”. For instructions, see [Define mail flow rules to encrypt email messages in Office 365](define-mail-flow-rules-to-encrypt-email.md).

## Getting started with OME

Typically, the new OME capabilities are automatically enabled for your Office 365 organization. If you're ready to get started using the new OME capabilities within your organization, see [Set up new Office 365 Message Encryption capabilities](set-up-new-message-encryption-capabilities.md).

The legacy version of OME is automatically enabled for your Office 365 organization if you have enabled Azure Information Protection. In the past, legacy OME worked even if Azure Information Protection wasn’t enabled. This is no longer the case.

To start using legacy OME, if you have enabled Azure Information Protection, all you need to do is configure mail flow rules that use the rule action “Apply the previous version of OME”. For instructions, see [Define mail flow rules to encrypt email messages in Office 365](define-mail-flow-rules-to-encrypt-email.md).