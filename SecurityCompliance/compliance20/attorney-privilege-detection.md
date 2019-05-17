---
title: "Set up attorney-client privilege detection in Advanced eDiscovery"
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

# Set up attorney-client privilege detection (preview) in Advanced eDiscovery

A major and costly aspect of the review portion of any discovery process is reviewing for privileged content. Advanced eDiscovery provides an AI-based detection of privileged content in your case so that you can make this process more efficient. As this feature is currently in beta, an eDiscovery Administrator has to opt into the feature to use it.

## How does it work?

With the feature turned on, when you analyze a review set within a case, all documents run through the attorney-client privilege detection model. The model looks at two things:

- Content: the ML model determines the likelihood of the document's content being legal in nature.

- Participants: if there is a user-uploaded list of attorneys for the tenant, the model compares the participants of the document against the list to determine whether the document has at least one attorney participant.
The model outputs three values for every document, all of which will be searchable within a review set:

- Content score: the likelihood of the document being legal in nature (score between 0 and 1)

- Has Attorney: True if one of the participants is found in the uploaded attorney list, false otherwise, or if there is no attorney list.

-  Potentially Privileged: True if content score is above threshold or has an attorney participant, false otherwise.

## Opting into Attorney-client privilege detection

### Step 1: Opt into Attorney-client privilege detection (eDiscovery Admin)

Because Attorney-client privilege detection is a preview feature, your eDiscovery Administrator needs to opt in to make the feature available in your cases.

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