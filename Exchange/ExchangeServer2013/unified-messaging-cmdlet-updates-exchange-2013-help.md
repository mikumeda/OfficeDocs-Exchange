---
title: 'Unified Messaging cmdlet updates: Exchange 2013 Help'
TOCTitle: Unified Messaging cmdlet updates
ms:assetid: a42c6643-67ed-4003-854a-ac1d66efb965
ms:mtpsurl: https://technet.microsoft.com/library/JJ150557(v=EXCHG.150)
ms:contentKeyID: 47560083
ms.reviewer: 
ms.topic: article
manager: serdars
ms.author: serdars
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
description: An overview of the updated parameters in UM cmdlets in Exchange 2013.
---

# Unified Messaging cmdlet updates in Exchange Server

_**Applies to:** Exchange Server 2013, Exchange Server 2016_

Many of the Unified Messaging (UM) cmdlets that existed in Exchange Server 2010 have been brought over for Exchange Server 2013, but there have been changes to some of those cmdlets. In addition, new cmdlets were added for Exchange 2013.

## Updated parameters and new UM cmdlets

The following is a list of the updated parameters and new cmdlets for Exchange 2013.

|Cmdlet|Parameters|
|---|---|
|New-UMIPGateway|`[-IPAddressFamily <IPv4Only | IPv6Only | Any>]`|
|Set-UMIPGateway|`[-IPAddressFamily <IPv4Only | IPv6Only | Any>]`|
|Get-UMMailbox|`[-AccountPartition <AccountPartitionIdParameter>]`|
|Set-UMMailbox|`[-ImListMigrationCompleted <$true | $false> -VoiceMailAnalysisEnabled <$true | $false>]`|
|Test-Connectivity|`[-CallRouter <SwitchParameter>]`|
|New-UMCallAnsweringRule|`[-Name <String> [-CallerIds <MultiValuedProperty>] [-CallersCanInterruptGreeting <$true | $false>] [-CheckAutomaticReplies <$true | $false>] [-Confirm [<SwitchParameter>]] [-DomainController <Fqdn>] [-ExtensionsDialed <MultiValuedProperty>] [-KeyMappings <MultiValuedProperty>] [-Mailbox <MailboxIdParameter>] [-Organization <OrganizationIdParameter>] [-Priority <Int32>] [-ScheduleStatus <Int32>] [-TimeOfDay <TimeOfDay>] [-WhatIf [<SwitchParameter>]]`|
|Remove-UMCallAnsweringRule|`[-Identity <UMCallAnsweringRuleIdParameter> [-Confirm [<SwitchParameter>]] [-DomainController <Fqdn>] [-Mailbox <MailboxIdParameter>] [-WhatIf [<SwitchParameter>]]`|
|Get-UMCallAnsweringRule|`[-Identity <UMCallAnsweringRuleIdParameter>] [-DomainController <Fqdn>] [-Mailbox <MailboxIdParameter>]`|
|Set-UMCallAnsweringRule|`[-Identity <UMCallAnsweringRuleIdParameter> [-CallerIds <MultiValuedProperty>] [-CallersCanInterruptGreeting <$true | $false>] [-CheckAutomaticReplies <$true | $false>] [-Confirm [<SwitchParameter>]] [-DomainController <Fqdn>] [-ExtensionsDialed <MultiValuedProperty>] [-KeyMappings <MultiValuedProperty>] [-Mailbox <MailboxIdParameter>] [-Name <String>] [-Priority <Int32>] [-ScheduleStatus <Int32>] [-TimeOfDay <TimeOfDay>] [-WhatIf [<SwitchParameter>]]`|
|Enable-UMCallAnsweringRule|`[-Identity <UMCallAnsweringRuleIdParameter> [-Confirm [<SwitchParameter>]] [-DomainController <Fqdn>] [-Mailbox <MailboxIdParameter>] [-WhatIf [<SwitchParameter>]]`|
|Disable-UMCallAnsweringRule|`[-Identity <UMCallAnsweringRuleIdParameter> [-Confirm [<SwitchParameter>]] [-DomainController <Fqdn>] [-Mailbox <MailboxIdParameter>] [-WhatIf [<SwitchParameter>]]`|
|Get-UMCallRouterSettings|`[-DomainController <Fqdn>] [-Server <ServerIdParameter>]`|
|Set-UMCallRouterSettings|`Set-UMCallRouterSettings [-Confirm [<SwitchParameter>]] [-DialPlans <MultiValuedProperty>] [-DomainController <Fqdn>] [-IPAddressFamily <IPv4Only | IPv6Only | Any>] [-IPAddressFamilyConfigurable <$true | $false>] [-Server <ServerIdParameter>] [-SipTcpListeningPort <Int32>] [-SipTlsListeningPort <Int32>] [-UMPodRedirectTemplate <String>] [-UMStartupMode <TCP | TLS | Dual>] [-WhatIf [<SwitchParameter>]]`|
|Disable-UMService|`-Identity <UMServerIdParameter> [-Confirm [<SwitchParameter>]] [-DomainController <Fqdn>] [-Immediate <$true | $false>] [-WhatIf [<SwitchParameter>]]` <p> **Note**: This cmdlet only works with Exchange 2007 and 2010 UM servers.|
|Enable-UMService|`-Identity <UMServerIdParameter> [-Confirm [<SwitchParameter>]] [-DomainController <Fqdn>] [-WhatIf [<SwitchParameter>]]` <p> **Note**: This cmdlet only works with Exchange 2007 and 2010 UM servers.|
|Get-UMService|`[-Identity <UMServerIdParameter>] [-DomainController <Fqdn>]`|
|Set-UMService|`Set-UMService -Identity <UMServerIdParameter> [-Confirm [<SwitchParameter>]] [-DialPlans <MultiValuedProperty>] [-DomainController <Fqdn>] [-GrammarGenerationSchedule <ScheduleInterval[]>] [-IPAddressFamily <IPv4Only | IPv6Only | Any>] [-IPAddressFamilyConfigurable <$true | $false>] [-IrmLogEnabled <$true | $false>] [-IrmLogMaxAge <EnhancedTimeSpan>] [-IrmLogMaxDirectorySize <Unlimited>] [-IrmLogMaxFileSize <ByteQuantifiedSize>] [-IrmLogPath <LocalLongFullPath>] [-MaxCallsAllowed <Int32>] [-SIPAccessService <ProtocolConnectionSettings>] [-UMStartupMode <TCP | TLS | Dual>] [-WhatIf [<SwitchParameter>]]`|

For details about all UM cmdlets, see [Exchange PowerShell](/powershell/exchange/).
