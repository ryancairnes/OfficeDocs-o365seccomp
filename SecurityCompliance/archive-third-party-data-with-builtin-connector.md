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

You must meet the following prerequisites before you can set up and configure a built-in connector in the Security & Compliance Center to import and archive data from your organization's Facebook Business pages. 

- You need a Facebook account for your organization's business pages (you need to sign in to this account when setting up the connector). Currently, you can only archive data from Facebook Business pages; you can't archive data from individual Facebook profiles.

- Your organization must have a valid Azure subscription. If you don't have an existing Azure subscription, you can sign up for one of these options:

    - [Sign up for a free 1 year Azure subscription](https://azure.microsoft.com/free) 

    - [Sign up for a Pay-As-You-Go Azure subscription](https://azure.microsoft.com/pricing/purchase-options/pay-as-you-go/)

    > [!NOTE]
    > The [free Azure Active Directory subscription](use-your-free-azure-ad-subscription-in-office-365.md) that's included with your Office 365 subscription doesn't support the built-in connectors in the Security & Compliance Center.

- Your organization must consent to allow the Office 365 Import service access mailbox data in your organization. To consent to this request, go to [this page](https://login.microsoftonline.com/common/oauth2/authorize?client_id=570d0bec-d001-4c4e-985e-3ab17fdc3073&response_type=code&redirect_uri=https://portal.azure.com/&nonce=1234&prompt=admin_consent), sign in use the credentials of an Office 365 global admin, and then accept the request.

## Step 1: Create an app in Azure Active Directory

The first step is to register a new app in Azure Active Directory. This app will corresponding to the Facebook connector that you'll implement in Step 5. 

For step-by-step instructions, see 



## Step 2: Create an Azure storage account

The Facebook Connector will store the items from your Facebook Business pages to the Azure storage location that you create in this step. The connection string for the Azure storage location will be used to configure the connector in Step 6.

For step-by-step instructions, see


## Step 3: Create a web app resource in Azure



## Step 4: Register the web app on Facebook

The next step is to create and configure a new app on Facebook. 


## Step 5: Download the pre-built connector app package from Github

The next step is to download the source code for the pre-built Facebook connector app that will use a Facebook API to connect to your Facebook Business pages and extract Facebook data so you can import it to Office 365.

1. Go to [this GitHub site](https://github.com/Microsoft/m365-sample-connector-csharp-aspnet). 
2. Click **Clone or download** and then click **Download ZIP**.
3. Save the ZIP file to a location on your local computer.
4. Extract all files in the ZIP file.

## Step 6: Configure the connector app



## Step 7: Set up a custom connector in the Security & Compliance Center

The final step is to set up the custom connector in the Security & Compliance Center that will import data from your Facebook Business pages to a specified mailbox in Office 365.





## Set up


3.  Create AAD app using [Azure portal](https://portal.azure.com)

4.  Create storage account using [Azure portal](https://portal.azure.com)

5.  Create a Facebook developer App on [Facebook developer portal](https://developers.facebook.com/docs/pages/getting-started/).

## Finalize

1.  Download the Zip file of connector code

2.  Deploy it in Azure and bring up the connector service

3.  Configure Login and webhook on Facebook developer portal

4.  Go to SCC portal <https://protection.office.com>

5.  Go to Data Governance \> Import\> Archive third-party data. Click on Add connector button, choose custom and follow the onscreen steps
