---
title: "Set up smart tags for attorney-client privilege detection in Advanced eDiscovery"
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
ROBOTS: NOINDEX, NOFOLLOW 

description: ""
---

# Set up smart tags for ML-assisted review in Advanced eDiscovery

## Overview
Machine learning capabilities in Advanced eDiscovery are meant to help make decision process on documents more efficient. Smart tags is a way to bring the machine learning capabilities into where the decisions are recorded: tags and tag groups. When you create a smart tag group, then the decisions of the ML model mapped to the group will be shown in-line with the tags in the group to help you see the information in-line, where they contextually make most sense.

## How to set up a smart tag group
1. In a review set, go to **Manage review set** -> **Manage tags**.
2. Click on the drop-down next to **Add tag group** and select **Add smart tag group**.
3. Select the model you want to map to this group. This will create a tag section and N child tags, where N is the number of possible outputs of the model. For instance, attorney-client privilege detection model has two possible outputs - privileged and not privileged; selecting this model will create two child tags in the review set, each corresponding to one of the possible outputs.
4. Rename the tag group and tags as you see fit.

## How to use a smart tag group
When reviewing a document, the model's results will be exposed next to the appropriate tag value. For instance, if you have a smart tag group for attorney-client privilege detection and you review a document that the model has decided is potentially previleged, you will see the reason for that next to the appropriate tag. It is important to note that the tag is not automatically applied; for all intents and purposes, tags within a smart tag group act just like normal tags, except that they expose the model results next to them when appropriate.