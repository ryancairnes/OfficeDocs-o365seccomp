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

The data an evidence set on the **Evidence** tab in an investigation in Data Investigations (Preview) is a snapshot of the search results that you collected and added to the evidence set. When you add search results to evidence, a process is triggered to extract files, metadata, and text from each item returned by the search. Then, the system builds a new index of all the data (by a process called *Advanced indexing*) and then adds the files, metadata, and text to the evidence set. The data in an evidence set is actually uploaded to an Azure blob in an Azure storage location for your organization. In other words, when your working on data in an evidence you're working on an offline copy of the data in the live service.

For any time-sensitive incidents, this allows you to quickly contain the environment by deleting data in original content locations (in the live service) while you're investigating the re-created evidence in the quarantined environment of the Azure blog. After you collect the evidence, you can review individual documents in their native format, text format, or a near-native format. Additionally, you can run queries to narrow the data by time range, file types, data owners, and other properties by using search conditions. For example, using Author, Sender, and Recipient search conditions, you can quickly examine who is involved in the data spill and determine if any data was shared with people outside of your organization. For more information about using conditions to search the data in an evidence set, see [Query the data in evidence](evidence-query.md).

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


  