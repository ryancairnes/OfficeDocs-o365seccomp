---
title: "Create custom sensitive information types with Exact Data Match"
ms.author: deniseb
author: denisebmsft
manager: laurawi
ms.audience: Admin
ms.topic: article
ms.service: O365-seccomp
ms.date: 04/30/2019
localization_priority: Priority
ms.collection: 
- M365-security-compliance
search.appverid: 
- MOE150
- MET150
description: "Create custom sensitive information types with Exact Data Match."
---

# Create custom sensitive information types with Exact Data Match (EDM) (Preview)

## Overview

With Office 365 for business, you can define [custom sensitive information types](custom-sensitive-info-types.md) that you can use to help prevent people from inadvertently or inappropriately sharing sensitive data within your organization. You can [use the Security & Compliance Center](create-a-custom-sensitive-information-type.md) or [use PowerShell](create-a-custom-sensitive-information-type-in-scc-powershell.md) to define a custom sensitive information type based on patterns, evidence (evidence includes keywords like *employee*, *badge*, *ID*, and so on), character proximity (how close evidence is to characters in a particular pattern), and confidence levels. 

But what if you wanted a custom sensitive information type that uses exact data values, instead of patterns and proximity? With Exact Data Match (EDM) classification, you can create a custom sensitive information type that:
- is dynamic (refreshable daily or weekly);
- is more scalable;
- results in fewer false-positives;
- is based on structured sensitive data;
- handles sensitive information more securely; and
- can be leveraged with several Microsoft cloud services.

![EDM classification](media/EDMClassification.png)

