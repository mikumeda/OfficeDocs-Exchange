---
title: 'Exchange Management Shell quick reference for Exchange 2013'
TOCTitle: Exchange Management Shell quick reference for Exchange 2013
ms:assetid: 3ea4a105-a93c-48ba-96ce-6170125354e1
ms:mtpsurl: https://technet.microsoft.com/library/JJ619302(v=EXCHG.150)
ms:contentKeyID: 49352789
ms.reviewer: 
manager: serdars
ms.author: serdars
author: msdmaguire
ms.topic: article
description: Exchange Management Shell quick reference for Exchange 2013 
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# Exchange Management Shell quick reference for Exchange 2013

_**Applies to:** Exchange Server 2013_

This topic describes the most frequently used cmdlets available in the release to manufacturing (RTM) and later versions of Microsoft Exchange Server 2013 and provides examples of their use.

> [!NOTE]
> More content will be added about other areas of Exchange 2013 soon.

For more information about the Exchange Management Shell in Exchange 2013 and all the available cmdlets, see the following topics:

- [Using PowerShell with Exchange 2013 (Exchange Management Shell)](/powershell/exchange/exchange-management-shell)

- [Exchange PowerShell](/powershell/exchange/)

## What would you like to learn about?

## Common cmdlet actions

The following verbs are supported by most cmdlets and are associated with a specific action.

|Verb|Description|
|---|---|
|New|The New verb creates an instance of something, such as a new configuration setting, a new database, or a new SMTP connector.|
|Remove|The Remove verb removes an instance of something, such as a mailbox or transport rule. <br/><br/> All Remove cmdlets support the _WhatIf_ and _Confirm_ parameters. For more information about these parameters, see Important Parameters.|
|Enable|The Enable verb enables a setting or mail-enables a recipient.|
|Disable|The Disable verb disables an enabled setting or mail-disables a recipient. <br/><br/> All Disable tasks also support the _WhatIf_ and _Confirm_ parameters. For more information about these parameters, see Important Parameters.|
|Set|The Set verb modifies specific settings of an object, such as the alias of a contact or the deleted item retention of a mailbox database.|
|Get|The Get verb queries a specific object or a subset of a type of object, such as a specific mailbox, all mailbox users, or mailbox users in a domain.|

## Important parameters

The following parameters help you control how your commands run and indicate exactly what a command will do before it affects data.

|Parameter|Description|
|---|---|
|Identity|The _Identity_ parameter identifies the unique object for the task. It's typically used with Enable, Disable, Remove, Set, and Get cmdlets. _Identity_ is also a positional parameter, which means that you don't have to specify _Identity_ when you specify the parameter's value on the command line. <br/><br/> For example, _Get-Mailbox -Identity user1_ queries for the mailbox of _user1_. _Get-Mailbox user1_ is equivalent to `Get-Mailbox -Identity user1`.|
|WhatIf|The _WhatIf_ parameter instructs the cmdlet to simulate the actions that it would take on the object. By using the _WhatIf_ parameter, you can view what changes would occur without actually applying any of the changes. The default value is $true.|
|Confirm|The _Confirm_ parameter causes the cmdlet to pause processing and requires the administrator to acknowledge what the cmdlet will do before processing continues. The default value is $true.|
|Validate|The _Validate_ parameter causes the cmdlet to check that all prerequisites for running the operation are satisfied and that the operation will complete successfully.|

## Tips and tricks

The following commands are associated with various tasks that you can use when administering Exchange 2013.

|Cmdlet|Description|
|---|---|
|`Get-Command`|This cmdlet retrieves all tasks that can be executed in Exchange 2013.|
|`Get-Command *keyword*`|This cmdlet retrieves tasks that have _keyword_ in the cmdlet.|
|`Get-Task | Get-Member`|This cmdlet retrieves all properties and methods of _Task_.|
|`Get-Task | Format-List`|This cmdlet displays the output of the query in a formatted list. You can pipe the output of any Get cmdlet to Format-List to view the whole set of properties that exist on the object returned by that command, or you can specify individual properties that you want to view, separated by commas, as in the following example: `Get-Mailbox john | Format-List alias,*quota*`.|
|`Help Task`|This cmdlet retrieves Exchange Management Shell help information for any task in Exchange 2013, as in the following example: `Help Get-Mailbox`.|
|`Get-Task | Format-List > file.txt`|This cmdlet exports the output of _Task_ to a text file: _file.txt_|

## Permissions

