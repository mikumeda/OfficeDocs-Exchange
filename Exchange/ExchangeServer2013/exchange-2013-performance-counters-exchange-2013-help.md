---
title: 'Exchange 2013 Performance Counters: Exchange 2013 Help'
TOCTitle: Exchange 2013 Performance Counters
ms:assetid: 9143dd77-7c30-4769-8de1-28c717cfa9e9
ms:mtpsurl: https://technet.microsoft.com/library/Dn904093(v=EXCHG.150)
ms:contentKeyID: 63917938
ms.reviewer: 
manager: serdars
ms.author: serdars
ms.topic: article
description: Using performance counters to troubleshooting Exchange Server
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# Exchange 2013 Performance Counters

_**Applies to:** Exchange Server 2013_

The following sections list helpful performance counters you can use when troubleshooting Exchange 2013 performance issues.

## Exchange Domain Controller Connectivity Counters

The following table displays acceptable thresholds and information about Exchange domain controller connectivity counters.

|Counter|Description|Threshold|
|---|---|---|
|MSExchange ADAccess Domain Controllers(\*)\LDAP Read Time|Shows the time in milliseconds (ms) to send an LDAP read request to the specified domain controller and receive a response.|Should be below 50 ms on average. Spikes (maximum values) shouldn't be higher than 100 ms.|
|MSExchange ADAccess Domain Controllers(\*)\LDAP Search Time|Shows the time (in ms) to send an LDAP search request and receive a response.|Should be below 50 ms on average. Spikes (maximum values) shouldn't be higher than 100 ms.|
|MSExchange ADAccess Processes(\*)\LDAP Read Time|Shows the time (in ms) to send an LDAP read request to the specified domain controller and receive a response.|Should be below 50 ms on average. Spikes (maximum values) shouldn't be higher than 100 ms.|
|MSExchange ADAccess Processes(\*)\LDAP Search Time|Shows the time (in ms) to send an LDAP search request and receive a response.|Should be below 50 ms on average. Spikes (maximum values) shouldn't be higher than 100 ms.|

## Processor and Process Counters

The following table displays acceptable thresholds and information about processors and process counters.

|Counter|Description|Threshold|
|---|---|---|
|Processor(\_Total)\% Processor Time|Shows the percentage of time that the processor is executing application or operating system processes. This value is when the processor isn't idle.|Should be less than 75% on average.|
|Processor(\_Total)\% User Time|Shows the percentage of processor time spent in user mode. User mode is a restricted processing mode designed for applications, environment subsystems, and integral subsystems.|Should be less than 75% on average.|
|Processor(\_Total)\% Privileged Time|Shows the percentage of processor time spent in privileged mode. Privileged mode is a processing mode designed for operating system components and hardware-manipulating drivers. It allows direct access to hardware and all memory.|Should be less than 75% on average.|
|System\Processor Queue Length (all instances)|Indicates the number of threads each processor is servicing. Processor Queue Length can be used to identify if processor contention or high CPU utilization is caused by the processor capacity being insufficient to handle the workloads assigned to it. Processor Queue Length shows the number of threads that are delayed in the Processor Ready Queue and are waiting to be scheduled for execution. The value listed is the last observed value at the time the measurement was taken.|Shouldn't be greater than 5 per processor.|
|Process(\*)\% Processor Time|Can be used to identify specific processes consuming CPU.|Not applicable|

## Memory Counters

The following table displays acceptable thresholds and information about memory counters.

|Counter|Description|Threshold|
|---|---|---|
|Memory\Available Mbytes|Shows the amount of physical memory, in megabytes (MB), immediately available for allocation to a process or for system use. It's equal to the sum of memory assigned to the standby (cached), free, and zero page lists. For a full explanation of the memory manager, refer to Microsoft Developer Network (MSDN) or "System Performance and Troubleshooting Guide" in the Windows Server 2003 Resource Kit.|Should remain above 5% of total RAM.|
|Memory\% Committed Bytes In Use|Shows the ratio of Memory\Committed Bytes to the Memory\Commit Limit. Committed memory is the physical memory in use for which space has been reserved in the paging file should it need to be written to disk. The commit limit is determined by the size of the paging file. If the paging file is enlarged, the commit limit increases, and the ratio is reduced. This counter displays the current percentage value only; it isn't an average.|If this value is more than 80%, it is an indication that the system is likely under stress to provide more memory.|

