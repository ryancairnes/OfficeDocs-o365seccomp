---
title: "Information barriers"
ms.author: deniseb
author: denisebmsft
manager: laurawi
ms.date: 01/16/2019
ms.audience: Admin
ms.topic: article
ms.service: o365-administration
localization_priority: None
description: "Use information barriers to ensure communication compliance within your organization."
---

# Information barriers

## Overview

Among the many powerful features included in Microsoft cloud services are communication and collaboration capabilities. But suppose that you want to restrict communications between two groups to avoid a conflict of interest from occurring in your organization. Or, suppose that you want to restrict communications between a group in your organization and outside parties to safeguard internal information. Information barriers, coming soon for Microsoft Teams, can help! 

Read this article to get a brief overview of information barriers, and how to define policies.

## How information barriers work

Information barriers help prevent communications in Microsoft Teams between specific groups of people. Here are a few examples:

- A day trader can be restricted from calling someone on the marketing team
- Finance personnel working on confidential company information can be prevented from receiving phone calls from people outside the organization
- An internal team working on trade secret material can be prevented from calling or chatting online with people outside the organization

For all of these example scenarios, information barriers policies can be defined to prevent people from calling or chatting with those they shouldn't be communicating with in Microsoft Teams. Once information barriers policies are in place, certain user activities in Microsoft Teams trigger checks against those policies to prevent unauthorized communication. These activities include:

- Adding a member to a team

- Starting a chat 

- Inviting someone to join a meeting

- Sharing a screen 

- Placing a call

If the people involved are included in an information barriers policy to prevent the activity, they will not be able to proceed. 

> [!IMPORTANT]
> Potentially, everyone included in an information barriers policy can be blocked from communicating with others in Microsoft Teams. When people affected by information barriers policies are part of the same team or group chat, they will be removed from those chat sessions. However, information barriers will not apply to email communications or to file sharing through SharePoint Online or OneDrive. 

To learn more about the user experience with information barriers, see [Information barriers in Microsoft Teams](https://docs.microsoft.com/MicrosoftTeams/information-barriers-in-teams).

## How to define policies for information barriers

Currently, information barriers policies are defined and managed in the Office 365 Security & Compliance Center using PowerShell cmdlets. This is typically done by a compliance administrator or a global administrator.

1. As a global administrator or compliance administrator, create a remote PowerShell session to the Security & Compliance Center. (To get help with this, see [Connect to Office 365 Security & Compliance Center PowerShell](https://docs.microsoft.com/powershell/exchange/office-365-scc/connect-to-scc-powershell).)

2. Depending on whether you want to view, modify, or remove an information barriers policy, use one of the following PowerShell cmdlets.
    - To view existing policies, see  [Get-InformationBarrierPolicy](https://github.com/MicrosoftDocs/office-docs-powershell/blob/InfoBarrier-chrisda/exchange/exchange-ps/exchange/policy-and-compliance/Get-InformationBarrierPolicy.md)
    - To define or edit a policy, see  [Set-informationBarrierPolicy](https://github.com/MicrosoftDocs/office-docs-powershell/blob/InfoBarrier-chrisda/exchange/exchange-ps/exchange/policy-and-compliance/Set-InformationBarrierPolicy.md)
    - To remove a policy, see [Remove-InformationBarrierPolicy](https://github.com/MicrosoftDocs/office-docs-powershell/blob/InfoBarrier-chrisda/exchange/exchange-ps/exchange/policy-and-compliance/Remove-InformationBarrierPolicy.md)

3. After your information barriers policies are in place, wait about 30 minutes for those policies to work their way through your data center and services, and then test your policies, and adjust as needed.<br>We recommend testing with a few users who are and aren't included in information barriers policies.



## Related articles

[Information barriers in Microsoft Teams](https://docs.microsoft.com/MicrosoftTeams/information-barriers-in-teams)
