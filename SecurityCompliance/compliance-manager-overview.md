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
description: "Microsoft Compliance Manager is a free workflow-based risk assessment tool in the Microsoft Service Trust Portal. Compliance Manager enables you to track, assign, and verify regulatory compliance activities related to Microsoft cloud services."
---

# Microsoft Compliance Manager

> [!IMPORTANT]
> Compliance Manager isn't available in Office 365 operated by 21Vianet, Office 365 Germany, Office 365 U.S. Government Community High (GCC High), or Office 365 Department of Defense.

[Microsoft Compliance Manager](https://servicetrust.microsoft.com/ComplianceManager) is a free workflow-based risk assessment tool that lets you track, assign, and verify regulatory compliance activities related to Microsoft cloud services. Part of your Microsoft 365, Office 365, or Azure Active Directory subscription, Compliance Manager helps you manage regulatory compliance within the shared responsibility model for Microsoft cloud services. It offers a centralized dashboard for viewing standards, regulations, and assessments that outline control implementation details and test results for Microsoft services. It also includes tools allowing you to manage custom control implementations and compliance tracking specific to your organization.

With Compliance Manager, your organization can:
  
- Combine detailed compliance information Microsoft has provided to auditors and regulators about its cloud services with your compliance self-assessment for standards and regulations applicable for your organization. These include standards and regulations outlined by the International Organization for Standardization (ISO), the National Institute of Standards and Technology (NIST), the Health Insurance Portability and Accountability Act (HIPAA), the General Data Protection Regulation (GDPR), and many others.
- Enables you to assign, track, and record compliance and assessment-related activities, which can help your organization cross team barriers to achieve your organization's compliance goals.
- Provides a Compliance Score to help you track your progress and prioritize auditing controls that help reduce your organization's exposure to risk.
- Provides a secure repository for you to upload and manage evidence and other artifacts related to your compliance activities.
- Produces richly detailed Microsoft Excel reports that document compliance activities performed by Microsoft and your organization for auditors, regulators, and other compliance stakeholders.

> [!NOTE]
> The customer actions provided in Compliance Manager are recommendations; it is up to your organization to evaluate the effectiveness of these recommendations in their respective regulatory environment prior to implementation. Recommendations found in Compliance Manager should not be interpreted as a guarantee of compliance.

## Compliance Manager relationships

Compliance Manager uses several components help you with your compliance management activities. These components work together to provide a complete management work flow and hassle-free compliance reports for auditors.

RELATIONSHIP ARTWORK

## Groups

[Groups](working-with-compliance-manager) are containers that allow you to organize Assessments and share common information and workflow tasks between Assessments that have the same or related customer-managed controls. When two different Assessments in the same group share customer-managed control, then the completion of implementation details, testing information, and status for the control are automatically synchronized to the same control in any other Assessment in the group. This helps unify the assigned Action Items for each control across the group and reduce duplicating work. You can also choose to use groups to organize. Assessments by year, area, compliance standard, or other groupings to help organize your compliance work.

## Assessments

[Assessments](working-with-compliance-manager) are containers that allow you to organize Controls based on the responsibility shared between Microsoft and your organization for assessing security and compliance risks in the Microsoft cloud services. Assessments help you implement data protection safeguards specified by a compliance standard and applicable data protection standards, regulations, or laws. They help you discern your organization's data protection and compliance posture against the selected industry standard for the selected Microsoft cloud service. Assessments are completed by the implementation of controls included in the Assessment that map to the certification standard being assessed.

By default, Compliance Manager creates the following Assessments for your organization:

- Office 365 ISO 27001
- Office 365 NIST 800-53
- Office 365 GDPR

Assessments include several components:
  
- **In-Scope Services**: Each assessment applies to a specific set of Microsoft services, which are listed in the In-Scope Cloud Services section.
- **Microsoft-managed controls**: For each cloud service, Microsoft implements and manages a set of controls as part of Microsoft's compliance with various standards and regulations.
- **Customer-managed controls**: This is the collection of controls that are implemented by your organization when you take the action(s) to each control.
- **Assessment Score**: The percentage of the total possible score for customer-managed controls in the Assessment. This helps you track the implementation of the Actions assigned to each control.

## Controls

[Controls]((working-with-compliance-manager) are compliance process containers in Compliance Manager that define how you manage compliance activities. These controls are organized into control families that align with the structure from the corresponding certification or regulation that Assessments are aligned to.

- **Control ID**: The name of the selected control from the corresponding certification or regulation.
- **Control Title**: The title for the Control ID from the corresponding certification or regulation.
- **Article ID**: This field is included only for GDPR assessments, as it specifies the corresponding GDPR article number.
- **Description**: Text of control from the corresponding certification or regulation. For ISO certifications, a link to the relevant standard is provided due to copyright restrictions.

There are three types of controls in Compliance Manager, **Microsoft-managed controls**, **customer-managed controls**, and **Shared management controls**

### Microsoft-managed controls

For each cloud service, Microsoft implements and manages a set of controls as part of Microsoft's compliance with various standards and regulations. Each provides details about how Microsoft implemented the control, along with how and when that implementation was tested and validated by Microsoft and/or by an independent third-party auditor.

### Customer-managed controls

This is the collection of controls that are managed by your organization. Your organization is responsible for implementing these controls as part of your compliance process for a given standard or regulation. Customer-managed controls are also organized into control families for the corresponding certification or regulation. Use the customer-managed controls to implement the recommended actions suggested by Microsoft as part of your compliance activities. Your organization can use the prescriptive guidance and recommended customer actions in each customer-managed control to manage the implementation and assessment process for that control.

Customer-managed controls in Assessments also have built-in workflow management functionality that you can use to manage and track your organization's progress towards completing the Assessment. With this workflow functionality, you can:

- Assign Action Items for each control
- Track assigned Action Items
- Upload evidence of the implementation of the control
- Document the testing and validation of the control
- Mark the Action Items as implemented and tested

For example, a Compliance Officer in your organization can assign an Action Items to an IT admin who has the responsibility and necessary permissions to perform the recommended actions. When that work is complete, the IT admin uploads evidence of their implementation tasks (for example, screenshots of configuration or policy settings) and assigns the Action Items back to the Compliance Officer. The Compliance Officer evaluates the collected evidence, tests the implementation of the control, and records the implementation date and test results in Compliance Manager.

### Shared management controls

A shared control refers to any control where Microsoft and customers both share responsibilities for implementation. For example, controls related to personnel screening, account and password management, and encryption require actions to be taken by both Microsoft and customers.

## Action Items

[Actions Items](working-with-compliance-manager.md) are included in customer-managed controls as part of the built-in workflow management functionality that you can use to manage and track your organization's progress towards completing an assessment.

People involved in the compliance assessment process in your organization can use Compliance Manager to review the customer-managed controls from all Assessments for which they are assigned. When a user signs in to Compliance Manager and opens the **Action Items** dashboard, a list of Action Items assigned to them is displayed. Depending on the Compliance Manager role assigned to the user, they can provide implementation or test details, update the Status, or assign Action Items.

Certification controls are usually implemented by one person and tested by another. Action Items initially assigned to one person for implementation, and once that is complete, that person can reassign the Action Item to the next person for testing and uploading of evidence. This assignment/reassignment of Action Items can be performed by any users who have a Compliance Manager role with sufficient permissions, allowing for central management of control assignments, or decentralized routing of Action Items, from implementer to tester as appropriate.

## Permissions

Compliance Manager uses a role-based access control permission model. By default, everyone in your organization with Azure Active Directory (Azure AD) account has full access and can perform any action in Compliance Manager. Once role-based access control has been implemented by your organization, any user not assigned to a defined Compliance Manager role are assigned guest access.

To change from default permissions and implement a fully role-based access control model, at least one user must be added to each Compliance Manager role. After a user is added to a role, the permissions to perform the actions assigned to that role are removed from the default set of permissions available to all users, and only users that have been provisioned that role will be able to access Compliance Manager and perform the actions allowed by that role.

For example, if you add a user to the role that lets users manage Assessments, only members of that role can manage Assessments. Similarly, if you don't add a user to the role that lets users read the data in Assessments, then all users in your organization can access Compliance Manager and read data in any Assessment.
  
## Manage evidence

Compliance Manager can store evidence of your implementation tasks for performing testing and validation of customer-managed controls. Evidence includes documents, files, screenshots, images, scripts, script output files, etc. Compliance Manager also automatically receives telemetry and creates an evidence record for Action Items that are integrated with Secure Score.

## Templates

Compliance Manager provides pre-configured templates for Assessments and allows you to create customized templates for customer-managed controls for your organization's compliance needs. New templates can be created by importing controls information from an Excel file, or you can create a template from a copy of an existing template.

The pre-configured templates included with Compliance Manager are:
 
- [ISO 27001:2013](https://www.iso.org/obp/ui/#iso:std:iso-iec:27001:ed-2:v1:en)
- [ISO 27018:2019](https://www.iso.org/obp/ui/#iso:std:iso-iec:27018:ed-2:v1:en)
- [NIST 800-53](https://csrc.nist.gov/publications/detail/sp/800-53/rev-4/final)
- [NIST 800-171](https://csrc.nist.gov/publications/detail/sp/800-171/rev-1/final)
- [NIST Cybersecurity Framework (CSF)](https://www.nist.gov/cyberframework)
- [Cloud Security Alliance (CSA) Cloud Control Matrix  (CCM) 3.0.1](https://cloudsecurityalliance.org/working-groups/cloud-controls-matrix/#_overview)
- [Federal (FFIEC) Information Security Booklet](https://ithandbook.ffiec.gov/it-booklets/information-security.aspx) 
- [HIPAA](https://www.hhs.gov/hipaa/for-professionals/index.html / [HITECH](https://www.hhs.gov/hipaa/for-professionals/special-topics/hitech-act-enforcement-interim-final-rule/index.html)
- [FedRAMP Moderate](https://www.fedramp.gov/documents/)
- [European Union GDPR](https://eur-lex.europa.eu/legal-content/EN/TXT/HTML/?uri=CELEX:32016R0679&from=EN)

## Compliance Score

The [Compliance Score](compliance-score-methodology.md) is a core component of Compliance Manager that helps your organization understand and manage compliance. Like the [Microsoft Secure Score](microsoft-secure-score.md), the Compliance Score is a behavior-based scoring system for activities related to data protection, privacy, and security in your organization. The Compliance Score for an Assessment is an expression of compliance with a given standard or regulation. The higher the numeric score, the better the compliance posture for the Assessment. Understanding the compliance scoring methodology is crucial for prioritizing required customer-managed control actions.
  
> [!IMPORTANT]
> The Compliance Score does not express an absolute measure of organizational compliance with any particular standard or regulation. It expresses the extent to which you have adopted controls which can reduce the risks to personal data and individual privacy. No service can guarantee that you are compliant with a standard or regulation, and the Compliance Score should not be interpreted as a guarantee in any way.

## Secure Score integration

Compliance Manager is integrated with Microsoft Secure Score to automatically apply Secure Score credit to the Compliance Score for synced Action Items.

## Ready to get started?

Start [working with Compliance Manager](working-with-compliance-manager.md) to manage regulatory compliance activities for your organization.

## Resources

- [Interactive guide: Assess and enhance your data protection controls with Compliance Manager](https://content.cloudguides.com/guides/Compliance%20Manager)
- [Microsoft Security, Privacy, and Compliance Tech Community](https://techcommunity.microsoft.com/t5/Security-Privacy-Compliance/ct-p/SecurityPrivacyCompliance)
