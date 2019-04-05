---
title: "Attributes for information barrier policies"
ms.author: deniseb
author: denisebmsft
manager: laurawi
ms.date: 04/04/2019
ms.audience: ITPro
ms.topic: article
ms.service: O365-seccompms.collection:
- M365-security-compliance
localization_priority: None
description: "Use this article as a reference for various attributes you can use in information barrier policies."
---

# Attributes for information barrier policies (Preview)

[Information barriers](information-barriers.md) can be defined using certain attributes in Azure Active Directory. Use the following table as a reference of attributes for [information barrier policies](define-information-barriers-policies.md).


|Azure Active Directory property name (LDAP display name)  |Exchange property name  |Value type  |
|---------|---------|---------|
|Co       | Co        | String        |
|Company     |Company         |String         |
|Department     |Department         |String         |
|ExtensionAttribute1 |CustomAttribute1 |String |
|ExtensionAttribute2 |CustomAttribute2 |String |
|ExtensionAttribute3 |CustomAttribute3 |String |
|ExtensionAttribute4 |CustomAttribute4 |String |
|ExtensionAttribute5 |CustomAttribute5 |String |
|ExtensionAttribute6 |CustomAttribute6 |String |
|ExtensionAttribute7 |CustomAttribute7 |String |
|ExtensionAttribute8 |CustomAttribute8 |String |
|ExtensionAttribute9 |CustomAttribute9 |String |
|ExtensionAttribute10 |CustomAttribute10 |String |
|ExtensionAttribute11 |CustomAttribute11 |String |
|ExtensionAttribute12 |CustomAttribute12 |String |
|ExtensionAttribute13 |CustomAttribute13 |String |
|ExtensionAttribute14 |CustomAttribute14 |String |
|ExtensionAttribute15 |CustomAttribute15 |String |
|MSExchExtensionCustomAttribute1 |ExtensionCustomAttribute1 |String |
|MSExchExtensionCustomAttribute2 |ExtensionCustomAttribute2 |String |
|MSExchExtensionCustomAttribute3 |ExtensionCustomAttribute3 |String |
|MSExchExtensionCustomAttribute4 |ExtensionCustomAttribute4 |String |
|MSExchExtensionCustomAttribute5 |ExtensionCustomAttribute5 |String |
|MailNickname |Alias |String |
|PhysicalDeliveryOfficeName |Office |String |
|PostalCode |PostalCode |String |
|ProxyAddresses |EmailAddresses |String |
|StreetAddress |StreetAddress |String |
|TargetAddress |ExternalEmailAddress |String |
|UsageLocation |UsageLocation |A valid two-letter country/region ISO 3166 value, or the corresponding display name (for example, US or UnitedStates). For more information, see [Country Codes - ISO 3166](https://go.microsoft.com/fwlink/p/?linkid=213779). |
|UserPrincipalName	|UserPrincipalName	|String |
|Mail	|WindowsEmailAddress	|String |
|Description	|Description	|String |
|MemberOf	|MemberOfGroup	|String (can be DistinguishedName, ExternalDirectoryObjectId or ProxyAddress)|

## Related topics

[Define policies for information barriers in Microsoft Teams (Preview)](define-information-barriers-policies.md)

[Information barriers (Preview)](information-barriers.md)



