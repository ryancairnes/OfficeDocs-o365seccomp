---
title: "Review the data in evidence"
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

# Review the data in evidence

The data in an evidence set in a data investigation is a snapshot of the search results that you collected and added to the evidence set. When you add search results to evidence, a process is triggered to extract files, metadata, and text from the items returned by the search. Then the Data Investigations (Preview) tool then builds a new index (by a process called *Advanced indexing*) of all the data and adds to an evidence set on the **Evidence** tab. 

For time-sensitive investigations, this allows you to quickly contain the environment by deleting the actual spilled or malicious data located in the at original data source, while at the same time allowing you to investigate the re-created evidence in a quarantined environment, which in this case is the data copied to the evidence set). After the evidence is collected and added to the evidence set, you can review individual documents in their native format, text format, or a near-native format that you can use to annotate and redact documents. Additionally, you can run queries to narrow the data set by time range, file types, data owners, and many other properties and search conditions. For example, by using the Author, Sender, or Recipient conditions, you can quickly identify the people are involved in the incident and if any data from your organization has been shared with external users. For more information about searching through data in an evidence set, see [Query the data in evidence](evidence-query.md).

To group documents and get more assistance for your review, select an evidence set on the **Evidence** tab, and then click **Manage evidence**. In the **Analytics** tile, click **Rebuild analytics for the whole set**. This will run advanced analytics such as duplicate detection, email threading, and theme analysis. Afterwards, you can see the general themes of the data and also organize documents by email threads, near duplicates, and exact duplicates and to help your investigation. For more information, see [Run analytics to investigate faster](run-analytics-to-investigate-faster.md).

## View documents in evidence

Data Investigations (Preview) allows you to display content in several different viewers, with each viewer having a different purpose. These viewers are:

- File metadata
- Native view
- Text view
- Annotate view

To access any of these viewers, just select a document in an evidence set.

## File metadata

This view displays various metadata associated with the selected document. You can toggle this view on and off by clicking **File metadata**. Although the search results grid can be customized to display specific metadata, there are instances where scrolling horizontally can be difficult while reviewing documnts. The **File metadata** view allows you change between the different viewers when reviewing a document.

Here's an example of the file metadata for a document. For more information about the metadata fields, see [Document metadata fields in Data Investigations (Preview)](document-metadata-fields.md).

![File metadata panel](../media/Reviewimage2.png)

## Native view

The Native viewer displays the richest view of a document. It supports hundreds of file types and is meant to display documents in the truest native experience possible. For Microsoft Office files, the Native viewer uses Office Online. This allows you to view content such as document comments, formulas and hidden rows/columns in Excel, and PowerPoint notes.

![Native view
](../media/Reviewimage3.png)

## Text view

The Text viewer provides a view of the extracted text of a file. It ignores any embedded images and formatting but it's very useful if you're trying to quickly review and understand the content in a document. Text view also includes these features:

  - A line counter makes it easier to reference specific portions of a document.

  - Search hit highlighting will highlight terms in the document as well as on the scrollbar

  - A diff view provides a comparison view that highlights the textual differences when viewing documents using the Near duplicates panel.

![Text view
](../media/Reviewimage4.png)

![Diff view
](../media/Reviewimage5.png)

## Annotate view

The Annotate view provides features that allow you to apply markup on a document during investigation including:

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


  