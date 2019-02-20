---
title: "Protect apps with Office 365 Cloud App Security Conditional Access App Control"
ms.author: deniseb
author: denisebmsft
manager: laurawi
ms.reviewer: alesibov
ms.audience: Admin
ms.topic: reference
ms.date: 02/14/2019
ms.service: o365-administration
localization_priority: Normal
description: "Stop breaches and leaks in real time with Office 365 Cloud App Security Conditional Access App Control."
---

# Protect apps with Office 365 Cloud App Security Conditional Access App Control

|****Evaluation** \>**|****Planning** \>**|****Deployment** \>**|****Utilization****|
|:-----|:-----|:-----|:-----|
|[Start evaluating](office-365-cas-overview.md) <br/> |[Start planning](get-ready-for-office-365-cas.md) <br/> |You are here!  <br/> [Next step](ocas-deploy-conditional-access-app-control.md) <br/> |[Start utilizing](utilization-activities-for-ocas.md) <br/> |

In today’s workplace, it’s often not enough to know what’s happening in your cloud environment after the fact. You want to stop breaches and leaks in real time, before employees intentionally or inadvertently put your data and your organization at risk. It's important to enable users in your organization to make the most of the services and tools available to them in cloud apps, and let them bring their own devices to work. At the same time, you need tools to help protect your organization from data leaks, and data theft, in real time. Together with Azure Active Directory, Office 365 Cloud App Security delivers these capabilities in a holistic and integrated experience with Conditional Access App Control.

> [!IMPORTANT]
> To use Cloud App Security Conditional Access App Control, you need an [Azure Active Directory P1 license](https://azure.microsoft.com/pricing/details/active-directory/) and an active [Office 365 Cloud App Security](office-365-cas-overview.md) subscription.

## How it works

Conditional Access App Control uses a reverse proxy architecture and is uniquely integrated with Azure AD conditional access. Azure AD conditional access allows you to enforce access controls on your organization’s apps based on certain conditions. The conditions define *who* (user or group of users) and *what* (which cloud apps) and *where* (which locations and networks) a conditional access policy is applied to. After you’ve determined the conditions, you can route users to Office 365 Cloud App Security where you can protect data with Conditional Access App Control by applying access and session controls.

Conditional Access App Control enables user app access and sessions to be monitored and controlled in real time based on access and session policies. Access and session policies are used within the Cloud App Security portal to further refine filters and set actions to be taken on a user. With the access and session policies, you can:

- **Block on download**: You can block the download of sensitive documents. For example, on unmanaged devices.

- **Protect on download**: Instead of blocking the download of sensitive documents, you can require documents to be protected via encryption on download. This encryption makes sure the document is protected and user access is authenticated if the data is downloaded to an untrusted device.

- **Monitor low-trust user sessions**: Risky users are monitored when they sign into apps and their actions are logged from within the session. You can investigate and analyze user behavior to understand where, and under what conditions, session policies should be applied in the future.

- **Block access**: You can completely block access to specific apps for users coming from unmanaged devices or from non-corporate networks.

- **Create read-only mode**: By monitoring and blocking custom in-app activities, you can create a read-only mode to specific apps for specific users.

- **Restrict user sessions from non-corporate networks**: Users accessing a protected app from a location that isn't part of your corporate network are allowed restricted access. The download of sensitive materials is blocked or protected.

### How session control works

Creating a session policy with Conditional Access App Control enables you to control user sessions by redirecting the user through a reverse proxy instead of directly to the app. From then on, user requests and responses go through Office 365 Cloud App Security rather than directly to the app.

To keep the user within the session, all the relevant URLs, Java scripts, and cookies within the app session are replaced with Office 365 Cloud App Security URLs. For example, if the app returns a page with links whose domains end with myapp.com, the link is replaced with domains ending with something like: myapp.com.us.cas.ms

This method doesn't require you to install anything on the device. This method is ideal when monitoring sessions from unmanaged devices.

After a session is directed through Office 365 Cloud App Security, the following actions can be done:

1. Inspect the traffic for user activities

2. Display the identified activities in the Office 365 Cloud App Security Activity log

3. Save the traffic logs and analyze them

4. Enable the admin to export the traffic logs

5. Enforce policies on the session

## Managed device identification

Conditional Access App Control enables you to create policies that take into account whether a device is managed or not. To identify whether a device is managed or not, the feature uses:

- Compliant devices

- Domain-joined devices

- Client certificates deployment

### Compliant and domain-joined devices

Azure AD conditional access enables compliant and domain-joined device information to be passed directly to Office 365 Cloud App Security. From there, an access policy or a session policy can be developed that uses device state as a filter. For more information, see the [Introduction to device management in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/device-management-introduction).

### Client-certificate authenticated devices

The device identification mechanism can request authentication from relevant devices using client certificates. You can either use existing client certificates already deployed in your organization or roll out new client certificates to managed devices. You then use the presence of those certificates to set access and session policies. For information on how to deploy client certificates see [Deploy Conditional Access App Control for Office 365 apps](ocas-deploy-conditional-access-app-control.md).

## Supported apps and clients

Conditional Access App Control for Office 365 supports the following featured apps:

- Exchange Online (preview)

- OneDrive for Business (preview)

- Power BI (preview)

- SharePoint Online (preview)

- Microsoft Teams (preview)

- Yammer (preview)

Additional apps are being continuously on-boarded to session control.

## Next steps

- [Deploy Conditional Access App Control for Office 365 apps](ocas-deploy-conditional-access-app-control.md)

- [Learn about session policies in Office 365 Cloud App Security](ocas-session-policies.md)

- [Learn about access policies in Office 365 Cloud App Security](ocas-access-policies.md) 