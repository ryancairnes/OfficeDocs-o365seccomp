---
title: "Automated Investigation and Response (AIR) with Office 365 Threat Intelligence"
ms.author: deniseb
author: denisebmsft
manager: laurawi
ms.date: 03/21/2019
ms.audience: ITPro
ms.topic: article
ms.service: O365-seccomp
localization_priority: Normal
search.appverid:
- MET150
- MOE150
ms.collection: M365-security-compliance
description: "Learn about Automated Investigation and Response capabilities in Office 365 Advanced Threat Protection."
---

# Automated Investigation and Response (AIR) with Office 365 Threat Intelligence

Automated Investigation and Response (AIR) (coming soon to [Office 365 Threat investigation and response capabilities](office-365-ti.md)) enables you to run automated investigation and remediation to well-known threats that exist today. Read this article to get an overview of AIR and how it can help your organization mitigate threats more effectively and efficiently. Tolearn more about when AIR will be available, see the [Microsoft 365 Roadmap](https://www.microsoft.com/microsoft-365/roadmap).

## Alerts

[Alerts](alert-policies.md#viewing-alerts) represent triggers for Security Operations team workflows for incident response. Prioritizing the right set of alerts for investigation while making sure no threats are unaddressed is challenging. When investigations into alerts are performed manually, Security Operations teams must hunt and correlate entities (e.g. content, devices and users) at risk from threats. Such tasks and workflows are very time consuming and involve multiple tools and systems. With AIR, investigation and response are automated into key security and threat management alerts that trigger your security response playbooks automatically. 

To view alerts, in the Office 365 Security & Compliance Center, choose **Alerts** > **View alerts**.

![Alerts that link to investigations](media/air-alerts-page-details.png) 

Select an alert to view its details, and from there, use the **View investigation** link to go to the corresponding [investigation](#investigation-graph).

## Security playbooks

Security playbooks are back-end policies that are at the heart of automation in Microsoft Threat Protection. The security playbooks provided in AIR are based on common real-world security scenarios. A security playbook is launched automatically when an alert is triggered within your organization. Once the alert triggers, the associated playbook is run automatically. The playbook runs an investigation, looking at all the associated metadata (including email messages, users, subjects, senders, etc.) and, based on its findings, recommends a set of actions that your organization's security team can take to control and mitigate the threat. 

The security playbooks you'll get with AIR are designed to tackle the most frequent threats that organizations face today. They're based on input from Security Operations and Incident Response teams, including those who help defend Microsoft assets.

### Security playbooks are rolling out in phases

As part of AIR, security playbooks are rolling out in phases

- **Phase 1 (April 2019)**: Playbooks include recommendations that security administrators review and approve. 

- **Phase 2 (June 2019)**: Security administrators will have the option to allow security playbooks to take action automatically, without administrative interaction.

Phase 1 will include the following playbooks:
- User-reported phish message
- URL click verdict change and ATP Safe Links block override
- Malware ZAP
- Phish ZAP
- Manual investigations (using Explorer)

Several more playbooks are planned for Phase 2.

### Playbooks include investigation and recommendations

Each playbook includes: 
- a root investigation, 
- steps to hunt down other potential threats, and 
- recommended threat remediation.

Each high-level step includes many sub-steps that are executed to provide a deep, detailed, and exhaustive response to threats.

## Example: User-reported phish message

When a user in your organization submits an email message and reports it to Microsoft by using the [Report Message add-in for Outlook or Outlook Web Access](enable-the-report-message-add-in.md). This triggers a system-based informational alert that automatically launches the investigation playbook.

During the root investigation phase, various aspects of the email are assessed. These include:
- A determination about what type of threat it might be;
- Who sent it;
- Where the email was sent from (sending infrastructure);
- Whether other instances of the email were delivered or blocked;
- An assessment from our analysts;
- Whether the email is associated with any known campaigns;
- and more.

After the root investigation is complete, the playbook provides a list of recommended actions to take.
  
Next, several hunting steps are executed:

- Similar email messages in other email clusters are searched.
- The signal is shared with other platforms, such as [Windows Defender ATP](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-atp/windows-defender-advanced-threat-protection).
- A determination is made on whether any users have clicked through on the suspicious email message.
- A check is done across Office 365 [EOP](eop/exchange-online-protection-eop.md) and [ATP](office-365-atp.md) to see if there are any other similar messages reported by users.
- A check is done to see if a user has been compromised. This check leverages signals across [Microsoft Cloud App Security](https://docs.microsoft.com/cloud-app-security) and [Azure Active Directory](https://docs.microsoft.com/azure/active-directory), correlating any related events or alerts. 

During the hunting phase, risks and threats are assigned to various hunting steps.  

Remediation is the final phase of the playbook. During this phase, remediation steps are taken, based on theinvestigation and hunting phases.  

## Getting started

To access your investigations, as an Office 365 global administrator or security administrator, Go to the Office 365 Security & Compliance Center ([https://protection.office.com](https://protection.office.com)) and sign in. Then, do one of the following:

- In the left navigation, go to **Threat management** > **Investigations**.

    or

- Visit the Threat management dashboard (In the Security & Compliance Center, go to **Threat management** > **Dashboard**).

![AIR widgets](media/air-widgets.png)

Your AIR widgets will appear across the top of the [Security Dashboard](security-dashboard.md). Select a widget to get started.

### Automated investigations

The automated investigations page shows your organization's investigations and their current states.

![Main investigation page for AIR](media/air-maininvestigationpage.png) 
  
You can:
- Navigate directly to an investigation (select an **Investigation ID**).
- Apply filters. Choose from **Investigation Type**, **Time range**, **Status**, or a combination of these.
- Export the data to a CSV file.

### Investigation graph

When you open a specific investigation, you see the investigation graph page. This page shows all the different entities: email messages, users (and their activities), and devices that were automatically investigated as part of the alert that was triggered.

![AIR investigation graph page](media/air-investigationgraphpage.png)

You can:
- Get a visual overview of the current investigation.
- View a summary of the investigation timings.
- Select a node in the visualization to view details for that node.
- Select a tab across the top to view details for that tab.

### Alert investigation

On the **Alerts** tab for an investigation, you can see all of the alerts relevant to the investigation. Details include the alert that triggered the investigation and other alerts, such as risky sign-in, mass download, etc., that are correlated to the investigation. From this page, a security analyst can also view additional details on individual alerts.

![AIR alerts page](media/air-investigationalertspage.png)

You can:
- Get a visual overview of the current triggering alert and any associated alerts.
- Select an alert in the list to open a fly-out page that shows full alert details.

### Email investigation

On the **Email** tab for an investigation, you can see all the email clusters identified as part of the investigation. 

Given the sheer volume of email that users in an organization send and receive, the process of 
- clustering email messages based on similar attributes from a message header, body, URL and attachment; 
- separating malicious email from the good email; and 
- taking action on malicious email messages 

can take many hours. AIR now automates this process, saving your organization's security team time and effort. 

As an example, consider the following image. The first cluster of three email messages were deemed to be phish. Another cluster of similar messages with the same IP and subject was found and is considered to be malicious, as some of them were identified as phish during initial detection. 

![AIR email investigation page](media/air-investigationemailpage.png)

You can:
- Get a visual overview of the current clustering results and threats found.
- Click a cluster entity or a threat list to open a fly-out page that shows the full alert details.

![AIR investigation email with flyout details](media/air-investigationemailpageflyoutdetails.png)

### User investigation

On the **Users** tab, you can see all the users identified as part of the investigation. 

For example, in the following image, AIR has identified indicators of compromise and anomalies based on a new inbox rule that was created. Additional details (evidence) of the investigation are available through detailed views within this tab.

![AIR investigation users page](media/air-investigationuserspage.png)

You can:
- Get a visual overview of identified user results and risks found.
- Select a user to open a fly-out page that shows the full alert details.

### Machine investigation

On the **Machines** tab, you can see all the machines identified as part of the investigation. 

![AIR investigation machine page](media/air-investigationmachinepage.png)

As part of the investigation, AIR correlates email threats to devices. For example, an investigation passes a file hash across to [Windows Defender ATP](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-atp/windows-defender-advanced-threat-protection) to investigate. This allows for automated investigation of relevant machines for your users and helps to ensure that threats are addressed both in the cloud and across your devices. 

You can:
- Get a visual overview of the current machines and threats found.
- Select a machine to open a view that into the related [Windows Defender ATP investigations](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-atp/automated-investigations-windows-defender-advanced-threat-protection).

### Entity investigation

On the **Entities** tab, you can see all the machines identified as part of the investigation. 

Here, you can see the investigated entities. You can see details of the types of entities, such as email messages, clusters, IP addresses, users, and more. You can also see how many entities were analyzed, and the threats that were associated with each. 

![AIR investigation entities page](media/air-investigationentitiespage.png)

You can:
- Get a visual overview of the investigation entities and threats found.
- Select an entity to open a fly-out page that shows the related entity detail.

![AIR investigation entities details](media/air-investigationsentitiespagedetails.png)

### Playbook log

On the **Log** tab, you can see all the playbook steps that have occurred during the investigation. The log captures a complete inventory of all actions completed by Office 365 Threat Intelligence capabilities as part of AIR. It provides a clear view of all the steps taken, including the Action itself, a description and the duration of the actual from start to finish. 

![AIR investigation log page](media/air-investigationlogpage.png)

You can:
- Get see a visual overview of the playbook steps taken.
- Export the results to a CSV file.
- Filter the view.

### Recommended actions

On the **Actions** tab, you can see all the playbook actions that are recommended for remediation after the investigation has completed. 

Actions capture a complete list of all the steps Microsoft recommends you take at the end of a investigation. You can take remediation actions here by selecting one or more actions. Clicking **Approve** will allow remediation to begin. (Appropriate permissions might be required. For example, a Security Reader can view actions but not approve them.)  

![AIR investigations action page](media/air-investigationactionspage.png)

You can:
- Get a visual overview of the playbook-recommended actions.
- Select a single action or multiple actions.
- Approve recommended actions. (These are started immediately with comments.)
- Export the results to a CSV file.
- Filter the view.

## How to get AIR

Currently, AIR is in preview. When released, AIR will be included in the following subscriptions:

- Microsoft 365 Enterprise E5
- Office 365 Enterprise E5
- Microsoft Threat Protection
- Office 365 Advanced Threat Protection Plan 2

To learn more about feature availability, visit the [Microsoft 365 Roadmap](https://www.microsoft.com/microsoft-365/roadmap).
