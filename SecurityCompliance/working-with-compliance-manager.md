---
title: "Working with Microsoft Compliance Manager"
ms.author: robmazz
author: robmazz
manager: laurawi
ms.audience: Admin
ms.topic: article
ms.service: O365-seccomp
localization_priority: Normal
ms.collection: M365-security-compliance
search.appverid: 
- MOE150
- MET150
description: "Microsoft Compliance Manager is a workflow-based risk assessment tool in the Microsoft Service Trust Portal that enables you to track, assign, and verify your organization's regulatory compliance activities related to Microsoft Professional Services and Microsoft cloud services, such as Microsoft Office 365, Microsoft Dynamics 365, and Microsoft Azure."
---

# Working with Microsoft Compliance Manager

> [!IMPORTANT]
> Microsoft Compliance Manager is a dashboard and management tool that provides a summary of your data protection and compliance stature and recommendations to improve data protection and compliance. The customer actions provided in Compliance Manager are recommendations; it is up to your organization to evaluate the effectiveness of these recommendations in their respective regulatory environment prior to implementation. Recommendations found in Compliance Manager should not be interpreted as a guarantee of compliance.

## Groups

As shown in the example below, you could group Assessments by year, standard, service, team, division, or agencies within your organization to minimize customer actions:
  
- **GDPR Assessments - 2019**
  - Office 365 + GDPR
  - Azure + GDPR
  - Dynamics + GDPR
- **Azure Assessments - 2019**
  - Azure + GDPR
  - Azure + ISO 27001:2013
  - Azure + ISO 27018:2014
- **Data Security and Privacy Assessments**
  - Office 365 + ISO 27001:2013
  - Office 365 + ISO 27018:2014
  - Azure + ISO 27001:2013
  - Azure + ISO 27018:2014
  - 

When you create a new Assessment, you're prompted to create a new group to assign the Assessment to or assign the Assessment to an existing group. However, it's recommend that your determine a grouping strategy for your organization *before* adding new assessments.

When working with groups, remember that:
  
- Group names (also called *Group IDs*) must be unique within your organization.
- Groups can contain Assessments for the same certification/regulation, but each group can only contain one Assessment for a specific cloud service/certification pair. For example, a group can't contain two Assessments for Office 365 and GDPR. Similarly, a group can contain multiple Assessments for the same cloud service as long as the corresponding certification/regulation for each one is different.
- Once an assessment has been added to an assessment grouping, the grouping cannot be changed. You can rename the assessment group, which changes the name of the assessment grouping for all of the assessments associated with that group. You can create a new assessment and a new assessment group and copy information from an existing assessment, which effectively creates a duplicate of that assessment in a different assessment group. Archiving an assessment breaks the relationship between that assessment and the assessment group; any further updates to other related assessments are no longer reflected in the archived assessment.

### Groups example

As an example of this, consider these two related assessment controls, each having to do with encryption of data on public networks, control 6.10.1.2 in the Office 365 - GDPR assessment, and control SC-13 in the Office 365 - NIST 800-53 assessment. These are related assessment controls, in two different assessments, both in the Default Group; initially, neither assessment has completed any customer control assessments, as is displayed on the Compliance Manager Dashboard that shows these two Assessments.
  
![Compliance Manager Dashboard - grouped assessments - before](media/dc0126a3-415c-4fbe-a020-1806dd1caebd.png)
  
By clicking the **Office 365 - GDPR** assessment, and using the filter controls to view GDPR control 6.10.1.2, we see that NIST 800-53 control SC-13 is listed as a related control.
  
![Compliance Manager Assessment - shared controls](media/aafb106e-0abc-4918-8038-de11cf326dfe.png)
  
 Here we show the completion of the implementation and testing of GDPR control 6.10.1.2. 
  
![Compliance Manager Assessment control GDPR 6.10.1.2 - passed](media/ee9e83b6-9d51-4b3b-85eb-96bec0fef2e1.png)
  
By navigating to the related control in the grouped assessment, we see that NIST 800-53 SC-13 has also been marked as completed with the same date and time, with no additional implementation or testing effort.
  
![Compliance Manager assessment - NIST 800-53 SC(13) completed](media/b5933592-db5a-4fdd-9be2-bba777646a88.png)
  
Back at the Dashboard, we can see that each assessment has 1 control assessment completed and that the total Compliance Score for each assessment has increased by 8 (the compliance score value of that shared control).
  
