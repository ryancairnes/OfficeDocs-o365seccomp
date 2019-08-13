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

You can track the progress of the job on the **Jobs** tab. When the job status is complete, the items are deleted. 

## What happens when you delete items

At this time, when you delete items from their original content location, the items are *soft-deleted*. This means they will be moved to special location and retained until the deleted items retention period expires and an item is marked for permanent deletion from Office 365. Soft-deleting items means users can still recover these items until the retention period expires. The following describes what happens when items are soft-deleted from Exchange mailboxes and SharePoint and OneDrive for Business sites, and what users can do after items are soft-deleted from their original locations.

- **Mailboxes:** When a mailbox item is soft-deleted, it's moved to the Recoverable Items folder in the mailbox.  This is similar to when an is deleted from the Deleted Items folder or when a user deletes an item by pressing Shift + Delete. At this point, the item can be recovered by the user until the deleted item retention period expires. In Office 365, the deleted item retention period is 14 days by default, but can be increased up to 30 days by an admin. After the retention period expires, the item is moved to a hidden folder (called the *Purges* folder). The item is permanently removed (purged) from Office 365 the next time the mailbox is processed (mailboxes are processed once every seven days).

- **SharePoint and OneDrive sites:** When a file or document on a site is soft-deleted, it's moved to the site's Recycle Bin (also called the *first-stage* Recycle Bin). The item remains in the Recycle Bin for 93 days (the deleted item retention period for sites in Office 365). During the 93-day period, deleted items can still be recovered by a site collection administrator in SharePoint or by the user or admin in OneDrive. Items can also be deleted from the first-stage recycle bin. When that happens, they're moved to the Recycle Bin for the site collection, which is called the *second-stage* Recycle Bin. The retention period is 93 days for both the first-stage and second-stage recycle bins. That means the second-stage Recycle Bin retention starts when the item is first deleted. That means the total maximum retention time is 93 days for both recycle bins. If an item is deleted from the second-stage Recycle Bin (either manually by an admin or automatically when the retention period expires), it's no longer accessible by an admin.

## What happens if a content location is on hold

In Office 365, a mailboxes and sites can be placed on hold or assigned to a retention policy. This means that nothing is permanently removed until the retention period for an item expires or until the hold is removed. This means that even if you delete an item from its original location, the item is might not be permanently removed from Office 365. For example, if a mailbox is on hold, soft-deleted items will be moved to Purges or DiscoveryHolds sub-folder in the Recoverable Items folder and retained until the hold-duration or retention period expires. For sites, soft-deleted items are copied to the Preservation Hold library that's create when a hold or retention policy is placed on a site.