## .NET Framework Counters

The following table displays acceptable thresholds and information about .NET Framework counters.

|Counter|Description|Threshold|
|---|---|---|
|.NET CLR Memory(\*)\% Time in GC|Shows when garbage collection has occurred. When the counter exceeds the threshold, it indicates that CPU is cleaning up and isn't being used efficiently for load. Adding memory to the server would improve this situation.|Should be below 10% on average.|
|.NET CLR Exceptions(\*)\# of Exceps Thrown / sec|Displays the number of exceptions thrown per second. These exceptions include both .NET Framework exceptions and unmanaged exceptions that get converted into .NET Framework exceptions. For example, the null pointer reference exception in unmanaged code would get thrown again in managed code as a .NET Framework System.NullReferenceException. This counter includes both handled and unhandled exceptions.|Should be less than 5% of total requests per second (RPS) (`Web Server(_Total)\Connection Attempts/sec * .05)`.|
|.NET CLR Memory(\*)\# Bytes in all Heaps|Shows the sum of four other counters: Gen 0 Heap Size, Gen 1 Heap Size, Gen 2 Heap Size, and Large Object Heap Size. This counter indicates the current memory allocated in bytes on the GC Heaps.|Not applicable|

## Network Counters

The following table displays acceptable thresholds and information about common network counters.

|Counter|Description|Threshold|
|---|---|---|
|Network Interface(\*)\Packets Outbound Errors|Indicates the number of outbound packets that couldn't be transmitted because of errors.|Should always be 0.|
|TCPv6\Connection Failures|Shows the number of times TCP connections have made a direct transition to the CLOSED state from the SYN-SENT state or the SYN-RCVD state, plus the number of times TCP connections have made a direct transition to the LISTEN state from the SYN-RCVD state.|An increasing number of failures, or a consistently increasing rate of failures, can indicate a bandwidth shortage.|
|TCPv4\Connections Reset|Shows the number of times TCP connections have made a direct transition to the CLOSED state from either the ESTABLISHED state or the CLOSE-WAIT state.|An increasing number of resets, or a consistently increasing rate of resets, can indicate a bandwidth shortage.|
|TCPv6\Connections Reset|Shows the number of times TCP connections have made a direct transition to the CLOSED state from either the ESTABLISHED state or the CLOSE-WAIT state.|An increasing number of resets, or a consistently increasing rate of resets, can indicate a bandwidth shortage.|

## Netlogon Counters

