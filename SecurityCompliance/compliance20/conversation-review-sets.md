---
title: "Conversation review sets"
ms.author: markjjo
author: markjjo
manager: laurawi
ms.date: 
audience: Admin
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

# Review Conversations in Advanced eDiscovery 

## Overview
Instant messaging is a convenient way to ask questions, share ideas, or quickly communicate across large audiences. As instant messaging platforms, like Microsoft Teams, become core to enterprise collaboration, organizations must evaluate how their eDiscovery workflow will address these new forms of communication and collaboration. 

Conversation Reconstruction from Advanced eDiscovery is designed to help you identify contextual content and produce distinct conversation views, allowing for efficient and rapid review of instant messaging platforms like Microsoft Teams. 
With Conversation Reconstruction, users can leverage built-in capabilities to reconstruct, review, and export threaded conversations. Use Advanced eDiscovery Conversation Reconstruction to:
  1. Preserve unique message-level metadata across all messages within a conversation
  2. Collect contextual messages around your search results
  3. Review, annotate, and redact threaded conversations
  4. Export individual messages or threaded conversations

## Terminology
**Messages** represent the smallest unit of a conversation. Messages may vary in size, structure, and metadata. 

A **conversation** represents a grouping of one or more messages. Across different applications, conversations may be represented in different ways. In some applications, there is an explicit action of replying to existing messages and conversations are formed explicitly as a result of this user action. 
    ![Microsoft Teams Channel Conversation](../media/threadedchat.png)

In other applications, messages appear as a “flat river of messages” within a thread. Here, conversations are inferred heuristically such that there may be a ‘soft’ grouping of a set of messages representing the “back and forth” about a topic of interest.  

## Step 1: Run a search
After you have identified relevant custodians and locations, you can create a search to find potentially relevant content. On the **Searches** tab, you can create a new search by clicking ** + New search** and following the wizard.

>[!NOTE]
> For additional information on how you can create a search, build a search query, and view search results, see [Collect data for a case](create-search-to-collect-data.md).

## Step 2: Create a Review Set
Within a review set, you can search, tag, annotate, and redact documents, emails, and chat conversations. Using Advanced eDiscovery, you can tailor your review for conversations to be based off individual messages or threaded conversations.  
The mode in which you can tailor your review is based off the review set type. Advanced eDiscovery has two different types of review sets: 
  - **Traditional Review Set:** Messages are processed and displayed as individual items. 
  - **Conversational Review Set:** Messages are processed individually but displayed in a conversation view. Users in this mode can annotate, tag, and redact a threaded conversation view. 

> [!Note]
> For additional information on how you can create and manage review sets, see the section on how to [Manage Review Sets](managing-review-sets.md). 

## Step 3: Enable Conversation Retrieval Options
Once you have reviewed and finalized your search query, you can add the results into a review set. When you add your search results into a review set, the original data is copied to facilitate the review and analysis process.

>[!Note]
>For more information on adding search results to a review set, see [Add search results to a review set](add-data-to-review-set.md). 

In addition, when you add data from convsations into a review set, you can leverage the conversation retrieval options to expand your search and include contextual messages. After conversation retrieval is enabled, the following can happen:
  1. Using a keyword and date range query, the search returned a hit on *Message 3*. This message was part of a larger conversation, illustrated by *CRC1*. 
  2. When the user adds the data into a review set and enables the conversation retrieval options, the system will go back and collect other items in *CRC1*. 
  3. After the items have been added into a review set, the user can review all the individual messages from *CRC1*. 

    ![Conversation Retrieval](../media/messagesandconversations.png)

### To enable conversation retrieval:
  1. Navigate to the **Searches** tab.
  2. Select a search and then click **+ Add to Review Set**.
  3. Select an existing review set or create a new review set. 
    > [!Note]: 
    > For more information on the different kinds of review sets, see the section on [Managing Review Sets](managing-review-sets.md).
  4. Ensure that you have enabled conversation retrieval for the sources that you would like to expand in your search.  
  5. Once your Add to Review Set job has finished, you can go ahead and start reviewing your conversations.

## Step 4: Review Conversations
Once your content has been processed, you can start reviewing your data within a review set. The review capabilities differ depending on the review set mode.

### Traditional Review Set
In a traditional review set, messages are processed and displayed as individual items, similar to how they are stored within a mailbox. 
> [!Note] 
> In this workflow, each message is processed as a separate item. As a result, the threaded summary and export options are not available in a traditional review set. 

### Conversational Review Set
In a Conversational Review Set, individual messages are threaded together and presented as conversations. This enables users to review and export contextual conversations. 

#### Review
In a conversational review set, you can use the following options to tailor your review process: 

##### Group by Conversation
This option groups messages within the same conversation together to help users simplify and expedite their review process. 

##### Summary View
The summary view displays the threaded conversation. Here, you can view the entire conversation and also access the metadata for each individual message.  
  - View Metadata for Individual Messages
  - Download individual messages

##### Text View
The text view provides the extracted text for the entire conversation. 

##### Annotate View
The annotate view allows the user to apply markup on a threaded view of the conversation. All messages within a conversation will share the same annotated document.

##### Tag
When viewing conversations in a review set, you can view and apply tags by clicking on the Coding Panel.

##### Re-Run Conversation Conversion
When messages are added to a conversational review set, a conversion job is automatically run to create the threaded summary and annotate views. If the Conversation Reconstruction job fails, you can re-run the conversion job by navigating to ![Action](../media/Actionbutton.png) and then ![Create Conversation PDFs](../media/createconvoPDFs.png) .


#### Export
In a Conversational review set, you can leverage the following options to export conversations:

![Export](../media/export.png)

##### Metadata File
Like a “load file”, this will contain metadata for each individual message, email, and document. You will see one row for each message within a conversation. 

#####	Tags
This option will allow you to include tags from your review process in your metadata file. Messages within a conversation will share the same tag. 

#####	Content
  - **Conversation files**: When you export conversation files, the annotate view is converted into a PDF and downloaded into your export folder. Messages within one conversation file will point to the same conversation file PDF.  
  - **Individual Messages:** When you export individual messages, each unique message within the conversation is exported as a standalone item. The file is exported in the same format that it is saved within the mailbox. For a given conversation, you will receive multiple .msg files. 

  >[!Warning]
  > If you applied markups to the conversation file, these will not be transferred to the individual messages. 

##### Text Files 
Text files can be generated for each conversation exported from the review set. 

#####	Replace Exported Content with Redacted PDFs
If redacted conversation files are generated during review, these files are available during export. Users can decide whether to export native files only or to replace natives that have redactions with the burned in PDFs.

>[!Note]
>To learn more about how to review case data, check out the following resources:
> - [View Case Data](view-documents-in-review-set.md) 
> - [Analyze Case Data](analyzing-data-in-review-set.md)
> - [Export Case Data](exporting-data-ediscover20.md)
