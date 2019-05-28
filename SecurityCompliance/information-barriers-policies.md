---
title: "Define information barrier policies"
ms.author: deniseb
author: denisebmsft
manager: laurawi
ms.date: 05/28/2019
ms.audience: ITPro
ms.topic: article
ms.service: O365-seccomp
ms.collection:
- M365-security-compliance
localization_priority: None
description: "Learn how to define policies for information barriers in Microsoft Teams."
---

# Define policies for information barriers in Microsoft Teams (Preview)

With information barriers, you can define policies that are designed to prevent certain segments of users from communicating with each other, or allow specific segments to communicate only with certain other segments. Information barrier policies can help your organization maintain compliance with relevant industry standards and regulations, and avoid potential conflicts of interest. To learn more, see [Information barriers (Preview)](information-barriers.md). 

> [!IMPORTANT]
> This article describes how to plan, define, implement, and manage information barrier policies. Several steps are involved, and the work flow is divided into several parts. Make sure to read through the [prerequisites](#prerequisites) and the entire process before you begin defining (or editing) information barrier policies.

## The work flow at a glance

|Phase    |What's involved  |
|---------|---------|
|[Make sure prerequisites are met](#prerequisites)     |- Confirm that you have a subscription that includes information barriers<br/>- Verify that licenses are assigned and users are mail-enabled<br/>- Verify that you have the necessary permissions to define/edit policies<br/>- Make sure that your directory data reflects your organization's structure<br/>- Make sure that scoped directory search is enabled in Microsoft Teams<br/>- Use PowerShell (example cmdlets are provided)<br/>- Provide admin consent (steps are included)          |
|[Part 1: Segment all the users in your organization](#part-1-segment-users)     |- Determine what policies are needed<br/>- Make a list of segments to define<br/>- Identify which [attributes](information-barriers-attributes.md) to use<br/>- Define segments in terms of policy filters<br/>- (As needed) View/edit segments         |
|[Part 2: Define information barrier policies](#part-2-define-information-barrier-policies)     |- Define the policies (do not apply yet)<br/>- (As needed) View/edit policies         |
|[Part 3: Apply information barrier policies](#part-3-apply-information-barrier-policies)     |- Set policies to active status<br/>- Run the policy application<br/>- Verify policy status         |
|(As needed) [Edit or remove an information barrier policy](#edit-or-remove-an-information-barrier-policy)     |- Set a policy to inactive status<br/>- Edit or remove a policy<br/>- Run the policy application         |
|(As needed) [Troubleshooting](information-barriers-troubleshooting.md)|- Take action when policies are not working as expected<br/>- Take action if policy application appears to be stuck<br/>- [See troubleshooting for information barriers (Preview)](information-barriers-troubleshooting.md)|

## Prerequisites

### Licenses and subscriptions

**Currently, the information barrier feature is in preview**. When information barrier policies are generally available, they'll be included in the following subscriptions:
- Microsoft 365 E5
- Office 365 E5<br/>
- Office 365 Advanced Compliance
- Microsoft 365 Information Protection and Compliance

For more details about these plans and compliance features, see [Compliance Solutions](https://products.office.com/business/security-and-compliance/compliance-solutions).

Licenses must be assigned to users who will be affected by information barrier policies. In addition, users must be mail-enabled in Office 365. 

### Permissions

To define or edit information barrier policies, **you must be assigned an appropriate role**, such as one of the following:
- Microsoft 365 Enterprise Global Administrator
- Office 365 Global Administrator
- Compliance Administrator
- Information barriers administrator (this is a new role!)       

### Directory data

**Make sure that your organization's structure is reflected in directory data**. To do this, make sure that attributes, such as group membership, department name, etc. are populated correctly in Azure Active Directory (or Exchange Online).

To learn more, see the following resources:
- [Attributes for information barrier policies (Preview)](information-barriers-attributes.md)
- [Add or update a user's profile information using Azure Active Directory](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-users-profile-azure-portal).

### Scoped directory search

**Before you define your organization's first information barrier policy, you must [enable scoped directory search in Microsoft Teams](https://docs.microsoft.com/MicrosoftTeams/teams-scoped-directory-search)**. Wait at least 24 hours after enabling scoped directory search before you set up or define information barrier policies.

### PowerShell

Currently, information barrier policies are defined and managed in the Office 365 Security & Compliance Center using PowerShell cmdlets. Although several scenarios and examples are provided in this article, you'll need to be familiar with PowerShell cmdlets and parameters. 

### Connect to the Security & Compliance Center and provide admin consent

1. As a global administrator or compliance administrator, [connect to Office 365 Security & Compliance Center PowerShell](https://docs.microsoft.com/powershell/exchange/office-365-scc/connect-to-scc-powershell/connect-to-scc-powershell?view=exchange-ps).

2. Run the following PowerShell cmdlets, one at a time:<br>

    `Login-AzureRmAccount`  

    `$appId="bcf62038-e005-436d-b970-2a472f8c1982"` 

    `$sp=Get-AzureRmADServicePrincipal -ServicePrincipalName $appId` 

    `if ($sp -eq $null) { New-AzureRmADServicePrincipal -ApplicationId $appId }`

    `Start-Process  "https://login.microsoftonline.com/common/adminconsent?client_id=$appId"`

3. When prompted, sign in using your work or school account for Office 365.

4. In the **Permissions requested** dialog box, review the information, and then choose **Accept**.

## Part 1: Segment users

### Determine what policies are needed

You can use information barrier policies to block communications between segments, or to allow segments to communicate with only certain other segments. As you plan your policies, aim for the minimum number of policies to meet compliance. 

As an example, suppose that Contoso has five departments: HR, Sales, Marketing, Research, and Manufacturing. In order to remain compliant with industry regulations, people in some departments are not supposed to communicate with certain other departments, as listed in the following table:

|Segment  |Can talk to  |Cannot talk to  |
|---------|---------|---------|
|HR     |Everyone         |(no restrictions)         |
|Sales     |HR, Marketing, Manufacturing         |Research         |
|Marketing     |HR, Sales, Manufacturing         |Research         |
|Research     |HR (only)        |Sales, Marketing, Manufacturing     |
|Manufacturing |Everyone |(no restrictions) |

In this case, Contoso's plan would include two information barrier policies, as follows:

1. A policy designed to prevent Sales and Marketing from communicating with Research
2. A policy designed to allow Research to communicate with HR only 

The Manufacturing and HR departments don't have any other restrictions, so Contoso does not need additional information barrier policies at this time. 

### Make a list of segments to define

In addition to your list of needed policies, make a list of segments for your organization. Every user in your organization should belong to a segment, and no user should belong to two or more segments. Each segment can have only one information barrier policy applied. You will most likely have some segments that are not included in information barrier policies. As a best practice, plan to define segments for all users anyway.  

Referring to our example of Contoso with five departments, our plan includes one policy that will be applied to the Sales and Marketing departments, and another policy that will be applied to Research. Notice that in this example, no policies will be defined to limit HR or Manufacturing. However, the HR and Manufacturing segments will be defined anyway. 

As part of this planning process, determine which attributes in your organization's directory data you'll use to define segments. We recommend using an attribute, such as *Department* or *MemberOf*, in Azure Active Directory. To see a list of supported attributes, refer to [Attributes for information barrier policies (Preview)](information-barriers-attributes.md).

If your directory data does not have values for attributes you want to use, update user accounts. To get help with this, see the following resources:
- [Configure user account properties with Office 365 PowerShell](https://docs.microsoft.com/office365/enterprise/powershell/configure-user-account-properties-with-office-365-powershell)
- [Add or update a user's profile information using Azure Active Directory](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-users-profile-azure-portal)

> [!IMPORTANT]
> Before you proceed to the next section, make sure your directory data has values for attributes that you can use to define segments.

### Define segments in terms of policy filters

To define an organizational segment, use the `New-OrganizationSegment` cmdlet with the `UserGroupFilter` parameter that corresponds to the attribute you want to use. 

As an example, suppose that Contoso has five departments: HR, Sales, Marketing, Research, and Manufacturing. Contoso will define segments using the Department attribute in Azure Active Directory, as shown in the following examples:

`New-OrganizationSegment -Name "HRSeg" -UserGroupFilter "Department -eq 'HR'"`

`New-OrganizationSegment -Name "SalesSeg" -UserGroupFilter "Department -eq 'Sales'"`

`New-OrganizationSegment -Name "MarketingSeg" -UserGroupFilter "Department -eq 'Marketing'"`

`New-OrganizationSegment -Name "ResearchSeg" -UserGroupFilter "Department -eq 'Research'"`

`New-OrganizationSegment -Name "ManufacturingSeg" -UserGroupFilter "Department -eq 'Manufacturing'"`

After you run each cmdlet, you should see a list of details about the new segment. Details include the segment's type, who created or last modified it, and so on. 

> [!IMPORTANT]
> **Make sure that your segments do not overlap**. Each user in your organization should belong to one (and only one) segment. No user should belong to two or more segments. 


### View or edit existing segments

1. To view all existing segments, run the `Get-OrganizationSegment` cmdlet.

    You will see a list of segments and details for each, such as segment type, its UserGroupFilter value, who created or last modified it, GUID, and so on.

    > [!TIP]
    > Print or save your list of segments for reference later. For example, if you want to edit a segment, you will need to know its name or identify value (this will be used with the Identity parameter).

2. To edit a segment, use the `Set-OrganizationSegment` cmdlet with the Identity parameter and relevant details. Here's an example:

    `Set-OrganizationSegment -Identity c96e0837-c232-4a8a-841e-ef45787d8fcd -UserGroupFilter "Department -eq 'HRDept'"`

    In this example, for the segment that has the GUID "c96e0837-c232-4a8a-841e-ef45787d8fcd", we are updating the department name to "HRDept".

When you have finished defining or editing your segments, proceed to plan (or define) information barrier policies.



### A few important points to keep in mind

As you plan your information barrier policies, keep the following points in mind:

- Currently, information barrier policies do not apply to email communications or to file sharing through SharePoint Online or OneDrive. 
- Potentially, everyone included in an information barrier policy can be blocked from communicating with others in Microsoft Teams. When people affected by information barrier policies are part of the same team or group chat, they might be removed from those chat sessions. [Learn more about information barriers in Microsoft Teams](https://docs.microsoft.com/MicrosoftTeams/information-barriers-in-teams).
- Avoid bulk moves when information barrier policies are in effect. Ask your tenant admins not to move users between segments who cannot talk to each other. Either temporarily grant communication access and disable it later, after all users are moved, or create an intermediate segment who can talk to each of the initial segments. In any case, do not move users in bulk between entities who cannot communicate.

## Part 2: Define information barrier policies

When you have a list of user segments and the information barrier policies you want to define, select a scenario, and then follow the steps.

- [Scenario 1: Block communications between segments](#scenario-1-block-communications-between-segments)
- [Scenario 2: Allow a segment to communicate only with one other segment](#scenario-2-allow-a-segment-to-communicate-only-with-one-other-segment)

> [!IMPORTANT]
> As you define information barrier policies, make sure to set those policies to inactive status until you are ready to apply them. 

### Scenario 1: Block communications between segments

To block communications between segments, use the `New-InformationBarrierPolicy` cmdlet with the SegmentsBlocked parameter. 

For example, for Contoso, to prevent Sales and Marketing from communicating with Research, we would use the following cmdlet:

`New-InformationBarrierPolicy -Name "SalesMarketingBlockedFromResearch" -AssignedSegment "Sales, Marketing" -SegmentsBlocked "Research" -State Inactive`

In this example, the information barrier policy is called *SalesMarketingBlockedFromResearch*. When this policy is active and applied, it will be assigned to users who are in the Sales and Marketing segments. Everyone in those two segments will be prevented from communicating with users in the Research segment.

### Scenario 2: Allow a segment to communicate only with one other segment

To allow one segment to communicate with only one other segment, use the `New-InformationBarrierPolicy` cmdlet with the SegmentsAllowed parameter. For example, to allow Research to communicate with HR only, we would use the following cmdlet:
 
`New-InformationBarrierPolicy -Name "Research-Engineering" -AssignedSegment "Research" -SegmentsAllowed "HR" -State Active`    

In this case, Research can communicate only with HR, but HR is not restricted from communicating with other segments.

Keep in mind that by default, your information barrier policies are inactive until they are explicitly set to active status and applied. After you have defined your policies, proceed to the next section.

## Part 3: Apply information barrier policies

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

### Verify status of information barrier policies

After you have applied information barrier policies, follow these steps to verify status:

1. If you haven't already done so, as a global administrator or compliance administrator, [connect to Office 365 Security & Compliance Center PowerShell](https://docs.microsoft.com/powershell/exchange/office-365-scc/connect-to-scc-powershell/connect-to-scc-powershell?view=exchange-ps).

2. To verify status for an information barrier policy, use the `Get-InformationBarrierPoliciesApplicationStatus` cmdlet.

    If you want to view a list of all information barrier policy applications, run the following cmdlet:

    `Get-InformationBarrierPoliciesApplicationStatus -All`

3. To verify status for a specific user, run the `Get-InformationBarrierRecipientStatus -user1 username -user2 username` cmdlet, where each *username* refers to a user account in Office 365. (For example, Megan Bowen at Contoso has a user account *meganb*, and Alex Williams has a user account *alexw*.)

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

6. If the process is taking a long time to finish, you can update recipients in Azure Active Directory and wait 30 minutes for FwdSync to occur. For more details about how this works, see [New address lists that you create in Exchange Online don't contain all the expected recipients](https://support.microsoft.com/help/2955640/new-address-lists-that-you-create-in-exchange-online-don-t-contain-all).

At this point, your information barrier policy is set to inactive. You can leave it as is, edit it, or remove it altogether.

## Related articles

[Get an overview of information barriers](information-barriers.md)

[Learn more about information barriers in Microsoft Teams](https://docs.microsoft.com/MicrosoftTeams/information-barriers-in-teams)

[Attributes for information barrier policies (Preview)](information-barriers-attributes.md)

[Troubleshooting information barriers (Preview)](information-barriers-troubleshooting.md)