The following table displays acceptable thresholds and information about common counters for monitoring NTLM authentication issues and MaxConcurrentAPI issues. For more information, see the Microsoft Knowledge Base article [KB2688798](https://support.microsoft.com/help/2688798).

|Counter|Description|Threshold|
|---|---|---|
|\Netlogon\Semaphore Waiters|The number of the thread that is waiting to obtain the semaphore.|For more information, see the Microsoft Knowledge Base article [KB2688798](https://support.microsoft.com/help/2688798).|
|\Netlogon\Semaphore Holders|The number of the thread that is holding the semaphore.|Not applicable|
|\Netlogon\Semaphore Acquires|The total number of times that the semaphore has been obtained over the lifetime of the security channel connection, or since system startup for _Total.|Not applicable|
|\Netlogon\Semaphore Timeouts|The total number of times that a thread has timed out while it waited for the semaphore over the lifetime of the security channel connection, or since system startup for \_Total.|Not applicable|
|\Netlogon\Average Semaphore Hold Time|The average time (in seconds) that the semaphore is held over the last sample.|Not applicable|

## Database Counters

The following table shows active log I/O latency requirements counters and their acceptable thresholds. When thresholds are exceeded, the client experience degrades. For example, users may experience message delivery delays or slow system performance.

> [!NOTE]
> Normal storage latency guidance in Exchange 2013 is very similar to the guidance from Exchange 2010. Additional database counters can be found in [Mailbox Server Counters](/previous-versions/office/exchange-server-2010/ff367871(v=exchg.141)).

|Counter|Description|Threshold|
|---|---|---|
|MSExchange Database ==> Instances(\*)\I/O Database Reads (Attached) Average Latency|Shows the average length of time, in milliseconds (ms), per database read operation.|Should be less than 20 ms on average.|
|MSExchange Database ==> Instances(\*)\I/O Database Writes (Attached) Average Latency|Shows the average length of time, in ms, per database write operation.|Should be less than 50 ms on average.|
|MSExchange Database ==> Instances(\*)\I/O Log Writes Average Latency|Shows the average length of time, in ms, per Log write operation.|Should be less than 10 ms on average.|
|MSExchange Database ==> Instances(\*)\I/O Database Reads (Recovery) Average Latency|Shows the average length of time, in ms, per passive database read operation.|Should be less than 200 ms on average.|
|MSExchange Database ==> Instances(\*)\I/O Database Writes (Recovery) Average Latency|Shows the average length of time, in ms, per passive database write operation.|Should be less than the read latency for the same instance, as measured by the MSExchange Database ==> Instances(\*)\I/O Database Reads (Recovery) Average Latency counter.|
|MSExchange Database ==> Instances(\*)\I/O Database Reads (Attached)/sec|Shows the number of database read operations per second for each attached database instance.|Not applicable|
|MSExchange Database ==> Instances(\*)\I/O Database Writes (Attached)/sec|Shows the number of database write operations per second for each attached database instance.|Not applicable|
|MSExchange Database ==> Instances(\*)\I/O Log Writes/sec|Shows the number of log writes per second for each database instance.|Not applicable|
|MSExchange Active Manager(\_total)\Database Mounted|Shows the number of active database copies on the server.|Not applicable|

## ASP.NET

The following table displays acceptable thresholds and information about ASP.NET counters.

|Counter|Description|Threshold|
|---|---|---|
|ASP.NET\Application Restarts|Shows the number of times the application has been restarted during the Web server's lifetime.|Should always be 0.|
|ASP.NET\Worker Process Restarts|Shows the number of times a worker process has restarted on the computer.|Should always be 0.|
|ASP.NET\Request Wait Time|Shows the number of ms the most recent request was waiting in the queue.|Should always be 0.|
|ASP.NET Applications(\*)\Requests In Application Queue|Shows the number of requests in the application request queue.|Should always be 0.|
|ASP.NET Applications(\*)\Requests Executing|Shows the number of requests currently executing.|Not applicable|
|ASP.NET Applications(\*)\Requests/Sec|Shows the number of requests executed per second.|Not applicable|

## RPC Client Access Counters

The following table displays acceptable thresholds and information about RPC Client Access counters.

|Counter|Description|Threshold|
|---|---|---|
|MSExchange RpcClientAccess\RPC Averaged Latency|Shows the latency, in milliseconds (ms), averaged for the past 1,024 packets.|Should be below 250 ms.|
|MSExchange RpcClientAccess\RPC Requests|Shows the number of client requests currently being processed by the RPC Client Access service.|Shouldn't be over 40.|
|MSExchange RpcClientAccess\Active User Count|Shows the number of unique users that have shown some activity in the last 2 minutes.|Not applicable|
|MSExchange RpcClientAccess\Connection Count|Shows the total number of client connections maintained.|Not applicable|
|MSExchange RpcClientAccess\RPC Operations/sec|Shows the rate at which RPC operations occur, per second.|Not applicable|
|MSExchange RpcClientAccess\User Count|Shows the number of users connected to the service.|Not applicable|

## HTTP Proxy Counters

The following table displays information about HTTP Proxy counters.

|Counter|Description|
|---|---|
|MSExchange HttpProxy(\*)\MailboxServerLocator Average Latency|Shows the average latency (ms) of MailboxServerLocator web service calls.|
|MSExchange HttpProxy(\*)\Average Authentication Latency|Shows the average time spent authenticating CAS requests over the last 200 samples.|
|MSExchange HttpProxy(\*)\Average ClientAccess Server Processing Latency|Shows the average latency (ms) of CAS processing time (does not include time spent proxying) over the last 200 requests.|
|MSExchange HttpProxy(\*)\Mailbox Server Proxy Failure Rate|Shows the percentage of connectivity related failures between this Client Access Server and MBX servers over the last 200 samples.|
|MSExchange HttpProxy(\*)\Outstanding Proxy Requests|Shows the number of concurrent outstanding proxy requests.|
|MSExchange HttpProxy(\*)\Proxy Requests/Sec|Shows the number of proxy requests processed each second.|
|MSExchange HttpProxy(\*)\Requests/Sec|Shows the number of requests processed each second.|

## Information Store Counters

The following table displays acceptable thresholds and information about Information Store counters.

> [!NOTE]
> Normal storage latency guidance in Exchange 2013 is very similar to the guidance from Exchange 2010. Additional Information Store counters can be found in [Mailbox Server Counters](/previous-versions/office/exchange-server-2010/ff367871(v=exchg.141)).

|Counter|Description|Threshold|
|---|---|---|
|MSExchangeIS Store(\*)\RPC Requests|Indicates the overall RPC requests currently executing within the information store process.|Should always be below 70.|
|MSExchangeIS Client Type(\*)\RPC Average Latency|Shows a server RPC latency, in ms, averaged for the past 1,024 packets for a particular client protocol.|Should be less than 50 ms on average for each client.|
|MSExchangeIS Store(\*)\RPC Average Latency|RPC Latency average (msec) is the average latency in milliseconds of RPC requests per database. Average is calculated over all RPCs since exrpc32 was loaded.|Should always be less than 50 ms, with spikes less than 100 ms.|
|MSExchangeIS Store(\*)\RPC Operations/sec|Shows the number of RPC operations per second for each database instance.|Not applicable|
|MSExchangeIS Client Type(\*)\RPC Operations/sec|Shows the number of RPC operations per second for each client type connection.|Not applicable|

## Client Access Server Counters

The following table displays information about client connection counters and Internet Information Services (IIS) counters.

|Counter|Description|
|---|---|
|MSExchange ActiveSync\Requests/sec|Shows the number of HTTP requests received from the client via ASP.NET per second. Determines the current Exchange ActiveSync request rate. Used only to determine current user load.|
|MSExchange ActiveSync\Ping Commands Pending|Shows the number of ping commands currently pending in the queue.|
|MSExchange ActiveSync\Sync Commands/sec|Shows the number of sync commands processed per second. Clients use this command to synchronize items within a folder.|
|MSExchange Availability Service\Availability Requests (sec)|Shows the number of requests serviced per second. The request can be only for free/ busy information or include suggestions. One request may contain multiple mailboxes. Determines the rate at which Availability service requests are occurring.|
|MSExchange OWA\Current Unique Users|Shows the number of unique users currently logged on to Outlook Web App. This value monitors the number of unique active user sessions, so that users are only removed from this counter after they log off or their session times out. Determines current user load.|
|MSExchange OWA\Requests/sec|Shows the number of requests handled by Outlook Web App per second. Determines current user load.|
|MSExchangeAutodiscover\Requests/sec|Shows the number of Autodiscover service requests processed each second. Determines current user load.|
|MSExchangeWS\Requests/sec|Shows the number of requests processed each second. Determines current user load.|
|Web Service(\_Total)\Current Connections|Shows the current number of connections established with the Web service. Determines current user load.|
|Web Service(Default Web Site)\Current Connections|Shows the current number of connections established to the Default website, which corresponds to the number of connections hitting the Front End CAS server role. Determines current user load.|
|WebService(\_Total)\Connection Attempts/sec|Shows the rate that connections to the Web service are being attempted. Determines current user load.|
|Web Service(\_Total)\Other Request Methods/sec|Shows the rate HTTP requests are made that don't use the OPTIONS, GET, HEAD, POST, PUT, DELETE, TRACE, MOVE, COPY, MKCOL, PROPFIND, PROPPATCH, SEARCH, LOCK, or UNLOCK methods. Determines current user load.|

## Workload Management Counters

The following table displays information about Exchange Workload Management counters. These counters are important to monitor because workload management may run tasks in the background during off-peak times.

|Counter|Description|
|---|---|
|MSExchange WorkloadManagement Workloads(\*)\ActiveTasks|Shows the number of active tasks currently running in the background for workload management.|
|MSExchange WorkloadManagement Workloads(\*)\CompletedTasks|Shows the number of workload management tasks that have been completed.|
|MSExchange WorkloadManagement Workloads(\*)\QueuedTasks|Shows the number of workload management tasks that are currently queued up waiting to be processed.|
