---
title: "What's new in the Microsoft 365 compliance center"
ms.author: brendonb
author: MSFTTracyP
manager: dansimp
ms.date: 01/14/2019
audience: Admin
ms.topic: reference
ms.service: O365-seccomp
localization_priority: Normal
search.appverid:
- SPO160
- MOE150
- MET150
ms.assetid: e3c6df61-8513-499d-ad8e-8a91770bff63
ms.collection:
- M365-security-compliance
description: "Office 365 can help protect your environment from malware by detecting viruses in files that users upload to SharePoint Online. Files are scanned for viruses after they are uploaded. If a file is found to be infected, a property is set so that users can't download or sync the file."
---

# What's new in the Microsoft 365 compliance center

We're continuously adding new features to the [Microsoft 365 compliance center](microsoft-365-compliance-center.md), fixing issues we learn about, and making changes based on your feedback. Take a look below to see what's available for you today.

> [!TIP]
> Interested in what's going on in other admin centers? Check out these articles:<br>[What's new in the Microsoft 365 admin center](https://docs.microsoft.com/office365/admin/whats-new-in-preview?view=o365-worldwide)<br>[What's new in the SharePoint admin center](https://docs.microsoft.com/sharepoint/what-s-new-in-admin-center)

## New admin roles

We released two new admin roles to help manage security and compliance in your org. Tell all your friends.

- **Compliance data admin**. Users with this role have permissions to protect and track data in the Microsoft 365 compliance center, Microsoft 365 admin center, and Azure. They can also manage everything the Exchange admin center, Compliance Manager, Teams & Skype for Business admin center and create support tickets for Azure and Microsoft 365.
- **Security operator**. Users with this role can manage alerts and have global read-only access to security-related features, including everything in the Microsoft 365 security center, Azure Active Directory, Identity Protection, Privileged Identity Management and Office 365 Security & Compliance Center.

[Learn more about these roles](https://docs.microsoft.com/office365/securitycompliance/permissions-microsoft-365-compliance-security)

## Search and filtering for reports

No more scrolling through a sea of reports to find the ones you want. You can now search for reports (based on their titles) and filter on categories like ‘Labels’ and ‘Compliance’ and sources like ‘Office 365’ and 'Microsoft Cloud App Security’.

![Screen capture of the search and filter buttons for reports with an applied filter](media/mcc_report_filtering.png)

## Partners: Admin on behalf of (AOBO) permissions

Good news for Microsoft Certified Partners. Partners with Admin On Behalf Of (AOBO) permissions can now access the Microsoft 365 security and compliance centers by adding the customer’s domain to the URL. For example: `https://security.microsoft.com/contoso.com`.

## Help content

Pull up a chair, grab a cup of coffee, and let our latest compliance docs sweep you away.

### New

[Review conversations in Advanced eDiscovery](compliance20/conversation-review-sets.md). Conversation reconstruction lets you reconstruct, review, annotate, and export a group of messages in the context of a conversation.

### Updated

[Troubleshoot AzCopy in Advanced eDiscovery](compliance20/troubleshooting-azcopy.md)<br>
[Load non-Office 365 data into a review set](compliance20/load-non-office365-data.md)<br>
[Error remediation when processing data](compliance20/error-remediation.md)<br>
All three topics updated with info about requirement to use AzCopy v8.1.

[Set up a connector to archive Instant Bloomberg data in Office 365](archive-instant-bloomberg-data.md). SSH key, PGP key, and IP address for Office 365 now downloaded in three separate files. Also new instructions about working with Bloomberg support to set up an SFTP site.

[Create custom sensitive information types with Exact Data Match based classification (Preview)](create-custom-sensitive-info-type-edm.md). Updated UI and PowerShell procedures.

[Supervision policies in Office 365](supervision-policies.md). New info about the offensive language model and condition for excluding email messages in a policy.
