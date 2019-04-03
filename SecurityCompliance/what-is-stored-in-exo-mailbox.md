---
title: "Content stored in Exchange Online mailboxes"
ms.author: markjjo
author: markjjo
manager: laurawi
ms.audience: Admin
ms.topic: article
ms.service: O365-seccomp
localization_priority: Normal
ms.collection: M365-security-compliance
search.appverid:
- MOE150
- MED150
- MET150
ms.assetid: 
description: ""
---

# Content stored in Exchange Online mailboxes

A mailbox in Exchange Online is primarily used to store email-related items such as messages, calendar items, tasks, and notes. But that's changing as more Office 365 apps also store their data in a user's cloud-based Exchange mailbox. One advantage of storing data in a mailbox is that Microsoft compliance tools such as eDiscovery, archiving, and retention policies can used to find, store, and retain data from these other apps in the Microsoft cloud.

 The following table lists the Office 365 apps that store data in a mailbox. The table also describe the type of content that each app stores in a mailbox.

|Office 365 app  |Description  |
|:---------|:---------|
|Forms     <br/> |         <br/> |
|MyAnalytics    <br/> |         <br/> |
|Office 365 Groups    <br/>|  Email messages, calendar items, contacts (People), notes, and tasks are stored in the mailbox that's associated with an Office 365 group.       <br/> |
|Outlook/Exchange Online<br/>|  Email messages, calendar items, contacts (People), notes, and tasks are stored in a user's mailbox.       <br/> |
|People    <br/> |  Contacts in the People app (which are the same contacts as the ones accessible in Outlook) are stored in a user's mailbox.      <br/> |
|Planner     <br/> |         <br/> |
|Skype for Business    <br/>  | Conversations in Skype for Business are stored in the Conversation History folder in a user's mailbox. If the mailbox of a participant of a Skype meeting is placed on Litigation Hold or assigned to a retention policy, files attached to a meeting are retained in the participants mailbox.         <br/> |
|Sway     <br/> |         <br/> |
|Tasks    <br/> |  Tasks in the Tasks app (which are the same tasks as the ones accessible in Outlook) are stored in a user's mailbox.       <br/> |
|Teams    <br/>  |Conversations that are part of a Teams channel are stored in the mailbox that's associated with the Team. Conversations that are part of the Chat list in Teams (also called *1 x N chats*) are stored in the mailbox of the users who participate in the chat. Additionally, summary information for meetings and calls in a Teams channel are stored in the mailboxes of users who dialed into the meeting or call. <br/> | 
|To-Do  <br/> | Tasks (called *to-dos*, which are saved in to-do lists) in the To-Do app are stored in a user's mailbox.        <br/> |
