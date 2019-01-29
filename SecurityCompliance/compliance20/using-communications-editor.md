---
title: "Using the communications editor"
ms.author: markjjo
author: markjjo
manager: laurawi
ms.date: 
ms.audience: Admin
ms.topic: article
ms.service: o365-administration
localization_priority: Normal
ms.collection: 
search.appverid: 
- MOE150
- MET150
ms.assetid: 

description: ""
---

# Using the Communications Editor
As you define the content of your portal content, legal hold notifications, and related reminders/escalations, you can leverage the Communications Editor to format and dynamically customize your content.

## Rich-Text Editor 

The Communications Editor allows user to customize the text using the editor options. For example, users can change font types, create bulleted lists, highlight content, and more. 

<<include screenshot>>

## Merge Field Variables

You can leverage email merge variables from the Communications Editor to embed customized custodian attributes into a communication's body text. When sent to the custodian, the merge field will be populated with the corresponding field. For example, when sent to custodian John Smith, the merge field [Custodian Name] would be translated with the corresponding name. 

You can use email merge fields by selecting the **Merge Field** icons on the top of the rich-text editor control. The placeholder will be added based off the location of the users' cursor. 

### List of Merge Field Variables
| Field Name                  | Field Details | 
| :------------------- | :-------------------: |
| Display Name  | Custodian's first and last name | 
| Acknowledgement Link                 | Customized link to record each custodian's acknowledgement                 |
| Portal Link     | Customized link for the custodian's Compliance Portal                 |
| Issuing Officer                   | Email address of the specified issuing officer                   |
| Issuing Date                   | date that the notice was issued (UTC)              |