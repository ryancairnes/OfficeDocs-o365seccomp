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
> Microsoft Compliance Manager is a dashboard and management tool that provides a summary of your data protection and compliance stature and recommendations to improve data protection and compliance. The customer actions provided in Compliance Manager are recommendations; it is up to your organization to evaluate the effectiveness of these recommendations in their respective regulatory environment prior to implementation. Recommendations found in Compliance Manager should not be interpreted as a guarantee of compliance. Compliance Manager isn't available in Office 365 operated by 21Vianet, Office 365 Germany, Office 365 U.S. Government Community High (GCC High), or Office 365 Department of Defense.

[Microsoft Compliance Manager](https://servicetrust.microsoft.com/ComplianceManager) is a workflow-based risk assessment tool included as a part of your Microsoft 365 or Office 365 subscription that is designed to help you manage regulatory compliance within the shared responsibility model of the Microsoft cloud. It provides you with a centralized dashboard for viewing standards, regulations, and assessments that outline Microsoft's control implementation details and test results, as well as tools allowing you to manage custom control implementations and compliance tracking for your organization.

With Compliance Manager, your organization can:
  
- Combine detailed compliance information Microsoft has provided to auditors and regulators about its cloud services with your own self-assessment of your organization's compliance with standards and regulations. These include standards and regulations outlined by the International Organization for Standardization (ISO), the National Institute of Standards and Technology (NIST), the Health Insurance Portability and Accountability Act (HIPAA), the General Data Protection Regulation (GDPR), and many others.
- Enables you to assign, track, and record compliance and assessment-related activities, which can help your organization cross team barriers to achieve your organization's compliance goals.
- Provides a Compliance Score to help you track your progress and prioritize the auditing controls that will help reduce your organization's exposure to risk.
- Provides a secure repository for you to upload and manage evidence and other artifacts related to your compliance activities.
- Produces richly detailed reports in Microsoft Excel that document the compliance activities performed by Microsoft and your organization, which can be provided to auditors, regulators, and other compliance stakeholders.

Overview and new component relationship artwork

### Groups

Groups are containers that allow you to logically organize *Assessments* and that share common information and workflow tasks between Assessments that have the same or related customer managed controls. This means that when two different Assessments in the same group share the same customer managed control, then the completion of implementation details, testing information, and status for the control in one Assessment are automatically synchronized to the same control in any other Assessment in the group. This helps unify the assigned customer actions for each control across the group and reduces potential duplicate customer action work. 

Learn more about working with Groups in Compliance Manager.

### Assessments

Assessments are logical structures based on the responsibility that is shared between Microsoft and your organization for assessing security and compliance risks in the Microsoft cloud services and for implementing the data protection safeguards specified by compliance standard and data protection standards, regulations, or laws. They help you discern your organization's data protection and compliance posture against the selected industry standard for the selected Microsoft cloud service. Assessments are completed by the implementation of the controls that map to the certification standard being assessed.

Learn more about working with Assessments in Compliance Manager.

### Controls

Controls are compliance process containers in Compliance Manager that define how you manage compliance activities. As previously mentioned, there are two types of controls in Compliance Manager:

- **Microsoft-managed Controls**: For each cloud service, Microsoft implements and manages a set of *controls* as part of Microsoft's compliance with various standards and regulations.
- **Customer-managed Controls**: This is the collection of controls that are managed by your organization. Your organization is responsible for implementing these 

### Actions

Actions are included in customer-managed controls as part of the built-in workflow management functionality that you can use to manage and track your organization's progress towards completing an assessment. 

The people involved in the assessment process in your organization can use Compliance Manager to review the customer managed controls from all Assessments for which they are users. When a user signs in to Compliance Manager and opens the **Action Items** dashboard, a list of Action Items assigned to them is displayed. Depending on the Compliance Manager role assigned to the user, they can provide implementation or test details, update the Status, or assign Action Items. 

As certification controls are generally implemented by one person and tested by another, the control action item can be initially assigned to one person for implementation, and once that is complete, that person can reassign the control action item to the next person for control testing and uploading of evidence. This assignment/reassignment of control actions can be performed by any users who have a Compliance Manager role with sufficient permissions, allowing for central management of control assignments, or decentralized routing of control action items, from implementer to tester as appropriate.

## Permissions

By default, everyone in your organization with an Office 365 or Azure AD account has access to Compliance Manager and can perform any action in Compliance Manager. To change from default permissions to the role-based access control model, at least one user must be added to each Compliance Manager role (see the following instructions). After a user is added to a role, the permissions to perform the actions assigned to that role are removed from the default set of permissions available to all users, and only users that have been provisioned that role will be able to access Compliance Manager and perform the actions allowed by that role.
  
Once role-based access has been implemented, any user that is not assigned to a defined Compliance Manager role will have Guest access.
  
> [!NOTE]
> To fully implement role-based access control to manage who can access and perform actions in Compliance Manager, a user must be added to each role to change the default permissions. For example, if you add a user to the role that lets users manage Assessments, only members of that role can manage Assessments. Similarly, if you don't add a user to the role that lets users read the data in Assessments, then all users in your organization can access Compliance Manager and read data in any Assessment. 
  
### Documents management

Documents related to related to performing implementation tasks and for performing testing and validation tasks in customer-managed controls can be uploaded to Compliance Manager.

Customer managed controls also have a place to manage documents that are related to performing implementation tasks and for performing testing and validation tasks. Anyone with permissions to edit data in Compliance Manager can upload documents by clicking **Manage Documents**. After a documented has been uploaded, you can click **Manage Documents** to view and download files. 

### Templates

### Workflow

## Compliance Score

The Compliance Score is a core component of the way that Compliance Manager helps your organization understand and manage compliance. The Compliance Score for an assessment is an expression of the company's compliance with a given standard or regulation as a number, where the higher the score (up to the maximum number of points allocated for the Assessment), the better the company's compliance posture. Understanding the compliance scoring methodology in which assessment controls are assigned risk severity values between 1- 10 (low to high), and how completed control assessments add to the total compliance score is crucial to organizations for prioritizing their actions.

The Compliance Score, like the Microsoft Secure Score, is similar to other behavior-based scoring systems; your organization's activity can increase its Compliance Score by performing activities related to data protection, privacy, and security.
  
> [!NOTE]
> The Compliance Score does not express an absolute measure of organizational compliance with any particular standard or regulation. It expresses the extent to which you have adopted controls which can reduce the risks to personal data and individual privacy. No service can guarantee that you are compliant with a standard or regulation, and the Compliance Score should not be interpreted as a guarantee in any way. 

## Secure Score integration

## Change log for Customer Managed Controls

Compliance Manager is designed to be regularly updated to keep pace with changes in regulatory requirements, as well as changes in our cloud services. These updates include changes to the Customer Managed Controls. A Change Log is provided to help you understand the impact of these changes, including the details of the content being added or changed, and guidance as to what effect the changes have on existing Assessments. Generally, there are two types of changes:
  
- A **Major** change is a significant change to a Customer Action, such as the addition or removal of a control or specific numbered steps, or a change in the guidance around responsibilities, recommendations, or evidence. For Major changes, we recommend that you re-evaluate your implementation and/or assessment of the affected control.
    
- A **Minor** change is an insignificant change to a Customer Actions, such as fixing a typo or formatting issues, or updating or correcting hyperlinks. Minor changes generally do not require the control to be re-evaluated; however, we do recommend that you review the updated Customer Action.

## Ready to get started?

## See also

- [Compliance Manager Interactive guide](https://content.cloudguides.com/guides/Compliance%20Manager)
- [Announcing Compliance Manager general availability](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Announcing-Compliance-Manager-general-availability/ba-p/161922)
- [Microsoft 365 provides an information protection strategy to help with the GDPR](https://blogs.office.com/en-us/2018/02/22/microsoft-365-provides-an-information-protection-strategy-to-help-with-the-gdpr)

