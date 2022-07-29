---
title: Troubleshooting DataProtection Health Set
TOCTitle: Troubleshooting DataProtection Health Set
ms:assetid: cde3cc34-2076-4e30-8d3c-265b66d00ae8
ms:mtpsurl: https://technet.microsoft.com/library/ms.exch.scom.dataprotection(v=EXCHG.150)
ms:contentKeyID: 49720873
ms.reviewer:
manager: serdars
ms.author: serdars
ms.topic: article
description: How to troubleshoot the DataProtection Health Set in Exchange 2013
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# Troubleshooting DataProtection Health Set

_**Applies to:** Exchange Server 2013_

The DataProtection Health set monitors the redundancy of databases in a database availability group (DAG).

If you receive an alert that specifies that DataProtection is unhealthy, this indicates an issue that may affect the replication or cluster components, and that can prevent access to the Exchange databases.

## Explanation

The DataProtection Health service is monitored by using the following probes and monitors.

|Probe|Health Set|Dependencies|Associated Monitors|
|---|---|---|---|
|ClusterEndpointProbe|DataProtection|Active Directory|ClusterEndpointMonitor|
|ClusterGroupProbe|DataProtection|Active Directory|ClusterGroupMonitor|
|ClusterNetworkProbe|DataProtection|Active Directory|ClusterNetworkMonitor|
|ClusterServiceCrashProbe|DataProtection|Active Directory|ClusterServiceCrashMonitor|
|ServerOneCopyProbe|DataProtection|Active Director|ServerOneCopyMonitor|
|ServerOneCopyInternalMonitorProbe|DataProtection|Active Directory|ServerOneCopyInternalMonitorMonitor|
|ServiceHealthMSExchangeReplEndpointProbe|DataProtection|Active Directory|ServiceHealthMSExchangeReplEndpointMonitor|
|ServiceHealthMSExchangeReplCrashProbe |DataProtection|Active Directory|ServiceHealthMSExchangeReplCrashMonitor|
|ServerSiteFailureProbe|DataProtection|Active Directory|ServerSiteFailureMonitor|
|StorageApparentControllerIssuesProbe|DataProtection|Active Directory|StorageApparentControllerIssuesMonitor|
|DatabaseHealthTooManyMountedDatabaseProbe|DataProtection|Active Directory|DatabaseHealthTooManyMountedDatabaseMonitor|

For more information about probes and monitors, see [Server health and performance](../../server-health-and-performance-exchange-2013-help.md).

## User Action

It's possible that the service recovered after it issued the alert. Therefore, when you receive an alert that specifies that the health set is unhealthy, first verify that the issue still exists. If the issue does exist, perform the appropriate recovery actions outlined in the following sections.

## Verifying the issue still exists

1. Identify the health set name and the server name in the alert.

2. The message details provide information about the exact cause of the alert. In most cases, the message details provide sufficient troubleshooting information to identify the root cause. If the message details are not clear, do the following:

   1. Open the Exchange Management Shell, and then run the following command to retrieve the details of the health set that issued the alert:

      ```powershell
      Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
      ```

      For example, to retrieve the Autodiscover.Protocol health set details about server1.contoso.com, run the following command:

      ```powershell
      Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "Autodiscover.Protocol"}
      ```

      Review the command output to determine which monitor reported the error. The **AlertValue** value for the monitor that issued the alert will be `Unhealthy`.

   2. Identify the probe that the monitor is based on. Note that most probes share the same name prefix. By using the previous example, search for "**ClusterNetwork\***":

      ```powershell
      Get-MonitoringItemIdentity -Identity DataProtection -Server server1.contoso.com | ?{$_.Name -like "ClusterNet ItemType work*"}
      ```

      The returned results should resemble the following.

      |ItemType|HealthSetName|Name|TargetResource|
      |---|---|---|---|
      |`Probe`|`DataProtection`|`ClusterNetworkProbe`|`MSExchangeRepl`|

   3. Rerun the associated probe for the monitor that's in an unhealthy state. Refer to the table in the Explanation section to find the associated probe. To do this, run the following command:

      ```powershell
      Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
      ```

      For example, assume that the failing monitor is **AutodiscoverSelfTestMonitor**. The probe associated with that monitor is **AutodiscoverSelfTestProbe**. To run that probe on server1.contoso.com, run the following command:

      ```powershell
      Invoke-MonitoringProbe Autodiscover.Protocol\AutodiscoverSelfTestProbe -Server server1.contoso.com | Format-List
      ```

   4. In the command output, review the **Result** value of the probe. If the value is **Succeeded**, the issue was a transient error, and it no longer exists. Otherwise, refer to the recovery steps outlined in the following sections.

## Troubleshooting steps

When you receive an alert from a health set, the email message contains the following information:

- Name of the server that sent the alert
- Time and date when the alert occurred
- Authentication mechanism that was used, and credential information
- Full exception trace of the last error, including diagnostic data and specific HTTP header information

  You can use the information in the full exception trace to help troubleshoot the issue. The exception generated by the probe contains a failure Reason that describes why the probe failed.

For most issues that occur in high availability environments, you can run the **Test-ReplicationHealth** cmdlet to help troubleshoot the cluster/networking/ActiveManager/services. Other HealthSet/Components will have different Test-\* cmdlets.

For example:

```powershell
Test-ReplicationHealth <ServerName>
```

The returned results will resemble the following table:

|Server|Check|Result|
|---|---|---|
|_\<ServerName\>_|`ClusterService`|`Passed`|
|_\<ServerName\>_|`ReplayService`|`Passed`|
|_\<ServerName\>_|`ActiveManager`|`Passed`|
|_\<ServerName\>_|`TasksRpcListener`|`Passed`|
|_\<ServerName\>_|`TcpListener`|`Passed`|
|_\<ServerName\>_|`ServerLocatorService`|`Passed`|
|_\<ServerName\>_|`DagMembersUp`|`Passed`|
|_\<ServerName\>_|`ClusterNetwork`|`Passed`|
|_\<ServerName\>_|`QuorumGroup`|`Passed`|
|_\<ServerName\>_|`FileShareQuorum`|`Passed`|
|_\<ServerName\>_|`DatabaseRedundancyCheck`|`Passed`|
|_\<ServerName\>_|`DatabaseAvailabilityCheck`|`Passed`|
|_\<ServerName\>_|`DBCopySuspended`|`Passed`|
|_\<ServerName\>_|`DBCopyFailed`|Passed|
|_\<ServerName\>_|`DBInitializing`|`Passed`|
|_\<ServerName\>_|`DBDisconnected`|`Passed`|
|_\<ServerName\>_|`DBLogCopyKeepingUp`|`Passed`|
|_\<ServerName\>_|`DBLogReplayKeepingUp`|`Passed`|

If all components display **Passed** in the **Result** column, try to rerun the associated probe as shown in step 2c in the Verifying the issue still exists section.

If the issue still exists, restart the server. After the server restarts, rerun the associated probe as shown in step 2c in the Verifying the issue still exists section.

If the probe continues to fail, you may need assistance to resolve this issue. Contact a Microsoft Support professional to resolve this issue. To contact a Microsoft Support professional, visit [Support for business](https://support.microsoft.com/supportforbusiness/productselection) and then select **Servers** \> **Exchange Server**. Because your organization may have a specific procedure for directly contacting Microsoft Product Support Services, be sure to review your organization's guidelines first.

## For More Information

[What's new in Exchange 2013](../../what-s-new-in-exchange-2013-exchange-2013-help.md)

[Exchange PowerShell](/powershell/exchange/)
