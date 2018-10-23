---
title: Release notes
titleSuffix: Configuration Manager
description: Learn about urgent issues that are not yet fixed in the product or covered in a Microsoft Support knowledge base article.
ms.date: 08/21/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 030947fd-f5e0-4185-8513-2397fb2ec96f
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Release notes for Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

With Configuration Manager, product release notes are limited to urgent issues. These issues aren't yet fixed in the product, or detailed in a Microsoft Support knowledge base article.  

Feature-specific documentation includes information about known issues that affect core scenarios.  

> [!TIP]  
>  This topic contains release notes for the current branch of Configuration Manager. For information on the technical preview branch, see [Technical Preview](/sccm/core/get-started/technical-preview)  

For information about the new features introduced with different versions, see the following articles:
- [What's new in version 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806)  
- [What's new in version 1802](/sccm/core/plan-design/changes/whats-new-in-version-1802)
- [What's new in version 1710](/sccm/core/plan-design/changes/whats-new-in-version-1710)



## Setup and upgrade  


### When using redistributable files from the CD.Latest folder, setup fails with a manifest verification error
<!-- 510080, 490569  -->

When you run setup from the CD.Latest folder created for version 1606, and use the redistributable files included with that CD.Latest folder, setup fails with the following errors in the Configuration Manager Setup log:

  `ERROR: File hash check failed for defaultcategories.dll`  
  `ERROR: Manifest verification failed. Wrong version of manifest?`

#### Workaround
Use one of the following options:
 - During Setup, choose to download the most current redistributable files from Microsoft. Use the latest redistributable files instead of the files included in the CD.Latest folder.
 - Manually delete the *cd.latest\redist\languagepack\zhh* folder, and then run Setup again.


### Setup command-line option JoinCEIP must be specified
<!--510806-->
*Applies to: Configuration Manager version 1802*

Starting in Configuration Manager version 1802, the Customer Experience Improvement Program (CEIP) feature is removed from the product. When [automating installation](/sccm/core/servers/deploy/install/command-line-options-for-setup) of a new site from a command-line or unattended script, setup returns an error that a required parameter is missing. 

#### Workaround
While it has no affect on the outcome of the setup process, include the **JoinCEIP** parameter in your setup command line.

 > [!Note]  
 > The EnableSQM parameter for [console setup](/sccm/core/servers/deploy/install/install-consoles) is not required.


### Cloud service manager component stopped on site server in passive mode
<!--VSO 2858826, SCCMDocs issue 772-->
*Applies to: Configuration Manager version 1806*

If the [service connection point](/sccm/core/servers/deploy/configure/about-the-service-connection-point) is co-located with a [site server in passive mode](/sccm/core/servers/deploy/configure/site-server-high-availability), then deployment and monitoring of a [cloud management gateway](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway) doesn't start. The cloud service manager component (SMS_CLOUD_SERVICES_MANAGER) is in a stopped state.

#### Workaround
Move the service connection point role to another server.



<!-- ## Backup and recovery  -->


## Client deployment and upgrade

### Azure AD-enabled clients can't communicate with management point
<!--501089-->  
*Applies to: Configuration Manager version 1706*
<!--also fixed in 1710 HFRU-->  
In the scenario to [install and assign Configuration Manager Windows 10 clients using Azure AD for authentication](/sccm/core/clients/deploy/deploy-clients-cmg-azure), client communication fails when the HTTPS-enabled management point uses alternate database credentials. 

#### Workaround
Mitigate this issue with one of the following actions:
- Update the site to the latest version, and apply the latest hotfix
- Change the credentials that the management point uses.


<!-- ## Operating system deployment  -->



## Software updates

### Changing Office 365 client setting doesn’t apply 
<!--511551-->
*Applies to: Configuration Manager version 1802*  

Deploy a [client setting](/sccm/core/clients/deploy/about-client-settings#enable-management-of-the-office-365-client-agent) with **Enable Management of the Office 365 Client Agent** configured to `Yes`. Then change that setting to `No` or `Not Configured`. After updating policy on targeted clients, Office 365 updates are still managed by Configuration Manager. 

#### Workaround
Change the following registry value to `0` and restart the **Microsoft Office Click-to-Run Service** (ClickToRunSvc):

```
[HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\office\16.0\Common\officeupdate]
"OfficeMgmtCOM"=dword:00000000
```



## Mobile device management  

### You can no longer deploy Windows Phone 8.1 VPN profiles to Windows 10
<!-- 503274  -->
*Applies to: Configuration Manager version 1710*

You can't create a VPN profile, using the Windows Phone 8.1 workflow, which is also applicable to Windows 10 devices. For these profiles, the creation wizard no longer shows the Supported Platforms page. Windows Phone 8.1 is automatically selected on the back-end. The Supported Platforms page is available in the profile properties, but it doesn't display the Windows 10 options.

#### Workaround
 Use the Windows 10 VPN profile workflow for Windows 10 devices. If this option isn't feasible for your environment, contact support. Support can help you add the Windows 10 targeting.



<!-- ## Reports and monitoring    -->
<!-- ## Conditional access   -->
<!-- ## Endpoint Protection -->
