---
title: "Edit or remove information barrier policies"
ms.author: deniseb
author: denisebmsft
manager: laurawi
ms.date: 06/24/2019
audience: ITPro
ms.topic: article
ms.service: O365-seccomp
ms.collection:
- M365-security-compliance
localization_priority: None
description: "Learn how to edit or remove policies for information barriers."
---

# Edit or remove information barrier policies (Preview)

## Overview

## Stop a policy application

If, after you have started applying information barrier policies, you want to stop those policies from being applied, use the following procedure. Keep in mind that it will take approximately 30-35 minutes for the process to begin.

1. To view the status of the most recent information barrier policy application, use the **Get-InformationBarrierPoliciesApplicationStatus** cmdlet.

    Syntax: `Get-InformationBarrierPoliciesApplicationStatus`

    Note the application's GUID.

2. Use the **Stop-InformationBarrierPoliciesApplication** cmdlet with an Identity parameter.

    Syntax:  `Stop-InformationBarrierPoliciesApplication -Identity GUID`

    Example: `Stop-InformationBarrierPoliciesApplication -Identity 46237888-12ca-42e3-a541-3fcb7b5231d1`

    In this example, we are stopping information barrier policies from being applied.

## Edit a segment or a policy

### Edit a segment

1. To view all existing segments, use the **Get-OrganizationSegment** cmdlet.
    
    Syntax: `Get-OrganizationSegment`

    You will see a list of segments and details for each, such as segment type, its UserGroupFilter value, who created or last modified it, GUID, and so on.

    > [!TIP]
    > Print or save your list of segments for reference later. For example, if you want to edit a segment, you will need to know its name or identify value (this is used with the Identity parameter).

2. To edit a segment, use the **Set-OrganizationSegment** cmdlet with the **Identity** parameter and relevant details. 

    Syntax: `Set-OrganizationSegment -Identity GUID -UserGroupFilter "attribute -eq 'attributevalue'"`

    Example: `Set-OrganizationSegment -Identity c96e0837-c232-4a8a-841e-ef45787d8fcd -UserGroupFilter "Department -eq 'HRDept'"`

    In this example, for the segment that has the GUID *c96e0837-c232-4a8a-841e-ef45787d8fcd*, we updated the department name to "HRDept".

When you have finished editing segments for your organization, you can proceed to [define](#part-2-define-information-barrier-policies) or [edit](#edit-a-policy) information barrier policies.

### Edit a policy

1. To view a list of current information barrier policies, use the **Get-InformationBarrierPolicy** cmdlet.

    Syntax: `Get-InformationBarrierPolicy`

    In the list of results, identify the policy that you want to change. Note the policy's GUID and name.

2. Use the **Set-InformationBarrierPolicy** cmdlet with an **Identity** parameter, and specify the changes you want to make.

    Example: Suppose a policy was defined to block the *Research* segment from communicating with the *Sales* and *Marketing* segments. The policy was defined by using this cmdlet: `New-InformationBarrierPolicy -Name "Research-SalesMarketing" -AssignedSegment "Research" -SegmentsBlocked "Sales","Marketing"`
    
    Suppose we want to change it so that people in the *Research* segment can only communicate with people in the *HR* segment. To make this change, we use this cmdlet: `Set-InformationBarrierPolicy -Identity 43c37853-ea10-4b90-a23d-ab8c93772471 -SegmentsAllowed "HR"`

    In this example, we changed "SegmentsBlocked" to "SegmentsAllowed" and specified the *HR* segment.

3. When you are finished editing a policy, make sure to apply your changes. (See [Apply information barrier policies](#part-3-apply-information-barrier-policies).)

### Remove a policy

1. To view a list of current information barrier policies, use the **Get-InformationBarrierPolicy** cmdlet.

    Syntax: `Get-InformationBarrierPolicy`

    In the list of results, identify the policy that you want to remove. Note the policy's GUID and name. Make sure the policy is set to inactive status.

2. Use the **Remove-InformationBarrierPolicy** cmdlet with an Identity parameter.

    Syntax: `Remove-InformationBarrierPolicy -Identity GUID`

    Example: Suppose we want to remove a policy that has GUID *43c37853-ea10-4b90-a23d-ab8c93772471*. To do this, we use this cmdlet:
    
    `Remove-InformationBarrierPolicy -Identity 43c37853-ea10-4b90-a23d-ab8c93772471`

    When prompted, confirm the change.

3. Repeat steps 1-2 for each policy you want to remove.

4. When you are finished removing policies, apply your changes. To do this, use the **Start-InformationBarrierPoliciesApplication** cmdlet.

    Syntax: `Start-InformationBarrierPoliciesApplication`

    Changes are applied, user by user, for your organization. If your organization is large, it can take 24 hours (or more) for this process to complete.

### Set a policy to inactive status

1. To view a list of current information barrier policies, use the **Get-InformationBarrierPolicy** cmdlet.

    Syntax: `Get-InformationBarrierPolicy`

    In the list of results, identify the policy that you want to change (or remove). Note the policy's GUID and name.

2. To set the policy's status to inactive, use the **Set-InformationBarrierPolicy** cmdlet with an Identity parameter and the State parameter set to Inactive.

    Syntax: `Set-InformationBarrierPolicy -Identity GUID -State Inactive`

    `Set-InformationBarrierPolicy -Identity 43c37853-ea10-4b90-a23d-ab8c9377247 -State Inactive`

    In this example, we set an information barrier policy that has GUID *43c37853-ea10-4b90-a23d-ab8c9377247* to an inactive status.

3. To apply your changes, use the **Start-InformationBarrierPoliciesApplication** cmdlet.

    Syntax: `Start-InformationBarrierPoliciesApplication`

    Changes are applied, user by user, for your organization. If your organization is large, it can take 24 hours (or more) for this process to complete. (As a general guideline, it takes about an hour to process 5,000 user accounts.)

At this point, one or more information barrier policies are set to inactive status. From here, you can do any of the following:
- Keep it as is (a policy set to inactive status has no effect on users)
- [Edit a policy](#edit-a-policy) 
- [Remove a policy](#remove-a-policy)


## Related articles

[Get an overview of information barriers](information-barriers.md)

[Learn more about information barriers in Microsoft Teams](https://docs.microsoft.com/MicrosoftTeams/information-barriers-in-teams)

[Attributes for information barrier policies (Preview)](information-barriers-attributes.md)

[Troubleshooting information barriers (Preview)](information-barriers-troubleshooting.md)
