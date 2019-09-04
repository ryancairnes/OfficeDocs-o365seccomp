---
title: "Configure outbound spam policy notifications in Office 365"
ms.author: tracyp
author: MSFTTracyP
manager: dansimp
ms.date: 11/10/2016
audience: ITPro
ms.topic: article
ms.service: O365-seccomp
localization_priority: Normal
search.appverid:
- MET150
ms.assetid: a44764e9-a5d2-4c67-8888-e7fb871c17c7
ms.collection:
- M365-security-compliance
description: "Admins can learn how to modify the notification settings for outbound spam detections in Office 365."
---

# Configure outbound spam policy notifications in Office 365

Outbound spam filtering is always enabled if you use the service for sending outbound email, thereby protecting organizations using the service and their intended recipients. Similar to inbound filtering, outbound spam filtering is comprised of connection filtering and content filtering, however the outbound filter settings are not configurable. If an outbound message is determined to be spam, it is routed through the higher risk delivery pool, which reduces the probability of the normal outbound-IP pool being added to a block list. If a customer continues to send outbound spam through the service, they will be blocked from sending messages.

Although you can't disable or change outbound spam filtering, you can configure the following outbound spam notification settings:

- **Send copies of suspicious messages**: These messages are marked as spam (regardless of the SCL rating) and are not rejected by the filter, but are routed through the higher risk delivery pool. You can use the Exchange admin center (EAC) or the **\*-HostedOutboundSpamFilterPolicy** cmdlets in Exchange Online PowerShell or Exchange Online Protection PowerShell to specify addition recipients for these detected messages. Note that the recipients are added as **Bcc** recipients (the **From** and **To** fields are the original sender and recipient).

