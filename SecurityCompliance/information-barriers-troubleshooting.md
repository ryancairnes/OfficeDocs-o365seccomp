---
title: "Troubleshooting information barriers"
ms.author: deniseb
author: denisebmsft
manager: laurawi
ms.date: 05/29/2019
ms.audience: ITPro
ms.topic: article
ms.service: O365-seccomp
ms.collection:
- M365-security-compliance
localization_priority: None
description: "Use this article as a guide for troubleshooting information barriers."
---

# Troubleshooting information barriers (Preview)

Information barriers can help your organization remain compliant with legal requirements and industry regulations. For example, with information barriers, you can restrict communication between specific groups of users to avoid a conflict of interest or other issues. To learn more, see [Information barriers (Preview)](information-barriers.md).

This article provides guidance you can use to get answers to questions or resolve issues that may arise with information barriers.  

## Before you begin...

To perform the tasks described in this article, you must be assigned an appropriate role, such as one of the following:
- Microsoft 365 Enterprise Global Administrator
- Office 365 Global Administrator
- Compliance Administrator
- Information barriers administrator (this is a new role!)

To learn more about prerequisites for information barriers, see [Prerequisites (for information barrier policies)](information-barriers-policies.md#prerequisites).

Also, make sure to [connect to the Security & Compliance Center and provide admin consent](information-barriers-policies.md#connect-to-the-security--compliance-center-and-provide-admin-consent).

## Issue: People are unexpectedly blocked from communicating in Microsoft Teams 

- A user is unable to find or communicate with another user in Microsoft Teams.
- A user cannot see or select another user in Microsoft Teams.
- A user can see, but cannot send messages to, another user in Microsoft Teams.

### What to do

Follow these steps to determine whether the users are affected by an information barrier policy, whether the users are in the correct segments, and whether filters are applied correctly in information barriers.

1. Check to see if each user is included in an information barrier policy. To do this, use the `Get-InformationBarrierRecipientStatus` cmdlet with the Identity parameter. 

    You can use any identity value that uniquely identifies each recipient, such as Name, Alias, Distinguished name (DN), Canonical DN, Email address, or GUID.

    Example: `Get-InformationBarrierRecipientStatus -Identity meganb`

    In this example, we are using an alias (*meganb*) for the Identity parameter. This cmdlet will return information that indicates whether the user is affected by an information barrier policy. (Its GUID will be listed as *ExoPolicyId*.)

    If the users are not included in information barrier policies, contact support. Otherwise, proceed to the next step.

2. Check to see which segments are affected by an information barrier policy. To do this, use the `Get-InformationBarrierPolicy` cmdlet with the Identity parameter. Use details, such as the policy GUID (ExoPolicyId) you received during the previous step, as an identity value.

    Example: `Get-InformationBarrierPolicy -Identity b42c3d0f-49e9-4506-a0a5-bf2853b5df6f`

    In this example, we are getting detailed information about the information barrier policy that has ExoPolicyId *b42c3d0f-49e9-4506-a0a5-bf2853b5df6f*.
    
    After you run the cmdlet, in the results, look for **AssignedSegment**, **SegmentsAllowed**, and **SegmentsBlocked** values.

    Example: After running the `Get-InformationBarrierPolicy` cmdlet, we saw the following in our list of results:

    ```powershell
        AssignedSegment      : Sales
        SegmentsAllowed      : {}
        SegmentsBlocked      : {Research}
    ```
    In this case, we can see that an information barrier policy affects people who are in the Sales and Research segments. In this case, people in Sales are prevented from communicating with people in Research. If this seems correct, then information barriers are working as expected. If not, proceed to the next step.

4. Make sure your segments are defined correctly. To do this, use the `Get-OrganizationSegment` cmdlet, and review the list of results. 

    To view details for a specific segment, use the `Get-OrganizationSegment` cmdlet with an Identity parameter. 

    Example: `Get-OrganizationSegment -Identity c96e0837-c232-4a8a-841e-ef45787d8fcd`

    In this example, we are getting information about the segment that has GUID *c96e0837-c232-4a8a-841e-ef45787d8fcd*.

    Review the details for the segment. If necessary, [edit a segment](information-barriers-policies.md#view-or-edit-existing-segments), wait 30 minutes, and then re-use the `Start-InformationBarrierPoliciesApplication` cmdlet.

    If you are still having issues with your information barrier policy, contact support.
    

## Issue: The information barrier application process is taking too long

After running the `Start-InformationBarrierPoliciesApplication` cmdlet, the process is taking a really long time to finish.

### What to do

1. Keep in mind that when you run the policy application cmdlet, information barrier policies are being applied (or removed), user by user, for all accounts in your organization. If you have a lot of users, it will take a while to process. 

2. If you have waited a long time and the process still isn't finished, you can update a field in the users' profiles in Azure Active Directory, and then wait about 30 minutes for FwdSync to occur. For more details about how this works, see [New address lists that you create in Exchange Online don't contain all the expected recipients](https://support.microsoft.com/help/2955640/new-address-lists-that-you-create-in-exchange-online-don-t-contain-all).

3. If after step 2 you are still having issues with the process finishing, contact support.

## Related topics

[Define policies for information barriers in Microsoft Teams (Preview)](information-barriers-policies.md)

[Information barriers (Preview)](information-barriers.md)



