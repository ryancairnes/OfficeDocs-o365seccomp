---
title: "Protect information"
ms.author: bcarter
author: brendacarter
manager: laurawi
ms.date: 4/26/2019
ms.audience: Admin
ms.topic: hub-page
ms.service: O365-seccomp
localization_priority: Normal
search.appverid: 
- MOE150
- MET150
ms.assetid: a6ef28a4-2447-4b43-aae2-f5af6d53c68e
description: "landing page for protecting information"
---

# Protect information

Microsoft 365 and Office 365 include capabilities that can be applied to specific types of data to protect information. 


|**Capability**|**More information**|
|:-----|:-----|
|[Sensitivity labels](sensitivity-labels.md) <br/> |With sensitivity labels you can classify and help protect your sensitive content. Protection options include labels, watermarks, and encryption. Sensitivity labels use Azure Information Protection. If you are using Azure Information Protection labels, for now we recommend that you avoid creating new labels in other admin centers until after you've completed your migration. See [Azure Information Protection migration](https://docs.microsoft.com/en-us/azure/information-protection/configure-policy-migrate-labels). <br/> [Retention labels](retention-policies.md) are different than sensitivity labels. Retention labels help you retain or delete content based on policies that you define. These help organizations comply with industry regulations and internal policies.|
|[Data loss prevention](data-loss-prevention-policies.md) (DLP)  <br/> |With DLP policies, you can identify, monitor, and automatically protect sensitive information across Office 365. Data loss prevention policies can use sensitivity labels and sensitive information types to identify sensitive information. <br/> |
|[Sensitive information types](what-the-sensitive-information-types-look-for.md)  <br/> |DLP includes many sensitive information types that are ready for you to use in DLP policies. Sensitive information types define how the automated process recognizes specific information types such as health service numbers and credit card numbers.   <br/> |
|[Office 365 Message Encryption](ome.md) (OME)  <br/> |With Office 365 Message Encryption, your organization can send and receive encrypted email messages between people inside and outside your organization. Office 365 Message Encryption works with Outlook.com, Yahoo!, Gmail, and other email services. Email message encryption helps ensure that only intended recipients can view message content.  <br/> |
|[Azure Information Protection](https://docs.microsoft.com/en-us/azure/information-protection/)<br/> |If you are using sensitivity labels or Office Message Encryption, you are already using Azure Information Protection. If you have not yet migrated Azure Information Protection labels to Office 365, continue to manage these in Azure Information Protection.  <br/>The [Azure Information Protection scanner](https://docs.microsoft.com/en-us/azure/information-protection/deploy-aip-scanner) can be run on premises to classify and protect files on Windows Server, network shares, and SharePoint Server sites and libraries. This can be a first step toward identifying data to migrate to Office 365.
|Azure Information Protection with BYOK or HYOK solutions <br/> |Some organizations have a business need or compliance requirement to retain control of an encyption key on premises or in the cloud. This is not common. For more information, see [Hold your own key (HYOK) for Azure Information Protection](https://docs.microsoft.com/en-us/azure/information-protection/configure-adrms-restrictions) and [Bring your own key (BYOK) for Azure Information Protection](https://docs.microsoft.com/en-us/azure/information-protection/byok-price-restrictions). <br/> |
    

