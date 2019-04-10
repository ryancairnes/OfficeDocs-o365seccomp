---
title: "Microsoft Compliance Manager Overview"
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

# Microsoft Compliance Manager

> [!IMPORTANT]
> Microsoft Compliance Manager is a dashboard and management tool that provides a summary of your data protection and compliance stature and recommendations to improve data protection and compliance. The customer actions provided in Compliance Manager are recommendations; it is up to your organization to evaluate the effectiveness of these recommendations in their respective regulatory environment prior to implementation. Recommendations found in Compliance Manager should not be interpreted as a guarantee of compliance.

[Microsoft Compliance Manager](https://servicetrust.microsoft.com/ComplianceManager) is a workflow-based risk assessment tool included as a part of your Microsoft 365 or Office 365 subscription that is designed to help you manage regulatory compliance within the shared responsibility model of the Microsoft cloud. It provides you with a centralized dashboard for viewing standards, regulations, and assessments that outline Microsoft's control implementation details and test results, as well as tools allowing you to manage custom control implementations and compliance tracking for your organization.

With Compliance Manager, your organization can:
  
- Combine detailed compliance information Microsoft has provided to auditors and regulators about its cloud services with your own self-assessment of your organization's compliance with standards and regulations. These include standards and regulations outlined by the International Organization for Standardization (ISO), the National Institute of Standards and Technology (NIST), the Health Insurance Portability and Accountability Act (HIPAA), the General Data Protection Regulation (GDPR), and many others.
- Enables you to assign, track, and record compliance and assessment-related activities, which can help your organization cross team barriers to achieve your organization's compliance goals.
- Provides a Compliance Score to help you track your progress and prioritize the auditing controls that will help reduce your organization's exposure to risk.
- Provides a secure repository for you to upload and manage evidence and other artifacts related to your compliance activities.
- Produces richly detailed reports in Microsoft Excel that document the compliance activities performed by Microsoft and your organization, which can be provided to auditors, regulators, and other compliance stakeholders.

## Components

Overview and new component relationship artwork

### Groups

Groups are containers that allow you to logically organize *Assessments* and that share common information and workflow tasks between Assessments that have the same or related customer managed controls. This means that when two different Assessments in the same group share the same customer managed control, then the completion of implementation details, testing information, and status for the control in one Assessment are automatically synchronized to the same control in any other Assessment in the group. This helps unify the assigned customer actions for each control across the group and reduces potential duplicate customer action work. 

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

When you create a new Assessment, you're prompted to create a new group to assign the Assessment to or assign the Assessment to an existing group. However, it's recommend that your determine a grouping strategy for your organization *before* adding new assessments.

When working with groups, remember that:
  
- Group names (also called *Group IDs*) must be unique within your organization.
- Groups can contain Assessments for the same certification/regulation, but each group can only contain one Assessment for a specific cloud service/certification pair. For example, a group can't contain two Assessments for Office 365 and GDPR. Similarly, a group can contain multiple Assessments for the same cloud service as long as the corresponding certification/regulation for each one is different.
- Once an assessment has been added to an assessment grouping, the grouping cannot be changed. You can rename the assessment group, which changes the name of the assessment grouping for all of the assessments associated with that group. You can create a new assessment and a new assessment group and copy information from an existing assessment, which effectively creates a duplicate of that assessment in a different assessment group. Archiving an assessment breaks the relationship between that assessment and the assessment group; any further updates to other related assessments are no longer reflected in the archived assessment.

### Assessments

Assessments are logical structures based on the responsibility that is shared between Microsoft and your organization for assessing security and compliance risks in the Microsoft cloud services and for implementing the data protection safeguards specified by compliance standard and data protection standards, regulations, or laws. They help you discern your organization's data protection and compliance posture against the selected industry standard for the selected Microsoft cloud service. Assessments are completed by the implementation of the controls that map to the certification standard being assessed.
  
Assessments include several components:
  
- **In-Scope Services**: Each assessment applies to a specific set of Microsoft services, which are listed in the In-Scope Cloud Services section.
- **Microsoft Managed controls**: For each cloud service, Microsoft implements and manages a set of controls as part of Microsoft's compliance with various standards and regulations.
- **Customer anaged controls**: This is the collection of controls that are managed by your organization.
- **Assessment score**: 

You can export an Assessment to an Excel file, which can be reviewed by compliance stakeholders in your organization, and provided to auditors and regulators. This assessment report is a snapshot of the assessment as of the date and time that the report is created, and it contains the details of both the Microsoft-managed controls and the customer managed controls for that assessment, including control implementation status, control test date and test results, and provides links to the uploaded evidence documents.

When you have completed an Assessment and no longer need it for compliance purposes, you can archive it. When an Assessment is archived, it is removed from Assessments dashboard.
  
> [!NOTE]
> When an Assessment is archived, it cannot be 'unarchived' or restored to a read-write in progress state. Please note that archived Assessments do not retain their links to uploaded evidence documents, so it is highly recommended that you perform an Export of the Assessment before archiving it, as the exported assessment report will contain links to the evidence documents, enabling you to continue to access them.

### Controls

Controls are compliance process containers in Compliance Manager that define how you manage compliance activities. As previously mentioned, there are two types of controls in Compliance Manager:

- **Microsoft Managed Controls**: For each cloud service, Microsoft implements and manages a set of *controls* as part of Microsoft's compliance with various standards and regulations.
- **Customer Managed Controls**: This is the collection of controls that are managed by your organization. Your organization is responsible for implementing these 

### Actions

## Permissions

### Documents

### Templates

### Workflow

## Compliance Score

The Compliance Score, like the Microsoft Secure Score, is similar to other behavior-based scoring systems; your organization's activity can increase its Compliance Score by performing activities related to data protection, privacy, and security.
  
> [!NOTE]
> The Compliance Score does not express an absolute measure of organizational compliance with any particular standard or regulation. It expresses the extent to which you have adopted controls which can reduce the risks to personal data and individual privacy. No service can guarantee that you are compliant with a standard or regulation, and the Compliance Score should not be interpreted as a guarantee in any way. 
  
Assessments in Compliance Manager are based on the shared responsibility model for cloud computing. In the shared responsibility model, Microsoft and each customer share responsibility for the protection of the customer's data when that data is stored in our cloud.
  
As shown in the Office 365 GDPR Assessment below, Microsoft and customers are each responsible for performing a variety of Actions that are designed to satisfy the requirements of the standard or regulation being assessed. To rationalize and understand the required Actions across a variety of standards and regulations, Compliance Manager treats all standards and regulations as if they were control frameworks. Thus, the Actions performed by Microsoft and by customers for each Assessment involve the implementation and validation of various controls.

## Secure Score integration