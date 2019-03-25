---
title: "Manage jobs in Advanced eDiscovery (Preview)"
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

# Manage jobs in Advanced eDiscovery (Preview)

Here's a list of the jobs that are tracked on the **Jobs** tab of a case in Advanced eDiscovery (Preview).

| Job Type | Description | Workloads this job applies to |
| :- | :- | :- |
| Re-indexing custodian data | When a custodian is added to a case, all partially indexed items are re-indexed with Advanced eDiscovery indexing, for more information, see [Advanced indexing of custodian data](indexing-custodian-data.md). | Advanced eDiscovery |
| Estimating search results | Estimating search results is the result of creating and running a search against workloads such as Exchange, SharePoint and OneDrive for Business.  The estimates include statistics such as number of items returned by the search and size.  For more information on search, see [Collect data for a case in Advanced eDiscovery](collecting-data-for-ediscovery.md). | Advanced eDiscovery |
| Preparing search preview | Preparing search preview jobs are the result of creating and running a search against workloads such as Exchange, SharePoint and OneDrive for Business.  A preview of the search results are available to help determine the efficacy of the search.  For more information on search, see [Collect data for a case in Advanced eDiscovery](collecting-data-for-ediscovery.md). | Advanced eDiscovery |
| Adding data to a working set | Adding data to a working set jobs happen when the results of a search are added to a working set.  For more information on managing working sets, see [Manage working sets in Advanced eDiscovery](managing-working-sets.md). | Advanced eDiscovery |
| Adding data to another working set | Adding data to another working set jobs are created when a user chooses to added data from one working set to another. | Advanced eDiscovery |
| Adding non-Office 365 data to a working set | Adding non-Office 365 data to a working set jobs include processing and adding data to a working set that was uploaded from a client computer which may be relevant to a case, for more information on adding Non-Office 365 data, see [Load non-Office 365 data into a working set](load-non-office365-data.md). | Advanced eDiscovery |
| Preparing for error resolution |  | Advanced eDiscovery |
| Adding remediated data to a working set | Adding remediated data to a working set refer to jobs created when erroneous files are remediated and loaded back into an Office 365 Advanced eDiscovery working set.  For more information on error remediation, see [Error remediation when processing data](error-remediation.md). | Advanced eDiscovery |
| Comparing load sets | Comparing load sets allows users to inspect the differences between loads into working sets, for more information about load sets, see [Manage load sets](manage-load-sets.md). | Advanced eDiscovery |
| Tagging documents | Tagging documents jobs occur when multiple documents in a working set are tagged.  For more information, see [Tag documents in a working set](tagging-documents.md). | Advanced eDiscovery |
| Running analytics | Running analytics jobs refer to processing jobs including Near Duplicate Identification, Email thread analysis and Themes Analysis, for more information on analytics, see [Analyze data in a working set in Advanced eDiscovery](analyzing-data-in-working-set.md). | Advanced eDiscovery |
| Preparing data for export | Preparing data for export jobs are the result of exporting data from a working set, for more information about export, see [Export case data in Advanced eDiscovery](exporting-data-ediscover20.md). | Advanced eDiscovery |
