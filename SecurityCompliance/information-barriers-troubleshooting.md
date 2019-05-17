---
title: "Troubleshooting information barriers"
ms.author: deniseb
author: denisebmsft
manager: laurawi
ms.date: 05/17/2019
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

## People are blocked from communicating in Microsoft Teams

### Issues 

- A user is unable to find or communicate with another user in Microsoft Teams.
- A user cannot see (or select) another user in Microsoft Teams.
- A user can see, but cannot send messages to, another user in Microsoft Teams.

### What to do

Follow these steps to determine whether the users are affected by an information barrier policy, whether the users are in the correct segments, and whether filters are applied correctly in information barriers.

1. As a global administrator or compliance administrator, [connect to Office 365 Security & Compliance Center PowerShell](https://docs.microsoft.com/powershell/exchange/office-365-scc/connect-to-scc-powershell/connect-to-scc-powershell?view=exchange-ps).

2. To see if the users in question are included in an information barrier policy, run the `Get-InformationBarrierRecipientStatus` cmdlet with the Identity parameter. You can use any identity value that uniquely identifies each recipient, such as Name, Alias, Distinguished name (DN), Canonical DN, Email address, or GUID.

    Example: `Get-InformationBarrierRecipientStatus -User1 meganb -User2 alexw`

    In this example, we are using each user's alias. When we run this cmdlet, if each user is included in an information barrier policy, we will see its GUID listed as ExoPolicyId.

    If the users are not included in information barrier policies, contact support. Otherwise, proceed to the next step.

3. To see which segments are affected by an information barrier policy, run the `Get-InformationBarrierPolicy` cmdlet with the Identity parameter. Use the policy GUID (ExoPolicyId) from the previous step.

    Example: `Get-InformationBarrierPolicy -Identity b42c3d0f-49e9-4506-a0a5-bf2853b5df6f`

    In the results, look for AssignedSegment, SegmentsAllowed, SegmentsBlocked, and SegmentAllowedFilter values.

    Example: After running the cmdlet, we saw the following in our list of results:

    ```powershell
        AssignedSegment      : Sales
        SegmentsAllowed      : {}
        SegmentsBlocked      : {Research}
        SegmentAllowedFilter :
    ```
    In this case, we have an information barrier policy such that users in the Sales segment are prevented from communicating with users in the Research segment.


## The information barrier application process is taking too long

### Issue

After running the `Start-InformationBarrierPoliciesApplication` cmdlet, the process is taking a really long time to finish.

### What to do

1. Keep in mind that when you run the policy application cmdlet, information barrier policies are being applied (or removed), user by user, for all accounts in your organization. If you have a lot of users, it will take a while to process. 

2. If you have waited a long time and the process still isn't finished, you can update a field in the users' profiles in Azure Active Directory, and wait 30 minutes for FwdSync to occur. For more details about how this works, see [New address lists that you create in Exchange Online don't contain all the expected recipients](https://support.microsoft.com/help/2955640/new-address-lists-that-you-create-in-exchange-online-don-t-contain-all).

3. If after step 2 you are still having issues with the process, contact support.

## Related topics

[Define policies for information barriers in Microsoft Teams (Preview)](information-barriers-policies.md)

[Information barriers (Preview)](information-barriers.md)



