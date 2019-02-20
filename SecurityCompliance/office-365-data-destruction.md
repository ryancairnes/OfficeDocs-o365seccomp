---
title: "Office 365 Data Destruction"
ms.author: robmazz
author: robmazz
manager: laurawi
audience: ITPro
ms.topic: article
ms.service: Office 365 Administration
localization_priority: None
search.appverid:
- MET150
ms.collection:
- Strat_O365_IP
- M365-security-compliance
description: "An overview of Microsoft's policies regarding the recycling, disposal, or destruction of Office 365 datacenter disk drives and servers."
---

# Office 365 Data Destruction

## Physical data destruction

Microsoft has Data Handling Standard policies that addresses recycle and disposal of disk drives and failed or retiring servers. Before re-using any disk drives within Office 365, Microsoft performs a physical sanitization process that is consistent with National Institute of Standards and Technology Special Publication 800-88 ([NIST SP 800-88 Guidelines for Media Sanitization](http://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-88r1.pdf)). All disk drives in Office 365 are encrypted using BitLocker volume level encryption, so in practice, NIST SP 800-88-compliant erasure is not necessary. Nonetheless, it is still performed by Microsoft.

Failed disks used within Office 365 datacenters are physically destroyed and audited through the ISO process. The appropriate means of disposal is determined by the asset type. For hard drives that can't be wiped, Microsoft uses a destruction process that destroys the media (e.g., disintegrates, pulverizes, or incinerates) and renders the recovery of information impossible. Microsoft also retains all records of the destruction. Microsoft performs a similar sanitization process on servers that are being re-used within Office 365. These guidelines encompass both electronic and physical sanitization.

Disk drives that cannot be re-used are disposed of using a physical destruction process that is performed on-site within the datacenter containing the disks being destroyed. Storage media designated for disposal are placed in secure bins located in each area of the datacenter. Each secure bin station is monitored by video surveillance. Once a disposal bin reaches approximately 50% capacity, the Site Services team contacts the Physical Security team to coordinate its removal. Site Services personnel then remove the disposal bin under escort by a Security Officer until it is placed in a secured storage area to await data destruction. Policies and procedures governing the handling of data bearing devices during disposal are routinely tested including procedures to ensure the condition of machinery approved for destruction.

In the data destruction process, the disk is first erased in a manner that is compliant with NIST 800-88 (if possible), and then it is placed into an industrial shredder and physically demolished. Microsoft maintains accountability for assets leaving the datacenter using NIST SP 800-88 consistent cleansing/purging, asset destruction, encryption, accurate inventorying, tracking, and protection of chain of custody during transport. This process is monitored via closed-circuit television and a Certificate of Destruction is issued upon completion.

Microsoft uses data erasure units from [Extreme Protocol Solutions](http://www.enterprisedataerasure.com/) (EPS). EPS software supports NIST SP 800-88 requirements for cleansing and purging/secure erasure. Prior to cleansing or destruction, an inventory is created by the Microsoft asset manager. If a vendor is used for destruction, the vendor provides a certificate of destruction for each asset destroyed, which is validated by the asset manager.

## Virtual data destruction

Microsoft has data handling policies and procedures that also address effective virtual destruction of data to protect against the possibility of data being inappropriately shared between service tenants, or being accessible after hard deletion in the service. Data that is deleted from the service in one tenant is not accessible to another service tenant even if some or all of the same underlying physical storage is later reassigned. This is an outcome of the compounded effects of multiple virtualization and fragmentation technologies used to scale virtual environments, the active delete behaviors of applications within each service tenant (such as [page zeroing](https://docs.microsoft.com/office365/securitycompliance/office-365-exchange-online-data-deletion#page-zeroing)), and the required media and application content encryption processes.