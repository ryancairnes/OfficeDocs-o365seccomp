---
title: "Define information barrier policies"
ms.author: deniseb
author: denisebmsft
manager: laurawi
ms.date: 05/30/2019
ms.audience: ITPro
ms.topic: article
ms.service: O365-seccomp
ms.collection:
- M365-security-compliance
localization_priority: None
description: "Learn how to define policies for information barriers in Microsoft Teams."
---

# Define policies for information barriers (Preview)

With information barriers, you can define policies that are designed to prevent certain segments of users from communicating with each other, or allow specific segments to communicate only with certain other segments. Information barrier policies can help your organization maintain compliance with relevant industry standards and regulations, and avoid potential conflicts of interest. To learn more, see [Information barriers (Preview)](information-barriers.md). 

> [!IMPORTANT]
> This article describes how to plan, define, implement, and manage information barrier policies. Several steps are involved, and the work flow is divided into several parts. Make sure to read through the [prerequisites](#prerequisites) and the entire process before you begin defining (or editing) information barrier policies.

## The work flow at a glance

|Phase    |What's involved  |
|---------|---------|
|[Make sure prerequisites are met](#prerequisites)     |- Verify that you have the necessary permissions to define/edit policies<br/>- Make sure that your directory data reflects your organization's structure<br/>- Make sure that scoped directory search is enabled in Microsoft Teams<br/>- Use PowerShell (example cmdlets are provided)<br/>- Provide admin consent (steps are included)          |
|[Part 1: Segment all the users in your organization](#part-1-segment-users)     |- Determine what policies are needed<br/>- Make a list of segments to define<br/>- Identify which attributes to use<br/>- Define segments in terms of policy filters        |
|[Part 2: Define information barrier policies](#part-2-define-information-barrier-policies)     |- Define the policies (do not apply yet)       |
|[Part 3: Apply information barrier policies](#part-3-apply-information-barrier-policies)     |- Set policies to active status<br/>- Run the policy application<br/>- Verify policy status         |
|(As needed) [Edit a segment or a policy](#edit-a-segment-or-a-policy)     |- Edit a segment<br/>- Edit or remove a policy<br/>- Run the policy application<br/>- Verify policy status         |
|(As needed) [Troubleshooting](information-barriers-troubleshooting.md)|- Take action when policies are not working as expected|

## Prerequisites

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

Before you define or edit segments or information barrier policies, follow these steps:

1. As a global administrator or compliance administrator, [connect to Office 365 Security & Compliance Center PowerShell](https://docs.microsoft.com/powershell/exchange/office-365-scc/connect-to-scc-powershell/connect-to-scc-powershell?view=exchange-ps).

2. Run the following PowerShell cmdlets:

    ```
    Login-AzureRmAccount 
    $appId="bcf62038-e005-436d-b970-2a472f8c1982" 
    $sp=Get-AzureRmADServicePrincipal -ServicePrincipalName $appId
    if ($sp -eq $null) { New-AzureRmADServicePrincipal -ApplicationId $appId }
    Start-Process  "https://login.microsoftonline.com/common/adminconsent?client_id=$appId"
    ```

3. When prompted, sign in using your work or school account for Office 365.

4. In the **Permissions requested** dialog box, review the information, and then choose **Accept**.

## Part 1: Segment users

During this phase, you determine what policies are needed, make a list of segments to define, and then define your segments.

### Determine what policies are needed

Make a list of information barrier policies needed for your organization. You can use information barrier policies to:
- Block communications between certain segments; or 
- Allow communications between certain segments.

(See [Example: Contoso's departments, segments, and policies](#example-contosos-departments-segments-and-policies) in this article.)

### Make a list of segments

In addition to your list of needed policies, make a list of segments for your organization. Every user in your organization should belong to a segment, and no user should belong to two or more segments. Each segment can have only one information barrier policy applied. 

Determine which attributes in your organization's directory data you'll use to define segments. You can use *Department*, *MemberOf*, or any of the supported attributes. Make sure that you have values in the attribute you select for all users. To see a list of supported attributes, refer to [Attributes for information barrier policies (Preview)](information-barriers-attributes.md).

> [!IMPORTANT]
> **Before you proceed to the next section, make sure your directory data has values for attributes that you can use to define segments**. If your directory data does not have values for the attributes you want to use, then all user accounts must be updated to include that information before you proceed with information barriers. To get help with this, see the following resources:<br/>- [Configure user account properties with Office 365 PowerShell](https://docs.microsoft.com/office365/enterprise/powershell/configure-user-account-properties-with-office-365-powershell)<br/>- [Add or update a user's profile information using Azure Active Directory](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-users-profile-azure-portal)

### Define segments using PowerShell

1. To define an organizational segment, use the **New-OrganizationSegment** cmdlet with the **UserGroupFilter** parameter that corresponds to the attribute you want to use. 

    The syntax is `New-OrganizationSegment -Name "segmentname" -UserGroupFilter "attribute -eq 'attributevalue'"`

    Example: `New-OrganizationSegment -Name "HR" -UserGroupFilter "Department -eq 'HR'"`

    In this example, a segment called *HR* is defined using *HR*, a value in the Department attribute.

2. Repeat step 1 for each segment you want to define.

    After you run each cmdlet, you should see a list of details about the new segment. Details include the segment's type, who created or last modified it, and so on. 

> [!IMPORTANT]
> **Make sure that your segments do not overlap**. Each user in your organization should belong to one (and only one) segment. No user should belong to two or more segments. Segments should be defined for all users in your organization. 

(See [Example: Contoso's departments, segments, and policies](#example-contosos-departments-segments-and-policies).)


## Part 2: Define information barrier policies

> [!IMPORTANT]
> As you define information barrier policies, make sure to set those policies to inactive status until you are ready to apply them. Defining (or editing) policies does not affect users until those policies are set to active status and then applied.

When you have a list of user segments and the information barrier policies you want to define, select a scenario, and then follow the steps.

- [Scenario 1: Block communications between segments](#scenario-1-block-communications-between-segments)
- [Scenario 2: Allow a segment to communicate only with one other segment](#scenario-2-allow-a-segment-to-communicate-only-with-one-other-segment)

(See [Example: Contoso's departments, segments, and policies](#example-contosos-departments-segments-and-policies).)


### Scenario 1: Block communications between segments

1. To block communications between segments, use the `New-InformationBarrierPolicy` cmdlet with the **SegmentsBlocked** parameter. 

    Example: `New-InformationBarrierPolicy -Name "SalesBlockedFromResearch" -AssignedSegment "Sales" -SegmentsBlocked "Research" -State Inactive`

    In this case, we are defining a policy called *SalesBlockedFromResearch*. This policy can be applied to users in a segment called *Sales*. When active and applied, this policy will help prevent people in *Sales* from communicating with people in a segment called *Research*.

    Repeat this step for each policy you want to define to block communications.
 
2. Do one of the following:

   - (If needed) [Define a policy to allow a segment to communicate only with one other segment](#scenario-2-allow-a-segment-to-communicate-only-with-one-other-segment) 
   - (After all your policies are defined) [Apply information barrier policies](#part-3-apply-information-barrier-policies)

### Scenario 2: Allow a segment to communicate only with one other segment

1. To allow one segment to communicate with only one other segment, use the `New-InformationBarrierPolicy` cmdlet with the **SegmentsAllowed** parameter. 

    Example: `New-InformationBarrierPolicy -Name "ResearchTalksToHR" -AssignedSegment "Research" -SegmentsAllowed "HR" -State Inactive`

    In this case, we are defining a policy called *ResearchTalksToHR*. This policy can be applied to users in a segment called *Research*. When active and applied, this policy will allow people in *Research* to communicate only with people in a segment called *HR*. (In this case, Research cannot communicate with users who are not part of HR.)

    Repeat this step for each policy you want to define to restrict communications.

2. Do one of the following:

   - (If needed) [Define a policy to block communications between segments](#scenario-1-block-communications-between-segments) 
   - (After all your policies are defined) [Apply information barrier policies](#part-3-apply-information-barrier-policies)

## Part 3: Apply information barrier policies

Information barrier policies are not in effect until you set them to active status, and then apply the policies.

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
    
3. To verify status for a specific user, use the **Get-InformationBarrierRecipientStatus** cmdlet with Identity parameters. 

    The syntax is `Get-InformationBarrierRecipientStatus -Identity <value> -Identity2 <value>`

    You can use any value that uniquely identifies each user, such as name, alias, distinguished name, canonical domain name, email address, or GUID.

    Example: 
    
    `Get-InformationBarrierRecipientStatus -Identity meganb -Identity2 alexw`
    
    In this example, we are referring to user accounts in Office 365: meganb for Megan, and alexw for Alex.
    
    (You can also use this cmdlet for a single user: `Get-InformationBarrierRecipientStatus -Identity <value>`)
    
    This returns information about the users, such as whether any policies are defined that affect the users.

## Edit a segment or a policy

### Edit a segment

1. To view all existing segments, use the **Get-OrganizationSegment** cmdlet.
    
    The syntax is `Get-OrganizationSegment`

    You will see a list of segments and details for each, such as segment type, its UserGroupFilter value, who created or last modified it, GUID, and so on.

    > [!TIP]
    > Print or save your list of segments for reference later. For example, if you want to edit a segment, you will need to know its name or identify value (this is used with the Identity parameter).

2. To edit a segment, use the `Set-OrganizationSegment` cmdlet with the Identity parameter and relevant details. Here's an example:

    `Set-OrganizationSegment -Identity c96e0837-c232-4a8a-841e-ef45787d8fcd -UserGroupFilter "Department -eq 'HRDept'"`

    In this example, for the segment that has the GUID *c96e0837-c232-4a8a-841e-ef45787d8fcd*, we are updating the department name to "HRDept".

When you have finished editing segments for your organization, you can [define](#part-2-define-information-barrier-policies) or [edit](#edit-a-policy) information barrier policies.

### Edit a policy

1. To view a list of current information barrier policies, use the `Get-InformationBarrierPolicy` cmdlet.

    In the list of results, identify the policy that you want to change. Note the policy's GUID and name. Make sure the policy is set to inactive status.

2. Use the `Set-InformationBarrierPolicy` cmdlet using an Identity parameter, and specify any changes you want to make.

    For example, suppose a policy was defined by using this cmdlet: `New-InformationBarrierPolicy -Name "ResearchBlockedFromSalesMarketing" -AssignedSegment "Research" -SegmentsBlocked "Sales, Marketing"`
    
    Suppose we want to change it so that people in Research can only communicate with people in HR. To make this change, we might use a cmdlet like this: `Set-InformationBarrierPolicy -Identity 43c37853-ea10-4b90-a23d-ab8c93772471 -SegmentsAllowed "HR"`

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

5. When you are finished removing policies, apply your changes. To do this, use the `Start-InformationBarrierPoliciesApplication` cmdlet.

    Changes are applied, user by user, for your organization. If your organization is large, it can take 24 hours (or more) for this process to complete.

### Set a policy to inactive status

1. To view a list of current information barrier policies, use the `Get-InformationBarrierPolicy` cmdlet.

    In the list of results, identify the policy that you want to change (or remove). Note the policy's GUID and name.

2. To set the policy's status to inactive, use the `Set-InformationBarrierPolicy` cmdlet with an Identity parameter and the State parameter set to Inactive, as shown in the following example:

    `Set-InformationBarrierPolicy -Identity 43c37853-ea10-4b90-a23d-ab8c9377247 -State Inactive`

    In this example, we are setting an information barrier policy that has GUID *43c37853-ea10-4b90-a23d-ab8c9377247* to an inactive status.

3. Use the `Start-InformationBarrierPoliciesApplication` cmdlet.

    Changes are applied, user by user, for your organization. If your organization is large, it can take 24 hours (or more) for this process to complete.

At this point, one or more information barrier policies are set to inactive status. From here, you can do any of the following:
- Leave it as is (a policy set to inactive status has no effect on users)
- [Edit a policy](#edit-a-policy) 
- [Remove a policy](#remove-a-policy)

## Example: Contoso's departments, segments, and policies

To see how an organization might approach defining segments and policies, consider the following example.

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

Contoso will use the Department attribute in Azure Active Directory to define segments, as follows:

|Department  |Segment Definition  |
|---------|---------|
|HR     | `New-OrganizationSegment -Name "HR" -UserGroupFilter "Department -eq 'HR'"`        |
|Sales     | `New-OrganizationSegment -Name "Sales" -UserGroupFilter "Department -eq 'Sales'"`        |
|Marketing     | `New-OrganizationSegment -Name "Marketing" -UserGroupFilter "Department -eq 'Marketing'"`        |
|Research     | `New-OrganizationSegment -Name "Research" -UserGroupFilter "Department -eq 'Research'"`        |
|Manufacturing     | `New-OrganizationSegment -Name "Manufacturing" -UserGroupFilter "Department -eq 'Manufacturing'"`        |

With the segments defined, Contoso proceeds to define two policies. 


|Policy  |Policy Definition  |
|---------|---------|
|Policy 1: Prevent Sales and Marketing from communicating with Research     | `New-InformationBarrierPolicy -Name "SalesMarketingBlockedFromResearch" -AssignedSegment "Sales, Marketing" -SegmentsBlocked "Research" -State Inactive` <p> In this example, the information barrier policy is called *SalesMarketingBlockedFromResearch*. When this policy is active and applied, it will help prevent users who are in the Sales and Marketing segments from communicating with users in the Research segment.       |
|Policy 2: Allow Research to communicate with HR only     | `New-InformationBarrierPolicy -Name "ResearchTalksToHR" -AssignedSegment "Research" -SegmentsAllowed "HR" -State Inactive` <p>In this case, the information barrier policy is called *ResearchTalksToHR*. When this policy is active and applied, Research can communicate only with HR, but HR is not restricted from communicating with other segments. |

With segments and policies defined, Contoso applies the policies. When that finishes, Contoso is compliant with legal and industry requirements.

## Related articles

[Get an overview of information barriers](information-barriers.md)

[Learn more about information barriers in Microsoft Teams](https://docs.microsoft.com/MicrosoftTeams/information-barriers-in-teams)

[Attributes for information barrier policies (Preview)](information-barriers-attributes.md)

[Troubleshooting information barriers (Preview)](information-barriers-troubleshooting.md)
