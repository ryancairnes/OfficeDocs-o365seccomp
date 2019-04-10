---
title: "Define information barrier policies"
ms.author: deniseb
author: denisebmsft
manager: laurawi
ms.date: 04/10/2019
ms.audience: ITPro
ms.topic: article
ms.service: O365-seccompms.collection:
- M365-security-compliance
localization_priority: None
description: "Learn how to define policies for information barriers in Microsoft Teams."
---

# Define policies for information barriers in Microsoft Teams (Preview)

[Information barriers](information-barriers.md) can help limit communications between specific groups of people to help your organization comply with certain industry standards and regulations. Information barriers can also help your organization avoid potential conflicts of interest. Information barriers are implemented through policies that are defined by an Office 365 global administrator or compliance administrator.

## Information barrier policy life cycle

Here's a high-level overview of the life cycle of an information barrier policy:

1. [Plan your policies](#plan-your-information-barrier-policies).

2. [Segment users in your organization](#segment-users).

3. [Define your information barrier policies](#define-information-barrier-policies).

4. [Apply information barrier policies](#apply-information-barrier-policies).

5. [Verify the status of information barrier policies](#verify-status-of-information-barrier-policies).

6. If necessary, [edit or remove a policy](#edit-or-remove-an-information-barrier-policy).

## Prerequisites

### Licenses & subscriptions

**Currently, the information barrier feature is in preview**. When these features are generally available, they'll be included in subscriptions, such as:

- Microsoft 365 Enterprise E5

- Office 365 Enterprise E5

- Office 365 Advanced Compliance

- Information Protection & Compliance

For more details about these plans and compliance features, see [Compliance Solutions](https://products.office.com/business/security-and-compliance/compliance-solutions).

### Permissions

To define or edit information barrier policies, you must be assigned one of the following roles:

- Microsoft 365 Enterprise Global Administrator

- Office 365 Global Administrator

- Compliance Administrator

### Directory data

You must have enough data in your directory to be able to segment users. You could use attributes, such as group membership, department name, etc. as configured in Azure Active Directory (or your on-premises directory solution).

### Scoped directory search

**Before you define your organization's first information barrier policy, you must [enable scoped directory search in Microsoft Teams](https://docs.microsoft.com/MicrosoftTeams/teams-scoped-directory-search)**. Wait at least 24 hours after enabling scoped directory search before you set up or define information barrier policies.

### PowerShell

Currently, information barrier policies are defined and managed in Office 365 by using PowerShell cmdlets. Although several scenarios and examples are provided in this article, you'll need to be familiar with PowerShell cmdlets and parameters.

## Plan your information barrier policies

Determine which groups of users for whom you want to prevent (or allow) communications to occur in Microsoft Teams (chat sessions and calls). For example, you can use information barrier policies to:
- Block communications between two groups;
- Allow one group to communicate with only one other group;
- Prevent one group from communicating with two other groups;
- ...and so on.

Make a list of all the policies you'll want to implement. As you plan your information barrier policies, keep the following points in mind:

- Information barrier policies do not apply to email communications or to file sharing through SharePoint Online or OneDrive. 

- Potentially, everyone included in an information barrier policy can be blocked from communicating with others in Microsoft Teams. When people affected by information barrier policies are part of the same team or group chat, they might be removed from those chat sessions. [Learn more information barriers in Microsoft Teams](https://docs.microsoft.com/MicrosoftTeams/information-barriers-in-teams).

- Avoid bulk moves when information barrier policies are in effect. Ask your tenant admins not to move users between segments who cannot talk to each other. Either temporarily grant communication access and disable it later, after all users are moved, or create an intermediate segment who can talk to each of the initial segments. In any case, do not move users in bulk between entities who cannot communicate.

## Segment users

To segment users, consider using an attribute in Azure Active Directory. For example, you might use Department, assuming no single employee is assigned to more than one department. To learn more, see the following resources:


|Resource  |Description  |
|---------|---------|
|[Attributes for information barrier policies (Preview)](information-barriers-attributes.md) |Use this article as a reference for various attributes you can use in information barrier policies |
|[Create a basic group and add members using Azure Active Directory](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-groups-create-azure-portal) |You can create a basic group using the Azure Active Directory (Azure AD) portal. |
|[Create a dynamic group and check status](https://docs.microsoft.com/azure/active-directory/users-groups-roles/groups-create-rule)     |In Azure Active Directory, you can use rules to determine group membership based on user or device properties. |
|[Azure AD cmdlets for working with extension attributes](https://docs.microsoft.com/powershell/azure/active-directory/using-extension-attributes-sample?view=azureadps-2.0)     | Extension attributes offer a convenient way to extend your Azure AD directory with new attributes that you can use to store attribute values for objects in your directory.  |

## Define information barrier policies

1. As a global administrator or compliance administrator, [connect to Office 365 Security & Compliance Center PowerShell](https://docs.microsoft.com/powershell/exchange/office-365-scc/connect-to-scc-powershell/connect-to-scc-powershell?view=exchange-ps).

2. Run the following PowerShell cmdlets, one at a time:<br>

    `Login-AzureRmAccount`  

    `$appId="__TODO__"` 

    `New-AzureRmADServicePrincipal -ApplicationId $appId` 

3. When prompted, sign in using your work or school account for Office 365.

4. In the **Permissions requested** dialog box, review the information, and then choose **Accept**.

5. Depending on how you want the policy to work, run a cmdlet similar to an example in the following table:

    |Example cmdlet  |Description  |
    |---------|---------|
    |`New-InformationBarrierPolicy -Name "InvestorsIBPolicy" -AssigneeFilterName "Investors" -AssigneeFilter $investorsFilter -CommunicationAllowedFilterName "NotResearch" -CommunicationAllowedFilter $researchFilter`  |Defines a policy called "InvestorsIBPolicy" that prevents people in a group called "Investors" from communicating with people in a group called "Research." |
    |`New-InformationBarrierPolicy -Name "ProductsResearchIBPolicy" -AssigneeFilterName "Products" -AssigneeFilter $productsFilter -CommunicationAllowedFilterName "Research" -CommunicationAllowedFilter $productsFilter or $researchFilter`  |Defines a policy called "ProductsResearchIBPolicy" that allows people in a group called "Products" to communicate with only people in a group called "Research."   |
    |`New-InformationBarrierPolicy -Name "InvestorsResearchSalesIBPolicy"  -AssigneeFilterName "Investors" -AssigneeFilter $investorFilter -CommunicationAllowedFilterName "NotResearchAndSales"  -CommunicationFilter $researchFilter and $salesFilter` |Defines a policy called "InvestorsResearchSalesIBPolicy" that prevents people in one group called "Investors" from communicating with people in two other groups ("Research" and "Sales").         |

Finish defining your policies, and then proceed to apply those policies.

## Apply information barrier policies

Information barrier policies are not in effect until they are applied. 

1. Run the `Start-InformationBarrierPoliciesApplication`  cmdlet in the Office 365 Security & Compliance Center.

2. Wait at least 24 hours for the policy to work its way through your data center and services. 

## Verify status of information barrier policies

1. To verify status for an information barrier policy, run the the `Get-InformationBarrierPoliciesApplicationStatus` cmdlet.

2. To verify status for a specific user, run the `Get-InformationBarrierRecipientStatus` cmdlet.

## Edit or remove an information barrier policy

If you want to edit or remove an information barrier policy, you must set the policy to inactive status. 

1. To view a list of current information barrier policies, run the `Get-InformationBarrierPolicy` cmdlet.

2. In the list of results, identify the policy that you want to change (or remove). Note the policy's name.

3. To set the policy's status to inactive, run the `Set-InformationBarrierPolicy` cmdlet.

4. Run the `Start-InformationBarrierPoliciesApplication` cmdlet.

5. If the process is taking a long time to finish, you can update recipients in Azure Active Directory and wait 30 minutes for FwdSync to occur. See [New address lists that you create in Exchange Online don't contain all the expected recipients](https://support.microsoft.com/help/2955640/new-address-lists-that-you-create-in-exchange-online-don-t-contain-all).

At this point, your information barrier policy is set to inactive. You can leave it as is, edit it, or remove it altogether.

## Related articles

[Get an overview of information barriers](information-barriers.md)

[Learn more about information barriers in Microsoft Teams](https://docs.microsoft.com/MicrosoftTeams/information-barriers-in-teams)
