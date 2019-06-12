---
title: "Set up a connector to archive LinkedIn data in Office 365 (Preview)"
ms.author: markjjo
author: markjjo
manager: laurawi
ms.date: 
audience: Admin
ms.topic: article
ms.service: O365-seccomp
localization_priority: Normal
ms.collection: M365-security-compliance
description: "Administrators can set up a native connector to import data from a LinkedIn Company Page to Office 365. This lets you archive data from third-party data sources in Office 365 so you can use compliance features such as legal hold, content search, and retention policies to manage the compliance of your organization's third-party data."
---

# Set up a connector to archive LinkedIn data in Office 365 (Preview)

The connector feature to archive data from LinkedIn Company pages in Office 365 is in Preview.

Use a native connector in the Security & Compliance Center in Office 365 to import and archive data from LinkedIn Company pages. After you set up and configure a connector, it connects to the account for the specific LinkedIn Company page (once every day), converts the content messages posted to the Company page to an email message format, and then imports those items to a mailbox in Office 365.

After the LinkedIn Company page data is stored in a mailbox, you can use Office 365 compliance features such as Litigation Hold, Content Search, In-Place Archiving, Auditing, and Office 365 retention policies to Instant Bloomberg data. For example, you can search for these items using Content Search or associate the storage mailbox with a custodian in an Advanced eDiscovery case. Using a connector to import and archive LinkedIn data in Office 365 can help your organization stay compliant with government and regulatory policies.

## Before you  begin

- You must have the sign-in credentials (email address or phone number and password) of a LinkedIn user account that is an admin for the LinkedIn Business Page that you want to archive. You'll use these credentials to sign in to LinkedIn when setting up the connector.

- The user who creates an LinkedIn Company Page connector must be assigned the Mailbox Import Export role in Exchange Online. This is required to access the **Archive third-party data** page in the Security & Compliance Center. By default, this role isn't assigned to any role group in Exchange Online. You can add the Mailbox Import Export role to the Organization Management role group in Exchange Online. Or you can create a new role group, assign the Mailbox Import Export role, and then add the appropriate users as members. For more information, see the  [Create role groups](https://docs.microsoft.com/Exchange/permissions-exo/role-groups#create-role-groups) or [Modify role groups](https://docs.microsoft.com/Exchange/permissions-exo/role-groups#modify-role-groups) sections in the article "Manage role groups in Exchange Online".


## Create a LinkedIn connector

1. Go to <https://protection.office.com> and then click **Data governance \> Import** and then click **Archive third-party data**.

2. On the **Archive third-party data** page, click **Add a connector**, and then click **LinkedIn**.

3. On the **Terms of service** page, click **Accept**.

4. On the **Sign in with LinkedIn** page, click **Sign in with LinkedIn**.

5.