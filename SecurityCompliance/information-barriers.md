---
title: "Information barriers overview"
ms.author: deniseb
author: denisebmsft
manager: laurawi
ms.date: 03/13/2019
ms.audience: ITPro
ms.topic: article
ms.service: o365-administration
ms.collection:
- M365-security-compliance
localization_priority: None
description: "Use information barriers to ensure communication compliance using Microsoft Teams within your organization."
---

# Information barriers (Preview)

## Overview

Among the many powerful features included in Microsoft cloud services are communication and collaboration capabilities. But suppose that you want to restrict communications between two groups to avoid a conflict of interest from occurring in your organization. Or, suppose that you want to restrict communications between a group in your organization and outside parties to safeguard internal data. Information barriers, in preview and coming soon for Microsoft Teams, can help! 

Information barriers help limit communications in Microsoft Teams between specific groups of people. Here are a few examples:

- A day trader can be restricted from calling someone on the marketing team

- Finance personnel working on confidential company information can be prevented from receiving phone calls from people outside the organization

- An internal team working on trade secret material can be prevented from calling or chatting online with people outside the organization

- A research team can only call or chat online with a product development team

For all of these example scenarios, information barrier policies can be defined to prevent people from calling or chatting with those they shouldn't be communicating with in Microsoft Teams. Once information barrier policies are in place, when users who are covered by those policies attempt to communicate with others in Microsoft Teams, checks are in place to prevent unauthorized communication. 

Information barrier policies determine and prevent the following kinds of unauthorized communications:

- Searching for user

- Adding a member to a team

- Starting a chat session with someone

- Starting a group chat 

- Inviting someone to join a meeting

- Sharing a screen 

- Placing a call

If the people involved are included in an information barrier policy to prevent the activity, they will not be able to proceed. To learn more about the user experience with information barriers, see [information barriers in Microsoft Teams](https://docs.microsoft.com/MicrosoftTeams/information-barriers-in-teams).

> [!IMPORTANT]
> Potentially, everyone included in an information barrier policy can be blocked from communicating with others in Microsoft Teams. When people affected by information barrier policies are part of the same team or group chat, they might be removed from those chat sessions and further communication with the group might not be allowed. However, information barriers will not apply to email communications or to file sharing through SharePoint Online or OneDrive. 

Currently, information barrier policies are defined and managed in Office 365 by using PowerShell cmdlets. This is typically done by a compliance administrator or a global administrator, and requires familiarity with PowerShell cmdlets (and parameters).

## Required licenses and permissions

**Currently, the information barrier feature is in private preview**. When these features are generally available, they'll be included in subscriptions, such as:

- Microsoft 365 Enterprise E5

- Office 365 Enterprise E5

- Office 365 Advanced Compliance

- Information Protection & Compliance

For more details, including plans and pricing, see [Compliance Solutions](https://products.office.com/business/security-and-compliance/compliance-solutions).

To [define or edit information barrier policies](define-information-barriers-policies.md), you must be assigned one of the following roles:

- Microsoft 365 Enterprise Global Administrator

- Office 365 Global Administrator

- Compliance Administrator

You must be familiar with PowerShell cmdlets in order to define, validate, or edit information barrier policies. Although we provide several examples of PowerShell cmdlets in the [how-to information](define-information-barriers-policies.md), you'll need to know additional details, such as parameters, for your organization.

## Next steps

- [Learn more about the user experience of information barriers in Microsoft Teams](https://docs.microsoft.com/MicrosoftTeams/information-barriers-in-teams).

- [Define policies for information barriers in Microsoft Teams](define-information-barriers-policies.md). 

