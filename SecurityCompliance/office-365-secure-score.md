---
title: "Office 365 Secure Score"
ms.author: deniseb
author: denisebmsft
manager: laurawi
ms.date: 01/25/2019
ms.audience: Admin
ms.topic: overview
ms.service: o365-administration
localization_priority: Normal
search.appverid: 
- MOE150
- MET150
ms.assetid: c9e7160f-2c34-4bd0-a548-5ddcc862eaef
description: "Ever wonder how secure your organization really is in Office 365? Secure Score is here to help. Secure Score analyzes your organization's security  based on your regular activities and security settings in Office 365, and assigns a score."
---

# Office 365 Secure Score

**Summary** Ever wonder how secure your organization really is in Office 365? Secure Score is here to help. Secure Score analyzes your organization's security  based on your regular activities and security settings in Office 365, and assigns a score. Read this article to get an overview of Secure Score and how you can use it.
  
## How to get to Secure Score

If your organization has a subscription that includes [Office 365 Enterprise](https://docs.microsoft.com/office365/enterprise/), [Microsoft 365 Business](https://docs.microsoft.com/microsoft-365/business/), or Office 365 Business Premium, and you have the [necessary permissions](#required-permissions), you can view your organization's secure score by visiting [https://securescore.office.com](https://securescore.office.com). 

Alternatively, you can visit the Security & Compliance Center ([https://protection.office.com](https://protection.office.com)), where you'll find a Secure Score widget that provides you with your current score.

![Secure Score widget](media/SecureScoreWidget-o365.png)

The widget includes a link to your Secure Score dashboard.

![Secure Score dashboard](media/SecureScore-WelcomeScreen.png)
  
## How it works

Secure Score determines what Office 365 services you're using (such as OneDrive, SharePoint, and Exchange) then compares your settings and activities to a baseline established by Microsoft. You'll get a score based on how well aligned your organization is with security best practices. You'll also get recommendations on steps you can take to improve your organization's score. 
  
![Actions queue in the Office 365 Secure Score tool](media/SecureScore-ActionsToTake.png)
  
Secure Score calculates your score based on the services you purchased. For example, if you only purchased an Exchange Online plan, you won't be scored for SharePoint Online security features. The denominator of the score is the sum of all the baselines for the controls that apply to the products you purchased. The numerator is the sum of all the controls for which you completed, or partially completed, the actions to fulfill that control.

Expand an action to learn about what steps to take, the threats it'll help protect you from, and how many points your score will increase once you follow the recommendation.
  
![Expanded action in the Office 365 Secure Score tool](media/SecureScore-DetailedActionToTake.png)
  
To see the impact of your actions on your organization's security, select the **Score Analyzer** tab and review your history. 
  
![Score Analyzer tab of the Office 365 Secure Score tool](media/SecureScore-ScoreAnalyzer-7days.png)
  
Below the chart, you'll see a list of scores and actions by category. 
  
![Graph on the Score Analyzer tab showing a data point selected](media/SecureScore-Analyzer-breakdownbelowchart.png)
 
Actions that are labeled as **[Not Scored]** are ones you can perform for your organization, but because they are not connected to Secure Score, they are not scored.  

On the **Score Analyzer** page, click a data point for a specific day, then scroll down to see the completed and incomplete actions for that day to find out what changed. The score is calculated once per day (around 1:00 AM PST). If you make a change to a measured action, the score will automatically update the next day. It takes up to 48 hours for a change to be reflected in your score.

Secure Score does not express an absolute measure of how likely you are to get breached. It expresses the extent to which you have adopted features that can offset the risk of being breached. No service can guarantee that you will not be breached, and the Secure Score should not be interpreted as a guarantee in any way.
 
## How Secure Score helps

With Secure Score, you can help improve your organization's security posture by using the built-in security features in Office 365 (many of which you already purchased but might not be aware of). Learning more about these features can help give you peace of mind that you're taking the right steps to protect your organization from threats.
  
But don't just take our word for it. Customers who are using Secure Score have seen their score increase five times more than customers who aren't using it. (The increase in their score corresponds with the security features being used in their organizations.)
  
> [!NOTE]
> Secure Score does not express an absolute measure of how likely you are to get breached. It expresses the extent to which you have adopted controls which can offset the risk of being breached. No service can guarantee that you will not be breached, and Secure Score should not be interpreted as a guarantee in any way. 
  
## Required permissions

In order to view and use your Secure Score dashboard, you must be assigned one of the following roles in Azure Active Directory:
- Global Administrator
- Billing Administrator
- User Administrator
- Password Administrator
- Security Administrator
- Security Reader
- Exchange Administrator
- SharePoint Administrator

 Users who aren't assigned an admin role won't be able to access Secure Score.

## Related topics

[Security dashboard overview](security-dashboard.md)

[What subscription do I have?](https://docs.microsoft.com/office365/admin/admin-overview/what-subscription-do-i-have?view=o365-worldwide)