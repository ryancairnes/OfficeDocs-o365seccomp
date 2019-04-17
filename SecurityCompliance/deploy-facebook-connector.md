---
title: "Deploy a connector to archive Facebook data in Office 365"
ms.author: markjjo
author: markjjo
manager: laurawi
ms.date: 
ms.audience: Admin
ms.topic: article
ms.service: O365-seccomp
localization_priority: Normal
ms.collection: M365-security-compliance
ROBOTS: NOINDEX, NOFOLLOW
description: "Administrators can set up a native connector to import and archive Facebook Business pages to Office 365. After this data is imported to Office 365, you can use compliance features such as legal hold, content search, and retention policies to manage the governance of your organization's Facebook data."
---

# Deploy a connector to archive Facebook data in Office 365



## Prerequisites

1.  You need to have a Facebook account for your company pages. (This sample connector currently only allows importing data on your company’s Facebook business pages and not individual Facebook profiles.

2.  You should have a valid Azure Subscription
    
    1.  If you don’t have an existing Azure Subscription, you can either get
        
        1.  Free subscription (valid for 1 year) [here](https://azure.microsoft.com/en-us/free/)
        
        2.  Pay as you go subscription [here](https://azure.microsoft.com/en-us/pricing/purchase-options/pay-as-you-go/)

## Set up

1.  Make sure the user who is setting up connector has Mailbox Import Export role.

> For more information see the "Add a role in a role group" or the "Create a role group" sections in [Manage role groups](https://docs.microsoft.com/en-us/exchange/manage-role-groups-exchange-2013-help)

2.  Ensure that you have accepted the consent by following the steps in the below link. Tenant admin has to click below link and log in with their credential.
    
    1.  [<span class="underline">https://login.microsoftonline.com/common/oauth2/authorize?client\_id=570d0bec-d001-4c4e-985e-3ab17fdc3073\&response\_type=code\&redirect\_uri=https://portal.azure.com/\&nonce=1234\&prompt=admin\_consent</span>](https://login.microsoftonline.com/common/oauth2/authorize?client_id=570d0bec-d001-4c4e-985e-3ab17fdc3073&response_type=code&redirect_uri=https://portal.azure.com/&nonce=1234&prompt=admin_consent)

3.  Ensure that you have an active Azure subscription as mentioned in Prerequisites point \#2

4.  Create AAD app using [Azure portal](https://portal.azure.com). Follow the below steps or refer [Create AAD App](#step-2-create-an-app-in-azure-active-directory) with screen shots
    
    2.  Azure Active Directory -\> App Registrations -\> New Application Registration Name of App : - i.e. FacebookConnector or any preferable name

> Application type : - Web app / API
> 
> Sign on URL : - [<span class="underline">https://portal.azure.com</span>](https://portal.azure.com)

3.  Register App and note **AAD APP ID **

4.  Go to app -\> Settings -\> Keys -\> Fill Passwords details -\> Save keys -\> Copy **Password** value and save it to your secret location. This will be used when configuring the Connector.

<!-- end list -->

5.  Create storage account using [Azure portal](https://portal.azure.com). Follow the below steps or refer [Storage account creation](#step-3-create-an-azure-storage-account) with screen shots
    
    5.  Create a new Storage Account (Create a resource -\> Storage -\> Storage Account) -\> Fill details -\> Review & Create -\>It will take some time)
    
    6.  Go to Storage account created above -\> Copy primary **connection string** and save it to a secret location. This will be used during deployment.

6.  Create a Facebook developer App
    
    7.  Refer screenshot [Facebook App Registration](#step-5-register-the-facebook-app) or follow documentation on [Facebook developer portal](https://developers.facebook.com/docs/pages/getting-started/).

## Finalize

1.  Download the builds of connector code and unzip it. It would have a single file
    
      - SampleConnector.zip

2.  Deploy the web app in Azure
    
      - Follow the steps in [Step 4: Create a new web app resource in Azure](#step-4-create-a-new-web-app-resource-in-azure).
    
      - Note your App Service URL required for Facebook App creation and Connector setup in SCC

3.  Configure Login and Webhook products on Facebook developer portal
    
      - LoginUrl
        
          - \<App Service URL\>
    
      - RedirectUrl in Settings of Login product should be
        
          - \<App Service URL\>/Views/FacebookOAuth
    
      - SubscriptionUrl while setting up Webhooks product should be
        
          - \<App Service URL\>/api/FbPageWebhook

4.  Go to Security & Compliance Center <https://protection.office.com> and then go to Data Governance \> Import. Follow the steps in [Step 7: Set up a custom connector in the Security & Compliance Center](#step-7-set-up-a-custom-connector-in-the-security--compliance-center).


## Step 1: Download the package

Download the prebuilt package from repository’s Release section, <https://github.com/Microsoft/m365-sample-connector-csharp-aspnet/releases>.

## Step 2: Create an app in Azure Active Directory

1. Go to <https://portal.azure.com> and sign in using the credentials of an Office 365 global admin account.

    ![Create app in AAD](media/FBCimage1.png)

2. In the left navigation pane, click **Azure Active Directory**.

    ![](media/FBCimage2.png)

3. In the left navigation pane, click **App registrations (Preview)** and then click New registration**.**

    ![](media/FBCimage3.png)

4. Register the application. Under Redirect URI, select Web in the application type dropdown list and then type <https://portal.azure.com> in the box for the URI.

   ![](media/FBCimage4.png)

5. Copy the **Application (client) ID** and **Directory (tenant) ID** and save them to a text file or other safe location. You’ll use these IDs in later steps.

   ![](media/FBCimage5.png)

6. Go to **Certificates & secrets for the new app.**

   ![](media/FBCimage6.png)

7. Click **New client secret**

   ![](media/FBCimage7.png)

8. Create new secret

    ![](media/FBCimage8.png)

9. Copy the client secret and save it to a text file or other storage location. You’ll use this client secret in a later step.

   ![](media/FBCimage9.png)

10. Go to **Manifest** and copy the identifierUris (which is also called the app id uri) as highlighted in the following screenshot. Copy the app id url to a text file or other storage location. You’ll use it in a later step.

   ![](media/FBCimage10.png)

## Step 3: Create an Azure storage account

1. Go to the Azure home page for your organization.

    ![](media/FBCimage11.png)

2. Click **Create a resource** and they type **storage account** in the search box.

    ![](media/FBCimage12.png)

3. Click **Storage**, and then click **Storage account – blob, file, table, queue**.

    ![](media/FBCimage13.png)

4. On the **Create storage account** page, select or create a resource group.

    ![](media/FBCimage14.png)

5. Type a name for the storage account.

    ![](media/FBCimage15.png)

6. Review and then click **Create** to create the storage account.

    ![](media/FBCimage16.png)

7. Click **Go to resource** to navigate to the storage account resource.

    ![](media/FBCimage17.png)

8. Click **Access keys** in the left navigation pane.

    ![](media/FBCimage18.png)

9. Copy the **Connection string** and save it to a text file or other storage location. You’ll use this when creating a web app resource.

    ![](media/FBCimage19.png)

## Step 4: Create a new web app resource in Azure

1. On the **Home** page in the Azure portal, click **Create a resource \> Everything \> Web app**. On the **Web app** page, click **Create**. 

   ![](media/FBCimage20.png)

2. Fill in the details (as shown below) and then create the Web app.

   ![](media/FBCimage21.png)

3. Go to the newly created Web App resource and enter the values (that you copied to the text file) for the following settings: 

    - **APISecretKey** – The is the client secret value that you copied after creating the client secret in Step 2. This will be used to configure the connector service.

    - **StorageAccountConnectionString** – The connection string Uri that you copied after creating the Azure storage account in Step 3.

    - **tenantId** – The tenant ID of your Office 365 organization that you copied after creating the Facebook connector app in Azure Active Directory in Step 2.

    ![](media/FBCimage22.png)

4. On the **Applications settings** page, click **On** next to the **Always On**.

   ![](media/FBCimage23.png)

5. Upload the app service bits (zip file downloaded as mentioned above) using the below url

\<AppService\>.scm.azurewebsites.net/ZipDeployUi

   ![](media/FBCimage24.png)

## Step 5: Register the Facebook app

#### Go to <https://developers.facebook.com> , log in using the credentials for the account for your organization’s Facebook Business pages, and then click **Add New App**.

![](media/FBCimage25.png)

#### Create a new app ID.

![](media/FBCimage26.png)

#### In the left navigation pane, click **Add Products** and then click **Set Up** in the **Facebook Login** tile**.**

![](media/FBCimage27.png)

#### On the Integrate Facebook Login page, click **Web**.

![](media/FBCimage28.png)

#### Add the hosted site URL. 

![](media/FBCimage29.png)

#### Complete the QuickStart section of the Facebook Login setup.

![](media/FBCimage30.png)

#### In the left navigation pane under **Facebook Login**, click **Settings**, and add the OAuth redirect URI in the **Valid OAuth Redirect URIs** box; use the format **\<connectorserviceuri\>/Views/FacebookOAuth,** where the value for connectorserviceuri is the tenantID for your organization.

![](media/FBCimage31.png)

#### In the left navigation pane, click **Add Products** and then click **Webhooks.** In the **Page** pull-down menu, click **Page**. 

![](media/FBCimage32.png)

#### Add Webhooks Callback URL and add a verify token.

![](media/FBCimage33.png)

#### Test and subscribe to the endpoint for feed.

![](media/FBCimage34.png)

#### Add a privacy URL, app icon, and business use.

![](media/FBCimage35.png)

#### Make the app public.

![](media/FBCimage36.png)

#### Add user to the admin or tester role.

![](media/FBCimage37.png)

#### Add the **Page Public Content Access** permission.

![](media/FBCimage38.png)

#### Add Manage Pages permission.

![](media/FBCimage39.png)

#### Get the application reviewed by Facebook.

![](media/FBCimage40.png)

## Step 6: Configure the connector
1. Configure the app service by clicking on the configure button on the home page of your app.

  \<appservice\>.azurewebsites.net

  ![](media/FBCimage41.png)

2. Type your tenant Id and the APISecretKey (that you copied after creating the client secret in Step 2 and added to the application settings in Step 4.) and then click **Set Configuration Settings**.

   ![](media/FBCimage42.png)

3. Enter the following configuration setting under **Configuration Details**:

   - **Facebook application ID** - 
   - **Facebook application secret** - 
   - **Facebook webhooks verify token** - 
   - **AAD application ID** - 
   - **AAD application secret** - 
   - **AAD application Uri** - 
   - **App insights instrumentation key** - 

    ![](media/FBCimage43.png)

4. Click **Save** to save the connector settings.

## Step 7: Set up a custom connector in the Security & Compliance Center

1. Go to <https://protection.office.com> and then click **Data governance \> Import \> Archive third-party data**.

   ![](media/FBCimage44.png)

2.  Click **Add a connector** and then click **Custom**.

    ![](media/FBCimage46.png)

3.  Provide Connector App details and click Next

    ![](media/FBCimage47.png)

    Fill the name as Facebook

    Provide API secret key and connector URL as created in Finalize step 4

4.  Click **Login with Connector App**.

    ![](media/FBCimage45.png)

5. Provide secret and click login to connector service

   ![](media/FBCimage48.png)

Secret key is same as the one entered in step above

6. Click **Continue with Facebook.**

   ![](media/FBCimage49.png)

7. On the **Log in to Facebook** page, log in using the credentials for the account for your organization’s Facebook Business pages. Make sure the Facebook account you logged in to is assigned the admin role for your organization’s Business pages

   ![](media/FBCimage50.png)

8. Click **Select Pages** to choose your organization’s business pages that you want to archive in Office 365.

   ![](media/FBCimage51.png)

9. A list of Business pages managed by the Facebook account that your logged in to is displayed. Select the pages to archive and then click **Save**.

    ![](media/FBCimage52.png)

10. Click **Finish** to exit the setup of the connector service app.

    ![](media/FBCimage53.png)

11. You can apply a filter to only import items (and archive) that are a certain age. 

    ![](media/FBCimage54.png)

12. Specify the mailbox in Office 365 to import (and archive) the items from the Facebook Business pages that you previously selected.

    ![](media/FBCimage55.png)

13. Review settings and then click **Finish** to complete the connector setup.

    ![](media/FBCimage56.png)

14. Go to the **Archive third-party data** page to see the progress of the import process.

    ![](media/FBCimage58.png)
