---
title: Manage Office 365 ProPlus updates | Microsoft Docs
description: "Configuration Manager synchronizes Office 365 client updates from the WSUS catalog to the site server to make updates available to deploy to clients."
keywords:
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 02/03/2017
ms.topic: article
ms.prod: configuration-manager
ms.service:
ms.technology:
 - configmgr-sum
ms.assetid: eac542eb-9aa1-4c63-b493-f80128e4e99b
---

# Manage Office 365 ProPlus updates with Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Beginning in Configuration Manager version 1602, Configuration Manager has the ability to manage Office 365 client updates by using the software update management workflow. When Microsoft publishes a new Office 365 client update to the Office Content Delivery Network (CDN), Microsoft also publishes an update package to Windows Server Update Services (WSUS). After Configuration Manager synchronizes the Office 365 client update from the WSUS catalog to the site server, the update is available to deploy to clients.

## Office 365 Client Management dashboard  
Beginning in Configuration Manager version 1610, the Office 365 Client Management dashboard is available in the Configuration Manager console. To view the dashboard, go to **Software Library** > **Overview** > **Office 365 Client Management**.

<!--- >[!NOTE]
>In the **What's New** workspace in the Configuration Manager console, the new dashboard is incorrectly named **Office 365 Servicing dashboard**. --->

The dashboard displays charts for the following:

