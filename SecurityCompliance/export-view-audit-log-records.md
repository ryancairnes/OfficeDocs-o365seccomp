---
title: "Export and view audit log records"
ms.author: markjjo
author: markjjo
manager: laurawi
audience: Admin
ms.topic: article
ms.service: O365-seccomp
localization_priority: Normal
ms.collection: 
- Strat_O365_IP
- M365-security-compliance
search.appverid: 
- MOE150
- MET150
ms.assetid: 0d4d0f35-390b-4518-800e-0c7ec95e946c
description: ""
---

# Export and view audit log records




## Step 1: Export audit log search results

The first step is to search the audit log and then export the results to a comma separated value (CSV) file on your local computer.
  
1. Run an [audit log search](search-the-audit-log-in-security-and-compliance.md#search-the-audit-log) and then revise the search criteria until you have the desired results.
    
2. Click **Export results** and select **Download all results**. 
    
   ![Click Download all results](media/ExportAuditSearchResults.png)

   This option to exports all the audit records from the audit log search you ran in step 1, and downloads the raw data from the audit log to a CSV file. 

   A message is displayed at the bottom of the window that prompts you to open or save the CSV file. 

3. Click **Save > Save as** and save the CSV file to your local computer. It will take a while to download a large number of search results.

> [!IMPORTANT]
  > You can download a maximum of 50,000 entries to a CSV file from a single audit log search. If 50,000 entries are downloaded to the CSV file, you can probably assume there are more than 50,000 events that met the search criteria. To export more than this limit, try using a date range to reduce the number of audit log records. You might have to run multiple searches with smaller date ranges to export more than 50,000 entries.


## Step 2: Format the audit log records using Power Query




1. In Excel 2016, open a blank workbook.
    
2. On the **Data** tab, click **From Text/CSV**, and open the CSV file that you downloaded in Step 1.
    
3. On the thumbnail page that's displayed, click **Transform Data**.

   The CSV file is opened in **Power Query Editor**. There are four columns: **CreationDate**, **UserIds**, **Operations**, and **AuditData**. The **AuditData** column is a JSON object that contains multiple properties. The next step is to create a new column for each of the properties in the JSON object. 
    
4. Right-click the title in the **AuditData** column, and then select **Transform > JSON**. 
 
5. 
    
    ![On the Home tab, click Split Column, and then click By Delimiter](media/aeb503e8-565b-42ea-91e2-9f127a74c00c.png)
  
6. In the **Split Column by Delimiter** window, do the following: 
    
      - Under **Select or enter delimiter**, select **Comma**.
    
      - Under **Split**, select **At each occurrence of the delimiter**.
    
7. Click **OK**.
    
    The **Detail** column is split into multiple columns. Each new column is named **Detail.1**, **Detail.2**, **Detail.3**, and so on. You'll notice the values in each cell in the **Detail.n** columns are prefixed with the name of the property; for example, **Operation:SharingSet**, **Operation:SharingInvitationAccepted**, and **Operation:SharingInvitationCreated**.
    
    ![The Detail column is split into multiple columns, one for each property](media/4b104ead-0313-4bd4-b2a9-f143ccb378ac.png)
  
8. On the **File** tab, click **Close &amp; Load** to close the Query Editor and open the file in an Excel workbook. 
    
    The next step is to filter the file to only display the **SharingSet** and **SharingInvitationCreated** events. 

## More information

- The **Download all results** option downloads the raw data from the Office 365 audit log to a CSV file. This file contains different column names (CreationDate, UserIds, Operation, AuditData) than the file that's downloaded if you select the **Save loaded results** option. The values in the two different CSV files for the same activity may also be different. For example, the activity in the **Action** column in the CSV file and may have a different value than the "user-friendly" version that's displayed in the **Activity** column on the **Audit log search** page; for example, MailboxLogin vs. User signed in to mailbox.
    
- If you download all results, the CSV file contains a column named **AuditData**, which contains additional information about each event. As previously stated, this column contains a multi-value property for multiple properties from the audit log record. Each of the **property:value** pairs in this multi-value property are separated by a comma. You can use the Power Query in Excel to split this column into multiple columns so that each property will have its own column. This will let you sort and filter on one or more of these properties. To learn how to do this, see the "Split a column by delimiter" section in [Split a column of text (Power Query)](https://support.office.com/article/5282d425-6dd0-46ca-95bf-8e0da9539662).
    
    After you split the **AuditData** column, you can filter on the **Operations** column to display the detailed properties for a specific type of activity. 
    
- There's a 3,060-character limit for the data that's displayed in the **AuditData** field for an audit record. If the 3,060-character limit is exceeded, the data in this field is truncated. 
    
- When you download all results from a search query that contains events from different Office 365 services, the **AuditData** column in the CSV file contains different properties depending on which service the action was performed in. For example, entries from Exchange and Azure AD audit logs include a property named **ResultStatus** that indicates if the action was successful or not. This property isn't included for events in SharePoint. Similarly, SharePoint events have a property that identifies the site URL for file and folder related activities. To mitigate this behavior, consider using different searches to export the results for activities from a single service. 
    
    For a description of the properties that are listed in the **AuditData** column in the CSV file when you download all results, and the service each one applies to, see [Detailed properties in the Office 365 audit log](detailed-properties-in-the-office-365-audit-log.md).