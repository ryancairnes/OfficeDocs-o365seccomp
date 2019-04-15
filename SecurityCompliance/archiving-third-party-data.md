---
title: "Archive third-party data in Office 365"
ms.author: markjjo
author: markjjo
manager: laurawi
ms.date: 
ms.audience: Admin
ms.topic: article
ms.service: O365-seccomp
localization_priority: Normal
ms.collection: 
- Strat_O365_IP
- M365-security-compliance
search.appverid: MOE150
ms.assetid: 0ce338d5-3666-4a18-86ab-c6910ff408cc
description: "Administrators can import third-party data from  social media platforms, instant messaging platforms, and document collaboration platforms to mailboxes in your Office 365 organization. This lets you archive data from Facebook, Twitter, and other third-party data sources in Office 365. Then you can apply Office 365 compliance features (such as legal hold, content search, and retention policies) to third-party data."
---

# Archive third-party data in Office 365

Office 365 lets administrators import and archive third-party data from social media platforms, instant messaging platforms, and document collaboration platforms, to mailboxes in your Office 365 organization. Examples of third-party data sources that you can import to Office 365 include the following: 
  
- **Social** - Twitter, Facebook, Yammer, and LinkedIn 
    
- **Instant messaging** - Yahoo Messenger, GoogleTalk, and Cisco Jabber 
    
- **Document collaboration** - Box and DropBox 
    
- **Vertical industries** - Customer Relationship Management (such as Salesforce Chatter) and Financial Services (such as Bloomberg and Thomson Reuters) 
    
- **SMS/text messaging** - BlackBerry 
    
After third-party data is imported, you can apply Office 365 compliance features—such as Litigation Hold, Content Search, In-Place Archiving, Auditing, and Office 365 retention policies—to this data. For example, when a mailbox is placed on Litigation Hold, third-party data will be preserved. You can search third-party data by using Content Search. Or you can apply archiving and retention polices to third-party data just like you can for Microsoft data. In short, archiving third-party data in Office 365 can help your organization stay compliant with government and regulatory policies.

There are two ways to import and archive third-party data in Office 365:

- **Use a third-party data connector in the Security & Compliance Center** - Use a third-party data connector that's built in to the Security & Compliance Center in Office 365. After you set up and configure a built-in connector, it connects to the third-party data source, converts the content of an item to an email message format, and then imports the item to mailboxes in Office 365. For the third-party data sources supported by built-in connectors and the step-by-step process to set up a connector, see [Use a built-in connector to archive third-party data in Office 365](archive-third-party-data-with-builtin-connector.md).

- **Work with a Microsoft partner** - Your organization works with a Microsoft Partner who will provide a custom connector that will be configured to extract items from the third-party data source (on a regular basis) and then connect to the Microsoft cloud by a third-party API and import those items to Office 365. The partner connector also converts the content of an item from the third-party data source to an email message and then imports them to a mailbox in Office 365. For a list of partners that you can work with and the step-by-step process for this method, see [Work with a partner to archive third-party data in Office 365](work-with-partner-to-archive-third-party-data.md).