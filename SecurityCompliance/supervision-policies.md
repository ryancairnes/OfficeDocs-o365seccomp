---
title: "Supervision Policies in Office 365"
ms.author: robmazz
author: robmazz
manager: laurawi
ms.audience: Admin
ms.topic: article
f1_keywords:
- 'ms.o365.cc.SupervisoryReview'
ms.service: o365-administration
localization_priority: Normal
ms.collection: Strat_O365_IP
search.appverid:
- MET150
- MOE150
ms.assetid: d14ae7c3-fcb0-4a03-967b-cbed861bb086
description: "Understanding supervision policies in Office 365"
---

# Supervision policies in Office 365

Supervision policies in Office 365 allow you to capture employee communications for examination by designated reviewers. You can define specific policies that capture internal and external email, Microsoft Teams, or 3rd-party communications in your organization. Reviewers can then examine the messages to make sure they are compliant with your organization's message standards and resolve them with classification type. These policies can also help you overcome many modern compliance challenges, including monitoring increasing types of communication channels, increasing volume of message data, and regulatory enforcement & the risk of fines.

In some organizations, there may be a separation of duties between IT support and the compliance management group. Office 365 supports the separation between configuring the tenant with supervision policy support features and the configuration of policies and acting on captured communications. For example, the IT group for an organization may be responsible for setting up role permissions and groups to support supervision policies that are configured and managed by the organization's compliance team.

## Scenarios for supervision policies

Supervision policies can assist monitoring communications in your organization in several areas:

- **Corporate policies**

    Employees must comply with acceptable use, ethical standards, and other corporate policies in all their business-related communications. Supervision policies can detect policy violations and help you take corrective actions to help mitigate these types of incidents. For example, you could monitor your organization for potential human resources violations such as harassment or the use of inappropriate or offensive language in employee communications.

- **Risk management**

    Organizations are responsible to all communications distributed throughout their infrastructure and corporate network systems. Using supervision policies to help identify and manage potential legal exposure and risk can help minimize risks before they can damage corporate operations. For example, you could monitor your organization for unauthorized communications for confidential projects such as upcoming acquisitions, mergers, earnings disclosures, reorganizations, or leadership team changes.

- **Regulatory compliance**

    Most organizations must comply with some type of regulatory compliance standards as part of their normal operating procedures. These regulations often require organizations to implement some type of supervisory or oversight process for messaging that is appropriate for their industry. The Financial Industry Regulatory Authority (FINRA) Rule 3110 is a good example of a requirement for organizations to have supervisory procedures in place to monitor the activities of its employees and the types of businesses in which it engages. Another example may be a need to monitor broker-dealers in your organization to safeguard against potential money-laundering, insider trading, collusion, or bribery activities. Supervision policies can help your organization meet these requirements by providing a process to both monitor and report on corporate communications.

## Feature components

### Supervision policy

You'll create supervision policies in the Security & Compliance Center. These policies define which communications and users are subject to review in your organization, define custom conditions that the communications must meet, and specifies who should perform reviews. Users included in the Supervisory Review role group can set up policies and anyone who has this role assigned can access the Supervision page under Data Governance in the Office 365 Security & Compliance Center.

### Supervised users

Before you start using supervision, you'll need to determine who will have their communications reviewed. In the policy, you'll use user email addresses to identify individuals or groups of people to supervise. Some examples of these groups are Office 365 Groups, Exchange-based distribution lists, and Microsoft Teams channels. You also can exclude specific users or groups from supervision that are included within a supervised group or a list of groups.

> [!IMPORTANT]
> All users monitored by supervision policies must have either an Office 365 Enterprise E3 license with the Advanced Compliance add-on or be included in an Office 365 Enterprise E5 subscription. If you don't have an existing Enterprise E5 plan and want to try supervision, you can [sign up for a trial of Office 365 Enterprise E5](https://go.microsoft.com/fwlink/p/?LinkID=698279).

### Reviewers

