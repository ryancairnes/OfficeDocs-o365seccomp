---
title: How policies and protections are combined when mail is red-flagged
description: Describes what policies and protections apply when e-mail encounters multiple protections and is scanned by multiple forms of detection.
keywords: security, malware, Microsoft 365, M365, security center, ATP, Windows Defender ATP, Office 365 ATP, Azure ATP
ms.author: tracyp
author: MSFTTracyp
manager: laurawi
ms.date: 03/26/2019
ms.audience: ITPro
ms.topic: article
ms.service: O365-seccomp
localization_priority: Normal
ms.collection:
- M365-security-compliance
description: "What policies apply, and what actions to take, when email is marked malware, spam, high confidence spam, phishing, and bulk by EOP, and/or ATP."
---

# What policy applies when multiple protection methods and detection scans run on your email

Potentially, your incoming mail may be flagged by multiple forms of protection (for example both EOP *and* ATP), and multiple detection scans (such as spam *and* phishing). This is possible because there are ATP Anti-phishing policies for ATP customers, and EOP Anti-phishing policies for EOP customers. This also means the message may navigate multiple detection scans for malware, phishing, and user-impersonation, for example. Given all this activity, there may be some confusion as to which policy applies.

In general, the policy applied to a message is identified in the **X-Forefront-Antispam-Report** header in the **CAT (Category)** property. If you have multiple Anti-phishing policies, the one at the highest priority will apply.

The Policies below apply to _all organizations_.

|Priority |Policy  |Category  |Where Managed |
|---------|---------|---------|---------|
|1     | Malware      | MALW      | Malware policy   |
|2     | Phishing     | PHSH     | Configure your spam filter policies     |
|3     | High confidence spam      | HSPM        | Configure your spam filter policies        |
|4     | Spoofing        | SPOOF        | Anti-phishing policy, spoof intelligence        |
|5     | Spam         | SPM         | Configure your spam filter policies         |
|6     | Bulk         | BULK        | Configure your spam filter policies         |

In addition, these policies apply to _organizations with ATP_.

|Priority |Policy  |Category  |Where Managed |
|---------|---------|---------|---------|
|7     | Domain Impersonation         | DIMP         | Set up Office 365 ATP anti-phishing and anti-phishing policies        |
|8     | User Impersonation        | UIMP         | Set up Office 365 ATP anti-phishing and anti-phishing policies         |

As an example, if you have two policies:

|Policy  |Priority  |User/Domain Impersonation  |Anti-spoofing  |
|---------|---------|---------|---------|
|A     | 1        | On        |Off         |
|B     | 2        | Off        | On        |

If a message comes in identified as both _user impersonation_ and _spoofing_ (see anti-spoofing in the table above), and the same set of users scoped to policy A is scoped to policy B, then the message is flagged and treated as a _spoof_, but no action is applied since Anti-spoofing is turned off, and because **spoof runs at a higher priority (4) than User Impersonation (8)**.

To make other types of phishing policy apply, you will need to adjust the settings of who the various policies apply to.



