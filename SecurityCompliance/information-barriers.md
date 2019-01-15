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

Among the many powerful features included in Microsoft cloud services are communication and collaboration capabilities. But suppose that you want to restrict communications between two groups to avoid a conflict of interest from occurring in your organization. Information barriers, **coming soon to [Microsoft Teams](https://docs.microsoft.com/MicrosoftTeams/information-barriers-in-teams)**, can help! Read this article to get an overview of information barriers, including what to expect, and next steps.

## How information barriers work

When information barriers become available for Microsoft Teams, your organization's security administrator or compliance administrator can define policies that limit communications between two groups of people within your organization. Currently, these policies are defined by using PowerShell cmdlets, as follows:


|PowerShell cmdlet  |Description  |
|---------|---------|
|[Get-InformationBarrierPolicy](https://github.com/MicrosoftDocs/office-docs-powershell/blob/InfoBarrier-chrisda/exchange/exchange-ps/exchange/policy-and-compliance/Get-InformationBarrierPolicy.md)     |Use the Get-InformationBarrierPolicy cmdlet to view information barrier policies in the Office 365 Security & Compliance Center         |
|[Set-informationBarrierPolicy](https://github.com/MicrosoftDocs/office-docs-powershell/blob/InfoBarrier-chrisda/exchange/exchange-ps/exchange/policy-and-compliance/Set-InformationBarrierPolicy.md)     |Use the Set-InformationBarrierPolicy cmdlet to modify information barrier policies in the Office 365 Security & Compliance Center         |
|[Remove-InformationBarrierPolicy](https://github.com/MicrosoftDocs/office-docs-powershell/blob/InfoBarrier-chrisda/exchange/exchange-ps/exchange/policy-and-compliance/Remove-InformationBarrierPolicy.md)     |Use the Remove-InformationBarrierPolicy cmdlet to remove information barrier policies from the Office 365 Security & Compliance Center         |
 
When information barrier policies are in effect, people in one group are not able to call people in the other group with Microsoft Teams.

> [!IMPORTANT]
> Information barriers for Microsoft Teams will prevent people in one group from calling people in another group, as specified in your organization's policies. In addition, potentially all the users in a policy can be blocked from communicating and will also be removed from Teams and Groups chats if they are part of the same Team or Group chat. However, these policies will not apply to email communications or to file sharing through SharePoint Online, OneDrive, or Microsoft Teams. 

Information barriers

## Related articles

[Information barriers in Microsoft Teams](https://docs.microsoft.com/MicrosoftTeams/information-barriers-in-teams)
