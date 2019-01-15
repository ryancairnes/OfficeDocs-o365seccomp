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

Among the many powerful features included in Microsoft cloud services are communication and collaboration capabilities. But suppose that you want to restrict communications between two groups to avoid a conflict of interest from occurring in your organization. Information barriers, **coming soon to [Microsoft Teams](https://docs.microsoft.com/MicrosoftTeams/information-barriers-in-teams)**, can help! Read this article to get an overview of information barriers as part of your organization's security and compliance strategy, including what to expect, and next steps.

## How information barriers work

When information barriers become available for Microsoft Teams, your organization's compliance administrator (or global administrator) can define policies that limit communications between two groups of people within your organization. When information barriers policies are in effect, people in one group affected by those policies are unable to call people in the other affected group using Microsoft Teams (and vice-versa), as specified in your organization's policies.  

> [!IMPORTANT]
> Potentially, everyone included in an information barriers policy can be blocked from communicating with others in Microsoft Teams. When people affected by information barriers policies are part of the same Microsoft Teams team or group chat, they will be removed from those chat sessions. However, information barriers will not apply to email communications or to file sharing through SharePoint Online, OneDrive, or Microsoft Teams. 

To learn more about the Microsoft Teams experience with information barriers, see [Information barriers in Microsoft Teams](https://docs.microsoft.com/MicrosoftTeams/information-barriers-in-teams).

## How policies are defined for information barriers

Currently, information barriers policies are defined by using PowerShell cmdlets, as follows:

|PowerShell cmdlet  |Description  |
|---------|---------|
|[Get-InformationBarrierPolicy](https://github.com/MicrosoftDocs/office-docs-powershell/blob/InfoBarrier-chrisda/exchange/exchange-ps/exchange/policy-and-compliance/Get-InformationBarrierPolicy.md)     |Enables you to view information barrier policies in the Office 365 Security & Compliance Center         |
|[Set-informationBarrierPolicy](https://github.com/MicrosoftDocs/office-docs-powershell/blob/InfoBarrier-chrisda/exchange/exchange-ps/exchange/policy-and-compliance/Set-InformationBarrierPolicy.md)     |Enables you to modify information barrier policies in the Office 365 Security & Compliance Center         |
|[Remove-InformationBarrierPolicy](https://github.com/MicrosoftDocs/office-docs-powershell/blob/InfoBarrier-chrisda/exchange/exchange-ps/exchange/policy-and-compliance/Remove-InformationBarrierPolicy.md)     |Enables you to remove information barrier policies from the Office 365 Security & Compliance Center         |

This is typically done by a compliance administrator or a global administrator.



## Related articles

[Information barriers in Microsoft Teams](https://docs.microsoft.com/MicrosoftTeams/information-barriers-in-teams)
