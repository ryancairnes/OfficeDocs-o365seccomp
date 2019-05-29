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
|(As needed) [Edit or remove an information barrier policy](#edit-or-remove-an-information-barrier-policy)     |- Set a policy to inactive status<br/>- Edit or remove a policy<br/>- Run the policy application<br/>- Verify policy status         |
|(As needed) [Troubleshooting](information-barriers-troubleshooting.md)|- Take action when policies are not working as expected<br/>- [See troubleshooting for information barriers (Preview)](information-barriers-troubleshooting.md)|

## Prerequisites

### Licenses and subscriptions

**Currently, the information barrier feature is in preview**. When information barrier policies are generally available, they'll be included in the following subscriptions:
- Microsoft 365 E5
- Office 365 E5
- Office 365 Advanced Compliance
- Microsoft 365 Information Protection and Compliance

For more details about these plans and compliance features, see [Compliance Solutions](https://products.office.com/business/security-and-compliance/compliance-solutions).

Licenses must be assigned to users who are affected by information barrier policies. In addition, users must be mail-enabled in Office 365. 

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

**Currently, information barrier policies are defined and managed in the Office 365 Security & Compliance Center using PowerShell cmdlets**. Although several scenarios and examples are provided in this article, you'll need to be familiar with PowerShell cmdlets and parameters. 

### Connect to the Security & Compliance Center and provide admin consent

Use the following procedure before you define (or edit) segments or information barrier policies.

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

During this phase, you determine what policies are needed, make a list of segments to define, and then define your segments.

### Determine what policies are needed

Make a list of information barrier policies needed for your organization. You can use information barrier policies to:
- Block communications between certain segments; or 
- Allow communications between certain segments.

Prepare a plan that includes the minimum number of policies you need for compliance. As you plan your information barrier policies, keep the following points in mind:
- Currently, information barrier policies do not apply to email communications or to file sharing through SharePoint Online or OneDrive. 
- Potentially, everyone included in an information barrier policy can be blocked from communicating with others in Microsoft Teams. When people affected by information barrier policies are part of the same team or group chat, they might be removed from those chat sessions. [Learn more about information barriers in Microsoft Teams](https://docs.microsoft.com/MicrosoftTeams/information-barriers-in-teams).


### Make a list of segments to define

In addition to your list of needed policies, make a list of segments for your organization. Every user in your organization should belong to a segment, and no user should belong to two or more segments. Each segment can have only one information barrier policy applied. You will most likely have some segments that are not included in information barrier policies. As a best practice, plan to define segments for all users anyway.  

Determine which attributes in your organization's directory data you'll use to define segments. Consider using *Department* or *MemberOf*, assuming you have values in those attributes for all users. To see a list of supported attributes, refer to [Attributes for information barrier policies (Preview)](information-barriers-attributes.md).

> [!IMPORTANT]
> **Before you proceed to the next section, make sure your directory data has values for attributes that you can use to define segments**. If your directory data does not have values for the attributes you want to use, then all user accounts must be updated to include that information before you proceed with information barriers. To get help with this, see the following resources:<br/>- [Configure user account properties with Office 365 PowerShell](https://docs.microsoft.com/office365/enterprise/powershell/configure-user-account-properties-with-office-365-powershell)<br/>- [Add or update a user's profile information using Azure Active Directory](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-users-profile-azure-portal)


### Define segments with policy filters

1. To define an organizational segment, use the `New-OrganizationSegment` cmdlet with the `UserGroupFilter` parameter that corresponds to the attribute you want to use. 

    Example: `New-OrganizationSegment -Name "Segment1" -UserGroupFilter "Department -eq 'Department1'"`

    In this example, a segment called *Segment1* is defined using *Department1*, a value in the Department attribute.

2. Repeat step 1 for each segment you want to define.

    After you run each cmdlet, you should see a list of details about the new segment. Details include the segment's type, who created or last modified it, and so on. 

> [!IMPORTANT]
> **Make sure that your segments do not overlap**. Each user in your organization should belong to one (and only one) segment. No user should belong to two or more segments. Segments should be defined for all users in your organization. 


### View or edit existing segments

1. To view all existing segments, use the `Get-OrganizationSegment` cmdlet.

    You will see a list of segments and details for each, such as segment type, its UserGroupFilter value, who created or last modified it, GUID, and so on.

    > [!TIP]
    > Print or save your list of segments for reference later. For example, if you want to edit a segment, you will need to know its name or identify value (this is used with the Identity parameter).

2. To edit a segment, use the `Set-OrganizationSegment` cmdlet with the Identity parameter and relevant details. Here's an example:

    `Set-OrganizationSegment -Identity c96e0837-c232-4a8a-841e-ef45787d8fcd -UserGroupFilter "Department -eq 'HRDept'"`

    In this example, for the segment that has the GUID *c96e0837-c232-4a8a-841e-ef45787d8fcd*, we are updating the department name to "HRDept".

When you have finished defining or editing your segments, proceed to [define](#part-2-define-information-barrier-policies) (or [edit](#edit-or-remove-an-information-barrier-policy)) information barrier policies.

## Part 2: Define information barrier policies

When you have a list of user segments and the information barrier policies you want to define, select a scenario, and then follow the steps.

- [Scenario 1: Block communications between segments](#scenario-1-block-communications-between-segments)
- [Scenario 2: Allow a segment to communicate only with one other segment](#scenario-2-allow-a-segment-to-communicate-only-with-one-other-segment)

> [!IMPORTANT]
> As you define information barrier policies, make sure to set those policies to inactive status until you are ready to apply them. 

### Scenario 1: Block communications between segments

1. To block communications between segments, use the `New-InformationBarrierPolicy` cmdlet with the **SegmentsBlocked** parameter. 

    Example: `New-InformationBarrierPolicy -Name "Seg1CannotTalkToSeg2" -AssignedSegment "Seg1" -SegmentsBlocked "Seg2" -State Inactive`

    In this case, we are defining a policy called *Seg1CannotTalkToSeg2*. This policy can be applied to users in a segment called *Seg1*. When active and applied, this policy will help prevent people in *Seg1* from communicating with people in a segment called *Seg2*.

2. Do one of the following:

   - Repeat step 1 for each policy you want to define to block communications
   - Proceed to [Scenario 2: Allow a segment to communicate only with one other segment](#scenario-2-allow-a-segment-to-communicate-only-with-one-other-segment) 
   - [View or edit an information barrier policy](#edit-or-remove-an-information-barrier-policy)
   - Proceed to [Part 3: Apply information barrier policies](#part-3-apply-information-barrier-policies)

### Scenario 2: Allow a segment to communicate only with one other segment

1. To allow one segment to communicate with only one other segment, use the `New-InformationBarrierPolicy` cmdlet with the **SegmentsAllowed** parameter. 

    Example: `New-InformationBarrierPolicy -Name "Seg3CanOnlyTalkToSeg4" -AssignedSegment "Seg3" -SegmentsAllowed "Seg4" -State Inactive`

    In this case, we are defining a policy called *Seg3CanOnlyTalkToSeg4*. This policy can be applied to users in a segment called *Seg3*. When active and applied, this policy will allow people in *Seg3* to communicate only with people in a segment called *Seg4*. (In this case, Seg3 cannot communicate with users who are not part of Seg4.)

2. Do one of the following:

   - Repeat step 1 for each policy you want to define to allow communications
   - Go to [Scenario 1: Block communications between segments](#scenario-1-block-communications-between-segments) 
   - [View or edit an information barrier policy](#edit-or-remove-an-information-barrier-policy)
   - Proceed to [Part 3: Apply information barrier policies](#part-3-apply-information-barrier-policies)

## Part 3: Apply information barrier policies

Information barrier policies are not in effect until they are set to active status and then applied. 

1. Use the `Get-InformationBarrierPolicy -Organization $org` cmdlet to see a list of policies that have been defined. Note the status and identity (GUID) of each policy.

2. To set a policy to active status, use the `Set-InformationBarrierPolicy` cmdlet with an Identity parameter, and the State parameter set to Active. Here's an example:
    
    `Set-InformationBarrierPolicy -Identity 43c37853-ea10-4b90-a23d-ab8c93772471 -State Active`
    
    In this example, we are setting an information barrier policy that has the GUID *43c37853-ea10-4b90-a23d-ab8c93772471* to active status.

    Repeat this step as appropriate for each policy.

3. When you have finished setting your information barrier policies to active status, use the `Start-InformationBarrierPoliciesApplication` cmdlet in the Office 365 Security & Compliance Center.

    Policies are applied, user by user, for your organization. If your organization is large, it can take 24 hours (or more) for this process to complete.

## Verify status of information barrier policies

After you have applied information barrier policies, follow these steps to verify status:

1. To view a list of all information barrier policy applications, use the `Get-InformationBarrierPoliciesApplicationStatus -All` cmdlet.

    This will confirm whether policy application completed, failed, or is in progress.

2. To view a list of information barrier policies, use the `Get-InformationBarrierPolicy -Organization $org` cmdlet.

    This will display a list of policies and their status.

3. To view information about segments, use the `Get-OrganizationSegment` cmdlet.

    This will display a list of segments defined for your organization.
    
3. To verify status for a specific user, use the `Get-InformationBarrierRecipientStatus` cmdlet with Identity parameters. 

    For example,  you could use `Get-InformationBarrierRecipientStatus -user1 username -user2 username`, where each *username* refers to a user account in Office 365. 
    
    This would return information about two users, such as whether a policy is defined that affects the users.

## Edit or remove an information barrier policy

If you want to edit or remove an information barrier policy, you must first set that policy to inactive status. 

### Set a policy to inactive status

1. To view a list of current information barrier policies, use the `Get-InformationBarrierPolicy` cmdlet.

    In the list of results, identify the policy that you want to change (or remove). Note the policy's GUID and name.

2. To set the policy's status to inactive, use the `Set-InformationBarrierPolicy` cmdlet with an Identity parameter and the State parameter set to Inactive, as shown in the following example:

    `Set-InformationBarrierPolicy -Identity 43c37853-ea10-4b90-a23d-ab8c9377247 -State Inactive`

    In this example, we are setting an information barrier policy that has GUID *43c37853-ea10-4b90-a23d-ab8c9377247* to an inactive status.

3. Use the `Start-InformationBarrierPoliciesApplication` cmdlet.

    Changes are applied, user by user, for your organization. If your organization is large, it can take 24 hours (or more) for this process to complete.

At this point, one or more information barrier policies are set to inactive status. From here, you can:
- Leave it as is (a policy set to inactive status has no effect on users); 
- [Edit a policy](#edit-a-policy); or 
- [Remove a policy](#remove-a-policy).

### Edit a policy

1. To view a list of current information barrier policies, use the `Get-InformationBarrierPolicy` cmdlet.

    In the list of results, identify the policy that you want to change. Note the policy's GUID and name. Make sure the policy is set to inactive status.

2. Use the `Set-InformationBarrierPolicy` cmdlet using an Identity parameter, and specify any changes you want to make.

    For example, suppose we want to change a policy such that instead of preventing a segment from communicating with two other segments, the segment can communicate with only one other specific segment.
    
    Originally, the policy we want to change was defined by using this cmdlet: `New-InformationBarrierPolicy -Name "Seg5CannotTalkToSeg6or7" -AssignedSegment "Seg5" -SegmentsBlocked "Seg6, Seg7"`

    The policy named *Seg5CannotTalkToSeg6or7* (which as GUID *43c37853-ea10-4b90-a23d-ab8c93772471*) was designed to prevents people in Seg5 from communicating with people in Seg6 and Seg7. 
    
    Suppose we want to change this so that people in Seg5 can only communicate with people in Seg8, and that we want to rename the policy to *Seg5CanOnlyTalkToSeg8*. To make these changes, we might use a cmdlet like this: `Set-InformationBarrierPolicy -Identity 43c37853-ea10-4b90-a23d-ab8c93772471 -Name "Seg5CanOnlyTalkToSeg8" -SegmentsAllowed "Seg8"`

    In this case, we have changed the policy's name and its effect on people in Seg5.

3. Repeat steps 1-2 for each policy you want to edit.

4. When you are finished editing your policies, proceed to [Part 3: Apply information barrier policies](#part-3-apply-information-barrier-policies).

### Remove a policy

1. Make sure to [set the policy to inactive status](#set-a-policy-to-inactive-status).

2. To view a list of current information barrier policies, use the `Get-InformationBarrierPolicy` cmdlet.

    In the list of results, identify the policy that you want to remove. Note the policy's GUID and name. Make sure the policy is set to inactive status.

3. Use the `Remove-InformationBarrierPolicy` cmdlet with an Identity parameter.

    For example, suppose we want to remove a policy that has GUID *43c37853-ea10-4b90-a23d-ab8c93772471*. To do this, we use this cmdlet:
    
    `Remove-InformationBarrierPolicy -Identity 43c37853-ea10-4b90-a23d-ab8c93772471`

    You will be prompted to confirm the change.

4. Repeat steps 1-3 for each policy you want to remove.

5. When you are finished removing policies, use the `Start-InformationBarrierPoliciesApplication` cmdlet.

    Changes are applied, user by user, for your organization. If your organization is large, it can take 24 hours for this process to complete.

## Example: Contoso's departments, segments, and policies

Contoso has five departments: HR, Sales, Marketing, Research, and Manufacturing. In order to remain compliant with industry regulations, people in some departments are not supposed to communicate with other departments, as listed in the following table:

|Segment  |Can talk to  |Cannot talk to  |
|---------|---------|---------|
|HR     |Everyone         |(no restrictions)         |
|Sales     |HR, Marketing, Manufacturing         |Research         |
|Marketing     |HR, Sales, Manufacturing         |Research         |
|Research     |HR (only)        |Sales, Marketing, Manufacturing     |
|Manufacturing |Everyone |(no restrictions) |

With this in mind, Contoso's plan includes two information barrier policies:

1. A policy designed to prevent Sales and Marketing from communicating with Research
2. A policy designed to allow Research to communicate with HR only 

The Manufacturing and HR departments don't have any other restrictions, so Contoso does not need additional information barrier policies at this time. 

The list of segments includes the Department attribute in Azure Active Directory:
- HR
- Sales
- Marketing
- Research
- Manufacturing

Although no information barrier policies are defined to limit HR or Manufacturing from communicating, those segments are defined anyway. Using the *Department* attribute in Azure Active Directory, Contoso's segments are defined as follows:

`New-OrganizationSegment -Name "HR" -UserGroupFilter "Department -eq 'HR'"`

`New-OrganizationSegment -Name "Sales" -UserGroupFilter "Department -eq 'Sales'"`

`New-OrganizationSegment -Name "Marketing" -UserGroupFilter "Department -eq 'Marketing'"`

`New-OrganizationSegment -Name "Research" -UserGroupFilter "Department -eq 'Research'"`

`New-OrganizationSegment -Name "Manufacturing" -UserGroupFilter "Department -eq 'Manufacturing'"`

With the segments defined, Contoso proceeds to define two policies. For the first policy, designed to prevent Sales and Marketing from communicating with Research, Contoso uses the following cmdlet:

`New-InformationBarrierPolicy -Name "SalesMarketingBlockedFromResearch" -AssignedSegment "Sales, Marketing" -SegmentsBlocked "Research" -State Inactive`

In this example, the information barrier policy is called *SalesMarketingBlockedFromResearch*. When this policy is active and applied, it will help prevent users who are in the Sales and Marketing segments from communicating with users in the Research segment.

For Contoso's second policy, to allow Research to communicate with HR only, Contoso uses the following cmdlet:
 
`New-InformationBarrierPolicy -Name "Research-Engineering" -AssignedSegment "Research" -SegmentsAllowed "HR" -State Inactive`    

In this case, Research can communicate only with HR, but HR is not restricted from communicating with other segments.

## Related articles

[Get an overview of information barriers](information-barriers.md)

[Learn more about information barriers in Microsoft Teams](https://docs.microsoft.com/MicrosoftTeams/information-barriers-in-teams)

[Attributes for information barrier policies (Preview)](information-barriers-attributes.md)

[Troubleshooting information barriers (Preview)](information-barriers-troubleshooting.md)
