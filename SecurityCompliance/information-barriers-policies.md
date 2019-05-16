---
title: "Define information barrier policies"
ms.author: deniseb
author: denisebmsft
manager: laurawi
ms.date: 05/16/2019
ms.audience: ITPro
ms.topic: article
ms.service: O365-seccomp
ms.collection:
- M365-security-compliance
localization_priority: None
description: "Learn how to define policies for information barriers in Microsoft Teams."
---

# Define policies for information barriers in Microsoft Teams (Preview)

Suppose that you want to prevent one group of users from calling or chatting with another group. Or, perhaps you want to allow one group of users to communicate with only one or two other groups. Where Microsoft 365 enables communication and collaboration across groups and organizations, is there a way to restrict communications among specific groups of users?

With information barriers for Microsoft Teams, you can! If you're a compliance administrator, you can define information barrier policies to prevent or allow chats and calls between specific groups of people. With such policies in place, your organization is better positioned to comply with relevant industry standards and regulations, and avoid potential conflicts of interest within your organization.  

This article describes how to plan, define, implement, and manage information barrier policies. To learn more about information barriers, see [Information barriers (Preview)](information-barriers.md).

## The work flow at a glance


|Phase    |What's involved  |
|---------|---------|
|[Prerequisites](#prerequisites)     |- Verify the necessary licenses and permissions are assigned<br/>- Confirm directory data is available<br/>- Enable [scoped directory search in Microsoft Teams](#scoped-directory-search)<br/>- Be acquainted with [PowerShell](#powershell)         |
|[Part 1: Plan your information barrier policies](#part-1-plan-your-information-barrier-policies)     |Determine what policies are needed         |
|[Part 2: Segment users](#part-2-segment-users)     |- Define groups of users with [attributes](information-barriers-attributes.md)<br/>- Define the policy filters         |
|[Part 3: Define information barrier policies](#part-3-define-information-barrier-policies)     |Using PowerShell, define the policies<br/>(Policies are neither active nor applied at this point)         |
|[Part 4: Apply information barrier policies](#part-4-apply-information-barrier-policies)     |- Set policies to active status<br/>- Start the policy application         |
|(As needed) [Edit or remove an information barrier policy](#edit-or-remove-an-information-barrier-policy)     |- Set a policy to inactive status<br/>- Edit or remove policy<br/>- Start policy application         |
|(As needed) [Troubleshooting](information-barriers-troubleshooting.md)|Take action when policies are not working as expected, or users are blocked from communicating with others|

## Prerequisites


|Requirement  |Details  |
|---------|---------|
|Licenses & subscriptions     |**Currently, the information barrier feature is in preview**. When information barrier policies are generally available, they'll be included in the following subscriptions:<br/>- Microsoft 365 E5<br/>- Office 365 E5<br/>- Office 365 Advanced Compliance<br/>- Microsoft 365 Information Protection and Compliance<br/>For more details about these plans and compliance features, see [Compliance Solutions](https://products.office.com/business/security-and-compliance/compliance-solutions).         |
|Permissions     |To define or edit information barrier policies, you must be assigned an appropriate role, such as one of the following:<br/>- Microsoft 365 Enterprise Global Administrator<br/>- Office 365 Global Administrator<br/>- Compliance Administrator<br/>Information barriers administrator         |
|Directory data | You must have enough data in your directory to be able to segment users. You could use attributes, such as group membership, department name, etc. as configured in Azure Active Directory (or your on-premises directory solution). To learn more, see [Attributes for information barrier policies (Preview)](information-barriers-attributes.md).|
Scoped directory search | **Before you define your organization's first information barrier policy, you must [enable scoped directory search in Microsoft Teams](https://docs.microsoft.com/MicrosoftTeams/teams-scoped-directory-search)**. Wait at least 24 hours after enabling scoped directory search before you set up or define information barrier policies.
|PowerShell | Currently, information barrier policies are defined and managed in Office 365 by using PowerShell cmdlets. Although several scenarios and examples are provided in this article, you'll need to be familiar with PowerShell cmdlets and parameters.| 

## Part 1: Plan your information barrier policies

Determine which groups of users for whom you want to prevent (or allow) communications to occur in Microsoft Teams (chat sessions and calls). For example, you can use information barrier policies to:
- Block communications between two groups;
- Allow one group to communicate with only one other group;
- Prevent one group from communicating with two other groups;
- ...and so on.

Make a list of all the policies you'll want to implement. As you plan your policies, keep the following points in mind:

- Information barrier policies do not apply to email communications or to file sharing through SharePoint Online or OneDrive. 
- Potentially, everyone included in an information barrier policy can be blocked from communicating with others in Microsoft Teams. When people affected by information barrier policies are part of the same team or group chat, they might be removed from those chat sessions. [Learn more about information barriers in Microsoft Teams](https://docs.microsoft.com/MicrosoftTeams/information-barriers-in-teams).
- Avoid bulk moves when information barrier policies are in effect. Ask your tenant admins not to move users between segments who cannot talk to each other. Either temporarily grant communication access and disable it later, after all users are moved, or create an intermediate segment who can talk to each of the initial segments. In any case, do not move users in bulk between entities who cannot communicate.

## Part 2: Segment users

To segment users, consider using an attribute in Azure Active Directory. Make sure that your segments do not overlap. For example, you might use the Department attribute, assuming no single employee is assigned to more than one department. To learn more, see the following resources:

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

    `Start-Process  "https://login.microsoftonline.com/common/adminconsent?client_id=$appId"`

3. When prompted, sign in using your work or school account for Office 365.

4. In the **Permissions requested** dialog box, review the information, and then choose **Accept**.

5. Define policies by using PowerShell cmdlets, such as used in the following examples. Select a scenario, and then run the cmdlets one at a time.

    PER DHANAS, THE CMDLETS AND PROCEDURE IS CHANGING.

     The first two cmdlets identify the users who are affected, the next two define variables for your policy, and the last defines the policy using those variables.<br/>
    - **Scenario 1: Block communications between two groups**. In this example, we define a policy to prevent people in the Investors department from communicating with people in the Research department.<br/><br/>`$investorsGroup = Get-DistributionGroup -Identity Investors | select Department`<br/><br>`$researchGroup = Get-DistributionGroup -Identity Research | select Department`<br/><br/>`$investorsFilter = "(MemberOfGroup -eq $investorsGroup)"`<br/><br/>`$researchFilter = "(MemberOfGroup -ne $researchGroup)"`<br/><br/> `New-InformationBarrierPolicy -Name "InvestorsIBPolicy" -AssigneeFilterName "Investors" -AssigneeFilter $investorsFilter -CommunicationAllowedFilterName "NotResearch" -CommunicationAllowedFilter $researchFilter`<br/><br/>
    - **Scenario 2: Allow one group to communicate with only one other group**. In this example, we define a policy to allow people in the Products department to communicate with only people in the Research department. <br/><br/>`$productsGroup = Get-DistributionGroup -Identity Products | select Department`<br/><br/>`$researchGroup = Get-DistributionGroup -Identity Research | select Department`<br/><br/>`$productsFilter = "(MemberOfGroup -eq $productsGroup)"`<br/><br/>`$researchFilter = "(MemberOfGroup -eq $researchGroup)"`<br/><br/>`New-InformationBarrierPolicy -Name "ProductsResearchIBPolicy" -AssigneeFilterName "Products" -AssigneeFilter $productsFilter -CommunicationAllowedFilterName "Research" -CommunicationAllowedFilter $productsFilter or $researchFilter` <br/><br/>
    - **Scenario 3: Prevent one group from communicating with two other groups**. In this example, we define a policy to prevent people in the Investors department from communicating with people in the Research and Sales departments. <br/><br/>*NOTE: Because this scenario involves three departments, more cmdlets are used. The first three cmdlets identify the users, the next three define variables, and the last cmdlet defines the policy.*  <br/><br/>`$investorsGroup = Get-DistributionGroup -Identity Investors | select Department`<br/><br/>`$researchGroup = Get-DistributionGroup -Identity Research | select Department`<br/><br/>`$salesGroup = Get-DistributionGroup -Identity Sales | select Department`<br/><br/>`$investorsFilter = "(MemberOfGroup -eq $investorsGroup)"`<br/><br/>`$researchFilter = "(MemberOfGroup -ne $researchGroup)"`<br/><br/>`$salesFilter = "(MemberOfGroup -ne $salesGroup"`<br/><br/>`New-InformationBarrierPolicy -Name "InvestorsResearchSalesIBPolicy"  -AssigneeFilterName "Investors" -AssigneeFilter $investorFilter -CommunicationAllowedFilterName "NotResearchAndSales"  -CommunicationFilter $researchFilter and $salesFilter`  <br/><br/>

    Repeat this step for each information barrier policy you want to define.

Keep in mind that by default, your information barrier policies are inactive until they are explicitly set to active status and applied. After you have defined your policies, proceed to the next section.

## Part 4: Apply information barrier policies

Information barrier policies are not in effect until they are set to active status and then applied. 

1. If you haven't already done so, as a global administrator or compliance administrator, [connect to Office 365 Security & Compliance Center PowerShell](https://docs.microsoft.com/powershell/exchange/office-365-scc/connect-to-scc-powershell/connect-to-scc-powershell?view=exchange-ps).

2. Run the `Get-InformationBarrierPolicy` cmdlet to see a list of policies that have been defined. Note the status of each policy.

3. To set a policy to active status, use the `Get-InformationBarrierPolicy` cmdlet with the State parameter set to Active, such as shown in the following example:
    
    `$identity  = | Get-InformationBarrierPolicy -Name "ResearchIBPolicy" | select Identity
    Set-InformationBarrierPolicy -Identity $identity -State Active`
    
    In this example, we are setting an information barrier policy called `ResearchIBPolicy` to active status.

    Repeat this step as appropriate for each new policy.

4. When you have finished setting your information barrier policies to active status, run the `Start-InformationBarrierPoliciesApplication` cmdlet in the Office 365 Security & Compliance Center.

    Policies are applied, user by user, for your organization. If your organization is large, it can take 24 hours for this process to complete.

## Part 5: Verify status of information barrier policies

After you have applied information barrier policies, follow these steps to verify status:

1. If you haven't already done so, as a global administrator or compliance administrator, [connect to Office 365 Security & Compliance Center PowerShell](https://docs.microsoft.com/powershell/exchange/office-365-scc/connect-to-scc-powershell/connect-to-scc-powershell?view=exchange-ps).

2. To verify status for an information barrier policy, use the `Get-InformationBarrierPoliciesApplicationStatus` cmdlet.

    If you want to view a list of all information barrier policy applications, run the following cmdlet:

    `Get-InformationBarrierPoliciesApplicationStatus -All`

3. To verify status for a specific user, run the `Get-InformationBarrierRecipientStatus -user1 username` cmdlet, where *username* refers to the user account in Office 365. (For example, Megan Bowen at Contoso has a user account *meganb*.)

## Edit or remove an information barrier policy

If you want to edit or remove an information barrier policy, you must first set that policy to inactive status. 

1. If you haven't already done so, as a global administrator or compliance administrator, [connect to Office 365 Security & Compliance Center PowerShell](https://docs.microsoft.com/powershell/exchange/office-365-scc/connect-to-scc-powershell/connect-to-scc-powershell?view=exchange-ps).

2. To view a list of current information barrier policies, run the `Get-InformationBarrierPolicy` cmdlet.

3. In the list of results, identify the policy that you want to change (or remove). Note the policy's name.

4. To set the policy's status to inactive, use the `Set-InformationBarrierPolicy` cmdlet with the State parameter set to Inactive, as shown in the following example:

    `$identity  = | Get-InformationBarrierPolicy -Name "ResearchIBPolicy" | select Identity
    Set-InformationBarrierPolicy -Identity $identity -State Inactive`

    In this example, we are setting an information barrier policy called ResearchIBPolicy to an inactive status.

5. Run the `Start-InformationBarrierPoliciesApplication` cmdlet.

6. If the process is taking a long time to finish, you can update recipients in Azure Active Directory and wait 30 minutes for FwdSync to occur. See [New address lists that you create in Exchange Online don't contain all the expected recipients](https://support.microsoft.com/help/2955640/new-address-lists-that-you-create-in-exchange-online-don-t-contain-all).

At this point, your information barrier policy is set to inactive. You can leave it as is, edit it, or remove it altogether.

## Related articles

[Get an overview of information barriers](information-barriers.md)

[Learn more about information barriers in Microsoft Teams](https://docs.microsoft.com/MicrosoftTeams/information-barriers-in-teams)

[Attributes for information barrier policies (Preview)](information-barriers-attributes.md)

[Troubleshooting information barriers (Preview)](information-barriers-troubleshooting.md)
