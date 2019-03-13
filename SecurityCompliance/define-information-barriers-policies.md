---
title: "Define information barrier policies"
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
description: "Learn how to define policies for information barriers in Microsoft Teams."
---

# Define policies for information barriers in Microsoft Teams (Preview)

[Information Barriers](information-barriers.md) can help limit communications between specific groups of people to help your organization comply with certain industry standards and regulations. Information barriers can also help your organization avoid potential conflicts of interest. Information barriers are implemented through policies that are defined by an Office 365 global administrator or compliance administrator.

This article describes how to define Information Barriers policies. 

> [!IMPORTANT]
> Before you define a policy, make sure to review the information in the [important considerations](#important-considerations-and-best-practices), [prerequisites](#prerequisites), and [prepare your environment](#prepare-your-environment-for-information-barriers) sections.

## Important considerations and best practices

- Information Barriers policies have effects similar to [address book policies in Exchange](https://docs.microsoft.com/exchange/address-books/address-book-policies/address-book-policies). These effects include potential limitations in people picker and email address resolution, depending on how policies are configured. We recommend using either Information Barriers policies or address book policies, but not both. 

- Information Barriers policies do not apply to email communications or to file sharing through SharePoint Online or OneDrive. 

- Potentially, everyone included in an Information Barriers policy can be blocked from communicating with others in Microsoft Teams. When people affected by Information Barriers policies are part of the same team or group chat, they might be removed from those chat sessions. To learn more, see [Learn more Information Barriers in Microsoft Teams](https://docs.microsoft.com/MicrosoftTeams/information-barriers-in-teams).

## Prerequisites

### Licenses & subscriptions

**Currently, the Information Barriers feature is in private preview**. When these features are generally available, they'll be included in subscriptions, such as:

- Microsoft 365 Enterprise E5

- Office 365 Enterprise E5

- Office 365 Advanced Compliance

- Information Protection & Compliance

For more details about these plans and compliance features, see [Compliance Solutions](https://products.office.com/business/security-and-compliance/compliance-solutions).

### Permissions

To define or edit Information Barriers policies, you must be assigned one of the following roles:

- Microsoft 365 Enterprise Global Administrator

- Office 365 Global Administrator

- Compliance Administrator

### Directory data

You must have enough data in your directory to be able to segment users. You could use attributes, such as group membership, department name, etc. as configured in Azure Active Directory (or your on-premises directory solution).

### PowerShell

Currently, Information Barriers policies are defined and managed in Office 365 by using PowerShell cmdlets. Although several scenarios and examples are provided in this article, you'll need to be familiar with PowerShell cmdlets and parameters.

## Prepare your environment for Information Barriers

**Before you define your organization's first Information Barriers policy, you must [enable scoped directory search in Microsoft Teams](https://docs.microsoft.com/MicrosoftTeams/teams-scoped-directory-search)**. Wait at least 24 hours after enabling scoped directory search before you set up or define policies for Information Barriers.

Then, follow these steps:

1. As a global administrator or compliance administrator, connect to PowerShell for Exchange Online, and connect to PowerShell for the Office 365 Security & Compliance Center.  

    - [Connect to Exchange Online PowerShell](https://docs.microsoft.com/powershell/exchange/exchange-online/connect-to-exchange-online-powershell/connect-to-exchange-online-powershell?view=exchange-ps)

    - [Connect to Office 365 Security & Compliance Center PowerShell](https://docs.microsoft.com/powershell/exchange/office-365-scc/connect-to-scc-powershell/connect-to-scc-powershell?view=exchange-ps)

    (Some cmdlets must be run for Exchange Online, and others for the Office 365 Security & Compliance Center.)

2. In the Office 365 Security & Compliance Center PowerShell window, run the following PowerShell cmdlets, one at a time:<br>

    `Login-AzureRmAccount`  

    `$appId="__TODO__"` 

    `New-AzureRmADServicePrincipal -ApplicationId $appId` 

3. When prompted, sign in using your work or school account for Office 365.

4. In the **Permissions requested** dialog box, review the information, and then choose **Accept**.

5. Gather a list of users and groups to be included in an Information Barriers policy. <br>In our example scenarios below, we have several groups predefined in Exchange (Investors, Research, Products, and Sales), and we use their Distinguished Name values in our cmdlets.

After you have completed these steps, select one of the following scenarios:

- [Scenario 1: Block communications between two groups](#scenario-1-block-communications-between-two-groups)

- [Scenario 2: Allow one group to communicate with only one other group](#scenario-2-allow-one-group-to-communicate-with-only-one-other-group)

- [Scenario 3: Prevent one group from communicating with two other groups](#scenario-3-prevent-one-group-from-communicating-with-two-other-groups)

## Scenario 1: Block communications between two groups

In this example scenario, we define an Information Barriers policy that prevents people in one group (Investors) from communicating with people in another group (Research). In our example, these groups are defined by their Department attribute in Exchange Online.

> [!IMPORTANT]
> Before you begin the following procedure, make sure you have completed the steps in the section, [Prepare your environment for Information Barriers](#prepare-your-environment-for-information-barriers). 

1. As a global administrator or compliance administrator, define the Investors and Research groups by running the following PowerShell cmdlets in Exchange Online. Run these cmdlets one at a time:

    `$investorsGroup = Get-DistributionGroup -Identity Investors | select DistinguishedName`

    `$researchGroup = Get-DistributionGroup -Identity Research | select DistinguishedName`

2. Define filter variables for the Investors group  by running the following PowerShell cmdlets in the Office 365 Security & Compliance Center. Run these cmdlets one a time:

    `$investorsFilter = "(MemberOfGroup -eq $investorsGroup)"`
    
    `$researchFilter = "(MemberOfGroup -ne $researchGroup)"` 

3. Define an Information Barriers policy that prevents the Investors group from communicating with the Research group in Microsoft Teams. Do this by running the following PowerShell cmdlet in the Office 365 Security & Compliance Center:

    `New-InformationBarrierPolicy -Name "InvestorsIBPolicy" -AssigneeFilterName "Investors" -AssigneeFilter $investorsFilter -CommunicationAllowedFilterName "NotResearch" -CommunicationAllowedFilter $researchFilter`

4. Define filter variables for the Research group  by running the following PowerShell cmdlets in the Office 365 Security & Compliance Center. Run these cmdlets one at a time:

    `$researchFilter = "(MemberOfGroup -eq $researchGroup)"`
    
    `$investorsFilter = "(MemberOfGroup -ne $investorsGroup)"`

5. Define an Information Barriers policy that prevents the Research group from communicating with the Investors group in Microsoft Teams. Do this by running the following PowerShell cmdlet in the Office 365 Security & Compliance Center:

    `New-InformationBarrierPolicy -Name "ResearchIBPolicy" -AssigneeFilterName "Research" -AssigneeFilter $researchFilter -CommunicationAllowedFilterName "NotInvestors" -CommunicationAllowedFilter $investorsFilter`

6. Apply the policies you defined in steps 1-5 by running the **Start-InformationBarrierPoliciesApplication**  cmdlets in the Office 365 Security & Compliance Center. Run these cmdlets on a time:

    `Start-InformationBarrierPoliciesApplication -InvestorsIBPolicy`

    `Start-InformationBarrierPoliciesApplication -ResearchIBPolicy`

7. Validate the policy application by running the **Get-InformationBarrierPoliciesApplicationStatus** cmdlets in the Office 365 Security & Compliance Center. Run these cmdlets one at a time:

    `Get-InformationBarrierPoliciesApplicationStatus -All -InvestorsIBPolicy`

    `Get-InformationBarrierPoliciesApplicationStatus -All -ResearchIBPolicy`

8. After you have defined your Information Barriers policy, wait at least 24 hours for the policy to work its way through your data center and services. Then, validate the Information Barriers status for a specific user by using the **Get-InformationBarrierRecipientStatus** cmdlet in the Office 365 Security & Compliance Center.

    `Get-InformationBarrierRecipientStatus`

> [!TIP]
> We recommend testing with a few users who are included in Information Barriers policies, as well as with a few users who are not included in those policies.

## Scenario 2: Allow one group to communicate with only one other group

In this example scenario, we define an Information Barriers policy that allows people in one group (Products) to communicate with only one other group (Research). With this policy in place, people in the Products group will not be able to call or chat with anyone except people in the Research group.

> [!IMPORTANT]
> Before you begin the following procedure, make sure you have completed the steps in the section, [Prepare your environment for Information Barriers](#prepare-your-environment-for-information-barriers). 

1. As a global administrator or compliance administrator, define two groups by running the following PowerShell cmdlets in Exchange Online. Run these cmdlets one a time:

    `$productsGroup = Get-DistributionGroup  -Identity Products | select DistinguishedName`
    
    `$researchGroup = Get-DistributionGroup -Identity Research | select DistinguishedName`

2. Define filter variables for the Products and Research groups  by running the following PowerShell cmdlets in the Office 365 Security & Compliance Center. Run these cmdlets one a time:

    `$productsFilter = "(MemberOfGroup -eq $productsGroup)"`
    
    `$researchFilter = "(MemberOfGroup -eq $researchGroup)"` 

3. Define an Information Barriers policy that allows the Products group to communicate with only the Research group in Microsoft Teams. Do this by running the following PowerShell cmdlet in the Office 365 Security & Compliance Center: 

    `New-InformationBarrierPolicy -Name "ProductsResearchIBPolicy" -AssigneeFilterName "Products" -AssigneeFilter $productsFilter -CommunicationAllowedFilterName "Research" -CommunicationAllowedFilter $productsFilter or $researchFilter`

4. Start the policy application by running the **Start-InformationBarrierPoliciesApplication**  cmdlet in the Office 365 Security & Compliance Center:

    `Start-InformationBarrierPoliciesApplication -ProductsResearchIBPolicy`

5. Validate the policy application by running the **Get-InformationBarrierPoliciesApplicationStatus** cmdlet in the Office 365 Security & Compliance Center:

    `Get-InformationBarrierPoliciesApplicationStatus -ProductsResearchIBPolicy`

6. After you have defined your Information Barriers policy, **wait at least 24 hours for the policy to work its way through your data center and services**. Then, validate the Information Barriers status for a specific user by running the **Get-InformationBarrierRecipientStatus** cmdlet in the Office 365 Security & Compliance Center:

    `Get-InformationBarrierRecipientStatus`

> [!TIP]
> We recommend testing with a few users who are included in Information Barriers policies, as well as with a few users who are not included in those policies.

## Scenario 3: Prevent one group from communicating with two other groups

In this scenario, we define an Information Barriers policy that prevents people in one group (Investors) to communicate with two other groups (Research and Sales). 

> [!IMPORTANT]
> Before you begin the following procedure, make sure you have completed the steps in the section, [Prepare your environment for Information Barriers](#prepare-your-environment-for-information-barriers). 

1. As a global administrator or compliance administrator, define three groups by running the following PowerShell cmdlets in Exchange Online. Run these cmdlets one a time:

    `$investorsGroup = Get-DistributionGroup -Identity Investors | select DistinguishedName`
    
    `$researchGroup = Get-DistributionGroup -Identity Research | select DistinguishedName`

    `$salesGroup = Get-DistributionGroup -Identity Sales | select DistinguishedName`

2. Define filter variables for the Investors, Research, and Sales groups by running the following PowerShell cmdlets in the Office 365 Security & Compliance Center. Run these cmdlets one a time:

    `$investorsFilter = "(MemberOfGroup -eq $investorsGroup)"`

    `$researchFilter = "(MemberOfGroup -ne $researchGroup)"`
    
    `$salesFilter = "(MemberOfGroup -ne $salesGroup"` 

3. Define an Information Barriers policy that allows the Products group to communicate with only the Research group in Microsoft Teams. Do this by running the following PowerShell cmdlet in the Office 365 Security & Compliance Center: 

    `New-InformationBarrierPolicy -Name "InvestorsResearchSalesIBPolicy"  -AssigneeFilterName "Investors" -AssigneeFilter $investorFilter -CommunicationAllowedFilterName "NotResearchAndSales"  -CommunicationFilter $researchFilter and $salesFilter`

4. Start the policy application by running the **Start-InformationBarrierPoliciesApplication**  cmdlet in the Office 365 Security & Compliance Center:

    `Start-InformationBarrierPoliciesApplication -InvestorsResearchSalesIBPolicy`

5. Validate the policy application by running the **Get-InformationBarrierPoliciesApplicationStatus** cmdlet in the Office 365 Security & Compliance Center:

    `Get-InformationBarrierPoliciesApplicationStatus -InvestorsResearchSalesIBPolicy`

6. After you have defined your Information Barriers policy, **wait at least 24 hours for the policy to work its way through your data center and services**. Then, validate the Information Barriers status for a specific user by running the following cmdlet in the Office 365 Security & Compliance Center:

    `Get-InformationBarrierRecipientStatus`

> [!TIP]
> We recommend testing with a few users who are included in Information Barriers policies, as well as with a few users who are not included in those policies.

## What if I want to edit or remove a policy?

If you want to edit or remove an Information Barriers policy, you should first set the policy to inactive status. 

### To set an Information Barriers policy to inactive status

1. As a global administrator or compliance administrator, connect to PowerShell for Exchange Online, and connect to PowerShell for the Office 365 Security & Compliance Center.  

    - [Connect to Exchange Online PowerShell](https://docs.microsoft.com/powershell/exchange/exchange-online/connect-to-exchange-online-powershell/connect-to-exchange-online-powershell?view=exchange-ps)

    - [Connect to Office 365 Security & Compliance Center PowerShell](https://docs.microsoft.com/powershell/exchange/office-365-scc/connect-to-scc-powershell/connect-to-scc-powershell?view=exchange-ps)

    (Depending on the changes you want to make, some cmdlets must be run for Exchange Online, and others for the Office 365 Security & Compliance Center.)

2. View a list of current Information Barriers policies by running the following PowerShell cmdlet in the Office 365 Security & Compliance Center:

    `Get-InformationBarrierPolicy`

3. In the list of results, identify the policy that you want to change (or remove). Make note of the policy's name.

4. To set the policy's status to inactive, run the **Set-InformationBarrierPolicy** cmdlet in the Office 365 Security & Compliance Center:

    `Set-InformationBarrierPolicy -Name "POLICYNAMEGOESHERE" -State "Inactive`

5. To apply the change (and make the policy inactive), run the **Start-InformationBarrierPoliciesApplication** cmdlet in the Office 365 Security & Compliance Center:

    `Start-InformationBarrierPoliciesApplication -POLICYNAMEGOESHERE`
    
6. (This is optional) If the process is taking a long time to finish, you can update recipients in Azure Active Directory and wait 30 minutes for FwdSync to occur. See [New address lists that you create in Exchange Online don't contain all the expected recipients](https://support.microsoft.com/help/2955640/new-address-lists-that-you-create-in-exchange-online-don-t-contain-all).

At this point, your Information Barriers policy is set to inactive. You can leave it as is, edit it, or remove it altogether.

## Related articles

[Get an overview of Information Barriers](information-barriers.md)

[Learn more Information Barriers in Microsoft Teams](https://docs.microsoft.com/MicrosoftTeams/information-barriers-in-teams)