|Command|Description|
|---|---|
|`Get-RoleGroupMember "Organization Management"`|This command retrieves the members of the _Organization Management_ management role group.|
|`Get-ManagementRoleAssignment -Role "Mail Recipient Creation" -GetEffectiveUsers`|This command retrieves a list of all the users who are granted permissions provided by the _Mail Recipient Creation_ management role. This includes users who are members of role groups or universal security groups (USGs) that are assigned the Mail Recipient Creation role. This doesn't include users who are members of linked role groups in another forest.|
|`Get-ManagementRoleAssignment -RoleAssignee Administrator | Get-ManagementRole | Get-ManagementRoleEntry`|This command retrieves a list of cmdlets that the user _Administrator_ can run.|
|`ForEach ($RoleEntry in Get-ManagementRoleEntry *Remove-Mailbox -Parameters Identity) {Get-ManagementRoleAssignment -Role $RoleEntry.Role -GetEffectiveUsers -Delegating $False | Where-Object {$_.EffectiveUserName -Ne "All Group Members"} | FL Role, EffectiveUserName, AssignmentChain}`|This command retrieves a list of all the users who can run the _Remove-Mailbox_ cmdlet.|
|`Get-ManagementRoleAssignment -WritableRecipient kima -GetEffectiveUsers | FT RoleAssigneeName, EffectiveUserName, Role, AssignmentChain`|This command retrieves a list of all users who can modify the mailbox of _kima_.|
|`New-ManagementScope "Seattle Users" -RecipientRestrictionFilter "City -Eq 'Seattle'"` <br/><br/> `New-RoleGroup "Seattle Admins" -Roles "Mail Recipients", "Mail Recipient Creation", "Mailbox Import Export", -CustomRecipientWriteScope "Seattle Users"`|This command creates a new management scope and management role group to enable members of the role group to manage recipients in Seattle. <br/><br/> First, the _Seattle Users_ management scope is created, which matches only recipients who have _Seattle_ in the _City_ attribute on their user object. <br/><br/> Then, a new role group called _Seattle Admins_ is created and the _Mail Recipients_, _Mail Recipient Creation_, and _Mailbox Import Export_ roles are assigned. The role group is scoped so that its members can manage only users who match the _Seattle Users_ recipient filter scope.|
|`New-ManagementScope "Vancouver Servers" -ServerRestrictionFilter "ServerSite -Eq 'Vancouver'"` <br/><br/> `$RoleGroup = Get-RoleGroup "Server Management" <br/><br/> New-RoleGroup "Vancouver Server Management" -Roles $RoleGroup.Roles -CustomConfigWriteScope "Vancouver Servers"`|This command creates a new management scope and copies an existing role group to enable members of the new role group to manage only servers in the Vancouver Active Directory site. <br/><br/> First, the _Vancouver Servers_ management scope is created, which matches only servers that are located in the _Vancouver_ Active Directory site. The Active Directory site is stored in the _ServerSite_ attribute on the server objects. <br/><br/> Then, a new role group called _Vancouver Server Management_ is created that's a copy of the _Server Management_ role group. This new role group, however, is scoped to allow its members to manage only servers that match the _Vancouver Servers_ configuration filter scope.|
|`Add-RoleGroupMember "Organization Management" -Member davids`|This command adds the user _davids_ to the _Organization Management_ role group.|
|`Get-ManagementRoleAssignment -Role "Mail Recipient Creation" -RoleAssignee "Seattle Admins" | Remove-ManagementRoleAssignment`|This command removes the _Mail Recipient Creation_ role from the _Seattle Admins_ role group. This command is useful because you don't need to know the name of the management role assignment that assigns the role to the role group.|

## Remote Shell

|Command|Description|
|---|---|
|`$Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri http://ExServer.contoso.com/PowerShell/ -Authentication Kerberos` <br/><br/> `Import-PSSession $Session`|These commands open a new remote Shell session between a local domain-joined computer and a remote Exchange 2013 server with the FQDN _ExServer.contoso.com_. Use this command if you want to administer a remote Exchange 2013 server and only have the Windows Management Framework, which includes the Windows PowerShell command-line interface, installed on your local computer. This command uses your current logon credentials to authenticate against the remote Exchange 2013 server.|
|`$UserCredential = Get-Credential` <br/><br/> `$Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri http://ExServer.contoso.com/PowerShell/ -Authentication Kerberos -Credential $UserCredential` <br/><br/> `Import-PSSession $Session`|These commands open a new remote Shell session between a local domain-joined computer and a remote Exchange 2013 server with the FQDN ExServer.contoso.com. Use this command if you want to administer a remote Exchange 2013 server and only have the Windows Management Framework, which includes Windows PowerShell, installed on your local computer. This command uses credentials you specify explicitly to authenticate against the remote Exchange 2013 server.|
|`Remove-PSSession $Session`|This command closes the remote Shell session between a local computer and the remote Exchange 2013 server.|
|`Import-RecipientDataProperty -Identity "Tony Smith" -SpokenName -FileData ([System.IO.File]::ReadAllBytes('M:\AudioFiles\TonySmith.wma'))`|This command shows an example of the syntax required to import a file into a remote Exchange 2013 server using the FileData parameter on a cmdlet. The syntax encapsulates the data contained in the _M:\AudioFiles\TonySmith.wma_ file and streams the data to the FileData property on the Import-RecipientDataProperty cmdlet. <br/><br/> The _FileData_ parameter accepts data from a file on your local computer using this syntax on most cmdlets.|
|`$SN = Export-RecipientDataProperty -Identity tonys@contoso.com -SpokenName` <p> `[System.IO.File]::WriteAllBytes('C:\tonysmith.wma', $SN.FileData)`|This command shows an example of the syntax required to export a file from a remote Exchange 2013 server. The syntax encapsulates the data stored in the FileData property on the object returned by the cmdlet and then streams the data to your local computer. The data is then stored in the _C:\tonysmith.wma_ file. <br/><br/> Most cmdlets that output objects with a FileData property use this syntax to export data to a file on your local computer.|
