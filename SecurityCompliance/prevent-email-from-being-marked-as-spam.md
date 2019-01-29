---
title: "How to prevent real email from being marked as spam in Office 365"
ms.author: stephow
author: stephow-MSFT
manager: laurawi
ms.date: 6/7/2018
ms.audience: Admin
ms.topic: overview
ms.service: o365-administration
localization_priority: Priority
ms.collection: Strat_O365_IP
search.appverid: 
- MOE150
- MET150
ms.assetid: 34823bbc-a3e3-4949-ba42-97c73997eeed
description: "Learn how to keep real email out of junk and from being marked as spam in Office 365."
---

# How to prevent real email from being marked as spam in Office 365

 **Is your real email getting marked as spam in Office 365? Do this.**
  
Exchange Online Protection (EOP) attempts to filter out spam, keeping your Inbox clear of content that users don't want to see. But sometimes, EOP filters out things that you do want to see.
  
## Determine the reason why the message was marked as spam

Many issues with spam in Office 365 can be resolved by [View e-mail message headers](https://support.office.com/article/cd039382-dc6e-4264-ac74-c048563d212c) and determining what went wrong. You will need to look for a header named X-Forefront-Antispam-Report. You can [learn more about anti-spam message headers](https://technet.microsoft.com/library/dn205071%28v=exchg.150%29.aspx).
  
In the header, look for the following headings and values.
  
### X-Forefront-Antispam-Report

- **SFV:SPM** Indicates that the message was marked as spam because of the EOP spam filters. 

- **SFV:BLK** Indicates that the message was marked as spam because the sending address is on the recipient's Blocked Senders List. 
    
- **SFV:SKS** Indicates that the message was marked as spam prior to the content filter. This could include a transport rule marking the message as spam. Run a message trace to see if a transport rule triggered which may have set a high spam confidence level (SCL). 
    
- **SFV:SKB** Indicates that the message was marked as spam because it matched a block list in the spam filter policy. 
    
- **SFV:BULK** Indicates that the Bulk Complaint Level (BCL) value located in the x-microsoft-antispam header is above the Bulk threshold that has been set for the content filter. Bulk email is email which users may have signed up for, but may still be undesirable. In the message header find the BCL (Bulk Confidence Level) property in the X-Microsoft-Antispam header. If the BCL value is less than the threshold set in the Spam Filter, you may want to adjust the threshold to instead mark these types of bulk messages as spam. Different users have different tolerances and preferences for [how bulk email is handled](https://docs.microsoft.com/en-us/office365/SecurityCompliance/bulk-complaint-level-values). You can create different policies or rules for different user preferences.
    
- **CAT:SPOOF** or **CAT:PHISH** Indicates that the ﻿message appears to be spoofed, meaning that the message source cannot be validated and could be suspicious. If valid, the sender will need to make sure that they have proper SPF and DKIM configuration. Check the Authentication-Results header for more information. Although it may be difficult to get all senders to use proper email authentication methods, bypassing these checks can be extremely dangerous and is the top cause of compromises. 
    
### x-customspam

- The presence of this header indicates that the message was marked as spam because one of the [advanced spam options is enabled](https://technet.microsoft.com/library/jj200750%28v=exchg.150%29.aspx) in your spam filter. Unless you need these features, we recommend that you use the default settings. 
    
## Solutions to additional causes of too much spam

In order to work effectively, Exchange Online Protection (EOP) requires that administrators complete a few tasks. If you are not the administrator for your Office 365 tenant and you are getting too much spam, then you may want to work with your administrator on these tasks. Otherwise, you can skip to the user section.
  
### For admins

- **Point your DNS records to Office 365** In order for EOP to provide protection, your mail exchanger (MX) DNS record(s) for all domains must be pointed to Office 365 -- and only to Office 365. If your MX does not point to Office 365, then EOP will not provide spam filtering for your users. In the situation where you wish to use another service or appliance to provide spam filtering for your domain, you should consider disabling the spam protection in EOP. You can do this by creating a transport rule that sets the SCL value to -1. If you later decide to use EOP, make sure to remove this transport rule. 
    
- **Disable SmartScreen filtering in Outlook** If your users are using the Outlook desktop client, they should disable the SmartScreen filtering functionality, which has been discontinued. If enabled, it can cause false positives. This should not be required if running an updated desktop Outlook client. 
    
- **Turn on the report message add-in for users** We strongly recommend that you [enable the report message add-in for your users](enable-the-report-message-add-in.md). As an administrator, you may also be able to view the feedback your users are sending and use any patterns to adjust any settings that may be causing problems.
    
- **Immediately allow a sender** In the case where you need to immediately allow a sender, we strongly recommend that you **ONLY allow a particular sender's IP address**. Alternately, you can allow a sender and also make sure that the sender passes an authentication check like SPF or DKIM by creating a transport rule that looks for **both** the sender domain and a successful Authentication-Results header. 
    
### For users

- **Report spam to Microsoft** Report spam messages to Microsoft by using the [Use the Report Message add-in](https://support.office.com/article/b5caa9f1-cdf3-4443-af8c-ff724ea719d2). Additionally, you can send a message to junk@office365.microsoft.com and attach one or more messages to report.
    
    **Important** If you do not forward the messages as attachments, then the headers will be missing and we will be unable to improve the junk mail filtering in Office 365. 
    
- **Add a sender to your allow list - but use sparingly** As a last resort, you can [Block or allow (junk email settings)](https://support.office.com/article/48c9f6f7-2309-4f95-9a4d-de987e880e46). If you do so, you should beware that a targeted phishing attempt may be allowed into your inbox.
