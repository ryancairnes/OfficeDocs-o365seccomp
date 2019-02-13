---
title: "View, edit, or remove information barriers policies"
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

# View, edit, or remove information barriers in Microsoft Teams

Coming soon to Microsoft Teams, information barriers policies can help limit communications between specific groups of people. Information barriers can help your organization comply with industry standards and regulations, and avoid potential conflicts of interest. To learn more, see [Information barriers (coming soon to Microsoft Teams!)](information-barriers.md). After [information barriers policies are defined](define-information-barriers-policies.md) for your organization, you can view, edit, or even remove those policies as appropriate.

To edit or remove information barriers policies, you must be assigned one of the following roles:

- Microsoft 365 Enterprise Global Administrator

- Office 365 Global Administrator

- Compliance Administrator

> [!IMPORTANT]
> Potentially, everyone included in an information barriers policy can be blocked from communicating with others in Microsoft Teams. When people affected by information barriers policies are part of the same team or group chat, they will be removed from those chat sessions. However, information barriers will not apply to email communications or to file sharing through SharePoint Online or OneDrive. 

Currently, information barriers policies are defined and managed in Office 365 by using PowerShell cmdlets. This is typically done by a compliance administrator or a global administrator, and requires familiarity with PowerShell cmdlets (and parameters). Although several scenarios and examples of PowerShell cmdlets are provided, you'll need to know additional details, such as parameters, for your organization.



## Prepare your environment for information barriers

**Before you begin, make sure that your organization already has one or more information barriers policies defined**. See [Define policies for information barriers in Microsoft Teams](define-information-barriers-policies.md).

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

After you have completed these steps, select one of the following procedures:

## View information barriers policies

1. 

2. 

3. 

## Edit information barriers policies

1. 

2. 

3. 

## Remove information barriers policies

1. 

2. 

3. 

## Related articles

[Get an overview of information barriers](information-barriers.md)

[Define policies for information barriers in Microsoft Teams](define-information-barriers-policies.md)

[Learn more about the user experience of information barriers in Microsoft Teams](https://docs.microsoft.com/SkypeForBusiness/MicrosoftTeams/information-barriers-in-teams)
