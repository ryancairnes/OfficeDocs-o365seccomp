---
title: "Add data from one working set to another working set"
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

# Add data to a working set from another working set
In some cases, it may be necessary to carve out a portion of documents from one working set and work with them individually in another working set.  This is especially useful if you've culled content in a working set and want to run analytics on the subset of data.

Use the following workflow to add content from one working set to another.

## Before you start
Before you start, you'll need to create a new working set.  A new working set can be added through the *Working sets* tab [Learn more](https://docs.microsoft.com/en-us/office365/securitycompliance/compliance20/managing-working-sets).

## Step 1: Identify content to add to another working set
You can add content to a working set by selecting emails and documents in the document grid or all items in a search result.  If choosing to add selected items, select the items and click the *Action* drop down then *Add to another working set*.

![Add to another working set](../media/64f2a4d4-eba3-4ab3-a3ba-d519feea3142.png)

## Step 2: Specify options for adding to another workings set
In the *Add to another working set options* flyout, first choose the working set you want to add the items to.  Choose whether to add All search results or Selected items.  Additional information provides options to include all metadata from the items and finally whether or not the document tags should be included in the new working set.  After clicking *OK* a new job will be created to add the content to a working set, you can monitor the progress of that job in the [Jobs](https://docs.microsoft.com/en-us/office365/securitycompliance/compliance20/managing-jobs-ediscovery20) tab.
![Add to another working set](../media/6440ee44-68fd-44d7-b43a-3a477345525c.png)
