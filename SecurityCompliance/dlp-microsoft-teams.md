---
title: "Data loss prevention and Microsoft Teams"
ms.author: deniseb
author: denisebmsft
manager: laurawi
ms.date: 04/18/2019
ms.audience: ITPro
ms.topic: conceptual
ms.service: O365-seccomp
localization_priority: Normal
ms.collection: 
- M365-security-compliance
search.appverid: 
- MET150
description: "You can now apply DLP policies to Microsoft Teams chats and channels. Read this article to learn more about how it works."
---

# Data loss prevention and Microsoft Teams

Recently, DLP capabilities were extended to include Microsoft Teams as a location. Now, if your organization has DLP, you can set policies to prevent people from sharing sensitive information in a Microsoft Teams channel or chat session. Read this article to get an overview of how this works, and then either edit your existing DLP policies to include Microsoft Teams, or define new policies.

## How it works

## Example 1: Protecting sensitive information in channels and chats

Suppose that someone attempts to share sensitive information in a Teams chat or channel with guests (external users). If you have a DLP policy defined to prevent this, messages with sensitive information that are sent to external users are deleted. This happens automatically, and within seconds, according to how your DLP policy is configured.

## Example 2: Protecting sensitive information in documents shared in channels and chats

Suppose that someone attempts to share a document with guests, and the document contains sensitive information. If you have a DLP policy defined to prevent this, the document won't open for those users. Note that in this case, you must have a policy defined for Microsoft Teams, SharePoint, nad OneDrive in order for protection to be in place.



Policy tips notify senders about why their messages were blocked or revoked. For example, a sender might be told that their message contains personally identifiable information (PII) that is not allowed to be shared with anyone, or that a document that contains PII cannot be shared with people outside their organization. The sender can then edit their message to be compliant with DLP policies.