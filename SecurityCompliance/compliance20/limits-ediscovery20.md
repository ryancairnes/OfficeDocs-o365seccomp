---
title: "Advanced eDiscovery limits"
ms.author: markjjo
author: markjjo
manager: laurawi
audience: Admin
ms.topic: article
ms.service: O365-seccomp
localization_priority: Normal
ms.collection: M365-security-compliance 
search.appverid: 
- MOE150
- MET150
description: ""
---

# Limits in Advanced eDiscovery

This article describes the limits in Advanced eDiscovery.

## Case limits

The following table lists the limits for cases in Advanced eDiscovery.

|**Description of limit**|**Limit**|
  |:-----|:-----|
  |Total number of documents that can be added to a case (for all review sets in the case).  <br/> |1 million  <br/> |
  |Total file size per load set.  <br/> |100 GB  <br/> |
  |Daily case load   <br/> |2 TB <br/> |
  |Loads per case.  <br/> |15 <br/> |
  |Review sets in a case.  <br/> |20 <br/> |
|||


## Indexing limits

The following table lists the indexing limits in Advanced eDiscovery.

|**Description of limit**|**Limit**|
  |:-----|:-----|
  |Maximum number of characters extracted from a single file.  <br/> |10 million <sup>1</sup> <br/> |
  |Maximum size of single file.   <br/> |100 MB <sup>1</sup> <br/> |
  |Maximum depth of embedded items in a document.  <br/> |25 <sup>1</sup> <br/> |
  |OCR file size.  <br/> |24 MB <sup>1</sup> <br/> |  
|||
## Search limits

|**Description of limit**|**Limit**|
  |:-----|:-----|
  |Characters per search.  <br/> |Mailbox: 10,000; Sites: 4,000 when searching all sites or 2,000 when searching up to 20 sites  <br/> |
  |Variants returned when using prefix wildcard to search for an exact phrase in a search or when using a prefix wildcard and the "NEAR" or "ONEAR" Boolean operator.  <br/> |10,000  <br/> |
  |Minimum number of alpha characters for preefix wildcards.  <br/> |3  <br/> |
  |Keywords per workload search.  <br/> |20  <br/> |
  |Mailboxes or sites per workload search.  <br/> |No limit  <br/> |
  |Simultaneous workload searches.  <br/> |No limit  <br/> |
  |Number of workload searches started by a single userKeywords per workload search.  <br/> |10  <br/> |
  |Items per mailbox in workload search preview.  <br/> |100  <br/> |
  |Items across all mailboxes per workload search preview.  <br/> |1000  <br/> |
  |Mailboxes per worload search preview.  <br/> |1000  <br/> |
  |SharePoint and OneDrive for Business items per site for workload search preview.  <br/> |200  <br/> |
  |SharePoint and OneDrive for Business sites per workload search preview.  <br/> |200  <br/> |
  |Public folder mailbox items per workload search preview.  <br/> |100  <br/> |
  |Items across all public folder mailbox per workload search preview.  <br/> |200  <br/> |
  |Public folder mailboxes per workload search preview.  <br/> |500  <br/> |
|||


## Viewer limits

|**Description of limit**|**Limit**|
  |:-----|:-----|
  |Excel files in native viewer.  <br/> |4 MB  <br/> |
|||


## Review set download limits

|**Description of limit**|**Limit**|
  |:-----|:-----|
  |Download action in a review set.  <br/> |3 MB or 50 files  <br/> |
|||

 > [!NOTE]
> <sup>1</sup> Any item that exceeds a single file limit will show up as a processing error. 
