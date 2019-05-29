---
title: "Attributes for information barrier policies"
ms.author: deniseb
author: denisebmsft
manager: laurawi
ms.date: 05/28/2019
ms.audience: ITPro
ms.topic: article
ms.service: O365-seccomp
ms.collection:
- M365-security-compliance
localization_priority: None
description: "Use this article as a reference for various attributes you can use in information barrier policies."
---

# Attributes for information barrier policies (Preview)

Certain attributes in Azure Active Directory can be used to segment users. Segments are then used as filters for information barrier policies. For example, you might use **Department** to define segments of users by department within your organization (assuming no single employee works for two departments at the same time). 

This article provides a list of attributes that can be used. To learn more about information barriers, see the following resources:
- [Information barriers (Preview)](information-barriers.md)
- [Define policies for information barriers in Microsoft Teams (Preview)](information-barriers-policies.md)

## How to use attributes in information barrier policies

The attributes listed in this article can be used to define (or edit) segments of users. Segments are used as parameters (UserGroupFilter) in information barrier policies.

Examples:

`New-OrganizationSegment -Name "Segment1" -UserGroupFilter "Department -eq 'Department1'"`

`New-OrganizationSegment -Name "SegmentA" -UserGroupFilter "MemberOf -eq 'BlueGroup'"`

When you define segments, use the same attribute for all your segments. For example, if you define some segments using *Department*, define all of the segments using *Department*. Don't define some segments using *Department* and others using *MemberOf*. Make sure your segments do not overlap; each user should be assigned to exactly one segment. 

To learn more, see [Define segments using PowerShell](information-barriers-policies.md#define-segments-using-powershell).

## Reference

The following table lists the attributes that you can use with information barriers.

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

[Define policies for information barriers in Microsoft Teams (Preview)](information-barriers-policies.md)

[Troubleshooting information barriers (Preview)](information-barriers-troubleshooting.md)

[Information barriers (Preview)](information-barriers.md)



