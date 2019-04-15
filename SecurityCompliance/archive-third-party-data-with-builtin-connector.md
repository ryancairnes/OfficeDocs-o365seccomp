---
title: "Use built-in connector to archive third-party data in Office 365"
ms.author: markjjo
author: markjjo
manager: laurawi
ms.date: 
ms.audience: Admin
ms.topic: article
ms.service: O365-seccomp
localization_priority: Normal
ms.collection: M365-security-compliance
description: "Administrators can set up a native connector to import third-party data from data sources such as Facebook Business pages, LinkedIn Company pages, and Instant Bloomberg. This lets you archive data from third-party data sources in Office 365 so you can use compliance features such as legal hold, content search, and retention policies to manage the governance of your organization's third-party data.
---

# Use a built-in connector to archive third-party data in Office 365

Use a built-in connector in the Security & Compliance Center in Office 365 to import and archive data from a third-party data source such as Facebook, LinkedIn, Twitter, and Bloomberg. After you set up and configure a built-in connector, it connects to the third-party data source (on a scheduled basis), converts the content of an item to an email message format, and then imports those items to a mailbox in Office 365.

After third-party data is imported, you can apply Office 365 compliance features such as Litigation Hold, Content Search, In-Place Archiving, Auditing, and Office 365 retention policies to this data. For example, when a mailbox is placed on Litigation Hold or assigned to a retention policy, the third-party data will be retained. You can search third-party data using Content Search or associate it with a custodian in an Advanced eDiscovery case. Using built-in connectors to import and archive third-party data in Office 365 can help your organization stay compliant with government and regulatory policies.

> [!NOTE]
> Currently, only the built-in connector for Facebook Business pages is available. More built-in connectors are coming soon.


## Prerequisites for setting up a connector for Facebook Business pages

You must meet the following prerequisites before you can set up and configure the built-in connector in the Security & Compliance Center to import and archive data from Facebook Business pages. 

- You need a Facebook account for your organization's business pages (you need to sign in to this account when setting up the connector). Currently, you can only archive data from Facebook Business pages; you can't archive data from individual Facebook profiles.

- Your organization must have a valid Azure subscription. If you don't have an existing Azure subscription, you can sign up for one of these options:

    - [Sign up for a free 1 year Azure subscription](https://azure.microsoft.com/free) 

    - [Sign up for a Pay-As-You-Go Azure subscription](https://azure.microsoft.com/pricing/purchase-options/pay-as-you-go/)

> [!NOTE]
> The [free Azure Active Directory subscription](use-your-free-azure-ad-subscription-in-office-365.md) that's included with your Office 365 subscription doesn't support the built-in connectors in the Security & Compliance Center.

## Set up

1.  Ensure that you have accepted the consent by following the steps in the below link. Tenant admin has to click below link and log in with their credential.
    
    -  <https://login.microsoftonline.com/common/oauth2/authorize?client_id=570d0bec-d001-4c4e-985e-3ab17fdc3073&response_type=code&redirect_uri=https://portal.azure.com/&nonce=1234&prompt=admin_consent>

2.  Ensure that you have an active Azure subscription as mentioned in Prerequisites point \#2

3.  Create AAD app using [Azure portal](https://portal.azure.com)

4.  Create storage account using [Azure portal](https://portal.azure.com)

5.  Create a Facebook developer App on [Facebook developer portal](https://developers.facebook.com/docs/pages/getting-started/).

## Finalize

1.  Download the Zip file of connector code

2.  Deploy it in Azure and bring up the connector service

3.  Configure Login and webhook on Facebook developer portal

4.  Go to SCC portal <https://protection.office.com>

5.  Go to Data Governance \> Import\> Archive third-party data. Click on Add connector button, choose custom and follow the onscreen steps
