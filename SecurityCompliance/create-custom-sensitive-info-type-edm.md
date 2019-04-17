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

Here's the overall process for setting up DLP policies that use EDM:
 
LIST GOES HERE

## Part 1: Set up your tabular data source for EDM

During this phase, you structure your sensitive data in a .csv (or .tsv) file, create a .xml file to define its schema, and use PowerShell to refer to the schema.

1. Structure the sensitive data you want to use for EDM in a .csv (or .tsv) file. Make sure the first row of the .csv (or .tsv) file includes the names of the fields you'll use for EDM. For example, you might have field names, such as `id`, `firstname`, `lastname`, and so on.

    - You can include up to one million rows of sensitive data across all data sources.
    - You can have up to 32 fields per data source.
    - You can have up to five indexed columns per data source.
    - Data refresh should not occur more frequently than weekly (during preview).

2. Set up a .xml file that represents the schema for the data in your .csv file. Name this file `edm.xlm`. As an example, the following .xml file defines the schema for our example SampleDataStore database.
    
    ```
    <?xml version="1.0" encoding="utf-8"?>
    <EdmSchema xmlns="http://schemas.microsoft.com/office/2018/edm">
      <DataStore name="SampleDataStore" description="Sample Datastore" version="1">
        <Field name="id" unique="true" searchable="true" />
        <Field name="firstname" unique="false" searchable="true" />
        <Field name="lastname" unique="false" searchable="false" />
        <Field name="title" unique="false" searchable="false" />
        <Field name="dob" unique="false" searchable="false" />
        <Field name="creditcard" unique="false" searchable="true" />
        <Field name="ssn" unique="false" searchable="true" />
      </DataStore>
    </EdmSchema>
    ```

3. [Connect to Exchange Online Protection PowerShell](https://docs.microsoft.com/powershell/exchange/exchange-eop/connect-to-exchange-online-protection-powershell?view=exchange-ps), replacing `https://ps.protection.outlook.com/powershell-liveid` with `https://ps.compliance.protection.outlook.com/powershell-liveid`.

3. Run the following cmdlets, one at a time:

    `$edmSchemaXml=Get-Content .\edm.xml -Encoding Byte -ReadCount 0`

    `New-DlpEdmSchema -FileData $edmSchemaXml`

## Part 2: Install and authorize the EDM Upload agent

EDM Upload Agent should have
o	Read access to the file with Lookup data (csv).
o	Write access to location for storing hashed data. 
o	Access to Microsoft Azure Service and ability to write to Azure Storage Blob.  <<Could we add more specific pointers here?>> 

1. Go to [https://WHATGOESHERE](https://WHATGOESHERE) and download the EDM Upload Agent (EdmUploadAgent)

## Part 3: Hash the sensitive data and upload it

-	Hash and upload
o	Hash and upload steps could be separated and deployed in two separate servers.
o	Enables limiting access for sensitive data server handling hashing.



## Part 4: List uploaded data and sessions




## Part 6: Create a sensitive type

## Part 7: Define rules using EDM

## Other methods to create a custom sensitive information type

EDM isn't the only way to create custom sensitive information types. You can also use PowerShell and the Security & Compliance Center ([https://protection.office.com](https://protection.office.com)). Each method has its advantages and limitations. To learn more, see:
- [Create a custom sensitive information type in Security & Compliance Center PowerShell](create-a-custom-sensitive-information-type-in-scc-powershell.md)
- c[Create a custom sensitive information type in the Security & Compliance Center](create-a-custom-sensitive-information-type.md) 