- **Send notifications when a sender is blocked**: When a significant amount of spam is coming from a particular user, the user is disabled from sending email messages. Admins are notified by default, but you can use the **User restricted from sending email** [alert policy](alert-policies.md) in the Office 365 Security & Compliance Center to configure additional notification recipients.

  To see what this notification looks like, see [Sample notification when a sender is blocked sending outbound spam](sample-notification-when-a-sender-is-blocked-sending-outbound-spam.md). For information about getting re-enabled, see [Removing a user, domain, or IP address from a block list after sending spam email](http://technet.microsoft.com/library/712cfcc1-31e8-4e51-8561-b64258a8f1e5.aspx).

## What do you need to know before you begin?

- Estimated time to complete: 5 minutes

- To open the Security & Compliance Center, see [Go to the Office 365 Security & Compliance Center](go-to-the-securitycompliance-center.md). To connect to Office 365 Security & Compliance Center PowerShell, see [Connect to Office 365 Security & Compliance Center PowerShell](https://docs.microsoft.com/powershell/exchange/office-365-scc/connect-to-scc-powershell/connect-to-scc-powershell).

- To open the EAC, see [Exchange admin center in Exchange Online](https://docs.microsoft.com/Exchange/exchange-admin-center) or [Exchange admin center in Exchange Online Protection](exchange-admin-center-in-exchange-online-protection-eop.md). To open Exchange Online PowerShell, see [Connect to Exchange Online PowerShell](https://docs.microsoft.com/powershell/exchange/exchange-online/connect-to-exchange-online-powershell/connect-to-exchange-online-powershell). To open Exchange Online Protection PowerShell, see [Connect to Exchange Online Protection PowerShell](https://docs.microsoft.com/powershell/exchange/exchange-eop/exchange-online-protection-powershell).

- Your account needs to be assigned permissions before you can perform this procedure. To see what permissions you need, see the "Manage Alerts" role entry in [Permissions in the Office 365 Security & Compliance Center](permissions-in-the-security-and-compliance-center.md).

## Use the EAC to configure additional recipients for outbound spam messages

1. In the EAC, go to **Protection** \> **Outbound spam**.

2. Select the policy named **Default**, and then click **Edit** ![Edit icon](media/ITPro-EAC-EditIcon.png).

3. In the properties page that opens, verify that the **Outbound spam preferences** tab is selected, and then configure the following setting:

   **Send a copy of all suspicious outbound email messages to the following email address or addresses**: Select the check box and enter the email addresses of one or more administrators who should be added to the **Bcc** field of detected messages. Separate multiple email addresses with a semicolon ( ; ).

   When you're finished, click **Save**.

### Use Exchange Online PowerShell or Exchange Online Protection PowerShell to configure additional recipients for outbound spam messages

To enable and configure additional recipients for outbound spam messages, use the following syntax:

```PowerShell
Set-HostedOutboundSpamFilterPolicy -Identity Default -BccSuspiciousOutboundMail $true -BccSuspiciousOutboundAdditionalRecipients <recipients>
```

- To specify recipients that overwrite all existing values, use the syntax `emailaddress1,emailaddress2,...emailaddressN`.

- To selectively add or remove recipients without affecting the other entries, use the syntax `@{Add="\<emailaddress1\>","\<emailaddress2\>"...; Remove="\<emailaddress1\>","\<emailaddress2\>"...}`.

This example enables and configures chris@contoso.com, laura@contoso.com and julia@contoso.com as Bcc recipients for outbound spam messages.

```PowerShell
Set-HostedOutboundSpamFilterPolicy -Identity Default -BccSuspiciousOutboundMail $true -BccSuspiciousOutboundAdditionalRecipients chris@contoso.com,laura@contoso.com,julia@contoso.com
```

This example adds michelle@contoso.com as an additional Bcc recipient.

```PowerShell
Set-HostedOutboundSpamFilterPolicy -Identity Default -BccSuspiciousOutboundAdditionalRecipients @{Add=michelle@contoso.com}
```

This example removes chris@contoso.com and julia@contoso.com from the list of Bcc recipients.

```PowerShell
Set-HostedOutboundSpamFilterPolicy -Identity Default -BccSuspiciousOutboundAdditionalRecipients @{Remove='chris@contoso.com','julia@contoso.com'}
```

For detailed syntax and parameter information, see [Set-HostedOutboundSpamFilterPolicy](https://docs.microsoft.com/powershell/module/exchange/antispam-antimalware/set-hostedoutboundspamfilterpolicy).

**Note**: Run the command `Get-HostedOutboundSpamFilterPolicy | Format-List` to see the current values of the *BccSuspiciousOutboundMail* and *BccSuspiciousOutboundAdditionalRecipients* properties.

## Use the Security & Compliance Center to configure notifications when a sender is blocked

1. In the Security & Compliance Center, go to **Alerts** \> **Alert Policies**.

2. Find and select the policy named **User restricted from sending email**.

3. In the fly out that opens, click **Edit policy**.

4. In the **Edit recipients** page that appears, configure the following settings:

   - **Send email notifications**: Verify that **On** is selected.

   - **Email recipients**: By default **TenantAdmins** is the only value here. To add additional recipients, click in an empty spot in this box and start typing the recipient. To remove recipients, click on the **X** next to their names.

   - **Daily notification limit**: The default value is **No limit**, but you can configure various limits from 1 to 200.

   When you're finished, click **Save**.

### Use Security & ComplianceCenter PowerShell to configure notifications when a sender is blocked

To specify recipients to receive notifications when users are blocked from sending email messages, use the following syntax:

```PowerShell
Set-ProtectionAlert -Identity "User restricted from sending email" -NotifyUser <emailaddress1>,<emailaddress2>,...<emailaddressN>
```

**Notes**:

- The *Disabled* parameter specifies whether notifications are turned on for the policy. The default value is `$false` (notifications are enabled).

- Any additional email address you specify will *overwrite* the existing values. To preserve the existing values, run the command `Get-ProtectionAlert -Identity "User restricted from sending email"` to record and reuse the existing values in the command.

This example preserves existing notifications for TenantAdmins, and adds chris@contoso.com and michelle@contoso.com.

```PowerShell
Set-ProtectionAlert -Identity "User restricted from sending email" -NotifyUser TenantAdmins,chris@contoso.com,michelle@contoso.com
```

For detailed syntax and parameter information, see [Set-ProtectionAlert](https://docs.microsoft.com/powershell/module/exchange/policy-and-compliance/set-protectionalert).

## For more information

[High-risk delivery pool for outbound messages](high-risk-delivery-pool-for-outbound-messages.md)

[Anti-spam protection FAQ](anti-spam-protection-faq.md)
