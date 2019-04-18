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

The process of setting up EDM consists of five main parts:
 
LIST GOES HERE

## Part 1: Set up your tabular data source for EDM

During this phase, you structure your sensitive data in a .csv (or .tsv) file, create a .xml file to define the data file schema, and then configure Exchange Online Protection to refer to the schema.

1. Structure the sensitive data you want to use for EDM in a .csv (or .tsv) file. Make sure the first row of the .csv (or .tsv) file includes the names of the fields you'll use for EDM. For example, you might have field names, such as `id`, `firstname`, `lastname`, and so on. Keep the following limits in mind:

    - The data file can include up to one million rows of sensitive data across all data sources.
    - The data file can include up to 32 fields per data source.
    - The data file can include up to five indexed columns per data source.
    - Data refresh for each data source can occur weekly (but not more often during preview).

2. Set up a .xml file that represents the schema for your data file. Name this schema file `edm.xlm`. As an example, the following .xml file defines the schema for our example *SampleDataStore* database.
    
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

4. Run the following cmdlets, one at a time:

    `$edmSchemaXml=Get-Content .\edm.xml -Encoding Byte -ReadCount 0`

    `New-DlpEdmSchema -FileData $edmSchemaXml`

5. Proceed to Part 2.

## Part 2: Install and authorize the EDM Upload agent

During this phase, you'll set up a dedicated user account for Office 365, download and install the EDM Upload Agent, and authorize the tool.

