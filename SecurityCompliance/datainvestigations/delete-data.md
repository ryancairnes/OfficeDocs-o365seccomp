---
title: "Delete data during data Investigation"
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

description: "This article describes how to delete data during investigation."
---

# Delete data during data investigation

Once you identified locations of misplaced, confidential or sensitive data, you may want to delete them so that the end users no longer has access. You can do this by using Security & Compliance Center and SharePoint Online Management PowerShell Commandlets.

## Before you begin

- Cmdlets & Roles required for email delete
- Cmdlets & Roles required for SPO
- Mention workflow is slightly broken but UI solution is coming up? 

## How to delete emails 

- Workflow: Search -> Validate in evidence tab if needed -> Use SCC cmdlet & search query to delete
- Additional info to capture: Provide examples and compare soft vs hard delete, impacting configs (e.g. legal hold, single-item recovery)
- How to validate this change: it's not easy to check (https://docs.microsoft.com/en-us/office365/securitycompliance/use-content-search-for-targeted-collections). e.g. SCC cmdlet doesn't have DumpsterOnly

## How to delete OneDrive or SharePoint sites 

- Workflow: Search -> Go to evidence tab, filter by SPO -> Check file path in metadata -> run SPO delete cmdlet per file or collection manually
- Additional info to capture: Provide examples and compare soft vs hard delete, impacting configs (e.g. legal hold, single-item recovery)
- How to validate: ... difficult... re-run search x many days later?