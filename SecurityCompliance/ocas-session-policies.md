---
title: "Session policies in Office 365 Cloud App Security"
ms.author: deniseb
author: denisebmsft
manager: laurawi
ms.reviewer: alesibov
ms.audience: Admin
ms.topic: reference
ms.date: 02/14/2019
ms.service: o365-administration
localization_priority: Normal
description: "Office 365 Cloud App Security session policies enable real-time session-level monitoring, affording you granular visibility into Office 365 apps and the ability to take different actions depending on the policy you set for a user session. Instead of allowing or blocking access completely, with session control you can allow access while monitoring the session and/or limit specific session activities using the reverse proxy capabilities of Conditional Access App Control."
---

# Session policies in Office 365 Cloud App Security

|****Evaluation** \>**|****Planning** \>**|****Deployment** \>**|****Utilization****|
|:-----|:-----|:-----|:-----|
|[Start evaluating](office-365-cas-overview.md) <br/> |[Start planning](get-ready-for-office-365-cas.md) <br/> |You are here!  <br/> [Next step](ocas-access-policies.md) <br/> |[Start utilizing](utilization-activities-for-ocas.md) <br/> |

Office 365 Cloud App Security session policies enable real-time session-level monitoring, affording you granular visibility into Office 365 apps and the ability to take different actions depending on the policy you set for a user session. Instead of allowing or blocking access completely, with session control you can allow access while monitoring the session and/or limit specific session activities using the reverse proxy capabilities of Conditional Access App Control.

For example, you can decide that from unmanaged devices, or for sessions coming from specific locations, you want to allow the user to access the app but also limit the download of sensitive files or require that certain documents be protected upon download. Session policies enable you to set these user-session controls and allow access and enables you to:

