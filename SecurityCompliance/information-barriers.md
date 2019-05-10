---
title: "Information barriers overview"
ms.author: deniseb
author: denisebmsft
manager: laurawi
ms.date: 04/26/2019
ms.audience: ITPro
ms.topic: article
ms.service: O365-seccomp
ms.collection:
- M365-security-compliance
localization_priority: None
description: "Use information barriers to ensure communication compliance using Microsoft Teams within your organization."
---

# Information barriers (Preview)

## Overview

Microsoft cloud services include powerful communication and collaboration capabilities. But suppose that you want to restrict communications between two groups to avoid a conflict of interest from occurring in your organization. Or, perhaps you want to restrict communications between certain people inside your organization and outside parties, in order to safeguard internal information. Information barriers can help! 

Information barriers are in preview now, and coming soon to Microsoft Teams. When these features are available for your organization, a compliance administrator or information barriers administrator can define policies to allow or prevent communications between groups of users in Microsoft Teams. Information barrier policies can be used for situations like these:

- A day trader cannot call someone on the marketing team

- Finance personnel working on confidential company information cannot receive calls from people outside their organization

- An internal team with trade secret material cannot call or chat online with people outside their organization

- A research team can only call or chat online with a product development team

For all of these example scenarios (and more), information barrier policies can be defined to prevent or allow communications in Microsoft Teams. Such poliicies can prevent people from calling or chatting with those they shouldn't, or enable people to communicate with specific groups in Microsoft Teams. With information barrier policies in effect, whenever users who are covered by those policies attempt to communicate with others in Microsoft Teams, checks are done to prevent unauthorized communication (or allow authorized communication). 

Information barrier policies determine and prevent the following kinds of unauthorized communications:

- Searching for user
- Adding a member to a team
- Starting a chat session with someone
- Starting a group chat 
- Inviting someone to join a meeting
- Sharing a screen 
- Placing a call

If the people involved are included in an information barrier policy that prevents the activity, they will not be able to proceed. To learn more about the user experience with information barriers, see [information barriers in Microsoft Teams](https://docs.microsoft.com/MicrosoftTeams/information-barriers-in-teams).

> [!IMPORTANT]
> Potentially, everyone included in an information barrier policy can be blocked from communicating with others in Microsoft Teams. When people affected by information barrier policies are part of the same team or group chat, they might be removed from those chat sessions and further communication with the group might not be allowed. However, information barriers will not apply to email communications or to file sharing through SharePoint Online or OneDrive. 

Currently, information barrier policies are defined and managed in Office 365 by using PowerShell cmdlets. This is typically done by a compliance administrator or a global administrator, and requires familiarity with PowerShell cmdlets (and parameters).

## Required licenses and permissions

**Currently, the information barrier feature is in private preview**. When these features are generally available, they'll be included in subscriptions, such as:

- Microsoft 365 E5
- Office 365 E5
- Office 365 Advanced Compliance
- Microsoft 365 E5 Information Protection and Compliance

For more details, including plans and pricing, see [Compliance Solutions](https://products.office.com/business/security-and-compliance/compliance-solutions).

To [define or edit information barrier policies](information-barriers-policies.md), you must be assigned one of the following roles:

- Microsoft 365 Global Administrator
- Office 365 Global Administrator
- Compliance Administrator

You must be familiar with PowerShell cmdlets in order to define, validate, or edit information barrier policies. Although we provide several examples of PowerShell cmdlets in the [how-to information](information-barriers-policies.md), you'll need to know additional details, such as parameters, for your organization.

## Next steps

- [Learn more about information barriers in Microsoft Teams](https://docs.microsoft.com/MicrosoftTeams/information-barriers-in-teams)
- a[See the attributes that can be used for information barrier policies](information-barriers-attributes.md)
- [Define policies for information barriers in Microsoft Teams](information-barriers-policies.md) 

