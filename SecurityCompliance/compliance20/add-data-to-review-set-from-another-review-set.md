---
title: "Add data from one review set to another review set"
ms.author: markjjo
author: markjjo
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

description: ""
---

# Add data to a review set from another review set

In some cases, it may be necessary to carve out a portion of documents from one review set and work with them individually in another review set.  This is especially useful if you've culled content in a review set and want to run analytics on the subset of data.

Use the following workflow to add content from one review set to another.

## Before you begin

Before you start, you'll need to create a new review set to add the data to.  A new review set can be added on the **Review sets** tab of the case. For more information, see [Manage review sets](managing-review-sets.md).

## Step 1: Identify content to add to another review set

You can add content to a review set by selecting emails and documents in the document grid or all items in a search result.  If choosing to add selected items, select the items, click **Action**, and then click **Add to another review set**.

![Add to another review set](../media/64f2a4d4-eba3-4ab3-a3ba-d519feea3142.png)

## Step 2: Specify options for adding to another review set

In the **Add to another review set** flyout page, choose the review set you want to add the items to. Choose whether to add **All search results** or **Selected items**.  Additional information provides options to include all metadata from the items and finally whether or not the document tags should be included in the new review set.  After clicking **Ok** a new job will be created to add the content to a review set; you can monitor the progress of that job on the **Job** tab. For more information, see [Manage jobs](managing-jobs-ediscovery20.md).

![Add to another review set](../media/6440ee44-68fd-44d7-b43a-3a477345525c.png)
