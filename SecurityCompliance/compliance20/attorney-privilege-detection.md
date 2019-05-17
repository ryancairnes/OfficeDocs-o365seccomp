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

# Set up attorney-client privilege detection in Advanced eDiscovery

A major and costly aspect of the review phase of any eDiscovery process is reviewing documents for privileged content. Advanced eDiscovery provides machine learning-based detection of privileged content to make this process more efficient. This feature is called *attorney-client privilege detection*.

> [!NOTE]
> attorney-client privilege detection in Advanced eDiscovery is in Preview. You must opt-in before you can use it.

## How does it work?

When attorney-client privilege detection is enabled, all documents in a review set will be processed by the attorney-client privilege detection model when you [ analyze the data](analyzing-data-in-review-set.md) in the review set. The model looks for two things:

- **Privileged content** - The model uses machine learning to determines the likelihood that the document contains content that is legal in nature.

- **Participants** - As part of setting up attorney-client privilege detection, you have to submit a list of attorneys for your organization. The model then compares the participants of the document with the attorney list to determine if a document has at least one attorney participant.

The model produces the following three properties for every document (and adds these *property:value* pairs to the document metadata):

- **Content score** - The likelihood the document is legal in nature; the values for the score are between **0** and **1**.

- **Has Attorney** - This property is set to **True** if one of the document participants is listed in the attorney list; otherwise the value is **False**. The value is also set to **False** if your organization didn't upload an attorney list.

- **Potentially Privileged** - This property is set to **True** if the **Content score** value is above threshold *or* if the document has an attorney participant; otherwise, the value is set to **False**.

The three previous values are searchable within a review set. For more information, see [Query the data in a review set](review-set-search.md).

## Set up the attorney-client privilege detection model

To enable the attorney-client privilege detection module, your organization has to opt-in and then upload an attorney list.

### Step 1: Opt-in to attorney-client privilege detection

As previously stated, the attorney-client privilege detection model is in Preview. Therefore a person in your organization eDiscovery Administrator (a member of the eDiscovery Administrator subgroup in the eDiscovery Manager role group) must to opt in to make the model available in your Advanced eDiscovery cases.

1. In the Security & Compliance Center, go to **eDiscovery > Advanced eDiscovery**.

2. On the **Advanced eDiscovery** home page, click the **Configure experimental features** tile.

3. Click **Manage attorney-client privilege detection**.

4. Click the toggle to turn on the feature.

### Step 2: Upload a list of attorneys (optional)

In take full advantage of the attorney-client privilege detection model, we recommend that you provide a list of email addresses for the lawyers and legal personnel who work for your organization. To do this, create a .csv file (without a header row) and then add the email address for each person on a separate line.

## Use the attorney-client privilege detection module

Follow the steps in this section use attorney-client privilege detection for documents in a review set.

### Step 1: Analyze a review set

When you analyze the documents in a review set, the attorney-client privilege detection model will also be run. For more information about analyzing data in review set, see [Analyze data in a review set in Advanced eDiscovery](analyzing-data-in-review-set.md).

### Step 2: Create a smart tag group with attorney-client privilege detection model

One of the primary ways to see the results of attorney-client privilege detection in your review process is by using a smart tag group. A smart tag group indicates the results of the attorney-client privilege detection and shows the results in-line next to the tags in a smart tag group. This lets you quickly identify potentially privileged documents during document review. Additionally, you can also use the tags in the smart tag group to tag documents as privileged or non-privileged. For more information about smart tags, see [Set up smart tags in Advanced eDiscovery](smart-tags.md).

1. In the review set that contains the documents that you analyzed in Step 1, click **Manage review set** and then click **Manage tags**.
 
2. Under **Tags**, click the pull-down next to **Add group** and then click **Add smart tag group**.

3. On the **Choose a model for your smart tag** page, click **Select** next to **Attorney-client privilege**.

   A tag group named **Attorney-client privilege** is displayed. It contains two child tags named **Positive** and **Negative**, which correspond to the possible results of the model.

3. Rename the tag group and tags as appropriate for your review. For example, you can rename **Positive** to **Privileged** and **Negative** to **Not privileged**.

### Step 3: Use the smart tag group for privilege review

When you review a document, if the model has determined that the document is potentially privileged, the corresponding smart tag will expose the result:

- If the document has content that may be legal in nature, the label **Legal content** is displayed next to the corresponding smart tag (which in this case is the default **Positive** tag).

- If the document has a participant that is found in your organization's attorney list, the label **Attorney** is displayed next to the corresponding smart tag (which in this case is also the default **Positive** tag).