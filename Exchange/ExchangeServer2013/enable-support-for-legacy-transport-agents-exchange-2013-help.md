---
title: 'Enable support for legacy transport agents: Exchange 2013 Help'
TOCTitle: Enable support for legacy transport agents
ms:assetid: 00617e87-7199-406e-b4a3-94378f657f1f
ms:mtpsurl: https://technet.microsoft.com/library/JJ591524(v=EXCHG.150)
ms:contentKeyID: 49084757
ms.reviewer: 
manager: serdars
ms.author: serdars
author: msdmaguire
ms.topic: article
description: How to enable support for legacy transport agents in Exchange Server 
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# Enable support for legacy transport agents

_**Applies to:** Exchange Server 2013_

In Microsoft Exchange Server 2013, transport agents that were created using the Microsoft .NET Framework version 4.0 are supported by default. Exchange 2013 supports transport agents that were created using previous versions of the .NET Framework, but support for these legacy transport agents isn't enabled by default. To enable support for legacy transport agents, you need to modify the appropriate XML application configuration file. The files you need to modify depend on where the transport agent is installed:

|Server|Application configuration files|Microsoft Windows service|
|---|---|---|
|Client Access server|%ExchangeInstallPath%Bin\MSExchangeFrontendTransport.exe.config|Microsoft Exchange Front End Transport (MSExchangeFrontendTransport)|
|Mailbox server|<ul><li>%ExchangeInstallPath%Bin\EdgeTransport.exe.config</li><li>%ExchangeInstallPath%Bin\MSExchangeTransport.exe.config</li></ul>|Microsoft Exchange Transport (MSExchangeTransport)|

Support for legacy transport agents is controlled by keys in the application configuration files. By default, none of the required keys are present in the application configuration files. You must add the keys manually. The following table explains each key in more detail.

|Key|Description|
|---|---|
|_useLegacyV2RuntimeActivationPolicy_|This key enables or disables support for legacy transport agents. Valid values for this key are `true` or `false`. If this key isn't specified, the default value is `false`.|
|_supportedRuntime version_|This key specifies the version of the Microsoft .NET Framework that's required by the agent. Valid values for this key are: <ul><li>`v4.0` or `v4.0.30319`</li><li>`v3.5` or `v3.5.21022`</li><li>`v3.0` or `v3.0.4506`</li><li>`v2.0` or `v2.0.50727`</li></ul><p>You specify multiple values using multiple separate instances of the _supportedRuntime version_ key. <br/><br/> When you enable legacy transport agent support using the _useLegacyV2RuntimeActivationPolicy_ key, you should always specify the value `v4.0` in addition to the values required by the legacy transport agent.|

## What do you need to know before you begin?

- Estimated time to complete: 15 minutes

- Exchange permissions don't apply to the procedures in this topic. These procedures are performed in the operating system of the Exchange Server.

- Changes you save to an application configuration file are applied after you restart the corresponding service.

- When you restart any of the services that are associated with the application configuration files, mail flow on the server is temporarily interrupted.

- Any customized per-server settings you make in Exchange XML application configuration files, for example, web.config files on Client Access servers or the EdgeTransport.exe.config file on Mailbox servers, will be overwritten when you install an Exchange Cumulative Update (CU). Make sure that you save this information so you can easily re-configure your server after the install. You must re-configure these settings after you install an Exchange CU.

- For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-2013-help.md).

> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at [Exchange Server](https://social.technet.microsoft.com/forums/office/home?category=exchangeserver).

## Use the Command Prompt to configure support for legacy transport agents

Use the following procedure to enable support for legacy transport agents:

1. In a Command prompt window, on the Exchange 2013 server where you want to configure the legacy transport agent support, open the appropriate application configuration file in Notepad by running the following command:

    ```powershell
    Notepad %ExchangeInstallPath%Bin\<AppConfigFile>
    ```

    For example, to open the EdgeTransport.exe.config file on a Mailbox server, run the following command:

    ```powershell
    Notepad %ExchangeInstallPath%Bin\EdgeTransport.exe.config
    ```

2. Locate the _\</configuration\>_ key at the end of the file, and paste the following keys before the _\</configuration\>_ key:

    ```powershell
    <startup useLegacyV2RuntimeActivationPolicy="true">
       <supportedRuntime version="v4.0" />
       <supportedRuntime version="v3.5" />
       <supportedRuntime version="v3.0" />
       <supportedRuntime version="v2.0" />
    </startup>
    ```

3. When you are finished, save and close the application configuration file.

4. Repeat Steps 1 through 3 to modify the other application configuration files.

5. Restart the associated Windows service by running the following command:

    ```powershell
    net stop <service> && net start <service>
    ```

    For example, if you modified the EdgeTransport.exe.config file, you need to restart the Microsoft Exchange Transport service by running the following command:

    ```powershell
    net stop MSExchangeTransport && net start MSExchangeTransport
    ```

6. Repeat Step 5 to restart services associated with the other modified application configuration files.

## How do you know this worked?

You'll know this procedure works if the legacy transport agent installs successfully. If you try to install a legacy transport agent without performing the procedures in this topic, you'll receive an error that's similar to the following:

`Mixed mode assembly is built against version '<version>' of the runtime and cannot be loaded in the 4.0 runtime without additional configuration information.`
