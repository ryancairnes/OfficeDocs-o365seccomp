---
title: "Set up smart tags in Advanced eDiscovery"
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
ROBOTS: NOINDEX, NOFOLLOW 

description: ""
---

# Set up smart tags in Advanced eDiscovery

Machine learning (ML) capabilities in Advanced eDiscovery can help you make the decision process more efficient when you're reviewing case documents in a review set. Smart tags are a way to bring the ML capabilities to where the decisions are recorded: when tagging documents during review. When you create a smart tag group, then the decisions that are the result of the ML model that you've associated with the smart tag group will be displayed in-line with the tags in the tag group. This helps see the ML results information in-line when you're reviewing specific documents.

## How to set up a smart tag group

1. In a review set, click **Manage review set** and then click **Manage tags**.

2. Click **Add tag group** and then select **Add smart tag group**.

3. Select the ML model that you want to associate to the tag group. 
    
   This will create a tag group and *N* child tags, where *N* is the number of possible outputs of the model. For example, the attorney-client privilege detection model has two possible outputs: **Privileged** and **Not privileged**. If you select this model, a tag group with two child tags is created (one child tag named **Privileged** and the other named **Not privileged**) for the review set. So in this example, each child tag corresponds to one of the possible outputs from the attorney-client privilege detection model.

4. Optionally, you can rename the tag group and the child tags.

## How to use smart tags

When reviewing a document, the model's results will be exposed next to the appropriate child tag. For example, if you have a smart tag group for attorney-client privilege detection and you review a document that the model has decided is potentially privileged, you will see the reason for that conclusion displayed next to the appropriate tag. It's important to note that the tag isn't automatically applied to the document. The reviewer will make the decision about how to tag the document. Tags within a smart tag group are just like normal tags, except that the model results are displayed next to a child tag when appropriate.