- [Monitor all activities](#monitor-all-activities)

- [Block all downloads](#block-all-downloads)

- [Block specific activities](#block-specific-activities)

- [Protect files on download](#protect-files-on-download)

## Prerequisites to using session policies

- Azure AD Premium P1 license

- The relevant Office 365 apps should be [deployed with Conditional Access App Control](ocas-deploy-conditional-access-app-control.md)

- An [Azure AD conditional access policy](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal) should be in place that redirects users to Office 365 Cloud App Security

## Create an Azure AD conditional access policy

Azure Active Directory conditional access policies and Cloud App Security session policies work in tandem to examine each user session and make policy decisions for each app. To set up a conditional access policy in Azure AD, follow this procedure:

1. Configure an [Azure AD conditional access policy](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal) with assignments for a user or group of users and the app you want to control with the Conditional Access App Control. NOTE: Only apps that were [deployed with Conditional Access App Control](ocas-deploy-conditional-access-app-control.md) will be affected by this policy.

2. Route users to Office 365 Cloud App Security by selecting the **Use Conditional Access App Control enforced restrictions** in the **Session** page.

## Create a Cloud App Security session policy

To create a new session policy, follow this procedure:

1. In the portal, select **Control** followed by **Policies**.

2. In the **Policies** page, click **Create policy** and select **Session policy**.

3. In the **Session policy** window, assign a name for your policy

4. In the **Session control type** field:
    
    - Select **Monitor only** if you only want to monitor activities by users. This selection will create a Monitor only policy for the apps you selected where all sign-ins, heuristic downloads, and Activity types will be downloaded.
    
    - Select **Control file download (with DLP)** if you want to monitor user activities. You can take additional actions like block or protect downloads for users.
    
    - Select **Block activities** to block specific activities, which you can select using the **Activity type** filter. All activities from selected apps will be monitored (and reported in the Activity log). The specific activities you select will be blocked if you select the **Block** action. The specific activities you selected will raise alerts if you select the **Test** action and have alerts turned on.

5. Under **Activity source** in the **Activities matching all of the following** section, select additional activity filters to apply to the policy. These filters can include the following options:
    
    - **Device tags**: Use this filter to identify unmanaged devices.
    
    - **Location**: Use this filter to identify unknown (and therefore risky) locations.
    
    - **IP address**: Use this filter to filter per IP addresses or use previously assigned IP address tags.
    
    - **User agent tag**: Use this filter to enable the heuristic to identify mobile and desktop apps. This filter can be set to equals or doesn't equal **Native client**. This filter should be tested against your mobile and desktop apps for each cloud app.<br>NOTE: Session policies don’t support mobile and desktop apps. Mobile apps and desktop apps can also be blocked or allowed by creating an access policy.

6. If you selected the option to **Control file download (with DLP)**, under **Activity source** in the **Files matching all of the following** section, select additional file filters to apply to the policy. These filters can include the following options:
        
    - **Classification label** - Use this filter if your organization uses Azure Information Protection and your data has been protected by its Classification labels. You can filter files based on the Classification label you applied to them. For more information about integration with Azure Information Protection, see [Azure Information Protection integration](https://docs.microsoft.com/cloud-app-security/azip-integration).
        
    - **File name** - Use this filter to apply the policy to specific files.
        
    - **File type** - Use this filter to apply the policy to specific file types, for example, block download for all .xls files.
    
    - In the **Content inspection** section, set whether you want to enable the DLP engine to scan documents and file content.
    
    - Under **Actions**, select one of the following items:
        
        - **Test (Monitor all activities)**: Set this action to explicitly allow download according to the policy filters you set.
        
        - **Block (Block file download and monitor all activities)**: Set this action to explicitly block download according to the policy filters you set. For more information, see [How block download works](https://docs.microsoft.com/en-us/cloud-app-security/session-policy-aad#block-download).
        
        - **Protect (Apply classification label to download and monitor all activities)**: This option is only available if you selected **Control file download (with DLP)** under **Session policy**. If your organization uses Azure Information Protection, you can set an **Action** to apply a classification label set in Azure Information Protection to the file. For more information, see [How protect download works](https://docs.microsoft.com/en-us/cloud-app-security/session-policy-aad#protect-download).

7. You can **Create an alert for each matching event with the policy's severity** and set an alert limit. Select whether you want the alert as an email, a text message, or both.

## Monitor all activities

When you create a session policy, each user session that matches the policy is redirected to session control rather than to the app directly. The user will see a monitoring notice to let them know that their sessions are being monitored.

If you don't want to notify the user that they're being monitored, you can disable the notification message.

1. Under the settings cog, select **General settings**.

2. Then, under **Conditional Access App Control** select **User monitoring** and unselect the **Notify users** checkbox.

To keep the user within the session, Conditional Access App Control replaces all the relevant URLs, Java scripts, and cookies within the app session with Office 365 Cloud App Security URLs. For example, if the app returns a page with links whose domains ends with `myapp.com`, Conditional Access App Control replaces the links with domains ending with something like `myapp.com.us.cas.ms`. This way the entire session is monitored by Office 365 Cloud App Security.

Conditional Access App Control records the traffic logs of every user session that is routed through it. The traffic logs include the time, IP, user agent, URLs visited, and the number of bytes uploaded and downloaded. These logs are analyzed and a continuous report, **Cloud App Security Conditional Access App Control**, is added to the list of Cloud Discovery reports in the Cloud Discovery dashboard.

### To export these logs:

1. Go to the settings cog and click **Conditional Access App Control**.

2. On the right side of the table, click the export button.<br>![export button](media/image3.png)<br>

3. Select the range of the report and click **Export**. This process may take some time.

### To download the exported log:

1. After the report is ready, go to **Settings** and then **Exported reports**.

2. In the table, select the relevant report from the list of **Conditional Access App Control traffic logs** and click download.<br>![download button](media/image4.png)<br>

## Block all downloads

When **Block** is set as the **Action** you want to take in the Cloud App Security session policy, Conditional Access App Control prevents a user from downloading a file per the policy’s file filters. A download event is recognized by Office 365 Cloud App Security for each app when a user starts a download. Conditional Access App Control intervenes in real time to prevent it from running. When the signal is received that a user has initiated a download, Conditional Access App Control returns a **Download restricted** message to the user and replaces the downloaded file with a text file. The text file's message to the user can be configured and customized from the session policy.

## Block specific activities

When **Block activities** is set as the **Activity type**, you can select specific activities to block in specific apps. All activities from selected apps will be monitored and reported in the Activity log. The specific activities you select will be blocked if you select the **Block** action. The specific activities you selected will raise alerts if you select the **Test** action and have alerts turned on.

**Block specific activities** and apply it to specific groups to create a comprehensive read-only mode for your organization.

## Protect files on download

Select **Block activities** to block specific activities, which you can find using the **Activity type** filter. All activities from selected apps will be monitored (and reported in the Activity log). The specific activities you select will be blocked if you select the **Block** action. The specific activities you selected will raise alerts if you select the **Test** action and have alerts turned on.

When **Protect** is set as the **Action** to be taken in the Cloud App Security session policy, Conditional Access App Control enforces the labeling and subsequent protection of a file per the policy’s file filters. Labels are configured in the Azure Information Protection console and **Protect** must be selected within the label for it to appear as an option in the Cloud App Security policy. When a label is selected, and a file is downloaded that meets the criteria of the Cloud App Security policy, the label, and corresponding protection (with permissions) is applied to the file upon download. The original file remains as-is in the cloud app while the downloaded file is now protected. Users who try to access the file must meet the permission requirements determined by the protection applied.

## Next steps

- [Learn about access policies in Office 365 Cloud App Security](ocas-access-policies.md)

- [Blocking downloads on unmanaged devices using Azure AD Conditional Access App Control capabilities](https://docs.microsoft.com/en-us/cloud-app-security/use-case-proxy-block-session-aad)

