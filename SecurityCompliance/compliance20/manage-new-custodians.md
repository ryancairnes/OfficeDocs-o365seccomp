---
title: "Manage custodians in an Advanced eDiscovery (Preview) case"
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
# Manage custodians in an Advanced eDiscovery (Preview) case

The Custodians tab contains a sortable list of all the custodians in the case. After you add custodians to a case, details about each custodian will automatically be collected from Azure Active Directory.

## Viewing custodian details

The flyout page that contains custodian details appears after you add a custodian to a case and select them from the list on the **Custodians** tab. From here, you can view all the details related to that custodian. The flyout page contains the following fields:

- Contact information

  - **Display Name**: The name displayed in the address book for the custodian. This is usually the combination of the custodian’s first name, middle initial and last name.
  - **Mail/SMTP**: The SMTP address for the custodian, for example, jeff@contoso.onmicrosoft.com.  
  - **Title**: The custodian’s job title.
  - **Department**: The name for the department in which the custodian works.
  - **Manager**: The custodian’s manager. The designated manager will receive any Escalation communications for this custodian.
  
- Location information

  - **City**: The city in which the custodian is located.
  - **State**: The state or province in the custodian’s address.
  - **Country/Region**: The country/region in which the custodian’s is located; for example, “US” or “UK”.
  - **Office**: The office location in the custodian’s place of business.

- Case information

  - **Hold status**: Indicates if the custodian has been placed on hold. 
  - **Communication status**: Indicates if the custodian has been issued a hold notice. If the custodian has been issued a notice, then this will be marked as *Published*. If the custodian has not been issued a notice, then this status will be *Un-Published*. 
  - **Status**: The status of the custodian within the case. This will be *Active* if the custodian is still on hold for the case. If a custodian is removed from a case, their status will change to *Released*. 

- Processing status

  - **Indexing status**: Indicates the status of the deep indexing job.  
  - **Indexing Last Updated Time**: Indicates the datestamp of when the deep indexing job was last triggered.
  - **Data sources**: Shows the count of mailboxes, sites, and Teams that have been selected for the custodian.

## Updating a custodian

As your case progresses, you may discover that there may be additional data sources relevant to a specific custodian & your case. In other scenarios, you may want to remove certain data sources that have been reviewed and deemed as not relevant.

To update a custodian and the selected data sources:

1. Select an existing case from the **eDiscovery > Advanced eDiscovery (Preview)**.
  
2. In the case, click the **Custodians** tab.
  
3. Select the custodian(s) from the list and click **Edit sources**.
  
4. Update selections for Exchange and OneDrive locations by clicking **Choose data sources**.
  
5. Add or remove Teams, SharePoint, or Exchange mailboxes mapped the user by clicking to **Select additional data sources**. For more information about how you to map data sources to a custodian, see [Add custodians to a case](add-custodians-to-case.md).
  
6. To update the custodian hold status, click **Place custodial holds**, and enable or disable the hold for custodians.

> [!TIP]
> You can select multiple custodians to perform bulk actions, like re-indexing, releasing, or editing a set of custodians.

## Resolving custodian processing errors

In most Legal workflows, after custodians are added for a specific investigation, a subset of the users’ data will be searched. Due to large file sizes or possible corruption, some items within the custodians’ data sources may be partially indexed. Using the Advanced eDiscovery (Preview) deep indexing capability, these partially indexed items can be automatically remediated by re-crawling and re-indexing these items on demand. 

When a custodian is added to a case, their data will automatically be "deep indexed”, allowing users to leave these partially indexed items in place instead of having to download, remediate and re-run searches outside of Office 365. During the lifecycle of a case, a user may remediate items or add new data sources for a given custodian. This may require the Custodian Index to be updated. 

To trigger a re-indexing process to address partially indexed items:

1. Go to **eDiscovery > Advanced eDiscovery (Preview)** and select an existing case.

2. In the case, click to **Custodians tab**. 

3. Select the custodian(s) that needs to be re-indexed, and then click **Update index** on the flyout page.

4. Check the status of the custodian index by clicking the link in the **Indexing job Status** column on the **Custodians** tab.  

5. The status for the re-indexing process can also be tracked on the **Jobs** tab.

For more information about re-indexing and remediating partially indexed items, see [Fix processing errors](processing-data-for-case.md).

## Releasing a custodian from a case

A custodian is released in situations where a case is closed, a custodian is no longer under obligation to preserve content for a case, or when a custodian is deemed to no longer be relevant to a particular case. 

If you release a custodian after a hold notice was published, a release notice will be sent to the custodian. In addition, any custodial holds attributed to the released custodians will also be removed.

If the custodian was placed on a silent hold, where they were not issued any legal hold notifications, then any custodial holds attributed to the released custodians will be removed.  

To release a custodian: 

1.	Go to the **Custodians** tab.

2.	Select the custodian from the list and click **Release custodians** on the flyout page.

    The status of the custodian on the **Custodians** tab is set to **Released** and the **Hold status** on the flyout page is changed to **Inactive**. 

> [!TIP]
> A custodian might be simultaneously be involved in several legal hold matters. When a custodian is released from a case, the holds and notifications across other matters will not be impacted.

## Related information

 - [Error remediation when processing data](error-remediation.md) 
- [Work with communications](managing-custodian-communications.md)
