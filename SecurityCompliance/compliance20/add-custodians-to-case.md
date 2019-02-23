---
title: "Add custodians to an Advanced eDiscovery (Preview) case"
ms.author: markjjo
author: markjjo
manager: laurawi
ms.date: 
ms.audience: Admin
ms.topic: article
ms.service: O365-seccomp
localization_priority: Normal
ms.collection: 
search.appverid: 
- MOE150
- MET150
ms.assetid: 

description: ""
---
# Add custodians to an Advanced eDiscovery (Preview) case

Using Advanced eDiscovery (Preview), you can leverage the built-in custodian management tool to coordinate your workflows around managing custodians and identifying relevant, custodial data sources within a case. When you add a custodian, the system can automatically identify, and place holds on their primary Exchange mailbox and OneDrive for Business site. As you conduct your discovery, you might also uncover and map additional mailboxes or sites that a custodian accessed in the past or Teams that a custodian is a member of today.

Use the following workflow to add and manage custodians in Advanced eDiscovery (Preview) cases within the Security & Compliance Center. 

## Step 1: Identify potential custodians

The first step is to identify the appropriate custodians for your matter. To add custodians to a case, you must be a member of the eDiscovery Managers or eDiscovery Admins role group.   

To add custodians to an existing Advanced eDiscovery (Preview) case:

1. From the **Advanced eDiscovery (Preview)** page, go to your case.
 
2. After you have selected a case, go to the **Custodians** tab and click **+ Add Custodian**. 
 
3. Choose the custodians that you want to add to the case. You can start by typing to search and select the users from your organization's Azure Active Directory.
 
4. After you have finalized the list of custodians, click **Next** to begin identifying potential data sources. 
   
## (Optional) Step 2: Select custodian data sources

After you have added custodians to a case, you can leverage Office 365 to help you identify and preserve the primary custodian data sources. The next step in this workflow is to select the data sources owned by the custodians specified in Step 1. 

To identify custodian data sources: 

1. For each custodian, select **Exchange** if you would like the system to automatically identify and add the custodian's primary Exchange mailbox. 
 
2. For each custodian, select **OneDrive** if you would like the system to automatically identify and add the custodian's primary OneDrive URL. 

    After you've made your selections, they system will automatically try to identify the data sources and add them to your case.
 
4. Click **Next** to begin mapping additional data sources to your custodian.

## (Optional) Step 3: Map additional data sources

Depending on your case, you may also want to add mailboxes that a given custodian may have used in the past, groups where a custodian is currently a member, or sites that a custodian had access to in the past. In addition to primary custodian data sources, you can add additional Office 365 data sources to a custodian or leverage Office 365 to help you identify potentially relevant data sources as well. 

To map mailboxes, sites, or teams to a specific custodian:

1. Select **Update** to assign content locations, like mailboxes, sites, and Teams to a specific custodian. 

2. In the flyout, specify the following:
   
  -  **Exchange Mailboxes** - Click **Choose users, groups, or Teams** and then click **Choose users, groups, or teams** again. To specify mailboxes to assign to the selected custodian, use the search box to find user mailboxes and distribution groups. You can also assign the associated mailbox for an Office 365 Group or a Microsoft Team. Select the user, group, team check box, click **Choose**, and then click **Done**.

      > [!NOTE]
      > When you click Choose users, groups, or teams to specify mailboxes, the mailbox picker that's displayed is empty. This is by design to enhance performance. To add people to this list, type a name (a minimum of 3 characters) in the search box.
     
   - **SharePoint Sites** - Click **Choose sites** and then click **Choose sites** again to specify additional SharePoint and OneDrive for Business sites that you would like to assign to the selected custodian. You can also add the URL for the SharePoint site for an Office 365 Group or a Microsoft Team. Type the URL for each site that you want to assign. Click **Choose**, and then click **Done**.
   - **Microsoft Teams** – Click **Choose Teams** and then click **Choose Teams** again to view a list of Microsoft Team groups that the custodian is a member of today. Select the Teams that you would like to add to your custodian. Once selected, the system will automatically identify & select the associated SharePoint site and Group Mailbox associated to that Microsoft Team. Click **Choose**, and then click **Done**.
        
      > [!NOTE]
      > To add additional Microsoft Teams, you will need to separately add the mailbox and SharePoint site as shown above.

After you have finished mapping your sources, you can view the total mailboxes, sites, and Teams for the custodians that you have just added. When you've finalized the data sources relevant for a specific custodian, this mapping will be maintained and extended to the eDiscovery collection, processing, and review workflows. 

## (Optional) Step 4: Place custodians on hold

 After you have finalized the custodians and data sources that you would like to add to your case, you can optionally place some or all of your custodians on hold. When you place a custodian on hold, the content mapped to that user is held until you release the custodian from the case or until you delete the hold. In some cases, you may want to add custodians to a case without placing them on hold. 

To place the selected custodians and data sources on hold:

1. Verify your custodian selections and select the checkbox to place each custodian on hold.Once a custodian is placed on hold, a custodian hold policy containing all custodial sources will automatically be created. If the option is not checked, the custodian & selected data sources will be added to the case but the content will not be preserved.

2. Go to the **Holds** tab and select the **Custodian Hold Policy**. 

3. Click **Edit** to view all the selected custodian data sources.
