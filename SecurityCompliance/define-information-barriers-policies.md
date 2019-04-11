---
title: "Define information barrier policies"
ms.author: deniseb
author: denisebmsft
manager: laurawi
ms.date: 04/11/2019
ms.audience: ITPro
ms.topic: article
ms.service: O365-seccomp
ms.collection:
- M365-security-compliance
localization_priority: None
description: "Learn how to define policies for information barriers in Microsoft Teams."
---

# Define policies for information barriers in Microsoft Teams (Preview)

[Information barriers](information-barriers.md) can help limit communications between specific groups of people to help your organization comply with certain industry standards and regulations. Information barriers can also help your organization avoid potential conflicts of interest. Information barriers are implemented through policies that are defined by an Office 365 global administrator or compliance administrator.

## Information barrier policy life cycle

Here's a high-level overview of the life cycle of an information barrier policy:

1. **[Plan your policies](#part-1-plan-your-information-barrier-policies)**. Create a plan for the policies you need and how you want the policies to work. 

2. **[Segment users in your organization](#part-2-segment-users)**. You can use attributes in Azure Active Directory for this. Make sure that each user belongs to only one segment. For example, if you use Department, make sure no single employee is assigned to two departments.  

3. **[Define your information barrier policies](#part-3-define-information-barrier-policies)**. During this phase, you define policies. Note that the policies are neither active nor applied during this phase.

4. **[Apply information barrier policies](#part-4-apply-information-barrier-policies)**. During this phase, you set policies to active status, and then start the policy application to apply your policies. Note that if your organization is very large, it can take 24 hours for the policies to go into effect.

5. **[Verify the status of information barrier policies](#part-5-verify-status-of-information-barrier-policies)**. You can verify status individual policies and users.

6. If necessary, **[edit or remove a policy](#edit-or-remove-an-information-barrier-policy)**. To do this, you must first set the policy you want to change or remove to inactive status, and then start the policy application to put that inactive status into effect.

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

## Part 1: Plan your information barrier policies

Determine which groups of users for whom you want to prevent (or allow) communications to occur in Microsoft Teams (chat sessions and calls). For example, you can use information barrier policies to:
- Block communications between two groups;
- Allow one group to communicate with only one other group;
- Prevent one group from communicating with two other groups;
- ...and so on.

Make a list of all the policies you'll want to implement. As you plan your policies, keep the following points in mind:

- Information barrier policies do not apply to email communications or to file sharing through SharePoint Online or OneDrive. 

- Potentially, everyone included in an information barrier policy can be blocked from communicating with others in Microsoft Teams. When people affected by information barrier policies are part of the same team or group chat, they might be removed from those chat sessions. [Learn more information barriers in Microsoft Teams](https://docs.microsoft.com/MicrosoftTeams/information-barriers-in-teams).

- Avoid bulk moves when information barrier policies are in effect. Ask your tenant admins not to move users between segments who cannot talk to each other. Either temporarily grant communication access and disable it later, after all users are moved, or create an intermediate segment who can talk to each of the initial segments. In any case, do not move users in bulk between entities who cannot communicate.

## Part 2: Segment users

To segment users, consider using an attribute in Azure Active Directory. For example, you might use Department, assuming no single employee is assigned to more than one department. To learn more, see the following resources:

|Resource  |Description  |
|---------|---------|
|[Attributes for information barrier policies (Preview)](information-barriers-attributes.md) |Use this article as a reference for attributes you can use in information barrier policies |
|[Create a basic group and add members using Azure Active Directory](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-groups-create-azure-portal) |Read this article to learn how to create a basic group in the Azure Active Directory (Azure AD) portal. |
|[Create a dynamic group and check status](https://docs.microsoft.com/azure/active-directory/users-groups-roles/groups-create-rule)     |Read this article to learn how to determine group membership by using rules in Azure Active Directory. Group membership can be based on user or device properties. |
|[Azure AD cmdlets for working with extension attributes](https://docs.microsoft.com/powershell/azure/active-directory/using-extension-attributes-sample?view=azureadps-2.0)     | Read this article to learn about extension attributes and how you can extend your Azure AD directory with new attributes.  |

## Part 3: Define information barrier policies

When you have a list of user segments and the information barrier policies you want to define, follow these steps:

1. As a global administrator or compliance administrator, [connect to Office 365 Security & Compliance Center PowerShell](https://docs.microsoft.com/powershell/exchange/office-365-scc/connect-to-scc-powershell/connect-to-scc-powershell?view=exchange-ps).

2. Run the following PowerShell cmdlets, one at a time:<br>

    `Login-AzureRmAccount`  

    `$appId="bcf62038-e005-436d-b970-2a472f8c1982"` 

    `$sp=Get-AzureRmADServicePrincipal -ServicePrincipalName $appId` 

    `if ($sp -eq $null) { New-AzureRmADServicePrincipal -ApplicationId $appId }`

3. When prompted, sign in using your work or school account for Office 365.

4. In the **Permissions requested** dialog box, review the information, and then choose **Accept**.

5. Define policies by using PowerShell cmdlets, such as the examples in the following table:

    |Example cmdlet  |Description  |
    |---------|---------|
    |`New-InformationBarrierPolicy -Name "InvestorsIBPolicy" -AssigneeFilterName "Investors" -AssigneeFilter $investorsFilter -CommunicationAllowedFilterName "NotResearch" -CommunicationAllowedFilter $researchFilter`  |Defines a policy called "InvestorsIBPolicy" that prevents people in a group called "Investors" from communicating with people in a group called "Research." |
    |`New-InformationBarrierPolicy -Name "ProductsResearchIBPolicy" -AssigneeFilterName "Products" -AssigneeFilter $productsFilter -CommunicationAllowedFilterName "Research" -CommunicationAllowedFilter $productsFilter or $researchFilter`  |Defines a policy called "ProductsResearchIBPolicy" that allows people in a group called "Products" to communicate with only people in a group called "Research."   |
    |`New-InformationBarrierPolicy -Name "InvestorsResearchSalesIBPolicy"  -AssigneeFilterName "Investors" -AssigneeFilter $investorFilter -CommunicationAllowedFilterName "NotResearchAndSales"  -CommunicationFilter $researchFilter and $salesFilter` |Defines a policy called "InvestorsResearchSalesIBPolicy" that prevents people in one group called "Investors" from communicating with people in two other groups ("Research" and "Sales").         |

    Repeat this step for each information barrier policy you want to define.

Keep in mind that by default, your information barrier policies are inactive until they are explicitly set to active status and applied. After you have defined your policies, proceed to the next section.

## Part 4: Apply information barrier policies

Information barrier policies are not in effect until they are set to active status and then applied. 

1. As a global administrator or compliance administrator, [connect to Office 365 Security & Compliance Center PowerShell](https://docs.microsoft.com/powershell/exchange/office-365-scc/connect-to-scc-powershell/connect-to-scc-powershell?view=exchange-ps).

2. Run the following PowerShell cmdlets, one at a time:<br>

    `Login-AzureRmAccount`  

    `$appId="__TODO__"` 

    `New-AzureRmADServicePrincipal -ApplicationId $appId` 

3. When prompted, sign in using your work or school account for Office 365.

4. In the **Permissions requested** dialog box, review the information, and then choose **Accept**.

5. Run the `Get-InformationBarrierPolicy` cmdlet to see a list of policies that have been defined. Note the status of each policy.

6. To set a policy to active status, use the `Get-InformationBarrierPolicy` cmdlet with the State parameter set to Active, such as shown in the following example:

    
    ```powershell
    $identity  = | Get-InformationBarrierPolicy -Name "ResearchIBPolicy" | select Identity
    Set-InformationBarrierPolicy -Identity $identity -State Active
    ```
    
    In this example, we are setting an information barrier policy called ResearchIBPolicy to active status.

    Repeat this step as appropriate.

7. When you have finished setting your information barrier policies to active status, run the `Start-InformationBarrierPoliciesApplication` cmdlet in the Office 365 Security & Compliance Center.

    Policies are applied, user by user, for your organization. If your organization is large, it can take 24 hours for this process to complete.

## Part 5: Verify status of information barrier policies

After you have applied information barrier policies, follow these steps to verify status:

1. As a global administrator or compliance administrator, [connect to Office 365 Security & Compliance Center PowerShell](https://docs.microsoft.com/powershell/exchange/office-365-scc/connect-to-scc-powershell/connect-to-scc-powershell?view=exchange-ps).

2. Run the following PowerShell cmdlets, one at a time:<br>

    `Login-AzureRmAccount`  

    `$appId="__TODO__"` 

    `New-AzureRmADServicePrincipal -ApplicationId $appId` 

3. When prompted, sign in using your work or school account for Office 365.

4. In the **Permissions requested** dialog box, review the information, and then choose **Accept**.

5. To verify status for an information barrier policy, use the `Get-InformationBarrierPoliciesApplicationStatus` cmdlet.

    If you want to view a list of all information barrier policy applications, run the following cmdlet:

    `Get-InformationBarrierPoliciesApplicationStatus -All`

6. To verify status for a specific user, run the `Get-InformationBarrierRecipientStatus` cmdlet.

## Edit or remove an information barrier policy

If you want to edit or remove an information barrier policy, you must first set that policy to inactive status. 

1. To view a list of current information barrier policies, run the `Get-InformationBarrierPolicy` cmdlet.

2. In the list of results, identify the policy that you want to change (or remove). Note the policy's name.

3. To set the policy's status to inactive, use the `Set-InformationBarrierPolicy` cmdlet with the State parameter set to Inactive, as shown in the following example:


    ```powershell
    $identity  = | Get-InformationBarrierPolicy -Name "ResearchIBPolicy" | select Identity
    Set-InformationBarrierPolicy -Identity $identity -State Inactive
    ```
    In this example, we are setting an information barrier policy called ResearchIBPolicy to an inactive status.

4. Run the `Start-InformationBarrierPoliciesApplication` cmdlet.

5. If the process is taking a long time to finish, you can update recipients in Azure Active Directory and wait 30 minutes for FwdSync to occur. See [New address lists that you create in Exchange Online don't contain all the expected recipients](https://support.microsoft.com/help/2955640/new-address-lists-that-you-create-in-exchange-online-don-t-contain-all).

At this point, your information barrier policy is set to inactive. You can leave it as is, edit it, or remove it altogether.

## Related articles

[Get an overview of information barriers](information-barriers.md)

[Learn more about information barriers in Microsoft Teams](https://docs.microsoft.com/MicrosoftTeams/information-barriers-in-teams)
