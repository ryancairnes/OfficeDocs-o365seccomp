---
title: "Review data in evidence"
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

# Review data in evidence

**Evidence** is a snapshot of search results that you collected. When you add search results to evidence, a process is triggered to extract files, metadata, and text. Then, the system builds a new index of all the data and adds to **Evidence**. 

For any time-sensitive incidents, this allows you to quickly contain the environment by deleting data at original locations while investigating re-created evidence in a quarantined environment. Once evidence is collected, you can review individual documents in their native format, text format, or a near-native format. Additionally, you can run queries to narrow the data by time range, file types, data owners, and many other condition cards. Using Author/Sender/Recipient condition cards, you can quickly examine who are involved in the spill and if there have been any external shares. For more information, see:

  - [Query the data in evidence](evidence-query.md)

To group documents and get more assistance for your review, click **Manage evidence**. In the **Analytics** tile, click **Analyze**. This will run advanced analytics such as duplicate detection, email threading, and theme analysis. Afterwards, you can see the general themes of the data and also organize documents by email threads, exact duplicates and near duplicates to facilitate your investigation. For more information, see:

  - [Run analytics to investigate faster](run-analytics-to-investigate-faster.md)

## View documents in evidence

Data investigation (Preview) displays content via several viewers each with different purposes. The various viewers can be used by clicking on any document in **Evidence**. The viewers currently provided are:

- File metadata
- Native view
- Text view
- Annotate view
- Converted view

## File metadata

This panel can be toggled on/off to display various metadata associated with the document. Although the search results grid can be customized to display specific metadata, there are instances where scrolling horizontally can be difficult while reviewing data. The File metadata panel allows a user to toggle on a view within the viewer.

![File metadata panel
](../media/Reviewimage2.png)

## Native view

The Native viewer displays the richest view of a document. It supports hundreds of file types and is meant to display the truest to native experience possible. For Microsoft Office files, for example, the viewer leverages Office Online in order to display content such as document comments, Excel formulas, hidden rows/columns, PowerPoint notes, etc. For more information regarding the Office Online viewers, visit here \[need link\]

![Native view
](../media/Reviewimage3.png)

## Text view

The Text viewer provides a view of the extracted text of a file. It ignores any embedded images and formatting but will be a very performant view if a user is trying to understand the content quickly. Text view also includes other features:

  - Line counter makes it easier to reference specific portions of a document

  - Search hit highlighting that will highlight terms within the document as well as the scrollbar

  - Diff view provides a comparison view that highlights textual differences when viewing Near Duplicate documents

![Text view
](../media/Reviewimage4.png)

![Diff view
](../media/Reviewimage5.png)

## Annotate view

The Annotate view provides features that allow users to apply markup on a document during investigation including:

  - Area redactions – users can draw a box on the document in order to hide sensitive content

  - Pencil – users can free-hand draw on a document in order to bring attention to certain portions of a document

  - Select annotations - users can select annotations on a document in order to delete

  - Toggle annotation transparency – makes annotations semi-transparent in order to view the content behind the annotation

  - Previous page – navigates to previous page

  - Next page – navigates to the next page

  - Go to page – user can enter a specific page number to navigate to

  - Zoom – set zoom level for annotate view

  - Rotate – user can rotate document clockwise

  - Search – user can search within a document and navigate to the various hits within the document
    
    ![Annotate view
    ](../media/Reviewimage1.png)

Note that these annotations are on data collected as evidence, not at its original location in live system. 

## More information

The following table lists the limits for evidence in Data Investigations (Preview).  Any items that exceed the single file maximums will show up as processing errors.
    
  |**Description of limit**|**Limit**|
  |:-----|:-----|
  |Maximum number of evidence collections  <br/> |50  <br/> |
  |Total number of documents that can be ingested into a case (for all evidence collections in the investigation)  <br/> |1 million  <br/> |
  |Total file size per load  <br/> |100 GB  <br/> |
  |Maximum size of single file   <br/> |100 MB  <br/> |
  |Maximum number of characters extracted from a single file  <br/> |10 million  <br/> |
  |Depth of embedded items in a document  <br/> |25  <br/> |
  