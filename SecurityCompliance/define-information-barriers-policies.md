---
title: "Define Information Barriers policies"
ms.author: deniseb
author: denisebmsft
manager: laurawi
ms.date: 02/21/2019
ms.audience: ITPro
ms.topic: article
ms.service: o365-administration
ms.collection:
- M365-security-compliance
localization_priority: None
description: "Using PowerShell, you can define policies for Information Barriers in Microsoft Teams."
---

# Define policies for Information Barriers in Microsoft Teams

Coming soon to Microsoft Teams, Information Barriers policies can help limit communications between specific groups of people. Information Barriers can help your organization comply with industry standards and regulations, and avoid potential conflicts of interest. To learn more, see [Information Barriers (coming soon to Microsoft Teams!)](information-barriers.md).

To define or edit Information Barriers policies, you must be assigned one of the following roles:

- Microsoft 365 Enterprise Global Administrator

- Office 365 Global Administrator

- Compliance Administrator

> [!IMPORTANT]
> Potentially, everyone included in an Information Barriers policy can be blocked from communicating with others in Microsoft Teams. When people affected by Information Barriers policies are part of the same team or group chat, they will be removed from those chat sessions. However, Information Barriers will not apply to email communications or to file sharing through SharePoint Online or OneDrive. 

Currently, Information Barriers policies are defined and managed in Office 365 by using PowerShell cmdlets. This is typically done by a compliance administrator or a global administrator, and requires familiarity with PowerShell cmdlets (and parameters). Although several scenarios and examples of PowerShell cmdlets are provided in this article, you'll need to know additional details, such as which parameters to use for your organization.

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

After you have completed these steps, select one of the following scenarios:

