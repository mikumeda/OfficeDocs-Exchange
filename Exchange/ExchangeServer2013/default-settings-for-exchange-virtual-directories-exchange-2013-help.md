---
title: 'Default settings for Exchange virtual directories: Exchange 2013 Help'
TOCTitle: Default settings for Exchange virtual directories
ms:assetid: d2d89ce6-4721-4737-a325-fba5ad9422e0
ms:mtpsurl: https://technet.microsoft.com/library/Gg247612(v=EXCHG.150)
ms:contentKeyID: 50934224
ms.reviewer: 
manager: serdars
ms.author: serdars
ms.topic: article
description: Default settings for Exchange virtual directories
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# Default settings for Exchange virtual directories

_**Applies to:** Exchange Server 2013_

Exchange Server 2013 automatically configures multiple Internet Information Services (IIS) virtual directories during installation. This topic contains information about the default IIS authentication settings and default Secure Sockets Layer (SSL) settings for the Client Access and Mailbox servers.

## Client Access server

The following table lists the default settings on a stand-alone Exchange 2013 Client Access server.

|Virtual directory|Authentication method|SSL settings|Management method|
|---|---|---|---|
|Default website|<ul><li>Anonymous</li></ul>|<ul><li>Required</li></ul>|IIS management console|
|aspnet_client|<ul><li>Anonymous authentication</li></ul>|<ul><li>SSL required</li><li>Requires 128-bit encryption</li></ul>|IIS management console|
|Autodiscover|<ul><li>Anonymous authentication</li><li>Basic authentication</li><li>Windows authentication</li></ul>|<ul><li>SSL required</li><li>Requires 128-bit encryption</li></ul>|Exchange Management Shell (Shell)|
|ecp|<ul><li>Anonymous authentication</li><li>Basic authentication</li></ul>|<ul><li>SSL required</li><li>Requires 128-bit encryption</li></ul>|Exchange admin center (EAC) or Shell|
|EWS|<ul><li>Anonymous authentication</li><li>Windows authentication</li></ul>|<ul><li>SSL required</li><li>Requires 128-bit encryption</li></ul>|Shell|
|Microsoft-Server-ActiveSync|<ul><li>Basic authentication</li></ul>|<ul><li>SSL required</li><li>Requires 128-bit encryption</li></ul>|EAC or Shell|
|OAB|<ul><li>Windows authentication</li></ul>|<ul><li>Not required</li></ul>|EAC or Shell|
|owa|<ul><li>Basic authentication</li></ul>|<ul><li>SSL required</li><li>Requires 128-bit encryption</li></ul>|EAC or Shell|
|PowerShell|<ul><li>Anonymous authentication</li></ul>|<ul><li>Not required</li></ul>|Shell|
|Rpc|<ul><li>Basic authentication</li><li>Windows authentication</li></ul>|<ul><li>SSL required</li><li>Requires 128-bit encryption</li></ul>|Shell|
|RpcWithCert|By default, all authentication methods are disabled.|<ul><li>Required</li></ul>||

## Mailbox server

The following table lists the default settings on a stand-alone Exchange 2013 Mailbox server.

### Default Mailbox server IIS authentication and SSL settings

|Virtual directory|Authentication method|SSL settings|Management method|
|---|---|---|---|
|Default website|<ul><li>Anonymous authentication</li></ul>|<ul><li>SSL required</li><li>Requires 128-bit encryption</li></ul>|This virtual directory can't be configured by the user.|
|PowerShell|<ul><li>Anonymous authentication</li></ul>|<ul><li>Not required</li></ul>|Shell|
