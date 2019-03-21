---
title: "Use Threat Explorer in the Security &amp; Compliance Center"
ms.author: deniseb
author: denisebmsft
manager: laurawi
ms.date: 03/21/2019
ms.audience: ITPro
ms.topic: article
ms.service: O365-seccomp
localization_priority: Normal
search.appverid:
- MET150
- MOE150
ms.assetid: 82ac9922-939c-41be-9c8a-7c75b0a4e27d
ms.collection: 
- M365-security-compliance
description: "Learn about Explorer (also called Threat Explorer) in the Security &amp; Compliance Center."
---

# Use Threat Explorer in the Security &amp; Compliance Center

If your organization has [Office 365 Advanced Threat Protection Plan 2](office-365-ti.md), and you have the necessary permissions, you can use Threat Explorer to identify and analyze threats. For example, you can identify and delete malicious email that was delivered, or see malware that was caught by Office 365 security features. Threat Explorer (also referred to as Explorer) is a powerful near real-time tool to help Security Operations teams investigate and respond to threats in the Security &amp; Compliance Center.
  
![Go to Threat management \> Explorer](media/cab32fa2-66f1-4ad5-bc1d-2bac4dbeb48c.png)
  
To use Explorer, in the Security &amp; Compliance Center, go to **Threat management** \> **Explorer**.

