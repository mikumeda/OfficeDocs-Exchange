---
title: 'Modify AD LDS configuration: Exchange 2013 Help'
TOCTitle: Modify AD LDS configuration
ms:assetid: 381f582c-15ec-43bc-b674-5399fad72c97
ms:mtpsurl: https://technet.microsoft.com/library/Aa997269(v=EXCHG.150)
ms:contentKeyID: 61200283
ms.reviewer: 
ms.topic: article
description: Modify Active Directory Lightweight Directory Services configuration in Exchange
manager: serdars
ms.author: serdars
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# Modify AD LDS configuration

_**Applies to:** Exchange Server 2013_

You can use the **ConfigureAdam.ps1** script (located in $env:ExchangeInstallPath\\Scripts) to modify the default Active Directory Lightweight Directory Services (AD LDS) configuration on Edge Transport servers before you subscribe the Edge Transport server to your Exchange organization.

> [!IMPORTANT]
> The **ConfigureAdam.ps1** script invokes the **dsdbutil** command to change the registry settings for AD LDS. The **dsdbutil** command is an AD LDS management tool intended for use only by experienced administrators; using **ConfigureAdam.ps1** is the recommended way of changing the AD LDS configuration.

The parameters in the following table are available for the **ConfigureAdam.ps1** script. You can use one, all, or any combination of these parameters to modify AD LDS.

|Parameter|Description|
|---|---|
|_Ldapport_|Modifies the port used for LDAP communication. By default, the Edge Transport server uses the nonstandard port 50389.|
|_Sslport_|Modifies the port used for secure LDAP communication. By default, the Edge Transport server uses the nonstandard port 50636.|
|_LogPath_|Modifies the log file location. By default, the Edge Transport server creates log files in the path %ExchangeInstallPath%Transport Roles\Data\adam|
|_DataPath_|Modifies the location of the directory database file. By default, the Edge Transport server stores the directory database in the path %ExchangeInstallPath%Transport Roles\Data\adam|

## What do you need to know before you begin?

- Estimated time to complete: five minutes.

- You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Edge Transport servers" section in [Mail flow permissions](mail-flow-permissions-exchange-2013-help.md).

- If you need to make any modifications to the Edge Transport server's AD LDS configuration, do so before subscribing the Edge Transport server to your Exchange organization. If you modify the AD LDS configuration of a subscribed Edge Transport server, you will then need to resubscribe the Edge Transport server to the Exchange organization.

- Always use the script to modify the registry settings. Making manual registry changes to the AD LDS configuration might make the AD LDS instance unavailable.

- If you need to modify the LDAP port or the SSL port used by AD LDS, first verify that the selected port isn't being used by another application. You can use the **netstat** command to view the ports being used on the Edge Transport server.

- You can only use the Shell to perform this procedure.

> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at [Exchange Server](https://social.technet.microsoft.com/forums/office/home?category=exchangeserver).

## Modify the AD LDS configuration on an Edge Transport server

This example changes the LDAP port used by AD LDS to 5000. The ampersand (&) is part of the command syntax.

```powershell
& $env:ExchangeInstallPath\Scripts\ConfigureAdam.ps1 -LdapPort:5000
```

This example makes the following changes to the AD LDS configuration. The ampersand (&) is part of the command syntax. Note the colon (:) used between each parameter and its value:

- Changes the LDAP port to 5000
- Changes the SSL port to 500
- Changes the log path to D:\\Exchange Server\\Data\\ADLDS
- Changes the data path to D:\\Exchange Server\\Data\\ADLDS

```powershell
& $env:ExchangeInstallPath\Scripts\ConfigureAdam.ps1 -LdapPort:5000 -SslPort:5001 -LogPath:"D:\Exchange Server\Data\ADLDS" -DataPath:"D:\Exchange Server\Data\ADLDS"
```
