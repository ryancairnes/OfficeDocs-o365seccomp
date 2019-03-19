---
title: "Quick Start: Set up Office 365 Advanced Threat Protection"
ms.author: deniseb
author: denisebmsft
manager: laurawi
ms.date: 03/19/2019
ms.audience: ITPro
ms.topic: article
ms.service: O365-seccomp
localization_priority: Normal
search.appverid:
- MET150
- MOE150
ms.collection: 
- M365-security-compliance
description: "Here's a quick-start guide you can use to make sure Office 365 Advanced Threat Protection (ATP) is set up and configured for your organization."
---

# Quick Start Guide: Set up Office 365 Advanced Threat Protection

Here's a quick-start guide you can use as a checklist to make sure Office 365 Advanced Threat Protection (ATP) is set up for your organization. If you're new to threat protection in Office 365, or you're just not sure where to begin, use the following guidance as a starting point. 

> [!IMPORTANT]
> **Initial recommended settings are included for each kind of policy; however, many options are available, and you can adjust your settings to meet your specific organization's needs**. Allow approximately 30 minutes for your policies or changes to work their way through your datacenter.

## Prerequisites

- Your organization must have a subscription that includes [Office 365 Advanced Threat Protection](office-365-atp.md) (ATP).

- You must be assigned an appropriate role to access ATP features. The following table includes some examples: 

    |Role or role group  |Where to learn more  |
    |---------|---------|
    |Office 365 Global Administrator |[About Office 365 admin roles](https://docs.microsoft.com/office365/admin/add-users/about-admin-roles)|
    |Security Administrator |[Administrator role permissions in Azure Active Directory](https://docs.microsoft.com/en-us/azure/active-directory/users-groups-roles/directory-assign-admin-roles)|
    |Exchange Online Organization Management |[Permissions in Exchange Online](https://docs.microsoft.com/en-us/exchange/permissions-exo/permissions-exo) <br>and<br> [Exchange Online PowerShell](https://docs.microsoft.com/powershell/exchange/exchange-online/exchange-online-powershell?view=exchange-ps)|

    (See [Permissions in the Office 365 Security &amp; Compliance Center](permissions-in-the-security-and-compliance-center.md).)

- Sign in to the Office 365 Security & Compliance Center ([https://protection.office.com](https://protection.office.com)).

## Part 1 - Anti-malware

1. In the [Office 365 Security & Compliance Center](https://protection.office.com), choose **Threat management** > **Policy** > **Anti-malware**.
2. Double-click the **Default** policy, and then choose **settings**.
3. Specify the following settings:
    - In the **Malware Detection Response** section, keep the default setting of **No**.
    - In the **Common Attachment Types Filter** section, choose **On**.
4. Click **Save**.

To learn more about anti-malware policy options, see [Configure anti-malware policies](configure-anti-malware-policies.md).

## Part 2 - Zero-day protection

Zero-day protection is set up through policies, such as ATP Safe Links and Safe Attachments policies.

### ATP Safe Attachments policies

1. In the [Office 365 Security & Compliance Center](https://protection.office.com), choose **Threat management** > **Policy** > **ATP safe attachments**.
2. Select the option **Turn on ATP for SharePoint, OneDrive, and Microsoft Teams**.
3. In the **Protect email attachments** section, click the plus sign (**+**).
4. Specify the following settings:
    - In the **Name** box, type `Block malware`.
    - In the response section, choose **Block**.
    - In the **Redirect attachment** section, select the option **Enable redirect**, and then specify the email address for your organization's security administrator or operator who will review detected files.
    - In the **Applied to** section, choose **The recipient domain is**. Then, select your domain, choose **Add**, and then click **OK**.
5. Click **Save**.
6. (Recommended additional step) As a global administrator or a SharePoint Online administrator run the **[Set-SPOTenant](https://docs.microsoft.com/powershell/module/sharepoint-online/Set-SPOTenant?view=sharepoint-ps)** cmdlet with the **DisallowInfectedFileDownload** parameter set to  *true* for your Office 365 environment. (This prevents people from opening, moving, copying, or sharing files that are detected as malicious.)  

To learn more, see [Set up Office 365 ATP Safe Attachments policies](set-up-atp-safe-attachments-policies.md) and [Turn on Office 365 ATP for SharePoint, OneDrive, and Microsoft Teams](turn-on-atp-for-spo-odb-and-teams.md).

### ATP Safe Links policies

To set up ATP Safe Links, review your default policy and add a policy.

1. In the [Office 365 Security & Compliance Center](https://protection.office.com), choose **Threat management** > **Policy** > **ATP Safe Links**.
2. Double-click the **Default** policy.
3. In the **Use safe links in** section, select the option **Office 365 ProPlus, Office for iOS and Android**, and then click **Save**.
4. In the **Policies that apply to specific recipients** section, click the plus sign (**+**).
5. Specify the following settings:
    - In the **Name** box, type a name, such as `Safe Links`.
    - In the **Select the action** section, choose **On**.
    - Select these options:
        - **Use safe attachments to scan downloadable content** 
        - **Apply safe links to email messages sent within the organization**
        - **Do not let users click through safe links to original URL**
    - In the **Applied to** section, choose **The recipient domain is**. Then, select your domain, choose **Add**, and then click **OK**.
6. Click **Save**.

To learn more, see [Set up Office 365 ATP Safe Links policies](set-up-atp-safe-links-policies.md). 

## Part 3 - Anti-phishing 

1. In the [Office 365 Security & Compliance Center](https://protection.office.com), choose **Threat management** > **Policy** > **ATP anti-phishing**.
2. Click **Default policy**.
3. In the **Impersonation** section, click **Edit**, and then specify the following settings:
    -  On the **Add users to protect** tab, turn protection on. Then add users, such as your organization's board members, your CEO, CFO, and other senior leaders. (You can type an individual email address, or click to display a list.)
    - On the **Add domains to protect** tab, turn on **Automatically include the domains I own**. If you have custom domains, add those as well.
    - On the **Actions** tab, select **Move message to the recipients' Junk Email folders** for both impersonated user and impersonated domain, and turn on safety tips.
    - On the **Mailbox intelligence** tab, make sure mailbox intelligence is turned on.
    - On the **Review your settings** tab, after you have reviewed your settings, click **Save**.
4. In the **Spoof** section, click **Edit**, and then specify the following settings:
    - On the **Spoofing filter settings** tab, make sure anti-spoofing protection is turned on.
    - On the **Actions** tab, choose Move message to the recipients' Junk Email folders.
    - On the **Review your settings** tab, after you have reviewed your settings, click **Save**. (If you didn't make any changes, click **Cancel**.)
5. Close the default policy settings page.

To learn more about your anti-phishing policy options, see [Set up Office 365 ATP anti-phishing and anti-phishing policies](set-up-anti-phishing-policies.md).

## Part 4 - Anti-spam

1. In the [Office 365 Security & Compliance Center](https://protection.office.com), choose **Threat management** > **Policy** > **Anti-spam**.
2. On the **Custom** tab, turn **Custom settings** on.
3. Expand **Default spam filter policy**, click **Edit policy**, and then specify the following settings:
    - In the **Spam and bulk actions** section, set the threshold to a value of 5 or 6.
    - In the **Allow lists** section, review (and if necessary, edit) your allowed senders and domains.
4. Click **Save**.

To learn more about your anti-spam policy options, see [Configure the anti-spam policies](configure-the-anti-spam-policies.md).

## Part 5 - Service-wide settings

### Zero-hour auto purge

Zero-hour auto purge (ZAP) is turned on by default; however, the following conditions must be met:
- Spam actions are set to **Move message to Junk Email folder** in anti-spam policies.
- Users have kept their default junk email settings, and have not turned off junk email protection.

To learn more, see [Zero-hour auto purge - protection against spam and malware](zero-hour-auto-purge.md).

### Audit logging

In order to view data in threat protection reports, such as the [Security Dashboard](security-dashboard.md) and [Explorer](use-explorer-in-security-and-compliance.md), audit logging must be turned on for your organization.

See [Turn Office 365 audit log search on or off](turn-audit-log-search-on-or-off.md).

## Post-setup tasks

### Watch for new features and service updates

- [Visit the Microsoft 365 Roadmap](https://www.microsoft.com/microsoft-365/roadmap?filters=&searchterms=advanced%2Cthreat%2Cprotection)

- [See the Office 365 Advanced Threat Protection Service Description](https://docs.microsoft.com/office365/servicedescriptions/office-365-advanced-threat-protection-service-description#whats-new-in-office-365-advanced-threat-protection-atp)

### See how ATP is working for your organization

- [View reports for Office 365 Advanced Threat Protection](view-reports-for-atp.md)

- [Use Explorer in the Security &amp; Compliance Center](use-explorer-in-security-and-compliance.md)

### Periodically review and revise your ATP policies

- [Keep your Office 365 users safe with Office 365 threat investigation and response](keep-users-safe-with-office-365-ti.md) 

- [Use the smart reports and insights in the Office 365 Security &amp; Compliance Center](reports-and-insights-in-security-and-compliance.md) 