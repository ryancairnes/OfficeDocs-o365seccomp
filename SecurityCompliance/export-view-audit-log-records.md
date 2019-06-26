---
title: "Export, configure, and view audit log records"
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

# Export, configure, and view audit log records




## Step 1: Export audit log search results

The first step is to search the audit log and then export the results to a comma separated value (CSV) file on your local computer.
  
1. Run an [audit log search](search-the-audit-log-in-security-and-compliance.md#search-the-audit-log) and revise the search criteria if necessary until you have the desired results.
    
2. Click **Export results** and select **Download all results**. 
    
   ![Click Download all results](media/ExportAuditSearchResults.png)

   This option to exports all the audit records from the audit log search you ran in step 1, and downloads the raw data from the audit log to a CSV file. 

   A message is displayed at the bottom of the window that prompts you to open or save the CSV file. 

3. Click **Save > Save as** and save the CSV file to your local computer. It will take a while to download a large number of search results. This is typically the case when searching for all activities or a broad date range. A message at the bottom of the windows is displayed when the CSV file is finished downloading.
 
   ![Message displayed when the CSV file is finished downloading](media/ExportAuditSearchResultsFinish.png)

> [!NOTE]
  > You can download a maximum of 50,000 entries to a CSV file from a single audit log search. If 50,000 entries are downloaded to the CSV file, you can probably assume there are more than 50,000 events that met the search criteria. To export more than this limit, try using a date range to reduce the number of audit log records. You might have to run multiple searches with smaller date ranges to export more than 50,000 entries.


## Step 2: Format the exported audit log using Power Query




1. Open a blank workbook in Excel for Office 365, Excel 2019, or Excel 2016.
    
2.  On the **Data** tab, in the **Get & Transform Data** ribbon group, click **From Text/CSV**.

    ![On the Data tab, click From Text/CSV](media/JSONTransformOpenCSVFile.png)

3. Open the CSV file that you downloaded in Step 1.
    
4. In the window that's displayed, click **Transform Data**.

   The CSV file is opened in **Power Query Editor**. There are four columns: **CreationDate**, **UserIds**, **Operations**, and **AuditData**. The **AuditData** column is a JSON object that contains multiple properties. The next step is to create a new column for each of the properties in the JSON object. 
    
5. Right-click the title in the **AuditData** column, click **Transform**, and then click **JSON**. 
 
   ![Right-click the AuditData column, click Transform, and then select JSON](media/JSONTransform.png)

6. In the upper-right corner of the **AuditData** column, click the expand icon.
    
   ![In the AuditData column, click the expand icon](media/JSONTransformExpandIcon.png)

   A partial list of the fields in the JSON object are displayed.

7. To display all fields in the JSON object, click **Load more**.

   ![Click Load more to display all fields from JSON object](media/JSONTransformLoadJSONProperties.png)

   You can unselect the checkbox next to any field that you don't want to include. This is a good way to simply the audit log by eliminating columns that aren't useful. 

8. Do one of the following things to format the title of the columns that will be added for each JSON field that's selected.

    - Unselect the **Use original column name as prefix** checkbox to use the name of the JSON field as the column names; for example, **RecordType** or **SourceFileName**.
    
   - Leave the **Use original column name as prefix** checkbox selected to add the AuditData prefix to the column names; for example, **AuditData.RecordType** or **AuditData.SourceFileName**.

9. Click **OK**.
    
    The **AuditData** column is split into multiple columns. Each new column corresponds to a property in the AuditData JSON object. Each row in the column contains the value for the property. If the property doesn't contain a value, the *null* value is displayed. In Excel, cells with null values are empty.
  
10. On the **Home** tab, click **Close & Load** to close the Power Query Editor and open the file in an Excel workbook. 
    
Here are screenshots of the CSV version of the audit log and the version in Excel after you use the JSON transform feature in Power Query editor.

**Before**



**After**

## Tips for viewing audit log records

Here are some tips and example of viewing the audit log after you use the JSON transform feature to split the AuditData column into multiple columns.

- 



## More information


    
- If you download all results, the CSV file contains a column named **AuditData**, which contains additional information about each event. As previously stated, this column contains a multi-value property for multiple properties from the audit log record. Each of the **property:value** pairs in this multi-value property are separated by a comma. You can use the Power Query in Excel to split this column into multiple columns so that each property will have its own column. This will let you sort and filter on one or more of these properties. To learn how to do this, see the "Split a column by delimiter" section in [Split a column of text (Power Query)](https://support.office.com/article/5282d425-6dd0-46ca-95bf-8e0da9539662).
    
    After you split the **AuditData** column, you can filter on the **Operations** column to display the detailed properties for a specific type of activity. 
    
- There's a 3,060-character limit for the data that's displayed in the **AuditData** field for an audit record. If the 3,060-character limit is exceeded, the data in this field is truncated. 