![Compliance Manager Dashboard - grouped assessment progress synchronization](media/727f1203-b98d-4a03-a7af-e9236f4c5534.png)



## Assessments

Assessments include several components:
  
- **In-Scope Services**: Each assessment applies to a specific set of Microsoft services, which are listed in the In-Scope Cloud Services section.
- **Microsoft Managed controls**: For each cloud service, Microsoft implements and manages a set of controls as part of Microsoft's compliance with various standards and regulations.
- **Customer anaged controls**: This is the collection of controls that are managed by your organization.
- **Assessment score**: 

You can export an Assessment to an Excel file, which can be reviewed by compliance stakeholders in your organization, and provided to auditors and regulators. This assessment report is a snapshot of the assessment as of the date and time that the report is created, and it contains the details of both the Microsoft-managed controls and the customer managed controls for that assessment, including control implementation status, control test date and test results, and provides links to the uploaded evidence documents.

When you have completed an Assessment and no longer need it for compliance purposes, you can archive it. When an Assessment is archived, it is removed from Assessments dashboard.
  
> [!NOTE]
> When an Assessment is archived, it cannot be 'unarchived' or restored to a read-write in progress state. Please note that archived Assessments do not retain their links to uploaded evidence documents, so it is highly recommended that you perform an Export of the Assessment before archiving it, as the exported assessment report will contain links to the evidence documents, enabling you to continue to access them.

### Managing the assessment process

The creator of an Assessment is initially the only Assessment User. For each customer managed control, you can assign an Action Item to a person in your organization so that person becomes an Assessment User who can perform the recommended Customer Actions, and gather and upload evidence. When you assign an Action Item, you can choose to send an email to the person that contains details including the recommended Customer Actions and the Action Item priority. The email notification includes a link to the **Action Items** dashboard, which lists all Action Items assigned to that person. 
  
Here's a list of tasks that you can perform using the workflow features of Compliance Manager.
  
![Compliance manager assessment workflow with callouts](media/9e5ae34d-b55e-4452-a021-e0e5b10218f5.png)
  
1. **Use the Filter Options to find specific assessment controls** - Compliance Manager provides **Filter Options**, giving you highly granular selection criteria for displaying assessment controls, helping you to precisely target specific areas of your compliance efforts. 
    
    Click on the funnel icon on the right hand side of the page to show or hide the **Filter Options** controls. These controls allow you to specify filter criteria, and only the assessment controls that fit those criteria will be displayed below. ![Compliance Manager Assessments filter controls](media/d44e1b4b-d928-4778-8a3a-6231edde9ca0.png)
  
    - **Articles** - filters on the article name and returns the assessment controls associated to that article. For instance, typing in "Article (5)" returns a selection list of articles whose name includes that string, i.e. Article (5)(1)(a), Article (5)(1)(b), Article (5)(1)(c), etc. Selecting Article (5)(1)(c) will return the controls associated with Article (5)(1)(c). This is multiselect field that uses an OR operator with multiple values -- for instance, if you select Article (5)(1)(a) and then add Article (5)(1)(c), the filter will return controls associated with either Article (5)(1)(a) or Article (5)(1)(c). 
    
      ![Compliance Manager Assessment view - Filter on Article Name](media/8b0507a0-589d-484a-bc60-80a3debe3ddb.png)
  
    - **Controls** - returns the list of controls whose names fit the filter, i.e. typing in 7.3 returns a selection list of items like 7.3.1, 7.3.4, 7.3.5, etc. This is multiselect field that uses an OR operator with multiple values -- for instance, if you select 7.3.1 and then add 7.3.4, the filter will return controls associated with either 7.3.1 or 7.3.4. 
    
      ![Compliance Manager Assessment view - filter control multiselect](media/c4fc25e8-2376-4f2d-b605-f9c3d90413bf.png)
  
    - **Assigned Users** - returns the list of controls who are assigned to the selected user. 
    
    - **Status** - returns the list of controls with the selected status. 
    
    - **Test Result** - returns the list of controls with the selected test result. 
    
    As you apply filter conditions, the view of applicable controls will change to correspond to your filter conditions. Expand the control family sections to show the control details below. 
    
    ![Compliance Manager Assessment view - Filter Article results](media/e6485d45-d47f-4b25-8b1c-b3c2ee4a8328.png)
  
