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

1. As a global administrator or compliance administrator, [connect to Office 365 Security & Compliance Center PowerShell](https://docs.microsoft.com/powershell/exchange/office-365-scc/connect-to-scc-powershell/connect-to-scc-powershell?view=exchange-ps).

2. To see if the users in question are included in an information barrier policy, run the `Get-InformationBarrierRecipientStatus` cmdlet with the Identity parameter. You can use any identity value that uniquely identifies each recipient, such as Name, Alias, Distinguished name (DN), Canonical DN, Email address, or GUID.

    Example: `Get-InformationBarrierRecipientStatus -User1 meganb -User2 alexw`

    In this example, we are using each user's alias. When we run this cmdlet, if each user is included in an information barrier policy, we will see its GUID listed as ExoPolicyId.

3. 

## My information barrier policy is not working

content coming

## Starting the information barrier application is taking too long

content coming

## I'm getting error messages while defining policies

content coming

## Related topics

[Define policies for information barriers in Microsoft Teams (Preview)](information-barriers-policies.md)

[Information barriers (Preview)](information-barriers.md)