- [Scenario 1: Block communications between two groups](#scenario-1-block-communications-between-two-groups)

- [Scenario 2: Allow one group to communicate with only one other group](#scenario-2-allow-one-group-to-communicate-with-only-one-other-group)

- [Scenario 3: Prevent one group from communicating with two other groups](#scenario-3-prevent-one-group-from-communicating-with-two-other-groups)

## Scenario 1: Block communications between two groups

In this example scenario, we will set up an Information Barriers policy that prevents people in one group (we'll call them Investors) from communicating with people in another group (we'll call them Research).

> [!IMPORTANT]
> Before you begin the following procedure, make sure you have completed the steps in the section, [Prepare your environment for Information Barriers](#prepare-your-environment-for-information-barriers). 

1. As a global administrator or compliance administrator, define the Investors and Research groups by running the following PowerShell cmdlets in Exchange Online. Run these cmdlets one at a time:

    `$investorsGroup = Get-DistributionGroup -Identity Investors | select DistinguishedName'`

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

In this example scenario, we will set up an Information Barriers policy that allows people in one group (we'll call them Products) to communicate with only one other group (we'll call them Research). With this policy in place, people in the Products group will not be able to call or chat with anyone except people in the Research group.

> [!IMPORTANT]
> Before you begin the following procedure, make sure you have completed the steps in the section, [Prepare your environment for Information Barriers](#prepare-your-environment-for-information-barriers). 

1. As a global administrator or compliance administrator, define two groups by running the following PowerShell cmdlets in Exchange Online. Run these cmdlets one a time:

    `$productsGroup = Get-DistributionGroup  -Identity Products | select DistinguishedName`
    
    `$researchGroup = Get-DistributionGroup -Identity Research | select DistinguishedName`

2. Define filter variables for the Products and Research groups  by running the following PowerShell cmdlets in the Office 365 Security & Compliance Center. Run these cmdlets one a time:

    `$productsFilter = "(MemberOfGroup -eq $productsGroup)"`
    
    `$researchFilter = "(MemberOfGroup -eq $researchGroup)"` 

3. Define an Information Barriers policy that allows the Products group to communicate with only the Research group in Microsoft Teams. Do this by running the following PowerShell cmdlet in the Office 365 Security & Compliance Center: 

    ```
    New-InformationBarrierPolicy -Name "ProductsResearchIBPolicy" -AssigneeFilterName "Products" -AssigneeFilter $productsFilter -CommunicationAllowedFilterName "Research" -CommunicationAllowedFilter $researchFilter
    ```

4. Start the policy application by running the **Start-InformationBarrierPoliciesApplication**  cmdlet in the Office 365 Security & Compliance Center:

    ```
    Start-InformationBarrierPoliciesApplication -ProductsResearchIBPolicy
    ```

5. Validate the policy application by running the **Get-InformationBarrierPoliciesApplicationStatus** cmdlet in the Office 365 Security & Compliance Center:

    ```
    Get-InformationBarrierPoliciesApplicationStatus -ProductsResearchIBPolicy
    ```

6. After you have defined your Information Barriers policy, **wait at least 24 hours for the policy to work its way through your data center and services**. Then, validate the Information Barriers status for a specific user by running the **Get-InformationBarrierRecipientStatus** cmdlet in the Office 365 Security & Compliance Center:

    ```
    Get-InformationBarrierRecipientStatus [-Identity] <RecipientIdParameter> [<CommonParameters>]
    ```

> [!TIP]
> We recommend testing with a few users who are included in Information Barriers policies, as well as with a few users who are not included in those policies.


## Scenario 3: Prevent one group from communicating with two other groups

In this scenario, we will set up an Information Barriers policy that prevents people in one group (we'll call them Investors) to communicate with two other groups (we'll call them Research and Sales). 

> [!IMPORTANT]
> Before you begin the following procedure, make sure you have completed the steps in the section, [Prepare your environment for Information Barriers](#prepare-your-environment-for-information-barriers). 

1. As a global administrator or compliance administrator, define three groups by running the following PowerShell cmdlets in Exchange Online:

    ```
    $investorsGroup = Get-DistributionGroup -Identity Investors | select DistinguishedName
    
    $researchGroup = Get-DistributionGroup -Identity Research | select DistinguishedName

    $salesGroup = Get-DistributionGroup -Identity Sales | select DistinguishedName 
    ```

2. Define filter variables for the Investors, Research, and Sales groups by running the following PowerShell cmdlets in the Office 365 Security & Compliance Center:

    ```
    $investorsFilter = "(MemberOfGroup -eq $investorsGroup)"

    $researchFilter = "(MemberOfGroup -ne $researchGroup)"
    
    $salesFilter = "(MemberOfGroup -ne $salesGroup"
    ``` 

3. Define an Information Barriers policy that allows the Products group to communicate with only the Research group in Microsoft Teams. Do this by running the following PowerShell cmdlet in the Office 365 Security & Compliance Center: 

    ```
    New-InformationBarrierPolicy -Name "InvestorsResearchSalesIBPolicy"  -AssigneeFilterName "Investors" -AssigneeFilter $investorFilter -CommunicationAllowedFilterName "NotResearchAndSales"  -CommunicationFilter $researchFilter and $salesFilter
    ```

4. Start the policy application by running the **Start-InformationBarrierPoliciesApplication**  cmdlet in the Office 365 Security & Compliance Center:

    ```
    Start-InformationBarrierPoliciesApplication -InvestorsResearchSalesIBPolicy
    ```

5. Validate the policy application by running the **Get-InformationBarrierPoliciesApplicationStatus** cmdlet in the Office 365 Security & Compliance Center:

    ```
    Get-InformationBarrierPoliciesApplicationStatus -InvestorsResearchSalesIBPolicy
    ```

6. After you have defined your Information Barriers policy, **wait at least 24 hours for the policy to work its way through your data center and services**. Then, validate the Information Barriers status for a specific user by running the **Get-InformationBarrierRecipientStatus** cmdlet in the Office 365 Security & Compliance Center:

    ```
    Get-InformationBarrierRecipientStatus [-Identity] <RecipientIdParameter> [<CommonParameters>]
    ```

> [!TIP]
> We recommend testing with a few users who are included in Information Barriers policies, as well as with a few users who are not included in those policies.

## Related articles

[Get an overview of Information Barriers](information-barriers.md)

[View, edit, or remove Information Barriers in Microsoft Teams](view-edit-remove-information-barriers-policies.md)

[Learn more about the user experience of Information Barriers in Microsoft Teams](https://docs.microsoft.com/SkypeForBusiness/MicrosoftTeams/information-barriers-in-teams)
