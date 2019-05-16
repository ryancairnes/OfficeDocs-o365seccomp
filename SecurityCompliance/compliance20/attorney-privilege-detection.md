---
title: "Set up attorney-client privilege detection in Advanced eDiscovery"
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

# Set up attorney-client privilege detection in Advanced eDiscovery

A major and costly aspect of the review phase of any eDiscovery process is reviewing documents for privileged content. Advanced eDiscovery provides machine learning-based detection of privileged content to make this process more efficient. This feature is called *attorney-client privilege detection*.

> [!NOTE]
> Attorney-client privilege detection in Advanced eDiscovery is in Preview. You must opt-in before you can use it.

## How does it work?

When attorney-client privilege detection is enabled, all documents in a review set will be processed by the attorney-client privilege detection model when you [ analyze the data](analyzing-data-in-review-set.md) in the review set. The model looks for two things:

- **Privileged content** - The model uses machine learning to determines the likelihood that the document contains content that is legal in nature.

- **Participants** - As part of setting attorney-client privilege detection, you have to submit a list of attorneys for your organization. The model then compares the participants of the document with the attorney list to determine if a document has at least one attorney participant.

The model outputs the following three values for every document; all of values are searchable within a review set.

- **Content score** - The likelihood of the document being legal in nature (score between 0 and 1).

- **Has Attorney** - Set to **True** if one of the document participants is listed in the attorney list; otherwise the value is **False**. Note that the value is also **False** if your organization didn't upload an attorney list.

- **Potentially Privileged** - Set to **True** if the **Content score** value is above threshold *or* it the document has an attorney participant; otherwise, the value is set to **False**.

The three previous values are searchable within a review set. For more information, see [Query the data in a review set](review-set-search.md).

## Set up the attorney-client privilege detection model

### Step 1: Opt into Attorney-client privilege detection (eDiscovery Admin)

Because Attorney-client privilege detection is in Preview, your eDiscovery Administrator needs to opt in to make the feature available in your cases.

- Go to "Configure experimental features" from Advanced eDiscovery page

- Click on "Manage Attorney-Client Privilege detection".

- Click on the toggle to turn the feature on.

### Step 2: Upload a list of attorneys (optional)

In order to take full advantage of attorney-client privilege detection we recommend providing a list of email addresses lawyers or legal personas who work for the company. The list should be a header-less CSV, with one email address per line.

## Leveraging attorney-client privilege detection 

### Step 1: Analyze a review set

When you analyze your review set, attorney-client privilege detection will be run as well. To learn more about analyzing data in review set, please refer to [Analyze data in a review set in Advanced eDiscovery](analyzing-data-in-review-set.md).

### Step 2: Create a smart tag group with attorney-client privilege detection model

One of the main ways you can consume the results of attorney-client privilege detection in your review process is by using a smart tag group. Smart tag groups take the results of an ML model and show the results of the model in-line next to the tags, so that you can easily consume the results of the model where relevant, and use the tags in your review process as you would any other tags in your tagging panel. Please refer to [Set up smart tags for ML-assisted review in Advanced eDiscovery](smart-tags.md) for more information.

- In "Manage tags", click on "Add smart tag section".

- Select "Attorney-client privilege detection". You will see that a tag group and two tags, corresponding to the possible results of the model, have been created.

- Rename the tag group and tags as you see fit for your review.

### Step 3: Use the smart tag group for privilege review

When you review a document, if the model has determined that the document is potentially privileged, the corresponding smart tag will expose the result:

- If the document has content that may be legal in nature, a "Legal content" label will appear next to the corresponding smart tag.

- If the document has a participant that is found in the uploaded attorney list, an "Attorney" label will appear next to the corresponding smart tag.