---
title: "Manage mailbox auditing"
ms.author: chrisda
author: chrisda
manager: serdars
ms.audience: Admin
ms.topic: article
ms.service: O365-seccomp
localization_priority: Normal
ms.collection: 
- Strat_O365_IP
- M365-security-compliance
search.appverid: 
- MOE150
- MET150
ms.assetid: aaca8987-5b62-458b-9882-c28476a66918
description: "Mailbox audit logging is turned on by default in Microsoft 365 (also called default mailbox auditing or mailbox auditing on by default). This means that certain actions performed by mailbox owners, delegates, and admins are automatically logged in a mailbox audit log, where you can search for activities performed on the mailbox."
---

# Manage mailbox auditing

Starting in January 2019, Microsoft is turning on mailbox audit logging by default for all Microsoft 365 organizations. This means that certain actions performed by mailbox owners, delegates, and admins are automatically logged, and the corresponding mailbox audit records will be available when you search for them in the mailbox audit log. Before mailbox auditing was turned on by default, you had to manually enable it for every user mailbox in your organization.

Here are some benefits of mailbox auditing on by default:

- Auditing will be enabled by default when you create a new mailbox. You won't have to manually enable it for new users.

- You won't have manage the mailbox actions that are audited. A predefined set of mailbox actions are audited by default for each type of logon. These [logon types](#mailbox-actions-logged-by-default) are Owner, Delegate, and Admin.

- New mailbox actions that are released by Microsoft will be audited by default. When Microsoft releases a new mailbox action (particularly ones that help protect your organization and help with forensic investigations), it will automatically be added to the list of mailbox actions audited by default. This means you don't have to add new actions to the list of mailbox actions performed by owners, delegates, or admins.

- Ensures that you're auditing the same actions for all mailboxes, so you have a consistent mailbox auditing policy across your organization.

> [!TIP]
> The important thing to remember is that with the release of mailbox auditing on by default, you don't have to do anything to manage mailbox auditing. However, if you want to learn more, change the behavior from the default settings, or turn it off altogether, this topic can help you with that.

## Verify mailbox auditing on by default is turned on

