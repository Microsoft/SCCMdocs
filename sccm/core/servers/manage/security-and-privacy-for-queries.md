---
title: "Security and privacy for queries"
titleSuffix: "Configuration Manager"
description: "Understand best practices for security and privacy when you query for information from the site database."
ms.date: 05/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 30080620-20d3-4c38-b8dd-db5516e1acae
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
---
# Security and privacy for queries in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Queries in System Center Configuration Manager let you retrieve information from the site database based on the criteria that you specify. Configuration Manager collects the site database information during standard operation. For example, by using information that has been collected from discovery or inventory, you can configure a query to identify devices that meet specified criteria.  

 For more information about queries, see [Introduction to queries in System Center Configuration Manager](../../../core/servers/manage/introduction-to-queries.md). For more information about security best practices and privacy information for Configuration Manager operations that collect the information that you can retrieve by using queries, see [Security and privacy for System Center Configuration Manager](../../../core/plan-design/security/security-and-privacy.md).  

## Security best practices for queries

 Use the following security best practice for queries.  

|Security best practice|More information|  
|----------------------------|----------------------|  
|When you export or import a query that is saved to a network location, secure the location and the network channel.|Restrict who can access the network folder.<br /><br /> Use server message block (SMB) signing or Internet Protocol Security (IPsec) between the network location and the site server to prevent an attacker from tampering with the query data before it is imported.|  

## Next steps
  
[Security and privacy for System Center Configuration Manager](../../../core/plan-design/security/security-and-privacy.md)
