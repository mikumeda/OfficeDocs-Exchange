---
ms.localizationpriority: high
description: Exchange Emergency Mitigation Service (Exchange EM Service)
ms.topic: overview
author: JoanneHendrickson
ms.author: jhendr
ms.reviewer:
title: Exchange Emergency Mitigation Service (Exchange EM Service)
ms.collection:
- Strat_EX_Admin
- exchange-server
f1.keywords:
- NOCSH
audience: ITPro
ms.prod: exchange-server-it-pro
manager: serdars
---

# Exchange Emergency Mitigation (EM) service

The Exchange Emergency Mitigation service (EM service) helps to keep your Exchange Servers secure by applying mitigations to address any potential threats against your servers. It uses the cloud-based Office Config Service (OCS) to check for and download available mitigations and to send diagnostic data to Microsoft.

The EM service runs as a Windows service on an Exchange Mailbox server. When you install the September 2021 CU (or later) on Exchange Server 2016 or Exchange Server 2019, the EM service will be installed automatically on servers with the Mailbox role. The EM service will not be installed on Edge Transport servers.

The use of the EM service is optional. If you do not want Microsoft to automatically apply mitigations to your Exchange servers, you can disable the feature.

## Mitigations

A _mitigation_ is an action or set of actions that are taken automatically to secure an Exchange server from a known threat that is being actively exploited in the wild. To help protect your organization and mitigate risk, the EM service might automatically disable features or functionality on an Exchange server.

The EM service can apply the following types of mitigations:

- **IIS URL Rewrite rule mitigation**: This mitigation is a rule that blocks specific patterns of malicious HTTP requests that can endanger an Exchange server.
- **Exchange service mitigation**: This mitigation disables a vulnerable service on an Exchange server.
- **App Pool mitigation**: This mitigation disables a vulnerable app pool on an Exchange server.

You have visibility and control over any applied mitigation by using Exchange PowerShell cmdlets and scripts.

### How does it work

If Microsoft learns about a security threat, we might create and release a mitigation for the issue. If this happens, the mitigation is sent from the OCS to the EM service as a signed XML file containing the configuration settings that are required to apply the mitigation.

After the EM service has been installed, it checks the OCS for available mitigations every hour. The EM service subsequently downloads the XML file and validates the signature to verify that the XML was not tampered with. The EM service checks the issuer, the Extended Key Usage, and the certificate chain. After successful validation, the EM service applies the mitigation.

Each mitigation is a temporary, interim fix until you can apply the Security Update that fixes the vulnerability. The EM service is not a replacement for Exchange SUs. However, it's the fastest and easiest way to mitigate the highest risks to internet-connected, on-premises Exchange servers before updating.

### List of mitigations released

The following table describes the repository of all released mitigations.

<br>

****

|Serial number|Mitigation ID|Description|Lowest version applicable|Highest version applicable|Rollback procedure|
|---|---|---|---|---|---|
|1|PING1|EEMS heartbeat probe. Does not modify any Exchange settings.|Exchange 2019: September 2021 CU <p> Exchange 2016: September 2021 CU| - |No rollback required.|
|

## Prerequisites

If these prerequisites are not already on the Windows Server where Exchange is installed or to be installed, Setup will prompt you to install these prerequisites during the readiness check:

- [IIS URL Rewrite Module](https://www.iis.net/downloads/microsoft/url-rewrite)
- [Universal C Runtime in Windows (KB2999226)](https://support.microsoft.com/topic/update-for-universal-c-runtime-in-windows-c0514201-7fe6-95a3-b0a5-287930f3560c) for Windows Server 2012 and Windows Server 2012 R2

## Connectivity

The EM service needs outbound connectivity to the OCS to check for and download mitigations. If outbound connectivity to the OCS is not available during the installation of Exchange Server, Setup issues a Warning during the readiness check.

While the EM service can be installed without connectivity to the OCS, it must have connectivity to the OCS in order to download and apply the latest mitigations. The OCS must be reachable from the computer on which Exchange Server is installed for the EM service to function correctly.

<br>

****

|Endpoint|Address|Port|Description|
|---|---|---|---|
|Office Config Service|`officeclient.microsoft.com/*`| 443|Required endpoint for the Exchange EM service|
|

If a network proxy is deployed for outbound connectivity, you need to configure the _InternetWebProxy_ parameter on the Exchange server by running the following command:

```Powershell
Set-ExchangeServer -Identity <ServerName> -InternetWebProxy <proxy.contoso.com:port>
```

## Test-MitigationServiceConnectivity script

You can verify that an Exchange server has connectivity to the OCS by using the **Test-MitigationServiceConnectivity.ps1** script in the `V15\Scripts` folder in the Exchange server directory.

If the server has connectivity, the output is:

```powershell
Result: Success.
Message: The Mitigation Service endpoint is accessible from this computer.
```

If the server doesn't have connectivity, the output is:

```Powershell
Result: Failed.
Message: Unable to connect to the Mitigation Service endpoint from this computer. To learn about connectivity requirements, see https://aka.ms/HelpConnectivityEEMS.
```

## Disabling auto apply of Mitigations through EM Service

One of the EM service functions is downloading mitigations from the OCS and automatically applying them to the Exchange Server. If your organization has an alternate means of mitigating a known threat, you might choose to disable automatic applications of mitigations. You can enable or disable automatic mitigation at an organizational level or at the Exchange server level.

To disable automatic mitigation for your entire organization, run the following command:

```powershell
Set-OrganizationConfig -MitigationsEnabled $false
```

By default, _MitigationsEnabled_ is set to `$true`. When set to `$false`, the EM service still checks for mitigations hourly but won't automatically apply mitigations to any Exchange server in the organization, regardless of the value of _MitigationsEnabled_ parameter at the server level.

To disable automatic mitigation on a specific server, replace \<ServerName\> with the name of the server, and then run the following command:

```Powershell
Set-ExchangeServer -Identity <ServerName> -MitigationsEnabled $false
```

By default, _MitigationsEnabled_ is set to `$true`. When set to `$false`, the EM service checks for mitigations hourly but won't automatically apply them to the specified server.

The combination of the organization setting and the server settings determine the behavior of the EM service on each Exchange server. This behavior is described in the following table:

<br>

****

|Organization setting|Server setting|Result|
|---|---|---|
|True|True|EM service will automatically apply mitigations to the Exchange server.|
|True|False|EM service will not automatically apply mitigations to a specific Exchange server.|
|False|False|EM service will not automatically apply mitigations to any Exchange server.|
|

> [!NOTE]
> The _MitigationsEnabled_ parameter automatically applies to all servers in an organization. This parameter is set to the value `$true` as soon as the first Exchange server in your organization is upgraded to the September 2021 CU (or later). This behavior is by design. After the other Exchange servers in the organization are upgraded with the September 2021 CU (or later), only then will the EM service honor the value of _MitigationsEnabled_ parameter.

### Viewing Applied Mitigations

Once mitigations are applied to a server, you can view the applied mitigations by replacing \<ServerName\> with the name of the server, and then running the following command:

```powershell
Get-ExchangeServer -Identity <ServerName> | Format-List Name,MitigationsApplied
```

Example output:

```Powershell
Name            :   Server1
MitigationsApplied  :   {M01.1, M01.2, M01.3}
```

To see the list of applied mitigations for all Exchange servers in your environment, run the following command:

```powershell
Get-ExchangeServer | Format-List Name,MitigationsApplied
```

Example output:

```powershell
Name            :   Server1
MitigationsApplied  :   {M01.1, M01.2, M01.3}

Name            :   Server2
MitigationsApplied  :   {M01.1, M01.2, M01.3}
```

## Reapplying a Mitigation

If you accidentally reverse a mitigation, the EM service will reapply it when it performs its hourly check for new mitigations. To manually reapply any mitigation, restart the EM service on the Exchange server by running the following command:

```PowerShell
Restart-Service MSExchangeMitigation
```

Ten minutes after restarting, the EM service will run its check and apply any mitigations.

### Blocking or Removing Mitigations

If a mitigation critically affects the functionality of your Exchange server, you can block the mitigation and manually reverse it.

To block any mitigation, add the Mitigation ID in the _MitigationsBlocked_ parameter:

```powershell
Set-ExchangeServer -Identity <ServerName> -MitigationsBlocked @("M1")
```

The previous command blocks the M1 mitigation, which ensures that EM service will not reapply this mitigation in the next hourly cycle.

To block more than one mitigation, use the following syntax:

```powershell
Set-ExchangeServer -Identity <ServerName> -MitigationsBlocked @("M1","M2")
```

Blocking a mitigation does not automatically remove it, but after blocking a mitigation, you can manually remove it. How a mitigation is removed depends on the type of mitigation. For example, to remove an IIS rewrite rule mitigation, delete the rule in IIS Manager. To remove a service or app pool mitigation, start the service or app pool manually.

You can also remove one or more mitigations from the blocked mitigations list by removing the Mitigation ID in the _MitigationsBlocked_ parameter in the same command.

For example:

```powershell
Set-ExchangeServer -Identity <ServerName> -MitigationsBlocked @()
```

After a mitigation is removed from the blocked mitigations list, the mitigation will be reapplied by the EM service on its next run. To manually reapply the mitigation, stop and restart the EM service by running the following command:

```PowerShell
Restart-Service MSExchangeMitigation
```

Ten minutes after restarting, the EM service will run its check and apply any mitigations.

> [!IMPORTANT]
> Refrain from making any changes to the _MitigationsApplied_ parameter, as it is used by the EM service to store and track mitigation status.

## Viewing Applied and Blocked Mitigations

You can view both applied and blocked mitigations for all Exchange servers in your organization by using the **Get-ExchangeServer** cmdlet.

To view the list of applied and blocked mitigations for all Exchange servers, run the following command:

```powershell
Get-ExchangeServer | Format-List Name,MitigationsApplied,MitigationsBlocked
```

Example output:

```powershell
Name            :   Server1
MitigationsApplied  :   {M01.1, M01.3}
MitigationsBlocked  :   {M01.2}

Name            :   Server2
MitigationsApplied  :   {M01.1, M01.2}
MitigationsBlocked  :   {M01.3}
```

To view the list of applied and blocked mitigations on a per-server basis, replace \<ServerName\> with the name of the server, and then run the following command:

```powershell
Get-ExchangeServer -Identity <ServerName> | fl name, *Mitigations*
```

Example output:

```powershell
Name            :   Server1
MitigationsEnabled  :   True
MitigationsApplied  :   {M01.1, M01.3}
MitigationsBlocked  :   {M01.2}
```

## Get-Mitigation Script

You can use the **Get-Mitigations.ps1** script to analyze and track the mitigations provided by Microsoft. This script is available in the `V15\Scripts` folder in the Exchange Server directory.

The script displays the ID, type, description, and status of each mitigation. The list includes any applied, blocked, or failed mitigations.

To view the details of a specific server, provide the server name in the _Identity_ parameter. For example, `.\Get-Mitigations.ps1 -Identity <ServerName>`.  To view the status of all the servers in your organization, simply omit the _Identity_ parameter.

**Example:** Export the list of applied mitigations and their descriptions to a CSV file by using the ExportCSV parameter:

```powershell
.\Get-Mitigations.ps1 -Identity <ServerName> -ExportCSV "C:\temp\CSVReport.csv"
```

> [!IMPORTANT]
> The Get-Mitigations script needs PowerShell version 4.0.

## Removing Mitigations after SU or CU upgrade

After an SU or a CU has been installed, an admin must manually remove any mitigations that are no longer needed. For example, if a Mitigation named **M1** is no longer relevant after installing an SU, the EM service will stop applying it, and it will be removed from the list of applied mitigations. Depending on the type of mitigation, it can be removed from the server if required.

## Audit and Logging

Any mitigations blocked by an admin will be logged in the Windows Application Event Log. In addition to logging blocked mitigations, the EM service also logs details about service startup, shutdown, and termination (like all services running on Windows) and details of its actions and any errors encountered by the EM service. For example, Events 1005 and 1006 with a source of "MSExchange Mitigation Service" will be logged for successful actions such as when a mitigation is applied. Event 1008 with the same source, will be logged for any encountered errors, such as when the EM service cannot reach the OCS.

You can use **Search-AdminAuditLog** to review actions taken by yourself or other admins, including enabling and disabling automatic mitigations.

The EM service maintains a separate log file in the `\V15\Logging\MitigationService` folder in the Exchange Server installation directory. This log details the tasks performed by the EM service, including fetched, parsed, and applied mitigations and details about the information sent to the OCS (if sending diagnostic data is enabled).

## Diagnostic Data

When data sharing is enabled, the EM service sends diagnostic data to the OCS. This data is used to identify and mitigate threats. To learn more about what is collected and how to disable data sharing, see [Diagnostic Data collected for Exchange Server](diagnostic-data-exchange-server.md).
