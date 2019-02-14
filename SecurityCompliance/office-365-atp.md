---
title: "Office 365 Advanced Threat Protection"
ms.author: deniseb
author: denisebmsft
manager: laurawi
ms.date: 02/08/2019
ms.audience: Admin
ms.topic: hub-page
ms.service: o365-administration
localization_priority: Normal
search.appverid:
- MET150
- MOE150
ms.assetid: e100fe7c-f2a1-4b7d-9e08-622330b83653
ms.collection:
- M365-security-compliance
description: "Office 365 Advanced Threat Protection includes spoof intelligence, safe links, safe attachments, advanced anti-phishing capabilities, and threat intelligence."
---

# Office 365 Advanced Threat Protection

> [!IMPORTANT]
> This article is intended for business customers. If you are a home user looking for information about Safe Links in Outlook, see [Advanced Outlook.com security](https://support.office.com/article/advanced-outlook-com-security-for-office-365-subscribers-882d2243-eab9-4545-a58a-b36fee4a46e2).

## Overview of Office 365 Advanced Threat Protection

Office 365 Advanced Threat Protection (ATP) helps to protect your organization from malicious attacks by:
  
- Scanning email attachments for malware with [ATP Safe Attachments](atp-safe-attachments.md)
    
- Scanning web addresses (URLs) in email messages and Office documents with [ATP Safe Links](atp-safe-links.md)
    
- Identifying and blocking malicious files in online libraries with [ATP for SharePoint, OneDrive, and Microsoft Teams](atp-for-spo-odb-and-teams.md)
    
- Checking email messages for unauthorized spoofing with [spoof intelligence](learn-about-spoof-intelligence.md)
    
- Detecting when someone attempts to impersonate your users and your organization's custom domains with [ATP anti-phishing capabilities in Office 365](atp-anti-phishing.md)
    
**Protection through Office 365 ATP is determined by policies that your organization's security team defines for Safe Links, Safe Attachments, and Anti-Phishing**. It's important to define policies, and to periodically review and revise those policies to keep them up to date and to take advantages of new features that are added to the service. 

[Reports are available](view-reports-for-atp.md) to show how ATP is working for your organization. These reports can also show you areas where you might need to review and update your policies. And, if you have files that are marked as malware that shouldn't be, or files you'd like Microsoft to examine, you can [submit a file to Microsoft for analysis](#submit-a-suspicious-file-to-microsoft-for-analysis).

## New features are continually being added to ATP

We are continuing to add new features to Office 365, and that includes ATP. Below is a list of several new features, some of which call for an ATP policy to be reviewed and updated. To learn more about new features coming to ATP (or Microsoft 365 in general), visit the [Microsoft 365 Roadmap](https://www.microsoft.com/microsoft-365/roadmap?filters=O365).


|Feature updates  |Action items  |
|---------|---------|
|Beginning in February 2019 and rolling out over the next several months, Threat Intelligence capabilities are being added to ATP. In addition, if your organization does not currently have ATP, you'll have new options to consider, including ATP Plan 1 and ATP Plan 2. To learn more, see [Office 365 Advanced Threat Protection plans and pricing](https://products.office.com/exchange/advance-threat-protection) and the [Office 365 Advanced Threat Protection Service Description](https://docs.microsoft.com/office365/servicedescriptions/office-365-advanced-threat-protection-service-description). |Review your organization's subscription, and if needed, [Buy or edit an add-on](https://docs.microsoft.com/office365/admin/subscriptions-and-billing/buy-or-edit-an-add-on).  |
|Beginning in October 2018 and rolling out over the next several months, when people are using Outlook or Outlook Web Application (OWA), ATP Safe Links renders original URLs, not rewritten URLs. (We call this native link rendering.)<br>When native link rendering is available for your organization, this feature will work in Outlook 365 (Click-to-Run) and OWA.|None         |
|Beginning in September 2018, [Office 365 ATP warning pages](atp-safe-links-warning-pages.md) feature a new color scheme, more details, and the ability to continue to a site despite given warnings and recommendations. |None         |
|Beginning in the second half of 2018, ATP Safe Links protection is extended to apply to URLs in Office Online (Word Online, Excel Online, PowerPoint Online, and OneNote Online) and Office 365 ProPlus on Mac.   |[Review and edit your ATP Safe Links policies](set-up-atp-safe-links-policies.md)  |
|Beginning in late May 2018, [quarantine](quarantine-email-messages.md) capabilities in the Security &amp; Compliance Center are being extended to [ATP for SharePoint Online, OneDrive for Business, and Microsoft Teams](atp-for-spo-odb-and-teams.md). |[Review and edit your ATP Safe Attachments policies](set-up-atp-safe-attachments-policies.md) |
|Beginning in March 2018, ATP Safe Links protection is extended to apply to email sent between people within an organization. |[Review and edit your ATP Safe Links policies](set-up-atp-safe-links-policies.md) |
|Beginning in late October 2017, ATP Safe Links protection is extended to apply to URLs in email as well as URLs in Office 365 ProPlus documents, such as Word, Excel, PowerPoint, and Visio on Windows, as well as Office apps on iOS and Android devices.  |Make sure you're using [Modern Authentication for Office](https://docs.microsoft.com/office365/enterprise/modern-auth-for-office-2013-and-2016) |


      
## Get Office 365 ATP

Office 365 ATP is included in subscriptions, such as [Microsoft 365 Enterprise](https://www.microsoft.com/microsoft-365/enterprise/home), [Microsoft 365 Business](https://www.microsoft.com/microsoft-365/business), Office 365 Enterprise E5, and Office 365 Education A5. If your organization has an Office 365 subscription that does not include Office 365 ATP, you can potentially purchase ATP as an add-on. For more information, see [Office 365 Advanced Threat Protection plans and pricing](https://products.office.com/exchange/advance-threat-protection) and the [Office 365 Advanced Threat Protection Service Description](https://docs.microsoft.com/office365/servicedescriptions/office-365-advanced-threat-protection-service-description). 

## Define policies for ATP

To define (or edit) ATP policies, you must be assigned one of the roles described in the following table:

|Role  |Where/how assigned  |
|---------|---------|
|Office 365 Global Administrator |The person who signs up to buy Office 365 is a global admin by default. (See [About Office 365 admin roles](https://docs.microsoft.com/office365/admin/add-users/about-admin-roles) to learn more.)         |
|Security Administrator |Azure Active Directory admin center ([https://aad.portal.azure.com](https://aad.portal.azure.com))|
|Exchange Online Organization Management |Exchange admin center ([https://outlook.office365.com/ecp](https://outlook.office365.com/ecp)) <br>or <br>  PowerShell cmdlets (See [Exchange Online PowerShell](https://docs.microsoft.com/powershell/exchange/exchange-online/exchange-online-powershell?view=exchange-ps)) |

> [!TIP]
> To learn more about roles and permissions, see [Permissions in the Office 365 Security &amp; Compliance Center](permissions-in-the-security-and-compliance-center.md).

There are several kinds of ATP policies to define and periodically review.

1. **[Set up ATP anti-phishing policies in Office 365](set-up-anti-phishing-policies.md)** including impersonation-based attacks to protect against attackers who send email messages that appear to be from trusted people or domains. 

2. **[Set up ATP Safe Links policies in Office 365](set-up-atp-safe-links-policies.md)** including your organization's [custom blocked URLs list](set-up-a-custom-blocked-urls-list-wtih-atp.md) and [custom "Do not rewrite" URLs list](set-up-a-custom-do-not-rewrite-urls-list-with-atp.md).
    
3. **[Set up ATP Safe Attachments policies in Office 365](set-up-atp-safe-attachments-policies.md)** and choose from several options, such as [Dynamic Delivery and previewing](dynamic-delivery-and-previewing.md).
  
## See how ATP is working by viewing reports

After your ATP policies are in place, reports are available to show how the service is working. (In the Office 365 Security & Compliance Center, go to **Reports** > **Dashboard**.)

[![The Security &amp; Compliance Center dashboard can help you see where Advanced Threat Protection is working](media/6b213d34-adbb-44af-8549-be9a7e2db087.png)](view-reports-for-atp.md)
  
1. As an Office 365 global administrator, a security administrator, or a security reader, go to [https://protection.office.com](https://protection.office.com) and sign in.
    
2. Go to **Reports** > **Dashboard**. (To get help with these reports, see [View reports for Advanced Threat Protection](view-reports-for-atp.md).)
    
3. If needed, make adjustments to your security policies. To get help with this, see the following resources:
      - [ATP anti-phishing policies in Office 365](set-up-anti-phishing-policies.md)
      - [ATP Safe Links policies in Office 365](set-up-atp-safe-links-policies.md)
      - [ATP Safe Attachments policies in Office 365](set-up-atp-safe-attachments-policies.md)
    
    
## Submit a suspicious file to Microsoft for analysis

- If you get a file that you suspect could be malware, you can submit that file to Microsoft for analysis. Visit the [Windows Defender Security Intelligence submission portal](https://go.microsoft.com/fwlink/?linkid=857185).

- If you get an email message (with or without an attachment) that you'd like to submit to Microsoft for analysis, use the [Report Message add-in](enable-the-report-message-add-in.md). 
  

