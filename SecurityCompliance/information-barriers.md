---
title: "Information barriers"
ms.author: deniseb
author: denisebmsft
manager: laurawi
ms.date: 01/28/2019
ms.audience: ITPro
ms.topic: article
ms.service: o365-administration
localization_priority: None
description: "Use information barriers to ensure communication compliance using Microsoft Teams within your organization."
---

# Information barriers (coming soon to Microsoft Teams!)

## Overview

Among the many powerful features included in Microsoft cloud services are communication and collaboration capabilities. But suppose that you want to restrict communications between two groups to avoid a conflict of interest from occurring in your organization. Or, suppose that you want to restrict communications between a group in your organization and outside parties to safeguard internal data. Information barriers, coming soon for Microsoft Teams, can help! 

Read this article to get a [brief overview of information barriers](#how-information-barriers-work), and [how to define and manage policies](#define-or-manage-policies-for-information-barriers).

## How information barriers work

Information barriers help prevent communications in Microsoft Teams between specific groups of people. Here are a few examples:

- A day trader can be restricted from calling someone on the marketing team
- Finance personnel working on confidential company information can be prevented from receiving phone calls from people outside the organization
- An internal team working on trade secret material can be prevented from calling or chatting online with people outside the organization

For all of these example scenarios, information barriers policies can be defined to prevent people from calling or chatting with those they shouldn't be communicating with in Microsoft Teams. Once information barriers policies are in place, certain user activities in Microsoft Teams trigger checks against those policies to prevent unauthorized communication. These activities include:

- Adding a member to a team

- Starting a chat session with someone

- Starting a group chat 

- Inviting someone to join a meeting

- Sharing a screen 

- Placing a call

If the people involved are included in an information barriers policy to prevent the activity, they will not be able to proceed. To learn more about the user experience with information barriers, see [Information barriers in Microsoft Teams](https://docs.microsoft.com/MicrosoftTeams/information-barriers-in-teams).

> [!IMPORTANT]
> Potentially, everyone included in an information barriers policy can be blocked from communicating with others in Microsoft Teams. When people affected by information barriers policies are part of the same team or group chat, they will be removed from those chat sessions. However, information barriers will not apply to email communications or to file sharing through SharePoint Online or OneDrive. 

## Define or manage policies for information barriers

Currently, information barriers policies are defined and managed in the Office 365 Security & Compliance Center using PowerShell cmdlets. This is typically done by a compliance administrator or a global administrator.

### Define an information barriers policy

> [!IMPORTANT]
> **Before you begin the following procedure, you must [enable scoped directory search in Microsoft Teams](https://docs.microsoft.com/MicrosoftTeams/teams-scoped-directory-search)**. Wait at least 24 hours after enabling scoped directory search before you set up or define policies for information barriers. 

1. As a global administrator or compliance administrator, create a remote PowerShell session to the Security & Compliance Center. (To get help with this, see [Connect to Office 365 Security & Compliance Center PowerShell](https://docs.microsoft.com/powershell/exchange/office-365-scc/connect-to-scc-powershell).)

2. Define a policy by running the **New-InformationBarrierPolicy** cmdlet.<br>
    ```
    New-InformationBarrierPolicy [-Name] <String> -AssigneeFilter <String> -AssigneeFilterName <String> -CommunicationAllowedFilter <String> -CommunicationAllowedFilterName <String>
     [-Comment <String>]
     [-Confirm]
     [-State <EopInformationBarrierPolicyState>]
     [-WhatIf] [<CommonParameters>]
    ```
<br>

3. Start the policy application by running the **Start-InformationBarrierPoliciesApplication**  cmdlet.<br>
    ```
    Start-InformationBarrierPoliciesApplication [[-Identity] <PolicyIdParameter>] [-Confirm] [-WhatIf]
     [<CommonParameters>]
    ```
<br>

4. Validate the policy application by running the **Get-InformationBarrierPoliciesApplicationStatus** cmdlet.<br>
    ```
    Get-InformationBarrierPoliciesApplicationStatus [-All <Boolean>] [[-Identity] <PolicyIdParameter>]
     [<CommonParameters>]
    ```

5. After you have defined your information barriers policy, wait at least 24 hours for the policy to work its way through your data center and services. Then, validate the information barriers status for a specific user by running the **Get-InformationBarrierRecipientStatus** cmdlet.<br>
    ```
    Get-InformationBarrierRecipientStatus [-Identity] <RecipientIdParameter> [<CommonParameters>]
    ```

> [!TIP]
> We recommend testing with a few users who are included in information barriers policies, as well as with a few users who are not included in those policies.

### View and edit information barriers policies

1. As a global administrator or compliance administrator, create a remote PowerShell session to the Security & Compliance Center. (To get help with this, see [Connect to Office 365 Security & Compliance Center PowerShell](https://docs.microsoft.com/powershell/exchange/office-365-scc/connect-to-scc-powershell).)

2. View your organization's existing information barriers policies by running the **Get-InformationBarrierPolicy** cmdlet.<br>
    ```
    Get-InformationBarrierPolicy [-ExoPolicyId <Guid>] [<CommonParameters>]
    ```

3. To edit an information barriers policy, run the **Set-InformationBarrierPolicy** cmdlet.<br>
    ```
    Set-InformationBarrierPolicy [-AssigneeFilter <String>] [-AssigneeFilterName <String>] [-Comment <String>]
     [-CommunicationAllowedFilter <String>] [-CommunicationAllowedFilterName <String>]
     [-Identity] <PolicyIdParameter> [-State <EopInformationBarrierPolicyState>] [<CommonParameters>]
    ```

4. Run the policy application using the **Start-InformationBarrierPoliciesApplication** cmdlet.<br>
    ```
    Start-InformationBarrierPoliciesApplication [[-Identity] <PolicyIdParameter>] [-Confirm] [-WhatIf]
     [<CommonParameters>]
    ```

> [!IMPORTANT]
> If your organization has personnel changes that affect an information barriers policy, such as a change in position, adding or removing a user, and so on, allow 24 hours for the changes to take effect. 

### Remove an information barriers policy

1. As a global administrator or compliance administrator, create a remote PowerShell session to the Security & Compliance Center. (To get help with this, see [Connect to Office 365 Security & Compliance Center PowerShell](https://docs.microsoft.com/powershell/exchange/office-365-scc/connect-to-scc-powershell).)

2. View your organization's existing information barriers policies by running the Get-InformationBarrierPolicy (https://github.com/MicrosoftDocs/office-docs-powershell/blob/InfoBarrier-chrisda/exchange/exchange-ps/exchange/policy-and-compliance/Get-InformationBarrierPolicy.md) cmdlet.

3. Run the Remove-InformationBarrierPolicy (https://github.com/MicrosoftDocs/office-docs-powershell/blob/InfoBarrier-chrisda/exchange/exchange-ps/exchange/policy-and-compliance/Set-InformationBarrierPolicy.md) cmdlet.

> [!IMPORTANT]
> Allow 24 hours for your changes to take effect. 

## Required licenses and permissions

INFO COMING SOON

## Related articles

https://github.com/MicrosoftDocs/OfficeDocs-SkypeForBusiness-pr/blob/v-sharos-info-barriers/Teams/information-barriers-in-teams.md
