---
title: "Information barriers"
ms.author: deniseb
author: denisebmsft
manager: laurawi
ms.date: 02/07/2019
ms.audience: ITPro
ms.topic: article
ROBOTS: NOINDEX, NOFOLLOW
ms.service: o365-administration
localization_priority: None
description: "Use information barriers to ensure communication compliance using Microsoft Teams within your organization."
---

# Information barriers (coming soon to Microsoft Teams!)

## Overview

Among the many powerful features included in Microsoft cloud services are communication and collaboration capabilities. But suppose that you want to restrict communications between two groups to avoid a conflict of interest from occurring in your organization. Or, suppose that you want to restrict communications between a group in your organization and outside parties to safeguard internal data. Information barriers, coming soon for Microsoft Teams, can help! 

Information barriers help limit communications in Microsoft Teams between specific groups of people. Here are a few examples:

- A day trader can be restricted from calling someone on the marketing team

- Finance personnel working on confidential company information can be prevented from receiving phone calls from people outside the organization

- An internal team working on trade secret material can be prevented from calling or chatting online with people outside the organization

- A research team can only call or chat online with a product development team

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

Currently, information barriers policies are defined and managed in Office 365 by using PowerShell cmdlets. This is typically done by a compliance administrator or a global administrator, and requires familiarity with PowerShell cmdlets (and parameters).

## Required licenses and permissions

**Currently, the information barriers feature is in private preview**. When these features are generally available, they'll be included in subscriptions, such as:

- Microsoft 365 Enterprise E5

- Office 365 Enterprise E5

To define or edit information barriers policies, you must be assigned one of the following roles:

- Microsoft 365 Enterprise Global Administrator

- Office 365 Global Administrator

- Compliance Administrator

> [!IMPORTANT]
> You must be familiar with PowerShell cmdlets in order to perform the procedures described in this article. Although several examples of PowerShell cmdlets are provided, you'll need to know additional details, such as parameters, for your organization.

## Start here: Prepare your environment for information barriers

Before define your first information barriers policy, you must **[enable scoped directory search in Microsoft Teams](https://docs.microsoft.com/MicrosoftTeams/teams-scoped-directory-search)**. Wait at least 24 hours after enabling scoped directory search before you set up or define policies for information barriers.

Next, make sure to complete the admin consent flow. To do that, follow these steps:

1. As a global administrator or compliance administrator, create a remote PowerShell session to Office 365. Because some cmdlets will be run in Exchange Online and others in the Office 365 Security & Compliance Center, we recommend that you [connect to all Office 365 services in a single Windows PowerShell window](https://docs.microsoft.com/Office365/Enterprise/powershell/connect-to-all-office-365-services-in-a-single-windows-powershell-window).

2. Run the following PowerShell script:<br>

    ```
    Login-AzureRmAccount  
    
    $appId="__TODO__" 
     
    New-AzureRmADServicePrincipal -ApplicationId $appId 
    
    ```

3. When prompted, sign in using your work or school account.

4. In the **Permissions requested** dialog box, review the information, and then choose **Accept**.

After you have completed these steps, select one of the following scenarios:


## Scenario 1: Block communications between two groups

In this scenario, we will set up information barriers policies that prevent people in one group (we'll call them Investors) from communicating with people in another group (we'll call them Research).

> [!IMPORTANT]
> **Before you begin the following procedure, make sure you have completed the steps in the section, [Start here: Prepare your environment for information barriers](#start-here-prepare-your-environment-for-information-barriers). 

1. As a global administrator or compliance administrator, define two groups by running the following PowerShell cmdlets in Exchange Online:<br>

    ```
    $investorsGroup = Get-DistributionGroup -Identity Investors | select DistinguishedName
    
    $researchGroup = Get-DistributionGroup -Identity Research | select DistinguishedName
    ```

2. Define filter variables for the Investors group as follows:<br>

    ```
    $investorsFilter = "(MemberOfGroup -eq $investorsGroup)"
    $researchFilter = "(MemberOfGroup -ne $researchGroup)"
    ``` 

3. Define an information barriers policy that prevents the Investors group from communicating with the Research group in Microsoft Teams, as follows: <br>

    ```
    New-InformationBarrierPolicy -Name "InvestorsIBPolicy" -AssigneeFilterName "Investors" -AssigneeFilter $investorsFilter -CommunicationAllowedFilterName "NotResearch" -CommunicationAllowedFilter $researchFilter
    ```

4. Define filter variables for the Research group as follows: <br>

    ```
    $researchFilter = "(MemberOfGroup -eq $researchGroup)"
    $investorsFilter = "(MemberOfGroup -ne $investorsGroup)"
    
    ```

5. Define an information barriers policy that prevents the Research group from communicating with the Investors group in Microsoft Teams, as follows:

    ```
    New-InformationBarrierPolicy -Name "ResearchIBPolicy" -AssigneeFilterName "Research" -AssigneeFilter $researchFilter -CommunicationAllowedFilterName "NotInvestors" -CommunicationAllowedFilter $investorsFilter
    ```

## Scenario 2: Allow one group to communicate with only one other group

> [!IMPORTANT]
> **Before you begin the following procedure, make sure you have completed the steps in the section, [Start here: Prepare your environment for information barriers](#start-here-prepare-your-environment-for-information-barriers). 

## Scenario 3: Prevent one group from communicating with two other groups

## Related articles

[Information barriers in Microsoft Teams](https://docs.microsoft.com/SkypeForBusiness/MicrosoftTeams/information-barriers-in-teams)
