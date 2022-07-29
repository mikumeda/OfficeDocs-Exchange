---
title: Troubleshooting FIPS Health Set
TOCTitle: Troubleshooting FIPS Health Set
ms:assetid: 96e1b096-9cb5-426f-a84e-50d5599e4bbb
ms:mtpsurl: https://technet.microsoft.com/library/ms.exch.scom.fips(v=EXCHG.150)
ms:contentKeyID: 49720857
manager: serdars
ms.author: serdars
ms.topic: article
description: How to troubleshoot the FIPS health set in Exchange 2013
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# Troubleshooting FIPS Health Set

_**Applies to:** Exchange Server 2013_

The **FIPS** health set monitors the overall health of the Federal Information Processing Standards (FIPS) settings on Exchange servers. For more information about FIPS 140, see [FIPS 140-2 Validation](/windows/security/threat-protection/fips-140-validation).

If you receive an alert that indicates that the **FIPS** health set is unhealthy, this alert indicates an issue that may prevent your Exchange server from using FIPS 140-compliant components and processes.

## Explanation

The **FIPS** service is monitored using the following probes and monitors.

|Probe|Health Set|Associated Monitors|
|---|---|---|
|none (notification or check)|FIPS|CrashEvent.scanningprocess|
|none (notification or check)|FIPS|MaintenanceFailureMonitor.FIPS|
|none (notification or check)|FIPS|MaintenanceTimeoutMonitor.FIPS|
|none (notification or check)|FIPS|PrivateWorkingSetWarning.scanningprocess|
|none (notification or check)|FIPS|PrivateWorkingSetError.scanningprocess|
|none (notification or check)|FIPS|ProcessProcessorTimeWarning.scanningprocess|
|none (notification or check)|FIPS|ProcessProcessorTimeError.scanningprocess|

For more information about probes and monitors, see [Server health and performance](../../server-health-and-performance-exchange-2013-help.md).

## User Action

It's possible that the service recovered after it issued the alert. So, when you receive an alert that specifies that the **FIPS** health set is unhealthy, first verify that the issue still exists. If the issue does exist, perform the appropriate recovery actions outlined in the following section.

## Verifying the issue

1. Identify the health set name and server name that are given in the alert.

2. The message details provide information about the exact cause of the alert. In most cases, the message details provide sufficient troubleshooting information to help identify the root cause. If the message details are not clear, follow these steps:

   1. Open the Exchange Management Shell. Run the following command to retrieve the details of the health set that issued the alert:

      ```powershell
      Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
      ```

      For example, to retrieve the **FIPS** health set details about server1.contoso.com, run the following command:

      ```powershell
      Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "FIPS"}
      ```

   2. Review the command output to determine which monitor reported the error. The **AlertValue** value for the monitor that issued the alert will be **Unhealthy**.