2. If after selecting the desired filters no results are shown, that means there are no controls that correspond to the specified filter conditions. For instance, if you select a particular **Assigned User** and then choose a **Control** name that does correspond to the control assigned to that user, no assessments will be shown in the page below. 
    
3. **Assign an Action Item to a user** - You can assign an Action Item to a person to implement the requirements of a certification/regulation, or to test, verify, and document your organization's implementation requirements. When you assign an Action Item, you can choose to send an email to the person that contains details including the recommended Customer Actions and the Action Item priority. You can also unassign or reassign an Action Item to a different person. 
    
4. **Manage documents** - Customer managed controls also have a place to manage documents that are related to performing implementation tasks and for performing testing and validation tasks. Anyone with permissions to edit data in Compliance Manager can upload documents by clicking **Manage Documents**. After a documented has been uploaded, you can click **Manage Documents** to view and download files. 
    
5. **Provide implementation and testing details** - Every customer managed control has an editable field where users can add implementation details that document the steps taken by your organization to meet the requirements of the certification/regulation, and to validate and document how your organization meets those requirements.
    
6. **Set Status** - Set the Status for each item as part of the assessment process. Available status values are **Implemented**, **Alternative Implementation**, **Planned**, and **Not in Scope**. 
    
7. **Enter test date and test result** - The person with the Compliance Manager Assessor role can verify that proper testing performed, review the implementation details, test plan, test results, and any uploaded evidence, and then set the Test Date and Test Result. Available test result values are **Passed**, **Failed-Low Risk**, **Failed-Medium Ris** **k**, and **Failed-High Risk**. 

### Adding an Assessment

To add an Assessment to Compliance Manager:
  
1. In the Compliance Manager dashboard, click ![Add Icon](media/ITPro-EAC-AddIcon.gif) **Add Assessment**. 
    