EDM classification enables you to create custom sensitive information types that refer to exact values in a database of sensitive information. The database can be refreshed daily or weekly, and it can contain up to ten million rows of data. So as employees, patients, or clients come and go, and records change, your custom sensitive information types remain current and applicable. And, you can use EDM classification with policies, such as [data loss prevention policies](data-loss-prevention-policies.md) (DLP) or [Microsoft Cloud App Security file policies](https://docs.microsoft.com/cloud-app-security/data-protection-policies).

> [!NOTE]
> **EDM classification is currently in preview**, and is currently supported for Office 365 DLP and Microsoft Cloud App Security, across Exchange Online and Microsoft Teams. To participate in the preview, must have Office 365 E5, Office 365 E5, or Office 365 Advanced Compliance. 

## Required licenses and permissions

- During the preview program, if your organization has [DLP](https://docs.microsoft.com/office365/servicedescriptions/exchange-online-protection-service-description/messaging-policy-and-compliance-servicedesc#data-loss-prevention-dlp), you can try EDM classification. If you are not already participating in the preview, [contact us](https://resources.office.com/us-landing-spe-contactus.html?LCID=EN-US) to get started.

- You must be a global admin, compliance administrator, or Exchange Online administrator to perform the tasks described in this article. To learn more about DLP permissions, see [Permissions](data-loss-prevention-policies.md#permissions).

## The work flow at a glance

|Phase  |What's needed  |
|---------|---------|
|[Part 1: Set up EDM classification](#part-1-set-up-edm-classification) |- Read access to the sensitive data<br/>- Ability to define a database schema in .xml format (this article includes an example)<br/>- Ability to create a rule package in .xml format (this article includes an example)<br/>- Admin permissions to upload the database schema file and rule package file to the Security & Compliance Center (using PowerShell) |
|[Part 2: Index and upload the sensitive data](#part-2-index-and-upload-the-sensitive-data) |- Custom security group and user account on Windows<br/>- EDM Upload Agent tool|    |         |
|[Part 3: Use EDM classification with your Microsoft cloud services (Example: DLP policy)](#part-3-use-edm-classification-with-your-microsoft-cloud-services-example-dlp-policy) |- Office 365 or Microsoft 365 subscription that includes DLP<br/>- EDM classification feature enabled (this is currently in preview) |

## Part 1: Set up EDM classification

Setting up and configuring EDM classification involves saving sensitive data in .csv format, defining a schema for your database of sensitive information, creating a rule package, and then uploading the schema and rule package.

### Define the schema for your database of sensitive information

1. Identify the sensitive information you want to use. Export the data to an app, such as Microsoft Excel, and save the file in .csv format. The data file can include:

    - Up to ten million rows of sensitive data
    - Up to 32 columns (fields) per data source

2. Structure the sensitive data in the .csv file. Make sure the first row of the .csv file includes the names of the fields you'll use for EDM classification. For example, you might have field names, such as `ssn`, `birthdate`, `firstname`, `lastname`, `employeeid`, and so on. 
    
    As an example, our .csv file is called *SampleDataStore.csv*. It includes columns, such as *id*, *firstname*, *lastname*, *title*, *creditcard* and so on.

3. Define the schema for the database of sensitive information in .xml format (similar to our example below). Name this schema file `edm.xml`, and configure it such that for each column in the database, there is a line that uses the syntax `<Field name="" unique="" searchable=""/>`. 

    - Use the column's name for the *Field name* value.
    - Use `unique="true"` for the fields that contain unique values (Social Security numbers, identification numbers, etc.); otherwise, use `unique="false"`.
    - Use `searchable="true"` for the fields that should be searchable. No more than five fields per database should be searchable. All the rest should have `searchable="false"`.  

    As an example, the following .xml file defines the schema for our example *SampleDataStore* database. Here, we specified three fields (*firstname*, *creditcard*, and *ssn*) as searchable for EDM classification. (You can copy our example and modify it for your use.)
    
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

4. [Connect to Office 365 Security & Compliance Center PowerShell](https://docs.microsoft.com/powershell/exchange/office-365-scc/connect-to-scc-powershell/connect-to-scc-powershell?view=exchange-ps).

5. To upload the database schema, run the following cmdlets, one at a time:

    `$edmSchemaXml=Get-Content .\edm.xml -Encoding Byte -ReadCount 0`

    `New-DlpEdmSchema -FileData $edmSchemaXml`

Now that the schema for your database of sensitive information is defined, the next step is to set up a rule package.

### Set up a rule package

1. Create a rule package in .xml format (with Unicode encoding), similar to the example included below. (You can copy our example and modify it for your use.) 

    Recall from the previous procedure that our SampleDataStore schema defines three fields as searchable for EDM: *firstname*, *creditcard*, and *ssn*. Our example file includes two of those three fields, listed as *ExactMatch* items. 

    ```
        <?xml version="1.0" encoding="utf-8"?>
    <RulePackage xmlns="http://schemas.microsoft.com/office/2018/edm">
      <RulePack id="fd098e03-1796-41a5-8ab6-198c93c62b11">
        <Version build="0" major="2" minor="0" revision="0" />
        <Publisher id="eb553734-8306-44b4-9ad5-c388ad970528" />
        <Details defaultLangCode="en-us">
          <LocalizedDetails langcode="en-us">
            <PublisherName>Microsoft EDM</PublisherName>
            <Name>SampleDataStore EDM Rulepack</Name>
            <Description> This rule package contains the EDM sensitive types for our SampleDataStore.</Description>
          </LocalizedDetails>
        </Details>
      </RulePack>
      <Rules>
        <ExactMatch id = "E1CC861E-3FE9-4A58-82DF-4BD259EAB371" patternsProximity = "300" dataStore ="SampleSchema" recommendedConfidence = "65" >
          <Pattern confidenceLevel="65">
            <idMatch matches="firstname" classification="firstname" />
            <match matches="firstname" />
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
    (To learn more about .xml files like this, see [Sample XML of a rule package](create-a-custom-sensitive-information-type-in-scc-powershell.md#sample-xml-of-a-rule-package).)
    
2. Upload the rule package by running the following PowerShell cmdlets, one at a time:

    `$rulepack=Get-Content .\rulepack.xml -Encoding Byte -ReadCount 0`

    `New-DlpSensitiveInformationTypeRulePackage -FileData $rulepack`

    To learn more about uploading rule packages, see [Upload your rule package](create-a-custom-sensitive-information-type-in-scc-powershell.md#upload-your-rule-package).

At this point, you have set up EDM classification. The next step is to index and upload the sensitive data. 

## Part 2: Index and upload the sensitive data

During this phase, you set up a custom security group and user account, install the EDM Upload Agent tool on your Windows machine, and then use the tool to index and upload the sensitive data.

### Set up a security group, user account, and Windows machine with the EDM Upload Agent

1. As an administrator on a Windows machine, create a security group and name it `EDM_DataUploaders`. Then add the *EDM_DataUploaders* security group to the Administrators group in Windows.

2. Create a new user account for the Windows machine, and add that account to the *EDM_DataUploaders* security group.

3. Sign out of Windows, and then sign back in using the new user account. 

5. Download and install the EDM Upload Agent at [https://go.microsoft.com/fwlink/?linkid=2088639](https://go.microsoft.com/fwlink/?linkid=2088639). Make sure to note the installation location (such as `C:\`). 

6. To authorize the EDM Upload Agent, run the following command in Windows Command Prompt:

    `EdmUploadAgent.exe /Authorize`

    When prompted, sign in using your work or school account for Office 365 (you must be a global admin, compliance administrator, or Exchange Online administrator).

The next step is to use the EDM Upload Agent to index the sensitive data, and upload the indexed data.

### Index and upload the sensitive data

1. Save the sensitive data file (recall our example is *SampleDataStore.csv*) to the local drive on the machine. (We saved our example *SampleDataStore.csv* file to `C:\Edm\Data`.)

2. To index the sensitive data, run the following command in Windows Command Prompt:

    `EdmUploadAgent.exe /CreateHash /DataStoreName <DataStoreName> /DataFile <DataFilePath> /HashLocation <HashedFileLocation>`

    Example: `EdmUploadAgent.exe /CreateHash /DataStoreName SampleDataStore /DataFile C:\Edm\Data\SampleDataStore.csv /HashLocation C:\Edm\Hash` 

3. To upload the indexed data, run the following command in Windows Command Prompt:

    `EdmUploadAgent.exe /UploadHash /DataStoreName <DataStoreName> /HashFile <HashedSourceFilePath>`

    Example: `EdmUploadAgent.exe /UploadHash /DataStoreName SampleDataStore /HashFile C:\Edm\Hash\SampleDataStore.EdmHash` 

4. To verify your sensitive data has been uploaded, run the following command in Windows Command Prompt:

    `EdmUploadAgent.exe /GetDataStore`

    You'll see a list of data stores and when they were last updated. Here's an example:

    ![Example of GetDataStore cmdlet and results](media/EDM-GetDataStore-example.png)

> [!TIP]
> We recommend setting up a regular schedule and process for updating the .csv file, and using [Task Scheduler](https://docs.microsoft.com/windows/desktop/TaskSchd/task-scheduler-start-page) to automate Steps 2-3. 

Now you can use EDM classification with your Microsoft cloud services. For example, you can set up a DLP policy using EDM classification. 

## Part 3: Use EDM classification with your Microsoft cloud services

EDM can be used with information protection features, such as [Office 365 DLP policies](data-loss-prevention-policies.md) and [Microsoft Cloud App Security file policies](https://docs.microsoft.com/cloud-app-security/data-protection-policies). As an example, the following procedure describes how to use EDM with a DLP policy that is created in the Office 365 Security & Compliance Center.

### To create a new DLP policy with EDM

1. Go to the Security & Compliance Center ([https://protection.office.com](https://protection.office.com)).

2. Choose **Data loss prevention** > **Policy**.

3. Choose **Create a policy** > **Custom** > **Next**.

4. On the **Name your policy** tab, specify a name and description, and then choose **Next**.

5. On the **Choose locations** tab, select **Let me choose specific locations**, and then choose **Next**.<br/>![Choose locations option](media/DLP-EDM-newpolicy-chooselocations.png)<br/>

6. In the **Status** column, select **Exchange email** only, and then choose **Next**. <br/>![EDM policy with Exchange only](media/EDM-DLPpolicy-ExchangeOnly.png)<br/>

7. On the **Policy settings** tab, choose **Use advanced settings**, and then choose **Next**.<br/>![Use advanced settings](media/edm-dlp-policy-advancedsettings.png)<br/>

8. Choose **+ New rule**.<br/>![Create a new rule](media/edm-dlp-newrule.png)<br/>

9. In the **Name** section, specify a name and description for the rule.<br/>![New rule fields](media/edm-dlp-newruleform.png)<br/>

10. In the **Conditions** section, in the **+ Add a condition** list, choose **Content contains sensitive type**.<br/>![Content contains sensitive info types](media/edm-dlp-newrule-conditions.png)<br/>

11. Search for the sensitive information type you created when you defined a rule package in [Part 4](#part-4-create-a-rule-package-with-exact-matching), and then choose **+ Add**.<br/>![Find the sensitive info type](media/edm-dlp-newrulefindsensitiverulepack.png)<br/>Then choose **Done**.

12. Finish selecting options for your rule, such as **User notifications**, **User overrides**, **Incident reports**, and so on, and then choose **Save**.

13. On the **Policy settings** tab, review your rule(s), and then choose **Next**.

14. Specify whether to turn on the policy right away, test it out, or keep it turned off. Then choose **Next**.

15. On the **Review your settings** tab, review your policy. Make any needed changes. When you're ready, choose **Create**.

> [!TIP]
> Allow approximately one hour for your new DLP policy to work its way through your data center.

## Refreshing your sensitive information database

You can refresh your sensitive information database daily or weekly. When your .csv file is refreshed, make sure to use the EDM Upload Tool to re-index the sensitive data and then re-upload the indexed data. To get help with this, see [Index and upload the sensitive data](#index-and-upload-the-sensitive-data) (in this article). 

## Related articles

[Built-in sensitive information types and what they look for](what-the-sensitive-information-types-look-for.md)

[Custom sensitive information types](custom-sensitive-info-types.md)

[Overview of DLP policies](data-loss-prevention-policies.md)

[Microsoft Cloud App Security](https://docs.microsoft.com/cloud-app-security)