To verify that mailbox auditing on by default is turned on for your organization, run the following command in [Exchange Online PowerShell](https://docs.microsoft.com/powershell/exchange/exchange-online/connect-to-exchange-online-powershell/connect-to-exchange-online-powershell):

```
Get-OrganizationConfig | Format-List AuditDisabled
```

A value of **False** indicates that mailbox auditing on by default is enabled for the organization. This on by default organizational value overrides the mailbox auditing setting on specific mailboxes. For example, if mailbox auditing is disabled for a mailbox (the *AuditEnabled* property is **False**), the default mailbox actions will still be audited for the mailbox, because mailbox auditing on by default is enabled for the organization.

To keep mailbox auditing disabled for specific mailboxes, you can set up mailbox auditing bypass for the mailbox owner and other users who have been delegated access to the mailbox. For more information, see the [Bypass mailbox audit logging](#bypass-mailbox-audit-logging) section in this topic.

> [!NOTE]
> When mailbox auditing on by default is turned on for the organization, the *AuditEnabled* property for affected mailboxes won't be changed from **False** to **True**. In other words, mailbox auditing on by default ignores the *AuditEnabled* property for mailboxes.

## Supported mailbox types

The following table shows the mailbox types that are currently supported by mailbox auditing on by default:

|**Mailbox type**|**Supported**|**Not supported**|
|:---------|:---------:|:---------:|
|User mailboxes|![Check mark](media/f3b4c351-17d9-42d9-8540-e48e01779b31.png)||
|Shared mailboxes|![Check mark](media/f3b4c351-17d9-42d9-8540-e48e01779b31.png)||
|Office 365 Group mailboxes|![Check mark](media/f3b4c351-17d9-42d9-8540-e48e01779b31.png)||
|Resource mailboxes||![Check mark](media/f3b4c351-17d9-42d9-8540-e48e01779b31.png)|
|Public folder mailboxes||![Check mark](media/f3b4c351-17d9-42d9-8540-e48e01779b31.png)|

## Mailbox actions logged by default

Logon types classify the type of user that did something to the mailbox. The following list describes the logon types that are used in mailbox audit logging:

- **Owner**: The mailbox owner.

- **Delegate**

  - A user who's been assigned the SendAs, SendOnBehalf, or FullAccess permission to another mailbox.

  - An admin who's been assigned the FullAccess permission to a user's mailbox.

- **Admin**

  - The mailbox is searched with one of the following Microsoft eDiscovery tools:

    - Content Search in the Compliance center.

    - eDiscovery or Advanced eDiscovery in the Compliance center.

    - In-Place eDiscovery in Exchange Online.

  - The mailbox is accessed by using the [Microsoft Exchange Server MAPI Editor](https://go.microsoft.com/fwlink/p/?linkId=204086).

The following table lists the mailbox actions that are currently logged by default for each logon type:

|**Admin actions**|**Delegate actions**|**Owner actions**|
|:---------|:---------|:---------|
|Create|Create|HardDelete|
|HardDelete|HardDelete|MoveToDeletedItems|
|MoveToDeletedItems|MoveToDeletedItems|SoftDelete|
|SendAs|SendAs|Update|
|SendOnBehalf|SendOnBehalf|UpdateCalendarDelegation|
|SoftDelete|SoftDelete|UpdateFolderPermissions|
|Update|Update|UpdateInboxRules|
|UpdateCalendarDelegation|UpdateFolderPermissions||
|UpdateFolderPermissions|UpdateInboxRules||
|UpdateInboxRules|||

The following table describes these default mailbox actions:

|**Mailbox action**|**Description**|
|:---------|:---------|
|**Create**|An item was created in the Calendar, Contacts, Notes, or Tasks folder in the mailbox (for example, a new meeting request is created). Note that creating, sending, or receiving a message isn't audited. Also, creating a mailbox folder is not audited.|
|**HardDelete**|A message was purged from the Recoverable Items folder.|
|**MoveToDeletedItems**|A message was deleted and moved to the Deleted Items folder.|
|**SendAs**|A message was sent using the SendAs permission. This means another user sent the message as though it came from the mailbox owner.|
|**SendOnBehalf**|A message was sent using the SendOnBehalf permission. This means another user sent the message on behalf of the mailbox owner. The message indicates to the recipient who the message was sent on behalf of and who actually sent the message.|
|**SoftDelete**|A message was permanently deleted or deleted from the Deleted Items folder. Soft-deleted items are moved to the Recoverable Items folder.|
|**Update**|A message or its properties was changed.|
|**UpdateCalendarDelegation**|A calendar delegation was assigned to a mailbox. Calendar delegation gives someone else in the same organization permissions to manage the mailbox owner's calendar.|
|**UpdateFolderPermissions**|A folder permission was changed. Folder permissions control which users in your organization can access folders in a mailbox and the messages located in those folders.|
|**UpdateInboxRules**|An inbox rule was added, removed, or changed. Inbox rules are used to process messages in the user's Inbox based on the specified conditions and take actions when the conditions of a rule are met, such as moving a message to a specified folder or deleting a message.|

For a complete list of mailbox actions, including actions that are available but aren't included in the set of default actions, see the [Mailbox auditing actions](#mailbox-auditing-actions) section in this topic.

> [!IMPORTANT]
> If you have explicitly configured the mailbox actions to audit for any logon type prior to mailbox auditing on by default being turned on for organization, the existing settings are preserved on the mailbox and won't be overwritten by the default mailbox actions described in this section. To revert to the default mailbox actions (which you can do at any time), see the [Restore the default mailbox actions](#restore-the-default-mailbox-actions) section later in this topic.

### Verify that default mailbox actions are being logged for each logon type

Mailbox auditing on by defaults adds a new *DefaultAuditSet* property to all mailboxes. The value of this property indicates whether the default mailbox actions (managed by Microsoft) are audited for each logon type on the mailbox. You can run the following Exchange Online PowerShell command to display the values of this property:

```
Get-Mailbox -Identity <UserName> | Format-List DefaultAuditSet
```

The value `Admin, Delegate, Owner` indicates:

- The default mailbox actions for all three logon types are being audited.

- An admin *has not* changed the actions for any logon type. Note this is the default state after mailbox auditing on by default is initially turned on in your organization.

If an admin changed the mailbox actions that are audited for a logon type (by using the *AuditAdmin*, *AuditDelegate*, or *AuditOwner* parameters on the **Set-Mailbox** cmdlet), the value of the *DefaultAuditSet* property will be different. For example:

- The value `Owner` indicates:

  - Only the default mailbox actions for the mailbox owner are being audited.

  - The actions for the `Delegate` and `Admin` logon types have been changed.

- A blank value indicates the mailbox actions for all three logon types have been changed.

For more information, see the [Change or restore mailbox actions logged by default](#change-or-restore-mailbox-actions-logged-by-default) section in this topic

### Display a list of mailbox actions logged by default

You can run the following commands in Exchange Online PowerShell to display the list of mailbox actions that are currently being for a mailbox for each logon type.

#### Owner actions

```
Get-Mailbox -Identity <UserName> | Select-Object -ExpandProperty AuditOwner
```

#### Delegate actions

```
Get-Mailbox -Identity <UserName> | Select-Object -ExpandProperty AuditDelegate
```

#### Admin actions

```
Get-Mailbox -Identity <UserName> | Select-Object -ExpandProperty AuditAdmin
```

## Change or restore mailbox actions logged by default

As previously explained, one of the key benefits of having mailbox auditing on by default is you don't have to manage the mailboxes actions that are audited. Microsoft does this for you and will automatically add new mailbox actions to be audited by default when they are released.

However, your organization may be required to audit a different set of mailbox actions. This section shows you how to change the mailbox actions that are audited for each logon type, and how to revert back to the Microsoft-managed default actions.

> [!IMPORTANT]
> If you make any change to the mailbox actions for a user that are logged by default (as described in the next section), then any new mailbox actions released by Microsoft will not be audited for those mailboxes. You'll have to explicitly add a new mailbox action to the list of actions that are audited for a logon type.

### Change the mailbox actions to audit

You can use the *AuditAdmin*, *AuditDelegate*, or *AuditOwner* parameters on the **Set-Mailbox** cmdlet to change the mailbox actions that are audited, depending on the logon type. You can use two different methods to specify the mailbox actions:

- *Replace* (overwrite) the existing values by using this syntax: `action1,action2,...actionN`.

- *Add or remove* mailbox actions without affecting other existing values by using this syntax: `@{Add="action1","action2",..."actionN"}` or `@{Remove="action1","action2",..."actionN"}`.

This example changes the admin mailbox actions by overwriting the default actions with SoftDelete and HardDelete.

```
Set-Mailbox -Identity <UserName> -AuditAdmin HardDelete,SoftDelete
```

This example adds the MailboxLogin owner action.

```
Set-Mailbox -Identity <UserName> -AuditOwner @{Add="MailboxLogin"}
```

This example removes the MoveToDeletedItems delegate action.

```
Set-Mailbox -Identity <UserName> -AuditDelegate @{Remove="MoveToDeletedItems"}
```

Regardless of the method you use, changing the mailbox actions that are audited has the following results:

- For the logon type you changed, the mailbox actions that are audited by default are no longer managed by Microsoft.

- The logon type that you changed is no longer displayed in the *DefaultAuditSet* property value for the mailbox as [previously described](#verify-that-default-mailbox-actions-are-being-logged-for-each-logon-type).

### Restore the default mailbox actions

If you made changes to the mailbox actions that are audited for a logon type, you can restore the default mailbox actions for one or all of the logon types by using this syntax:


```
Set-Mailbox -Identity <UserName> -DefaultAuditSet <Admin | Delegate | Owner>
```

This example restores the default mailbox actions that are audited for all logon types on the mailbox mark@contoso.onmicrosoft.com.

```
Set-Mailbox -Identity mark@contoso.onmicrosoft.com -DefaultAuditSet Admin,Delegate,Owner
```

This example restores the default mailbox actions that are audited for the Admin logon type on the mailbox chris@contoso.onmicrosoft.com, but leaves the customized mailbox actions for Delegate and Owner logon types.

```
Set-Mailbox -Identity chris@contoso.onmicrosoft.com -DefaultAuditSet Admin
```

Restoring he default mailbox actions that are audited for a logon type has the following results:

- The current list of mailbox actions will be replaced with the default mailbox actions for the logon type.

- Any new mailbox actions that are released by Microsoft are automatically added to the list of audited actions for the logon type.

- The *DefaultAuditSet* property value for the mailbox will be updated to include the logon type.

## Turn off mailbox auditing on by default for your organization

You can turn off mailbox auditing on by default for your entire organization by running the following command in Exchange Online PowerShell:

```
Set-OrganizationConfig -AuditDisabled $true
```

Turning off mailbox auditing on by default in your organization has the following results:

- Mailbox auditing is disabled for your organization.

- From the time you disabled mailbox auditing on by default, no mailbox actions will be audited, even if auditing is enabled on a mailbox (the *AuditEnabled* property on the mailbox is **True**).

- Mailbox auditing won't be enabled for new mailboxes and setting the *AuditEnabled* property on a new (or existing) mailbox to **True** will be ignored.

- Any mailbox audit bypass association settings (configured by using the **Set-MailboxAuditBypassAssociation** cmdlet) will be ignored.

- Existing mailbox audit records be retained until the audit log age limit for the the record expires.

### Turn on mailbox auditing on by default

To turn mailbox auditing back on for your organization, run the following command in Exchange Online PowerShell:

```
Set-OrganizationConfig -AuditDisabled $false
```

## Bypass mailbox audit logging

Currently, you can't disable mailbox auditing for specific mailboxes when mailbox auditing on by default is turned on in your organization. For example, setting the *AuditEnabled* mailbox property to **False** is ignored.

However, you can still use the **Set-MailboxAuditBypassAssociation** cmdlet in Exchange Online PowerShell to prevent *any and all* mailbox actions by the specified users from being logged, regardless where the actions occurred. For example:

- Mailbox owner actions performed by the specified users aren't logged.

- Delegate actions performed by the specified users on other users' mailboxes (including shared mailboxes) aren't logged.

- Admin actions performed by the specified users aren't logged.

To bypass mailbox audit logging for a specific user, run the following command:

```
Set-MailboxAuditBypassAssociation -Identity <UserName> -AuditByPassEnabled $true
```

To verify that auditing is bypassed for the specified user, run the following command:

```
Get-MailboxAuditBypassAssociation -Identity <UserName> | Format-List AuditByPassEnabled
```

A value of **True** indicates that mailbox audit logging is bypassed for that user.

## Mailbox auditing actions

The following table summarizes the actions that are audited for each user logon type.

**Notes**:

- An asterisk ( **<sup>\*</sup>** ) indicates that the action is logged by default when default mailbox auditing is enabled for the logon type.

- **No** indicates that an action can't be logged for that logon type.

- An admin who has been assigned the Full Access permission to a user's mailbox is considered a delegate user.

|**Action**|**Description**|**Admin**|**Delegate**|**Owner**|
|:-----|:-----|:-----|:-----|:-----|
|**Copy**|A message was copied to another folder.|Yes|No|No|
|**Create**|An item is created in the Calendar, Contacts, Notes, or Tasks folder in the mailbox; for example, a new meeting request is created. Note that creating, sending, or receiving a message isn't audited. Also, creating a mailbox folder is not audited.|Yes<sup>\*</sup>|Yes<sup>\*</sup>|Yes|
|**FolderBind**<sup>1</sup>|A mailbox folder was accessed. This action is also logged when the admin or delegate opens the mailbox.|Yes|Yes|No|
|**HardDelete**|A message was purged from the Recoverable Items folder.|Yes<sup>\*</sup>|Yes<sup>\*</sup>|Yes<sup>\*</sup>|
|**MailboxLogin**|The user signed into their mailbox.|No|No|Yes|
|**MessageBind**<sup>2</sup>|A message was viewed in the preview pane or opened.|Yes|No|No|
|**Move**|A message was moved to another folder.|Yes|Yes|Yes|
|**MoveToDeletedItems**|A message was deleted and moved to the Deleted Items folder.|Yes<sup>\*</sup>|Yes<sup>\*</sup>|Yes<sup>\*</sup>|
|**SendAs**|A message was sent using the SendAs permission. This means another user sent the message as though it came from the mailbox owner.|Yes<sup>\*</sup>|Yes<sup>\*</sup>|No|
|**SendOnBehalf**|A message was sent using the SendOnBehalf permission. This means another user sent the message on behalf of the mailbox owner. The message indicates to the recipient who the message was sent on behalf of and who actually sent the message.|Yes<sup>\*</sup>|Yes<sup>\*</sup>|No|
|**SoftDelete**|A message was permanently deleted or deleted from the Deleted Items folder. Soft-deleted items are moved to the Recoverable Items folder.|Yes<sup>\*</sup>|Yes<sup>\*</sup>|Yes<sup>\*</sup>|
|**Update**|A message or its properties was changed.|Yes<sup>\*</sup>|Yes<sup>\*</sup>|Yes<sup>\*</sup>|
|**UpdateCalendarDelegation**|A calendar delegation was assigned to a mailbox. Calendar delegation gives someone else in the organization permissions to manage the mailbox owner's calendar.|Yes<sup>\*</sup>|No|Yes<sup>\*</sup>|
|**UpdateFolderPermissions**|A folder permission was changed. Folder permissions control which users in your organization can access folders in a mailbox and the messages located in those folders.|Yes<sup>\*</sup>|Yes<sup>\*</sup>|Yes<sup>\*</sup>|
|**UpdateInboxRules**|An inbox rule has been added, removed, or changed. Inbox rules are used to process messages in the user's Inbox based on the specified conditions and take actions when the conditions of a rule are met, such as moving a message to a specified folder or deleting a message.|Yes<sup>\*</sup>|Yes<sup>\*</sup>|Yes<sup>\*</sup>|

<sup>1</sup>Audit records for folder bind actions performed by delegates are consolidated. One audit record is generated for individual folder access within 24 hour period.

<sup>2</sup>The MessageBind action has been deprecated in Exchange Online, and is no longer available to add to the list of mailbox actions for the admin logon type.

## More information

- By default, mailbox audit log records are retained for 90 days before they are deleted. You can change the age limit for audit log records by using the *AuditLogAgeLimit* parameter on the **Set-Mailbox** cmdlet in Exchange Online PowerShell. However, increasing this value doesn't allow you to search for events that are older than 90 days in the Microsoft 365 audit log.

  If you increase the age limit, you need to use the [Search-MailboxAuditLog](https://docs.microsoft.com/powershell/module/exchange/policy-and-compliance-audit/search-mailboxauditlog) cmdlet in Exchange Online PowerShell to search the user's mailbox audit log for records that are older than 90 days.

- If you've changed the *AuditLogAgeLimit* property for a mailbox prior to mailbox auditing on by default being turned on for organization, the existing audit log age limit for that mailbox will not be changed; in other words, mailbox auditing on by default doesn't effect the current age limit for mailbox audit records.

- Mailbox audit log records are stored in a subfolder (named *Audits*) in the Recoverable Items folder in each user's mailbox. Keep the following things in mind about mailbox audit records and the Recoverable Items folder:

  - Mailbox audit records count against the storage quota of the Recoverable Items folder, which is 30GB by default (the Warning quota is 20 GB). Note that the storage quota for the Recoverable Items folder is automatically increased from to 100 GB (90 MB Warning quota) when a hold is placed on a mailbox or the mailbox is assigned to a retention policy in the Compliance Center.

  - Mailbox audit records also counts against the [folder limit for the Recoverable Items folder](https://docs.microsoft.com/office365/servicedescriptions/exchange-online-service-description/exchange-online-limits#mailbox-folder-limits). The maximum number of items (which are audit records in this case) that can be stored in the Audits subfolder is 3 million items.

    > [!NOTE]
    > It's unlikely that mailbox auditing on by default will impact the storage quota or the folder limit for the Recoverable Items folder.

    - You can run the following command in Exchange Online PowerShell to display the size and number of items in the Audits subfolder in the Recoverable Items folder:

      ```
      Get-MailboxFolderStatistics <username> -FolderScope RecoverableItems | Where-Object {$_.Name -eq 'Audits'} | Format-List FolderPath,FolderSize,ItemsInFolder
      ```

    - You can't directly access an audit log record in the Recoverable Items folder; instead, you use the **Search-MailboxAuditLog** cmdlet or search the Microsoft 365 audit log to find and view mailbox audit records.

- If a mailbox is placed on hold or assigned to a retention policy in the Compliance Center, audit log records are still retained for the duration defined by the *AuditLogAgeLimit* property for the mailbox (which is set to 90 days by default). To retain audit log records longer for mailboxes on hold, you have to increase the retention period by increasing the value for the *AuditLogAgeLimit* property.