2. In the **Add an Assessment** window, you can create a new group to add the Assessment to or you can add it to an existing group (the built-in group is named "Initial Group".) Depending on the option you choose, either type the name of a new group or select an existing group from the drop-down list. For more information, see [Grouping Assessments](#grouping-assessments).
    
    If you create a new group, you also have the option to copy information from an existing group to the new Assessment. That means any information that was added to the Implementation Details and Test Plan and Management Response fields of customer managed controls from Assessments in the group that you're copying from are copied to the same (or related) customer managed controls in the new Assessment. If you're adding a new Assessment to an existing group, common information from Assessments in that group will be copied to the new Assessment. For more information, see [Copying information from existing Assessments](#copying-information-from-existing-assessments).
    
3. Click **Next**, and do the following:
    
    a. Choose a Microsoft cloud service to assess for compliance from the **Select a product** drop down list. 
    
    b. Choose a certification to assess the selected cloud service against from the **Select a certification** drop down list. 
    
4. Click **Add to Dashboard** to create the Assessment; the assessment will be added to the Compliance Manager dashboard as a new tile at the end of the list of existing tiles. 
    
    The **Assessment Tile** on the Compliance Manager dashboard, displays the assessment grouping, the name of the assessment (automatically created as a combination of the Service name and the certification selected), the date it was created and when it was last modified, the Total Compliance Score (which is the sum of all of the assigned control risk values that have been implemented, tested and passed), and progress indicators along the bottom that show the number of controls that have been assessed. 
    
5. Click the Assessment name to open it, and view the details of the Assessment.
    
6. Click on the **Actions** menu to view your assigned action items, rename the assessment group, export the assessment report, or archive the assessment. 
    
    ![Compliance Manager - Assessment Tile](media/abf35c11-9757-45c1-aa14-91178f67a18c.png)

### Copying information from existing Assessments

As previously explained, when you create a new assessment group, you have the option to copy information from Assessments in an existing group to the new Assessment in the new group. This allows you to apply the assessment and testing work that's been completed to the same customer managed controls in the new Assessment. For example, if you have a group for all GDPR-related Assessments in your organization, you can copy common information from existing assessment work when add a new Assessment to the group.
  
You can copy the following information from customer to a new Assessment:
  
- Assessment Users. An Assessment user is a user who the control is assigned to.
    
- Status, Test Date, and Test Results.
    
- Implementation details and test plan information.
    
Similarly, information from shared customer managed controls within the same Assessment group is synchronized. And information in related customer managed controls within the same Assessment is also synchronized.

### Viewing Assessments

1. Locate the Assessment Tile corresponding to the assessment you wish to view, then click the assessment name to open it and view the Microsoft and customer managed controls associated with the Assessment, along with a list of the cloud services that are in-scope for the Assessment. Here's an example of the Assessment for Office 365 and GDPR.
    
    ![Compliance Manager Assessment View - fullscreen with callouts](media/169a02eb-e805-412d-b9e7-89561aa7ad1d.png)
  
1. This section shows the Assessment summary information, including the name of the Assessment Grouping, Product, Assessment name, number of Assess controls
    
2. This section shows the Assessment Filter controls. For a more detailed explanation of how to use the Assessment Filter controls see the [Managing the assessment process](#managing-the-assessment-process) section. 
    
3. This section shows the individual cloud services that are in-scope for the assessment.
    
4. This section contains Microsoft managed controls. Related controls are organized by control family. Click a control family to expand it and display individual controls.
    
5. This section contains customer managed controls, which are also organized by control family. Click a control family to expand it and display individual controls.
    
6. Displays the total number of controls in the control family, and how many of those controls have been assessed. A key capability of Compliance Manager is tracking your organization's progress on assessing the customer managed controls. For more information, see the [Understanding the Compliance Score](#understanding-the-compliance-score) section. 

### Exporting information from an Assessment

You can export an Assessment to an Excel file, which can be reviewed by compliance stakeholders in your organization, and provided to auditors and regulators. This assessment report is a snapshot of the assessment as of the date and time that the report is created, and it contains the details of both the Microsoft-managed controls and the customer managed controls for that assessment, including control implementation status, control test date and test results, and provides links to the uploaded evidence documents. It is recommended that you export the assessment report prior to archiving an assessment, as archived assessments do not retain their links to uploaded documents.
  
To export an Assessment report:
  
- On the Compliance Manager dashboard, click **Actions** on the tile of the assessment you wish to export, and then choose **Export to Excel**

  Or
    
- If you are viewing the Assessment details page, click on the **Export to Excel** button, which is located in the upper right hand corner of the page above the assessment's Compliance Score.
    
The assessment report will be downloaded in your browser session. If you don't see a popup informing you of this, you may wish to check your browser's downloads folder.

### Archiving an Assessment

When you have completed an Assessment and no longer need it for compliance purposes, you can archive it. When an Assessment is archived, it is removed from Assessments dashboard.
  
> [!NOTE]
> When an Assessment is Archived, it cannot be 'unarchived' or restored to a read-write in progress state. Please note that Archived Assessments do not retain their links to uploaded evidence documents, so it is highly recommended that you perform an Export of the Assessment before archiving it, as the exported assessment report will contain links to the evidence documents, enabling you to continue to access them. 
  
To archive an assessment:
  
1. On the dashboard tile of the desired assessment, click **Actions**. 
    
2. Select **Archive Assessment**. 
 
    The **Archive Assessments** dialog is displayed, asking you to confirm that you want to archive the assessment.
    
4. To continue with archiving, click **Archive**, or else click **Cancel**. 
    
To view archived Assessments:
  
1. On the Compliance Manager dashboard, check the **Show Archived** checkbox. 
    
    The archived assessments will appear in a newly visible section below the rest of the active assessments under a bar titled **Archived Assessments**.
    
3. Click the name of the assessment you wish to view.
    
When viewing an archived assessment, none of the normally editable controls (i.e. Implementation, Test Results) will be active, and the **Managed Documents** button will be absent.

## Controls

## Actions

### Assigning action items
  
1. On the Compliance Manager dashboard, locate the assessment tile of the assessment you wish to work with and click on the name of the assessment to go to the assessment details page.
    
2. You can click **Filter** and use the filter controls to find the specific assessment control you wish to assign, or 
    
3. Scroll down to the Customer Managed Controls section, expand the control family, and scroll through the list of control until you have located the assessment control to be assigned
    
4. Under the **Assigned User** column, click **Assign**. 
    
5. In the Assign Action Item dialog box, click the **Assign To** field to populate the list of users to whom the action can be assigned. You can scroll through the list to find the target user or start typing in the field to search for the username. 
    
6. Click the user to assign them this action item.
    
7. If you wish to send an email notification to the user notifying them, ensure that the **Send Email Notification** checkbox is checked. 
    
8. Type any notes you wish to be displayed to that user and click **Assign**. 
 
    The user will receive notification of their action item assignment and any notes you have provided.
    
The notes that are associated with the action item are persisted in the notes section, available for the next time the action item is assigned. These notes are not read-only, can be edited, replaced or removed by the person assigning the action item.

### Viewing action items

Compliance Manager provides a convenient view of all your assigned control assessment action items, enabling you to quickly and easily take action on them. You can view all action items or select the action items that correspond with a specific certification by clicking on the tab associated with that assessment. For instance, in the image below, the GDPR tab has been selected, showing controls that related to the GDPR assessment.
  
![Compliance Manager - Action Items list multiple tabs GDPR selected](media/ba960f5c-becb-4d95-a000-d08ec77b7b46.png)
  
To view your action items:
  
1. Go to the Compliance Manager dashboard
    
2. Click the **Action Items** link, and the page will refresh to show the action items that have been assigned to you. 
    
    By default, all action items are shown. If you have action items across multiple certifications, the names of the certifications will be listed in tabs across the top of the assessment control. To see the action items for a specific certification, click that tab.

## Documents

## Templates

## Archiving

## Reporting

## Permissions

The following table describes each Compliance Manager permission and what it allows the user do. The table also indicates the role that each permission is assigned to.
  
||**Compliance Manager Reader**|**Compliance Manager Contributor**|**Compliance Manager Assessor**|**Compliance Manager Administrator**|**Portal Admin**|
|:-----|:-----|:-----|:-----|:-----|:-----|
|**Read data** - Users can read but not edit data.  <br/> |![Check mark](media/f3b4c351-17d9-42d9-8540-e48e01779b31.png)           <br/> |![Check mark](media/f3b4c351-17d9-42d9-8540-e48e01779b31.png)           <br/> |![Check mark](media/f3b4c351-17d9-42d9-8540-e48e01779b31.png)           <br/> |![Check mark](media/f3b4c351-17d9-42d9-8540-e48e01779b31.png)           <br/> |![Check mark](media/f3b4c351-17d9-42d9-8540-e48e01779b31.png)           <br/> |
|**Edit data** - Users can edit all fields, except the Test Result and Test Date fields.  <br/> ||![Check mark](media/f3b4c351-17d9-42d9-8540-e48e01779b31.png)           <br/> |![Check mark](media/f3b4c351-17d9-42d9-8540-e48e01779b31.png)           <br/> |![Check mark](media/f3b4c351-17d9-42d9-8540-e48e01779b31.png)           <br/> |![Check mark](media/f3b4c351-17d9-42d9-8540-e48e01779b31.png)           <br/> |
|**Edit test results** - Users can edit the Test Result and Test Date fields.  <br/> |||![Check mark](media/f3b4c351-17d9-42d9-8540-e48e01779b31.png)           <br/> |![Check mark](media/f3b4c351-17d9-42d9-8540-e48e01779b31.png)           <br/> |![Check mark](media/f3b4c351-17d9-42d9-8540-e48e01779b31.png)           <br/> |
|**Manage assessments** - Users can create, archive, and delete Assessments.  <br/> ||||![Check mark](media/f3b4c351-17d9-42d9-8540-e48e01779b31.png)           <br/> |![Check mark](media/f3b4c351-17d9-42d9-8540-e48e01779b31.png)           <br/> |
|**Manage users** - Users can add other users in their organization to the Reader, Contributor, Assessor, and Administrator roles. Only those users with the Global Administrator role in your organization can add or remove users from the Portal Admin role.  <br/> |||||![Check mark](media/f3b4c351-17d9-42d9-8540-e48e01779b31.png)           <br/> |
   
### Guest access
  
After Compliance Manager access has been configured, any user that does not have a provisioned role is in the **Guest access** role by default (which is also the experience of any non-organization-provisioned accounts like personal Microsoft Accounts). Guest Access users do not have full access to all of the Compliance Manager features and are not able to see any of the organization's compliance assessment data, however they are able to use Compliance Manager to view Microsoft's compliance assessment reports and Service Trust documents. For an illustration of what is and is not accessible, see the images below where accessible features are outlined in blue and inaccessible features are outlined in red. 
  
![Compliance Manager Dashboard - guest access experience](media/7c9cb09d-ba13-4633-ad89-129a33e291f7.png)
  
![Compliance Manager - guest access graphic](media/11dade9e-557d-4a7f-ac2a-a5a1c0eaea93.png)