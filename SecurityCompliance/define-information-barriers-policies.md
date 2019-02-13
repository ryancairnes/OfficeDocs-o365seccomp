---
title: "Define information barriers policies"
ms.author: deniseb
author: denisebmsft
manager: laurawi
ms.date: 02/13/2019
ms.audience: ITPro
ms.topic: article
ROBOTS: NOINDEX, NOFOLLOW
ms.service: o365-administration
localization_priority: None
description: "Using PowerShell, you can define policies for information barriers in Microsoft Teams."
---

# Define policies for information barriers in Microsoft Teams

Coming soon to Microsoft Teams, information barriers policies can help limit communications between specific groups of people. Information barriers can help your organization comply with industry standards and regulations, and avoid potential conflicts of interest. To learn more, see [Information barriers (coming soon to Microsoft Teams!)](information-barriers.md).

To define or edit information barriers policies, you must be assigned one of the following roles:

- Microsoft 365 Enterprise Global Administrator

- Office 365 Global Administrator

- Compliance Administrator

> [!IMPORTANT]
> Potentially, everyone included in an information barriers policy can be blocked from communicating with others in Microsoft Teams. When people affected by information barriers policies are part of the same team or group chat, they will be removed from those chat sessions. However, information barriers will not apply to email communications or to file sharing through SharePoint Online or OneDrive. 

Currently, information barriers policies are defined and managed in Office 365 by using PowerShell cmdlets. This is typically done by a compliance administrator or a global administrator, and requires familiarity with PowerShell cmdlets (and parameters). Although several scenarios and examples of PowerShell cmdlets are provided, you'll need to know additional details, such as parameters, for your organization.

## Prepare your environment for information barriers

**Before you define your organization's first information barriers policy, you must [enable scoped directory search in Microsoft Teams](https://docs.microsoft.com/MicrosoftTeams/teams-scoped-directory-search)**. Wait at least 24 hours after enabling scoped directory search before you set up or define policies for information barriers.

Then, follow these steps:

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

- [Scenario 1: Block communications between two groups](#scenario-1-block-communications-between-two-groups)

- [Scenario 2: Allow one group to communicate with only one other group](#scenario-2-allow-one-group-to-communicate-with-only-one-other-group)

- [Scenario 3: Prevent one group from communicating with two other groups](#scenario-3-prevent-one-group-from-communicating-with-two-other-groups)

## Scenario 1: Block communications between two groups

In this scenario, we will set up information barriers policies that prevent people in one group (we'll call them Investors) from communicating with people in another group (we'll call them Research).

> [!IMPORTANT]
> Before you begin the following procedure, make sure you have completed the steps in the section, [Prepare your environment for information barriers](#prepare-your-environment-for-information-barriers). 

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

6. Apply the policies you defined in steps 1-5 by running the **Start-InformationBarrierPoliciesApplication**  cmdlets.

    ```
    Start-InformationBarrierPoliciesApplication -InvestorsIBPolicy

     Start-InformationBarrierPoliciesApplication -ResearchIBPolicy
    ```

7. Validate the policy application by running the **Get-InformationBarrierPoliciesApplicationStatus** cmdlet.

    ```
    Get-InformationBarrierPoliciesApplicationStatus -All -InvestorsIBPolicy

    Get-InformationBarrierPoliciesApplicationStatus -All -ResearchIBPolicy

    ```

8. After you have defined your information barriers policy, wait at least 24 hours for the policy to work its way through your data center and services. Then, validate the information barriers status for a specific user by using the **Get-InformationBarrierRecipientStatus** cmdlet.

    ```
    Get-InformationBarrierRecipientStatus [-Identity] <RecipientIdParameter> [<CommonParameters>]
    ```

> [!TIP]
> We recommend testing with a few users who are included in information barriers policies, as well as with a few users who are not included in those policies.

## Scenario 2: Allow one group to communicate with only one other group

In this scenario, we will set up information barriers policies that allows people in one group (we'll call them Products) to communicate with only one other group (we'll call them Research).

> [!IMPORTANT]
> Before you begin the following procedure, make sure you have completed the steps in the section, [Prepare your environment for information barriers](#prepare-your-environment-for-information-barriers). 

1. As a global administrator or compliance administrator, define two groups by running the following PowerShell cmdlets in Exchange Online:

    ```
    $productsGroup = Get-DistributionGroup  -Identity Products | select DistinguishedName
    
    $researchGroup = Get-DistributionGroup -Identity Research | select DistinguishedName
    ```

2. Define filter variables for the Products and Research groups as follows:

    ```
    $productsFilter = "(MemberOfGroup -eq $productsGroup)"
    
    $researchFilter = "(MemberOfGroup -eq $researchGroup)"    
    ``` 

3. Define an information barriers policy that allows the Products group to communicate with only the Research group in Microsoft Teams, as follows: 

    ```
    New-InformationBarrierPolicy -Name "ProductsResearchIBPolicy" -AssigneeFilterName "Products" -AssigneeFilter $productsFilter -CommunicationAllowedFilterName "Research" -CommunicationAllowedFilter $researchFilter
    ```

4. Start the policy application by running the **Start-InformationBarrierPoliciesApplication**  cmdlet.

    ```
    Start-InformationBarrierPoliciesApplication -ProductsResearchIBPolicy
    ```

5. Validate the policy application by running the **Get-InformationBarrierPoliciesApplicationStatus** cmdlet.

    ```
    Get-InformationBarrierPoliciesApplicationStatus -ProductsResearchIBPolicy
    ```

6. After you have defined your information barriers policy, **wait at least 24 hours for the policy to work its way through your data center and services**. Then, validate the information barriers status for a specific user by running the **Get-InformationBarrierRecipientStatus** cmdlet.

    ```
    Get-InformationBarrierRecipientStatus [-Identity] <RecipientIdParameter> [<CommonParameters>]
    ```

> [!TIP]
> We recommend testing with a few users who are included in information barriers policies, as well as with a few users who are not included in those policies.


## Scenario 3: Prevent one group from communicating with two other groups

> [!IMPORTANT]
> Before you begin the following procedure, make sure you have completed the steps in the section, [Prepare your environment for information barriers](#prepare-your-environment-for-information-barriers). 

STEPS WILL FOLLOW SOON

## Related articles

[Get an overview of information barriers](information-barriers.md)

[Learn more about the user experience of information barriers in Microsoft Teams](https://docs.microsoft.com/SkypeForBusiness/MicrosoftTeams/information-barriers-in-teams)