1. Set up a user account with limited permissions for the EDM Upload Agent. (See [Add users to Office 365](https://docs.microsoft.com/office365/admin/add-users/add-users?view=o365-worldwide).) The user account you create should have:

    - Read access to your data file (This is the .csv or .tsv you created in [Part 1](#part-1-set-up-your-tabular-data-source-for-edm).)
    - Write access to the location you'll use for storing hashed data (this can be a folder on a local drive)
    - Write access to Microsoft Azure Service for [Azure Blob storage](https://docs.microsoft.com/azure/storage/blobs/storage-blobs-introduction)

2. [Download the EDM Upload Agent](http://download.microsoft.com/download/C/6/2/C62C41B6-8585-4655-9D93-EAC61042AC51/EdmUploadAgent.msi) (EdmUploadAgent.exe) and install it.

3. To authorize the EDM Upload Agent, run the following PowerShell cmdlet in Exchange Online Protection:

    `EdmUploadAgent.exe /Authorize`

4. When prompted, log in using the account credentials you created in step 1. 

5. Proceed to Part 3.

> [!TIP]
> If you get any error messages, repeat steps 3 and 4.

## Part 3: Hash the sensitive data and upload it

During this phase, you hash the sensitive data, and upload the hashed data using the EDMUploadAgent. 

> [!NOTE]
> The following procedure describes how to upload the data to a single server; however, you could use multiple servers.

1. To hash the data, run the following PowerShell cmdlet in Exchange Online Protection:

    `EdmUploadAgent.exe /CreateHash /DataStoreName <DataStoreName> /DataFile <DataFilePath> /HashLocation <HashedFileLocation>`

    Example: `EdmUploadAgent.exe /CreateHash /DataStoreName EmployeeDB /DataFile C:\Edm\Data\EmployeeData.csv /HashLocation C:\Edm\Hash` 

2. To upload the hashed data, run the following PowerShell cmdlet in Exchange Online Protection:

    `EdmUploadAgent.exe /UploadHash /DataStoreName <DataStoreName> /HashFile <HashedSourceFilePath>`

    Example: `EdmUploadAgent.exe /UploadHash /DataStoreName EmployeeDB /HashFile C:\Edm\Hash\EmployeeData.EdmHash` 

3. To see a list of uploaded data stores, run the following PowerShell cmdlet in Exchange Online Protection:

    `EdmUploadAgent.exe /GetDataStore`

    You'll see a list of data stores and when they were last updated. Here's an example:

    ![Example of GetDataStore cmdlet and results](media/EDM-GetDataStore-example.png)

4. To see a list of upload sessions for a single data store, run the following PowerShell cmdlet in Exchange Online Protection:

    `EdmUploadAgent.exe /GetSession /DataStoreName <DataStoreName>`

    For example, the cmdlet `EdmUploadAgent.exe /GetSession /DataStoreName patient` displays a list of upload sessions for the *Patient* data store.

    ![Example of EDM upload sessions for Patient data store](media/EDM-GetDataStore-sessionsexample.png)



## Part 4: Create a rule package with exact matching

During this phase, you configure exact matching and classification.

1. Create a rule package in .xml format (with Unicode encoding), similar to the follownig example:

    ```
    <?xml version="1.0" encoding="utf-8"?>
    <RulePackage xmlns="http://schemas.microsoft.com/office/2018/edm">
      <RulePack id="fd098e03-1796-41a5-8ab6-198c93c62b11">
        <Version build="0" major="2" minor="0" revision="0" />
        <Publisher id="eb553734-8306-44b4-9ad5-c388ad970528" />
        <Details defaultLangCode="en-us">
          <LocalizedDetails langcode="en-us">
            <PublisherName>Microsoft EDM</PublisherName>
            <Name>Health care EDM Rulepack</Name>
            <Description> This rule package contains the EDM sensitive types for health care.</Description>
          </LocalizedDetails>
        </Details>
      </RulePack>
      <Rules>
        <ExactMatch id = "E1CC861E-3FE9-4A58-82DF-4BD259EAB371" patternsProximity = "300" dataStore ="SampleSchema" recommendedConfidence = "65" >
          <Pattern confidenceLevel="65">
            <idMatch matches="MRN" classification="MRN" />
            <match matches="LastName" />
          </Pattern>
        </ExactMatch>
        <ExactMatch id = "E1CC861E-3FE9-4A58-82DF-4BD259EAB372" patternsProximity = "300" dataStore ="SampleSchema" recommendedConfidence = "65" >
          <Pattern confidenceLevel="65">
            <idMatch matches="SSN" classification="U.S. Social Security Number (SSN)" />
          </Pattern>
        </ExactMatch>
        <LocalizedStrings>
          <Resource idRef="E1CC861E-3FE9-4A58-82DF-4BD259EAB371">
            <Name default="true" langcode="en-us">Patient MRN exact match</Name>
            <Description default="true" langcode="en-us">EDM Sensitive type for detecting Patient MRN.</Description>
          </Resource>
          <Resource idRef="E1CC861E-3FE9-4A58-82DF-4BD259EAB372">
            <Name default="true" langcode="en-us">Patient SSN Exact Match.</Name>
            <Description default="true" langcode="en-us">EDM Sensitive type for detecting Patient SSN.</Description>
          </Resource>
        </LocalizedStrings>
      </Rules>
    </RulePackage>
    ```
    
    Note that column names in the data file are case-sensitive.

2. Upload the rule package by running the following PowerShell cmdlets, one at a time:

    `$rulepack=Get-Content .\rulepack.xml -Encoding Byte -ReadCount 0`

    `New-DlpSensitiveInformationTypeRulePackage -FileData $rulepack`

    To learn more about uploading a rule package, see [Upload your rule package](create-a-custom-sensitive-information-type-in-scc-powershell.md#upload-your-rule-package).

## Part 5: Apply EDM to a DLP policy

EDM can be used with Office 365 DLP policies and Microsoft Cloud App Security DLP policies. The following procedure describes how to use EDM with a DLP policy that you create in the Security & Compliance Center.

### To create a new DLP policy with EDM

1. Go to the Security & Compliance Center ([https://protection.office.com](https://protection.office.com)).

2. Choose **Data loss prevention** > **Policy**.

3. Choose **Create a policy** > **Custom** > **Next**.

4. On the **Name your policy** tab, specify a name and description, adn then choose **Next**.

5. On the **Choose locations** tab, select **Let me choose specific locations**, and then choose **Next**.

    ![EDM policy with Exchange only](media/EDM-DLPpolicy-ExchangeOnly.png)

6. On the **Policy settings** tab, choose **Use advanced settings**, and then choose **Next**.

7. Choose **+ New rule**.

8. In the **Name** section, specify a name and description for the rule.

9. In the **Conditions** section, in the **+ Add a condition** list, choose **Content contains EDM sensitive information type**.

10. Finish selecting options for the rule, and then choose **Save**.

11. On the **Policy settings** tab, review your rule(s), and then choose **Next**.

12. Specify whether to turn on the policy right away, test it out, or keep it turned off. Then choose **Next**.

13. On the **Review your settings** tab, review your policy. Make any needed changes. When you're ready, choose **Create**.

14. Allow approximately 30 minutes for your new DLP policy to work its way through your data center.

## Related articles

[Use PowerShell to create a custom sensitive information type in Security & Compliance Center](create-a-custom-sensitive-information-type-in-scc-powershell.md)

[Create a custom sensitive information type in the Security & Compliance Center](create-a-custom-sensitive-information-type.md) 

