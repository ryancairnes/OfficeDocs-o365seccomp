---
title: "Microsoft Compliance Manager Release Notes"
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
description: "Microsoft Compliance Manager is a free workflow-based risk assessment tool in the Microsoft Service Trust Portal. Compliance Manager enables you to track, assign, and verify regulatory compliance activities related to Microsoft cloud services."
---

# Release notes for Compliance Manager (Version 3 Preview)

You can use the updated [Compliance Manager (Version 3 Preview)](https://servicetrust.microsoft.com/ComplianceManager) tool on the [Service Trust Portal](https://servicetrust.microsoft.com) to track, assign, and verify regulatory compliance activities related to Microsoft cloud services. The Public Preview of Compliance Manager provides you with early access to the upcoming functionality and updates.

## What’s new in Compliance Manager Version 3 Preview

- **Integration with Microsoft Secure Score**: Compliance Manager supports integration with [Microsoft Secure Score](microsoft-secure-score.md) by mapping customer-managed Actions to almost 100 Secure Score actions. When you complete a mapped action in Secure Score, the corresponding Compliance Manager Action automatically completes.

- **Templates**: In addition to the standard Assessment templates available in previous versions, Compliance Manager now supports importing custom templates from Excel workbooks.

- **Actions Items**: Action Items are now individual items and most include telemetry collection from the Microsoft Secure Score Graph API. Where possible, technical action recommendations now have links to the applicable configuration page in the Office 365 service.

- **Ownership**: A responsible party is defined for Controls and Action Items as an Owner, mirroring the Responsible Party in Microsoft Trust Tools. One or more people or teams are assigned responsibility for Control implementation.

- **Dimensions**: New metadata for Action Items that allows configuring custom pivots for filters.

- **Compliance Score**: The methodology has changed to support syncing with Microsoft Secure Score. The scoring system removes the Microsoft-managed control credits and focuses solely on the completion of customer-managed controls. Multiple dimensions are used to calculate the score on a per-action basis. Compliance score data is a requirement for each template and Assessment.

- **In-scope Services**: In-scope Services are added to the data schema and are now a requirement for each template and Assessment.

- **Separate Excel workbooks**: Each template and Assessment have independent Excel workbooks with six tabs for easier mapping across multiple standards. The new tabs are:
    - Template-Assessment
    - Controls
    - Actions
    - Ownership
    - Dimensions
    - Microsoft

## Known issues

For general information about Compliance Manager v3 Public Preview, LINK TO MAIN TOPIC

The following sections cover known issues that are intended to be resolved in an upcoming release of Compliance Manager v3.

### Compliance Score

When Actions are marked as Not in Scope, the score assigned to the Action is not excluded from the Compliance Score calculation. Actions marked Not in Scope should not increase your Compliance Score.

### Customization

Adding custom Controls enables you to add a new control to an existing control family, but it does not allow you to add a new Control Family.

The Public Preview release does not support linking Actions or adding Actions or Controls to an Assessment.

### Filters

Filtering on Action Items or Controls does not consistently produce correct results.

### Locking and Archiving

Archived Templates can be edited, and they should not be editable. Similarly, locked Templates allow for Assessment creation when they should not. Locking a Template is meant to prevent it from being used to create Assessments.

### Exporting

Exporting a Template to JSON fails when the Template’s status is set to Imported or Pending Approval.

### Supported Browsers

The latest versions of Microsoft Edge, Chrome, and Safari are supported. The preview version of Microsoft Edge is not supported but has no known issues. Internet Explorer is not supported in Compliance Manager Public Preview. Note that there may be instances where updated data does not appear until your browser is refreshed.