---
title: "Set up new Office 365 Message Encryption capabilities"
ms.author: krowley
author: kccross
manager: laurawi
ms.audience: ITPro
ms.topic: article
ms.service: O365-seccomp
localization_priority: Normal
search.appverid: 
- MET150
ms.assetid: 7ff0c040-b25c-4378-9904-b1b50210d00e
description: "New Office 365 Message Encryption capabilities built on top of Azure Information Protection, your organization can use protected email communication with people inside and outside your organization. The new OME capabilities work with other Office 365 organizations, Outlook.com, Gmail, and other email services."
---

# Set up new Office 365 Message Encryption capabilities

The new Office 365 Message Encryption (OME) capabilities allow organizations to share protected email with anyone on any device. Users can exchange protected messages with other Office 365 organizations, as well as non-Office 365 customers using Outlook.com, Gmail, and other email services.


>[!NOTE]
>This article is intended for administrators and IT professionals. If you're an end-user, see the list of articles in [Office 365 Message Encryption (OME)](ome.md) for appropriate solutions.

Follow the steps below to ensure that the New OME capabilities are available in your Office 365 tenant. 

## Verify Azure Rights Management (ARM) is active

>[!NOTE]
>The new OME capabilities leverage the protection features in [Azure Information Protection](https://docs.microsoft.com/en-us/azure/information-protection/what-is-information-protection), the technology used by [Azure Rights Management (ARM)](https://docs.microsoft.com/en-us/azure/information-protection/what-is-azure-rms).

The only prerequisite for using the new OME capabilities is that [Azure Rights Management (ARM)](https://docs.microsoft.com/en-us/azure/information-protection/what-is-azure-rms) must be activated in your Office 365 tenant. If it is, Office 365 activates the new OME capabilities automatically and you don't need to do anything. 

ARM is also activated automatically for most eligible plans, so you probably don't have to do anything in this regard either. See [Activating Azure Rights Management](https://docs.microsoft.com/en-gb/azure/information-protection/activate-service) for more.

>[!IMPORTANT]
>If you use Active Directory Rights Management service (AD RMS) with Exchange Online, you need to [migrate to Azure Information Protection](https://docs.microsoft.com/en-us/azure/information-protection/migrate-from-ad-rms-to-azure-rms) before you can use the new OME capabilities. AD RMS is not compatible with ARM.  

For more, see:

- [What subscriptions do I need to use the new OME capabilities?](ome-faq.md#what-subscriptions-do-i-need-to-use-the-new-ome-capabilities) to check whether your subscription plan includes Azure Information Protection (which includes ARM).   
-  [Azure Information Protection](https://azure.microsoft.com/en-us/services/information-protection/) for information about purchasing an eligible subscription.  

### Manually activating ARM

If you disabled ARM, or if it was not automatically activated for any reason, you can activated it manually in the :

- **Office 365 admin center**: See [How to activate Azure Rights Management from the Office 365 admin center](https://docs.microsoft.com/en-us/azure/information-protection/activate-office365) for instructions
- **Azure portal**: See [How to activate Azure Rights Management from the Azure portal](https://docs.microsoft.com/en-gb/azure/information-protection/activate-azure) for instructions. 


## Configure management of your Azure Information Protection tenant key

This is an optional step. Allowing Microsoft to manage the root key for Azure Information Protection is the default setting and recommended best practice for most Office 365 tenants. If this is the case, you don't need to do anything. 

There are many reasons, for example compliance requirements, that may necessitate you generating and managing your own root key (also known as bring your own key (BYOK)). If this is the case, we recommend that you complete the required steps before setting up the new OME capabilities. See [Planning and implementing your Azure Information Protection tenant key](https://docs.microsoft.com/information-protection/plan-design/plan-implement-tenant-key) for more. 


## Verify new OME configuration in Exchange Online PowerShell

You can verify that your Office 365 tenant is properly configured to use the new OME capabilities in [Exchange Online PowerShell](https://docs.microsoft.com/en-us/powershell/exchange/exchange-online/exchange-online-powershell?view=exchange-ps).
  
1. [Connect to Exchange Online PowerShell](https://docs.microsoft.com/en-us/powershell/exchange/exchange-online/connect-to-exchange-online-powershell/connect-to-exchange-online-powershell) using an account with global administrator permissions in your Office 365 tenant.

2. Run the Test-IRMConfiguration cmdlet using the following syntax:

     ```powershell
     Test-IRMConfiguration [-Sender <email address >]
     ```  

   **Example**: 
   
     ```powershell
     Test-IRMConfiguration -Sender securityadmin@contoso.com
     ```
     
     - Providing a sender email is optional, but forces the system to perform additional checks. Use the email address of any user in your Office 365 tenant. 
     
    Your results should be similar to:

     ```text
    Results : Acquiring RMS Templates ...
                - PASS: RMS Templates acquired.  Templates available: Contoso  - Confidential View Only, Contoso  - Confidential, Do Not 
            Forward.
            Verifying encryption ...
                - PASS: Encryption verified successfully.
            Verifying decryption ...
                - PASS: Decryption verified successfully.
            Verifying IRM is enabled ...
                - PASS: IRM verified successfully.

            OVERALL RESULT: PASS
    ```

   - Your Office 365 organization name will replace *Contoso*.

   - The default template names may be different from those displayed above. See [Configuring and managing templates for Azure Information Protection](https://docs.microsoft.com/en-us/azure/information-protection/configure-policy-templates) for more.

3. Run the Remove-PSSession cmdlet to disconnect from the Rights Management service.
    
     ```powershell
     Remove-PSSession $session
     ```

## Update mail flow rules to use new OME capabilities

If there are previously configured [mail flow rules to encrypt email](define-mail-flow-rules-to-encrypt-email.md) in your Office 365 tenant, you need to update these existing rules to use the new OME capabilities. For new deployments, this step is unnecessary at this stage.   

>[!Note]
>Mail flow rules define the conditions under which email messages are encrypted, and when encryption should be removed. See [Define mail flow rules to encrypt email messages in Office 365](define-mail-flow-rules-to-encrypt-email.md) for more.

To update existing rules to use the new OME capabilities:

1. In the Office 365 admin center, go to **Admin centers > Exchange**.

2. In the Exchange admin center, go to **Mail flow > Rules**. 
3. For each rule, in **Do the following**:
    - Select **Modify the message security**.
    - Select **Apply Office 365 Message Encryption and rights protection**.
    - Select an RMS template from the list
    - Select **Save**.
    - Select **OK**.
  
>[!IMPORTANT]
>If you do not update existing mail flow rules, your users will continue to receive encrypted mail that uses the previous HTML attachment format, instead of the new OME capabilities.
