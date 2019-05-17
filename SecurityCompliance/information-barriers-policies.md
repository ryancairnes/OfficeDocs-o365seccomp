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

Suppose that you want to prevent one group of users from calling or chatting with another group. Or, perhaps you want to allow one group of users to communicate with only one or two other groups. Microsoft 365 enables communication and collaboration across groups and organizations, so is there a way to restrict communications among specific groups of users when necessary? With information barriers for Microsoft Teams, you can! 

If you're a global administrator, compliance administrator, or information barrier administrator, you can define policies that are designed to prevent or allow chats and calls between specific groups of people. With such policies in place, your organization is better positioned to comply with relevant industry standards and regulations, and avoid potential conflicts of interest within your organization.  

This article describes how to plan, define, implement, and manage information barrier policies. To learn more about information barriers, see [Information barriers (Preview)](information-barriers.md).

## The work flow at a glance


|Phase    |What's involved  |
|---------|---------|
|[Prerequisites](#prerequisites)     |- Verify that licenses are assigned<br/>- Verify that you have the necessary permissions<br/>- Confirm that directory data is available<br/>- Make sure [scoped directory search is enabled in Microsoft Teams](#scoped-directory-search)<br/>- Be familiar with [PowerShell](#powershell) (Example cmdlets are provided)         |
|[Part 1: Plan your information barrier policies](#part-1-plan-your-information-barrier-policies)     |- Make a list of groups (segments) who will be affected by information barriers<br/>- Determine which policies are needed|
|[Part 2: Segment users](#part-2-segment-users)     |- Identify which [attributes](information-barriers-attributes.md) to use<br/>- Define the segments in terms of policy filters<br/>- View (and if needed, edit) the segments         |
|[Part 3: Define information barrier policies](#part-3-define-information-barrier-policies)     |- Define the policies<br/>- View (and if needed, edit) the policies<br/>(Policies are neither active nor applied at this point)         |
|[Part 4: Apply information barrier policies](#part-4-apply-information-barrier-policies)     |- Set policies to active status<br/>- Run the policy application         |
|(As needed) [Edit or remove an information barrier policy](#edit-or-remove-an-information-barrier-policy)     |- Set a policy to inactive status<br/>- Edit or remove a policy<br/>- Run the policy application         |
|(As needed) [Troubleshooting](information-barriers-troubleshooting.md)|Take action when policies are not working as expected, or when the policy application process is taking too long|

## Prerequisites

|Requirement  |Details  |
|---------|---------|
|Licenses & subscriptions     |**Currently, the information barrier feature is in preview**. When information barrier policies are generally available, they'll be included in the following subscriptions:<br/>- Microsoft 365 E5<br/>- Office 365 E5<br/>- Office 365 Advanced Compliance<br/>- Microsoft 365 Information Protection and Compliance<br/>For more details about these plans and compliance features, see [Compliance Solutions](https://products.office.com/business/security-and-compliance/compliance-solutions).         |
|Permissions     |To define or edit information barrier policies, you must be assigned an appropriate role, such as one of the following:<br/>- Microsoft 365 Enterprise Global Administrator<br/>- Office 365 Global Administrator<br/>- Compliance Administrator<br/>- Information barriers administrator         |
|Directory data | You must have enough data in your directory to be able to segment users. Consider using attributes, such as group membership, department name, etc. as configured in Azure Active Directory (or Exchange Online). To learn more, see [Attributes for information barrier policies (Preview)](information-barriers-attributes.md).|
Scoped directory search | **Before you define your organization's first information barrier policy, you must [enable scoped directory search in Microsoft Teams](https://docs.microsoft.com/MicrosoftTeams/teams-scoped-directory-search)**. Wait at least 24 hours after enabling scoped directory search before you set up or define information barrier policies.
|PowerShell | Currently, information barrier policies are defined and managed in the Office 365 Security & Compliance Center using PowerShell cmdlets. Although several scenarios and examples are provided in this article, you'll need to be familiar with PowerShell cmdlets and parameters.| 

## Part 1: Plan your information barrier policies

Determine the groups of users for whom you want to prevent (or allow) communications to occur in Microsoft Teams (chat sessions and calls). For example, you can use information barrier policies to:
- Block communications between two groups;
- Allow one group to communicate with only one other group;
- Prevent one group from communicating with two other groups;
- ...and so on.

As an example, Contoso set up a table to determine which departments can (or cannot) talk to each other, like this:

|Group  |Can talk to  |Cannot talk to  |
|---------|---------|---------|
|HR     |Everyone         |(no restrictions)         |
|Sales     |HR, Marketing         |Research         |
|Marketing     |HR, Product Development, Sales         |Research         |
|Research     |HR, Product Development         |     |

In this case, the list of information barrier policies to define would include the following:

- Prevent Sales from communicating with Research (and vice versa)
- Prevent Marketing from communicating with Research (and vice versa)
- Allow Research to communicate with HR and Product Development only 

### A few important points to keep in mind

As you plan your information barrier policies, keep the following points in mind:

- Currently, information barrier policies do not apply to email communications or to file sharing through SharePoint Online or OneDrive. 
- Potentially, everyone included in an information barrier policy can be blocked from communicating with others in Microsoft Teams. When people affected by information barrier policies are part of the same team or group chat, they might be removed from those chat sessions. [Learn more about information barriers in Microsoft Teams](https://docs.microsoft.com/MicrosoftTeams/information-barriers-in-teams).
- Avoid bulk moves when information barrier policies are in effect. Ask your tenant admins not to move users between segments who cannot talk to each other. Either temporarily grant communication access and disable it later, after all users are moved, or create an intermediate segment who can talk to each of the initial segments. In any case, do not move users in bulk between entities who cannot communicate.

## Part 2: Segment users

To segment users, consider using an attribute in Azure Active Directory. Make sure that your segments do not overlap. For example, you might use the Department attribute, assuming no single employee is assigned to more than one department. To see a list of supported attributes, refer to [Attributes for information barrier policies (Preview)](information-barriers-attributes.md).

1. As a global administrator or compliance administrator, [connect to Office 365 Security & Compliance Center PowerShell](https://docs.microsoft.com/powershell/exchange/office-365-scc/connect-to-scc-powershell/connect-to-scc-powershell?view=exchange-ps).

2. Run the following PowerShell cmdlets, one at a time:<br>

    `Login-AzureRmAccount`  

    `$appId="bcf62038-e005-436d-b970-2a472f8c1982"` 

    `$sp=Get-AzureRmADServicePrincipal -ServicePrincipalName $appId` 

    `if ($sp -eq $null) { New-AzureRmADServicePrincipal -ApplicationId $appId }`

    `Start-Process  "https://login.microsoftonline.com/common/adminconsent?client_id=$appId"`

3. When prompted, sign in using your work or school account for Office 365.

4. In the **Permissions requested** dialog box, review the information, and then choose **Accept**.

5. To define an organizational segment, use the `New-OrganizationSegment` cmdlet with the `UserGroupFilter` parameter that corresponds to the attribute you want to use. Make sure that the attribute you use to define your segment is such that no single person belongs to more than one segment. Here's an example:

    `New-OrganizationSegment -Name "HR" -UserGroupFilter "Department -eq 'HR'"`

    In this example, we are defining a segment called HR. The segment includes people who have HR listed as their department. (In this case, no employees are assigned to more than one department.)

    After you run the cmdlet, you should see a list of details about the new segment. Details include the segment's type, who created or last modified it, and so on. 

6. Repeat the previous step for each segment. 

### View or edit existing segments

1. If you haven't already done so, as a global administrator or compliance administrator, [connect to Office 365 Security & Compliance Center PowerShell](https://docs.microsoft.com/powershell/exchange/office-365-scc/connect-to-scc-powershell/connect-to-scc-powershell?view=exchange-ps).

2. To view a list of existing segments, run the `Get-OrganizationSegment` cmdlet.

    You will see a list of segments and details for each. Details include each segment's type, who created or last modified it, and so on. 

    > [!TIP]
    > Print or save your list of segments for reference later. For example, if you want to edit a segment, you will need to know its Identity.

3. To edit a segment, use the `Set-OrganizationSegment` cmdlet with the Identity parameter and relevant details. Here's an example:

    `Set-OrganizationSegment -Identity "FFO.extest.microsoft.com/Microsoft Exchange Hosted Organizations/IBAPCorp04.onmicrosoft.com/Configuration/HR" -UserGroupFilter "Department -eq 'HRDept'"`

    In this example, we are updating the department name from "HR" to "HRDept" for the segment that has the Identity value of `FFO.extest.microsoft.com/Microsoft Exchange Hosted Organizations/IBAPCorp04.onmicrosoft.com/Configuration/HR`.

When you have finished editing your existing segments, proceed to define information barrier policies.

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



Keep in mind that by default, your information barrier policies are inactive until they are explicitly set to active status and applied. After you have defined your policies, proceed to the next section.

## Part 4: Apply information barrier policies

Information barrier policies are not in effect until they are set to active status and then applied. 

1. If you haven't already done so, as a global administrator or compliance administrator, [connect to Office 365 Security & Compliance Center PowerShell](https://docs.microsoft.com/powershell/exchange/office-365-scc/connect-to-scc-powershell/connect-to-scc-powershell?view=exchange-ps).

2. Run the `Get-InformationBarrierPolicy` cmdlet to see a list of policies that have been defined. Note the status of each policy.

3. To set a policy to active status, use the `Set-InformationBarrierPolicy` cmdlet with the State parameter set to Active, such as shown in the following example:
    
    `$identity  = | Set-InformationBarrierPolicy -Name "ResearchIBPolicy" | select Identity
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
