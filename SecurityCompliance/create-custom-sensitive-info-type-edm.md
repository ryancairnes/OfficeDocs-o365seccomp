---
title: "Create custom sensitive information types for DLP with Exact Data Match"
ms.author: deniseb
author: denisebmsft
manager: laurawi
ms.audience: Admin
ms.topic: article
ms.service: O365-seccomp
ms.date: 04/17/2019
localization_priority: Priority
ms.collection: 
- M365-security-compliance
search.appverid: 
- MOE150
- MET150
description: "Create custom sensitive information types for DLP with Exact Data Match."
---

# Create a custom sensitive information type for DLP with Exact Data Match (EDM) (Preview)

## Overview

Read this article to create a [custom sensitive information type](custom-sensitive-info-types.md) using Exact Data Match (EDM) classification. With EDM capabilities, you can define DLP policies that detect sensitive information, such as credit card numbers, employee identification numbers, patient record details, and more, by looking for specific data values in a database. Then, when people in your organization attempt to send sensitive information that matches information in the designated database, they'll be warned or prevented from sending the email (according to how your DLP policies are configured).

EDM looks for exact matches, and not just patterns or proximity.    

> [!NOTE]
> This feature is currently in preview, and is supported for [Outlook on the web](https://support.office.com/article/Compare-Outlook-for-PC-Outlook-on-the-web-and-Outlook-for-iOS-Android-b26a7bf5-0ac7-48ba-97af-984e0645dde5) only. 

## Required licenses and permissions

During the preview program, you can try EDM if your organization has a subscription that includes DLP, such as Office 365 Enterprise E3 or Office 365 Enterprise E5. (To learn more about these subscriptions, see [Get the latest advanced features with Office 365](https://products.office.com/business/compare-more-office-365-for-business-plans).)

When EDM is released, your organization must have Office 365 Enterprise E5.

You must be a global admin, compliance administrator, or Exchange Online administrator to perform the tasks described in this article. To learn more about DLP permissions, see [Permissions](data-loss-prevention-policies.md#permissions).

## The work flow at a glance

To set up EDM capabilities, you must set up a data store, install and authorize an EDM Upload agent, 

## Part 1: Create your EDM DataStore

## Part 2: Install the EDM Upload agent

## Part 3: Authorize EDM Upload

## Part 4: Hash sensitive data

## Part 5: Upload hashed data

## Part 6: Create a sensitive type

## Part 7: Define rules using EDM

## Other methods to create a custom sensitive information type

EDM isn't the only way to create custom sensitive information types. You can also use PowerShell and the Security & Compliance Center ([https://protection.office.com](https://protection.office.com)). To learn more about those methods, see:
- [Create a custom sensitive information type in Security & Compliance Center PowerShell](create-a-custom-sensitive-information-type-in-scc-powershell.md)
- c[Create a custom sensitive information type in the Security & Compliance Center](create-a-custom-sensitive-information-type.md) 