---
title: 'Server health and performance: Exchange 2013 Help'
TOCTitle: Server health and performance
ms:assetid: 9d1fdec8-8273-4c71-88f1-b4edfd542c4f
ms:mtpsurl: https://technet.microsoft.com/library/JJ150551(v=EXCHG.150)
ms:contentKeyID: 47560078
ms.reviewer: 
manager: serdars
ms.topic: article
description: Server health and performance in Microsoft Exchange Server
ms.author: serdars
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# Server health and performance

_**Applies to:** Exchange Server 2013_

Understanding server health and performance is critical to designing and maintaining a high-performance messaging infrastructure. Microsoft Exchange Server 2013 introduces improvements in server health and performance.

Looking for a list of all server health and performance topics? See Server health and performance documentation.

## Managed availability

Exchange 2013 introduces the concept of _managed availability_. Managed availability runs on every Exchange 2013 server. It's made up of two processes, the Exchange Health Manager Service (MSExchangeHMHost.exe) and the Exchange Health Manager Worker process (MSExchangeHMWorker.exe), and the following asynchronous components:

- **Probe engine**: The _probe engine_ takes measurements on the server.
- **Monitoring probe engine**: The _monitoring probe engine_ stores the business logic about what constitutes a healthy state. It functions like a pattern recognition engine, looking for patterns and measurements that differ from a healthy state, and then evaluating whether a component or feature is unhealthy.
- **Responder engine**: When the _responder engine_ is alerted about an unhealthy component, its first action is to try to recover that component. Managed availability enables multi-stage recovery actions. The first attempt may be to restart the application pool, the second attempt may be to restart the corresponding service, and the third attempt may be to restart the server. And, the final attempt may be to put the server offline, so that it no longer accepts traffic. If all of these actions fail, an alert is sent to the help desk.

For more information about managed availability, see [Managed Availability](managed-availability-exchange-2013-help.md).

## Workload management

Exchange 2013 workload management includes the following components:

- _User workload management_ is the new name for the user throttling features of Exchange Server 2010. You can customize these setting based on the needs of your environment.
- _System workload management_ is new for Exchange 2013 and is used to automatically throttle specific Exchange workloads by monitoring the health of key server resources. These settings should be customized only under the direction of Microsoft Customer Service and Support.

For more information, see [Exchange workload management](exchange-workload-management-exchange-2013-help.md).

## Server health and performance documentation

The following table contains links to topics that will help you learn about and manage server health and performance in Exchange 2013.

|Topic|Description|
|---|---|
|[Exchange workload management](exchange-workload-management-exchange-2013-help.md)|Learn about managing Exchange workloads by controlling how resources are consumed by individual users.|
|[Managed Availability](managed-availability-exchange-2013-help.md)|Learn about the built-in resource monitoring and recovery actions that are available in Exchange 2013.|