- Number of Office 365 clients
- Office 365 client versions
- Office 365 client languages
- Office 365 client channels     
For more information, see [Overview of update channels for Office 365 ProPlus](https://technet.microsoft.com/library/mt455210.aspx).
<!--- - Automatic deployment rules with Office 365 apps (have Office 365 Client selected in the set of available products). --->

<!---You can take the following actions on the dashboard:
- --->

At the top of the dashboard, use the **Collection** drop-down setting to filter the dashboard data by members of a specific collection.

### Display data in the Office 365 Client Management dashboard
The data that is displayed in the Office 365 Client Management dashboard comes from hardware inventory. Hardware inventory must be enabled and you must select the **Office 365 ProPlus Configurations** hardware inventory class before data is displayed in the dashboard.
#### To display data in the Office 365 Client Management dashboard
1. Enable hardware inventory, if it is not yet enabled. For details, see [Configure hardware inventory](\sccm\core\clients\manage\configure-hardware-inventory).
2. In the Configuration Manager console, navigate to **Administration** > **Client Settings** > **Default Client Settings**.  
3. On the **Home** tab, in the **Properties** group, click **Properties**.  
4. In the **Default Client Settings** dialog box, click **Hardware Inventory**.  
5. In the **Device Settings** list, click **Set Classes**.  
6. In the **Hardware Inventory Classes** dialog box, select **Office 365 ProPlus Configurations**.  
7.  Click **OK** to save your changes and close the **Hardware Inventory Classes** dialog box.  
The Office 365 Client Management dashboard will start displaying data as hardware inventory is reported.

<!---
 On the upper-right side of the dashboard, click **Office 365 Installer** to start the Office 365 Client Installation Wizard to deploy Office 365 apps to clients. For details, see [Deploy Office 365 apps to clients](#deploy-office-365-apps-to-clients).
- On the middle-right side of the dashboard, click **Create an ADR** to open the Automatic Deployment Rule Wizard to create a new automatic deployment rule (ADR). To create an ADR for Office 365 apps, select **Office 365 Client** when you choose the product. For more information, see [Automatically deploy software updates](/sccm/sum/deploy-use/automatically-deploy-software-updates).
- On the lower-right side of the dashboard, click **Create Client Agent Settings** to open Client Agent settings. For more information, see [About client settings](/sccm/core/clients/deploy/about-client-settings).
--->

## Deploy Office 365 updates with Configuration Manager
Use the following steps to deploy Office 365 updates with Configuration Manager:

1.  [Verify the requirements](https://technet.microsoft.com/library/mt628083.aspx) for using Configuration Manager to manage Office 365 client updates in the **Requirements for using Configuration Manager to manage Office 365 client updates** section of the topic.  

2.  [Configure software update points](../get-started/configure-classifications-and-products.md) to synchronize the Office 365 client updates. Set **Updates** for the classification and select **Office 365 Client** for the product. You might have to synchronize software updates at least one time before the Office 365 Client product is available for you to choose. You must synchronize software updates after you configure the software update points to use the **Updates** classification.
3.  Enable Office 365 clients to receive updates from Configuration Manager. You can do this by using Configuration Manager client settings or use group policy. Use one of the following methods to enable the client:  
    - Method 1: Beginning in Configuration Manager version 1606, you can use the Configuration Manager client setting to manage the Office 365 client agent. After you configure this setting and deploy Office 365 updates, the Configuration Manager client agent communicates with the Office 365 client agent to download Office 365 updates from a distribution point and install them. Configuration Manager takes inventory of Office 365 ProPlus Client settings.
      1.  In the Configuration Manager console, click **Administration** > **Overview** > **Client Settings**.  

      2.  Open the appropriate device settings to enable the client agent. For more information about default and custom client settings, see [How to configure client settings in System Center Configuration Manager](../../core/clients/deploy/configure-client-settings.md).  

      3.  Click **Software Updates** and select **Yes** for the **Enable management of the Office 365 Client Agent** setting.  

    - Method 2: [Enable Office 365 clients to receive updates](https://technet.microsoft.com/library/mt628083.aspx#BKMK_EnableClient) from Configuration Manager by using the Office Deployment Tool or Group Policy.  

4. [Deploy the Office 365 updates](deploy-software-updates.md) to clients.   

## Add other languages for Office 365 update downloads
Beginning in Configuration Manager version 1610, you can add support for Configuration Manager to download updates for any languages supported by Office 365 regardless of whether they are supported in Configuration Manager.
> [!IMPORTANT]  
> Configuring additional Office 365 update languages is a site-wide setting. After you add the languages by using the following procedure, all Office 365 updates will be downloaded in those languages as well as the languages that you select on the Language Selection page in the Download Software Updates or Deploy Software Updates wizards.

### To add support to download updates for additional languages
Use the following procedure on the central administration site, or stand-alone primary site, where the software update point site system role is installed.
1. From a command prompt, type *wbemtest* as an administrative user to open the Windows Management Instrumentation Tester.
2. Click **Connect**, and then type *root\sms\site_&lt;siteCode&gt;*.
3. Click **Query**, and then run the following query:
   *select &#42; from SMS_SCI_Component where componentname ="SMS_WSUS_CONFIGURATION_MANAGER"*  
![WMI query](..\media\1-wmiquery.png)
4. In the results pane, double-click the object with the site code for the central administration site or stand-alone primary site.
5. Select the **Props** property, click **Edit Property**, and then click **View Embedded**.
![Property editor](..\media\2-propeditor.png)
6. Starting at the first query result, open each object until you find the one with **AdditionalUpdateLanguagesForO365** for the **PropertyName** property.
7. Select **Value2** and click **Edit Property**.  
![Edit the Value2 property](..\media\3-queryresult.png)
8. Add additional languages to the **Value2** property and click **Save Property**.  
For example, pt-pt (for Portuguese - Portugal), af-za (for Afrikaans - South Africa), nn-no (for Norwegian (Nynorsk) - Norway), etc.  
![Add languages in Property Editor](..\media\4-props.png)  
9. Click **Close**, click **Close**, click **Save Property**, click **Save Object** (if you click **Close** here the values are discarded), click **Close**, and then click **Exit** to exit the Windows Management Intstrumentation Tester.
10. In the Configuration Manager console, go to **Software Library** > **Overview** > **Office 365 Client Management** > **Office 365 Updates**.
11. Now, when you download Office 365 updates, the updates will be downloaded in the language that you select in the wizard and the languages that you configured in this procedure. To verify that the updates downloaded in those languages, go to the package source for the update and look for files with the language code in the filename.  
![Filenames with additional languages](..\media\5-verification.png)


## Change the update channel after you enable Office 365 clients to receive updates from Configuration Manager
To change the update channel after you enable Office 365 clients to receive updates from Configuration Manager, you can use group policy to distribute a registry key value change to Office 365 clients . Change the **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Office\ClickToRun\Configuration\CDNBaseUrl** registry key to use one of the following values:

- Current Channel:  
  **CDNBaseUrl** = http&#58;//officecdn.microsoft.com/pr/492350f6-3a01-4f97-b9c0-c7c6ddf67d60

- Deferred Channel:  
  **CDNBaseUrl** = http&#58;//officecdn.microsoft.com/pr/7ffbc6bf-bc32-4f92-8982-f9dd17fd3114

- First Release for Current Channel:  
  **CDNBaseUrl** = http&#58;//officecdn.microsoft.com/pr/64256afe-f5d9-4f86-8936-8840a6a4f5be

- First Release for Deferred Channel:  
  **CDNBaseUrl** = http&#58;//officecdn.microsoft.com/pr/b8f9b850-328d-4355-9145-c59439a0c4cf

<!--- ## Next steps
Use the Office 365 Client Management dashboard in Configuration Manager to review Office 365 client information and deploy Office 365 apps. For details, see [Manage Office 365 apps](manage-office-365-apps.md). --->
