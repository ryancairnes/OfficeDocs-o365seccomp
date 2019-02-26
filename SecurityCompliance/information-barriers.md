---
title: "Information Barriers overview"
ms.author: deniseb
author: denisebmsft
manager: laurawi
ms.date: 02/13/2019
ms.audience: ITPro
ms.topic: article
ms.service: o365-administration
ms.collection:
- M365-security-compliance
localization_priority: None
description: "Use Information Barriers to ensure communication compliance using Microsoft Teams within your organization."
---

# Information Barriers (coming soon!)

## Overview

Among the many powerful features included in Microsoft cloud services are communication and collaboration capabilities. But suppose that you want to restrict communications between two groups to avoid a conflict of interest from occurring in your organization. Or, suppose that you want to restrict communications between a group in your organization and outside parties to safeguard internal data. Information Barriers, coming soon for Microsoft Teams, can help! 

Information Barriers help limit communications in Microsoft Teams between specific groups of people. Here are a few examples:

- A day trader can be restricted from calling someone on the marketing team

- Finance personnel working on confidential company information can be prevented from receiving phone calls from people outside the organization

- An internal team working on trade secret material can be prevented from calling or chatting online with people outside the organization

- A research team can only call or chat online with a product development team

For all of these example scenarios, Information Barriers policies can be defined to prevent people from calling or chatting with those they shouldn't be communicating with in Microsoft Teams. Once Information Barriers policies are in place, when users who are covered by those policies attempt to communicate with others in Microsoft Teams, checks are in place to prevent unauthorized communication. 

Information Barriers policies determine and prevent the following kinds of unauthorized communications:

- Searching for user

- Adding a member to a team

- Starting a chat session with someone

- Starting a group chat 

- Inviting someone to join a meeting

- Sharing a screen 

- Placing a call

If the people involved are included in an Information Barriers policy to prevent the activity, they will not be able to proceed. To learn more about the user experience with Information Barriers, see [Information Barriers in Microsoft Teams](https://docs.microsoft.com/MicrosoftTeams/information-barriers-in-teams).

> [!IMPORTANT]
> Potentially, everyone included in an Information Barriers policy can be blocked from communicating with others in Microsoft Teams. When people affected by Information Barriers policies are part of the same team or group chat, they will be removed from those chat sessions. However, Information Barriers will not apply to email communications or to file sharing through SharePoint Online or OneDrive. 

Currently, Information Barriers policies are defined and managed in Office 365 by using PowerShell cmdlets. This is typically done by a compliance administrator or a global administrator, and requires familiarity with PowerShell cmdlets (and parameters).

## Required licenses and permissions

**Currently, the Information Barriers feature is in private preview**. When these features are generally available, they'll be included in subscriptions, such as:

- Microsoft 365 Enterprise E5

- Office 365 Enterprise E5

- Office 365 Advanced Compliance

- Information Protection & Compliance

For more details, including plans and pricing, see [Compliance Solutions](https://products.office.com/business/security-and-compliance/compliance-solutions).

To [define or edit Information Barriers policies](define-information-barriers-policies.md), you must be assigned one of the following roles:

- Microsoft 365 Enterprise Global Administrator

- Office 365 Global Administrator

- Compliance Administrator

You must be familiar with PowerShell cmdlets in order to define, validate, or edit Information Barriers policies. Although we provide several examples of PowerShell cmdlets in the [how-to information](define-information-barriers-policies.md), you'll need to know additional details, such as parameters, for your organization.

## Next steps

- [Learn more about the user experience of Information Barriers in Microsoft Teams](https://docs.microsoft.com/MicrosoftTeams/information-barriers-in-teams).

- [Define policies for Information Barriers in Microsoft Teams](define-information-barriers-policies.md). 