> [!IMPORTANT]
> Office 365 Threat Intelligence is now Office 365 Advanced Threat Protection Plan 2, along with additional threat protection capabilities. To learn more, see [Office 365 Advanced Threat Protection plans and pricing](https://products.office.com/exchange/advance-threat-protection) and the [Office 365 Advanced Threat Protection Service Description](https://docs.microsoft.com/office365/servicedescriptions/office-365-advanced-threat-protection-service-description).
      
## Explorer overview

If your organization has [Office 365 Threat investigation and response capabilities](office-365-ti.md) (this is included in ATP Plan 2), and you have the necessary permissions, you can use Threat Explorer (also referred to as Explorer) to identify and analyze threats. (In the Security &amp; Compliance Center, go to **Threat management** \> **Explorer**.)

![Go to Threat management \> Explorer](media/cab32fa2-66f1-4ad5-bc1d-2bac4dbeb48c.png)

This article describes a few things you can do with Explorer (there are many more possibilities):

- [See what kinds of malware were detected in email](#see-malware-detected-in-email-by-technology), and by threat protection technology (anti-malware protection, ATP Safe Attachments, etc.)

- [View data about phishing links (URLs)](#view-data-about-phishing-urls-and-click-verdict), and what the click verdicts were (URLs blocked, allowed, or visited despite warnings)

- [Review email messages that were reported as Junk, Not Junk, or Phishing](#review-email-messages-reported-by-users), and identify any trends (such as a larger than usual number of messages reported as Phish) 

## See malware detected in email by technology

Suppose you want to see malware that was detected in email, and by what technology in Office 365. To do this, use the [Email > Malware](threat-explorer-views.md#email--malware) view of Explorer.

1. In the Office 365 Security & Compliance Center ([https://protection.office.com](https://protection.office.com)), choose **Threat management** > **Explorer**.
2. In the **View** menu, choose **Email** > **Malware**.<br/>![View menu for Explorer](media/ExplorerViewEmailMalwareMenu.png)<br/>
3. Click **Sender**, and then choose **Basic** > **Detection technology**.<br/>Your detection technologies are now available as filters for the report.<br/>![Malware detection technologies](media/ExplorerEmailMalwareDetectionTech.png)<br/> 
4. Select an option, and then click the Refresh button to apply that filter.<br/>![Selected detection technology](media/ExplorerEmailMalwareDetectionTechATP.png)<br/> 

The report refreshes to show the results malware detected in email, using the technology option you selected. From here, you can conduct further analysis.

## View data about phishing URLs and click verdict

Suppose you want to see phishing attempts through URLs in email, including a list of URLs that were allowed, blocked, and overridden. To do this, use the [Email > Phish](threat-explorer-views.md#email--phish) view of Explorer.

1. In the Office 365 Security & Compliance Center ([https://protection.office.com](https://protection.office.com)), choose **Threat management** > **Explorer**.
2. In the **View** menu, choose **Email** > **Phish**.<br/>![View menu for Explorer](media/ExplorerViewEmailPhishMenu.png)<br/>
3. Click **Sender**, and then choose **URLs** > **Click verdict**.
4. Select one or more options, such as **Blocked** and **Block overridden**, and then click the **Refresh** button to apply that filter.<br/>![URLs and click verdicts](media/ThreatExplorerEmailPhishClickVerdictOptions.png)<br/>

The report refreshes to show detected phishing URLs in email that were blocked (or visited despite a warning), along with email delivery status. From here, you can conduct further analysis. For example, below the chart, you can see the top URLs that were blocked in your organization's email. 

![Explorer URLs that were blocked](media/ExplorerPhishClickVerdictURLs.png) 

Select a URL to view more detailed information.

## Review email messages reported by users

Suppose you want to see email messages that users in your organization have reported as Junk, Not Junk, or Phishing by using the [Report Message add-in for Outlook and Outlook on the web](enable-the-report-message-add-in.md). To do this, use the [Email > User-reported](threat-explorer-views.md#email--user-reported) view of Explorer.

1. In the Office 365 Security & Compliance Center ([https://protection.office.com](https://protection.office.com)), choose **Threat management** > **Explorer**.
2. In the **View** menu, choose **Email** > **User-reported**.<br/>![View menu for Explorer](media/ExplorerViewMenuEmailUserReported.png)<br/>
3. Click **Sender**, and then choose **Basic** > **Report type**.
4. Select an option, such as **Phish**, and then click the **Refresh** button. <br/>![User-reported phish](media/EmailUserReportedReportType.png)<br/> 

The report refreshes to show data about email messages that people in your organization have reported as a phishing attempt. You can use this information to conduct further analysis, and if necessary, adjust your [ATP anti-phishing policies](set-up-anti-phishing-policies.md).

## There's more!

In addition to the three scenarios outlined in this article, you have many reporting scenarios available with Explorer. Here are a few more examples:

- [Find and investigate malicious email that was delivered](investigate-malicious-email-that-was-delivered.md)

- [View malicious files detected in SharePoint Online, OneDrive, and Microsoft Teams](malicious-files-detected-in-spo-odb-or-teams.md)

- [Get an overview of the views in Threat Explorer](threat-explorer-views.md)

## How to get Explorer

Explorer is included in [Office 365 Advanced Threat Protection Plan 2](office-365-ti.md). 

To view and use Explorer, you must have appropriate permissions, such as those granted to a security administrator or security reader. 

- For the Security &amp; Compliance Center, you must have one of the following roles assigned:
    - Organization Management
    - Security Administrator (this can be assigned in the Azure Active Directory admin center ([https://aad.portal.azure.com](https://aad.portal.azure.com)))
    - Security Reader

- For Exchange Online, you must have one of the following roles assigned in either the Exchange admin center ([https://outlook.office365.com/ecp](https://outlook.office365.com/ecp)) or with PowerShell cmdlets (See [Exchange Online PowerShell](https://docs.microsoft.com/powershell/exchange/exchange-online/exchange-online-powershell?view=exchange-ps)):
    - Organization Management
    - View-only Organization Management
    - View-Only Recipients role
    - Compliance Management

To learn more, see the following resources:

- [Permissions in the Office 365 Security &amp; Compliance Center](permissions-in-the-security-and-compliance-center.md)

- [Feature permissions in Exchange Online](https://docs.microsoft.com/exchange/permissions-exo/feature-permissions)
  
## Related topics

- [Automated Investigation and Response (AIR)](automated-investigation-response-office.md)

- [Threat Explorer views](threat-explorer-views.md)

- [View reports for Office 365 Advanced Threat Protection](view-reports-for-atp.md)
