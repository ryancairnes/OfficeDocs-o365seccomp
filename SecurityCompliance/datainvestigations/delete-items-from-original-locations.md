---
title: "Delete items from original locations"
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

description: "This article describes using the new Data Investigations (Preview) tool in the Security & Compliance Center to delete items from their original locations."
---

# Delete items from original locations

Using data investigations, you can delete items from their original locations (e.g. mailboxes, sharepoint sites) across the tenant. Because you collected items as evidence, you will have copies of the items in an evidence set to further investigate or simply preserve them. 

To delete items from original locations in **Evidence set**:

1. In **Evidence set**, select items that you want to delete. If you select attachments of an email, the parent email will be selected and deleted. 
 
2. Click **Action** and **Delete items from original locations**.

3. Verify the items that you are about to delete and click **Delete**.

Currently, deleted items will be retained until recovery or deleted items retention period expires. This is also known as **Soft delete**. You can check the result of deletion in **Jobs** tab. 
