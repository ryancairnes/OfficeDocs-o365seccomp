---
title: "Deploy Conditional Access App Control for Office 365 apps"
ms.author: deniseb
author: denisebmsft
manager: laurawi
ms.reviewer: alesibov
ms.audience: Admin
ms.topic: reference
ms.date: 02/14/2019
ms.service: o365-administration
localization_priority: Normal
description: "Follow these steps to configure Azure AD Office 365 apps to be controlled by Office 365 Cloud App Security Conditional Access App Control."
---

# Deploy Conditional Access App Control for Office 365 apps

|****Evaluation** \>**|****Planning** \>**|****Deployment** \>**|****Utilization****|
|:-----|:-----|:-----|:-----|
|[Start evaluating](office-365-cas-overview.md) <br/> |[Start planning](get-ready-for-office-365-cas.md) <br/> |You are here!  <br/> [Next step](ocas-session-policies.md) <br/> |[Start utilizing](utilization-activities-for-ocas.md) <br/> |

Follow these steps to configure Azure AD Office 365 apps to be controlled by Office 365 Cloud App Security Conditional Access App Control.

**Step 1: [Create an Azure AD conditional access test policy](#step-1-create-an-azure-ad-conditional-access-test-policy)**

**Step 2: [Sign in with a user scoped to the policy in the apps](#step-2-sign-in-with-a-user-scoped-to-the-policy-in-the-apps)**

**Step 3: If you did not select a built-in Cloud App Security policy in Azure AD or if you want to apply the policy to a non-featured app, [Configure advanced controls in the Cloud App Security portal](#step-3-configure-advanced-controls-in-the-cloud-app-security-portal)**

**Step 4: [Test the deployment](#step-4-test-the-deployment)**

> [!IMPORTANT]
> To deploy Conditional Access App Control for Office 365 apps, you need a valid [license for Azure AD Premium P1](https://docs.microsoft.com/azure/active-directory/license-users-groups) as well as a Office 365 Cloud App Security license.

## Step 1: Create an Azure AD conditional access test policy 

1. In Azure Active Directory, under **Security**, click on **Conditional access**.

2. Click **New policy** and create a new policy.

3. In the TEST policy, under **Users**, assign a test user or user that can be used for an initial sign-on and verification.

4. In the TEST policy, under **Cloud app**, assign the apps you want to control with Conditional Access App Control.

5. Under **Session**, set the policy to use either of the built-in policies, **Monitor only** or **Block downloads**. Or select **Use custom policy** to set an advanced policy in the Cloud App Security portal.

6. Add any applicable **Condition assignments** or **Grant controls** (optional).

> ![Azure AD conditional access](media/image1.png)

## Step 2: Sign in with a user scoped to the policy in the apps 

After you've created the policy, sign in to each app configured in that policy. Make sure you sign in using a user configured in the policy. Make sure to first sign out of existing sessions.

Cloud App Security will sync your policy details to its servers for each new app you log in to. This may take up to one minute.

## Step 3: Configure advanced controls in the Cloud App Security portal 

The instructions above helped you create a built-in Cloud App Security policy for featured apps directly in Azure AD.

To configure an advanced policy, create an [access policy](ocas-access-policies.md) or a [session policy](ocas-session-policies.md) in the Office 365 Cloud App Security portal.

### To identify devices using client certificates (this is optional):

1. Go to the settings cog and choose **Device identification**.

2. Upload one or more root or intermediate certificates.

3. After the certificate is uploaded, you can create access policies and session policies based on **Device tag** and **Valid client certificate**.

![Conditional access app control device ID](media/image2.png)

> [!NOTE]
> A certificate is only requested from a user if the session matches a policy that uses the valid client certificate filter.
> 
## Step 4: Test the deployment 

1. First sign out of any existing sessions. Then, try to sign in to each app that was successfully deployed. Sign in using a user that matches the policy configured in Azure AD.

2. In the Cloud App Security portal, under **Investigate**, select **Activity log**, and make sure the login activities are captured for each app.

3. You can filter by clicking on **Advanced**, and then filtering using **Source equals Access control**.

4. It's recommended that you sign into mobile and desktop apps from managed and unmanaged devices. This is to make sure that the activities are properly captured in the activity log. To verify that the activity is properly captured, click on a single sign-on log on activity so that it opens the activity drawer. Make sure the **User agent tag** properly reflects whether the device is a native client (meaning either a mobile or desktop app) or the device is a managed device (compliant, domain joined, or valid client certificate).

> [!NOTE]
> After it is deployed, you can't remove an app from the Conditional Access App Control page. As long as you don't set a session or access policy on the app, the Conditional Access App Control won't change any behavior for the app.

## Next steps

- [Learn about session policies in Office 365 Cloud App Security](ocas-session-policies.md)

- [Learn about access policies in Office 365 Cloud App Security](ocas-access-policies.md) 

- [Group your IP addresses to simplify management in Office 365 Cloud App Security](group-your-ip-addresses-in-ocas.md)