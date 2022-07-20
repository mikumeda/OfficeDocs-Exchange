---
title: 'Access control list (ACL) inheritance is blocked'
TOCTitle: Access control list (ACL) inheritance is blocked_InhBlockPublicFolderTree
ms:assetid: e3b89c8a-d6f8-4864-8bf0-35a78ce87cc4
ms:mtpsurl: https://technet.microsoft.com/library/ms.exch.setupreadiness.inhblockpublicfoldertree(v=EXCHG.150)
ms:contentKeyID: 46629148
ms.topic: article
ms.reviewer: 
manager: serdars
ms.author: serdars
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
description: Learn about the Access control list (ACL) inheritance is blocked\_InhBlockPublicFolderTree error.
---

# Access control list (ACL) inheritance is blocked\_InhBlockPublicFolderTree

_**Applies to:** Exchange Server 2013_

The content in this topic hasn't been updated for Microsoft Exchange Server 2013. While it hasn't been updated yet, it may still be applicable to Exchange 2013. If you still need help, check out the community resources below.

Having problems? Ask for help in the Exchange forums. Visit the forums at [Exchange Server](https://social.technet.microsoft.com/forums/office/home?category=exchangeserver).

Microsoft Exchange Server 2007 or Exchange Server 2010 setup cannot continue because the required permissions have not been able to propagate.

Exchange setup requires that inheritance for permissions be enabled on the following Exchange objects:

- Exchange Organization object

- Exchange Administrative Group object

- Exchange Servers container object

- Exchange Address List object

- Exchange Public Folder object

- Exchange Public Folder tree object

Failure to enable inheritance for permissions on these objects may result in mail flow problems, store mounting issues, and other service outages.

To resolve this issue, make sure that the "Allow permissions to propagate to this object and child objects" setting is enabled for the object, and then rerun Exchange Server 2007 or Exchange 2010 setup.

|To re-enable permissions inheritance for an Exchange configuration object using Exchange Server 2003 Exchange System Manager|
|---|
|<ol><li>Enable the **Security** tab for the object properties box of Exchange System Manager by setting a registry parameter. <ol><li>Start Registry Editor (Regedt32.exe).</li><li>Locate the following key in the registry: <br/> **HKEY_CURRENT_USER\Software\Microsoft\Exchange\EXAdmin**</li><li>On the **Edit** menu, click **New**, and then add the following registry value: <br/> **Value Name**: ShowSecurityPage <br/> **Data Type**: REG_DWORD <br/> **Radix**: Binary <br/> **Value**: 1</li><li>Quit Registry Editor.</li></ol> <p> **Note**: By default, the **Security** tab is not enabled in the configuration object properties box.</li><li>Open Exchange System Manager, find the object in question, right-click the object and select **Properties**.</li><li>Select the **Security** tab and then click **Advanced**.</li><li>Select **Allow inheritable permissions from the parent to propagate to this object and all child objects** to re-enable permissions inheritance.</li><li>Restart Exchange Server.</li></ol>|

> [!WARNING]
> If you incorrectly modify the attributes of Active Directory objects when you use ADSI Edit, the LDP tool, or another LDAP version 3 client, you may cause serious problems. These problems may require that you reinstall Microsoft Windows Server™ 2003, Exchange Server, or both. Modify Active Directory object attributes at your own risk.

|To re-enable permissions inheritance for an Exchange configuration object using ADSIEdit from Exchange Server 2007 or Exchange Server 2010|
|---|
|<ol><li>Install ADSI Edit.</li><li>Launch ADSI Edit. Click **Start**, click **Run**, type **adsiedit.msc** in the text box, and then click OK.</li><li>Navigate to the object in question, right-click the object and select **Properties**.</li><li>Select the **Security** tab and then click **Advanced**.</li><li>Select **Allow inheritable permissions from the parent to propagate to this object and all child objects** to re-enable permissions inheritance.</li><li>Select **Ok** twice to apply the change.</li><li>Wait for Active Directory replication to propagate the changes or force Active Directory replication.</li></ol>|