When you create a supervision policy, you'll also determine who will perform the reviews of the messages of the supervised users. In the policy, you'll use user email addresses to identify individuals or groups of people to review supervised communications.

### Groups for supervised users and reviewers

To simplify your setup, create groups for people who will have their communication reviewed and groups for people who will review those communications. If you're using groups, you might need several. For example, if you want to monitor communications between two distinct groups of people, or if you want to specify a group that isn't going to be supervised.

### Supported communication types

With supervision policies, you can choose to monitor messages in one or more of the following communication platforms:

- **Exchange email:** Mailboxes that are hosted on Exchange Online as part of your Office 365 subscription are all eligible for message supervision. Emails and attachments matching supervision policy conditions are instantly available for monitoring and in supervision reports. Supported attachment types for supervision are the same as the [file types supported for Exchange mail flow rule content inspections](https://docs.microsoft.com/exchange/security-and-compliance/mail-flow-rules/inspect-message-attachments#supported-file-types-for-mail-flow-rule-content-inspection).
- **Microsoft Teams:** Chat communications and associated attachments in both public and private Microsoft Teams channels and individual chats can be supervised. Teams chats matching supervision policy conditions are processed once every 24 hours and then are available for monitoring and in supervision reports.
- **Third-party sources:** You can supervise communications from third-party sources (like from Facebook or DropBox) if you've imported this data into Office 365 mailboxes in your organization. [Learn how to import 3rd-party data into Office 365](https://docs.microsoft.com/office365/securitycompliance/archiving-third-party-data).

### Policy settings

#### Direction

By default, the **Direction is** condition is displayed and can't be removed. Communication direction settings in a policy can be chosen individually or together:

- **Inbound** - You can choose **Inbound** to review communications that are sent **to** the people you chose to supervise **from** people not included in the policy.
- **Outbound** - You can choose **Outbound** if you want to review communications that are sent **from** the people you chose to supervise **to** people not included in the policy.
- **Internal** - You can choose **Internal** to review communications sent **between** the people you identified in the policy.

#### Sensitive information types

You have the option of including sensitive information types as part of your supervision policy. Sensitive information types are either pre-defined or custom data types that can help identify and protect credit card numbers, bank account numbers, passport numbers, and more. As a part of Office 365 [data loss prevention (DLP)](data-loss-prevention-policies.md), the sensitive information configuration can leverage patterns, character proximity, confidence levels, and even custom data types to help identify and flag content that may be sensitive. The default sensitive information types are:

- Financial
- Medical and health
- Privacy
- Custom information type

To learn more about sensitive information details and the patterns included in the default types, see [What sensitive information types look for](what-the-sensitive-information-types-look-for.md).

#### Custom keyword dictionaries

Configuring custom keyword dictionaries (or lexicons) can provide simple management of keywords specific to your organization or industry and can support up to 100,000 terms per dictionary. If needed, you can apply multiple custom keyword dictionaries to a single policy or have a single keyword dictionary per policy. These dictionaries are assigned in a supervision policy and can be sourced from a file (such as a .csv or .txt list), or from a list you can [enter directly in a PowerShell cmdlet](create-a-keyword-dictionary.md).

#### Conditional settings

The conditions you choose for the policy will apply to communications from both email and 3rd-party sources in your organization (like from Facebook or DropBox).

The following table explains more about each condition.
  
|**Condition**|**How to use this condition**|
|:-----|:-----|
|Message is received from any of these domains  <br><br> Message is not received from any of these domains | To apply the policy when certain domains are included or excluded in a received message, enter each domain and separate multiple domains with a comma. Each domain you enter will be applied separately (only one of these domains must apply for the policy to apply to the message). |
|Message is sent to any of these domains  <br><br> Message is not sent to  any of these domains | To apply the policy when certain domains are included or excluded in a sent message, enter each domain and separate multiple domains with a comma. Each domain you enter will be applied separately (only one of these domains must apply for the policy to apply to the message). |
|Message is classified with any of these labels  <br><br> Message is not classified with any of these labels | To apply the policy when certain retention labels are included or excluded in a message. Retention labels must be configured separately and configured labels can be chosen as part of this condition. Each label you choose will be applied separately (only one of these labels must apply for the policy to apply to the message). For more information about configuring retention labels, see [Overview of retention labels](https://docs.microsoft.com/office365/securitycompliance/labels).|
|Message contains any of these words  <br><br> Message contains none of these words | To apply the policy when certain words or phrases are included or excluded in a message, enter each word or phrase on a separate line. Each line of words you enter will be applied separately (only one of these lines must apply for the policy to apply to the message). For more information about entering words or phrases, see the next section [Matching words and phrases to emails or attachments](supervision-policies.md#Matchwords).|
|Attachment contains any of these words  <br><br> Attachment contains none of these words | To apply the policy when certain words or phrases are included or excluded in a message attachment (such as a Word document), enter each word or phrase on a separate line. Each line of words you enter will be applied separately (only one line must apply for the policy to apply to the attachment). For more information about entering words or phrases, see the next section [Matching words and phrases to emails or attachments](supervision-policies.md#Matchwords).|
|Attachment is any of these file types  <br><br> Attachment is none of these file types | To supervise communications that include or exclude specific types of attachments, enter the file extensions (such as .exe or .pdf). If you want to include or exclude multiple file extensions, enter these on separate lines. Only one attachment extension needs to match for the policy to apply.|
|Message size is larger than  <br><br> Message size is not larger than | To review messages based on a certain size, use these conditions to specify the maximum or minimum size a message can be before it is subject to review. For example, if you specify **Message size is larger than** \> **1.0 MB**, all messages that are 1.01 MB and larger will be subject to review. You can choose bytes, kilobytes, megabytes, or gigabytes for this condition.|
|Attachment is larger than  <br><br> Attachment is not larger than | To review messages based on the size of their attachments, specify the maximum or minimum size an attachment can be before the message and its attachments are subject to review. For example, if you specify **Attachment is larger than** \> **2.0 MB**, all messages with attachments 2.01 MB and over will be subject to review. You can choose bytes, kilobytes, megabytes, or gigabytes for this condition.|
   
##### Matching words and phrases to emails or attachments
<a name="Matchwords"> </a>

Each line of words you enter will be applied separately (only one line must apply for the policy condition to apply to the email or attachment). For example, let's use the condition, **Message contains any of these words**, with the keywords "banker" and "insider trading" on separate lines. The policy will apply to any messages that includes the word "banker" or the phrase "insider trading". Only one of these words or phrases must occur for this policy condition to apply. Words in the message or attachment must exactly match what you enter.
  
##### Entering multiple conditions

If you enter multiple conditions, Office 365 uses all the conditions together to determine when to apply the policy to communication items. When you set up multiple conditions, they must all be met for the policy to apply, unless you enter an exception. For example, let's say you need to create a policy that should apply if a message contains the word "trade", and is larger than 2MB. However, if the message also contains the words "Approved by Contoso financial", the policy should not apply. Thus, in this case, the three conditions would be as follows:
  
- **Message contains any of these words**, with the keywords "trade"

- **Message size is larger than**, with the value 2 MB

- **Message contains none of these words**, with the keywords "Approved by Contoso financial team".

#### Review percentage

You can specify a percentage of all the communications governed by a supervision policy if you want to reduce the amount of content to review. We'll randomly select that amount of content from the total percentage that matched the conditions you chose. If you want reviewers to review all items, you can enter **100%** in a supervision policy.

## Monitoring & managing

Monitoring the results of your supervision policies and applying a resolution tag is easy and convenient. You can quickly see the status of reviewed items, the users and groups under supervision, and the users and groups designated as reviewers.

### Supervision policy dashboard

The easiest way to manage supervision policy results and to resolve outstanding items is to use the supervision policy dashboard. This dashboard allows reviewers to quickly see the items that need to be reviewed, take action on an item, and review the results of previously reviewed and resolved items for each supervision policy. You can access the supervision policy dashboard in the Office 365 Security & Compliance Center at **Supervision** > *Your Custom Policy* > **Open**.

#### Dashboard Home

The dashboard **Home** page has several sections to help you quickly take action on your supervision policies. Here you can:

- Quickly review the pending and resolved highlights for the week
- See a list of the supervised users and supervised groups for the selected policy
- See a list of the reviewers and review teams for the selected policy
- See which communication platforms have content under supervision for the policy.

#### Supervise tab

The **Supervise** tab is where reviewers can take action and resolve items identified by the selected policy. Here you can:

- Filter by pending, compliant, non-compliant, and questionable items
- Tag a single item as compliant, non-compliant, or questionable. You can also record a comment with the item to help clarify the tagging action taken.
- Bulk tag multiple items as compliant, non-compliant, or questionable. You can also record a comment with multiple items to help clarify the tagging action taken.
- View the history of the tagging for a single item, including who resolved the item, the date and time of the action, the resolution tag, and any included comments.
- Reclassify previously reviewed items as compliant, non-compliant, or questionable. You can also record a comment with single or multiple items to help clarify the reclassification action taken.

#### Resolved Items tab

The **Resolved Items** tab is where reviewers can view all previously resolved items for the selected policy. Here you can:

- Quickly view and sort the subject, sender, and date of resolved items.
- View the classification and comment history of any selected item

### Other ways to review items

If reviewers would prefer not to use the supervision dashboard in Office 365, they also have other options to review and manage items collected by supervision policies.

#### Outlook on the web

Users designated as reviewers in a supervision policy can use Outlook on the web to review and resolved supervision items. The Supervision add-in is installed automatically in Outlook on the web for all reviewers you specified in the policy. No extra configuration is needed by your organization for supervision policy shared folders to be available for configured reviewers.

Using Outlook on the web, reviewers can:

- View filtered items by compliant, non-compliant, questionable, and resolved status
- Tag a single item as compliant, non-compliant, questionable, or resolved. You can also record a comment with the item to help clarify the tagging action taken.
- View the history of the tagging for a single item, including who resolved the item, the date and time of the action, the resolution tag, and any included comments.
- Reclassify previously reviewed items as compliant, non-compliant, or questionable. You can also record a comment with single items to help clarify the reclassification action taken.

#### Microsoft Outlook

To review communications identified by a supervision policy, reviewers can also use the Supervision add-in for Microsoft Outlook. However, reviewers must run through some steps to install it in the desktop version of Outlook. For detailed guidance about installing the Supervision add-in for Outlook, see [Configure supervision policies](configure-supervision-policies.md).

Using Outlook, reviewers can:

- View filtered items by compliant, non-compliant, questionable, and resolved status
- Tag a single item as compliant, non-compliant, questionable, or resolved. You can also record a comment with the item to help clarify the tagging action taken.
- View the history of the tagging for a single item, including who resolved the item, the date and time of the action, the resolution tag, and any included comments.
- Reclassify previously reviewed items as compliant, non-compliant, or questionable. You can also record a comment with single items to help clarify the reclassification action taken.

## Reporting

Use the supervision reports to see the review activity at the policy and reviewer level. For each policy, you can also view live statistics on the current state of review activity. You can use the supervision reports to:
  
- Verify that your policies are working as you intended.
- Find out how many communications are being identified for review.
- Find out how many communications aren't compliant and which ones are passing review. This information can help you decide whether to fine-tune your policies or change the number of reviewers.

### View the Supervision report

1. Sign into the [Security & Compliance Center](https://protection.office.com/) using the credentials for an admin account in your Office 365 organization that has permissions to view supervision reports.
2. Go to either **Reports** \> **Dashboard** or **Supervision**. You'll see a supervision reporting widget with a summary of current supervision policy activity.
3. Select the **Supervision** widget to open the detailed report page.

> [!NOTE]
> If you aren't able to access the **Reports** page, check that you're a member of the Supervisory Review role group, as described in [Make supervision available in your organization](configure-supervision-policies.md). Being included in this role group lets you create and manage supervision polices and run the report.
  
### How to use the report

When a supervision policy identifies a communication message for review, the email is delivered to the reviewer's Supervision folder in Outlook and Outlook web app. This report lists each policy's name and the number of communications at each stage in the review process.
  
Use the report to:
  
- View data for all or specific policies.
- View data grouped by tag type (such as Compliant, Questionable, etc.), reviewer, or message type.
- Export data to a CSV file based on activity date, policy, and by reviewer activity.
- Filter data based on activity date, tag type, reviewer, and message type.

Here's a breakdown of the values you might see in the **Tag type** column.
  
|**Tag type**|**What it means**|
|:-----|:-----|
| Not Reviewed | The number of emails that have not been reviewed yet. These emails are awaiting review in the Office 365 supervision dashboard or in the reviewer's supervision folder in Outlook/Outlook Web App.|
| Compliant | The number of emails reviewed and marked as compliant. These messages still need to be resolved. |
| Questionable | The number of emails reviewed and marked questionable. This acts as a flag; other reviewers can help check whether an email needs investigation for compliance. These messages still need to be resolved. |
| Non-Compliant (Active) | The number of non-compliant emails that reviewers are currently investigating. |
| Non-Compliant (Resolved) | The number of non-compliant emails that reviewers investigated and resolved. |
| Hit Policy | The total number (daily) of messages from Exchange, Teams, and third-party data sources that matched one or more conditions defined in a supervision policy |
| In Purview | The total number (daily) of messages from Exchange, Teams, and third-party data sources scanned by a supervision policy |
| Resolved | The total number of messages from Exchange, Teams, and third-party data sources that have been classified as **Resolved**|

> [!NOTE]
> Supervision policies must first be provisioned before they will appear in this report. Additionally, if policies are deleted, historical data is still shown. However, they're indicated as a "Non-existent policy" and the **Export** function isn't available.

## Auditing

In some instances, you'll need to provide information to regulatory or compliance auditors to prove supervision of employee activities and communications. This may be a summary of all supervisory activities associated with a defined policy or anytime a supervision policy was changed or updated. Supervision policies have built-in audit trails for complete readiness for internal or external audits. Proof of supervisory procedures can be demonstrated with a detailed audit history of every action monitored by your supervision policies.

The following supervision policy activities are audited and can be viewed using the unified Office 365 audit logs:

|**Activity**|**Associated commands**|
|:-----|:-----|
| Creating a policy | New-SupervisoryReviewPolicy <br> New-SupervisoryReviewRule |
| Editing a policy | Set-SupervisoryReviewPolicy <br> Set-SupervisoryReviewRule |
| Deleting a policy| Remove-SupervisoryReviewPolicy |

The audits can be retrieved using the unified audit log search function or by using the [Search-UnifiedAuditLog](https://docs.microsoft.com/powershell/module/exchange/policy-and-compliance-audit/search-unifiedauditlog) PowerShell cmdlet.

For example, the following example returns the activities for the all the supervisory review activities (policies and rules) and lists detailed information for each:

```
Search-UnifiedAuditLog -StartDate $startDate -EndDate $endDate -RecordType DataGovernance -ResultSize 5000 | Where-Object {$_.Operations -like "*SupervisoryReview*"} | fl CreationDate,Operations,UserIds,AuditData 
```

In addition to information provided in the supervision reports and logs, you can also use the [Get-SupervisoryReviewActivity](https://docs.microsoft.com/powershell/module/exchange/policy-and-compliance/get-supervisoryreviewactivity?view=exchange-ps) PowerShell cmdlet to return a complete detailed listing of all supervision policy activities.

## Ready to get started?

To start configuring supervision policies for your organization, see [Configure supervision policies](configure-supervision-policies.md).