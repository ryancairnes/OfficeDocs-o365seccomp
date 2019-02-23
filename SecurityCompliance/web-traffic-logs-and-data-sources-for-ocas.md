---
title: "Web traffic logs and data sources for Office 365 Cloud App Security"
ms.author: deniseb
author: denisebmsft
manager: laurawi
ms.date: 12/26/2018
ms.audience: ITPro
ms.topic: reference
ms.service: O365-seccomp
localization_priority: Normal
search.appverid:
- MET150
- MOE150
ms.assetid: 290b02bf-a988-4fb9-88b2-34e408216ac8
description: "Office 365 Cloud App Security works with web traffic logs from a wide range of providers. Read this article to learn more about web traffic logs and supported data sources for Office 365 Cloud App Security."
---

# Web traffic logs and data sources for Office 365 Cloud App Security
  
|****Evaluation** \>**|****Planning** \>**|****Deployment** \>**|****Utilization****|
|:-----|:-----|:-----|:-----|
|[Start evaluating](office-365-cas-overview.md) <br/> |[Start planning](get-ready-for-office-365-cas.md) <br/> |[Start deploying](turn-on-office-365-cas.md) <br/> |You are here!  <br/> [Next steps](#next-steps) <br/> |
  
You can use a wide range of web traffic log files and data sources with Office 365 Cloud App Security. However, your web traffic log files must include specific information and be formatted a certain way so that they will work with Office 365 Cloud App Security app discovery reports and the Cloud Discovery dashboard. Use this article as a reference guide for the web traffic logs and data sources you'll use with Office 365 Cloud App Security.
  
> [!NOTE]
> You must be a global administrator, security administrator, or security reader to access the Security &amp; Compliance Center and Office 365 Cloud App Security portal. See [Permissions in the Office 365 Security &amp; Compliance Center](permissions-in-the-security-and-compliance-center.md). 
  
## Web traffic log requirements

Office 365 Cloud App Security uses data in your web traffic logs to help you understand which apps people in your organization are using. The more details that are included in the log files, the better visibility you'll have into user activity.
  
The following sections list the necessary attributes and additional requirements for your web traffic logs to work correctly with Office 365 Cloud App Security.

### Attributes

Office 365 Cloud App Security can't show or analyze attributes that aren't included in your web traffic logs. For example, Cisco ASA Firewall's standard log format does not have the number of uploaded bytes per transaction, the username, or a target URL (only a target IP). Therefore, those attributes are not shown in Cloud Discovery data, and visibility into the cloud apps is limited. For Cisco ASA firewalls, the information level must be set to 6. 

Your web traffic logs should include the following attributes:

- Date of the transaction
- Source IP
- Source user (highly recommended)
- Destination IP address
- Destination URL (recommended; URLs provide higher accuracy for cloud app detection than IP addresses)
- Total amount of data (recommended; data information is highly valuable)
- Amount of uploaded or downloaded data (recommended; provides insights about cloud app usage patterns)
- Action taken (allowed or blocked)

### Additional requirements

In addition to including the attributes listed earlier in this article, your web traffic logs should meet the following requirements:

- The data source for the log files must be supported.
- The format the log files use must match the standard format. When the file is uploaded, app discovery will verify this.
- The events in the log must have taken place no more than 90 days ago.
- The log file must include outbound traffic information that can be analyzed for network activity.
  
## Data attributes for different vendors

The following table summarizes the information in web traffic logs from various vendors. **Be sure to check with your vendor for the most current information.**


|                 Data source                  |    Target App URL    |    Target App IP     |       Username       |      Origin IP       |    Total traffic     |    Uploaded bytes    |
|----------------------------------------------|----------------------|----------------------|----------------------|----------------------|----------------------|----------------------|
|                  Barracuda                   | <strong>Yes</strong> | <strong>Yes</strong> | <strong>Yes</strong> | <strong>Yes</strong> |          No          |          No          |
|                  Blue Coat                   | <strong>Yes</strong> |          No          | <strong>Yes</strong> | <strong>Yes</strong> | <strong>Yes</strong> | <strong>Yes</strong> |
|                  Checkpoint                  |          No          | <strong>Yes</strong> |          No          | <strong>Yes</strong> |          No          |          No          |
|              Cisco ASA (Syslog)              |          No          | <strong>Yes</strong> |          No          | <strong>Yes</strong> | <strong>Yes</strong> |          No          |
|           Cisco ASA with FirePOWER           | <strong>Yes</strong> | <strong>Yes</strong> | <strong>Yes</strong> | <strong>Yes</strong> | <strong>Yes</strong> | <strong>Yes</strong> |
|                  Cisco FWSM                  |          No          | <strong>Yes</strong> |          No          | <strong>Yes</strong> | <strong>Yes</strong> |          No          |
|              Cisco Ironport WSA              | <strong>Yes</strong> | <strong>Yes</strong> | <strong>Yes</strong> | <strong>Yes</strong> | <strong>Yes</strong> | <strong>Yes</strong> |
|                 Cisco Meraki                 | <strong>Yes</strong> | <strong>Yes</strong> |          No          | <strong>Yes</strong> |          No          |          No          |
|           Clavister NGFW (Syslog)            | <strong>Yes</strong> | <strong>Yes</strong> | <strong>Yes</strong> | <strong>Yes</strong> | <strong>Yes</strong> | <strong>Yes</strong> |
|                SonicWall (formerly Dell)                | <strong>Yes</strong> | <strong>Yes</strong> |          No          | <strong>Yes</strong> | <strong>Yes</strong> | <strong>Yes</strong> |
|            Digital Arts i-FILTER             | <strong>Yes</strong> | <strong>Yes</strong> | <strong>Yes</strong> | <strong>Yes</strong> | <strong>Yes</strong> | <strong>Yes</strong> |
|                  Fortigate                   |          No          | <strong>Yes</strong> |          No          | <strong>Yes</strong> | <strong>Yes</strong> | <strong>Yes</strong> |
|                 Juniper SRX                  |          No          | <strong>Yes</strong> |          No          | <strong>Yes</strong> | <strong>Yes</strong> | <strong>Yes</strong> |
|                 Juniper SSG                  |          No          | <strong>Yes</strong> | <strong>Yes</strong> | <strong>Yes</strong> | <strong>Yes</strong> | <strong>Yes</strong> |
|                  McAfee SWG                  | <strong>Yes</strong> |          No          |          No          | <strong>Yes</strong> | <strong>Yes</strong> | <strong>Yes</strong> |
|                    MS TMG                    | <strong>Yes</strong> |          No          | <strong>Yes</strong> | <strong>Yes</strong> | <strong>Yes</strong> | <strong>Yes</strong> |
|              Palo Alto Networks              |          No          | <strong>Yes</strong> | <strong>Yes</strong> | <strong>Yes</strong> | <strong>Yes</strong> | <strong>Yes</strong> |
|                    Sophos                    | <strong>Yes</strong> | <strong>Yes</strong> | <strong>Yes</strong> | <strong>Yes</strong> | <strong>Yes</strong> |          No          |
|                Squid (Common)                | <strong>Yes</strong> |          No          | <strong>Yes</strong> | <strong>Yes</strong> |          No          | <strong>Yes</strong> |
|                Squid (Native)                | <strong>Yes</strong> |          No          | <strong>Yes</strong> | <strong>Yes</strong> |          No          | <strong>Yes</strong> |
| Websense - Investigative detail report (CSV) | <strong>Yes</strong> | <strong>Yes</strong> | <strong>Yes</strong> | <strong>Yes</strong> | <strong>Yes</strong> | <strong>Yes</strong> |
|    Websense - Internet activity log (CEF)    | <strong>Yes</strong> | <strong>Yes</strong> | <strong>Yes</strong> | <strong>Yes</strong> | <strong>Yes</strong> | <strong>Yes</strong> |
|                   Zscaler                    | <strong>Yes</strong> | <strong>Yes</strong> | <strong>Yes</strong> | <strong>Yes</strong> | <strong>Yes</strong> | <strong>Yes</strong> |
   
## Supported vendor firewalls and proxies

Office 365 Cloud App Security supports the following firewalls and proxies.
  
- Barracuda - Web App Firewall (W3C)  
- Blue Coat Proxy SG - Access log (W3C)
- Check Point
- Cisco ASA Firewall (make sure to set the information level to 6)
- Cisco ASA with FirePOWER   
- Cisco IronPort WSA
- Cisco ScanSafe
- Cisco Merkai - URLs log
- Clavister NGFW (Syslog)
- Digital Arts i-FILTER
- Fortinet Fortigate
- iboss Secure Cloud Gateway
- Juniper SRX
- Juniper SSG
- McAfee Secure Web Gateway
- Microsoft Forefront Threat Management Gateway (W3C)
- Palo Alto series Firewall
- Sonicwall (formerly Dell)   
- Sophos SG
- Sophos XG
- Sophos Cyberoam
- Squid (Common)
- Squid (Native)
- Websense - Web Security Solutions - Investigative detail report (CSV)
- Websense - Web Security Solutions - Internet activity log (CEF)
- Zscaler
    
> [!NOTE]
> If a data source that you'd like to use is not included here, you can request that it be added to app discovery. To do that, when you're creating a report, select **Other** for **Data source**. Then type the name of the data source that you're trying to upload. We'll review the log, and let you know if we add support for that log type. Alternatively, you can [define a custom parser](https://docs.microsoft.com/cloud-app-security/custom-log-parser) that matches your format. 
  
## Troubleshoot errors when log files are uploaded

After you upload web traffic log files, check the governance log to see if there were any errors. If there are errors, use the information in the following table to resolve those errors.
  
|**Error**|**Description**|**Resolution**|
|:-----|:-----|:-----|
|Unsupported file type  <br/> |The file uploaded is not a valid log file. For example, an image file.  <br/> |Upload a text, zip, or gzip file that was directly exported from your firewall or proxy.  <br/> |
|Internal error  <br/> |An internal resource failure was detected.  <br/> |Click **Retry** to re-run the task.  <br/> |
|The log format does not match  <br/> |The log format you uploaded does not match the expected log format for this data source.  <br/> |
Verify that the log is not corrupt. Compare and match the log file format to the sample format shown on the upload page. |
|Transactions are more than 90 days old  <br/> |All transaction are more than 90 days old and therefore are being ignored.  <br/> |Export a new log with recent events and re-upload it.  <br/> |
|No transactions to catalogue cloud apps  <br/> |No transaction to any recognized cloud apps are found in the log.  <br/> |Verify that the log contains outbound traffic information.  <br/> |
|Unsupported log type  <br/> |When you select **Data source = Other (unsupported)**, the log is not parsed. Instead, it is sent for review to the [Microsoft Cloud App Security](https://aka.ms/whatiscas) technical team.  <br/> |The [Microsoft Cloud App Security](https://aka.ms/whatiscas) technical team builds a dedicated parser for each data source. Most popular data sources are already supported. When an unsupported data source is uploaded, it is reviewed and added to the list of potential new data source parsers.  <br/> When a new parser is added to the feature, a notification is included in the Microsoft Cloud App Security release notes.  <br/> |
   
## Next steps

- [Review and take action on alerts](review-office-365-cas-alerts.md)
    
- [Create app discovery reports](create-app-discovery-reports-in-ocas.md)
    
- [Review app discovery findings](review-app-discovery-findings-in-ocas.md)
    
- [Review your utilization activities for Office 365 Cloud App Security](utilization-activities-for-ocas.md)
    

