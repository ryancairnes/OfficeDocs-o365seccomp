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

Here's a list of the jobs (which are typically long-running processes) that are tracked on the **Jobs** tab of a case in Advanced eDiscovery (Preview). These jobs are triggered by user actions when using and managing cases.

| Job type           | Description     |
| :----------------- | :----------     |
|Adding data to a working set | A user adds the results of a search to a working set.  For more information, see [Add search results to a working set](add-data-to-working-set.md). |
|Adding data to another working set | A user adds documents from one working set to a different working set in the same case.|
|Adding non-Office 365 data to a working set | A user uploads non-Office 365 data to a working set. The data is also indexed during this process. For example, files from an on-premises file server or a client computer are uploaded to a working set. For more information, see [Load non-Office 365 data into a working set](load-non-office365-data.md).| 
|Adding remediated data to a working set | Data with processing errors are remediated and loaded back into a working set. For more information, see [Error remediation when processing data](error-remediation.md). | 
|Comparing load sets | A user looks at the differences between different load sets in a working sets. A load set is an instance of adding data to a working set. For example, if you add the results of two different searches to the same working set, each would represent a load set. For more information, see [Manage load sets](manage-load-sets.md). |
|Converting redacted documents to PDF|After a user annotates a document in a working set and redacts a portion of it, they can choose to convert the redacted document to a PDF file. This ensures that the redacted portion will not be visible if the document is exported for presentation. For more information, see [View documents in a working set](annotating-and-redacting-documents.md). |
|Estimating search results | After a user creates and runs a new search (or re-runs an existing search) the search tool searches the index for items that match the search query and prepares a estimate that includes the number and total size of all items by the search, and the number of data sources searched.  For more information, see [Collect data for a case](collecting-data-for-ediscovery.md). | 
|Preparing data for export | A user exports documents feom a from a working set. When the export process is complete, they can download the exported data to a local computer. For more information, see [Export case data](exporting-data-ediscover20.md). | 
|Preparing for error resolution |When a user selects a file and creates a new error remediation in the Error view on the **Processing** tab of a case, the first step in the process is to upload the file that has the processing error to an Azure storage location in the Microsoft cloud. This job tracks the progress of the upload process. For more information about the error remediation workflow, see [Error remediation when processing data](error-remediation.md). | 
|Preparing search preview | After a  user creates and runs a new search (or re-runs an existing search), the search tool prepare a sample subset of items (that match the search query) that can be previewed. Previewing search results help you determine the effectiveness of the search.  For more information, see [Collect data for a case](collecting-data-for-ediscovery.md#view-search-results-and-statistics). | 
|Re-indexing custodian data | When you add a custodian to a case, all partially indexed items in the custodian's selected data sources are re-indexed by a process called *Advanced indexing*. This job is also triggered when you click **Update index** in Index view on the **Processing** tab of a case. For more information, see [Advanced indexing of custodian data](indexing-custodian-data.md).
|Running analytics | A user analyzes data in a working set by running Advanced eDiscovery analytics tools such as near duplicate detection, email threading analysis, and themes analysis. For more information, see [Analyze data in a working set](analyzing-data-in-working-set.md). | 
|Tagging documents | This job is triggered when a user clicks **Start tagging job** in the **Tagging panel** when reviewing documents in a working set. A user can start this job after tagging documents in a working set and then bulk-selecting them in the view document panel. For more information, see [Tag documents in a working set](tagging-documents.md). | 
|||
