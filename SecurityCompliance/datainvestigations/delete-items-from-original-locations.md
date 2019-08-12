---
title: "Delete items from their original location"
ms.author: markjjo
manager: laurawi
ms.date: 
ms.audience: Admin
ms.topic: article
ms.service: O365-seccomp
localization_priority: Normal
ms.collection: M365-security-compliance
search.appverid: 
- MOE150
- MET150
ms.assetid: 

description: "This article describes how to use the new Data Investigations (Preview) tool in the Security & Compliance Center to delete items from their original locations."
---

# Delete items from their original location

Using data investigations, you can delete items from their original locations. This means you can delete items from  Exchange mailboxes, SharePoint sites, and OneDrive accounts across your organization. Because you collected items as evidence, you will have copies of the items retained in an evidence set to further investigate or to simply. 

## Before you begin

- To delete items, you have to be assigned the **Search And Purge** role in the Security & Compliance Center. This role is assigned by default to the built-in Data Investigator role group. 

- The procedure in this topic assume that you have run a content search associated with a data investigation and added the search results to evidence. After search results are added to evidence, you can select one or more items to delete. For more information, see [Search for data in an investigation](search-for-data.md).

- It's important to keep in mind that only the item in the original content locations (such as Exchange mailboxes, SharePoint sites, and OneDrive accounts) are deleted. These same items aren't deleted from the evidence set. That's because the items in an evidence set are copies of the original items. These were copied when you added the results of a search to an evidence set.

## Delete items

Perform the following steps to delete items from their original location:

1. In Data Investigations tool open the data investigation that contains the items you want to delete, and then click the the **Evidence** tab.

2. Select items that you want to delete. You can select all items in the evidence set or select just a subset of items. 

   > [!NOTE]
   > If you select the attachments of an email or a file attached to a document in SharePoint and OneDrive, the parent item will be also be selected and deleted when the item is deleted from its original location.
 
2. Click **Action** and then click **Delete items from original locations**.

3. Verify the items that you are about to delete and click **Delete**.

4. You can check the result of deletion in **Jobs** tab. 

## What happens when you delete items

At this time, when you delete items from their original content location, the items are *soft-deleted*. This means they will be moved to special location and retained until the deleted items retention period expires and the item is  marked for permanent deletion. This means users can still recover these deleted items until the retention period expires.  The following describes what happens and what users can do after mailbox and sites items are soft-deleted from their original locations.


(from DSR guide)

In Office 365 services such as Exchange Online, SharePoint Online, and OneDrive for Business there is the concept of soft deletion and hard deletion, which relates to the recoverability of a deleted item (usually for a limited period) before it’s permanently removed from the Microsoft cloud with no chance of recovery. In this context, a soft-deleted item can be recovered by a user and/or an admin for a limited amount of time before it’s hard-deleted. When an item has been hard-deleted, it’s marked for permanent removal and is purged when it's processed by the corresponding Office 365 service. Here’s how soft delete and hard delete works for items in mailboxes and sites (regardless of whether the data owner or an admin deletes an item):

Mailboxes: An item is soft-deleted when it’s deleted from the Deleted Items folder or when a user deletes an item by pressing Shift + Delete. When item is soft-deleted, it's moved to the Recoverable Items folder in the mailbox. At this point, the item can be recovered by the user until the deleted item retention period expires (in Office 365, the deleted item retention period is 14 days, but can be increased up to 30 days by an admin). After the retention period expires, the item is hard-deleted and moved to a hidden folder (called the Purges folder). The item will be permanently removed (purged) from Office 365 the next time the mailbox is processed (mailboxes are processed once every seven days).

SharePoint Online and OneDrive for Business sites: When a file or documented is deleted, it is moved to the site’s Recycle Bin (also called the first-stage Recycle Bin (which is like the Recycle Bin in Windows). The item remains in the Recycle Bin for 93 days (the deleted item retention period for sites in Office 365). After that period, the item is automatically moved to Recycle Bin for the site collection, which also called the second-stage Recycle Bin. (Note that users or admins--with the appropriate permissions--can also delete items from the first-stage Recycle Bin). At this point, the item becomes soft-deleted; it can still be recovered by a site collection administrator in SharePoint Online or by the user or admin in OneDrive for Business). When an item is deleted from the second-stage Recycle Bin (either manually or automatically), it becomes hard-deleted and isn't accessible by user or an admin. The retention period is 93 days for both the first-stage and second-stage recycle bins. That means the second-stage Recycle Bin retention starts when the item is first deleted. Therefore, the total maximum retention time is 93 days for both recycle bins.

## What happens if a content location is on hold

In Office 365, a “hold” can be place on mailboxes and sites. In short, this means that nothing is permanently removed (hard-deleted) if a mailbox or site is on hold, until the retention period for an item expires or until the hold is removed. This is important in the context of deleting Customer Content in response to a DSR: if an item is hard-deleted from a content location that is on hold, the item is not permanently removed from Office 365. That means it could conceivably be recovered by an IT admin. If your organization has a requirement or policy that data be permanently deleted and unrecoverable in Office 365 in response to DSR, then a hold would have to be removed from a mailbox or site to permanently delete data in Office 365. More than likely, your organization’s guidelines for responding to DSRs have a process in place to determine whether a specific DSR deletion request or a legal hold takes precedence. If a hold is removed to delete items, it can be reimplemented after the item is deleted.

