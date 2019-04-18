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

After third-party data is imported, you can apply Office 365 compliance features such as Litigation Hold, Content Search, In-Place Archiving, Auditing, Supervision, and Office 365 retention policies to this data. For example, when a mailbox is placed on Litigation Hold or assigned to a retention policy, the third-party data will be retained. You can search third-party data using Content Search or associate it with a custodian in an Advanced eDiscovery case. Using built-in connectors to import and archive third-party data in Office 365 can help your organization stay compliant with government and regulatory policies.

> [!NOTE]
> Currently, only the built-in connector for Facebook Business pages is available. More built-in connectors are coming soon.


## Prerequisites for setting up a connector for Facebook Business pages

You must complete the following prerequisites before you can set up and configure a built-in connector in the Security & Compliance Center to import and archive data from your organization's Facebook Business pages. 

- You need a Facebook account for your organization's business pages (you need to sign in to this account when setting up the connector). Currently, you can only archive data from Facebook Business pages; you can't archive data from individual Facebook profiles.

- Your organization must have a valid Azure subscription. If you don't have an existing Azure subscription, you can sign up for one of these options:

    - [Sign up for a free 1 year Azure subscription](https://azure.microsoft.com/free) 

    - [Sign up for a Pay-As-You-Go Azure subscription](https://azure.microsoft.com/pricing/purchase-options/pay-as-you-go/)

    > [!NOTE]
    > The [free Azure Active Directory subscription](use-your-free-azure-ad-subscription-in-office-365.md) that's included with your Office 365 subscription doesn't support the built-in connectors in the Security & Compliance Center.

- Your organization must consent to allow the Office 365 Import service to access mailbox data in your organization. To consent to this request, go to [this page](https://login.microsoftonline.com/common/oauth2/authorize?client_id=570d0bec-d001-4c4e-985e-3ab17fdc3073&response_type=code&redirect_uri=https://portal.azure.com/&nonce=1234&prompt=admin_consent), sign in with the credentials of an Office 365 global admin, and then accept the request.

- The user who sets up the customer connector in the Security & Compliance (in Step 7) must be assigned the Mailbox Import Export role in Exchange Online. By default, this role isn't assigned to any role group in Exchange Online. You can add the Mailbox Import Export role to the Organization Management role group in Exchange Online. Or you can create a new role group, assign the Mailbox Import Export role, and then add the appropriate users as members. For more information, see the  [Create role groups](https://docs.microsoft.com/Exchange/permissions-exo/role-groups#create-role-groups) or [Modify role groups](https://docs.microsoft.com/Exchange/permissions-exo/role-groups#modify-role-groups) sections in the article "Manage role groups in Exchange Online".

## Step 1: Download the pre-built connector app package from Github

The first step is to download the source code for the pre-built Facebook connector app that will use a Facebook API to connect to your Facebook Business pages and extract Facebook data so you can import it to Office 365.

1. Go to [this GitHub site](https://github.com/Microsoft/m365-sample-connector-csharp-aspnet/releases). 
2. Under the latest release, click the **SampleConnector.zip** file.
3. Save the ZIP file to a location on your local computer. You'll upload this zip file to Azure in Step 4.

## Step 2: Create an app in Azure Active Directory

The next step is to register a new app in Azure Active Directory. This app will correspond to the Facebook connector that you'll implement in Step 4. 

For step-by-step instructions, see [Create an app in Azure Active Directory](deploy-facebook-connector.md#step-2-create-an-app-in-azure-active-directory).

During the completion of this step (by following the step-by-step instructions), you'll save the following information to a text file. The values for these will be used in later steps of the deployment process.

- Application ID
- Tenant ID
- Client secret

## Step 3: Create an Azure storage account

The Facebook Connector that you deploy for your organization will store the items from your Facebook Business pages to the Azure storage location that you create in this step. After you create a custom connector in the Security & Compliance Center (in Step 7), the Office 365 Import service will copy the Facebook data from the Azure storage location to a mailbox in Office 365. As previous explained in the [Prerequisites](#prerequisites-for-setting-up-a-connector-for-facebook-business-pages) section, you must have a valid Azure subscription to create an Azure storage account.

For step-by-step instructions, see [Create an Azure storage account](deploy-facebook-connector.md#step-3-create-an-azure-storage-account).

During the completion of this step (by following the step-by-step instructions) you'll save the connection string Uri that is generated. You'll use this string when creating a web app resource in Azure in Step 4.

## Step 4: Create a web app resource in Azure

The next step is to create a web app resource in Azure for the Facebook Connector  For step-by-step instructions, see [Create a new web app resource in Azure](deploy-facebook-connector.md#step-4-create-a-new-web-app-resource-in-azure).

During the completion of this step (by following the step-by-step instructions), you'll provide the following information (that you've copied to a text file after completing the previous steps) when creating the web app resource.

- APISecretKey – The client secret value that you copied after creating the client secret in Step 2. This will be used to configure the connector service.

- StorageAccountConnectionString – The connection string Uri that you copied after creating the Azure storage account in Step 3.

- tenantId – The tenant ID of your Office 365 organization that you copied after creating the Facebook connector app in Azure Active Directory in Step 2.

Additionally, you will upload the SampleConnector.zip file (that you downloaded in Step 1) in this step to deploy the source code for the Facebook connector app.

After completing this step, be sure to copy the app Service URL (for example, https://facebookconnector.azurewebsites.net ). You'll need to use this to complete Step 5, Step 6, and Step 7).

## Step 5: Register the web app on Facebook

The next step is to create and configure a new app on Facebook. The custom connector that you create in Step 7 will use the Facebook web app to interact with the Facebook API to obtain data from your organization's Facebook Business pages.

For step-by-step instructions, see [Register the Facebook app](deploy-facebook-connector.md#step-5-register-the-facebook-app).

During the completion of this step (by following the step-by-step instructions), you'll save the following information to a text file. The values for these will be used to configure the connector app in Step 7.

- Facebook application ID
- Facebook application secret
- Facebook Webhooks verify token

## Step 6: Configure the Facebook connector app

The next step is to add configurations settings to the Facebook connector app that you uploaded when you created the Azure web app resource in Step 4. You'll do this by going to the home page of your connector app and configuring it.

For step-by-step instructions, see [Configure the connector](deploy-facebook-connector.md#step-6-configure-the-connector).

During the completion of this step (by following the step-by-step instructions), you'll provide the following information (that you've copied to a text file after completing the previous steps).

- Facebook application ID (obtained in Step 5)
- Facebook application secret (obtained in Step 5)
- Facebook webhooks verify token(obtained in Step 5)
- Azure Active Directory application ID (obtained in Step 2)
- Azure Active Directory application secret (the client secret obtained in Step 2)
- Azure Active Directory application Uri (the Azure app service URL obtained in Step 4; for example, https://facebookconnector.azurewebsites.net)
- App insights instrumentation key


## Step 7: Set up a custom connector in the Security & Compliance Center

The final step is to set up the custom connector in the Security & Compliance Center that will import data from your Facebook Business pages to a specified mailbox in Office 365. After you successfully complete this step, the Office 365 Import service will starting importing data from your Facebook Business pages to Office 365. 

For step-by-step instructions, see [Set up a custom connector in the Security & Compliance Center](deploy-facebook-connector.md#step-7-set-up-a-custom-connector-in-the-security--compliance-center). 

During the completion of this step (by following the step-by-step instructions), you'll provide the following information (that you've copied to a text file after completing the steps).

- Azure app service URL (obtained in Step 4; for example https://facebookconnector.azurewebsites.net)
- Client secret (obtained in Step 2)

