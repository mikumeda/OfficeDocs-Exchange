---
title: Troubleshooting HubTransport Health Set
TOCTitle: Troubleshooting HubTransport Health Set
ms:assetid: e3932ce3-836c-4230-9f64-63af1b704d79
ms:mtpsurl: https://technet.microsoft.com/library/ms.exch.scom.hubtransport(v=EXCHG.150)
ms:contentKeyID: 49720900
ms.reviewer: 
manager: serdars
ms.author: serdars
ms.topic: article
description: How to troubleshoot the HubTransport health set in Exchange 2013
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# Troubleshooting HubTransport Health Set

_**Applies to:** Exchange Server 2013_

The **HubTransport** health set monitors the overall health of the transport pipeline on Mailbox servers that's responsible for routing mail in your organization. For more information, see [Mail flow](../../mail-flow-exchange-2013-help.md).

If you receive an alert that indicates that the **HubTransport** health set is unhealthy, this indicates an issue that may prevent mail from being routed and delivered.

## Explanation

The **HubTransport** service is monitored using the following probes and monitors.

|Probe|Health Set|Associated Monitors|
|---|---|---
|ActiveQueueDrainFailureProbe|HubTransport|ActiveQueueDrainFailureMonitor|
|DiagnosticsAggregationLocalSnapshotProbe|HubTransport|DiagnosticsAggregationLocalSnapshotMonitor|
|DiagnosticsAggregationWebServiceProbe|HubTransport|DiagnosticsAggregationWebServiceMonitor|
|HubAvailabilityProbe|HubTransport|HubAvailabilityMonitor|
|HubTransportServiceRunning|HubTransport|HubTransportServiceRunningMonitor|
|ShadowQueueDiscardDrainFailureProbe|HubTransport|ShadowQueueDiscardDrainFailureMonitor|
|ThrottlingServiceRunning|HubTransport|ThrottlingServiceRunningMonitor|
|TransportEdgeSync.Service.Probe|HubTransport|TransportEdgeSync.Service.Monitor|
|TransportLogSearchRunningProbe|HubTransport|TransportLogSearchRunningMonitor|
|none (notification or check)|HubTransport|BootloaderOutstandingItemsTriggerMonitor|
|none (notification or check)|HubTransport|CrashEvent.edgetransport|
|none (notification or check)|HubTransport|CrashEvent.msexchangethrottling|
|none (notification or check)|HubTransport|CrashEvent.msexchangetransport|
|none (notification or check)|HubTransport|CrashEvent.msexchangetransportlogsearch|
|none (notification or check)|HubTransport|EdgeTransportBackpressureSustainedTimeMonitor|
|none (notification or check)|HubTransport|FederatedDecryptionAgentFailedToXDecryptMonitor|
|none (notification or check)|HubTransport|HubTransport.ServiceInconsistentState.Monitor|
|none (notification or check)|HubTransport|IsMemberOfResolverExpandedGroupsCacheSizeMonitor|
|none (notification or check)|HubTransport|IsMemberOfResolverResolvedGroupsCacheSizeMonitor|
|none (notification or check)|HubTransport|Messages.failed.to.be.made.redundant.Monitor|
|none (notification or check)|HubTransport|MessagesDeferredDuringCategorizationMonitor|
|none (notification or check)|HubTransport|MessageTrackingLogsDirQuotaMonitor|
|none (notification or check)|HubTransport|PrivateWorkingSetError.edgetransport|
|none (notification or check)|HubTransport|PrivateWorkingSetError.msexchahangetransportlogsearch|
|none (notification or check)|HubTransport|PrivateWorkingSetError.msexchangethrottling|
|none (notification or check)|HubTransport|PrivateWorkingSetError.msexchangetransport|
|none (notification or check)|HubTransport|PrivateWorkingSetWarning.edgetransport|
|none (notification or check)|HubTransport|PrivateWorkingSetWarning.msexchangethrottling|
|none (notification or check)|HubTransport|PrivateWorkingSetWarning.msexchangetransport|
|none (notification or check)|HubTransport|PrivateWorkingSetWarning.msexchangetransportlogsearch|
|none (notification or check)|HubTransport|ProcessProcessorTimeError.edgetransport|
|none (notification or check)|HubTransport|ProcessProcessorTimeError.msexchangethrottling|
|none (notification or check)|HubTransport|ProcessProcessorTimeError.msexchangetransport|
|none (notification or check)|HubTransport|ProcessProcessorTimeError.msexchangetransportlogsearch|
|none (notification or check)|HubTransport|ProcessProcessorTimeWarning.edgetransport|
|none (notification or check)|HubTransport|ProcessProcessorTimeWarning.msexchangethrottling|
|none (notification or check)|HubTransport|ProcessProcessorTimeWarning.msexchangetransport|
|none (notification or check)|HubTransport|ProcessProcessorTimeWarning.msexchangetransportlogsearch|
|none (notification or check)|HubTransport|QueueExternalAggregateMonitor|
|none (notification or check)|HubTransport|QueueInternalAggregateMonitor|
|none (notification or check)|HubTransport|QueueInternalAggregateNormalPriorityMonitor|
|none (notification or check)|HubTransport|QueueInternalHubRetryMonitor|
|none (notification or check)|HubTransport|QueueInternalHubRetryNormalPriorityMonitor|
|none (notification or check)|HubTransport|QueueMailboxRetryMonitor|
|none (notification or check)|HubTransport|QueueNonSMTPRetryMonitor|
|none (notification or check)|HubTransport|RuleEvaluationFailureEventLogMonitor|
|none (notification or check)|HubTransport|RuleEvaluationIgnoredFailureEventLogMonitor|
|none (notification or check)|HubTransport|RuleEvaluationIgnoredFipsFailureEventLogMonitor|
|none (notification or check)|HubTransport|RuleEvaluationSmallScaleFailureEventLogMonitor|
|none (notification or check)|HubTransport|RuleEvaluationSmallScaleFipsFailureEventLogMonitor|
|none (notification or check)|HubTransport|RuleExcessiveForkingEventLogMonitor|
|none (notification or check)|HubTransport|RuleLoadFailureEventLogMonitor|
|none (notification or check)|HubTransport|RuleLoadSmallScaleFailureEventLogMonitor|
|none (notification or check)|HubTransport|SmtpProxyEhloOptionsDoNotMatchContinueProxyingMonitor|
|none (notification or check)|HubTransport|SubmissionQueueMonitor|
|none (notification or check)|HubTransport|TlsDomainClientCertificateSubjectMismatchMonitor|
|none (notification or check)|HubTransport|Total.Shadow.Queue.Length.Above.Threshold.Monitor|
|none (notification or check)|HubTransport|TotalE2ELatencyHighForMSExchangeTransportMonitor|
|none (notification or check)|HubTransport|TotalE2ELatencyLowForMSExchangeTransportMonitor|
|none (notification or check)|HubTransport|TotalE2ELatencyNormalForMSExchangeTransportMonitor|
|none (notification or check)|HubTransport|Transport.CatExpiry.Monitor|
|none (notification or check)|HubTransport|Transport.Critical.Storage.Recovery.Failed.Monitor|
|none (notification or check)|HubTransport|Transport.DatabaseMoved.Monitor|
|none (notification or check)|HubTransport|Transport.DomainSecureCert.Monitor|
|none (notification or check)|HubTransport|Transport.DomainSecureCertAuth.Monitor|
|none (notification or check)|HubTransport|Transport.DomainSecureServerCertFailed.Monitor|
|none (notification or check)|HubTransport|Transport.DomainSecureServerDomainCertFailed.Monitor|
|none (notification or check)|HubTransport|Transport.FailedToCreatePickupDirectory.Monitor|
|none (notification or check)|HubTransport|Transport.InvalidAcceptedDomain.Monitor|
|none (notification or check)|HubTransport|Transport.LowDiskSpace.Monitor|
|none (notification or check)|HubTransport|Transport.Messages.Completing.Categorization.Monitor|
|none (notification or check)|HubTransport|Transport.NDRForUnrestrictedLargeDL.Monitor|
|none (notification or check)|HubTransport|Transport.PickupDelete.Monitor|
|none (notification or check)|HubTransport|Transport.PickupIsBadmailingFile.Monitor|
|none (notification or check)|HubTransport|Transport.SendConn.AuthKerb.Monitor|
|none (notification or check)|HubTransport|Transport.SendConnAuth.Monitor|
|none (notification or check)|HubTransport|Transport.SendConnTLS.Monitor|
|none (notification or check)|HubTransport|Transport.ServerCertExpireSoon.Monitor|
|none (notification or check)|HubTransport|Transport.ServerCertMismatch.Monitor|
|none (notification or check)|HubTransport|Transport.ServiceStartError.Monitor|
|none (notification or check)|HubTransport|Transport.SmtpSendDirectTrustFailed.Monitor|
|none (notification or check)|HubTransport|Transport.TemplateDoesNotExist.Monitor|
|none (notification or check)|HubTransport|Transport.TLSValidate.Monitor|
|none (notification or check)|HubTransport|Transport.UnknownTemplateInPublishingLicense.Monitor|
|none (notification or check)|HubTransport|TransportCategorizerJobAvailabilityMonitor|
|none (notification or check)|HubTransport|TransportDatabaseCorruptMonitor|
|none (notification or check)|HubTransport|TransportDeliveryFailures544Monitor|
|none (notification or check)|HubTransport|TransportDeliveryFailuresDeliveryStoreDriver520Monitor|
|none (notification or check)|HubTransport|TransportLogGenerationCheckpointDepthMonitor|
|none (notification or check)|HubTransport|TransportLogSearchLogPathInvalidMonitor|
|none (notification or check)|HubTransport|TransportMaxLocalLoopCountMonitor|
|none (notification or check)|HubTransport|TransportPickupReadMonitor|
|none (notification or check)|HubTransport|TransportPoisonMessageMonitor|
|none (notification or check)|HubTransport|TransportRejectingMessageSubmissionsMonitor|
|none (notification or check)|HubTransport|TransportServerCertPersonalStoreMonitor|
|none (notification or check)|HubTransport|UnreachableQueueMonitor|
|none (notification or check)|HubTransport|XProxyToTransientInvalidArgumentsMonitor|

