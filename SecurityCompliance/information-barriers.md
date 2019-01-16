---
title: "Information barriers"
ms.author: deniseb
author: denisebmsft
manager: laurawi
ms.date: 01/15/2019
ms.audience: Admin
ms.topic: article
ms.service: o365-administration
localization_priority: None
description: "Use information barriers to ensure communication compliance within your organization."
---

# Information barriers

## Overview

Among the many powerful features included in Microsoft cloud services are communication and collaboration capabilities. But suppose that you want to restrict communications between two groups to avoid a conflict of interest from occurring in your organization. Or, suppose that you want to restrict communications between a group in your organization and outside parties to safeguard internal information. [Information barriers, coming soon for Microsoft Teams](https://docs.microsoft.com/MicrosoftTeams/information-barriers-in-teams), can help! 

Read this article to get a brief overview of information barriers, how it works, and how policies are defined.

## How information barriers work

When information barriers become available for Microsoft Teams, your organization's compliance administrator (or global administrator) can define policies that limit communications between two groups of people within your organization. When information barriers policies are in effect, people in one group affected by those policies are unable to call people in the other affected group using Microsoft Teams (and vice-versa), as specified in your organization's policies.  

> [!IMPORTANT]
> Potentially, everyone included in an information barriers policy can be blocked from communicating with others in Microsoft Teams. When people affected by information barriers policies are part of the same Microsoft Teams team or group chat, they will be removed from those chat sessions. However, information barriers will not apply to email communications or to file sharing through SharePoint Online, OneDrive, or Microsoft Teams. 

To learn more about the Microsoft Teams experience with information barriers, see [Information barriers in Microsoft Teams](https://docs.microsoft.com/MicrosoftTeams/information-barriers-in-teams).

## How policies are defined for information barriers

Currently, information barriers policies are defined and managed in the Office 365 Security & Compliance Center using PowerShell cmdlets. This is typically done by a compliance administrator or a global administrator.

1. As a global administrator or compliance administrator, create a remote PowerShell session to the Security & Compliance Center. (To get help with this, see [Connect to Office 365 Security & Compliance Center PowerShell](https://docs.microsoft.com/powershell/exchange/office-365-scc/connect-to-scc-powershell).)

2. Depending on whether you want to view, modify, or remove an information barriers policy, use one of the following PowerShell cmdlets.
    - To view existing policies, see  [Get-InformationBarrierPolicy](https://github.com/MicrosoftDocs/office-docs-powershell/blob/InfoBarrier-chrisda/exchange/exchange-ps/exchange/policy-and-compliance/Get-InformationBarrierPolicy.md)
    - To define or edit a policy, see  [Set-informationBarrierPolicy](https://github.com/MicrosoftDocs/office-docs-powershell/blob/InfoBarrier-chrisda/exchange/exchange-ps/exchange/policy-and-compliance/Set-InformationBarrierPolicy.md)
    - To remove a policy, see [Remove-InformationBarrierPolicy](https://github.com/MicrosoftDocs/office-docs-powershell/blob/InfoBarrier-chrisda/exchange/exchange-ps/exchange/policy-and-compliance/Remove-InformationBarrierPolicy.md)

3. After your information barriers policies are in place, wait about 30 minutes for those policies to work their way through your data center and services, and then test your policies.<br><br>We recommend testing with a few users who are and aren't included in information barriers policies.



## Related articles

[Information barriers in Microsoft Teams](https://docs.microsoft.com/MicrosoftTeams/information-barriers-in-teams)
