---
title: "Automated Investigation and Response (AIR) with Office 365"
ms.author: deniseb
author: denisebmsft
manager: dansimp
ms.date: 08/30/2019
audience: ITPro
ms.topic: article
ms.service: O365-seccomp
localization_priority: Normal
search.appverid:
- MET150
- MOE150
ms.collection: M365-security-compliance
description: "Learn about Automated Investigation and Response capabilities in Office 365 Advanced Threat Protection."
---

# Automated Investigation and Response (AIR) with Office 365

Automated investigation and response (AIR) capabilities (included in [Office 365 Advanced Threat Protection](office-365-atp.md) Plan 2) enable you to run automated investigation and remediation processes in response to well known threats that exist today. Read this article to get an overview of AIR and how it can help your organization and security operations teams mitigate threats more effectively and efficiently. 

## Alerts

[Alerts](alert-policies.md#viewing-alerts) represent triggers for security operations team workflows for incident response. Prioritizing the right set of alerts for investigation, while making sure no threats are unaddressed is challenging. When investigations into alerts are performed manually, Security Operations teams must hunt and correlate entities (e.g. content, devices and users) at risk from threats. Such tasks and workflows are very time consuming and involve multiple tools and systems. With AIR, investigation and response are automated into key security and threat management alerts that trigger your security response playbooks automatically. 

In the initial release of AIR (beginning April 2019), alerts generated from following single events alert policies are auto-investigated. 

- A potentially malicious URL click was detected

- Email reported by user as phish*

- Email messages containing malware removed after delivery*

- Email messages containing phish URLs removed after delivery*

> [!NOTE]
> These alerts have been assigned an "Informational" severity in the respective alert policies within the Security & Compliance Center with email notifications turned off. These can be turned on through the Alert policy configuration.

To view alerts, in the Security & Compliance Center, choose **Alerts** > **View alerts**. Select an alert to view its details, and from there, use the **View investigation** link to go to the corresponding [investigation](#investigation-graph). Note that informational alerts are hidden in the alert view by default. To see them, you need to change the alert filtering to include informational alerts.

If your organization manages your security alerts through a alert management system, service management system, or Security Information and Event Management (SIEM) system, you can send Office 365 alerts to that system via either email notification or via the [Office 365 Management Activity API](https://docs.microsoft.com/office/office-365-management-api/office-365-management-activity-api-reference). The investigation alert notifications via email or API include links to access the alerts in the Security & Compliance Center, enabling the assigned security administrator to navigate quickly to the investigation.

![Alerts that link to investigations](media/air-alerts-page-details.png) 

## Security playbooks

Security playbooks are back-end policies that are at the heart of automation in Microsoft Threat Protection. The security playbooks provided in AIR are based on common real-world security scenarios. A security playbook is launched automatically when an alert is triggered within your organization. Once the alert triggers, the associated playbook is run automatically. The playbook runs an investigation, looking at all the associated metadata (including email messages, users, subjects, senders, etc.). Based on the playbook's findings, AIR recommends a set of actions that your organization's security team can take to control and mitigate the threat. 

The security playbooks you'll get with AIR are designed to tackle the most frequent threats that organizations face today. They're based on input from Security Operations and Incident Response teams, including those who help defend Microsoft and our customers assets.

### Security playbooks are rolling out in phases

As part of AIR, security playbooks are rolling out in phases. During Phase 1 (began rolling out in April 2019), several playbooks were released that include recommendations for actions that security administrators review and approve:
- User-reported phish message
- URL click verdict change 
- Malware detected post-delivery (Malware ZAP)
- Phish detected post-delivery ZAP (Phish ZAP)

Phase 1 also includes manual e-mail investigations (using [Threat Explorer](threat-explorer.md)).

Phase 2 is in progress now. Visit the [Microsoft 365 Roadmap](https://www.microsoft.com/microsoft-365/roadmap) to see what else is planned and coming soon.

### Playbooks include investigation and recommendations

In AIR, each security playbook includes: 
- a root investigation, 
- steps taken to identify and correlate other potential threats, and 
- recommended threat remediation actions.

Each high-level step includes many sub-steps that are executed to provide a deep, detailed, and exhaustive response to threats.

## Example: A user-reported phish message launches an investigation playbook

When a user in your organization submits an email message and reports it to Microsoft by using the [Report Message add-in for Outlook or Outlook Web Access](enable-the-report-message-add-in.md), the report is also sent to your system and is visible in Explorer in the User-reported view. This user-reported message now triggers a system-based informational alert, which automatically launches the investigation playbook.

During the root investigation phase, various aspects of the email are assessed. These include:
- A determination about what type of threat it might be;
- Who sent it;
- Where the email was sent from (sending infrastructure);
- Whether other instances of the email were delivered or blocked;
- An assessment from our analysts;
- Whether the email is associated with any known campaigns;
- and more.

After the root investigation is complete, the playbook provides a list of recommended actions to take on the original email and entities associated with it.
  
Next, several threat investigation and hunting steps are executed:

- Similar email messages in other email clusters are searched.
- The signal is shared with other platforms, such as [Microsoft Defender ATP](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection).
- A determination is made on whether any users have clicked through any malicious links in suspicious email messages.
- A check is done across Office 365 Exchange Online Protection ([EOP](eop/exchange-online-protection-eop.md)) and Office 365 Advanced Threat Protection ([ATP](office-365-atp.md)) to see if there are any other similar messages reported by users.
- A check is done to see if a user has been compromised. This check leverages signals across [Microsoft Cloud App Security](https://docs.microsoft.com/cloud-app-security) and [Azure Active Directory](https://docs.microsoft.com/azure/active-directory), correlating any related user activity anomalies. 

During the hunting phase, risks and threats are assigned to various hunting steps. 

Remediation is the final phase of the playbook. During this phase, remediation steps are taken, based on the investigation and hunting phases. 

## Example: A security administrator triggers an investigation from Threat Explorer

In addition to automatic investigations that are triggered by an alert, your organization's security operations team can trigger an automatic investigation from a view in [Threat Explorer](use-explorer-in-security-and-compliance.md).

For example, suppose that you are viewing data in Explorer about user-reported messages. You can select an item in the list of results, and then click **Investigate**.

![User-reported messages in Explorer with Investigate button](media/Explorer-UserReported-Investigate.png)

As another example, suppose you are viewing data about email messages detected as containing malware, and there are several email messages detected as containing malware. You can select the **Email** tab, select one or more email messages, and then, on the **Actions** menu, select **Investigate**. 

![Starting an investigation for malware in Explorer](media/Explorer-Malware-Email-ActionsInvestigate.png)

Similar to playbooks triggered by an alert, automatic investigations that are triggered from a view in Explorer include a root investigation, steps to identify and correlate threats, and recommended actions to mitigate those threats.

## How to get AIR

Office 365 AIR are included in the following subscriptions:

- Microsoft 365 Enterprise E5
- Office 365 Enterprise E5
- Microsoft Threat Protection
- Office 365 Advanced Threat Protection Plan 2

To learn more about feature availability, visit the [Feature availability across Advanced Threat Protection (ATP) plans](https://docs.microsoft.com/office365/servicedescriptions/office-365-advanced-threat-protection-service-description#feature-availability-across-advanced-threat-protection-atp-plans).