For more information about probes and monitors, see [Server health and performance](../../server-health-and-performance-exchange-2013-help.md).

## User Action

It's possible that the service recovered after it issued the alert. Therefore, when you receive an alert that specifies that the **HubTransport** health set is unhealthy, first verify that the issue still exists. If the issue does exist, perform the appropriate recovery actions outlined in the following section.

## Verifying the issue

1. Identify the health set name and server name that are given in the alert.

2. The message details provide information about the exact cause of the alert. In most cases, the message details provide sufficient troubleshooting information to help identify the root cause. If the message details are not clear, do the following:

   1. Open the Exchange Management Shell, and run the following command to retrieve the details of the health set that issued the alert:

      ```powershell
      Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
      ```

      For example, to retrieve the **HubTransport** health set details about mailbox1.contoso.com, run the following command:

      ```powershell
      Get-ServerHealth mailbox1.contoso.com | ?{$_.HealthSetName -eq "HubTransport"}
      ```

   2. Review the command output to determine which monitor reported the error. The **AlertValue** value for the monitor that issued the alert will be **Unhealthy**.

   3. Rerun the associated probe for the monitor that's in an unhealthy state. Refer to the table in the [Explanation](troubleshooting-activesync-health-set.md) section to find the associated probe. To do this, run the following command:

      ```powershell
      Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
      ```

      For example, assume that the failing monitor is **ActiveQueueDrainFailureMonitor**. The probe associated with that monitor is **ActiveQueueDrainFailureProbe**. To run this probe on mailbox1.contoso.com, run the following command:

      ```powershell
      Invoke-MonitoringProbe HubTransport\ActiveQueueDrainFailureProbe -Server mailbox1.contoso.com | Format-List
      ```

   4. In the command output, review the "Result" section of the probe. If the value is **Succeeded**, the issue was a transient error, and it no longer exists.
