---
title: "Create safe sender lists in Office 365"
ms.author: tracyp
author: MSFTTracyP
manager: laurawi
ms.date: 4/29/2019
ms.audience: ITPro
ms.topic: article
ms.service: O365-seccomp
localization_priority: Normal
search.appverid:
- MET150s
ms.assetid: 9721b46d-cbea-4121-be51-542395e6fd21
description: "If you want to be sure that you receive mail from a particular sender, because you trust them and their messages, you can adjust your allow list in a spam filter policy in the Exchange admin center."
---

#Create safe sender lists in Office 365

If you want to ensure that users receive emails from a particular sender or senders because you trust them and their messages, there are multiple methods available that you can choose from. These options include Exchange Transport Rules (ETRs), IP Allow Lists, Outlook Safe Senders, Anti-Spam Sender/Domain Allow Lists.

> [!IMPORTANT]
> While organization allow lists can be used to address false positives, this should be considered a temporary solution and avoided if possible. Managing false positives by using allow lists is not recommended as it can inadvertently open your organization up to spoofing, impersonation, and other attacks. If you will use an allow list for this purpose, you will need to be vigilant and keep the article for [submitting spam, non-spam, and phishing mails to Microsoft for analysis](https://docs.microsoft.com/en-us/office365/SecurityCompliance/submit-spam-non-spam-and-phishing-scam-messages-to-microsoft-for-analysis), at the ready.

The recommended method to configure a safe sender list is to use an Exchange Transport Rules (ETRs) as this presents the most flexibility to ensure that only the right messages get allowed. Anti-Spam policy email address and domain based allow lists are not as secure as IP address-based lists because domains can easily be spoofed. But anti-ppam policy IP based allow lists also present risks as they will allow any domains sent through that IP to bypass spam filtering.

##Using Exchange Transport Rules (ETRs) to allow specific senders (Recommended)

To ensure that only legitimate messages are allowed into your organization the condition should be one of the following:

- Use the sender authentication status of the sending domain. This is done by checking the Authentication-Results header to ensure that it contains “dmarc=pass” or “dmarc=bestguesspass”. This ensures that the sending domain has been authenticated and is not being spoofed. Click for more on [SPF](https://docs.microsoft.com/en-us/office365/SecurityCompliance/set-up-spf-in-office-365-to-help-prevent-spoofing), [DKIM](https://docs.microsoft.com/en-us/office365/SecurityCompliance/use-dkim-to-validate-outbound-email), and [DMARC](https://docs.microsoft.com/en-us/office365/SecurityCompliance/use-dmarc-to-validate-email) email authentication.

- Or, if the sending domain does not have authentication, use the sending domain *plus* a sending IP (or IP range). Ensure that you are *as restrictive as possible*, the goal being that we do this as securely as possible, and we recommend not including any range larger than a /24. Avoid adding IP address ranges that belong to consumer services or shared infrastructures.

- *Optionally*, add a condition that the message originates from outside the organization (this is implicit, but it's fine to add it as a condition to account for on-premise servers that may not be correctly configured).

- *Optionally*, if you can identify any unique keywords or phrases in the email Subject or Body use this information as an additional condition to further restrict the email messages allowed by the mail flow rule.

The action on the rule should be the following:

1. Set the spam confidence level (SCL) to -1 (bypass spam filtering).

2. Add an X-Header to say what the rule does. In the example below, you can add a simple header "X-ETR: Bypass spam filtering for authenticated sender contoso.com". If you have more than one domain in this rule, you can change the header text as appropriate.**When a message skips filtering due to an ETR, it stamps SFV:SKN in the X-Forefront-Antispam-Report header** (**if it's on an IP Allow list, it also stamps IPV:CAL**). This will assist with troubleshooting.

![GUI for bypassing spam filtering.](media/1_AllowList_SkipFilteringFromContoso.png)


