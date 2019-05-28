---
title: "Troubleshooting information barriers"
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
description: "Use this article as a guide for troubleshooting information barriers."
---

# Troubleshooting information barriers (Preview)

If you're a global administrator or compliance administrator and you define or manage your organization's information barrier policies, you can use this guide to get answers to questions or resolve issues that may arise with information barriers. 

## Issue: People are blocked from communicating in Microsoft Teams 

- A user is unable to find or communicate with another user in Microsoft Teams.
- A user cannot see (or select) another user in Microsoft Teams.
- A user can see, but cannot send messages to, another user in Microsoft Teams.

### What to do

Follow these steps to determine whether the users are affected by an information barrier policy, whether the users are in the correct segments, and whether filters are applied correctly in information barriers.

1. As a global administrator or compliance administrator, [connect to Office 365 Security & Compliance Center PowerShell](https://docs.microsoft.com/powershell/exchange/office-365-scc/connect-to-scc-powershell/connect-to-scc-powershell?view=exchange-ps).

2. Check to see if the users who are having trouble communicating in Microsoft Teams are included in an information barrier policy. To do this, run the `Get-InformationBarrierRecipientStatus` cmdlet with the Identity parameter. You can use any identity value that uniquely identifies each recipient, such as Name, Alias, Distinguished name (DN), Canonical DN, Email address, or GUID.

    Example: `Get-InformationBarrierRecipientStatus -User1 meganb -User2 alexw`

    In this example, we are using each user's alias. When we run this cmdlet, if either user is affected by an information barrier policy, we will see its GUID listed as "ExoPolicyId."

    If the users are not included in information barrier policies, contact support. Otherwise, proceed to the next step.

3. Check to see which segments are affected by an information barrier policy. To do this, run the `Get-InformationBarrierPolicy` cmdlet with the Identity parameter. Use details, such as the policy GUID (ExoPolicyId) you received during the previous step, as an identity value.

    Example: `Get-InformationBarrierPolicy -Identity b42c3d0f-49e9-4506-a0a5-bf2853b5df6f`

    In this example, we are getting detailed information about the information barrier policy that has "ExoPolicyId: b42c3d0f-49e9-4506-a0a5-bf2853b5df6f."
    
    After you run the cmdlet, in the results, look for **AssignedSegment**, **SegmentsAllowed**, **SegmentsBlocked**, and **SegmentAllowedFilter** values.

    Example: After running the cmdlet, we saw the following in our list of results:

    ```powershell
        AssignedSegment      : Sales
        SegmentsAllowed      : {}
        SegmentsBlocked      : {Research}
        SegmentAllowedFilter :
    ```
    In this case, we can see that the policy affects people who are in the Sales and Research segments, and that people in Sales are prevented from communicating with Research. If this seems correct, then information barriers are working as expected. If something is not correct, proceed to the next step.

4. Make sure your segments are defined correctly. To do this, run the `Get-OrganizationSegment` cmdlet, and review the list of results. 

    To view details for a specific segment, use the `Get-OrganizationSegment` cmdlet with an Identity parameter. 

    Example: `Get-OrganizationSegment -Identity "FFO.extest.microsoft.com/Microsoft Exchange Hosted Organizations/IBAPCorp04.onmicrosoft.com/Configuration/Sales"`

    Review the details for the segment. If necessary, [edit a segment](information-barriers-policies.md#view-or-edit-existing-segments), wait 30 minutes, and then re-run the `Start-InformationBarrierPoliciesApplication` cmdlet.

    If you are still having issues with your information barrier policy, contact support.
    

## Issue: The information barrier application process is taking too long

After running the `Start-InformationBarrierPoliciesApplication` cmdlet, the process is taking a really long time to finish.

### What to do

1. Keep in mind that when you run the policy application cmdlet, information barrier policies are being applied (or removed), user by user, for all accounts in your organization. If you have a lot of users, it will take a while to process. 

2. If you have waited a long time and the process still isn't finished, you can update a field in the users' profiles in Azure Active Directory, and wait 30 minutes for FwdSync to occur. For more details about how this works, see [New address lists that you create in Exchange Online don't contain all the expected recipients](https://support.microsoft.com/help/2955640/new-address-lists-that-you-create-in-exchange-online-don-t-contain-all).

3. If after step 2 you are still having issues with the process finishing, contact support.

## Related topics

[Define policies for information barriers in Microsoft Teams (Preview)](information-barriers-policies.md)

[Information barriers (Preview)](information-barriers.md)



