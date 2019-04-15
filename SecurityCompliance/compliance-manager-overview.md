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
> Compliance Manager isn't available in Office 365 operated by 21Vianet, Office 365 Germany, Office 365 U.S. Government Community High (GCC High), or Office 365 Department of Defense.

[Microsoft Compliance Manager](https://servicetrust.microsoft.com/ComplianceManager) is a dashboard and management tool that provides a summary of your data protection and compliance stature and recommendations to improve data protection and compliance. Included as a part of your Microsoft 365, Office 365, or Azure Active Directory subscription, it provides a workflow-based risk assessment tool designed to help you manage regulatory compliance within the shared responsibility model for Microsoft cloud services. It offers a centralized dashboard for viewing standards, regulations, and assessments that outline Microsoft's control implementation details and test results, as well as tools allowing you to manage custom control implementations and compliance tracking for your organization.

With Compliance Manager, your organization can:
  
- Combine detailed compliance information Microsoft has provided to auditors and regulators about its cloud services with your own self-assessment of your organization's compliance with standards and regulations. These include standards and regulations outlined by the International Organization for Standardization (ISO), the National Institute of Standards and Technology (NIST), the Health Insurance Portability and Accountability Act (HIPAA), the General Data Protection Regulation (GDPR), and many others.
- Enables you to assign, track, and record compliance and assessment-related activities, which can help your organization cross team barriers to achieve your organization's compliance goals.
- Provides a Compliance Score to help you track your progress and prioritize the auditing controls that will help reduce your organization's exposure to risk.
- Provides a secure repository for you to upload and manage evidence and other artifacts related to your compliance activities.
- Produces richly detailed reports in Microsoft Excel that document the compliance activities performed by Microsoft and your organization, which can be provided to auditors, regulators, and other compliance stakeholders.

> [!NOTE]
> The customer actions provided in Compliance Manager are recommendations; it is up to your organization to evaluate the effectiveness of these recommendations in their respective regulatory environment prior to implementation. Recommendations found in Compliance Manager should not be interpreted as a guarantee of compliance.

## Compliance Manager relationships

Compliance Manager use several components help you with your compliance management activities. These components work together to enable a complete management work flow and to make compliance reporting for audits easier and hassle-free. The chart below shows the relationship between the main components and the details for each are covered in following sections.

RELATIONSHIP ARTWORK

## Groups

Groups are containers that allow you to logically organize Assessments and that share common information and workflow tasks between Assessments that have the same or related customer managed controls. This means that when two different Assessments in the same group share the same customer managed control, then the completion of implementation details, testing information, and status for the control in one Assessment are automatically synchronized to the same control in any other Assessment in the group. This helps unify the assigned customer actions for each control across the group and reduce duplicating work for customer-managed Actions. Additionally, you can choose to use groups to organize Assessments by year, area, compliance standard, or other groupings to help organize your compliance work.

SECURITY PROPERTIES FOR GROUPS
ONLY CREATED IN ASSESSMENT
"DEFAULT GROUP" is default

Learn more about [working with Groups](working-with-compliance-manager) in Compliance Manager.

## Assessments

Assessments are containers that allow you to logically organize Controls based on the responsibility that is shared between Microsoft and your organization for assessing security and compliance risks in the Microsoft cloud services. Assessments help you implement data protection safeguards specified by a compliance standard and applicable data protection standards, regulations, or laws. They help you discern your organization's data protection and compliance posture against the selected industry standard for the selected Microsoft cloud service. Assessments are completed by the implementation of the controls included in the Assessment and that map to the certification standard being assessed.

DEFAULT ASSESSMENTS ASSIGNED??
 - Office 365 assesments (ISO 27001, NIST 800-53, GDPR)

Assessments include several components:
  
- **In-Scope Services**: Each assessment applies to a specific set of Microsoft services, which are listed in the In-Scope Cloud Services section.
- **Microsoft-managed controls**: For each cloud service, Microsoft implements and manages a set of controls as part of Microsoft's compliance with various standards and regulations.
- **Customer-managed controls**: This is the collection of controls that are implemented by your organization when you take the action(s) to each control.
- **Assessment Score**: The percentage of the total possible score for customer managed Controls in the Assessment.

Learn more about [working with Assessments](working-with-compliance-manager) in Compliance Manager.

## Controls

Controls are compliance process containers in Compliance Manager that define how you manage compliance activities. These controls are organized into control families that align with the structure from the corresponding certification or regulation that Assessments are aligned to. There are two types of controls in Compliance Manager, **Microsoft-managed controls** and **customer-managed controls**.

### Microsoft-managed controls
For each cloud service, Microsoft implements and manages a set of controls as part of Microsoft's compliance with various standards and regulations. Each provides details about how Microsoft implemented the control, along with how and when that implementation was tested and validated by an independent third-party auditor. Each Microsoft-managed control specifies the following information from the certification or regulation that maps to the control:

- **Control ID**: The section or article number from the certification or regulation that the control maps to.
- **Title**: The title from the corresponding certification or regulation.
- **Article ID**: This field is included only for GDPR assessments, as it specifies the corresponding GDPR article number.
- **Description**: Text of the standard or regulation that maps to the selected Microsoft managed control.

### Customer-managed controls
 This is the collection of controls that are managed by your organization. Your organization is responsible for implementing these controls as part of your compliance process for a given standard or regulation. Customer managed controls are also organized into control families for the corresponding certification or regulation. Use the customer managed controls to implement the recommended actions suggested by Microsoft as part of your compliance activities. Your organization can use the prescriptive guidance and recommended Customer Actions in each customer managed control to manage the implementation and assessment process for that control.

Customer-managed controls in Assessments also have built-in workflow management functionality that you can use to manage and track your organization's progress towards completing the Assessment. With this workflow functionality, you can:

- Assign tasks for each control
- Track assigned tasks
- Upload documentation evidence for the control task
- Document the testing and validation of the control
- Mark the control as implemented

For example, a Compliance Officer in your organization can assign an Action to an IT admin who has the responsibility and necessary permissions to perform the actions that are recommended for the control. When that work is complete, the IT admin can upload evidence of their implementation tasks (for example, screen shots of configuration or policy settings) and then assign the Action back to the Compliance Officer to evaluate the collected evidence, test the implementation of the control, and record the implementation date and test results in Compliance Manager.

Learn more about [working with Controls](working-with-compliance-manager) in Compliance Manager.

## Actions

Actions are included in customer-managed controls as part of the built-in workflow management functionality that you can use to manage and track your organization's progress towards completing an assessment.

People involved in the compliance assessment process in your organization can use Compliance Manager to review the customer managed controls from all Assessments for which they are assigned. When a user signs in to Compliance Manager and opens the **Action Items** dashboard, a list of Action Items assigned to them is displayed. Depending on the Compliance Manager role assigned to the user, they can provide implementation or test details, update the Status, or assign Action Items.

As certification controls are generally implemented by one person and tested by another, the control action item can be initially assigned to one person for implementation, and once that is complete, that person can reassign the control action item to the next person for control testing and uploading of evidence. This assignment/reassignment of control actions can be performed by any users who have a Compliance Manager role with sufficient permissions, allowing for central management of control assignments, or decentralized routing of control action items, from implementer to tester as appropriate.

Learn more about [working with Actions](working-with-compliance-manager) in Compliance Manager.

## Permissions

Compliance Manager uses a role-based access control permission model. By default, everyone in your organization with an Microsoft 365, Office 365, or Azure Active Directory (Azure AD) account has full access and can perform any action in Compliance Manager. Once role-based access has been implemented, any user that is not assigned to a defined Compliance Manager role will have guest access.

To change from default permissions and implement a fully role-based access control model, at least one user must be added to each Compliance Manager role. After a user is added to a role, the permissions to perform the actions assigned to that role are removed from the default set of permissions available to all users, and only users that have been provisioned that role will be able to access Compliance Manager and perform the actions allowed by that role. For example, if you add a user to the role that lets users manage Assessments, only members of that role can manage Assessments. Similarly, if you don't add a user to the role that lets users read the data in Assessments, then all users in your organization can access Compliance Manager and read data in any Assessment.
  
## Documents management

Documents related to related to implementation tasks and for performing testing and validation tasks in customer-managed controls can be uploaded to Compliance Manager. These documents are part of the Assessment that includes the customer-managed control and are available for view, export, and reporting to support auditing activities for the Assessment.

SUPPORTED FILE TYPES?? - no restrictions
LIMITS ON STORAGE SPACE?? - none
ANY RESTRICTIONS BASED ON SERVICE SUBSCRIPTION - gated by CM RBAC for your tenant

## Templates

Compliance Manager provides pre-configured templates for Assessments and allows you to create customized templates for customer-managed controls for your organization's compliance needs.

Create your own, can't customize built-in templates
 - 9-10 real ones, list from Scott
     - ISO 27001
     - ISO 27018
     - NIST 800-53
     - NIST 800-171
     - NIST CSF
     - Cloud Security Alliance (CSA) Cloud Control Matrix  (CCM) 3.0.1
     - Federal FFIEC Information Security 
     - HIPAA/HITECH
     - FedRAMP Moderate
     - EU GDPR
Add new templates from scratch, copy from template and modify, create an assessment on an existing template and then modify
Can only import from Excel file - any version

### Workflow

## Compliance Score

The Compliance Score is a core component of the way that Compliance Manager helps your organization understand and manage compliance. The Compliance Score for an assessment is an expression of the company's compliance with a given standard or regulation as a number, where the higher the score (up to the maximum number of points allocated for the Assessment), the better the company's compliance posture. Understanding the compliance scoring methodology in which assessment controls are assigned risk severity values between 1- 10 (low to high), and how completed control assessments add to the total compliance score is crucial to organizations for prioritizing their actions.

The Compliance Score, like the Microsoft Secure Score, is similar to other behavior-based scoring systems; your organization's activity can increase its Compliance Score by performing activities related to data protection, privacy, and security.
  
> [!IMPORTANT]
> The Compliance Score does not express an absolute measure of organizational compliance with any particular standard or regulation. It expresses the extent to which you have adopted controls which can reduce the risks to personal data and individual privacy. No service can guarantee that you are compliant with a standard or regulation, and the Compliance Score should not be interpreted as a guarantee in any way.

Learn more about how the [Compliance Score is calculated](compliance-score-methodology.md) in Compliance Manager.

## Secure Score integration

NEED DETAILS ABOUT INTEGRATION

## Updates for customer-managed controls

Compliance Manager is regularly updated to keep pace with changes in regulatory requirements and changes in our cloud services. These updates include changes to the customer-managed controls and a change log is provided to help you understand the impact of these changes. This log includes the details of the content being added or changed, and guidance as to what effect the changes have on existing Assessments. 

Generally, there are two types of changes:
  
- A **major** change is a significant change to a Customer Action, such as the addition or removal of a control or specific numbered steps, or a change in the guidance around responsibilities, recommendations, or evidence. For major changes, we recommend that you re-evaluate your implementation and/or assessment of the affected control.
- A **minor** change is an insignificant change to a Customer Actions, such as fixing a typo or formatting issues, or updating or correcting hyperlinks. Minor changes generally do not require the control to be re-evaluated. However, we do recommend that you review the updated Customer Action for minor changes.

Visit the [change log](need url) to view updates to Compliance Manager.

## Ready to get started?

## See also

- [Compliance Manager Interactive guide](https://content.cloudguides.com/guides/Compliance%20Manager)
- [Announcing Compliance Manager general availability](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Announcing-Compliance-Manager-general-availability/ba-p/161922)
- [Microsoft 365 provides an information protection strategy to help with the GDPR](https://blogs.office.com/en-us/2018/02/22/microsoft-365-provides-an-information-protection-strategy-to-help-with-the-gdpr)
