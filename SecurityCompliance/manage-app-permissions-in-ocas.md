---
title: "Manage OAuth apps using Office 365 Cloud App Security"
ms.author: deniseb
author: denisebmsft
manager: laurawi
ms.date: 12/26/2018
ms.audience: ITPro
ms.topic: article
ms.service: O365-seccomp
localization_priority: Normal
search.appverid:
- MET150
- MOE150
ms.assetid: 2062c312-b1e4-4ce7-8cb2-ea39bc0dfdad
description: "OAuth apps in Office 365 Cloud App Security help you manage the apps your users download for use with Office 365 data"
---

# Manage OAuth apps using Office 365 Cloud App Security

|****Evaluation** \>**|****Planning** \>**|****Deployment** \>**|****Utilization****|
|:-----|:-----|:-----|:-----|
|[Start evaluating](office-365-cas-overview.md) <br/> |[Start planning](get-ready-for-office-365-cas.md) <br/> |[Start deploying](turn-on-office-365-cas.md) <br/> |You are here!  <br/> [Next steps](manage-app-permissions-in-ocas.md#nextsteps) <br/> |
   
People love apps and they download them often, especially apps that people think will save time by making it easier to get at their work or school information. However, some apps could potentially be a security risk to your organization, depending on what information they access and how they handle that information. With [Office 365 Cloud App Security](office-365-cas-overview.md), if you are a global or security administrator, you can manage OAuth apps for your organization. You can see the apps people are using with Office 365 data, what permissions those apps have, and more. 
  
This article describes where to go to manage OAuth apps, how to approve, ban, or report an app, and how to create an app query.
  
## How to find the Manage OAuth apps page

> [!NOTE]
> OAuth apps are managed in the Office 365 Cloud App Security portal. You must be a global administrator or security administrator to perform the following task. To learn more see [Permissions in the Office 365 Security &amp; Compliance Center](permissions-in-the-security-and-compliance-center.md). 
  
1. Go to the Cloud App Security portal ([https://portal.cloudappsecurity.com](https://portal.cloudappsecurity.com)) and sign in.
  
2. Choose **Investigate** \> **OAuth apps**.<br/>![In the O365 CAS portal, choose Investigate.](media/OCAS-OAuthApps.png)<br/>
  
## What you'll see on the Manage OAuth apps page

The following table describes the controls and options available on the Manage OAuth apps page.
  
|**Item**|**Description**|
|:-----|:-----|
|Basic icon in the app query bar  <br/> ![Icon that indicates basic query view for querying](media/a459bc51-e86b-43d5-a0ee-661b9fb4afc9.png)|Select this to switch to the Advanced view.  <br/> (If you see **Basic**, you are using the Advanced view)  <br/> |
|Advanced icon in the app query bar  <br/> ![Icon that indicates advanced query view for querying](media/9958d832-2c81-45ed-a642-d926310ba6b6.png)|Select this to switch to the Basic view.  <br/> (If you see **Advanced**, you are using the Basic view.)  <br/> |
|Open or close all details icon in the app list  <br/> ![Click this icon to open or close all details for all apps](media/018fa996-10e8-48ff-986e-55f2b69a5753.png)|Select this icon to view more or fewer details about each app.  <br/> |
|Export icon in the app list  <br/> ![Click this icon to export a csv file of all apps](media/98446851-fd96-4d09-9bb0-831db33090c1.png)|Select this icon to export a CSV file that contains a list of apps, number of users for each app, permissions associated with the app, permissions level, app state, and community use level.  <br/> |
|Name  <br/> |Use this to see the name of an app. Select the name to view more information, such as its description, publisher, app website and app ID.  <br/> |
|Authorized by  <br/> |Use this to see how many users have authorized an app to access their Office 365 account. Select the number to view more information, such as a list of user accounts.  <br/> |
|Permissions Level  <br/> ![Icon that indicates the permisiions level for an app](media/aaebdd29-35b6-4c62-aef1-7c7817bd803d.png)|Use this to see how much access an app has to Office 365 data. Permissions levels indicate **Low**, **Medium**, or **High**, where **Low** might indicate that the app only accesses a user's profile and name. Select the level to view more information, such as permissions granted to the app, community use, and related activity in the [Governance log](suspend-or-restore-an-account-in-ocas.md).  <br/> |
|Last authorized <br/> |Use this to see the date and time an OAuth app was last authorized to access your organization's Office 365 data. <br/>  |
|Actions<br/>![OAuth apps](media/OCAS-OAuthAppApproveBanReport.png)<br/> |Use this to see or to mark an app as Approved or Banned, report an OAuth app to Microsoft, or leave it as undetermined.  <br/> |
   
## Mark an app as approved

On the **Manage OAuth apps** page, locate the app you want to approve, and choose the **Mark app as approved** icon. 
  
![Choose the Mark app as approved icon](media/OCAS-MarkOAuthApproved.png)
  
The icon turns green, and the app is approved for all your Office 365 users.
  
> [!NOTE]
> When you mark an app as approved, there is no effect on the end user. Visually marking the apps that are approved helps to separate them from apps that haven't been reviewed yet. 
  
## Ban an app

1. On the **Manage OAuth apps** page, locate the app you want to ban, and choose the **Mark app as banned** icon.<br/>![Choose the Mark app as banned icon](media/OCAS-MarkOAuthBanned.png)
  
2. In the notification message box, keep the existing text as it is, or customize the text. Choose whether to let users know that their app has been banned. <br/>![The mail template for a banned app](media/6d132700-5f7f-472c-bfb5-a44549e69c16.jpg)<br/>
  
3. Choose **Ban app**.

## Report an OAuth app to Microsoft

If you want to submit an OAuth app to Microsoft for analysis, you can report that app.

1. On the **Manage OAuth apps** page, locate the app you want to submit for analysis.

2. Choose the vertical ellipsis, and then choose **Report app...**.<br/>![Report an OAuth app](media/OCAS-MarkOAuthReported.png)<br/>

3. In the **Report this app** dialog box, use the drop-down list to indicate your concern. By default, **This app is malicious** is selected. However, you can choose on one of the other available options. <br/>![Report an OAuth app](media/OCAS-ReportOAuthApp.png)<br/>

4. (Recommended) Keep the option to contact you selected, and confirm (or edit) the email address listed.

5. Choose **Submit**. 
    
## Create an app query

We recommend using the Advanced view, which looks like this: 

![Advanced view](media/OCAS-OAuthAppsAdvQueryView.png)

In the app query bar, if you see **Advanced**, you're using the Basic view. Click (or tap) **Advanced** to go to the Advanced view. 

![Basic view](media/OCAS-OAuthAppsBasicQueryView.png)
    
1. In the query bar, use the **Select a filter** list to choose an option. 
    - **App** Apps with certain names
    - **App state** Apps based on their state (Approved, Banned, or Undetermined)
    - **Community use** Apps based on community use levels (Rare, Uncommon, or Common)
    - **Permission level** Apps based on certain permission levels 
    - **Permissions** Apps that require certain permissions
    - **Publisher**  Apps from certain publishers
    - **User** Apps that a certain user authorized
   
2. Select **equals** or **does not equal**, and then specify a value for your filter.
    
3. To add more filters, select the plus sign (![Add a filter icon for querying apps](media/771b2958-67cd-4e14-9302-283ef238cae5.jpg)), and then repeat steps 2 and 3.
    
4. To remove a filter, select the x (![Remove a filter icon for querying apps](media/5339277f-555d-4749-8dcc-d2574250556e.jpg)) next to a filter name.
    
The filters are applied automatically, and the apps list is updated accordingly.
  
## Next steps

- [Review and take action on alerts](review-office-365-cas-alerts.md)
    
- Review your [Web traffic logs and data sources for Office 365 Cloud App Security](web-traffic-logs-and-data-sources-for-ocas.md)
    
- Review your [utilization activities for Office 365 Cloud App Security](utilization-activities-for-ocas.md)
    

