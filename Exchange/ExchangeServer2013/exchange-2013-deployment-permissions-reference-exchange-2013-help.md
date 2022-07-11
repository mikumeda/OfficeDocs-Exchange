---
title: 'Exchange 2013 deployment permissions reference: Exchange 2013 Help'
TOCTitle: Exchange 2013 deployment permissions reference
ms:assetid: b13412d0-0cc4-4c1d-bf31-cae3d3e211a9
ms:mtpsurl: https://technet.microsoft.com/library/Ee681663(v=EXCHG.150)
ms:contentKeyID: 56348434
ms.reviewer:
ms.topic: article 
manager: serdars
ms.author: serdars
author: msdmaguire
description: Exchange Server deployment permissions reference
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# Exchange 2013 deployment permissions reference

_**Applies to:** Exchange Server 2013_

This topic describes the permissions that are required to set up a Microsoft Exchange Server 2013 organization. The universal security groups (USGs) that are associated with management role groups, and other Windows security groups and security principals, are added to the access control lists (ACLs) of various Active Directory objects. ACLs control what operations can be performed on each object. By understanding what permissions are granted to each role group, security group, or security principal, you can determine what minimum permissions are required to install Exchange 2013.

In some cases, the ACL isn't applied on the usual property, **ntSecurityDescriptor**, but on another property, such as **msExchMailboxSecurityDescriptor**. The directory service can't enforce security that isn't specified in the Windows security descriptor. In most cases, these ACLs are replicated to store ACLs on appropriate objects by the store service. Unfortunately, there is no tool to view these ACLs as anything other than raw binary data.

The columns of each permissions table include the following information:

- **Account**: The security principal granted or denied the permissions.
- **ACE type**: Access control entry (ACE) type
  - **Allow ACE**: An allow ACE allows the user or group associated with the ACE to access an item.
  - **Deny ACE**: A deny ACE prevents the user or group associated with the ACE from accessing an item.
- **Inheritance**: The type of inheritance used for child objects.
  - **All** indicates that the permissions apply to the object and all sub-objects.
  - **Desc** indicates the permissions apply to the object class listed in the On Property/Applies To row.
  - **None** indicates those permissions only apply the object.
- **Permissions**: The permissions granted to the account.
- **On Property/Applies To**: In some cases, permissions apply only to a given property, property set, or object class. These limited permissions are specified here.
- **Comments**: When applicable, this column explains why the permissions are required or provides other information about the permissions.

The permissions are generally listed in the table by the names that are used on the Active Directory Service Interfaces (ADSI) Edit (AdsiEdit.msc) **Security** property page in the **Advanced** view on the **View/Edit** tab. The ADSI Edit **Security** property page lists a much more condensed view of the permissions. The LDP tool (Ldp.exe) displays the access mask directly as a numeric value. The setup code refers to the permissions by predefined constants.

The following table shows the relationships between these values.

|ADSI Edit Summary page|ADSI Edit Advanced view, View/Edit tab|ACL entries applied to a given object|Binary value (access mask in LDP)|
|---|---|---|---|
|Full Control|Full Control|`WRITE_OWNER | WRITE_DAC | READ_CONTROL | DELETE | ACTRL_DS_CONTROL_ACCESS | ACTRL_DS_LIST_OBJECT | ACTRL_DS_DELETE_TREE | ACTRL_DS_WRITE_PROP | ACTRL_DS_READ_PROP | ACTRL_DS_SELF | ACTRL_DS_LIST | ACTRL_DS_DELETE_CHILD | ACTRL_DS_CREATE_CHILD`|`0x000F01FF`|
|Read|List Contents + Read All Properties + Read Permissions|`ACTRL_DS_LIST | ACTRL_DS_READ_PROP | READ_CONTROL`|`0x00020014`|
|Write|Write All Properties + All Validated Writes|`ACTRL_DS_WRITE_PROP | ACTRL_DS_SELF`|`0x00000028`|
||List Contents|`ACTRL_DS_LIST`|`0x00000004`|
||Read All Properties|`ACTRL_DS_READ_PROP`|`0x00000010`|
||Write All Properties|`ACTRL_DS_WRITE_PROP`|`0x00000020`|
||Delete|`DELETE`|`0x00010000`|
||Delete Subtree|`ACTRL_DS_DELETE_TREE`|`0x00000040`|
||Read Permissions|`READ_CONTROL`|`0x00020000`|
||Modify Permissions|`WRITE_DAC`|`0x00040000`|
||Modify Owner|`WRITE_OWNER`|`0x00080000`|
||All Validated Writes|`ACTRL_DS_SELF`|`0x00000008`|
||All Extended Rights|`ACTRL_DS_CONTROL_ACCESS`|`0x00000100`|
|Create All Child Objects|Create All Child Objects|`ACTRL_DS_CREATE_CHILD`|`0x00000001`|
|Delete All Child Objects|Delete All Child Objects|`ACTRL_DS_DELETE_CHILD`|`0x00000002`|
|||`ACTRL_DS_LIST_OBJECT`|`0x00000080`|

Extended rights are custom rights specified by individual applications. They are specified in the ACL. However, they are meaningless to Active Directory. The specific application enforces any extended rights. Examples of Exchange extended rights are "Create public folder" or "Create named properties in the information store."

For information about permissions that are set during a Microsoft Exchange Server 2010 installation, see [Exchange 2010 Deployment Permissions Reference](/previous-versions/office/exchange-server-2010/ee681663(v=exchg.141)).

## Prepare Active Directory Permissions

The permissions tables in this section show the permissions set when you execute the `Setup /PrepareAD` command.

> [!NOTE]
> The permissions described in this section are the default permissions that are configured when you deploy Exchange 2013 using the shared permissions model. If you've deployed Exchange 2013 using the Active Directory split permissions model, the default permission are different. For more information on the changes to the default permissions when using Active Directory split permissions and the shared and split permissions models in general, see [Active Directory split permissions](understanding-split-permissions-exchange-2013-help.md) in [Understanding split permissions](understanding-split-permissions-exchange-2013-help.md). If you don't choose to use Active Directory split permissions when you install Exchange, Exchange will use shared permissions.

## Microsoft Exchange Container Permissions

The following table shows the permissions that are set on the Microsoft Exchange container within the configuration partition.

### Distinguished name of the object: CN=Microsoft Exchange,CN=Services,CN=Configuration,DC=\<domain\>

|Account|ACE type|Inheritance|Permissions|On property/ Applies to|Comments|
|---|---|---|---|---|---|
|Installation Account|Allow ACE|All|Full Control||This is the account that is used to run `/PrepareAD`.|
|Organization Management|Allow ACE|All|Full Control|||
|Exchange Trusted Subsystem|Allow ACE|All|Full Control|||
|Exchange Servers|Allow ACE|All|Read|||
|Authenticated Users|Allow ACE|None|Read Property <br><br> List Contents|||
|Exchange Trusted Subsystem|Allow ACE|All|Modify Permissions|`msExchSmtpRceiveConnector`||
|Public Folder Management|Allow ACE|All|Read <br><br> List Object|||
|Delegated Setup|Allow ACE|All|Read <br><br> List Object|||

## Microsoft Exchange Autodiscover Container Permissions

The following table shows the permissions set on the Microsoft Exchange Autodiscover container within the configuration partition.

### Distinguished name of the object: CN=Microsoft Exchange Autodiscover,CN=Services,CN=Configuration,DC=\<domain\>

|Account|ACE type|Inheritance|Permissions|On property/ Applies to|
|---|---|---|---|---|
|Exchange Servers|Allow ACE|All|Read||

## Microsoft Exchange Organization Container Permissions

The permissions tables in this section show the permissions set on the Microsoft Exchange Organization and sub-containers within the configuration partition.

### Distinguished name of the object: CN=\<organization\>,CN=Microsoft Exchange,CN=Services,CN=Configuration,DC=\<domain\>

|Account(s)|ACE type|Inheritance|Permissions|On property/ Applies to|Comments|
|---|---|---|---|---|---|
|Enterprise Admins <br><br> Root Domain Admins <br><br> Installation Account <br><br> Organization Management|Deny ACE|All|Send As <br><br> Receive As||Windows administrators aren't allowed to open mailboxes.|
|Enterprise Admins <br><br> Schema Admins <br><br> Root Domain Admins <br><br> Installation Account <br><br> Organization Management|Deny ACE|All|Exchange Web Services Impersonation <br><br> Exchange Web Services Token Serialization||Extended right|
|Enterprise Admins <br><br> Schema Admins <br><br> Root Domain Admins <br><br> Installation Account|Deny ACE|All|Store Transport Access <br><br> Store Constrained Delegation <br><br> Store Read Access <br><br> Store Read Write Access|||
|Local System|Allow|All|All Extended Rights|||
|Authenticated Users|Deny ACE|Desc|Read Property|`msExchAvailabilityUserPassword / msExchAvailabilityAddressSpace`||
|Authenticated Users|Allow|None|Read|||
|Organization Management|Allow ACE|All|Read Permissions <br><br> List Contents <br><br> Read Property <br><br> List Object|||
|Public Folder Management|Allow ACE|All|Read Permissions <br><br> List Contents <br><br> Read Property <br><br> List Object|||
|NT Authority\Network Service|Allow ACE|All|Read|||
|Managed Availability Servers|Allow ACE|All|Read Permissions <br><br> List Contents <br><br> Read Property <br><br> List Object|||
|Exchange Servers|Allow ACE|All|All Extended Rights|||
|Exchange Servers|Allow ACE|All|Write Property|`groupType`||
|Exchange Servers|Allow ACE|All|Write Property|`msExchOwningServer`||
|Exchange Servers|Allow ACE|All|Write Property|`msExchMailboxSecurityDescriptor`||
|Exchange Servers|Allow ACE|All|Write Property|`msExchUMServerWritableFlags`||
|Exchange Servers|Allow ACE|All|Write Property|`msExchDatabaseCreated`||
|Exchange Servers|Allow ACE|All|Write Property|`msExchUserCulture`||
|Exchange Servers|Allow ACE|All|Write Property|`msExchMobileMailboxFlags`||
|Exchange Servers|Allow ACE|All|Write Property|`siteFolderGUID`||
|Exchange Servers|Allow ACE|All|Write Property|`siteFolderServer`||
|Exchange Servers|Allow ACE|All|Write Property|`msExchEDBOffline`||
|Exchange Servers|Allow ACE|All|Write Property|`userCertificate`||
|Exchange Servers|Allow ACE|All|Write Property|`msExchUMDtmfMap`||
|Exchange Servers|Allow ACE|All|Write Property|`msExchBlockedSendersHash`||
|Exchange Servers|Allow ACE|All|Write Property|`Personal Information`||
|Exchange Servers|Allow ACE|All|Write Property|`Public Information`||
|Exchange Servers|Allow ACE|All|Write Property|`Exchange Information`||
|Exchange Servers|Allow ACE|All|Write Property|`msExchPatchMDB`||
|Exchange Servers|Allow ACE|All|Write Property|`publicDelegates`||
|Exchange Servers|Allow ACE|All|Write Property|`msExchUMSpokenName`||
|Exchange Servers|Allow ACE|All|Write Property|`msExchUMPinChecksum`||
|Exchange Servers|Allow ACE|All|Write Property|`legacyExchangeDN`||
|Exchange Servers|Allow ACE|All|Write Property|`msExchSafeSendersHash`||
|Exchange Servers|Allow ACE|All|Write Property|`thumbnailPhoto`||
|Organization Management|Allow ACE|All|Create top level public folder|||
|Public Folder Management|Allow ACE|All|Create top level public folder|||
|Organization Management|Allow ACE|All|View information store status|||
|Public Folder Management|Allow ACE|All|View information store status|||
|Organization Management|Allow ACE|All|Administer information store|||
|Public Folder Management|Allow ACE|All|Administer information store|||
|Organization Management|Allow ACE|All|Create named properties in the information store|||
|Public Folder Management|Allow ACE|All|Create named properties in the information store|||
|Organization Management|Allow ACE|All|Modify public folder ACL|||
|Public Folder Management|Allow ACE|All|Modify public folder ACL|||
|Organization Management|Allow ACE|All|Modify public folder quotas|||
|Public Folder Management|Allow ACE|All|Modify public folder quotas|||
|Organization Management|Allow ACE|All|Modify public folder admin ACL|||
|Public Folder Management|Allow ACE|All|Modify public folder admin ACL|||
|Organization Management|Allow ACE|All|Modify public folder expiry|||
|Public Folder Management|Allow ACE|All|Modify public folder expiry|||
|Organization Management|Allow ACE|All|Modify public folder replica list|||
|Public Folder Management|Allow ACE|All|Modify public folder replica list|||
|Organization Management|Allow ACE|All|Modify public folder deleted item retention|||
|Public Folder Management|Allow ACE|All|Modify public folder deleted item retention|||
|Organization Management|Allow ACE|All|Create public folder|||
|Public Folder Management|Allow ACE|All|Create public folder|||
|Public Folder Management|Allow ACE|All|Mail Enable Public Folder|||
|Everyone <br><br> NT Authority\Anonymous Logon <br><br>|Allow ACE|All|Create named properties in the information store|||
|Everyone <br><br> NT Authority\Anonymous Logon <br><br>|Allow ACE|All|Create public folder|||
|Everyone <br><br> NT Authority\Anonymous Logon <br><br>|Allow ACE|Desc|Read Permissions <br><br> List Contents <br><br> Read Property <br><br> List Object|`/ msExchPrivateMDB`||
|Everyone <br><br> NT Authority\Anonymous Logon <br><br>|Allow ACE|Desc|Read Permissions <br><br> List Contents <br><br> Read Property <br><br> List Object|`/ msExchPublicMDB`||
|Exchange Servers|Allow ACE|Desc|Read Permissions <br><br> List Contents <br><br> Read Property <br><br> List Object|`/ siteAddressing`||

### Distinguished name of the object: CN=All Address Lists,CN=Address Lists Container,CN=\<organization\>

|Account|ACE type|Inheritance|Permissions|On property/ Applies to|
|---|---|---|---|---|
|Authenticated Users|Allow ACE|All|List Contents||
|Organization Management|Allow ACE|All|Write Property|`msExchLastAppliedRecipientFilter` <br><br> `msExchRecipientFilterFlags`|
|Public Folder Management|Allow ACE|All|Write Property|`msExchLastAppliedRecipientFilter` <br><br> `msExchRecipientFilterFlags`|

### Distinguished name of the object: CN=Offline Address Lists,CN=Address Lists Container, CN=\<organization\>

|Account|ACE type|Inheritance|Permissions|On property/ Applies to|
|---|---|---|---|---|
|Authenticated Users|Allow ACE|All|Download Offline Address Book||

### Distinguished name of the object: CN=Addressing,CN=\<organization\>

|Account|ACE type|Inheritance|Permissions|On property/ Applies to|
|---|---|---|---|---|
|Authenticated users|Allow ACE|All|Read||

### Distinguished name of the object: CN=Recipient Policies,CN=\<organization\>

|Account|ACE type|Inheritance|Permissions|On property/ Applies to|
|---|---|---|---|---|
|Organization Management|Allow ACE|All|Write Property|`msExchLastAppliedRecipientFilter` <br><br> `msExchRecipientFilterFlags`|
|Public Folder Management|Allow ACE|All|Write Property|`msExchLastAppliedRecipientFilter` <br><br> `msExchRecipientFilterFlags`|

## Configuration Partition Container Permissions

The permissions tables in this section show the permissions set by the `Setup /PrepareAD` command on various containers within the configuration partition.

### Distinguished name of the object: CN=Sites,CN=Configuration,DC=\<domain\>

|Account|ACE type|Inheritance|Permissions|On property/ Applies to|
|---|---|---|---|---|
|Organization Management <br><br> Exchange Trusted Subsystem|Allow ACE|All|Write Property|`msExchVersion / site`|
|Organization Management <br><br> Exchange Trusted Subsystem|Allow ACE|All|Write Property|`msExchVersion / site-link`|
|Organization Management <br><br> Exchange Trusted Subsystem|Allow ACE|All|Write Property|`msExchPartnerId / site`|
|Organization Management <br><br> Exchange Trusted Subsystem|Allow ACE|All|Write Property|`msExchMinorPartnerId / site`|
|Organization Management <br><br> Exchange Trusted Subsystem|Allow ACE|All|Write Property|`msExchResponsibleforSites / site`|
|Organization Management <br><br> Exchange Trusted Subsystem|Allow ACE||Write Property|`msExchTransportSiteFlags / site`|
|Organization Management <br><br> Exchange Trusted Subsystem|Allow ACE|All|Write Property|`msExchCost / site-link`|
|Organization Management <br><br> Exchange Trusted Subsystem <br><br> Local System <br><br> Exchange Servers|Allow ACE|Desc|Read Permissions <br><br> List Contents <br><br> Read Property <br><br> List Object|`/ msExchEdgeSyncEHFConnector`|
|Organization Management <br><br> Exchange Trusted Subsystem <br><br> Local System <br><br> Exchange Servers|Allow ACE|Desc|Read Permissions <br><br> List Contents <br><br> Read Property <br><br> List Object|`/ msExchEdgeSyncMservConnector`|
|Organization Management <br><br> Exchange Trusted Subsystem|Allow ACE|Children|Create Child <br><br> Delete Child <br><br> Delete Tree|`msExchEdgeSyncServiceConfig / site`|
|Organization Management <br><br> Exchange Trusted Subsystem <br><br> Local System <br><br> Exchange Servers|Allow ACE|Desc|Read Permissions <br><br> List Contents <br><br> Read Property <br><br> List Object|`/ msExchEdgeSyncServiceConfig`|
|Organization Management <br><br> Exchange Trusted Subsystem|Allow ACE|Children|Create Child <br><br> Delete Child <br><br> Delete Tree|`msExchEdgeSyncMservConnector / msExchEdgeSyncServiceConfig`|
|Organization Management <br><br> Exchange Trusted Subsystem|Allow ACE|Children|Create Child <br><br> Delete Child <br><br> Delete Tree|`msExchEdgeSyncEHFConnector / msExchEdgeSyncServiceConfig`|

### Distinguished name of the object: CN=Deleted Objects,CN=Configuration,DC=\<domain\>

|Account|ACE type|Inheritance|Permissions|On property/ Applies to|Comments|
|---|---|---|---|---|---|
|Exchange Servers|Allow ACE|All|List Contents|||
|Organization Administration|Allow ACE|All|Read <br><br> List Object|||
|Installation Account|Allow ACE|All|Read Permission <br><br> Write Permission <br><br> List Contents <br><br> Read Property <br><br> List Object||This is the account that is used to run `/PrepareAD`.|
|Exchange Trusted Subsystem|Allow ACE|All|Read <br><br> List Object|||
|Network Service|Allow ACE|All|List Contents|||

## Exchange Administrative Group Permissions

The `Setup /PrepareAD` command also configures the following permissions on the administrative groups within the organization.

### Distinguished name of the object: CN=\<admin group\>,CN=Administrative Groups,CN=\<organization\>

|Account|ACE type|Inheritance|Permissions|On property/ Applies to|Comments|
|---|---|---|---|---|---|
|Organization Management|Allow ACE|Desc|Access Recipient Update Service|`msExchExchangeServer`|Allows Exchange Recipient Administrators to stamp recipients with proxy address information.|
|Local System|Allow ACE|Desc|Access Recipient Update Service|`msExchExchangeServer`|Allows the servers to stamp recipients with proxy address information.|
|Public Folder Management|Allow ACE|Desc|Access Recipient Update Service|`msExchExchangeServer`|Allows Exchange Public Folder Administrators to stamp recipients with proxy address information.|

### Distinguished name of the object: CN=Advanced Security Settings,CN=\<admin group\>,CN=Administrative Groups,CN=\<organization\>

|Account|ACE type|Inheritance|Permissions|On property/ Applies to|
|---|---|---|---|---|
|Authenticated Users|Allow ACE|None|List Contents||

### Distinguished name of the object: CN=Encryption,CN=Advanced Security Settings,CN=\<admin group\>,CN=Administrative Groups,CN=\<organization\>

|Account|ACE type|Inheritance|Permissions|On property/ Applies to|
|---|---|---|---|---|
|Authenticated Users|Allow ACE|None|Read Property||

### Distinguished name of the object: CN=Arrays,CN=\<admin group\>,CN=Administrative Groups,CN=\<organization\>

|Account|ACE type|Inheritance|Permissions|On property/ Applies to|
|---|---|---|---|---|
|Authenticated Users|Allow ACE|None|List Contents||

### Distinguished name of the object: CN=Database Availability Groups,CN=\<admin group\>,CN=Administrative Groups,CN=\<organization\>

|Account|ACE type|Inheritance|Permissions|On property/ Applies to|
|---|---|---|---|---|
|Authenticated Users|Allow ACE|None|List Contents||

### Distinguished name of the object: CN=Databases,CN=\<admin group\>,CN=Administrative Groups,CN=\<organization\>

|Account|ACE type|Inheritance|Permissions|On property/ Applies to|
|---|---|---|---|---|
|Authenticated Users|Allow ACE|None|List Contents||

### Distinguished name of the object: CN=Servers,CN=\<admin group\>,CN=Administrative Groups,CN=\<organization\>

|Account|ACE type|Inheritance|Permissions|On property/ Applies to|Comments|
|---|---|---|---|---|---|
|Exchange Servers|Deny ACE|All|Receive As||Exchange Servers aren't allowed to open mailboxes.|
|Authenticated Users|Allow ACE|None|List Contents|||

## Microsoft Exchange Security Groups Container Permissions

The permissions tables in this section show the permissions set on the Microsoft Exchange Security Groups container within the root domain partition.

### Distinguished name of the object: OU=Microsoft Exchange Security Groups,DC=\<root domain\>

|Account|ACE type|Inheritance|Permissions|On property/ Applies to|
|---|---|---|---|---|
|Organization Management|Allow ACE|All|Full Control||
|Exchange Trusted Subsystem|Allow ACE|All|Create Child|`/ Group`|
|Exchange Trusted Subsystem|Allow ACE|Desc|Delete|`/ group`|
|Exchange Trusted Subsystem|Allow ACE|Desc|Write Property|`Member / group`|

### Distinguished name of the object: CN=Organization Management,OU=Microsoft Exchange Security Groups,DC=\<root domain\>

|Account|ACE type|Inheritance|Permissions|On property/ Applies to|
|---|---|---|---|---|
|Organization Management|Allow ACE|All|Full Control||

### Distinguished name of the object: CN=Public Folder Management,OU=Microsoft Exchange Security Groups,DC=\<root domain\>

|Account|ACE type|Inheritance|Permissions|On property/ Applies to|
|---|---|---|---|---|
|Organization Management|Allow ACE|All|Full Control||

### Distinguished name of the object: CN=ExchangeLegacyInterop,OU=Microsoft Exchange Security Groups,DC=\<root domain\>

|Account|ACE type|Inheritance|Permissions|On property/ Applies to|
|---|---|---|---|---|
|Organization Management|Allow ACE|All|Full Control||

### Distinguished name of the object: CN=Exchange Servers,OU=Microsoft Exchange Security Groups,DC=\<root domain\>

|Account|ACE type|Inheritance|Permissions|On property/ Applies to|
|---|---|---|---|---|
|Organization Management|Allow ACE|All|Full Control||
|Root Domain Administrators|Allow ACE|All|Read Members <br><br> Write Members||
|Child Domain Administrators|Allow ACE|All|Read Members <br><br> Write Members||

## Prepare Domain

The following tables show the permissions set when you execute the `Setup /PrepareDomain` command.

> [!NOTE]
> The permissions described in this section are the default permissions that are configured when you deploy Exchange 2013 using the shared permissions model. If you've deployed Exchange 2013 using the Active Directory split permissions model, the default permission are different. For more information on the changes to the default permissions when using Active Directory split permissions and the shared and split permissions models in general, see [Active Directory split permissions](understanding-split-permissions-exchange-2013-help.md) in [Understanding split permissions](understanding-split-permissions-exchange-2013-help.md). If you don't choose to use Active Directory split permissions when you install Exchange, Exchange will use shared permissions.

### Distinguished name of the object: DC=\<domain\>

|Account|ACE type|Inheritance|Permissions|On property/ Applies to|Comments|
|---|---|---|---|---|---|
|Authenticated Users|Allow ACE|All|Read Property|`Exchange Information`||
|NT AUTHORITY\NETWORK|Allow ACE|All|Read Property|`Exchange Personal Information`|Grants Transport service read permissions.|
|Exchange Servers|Allow ACE|All|Write Property|`groupType`||
|Exchange Servers|Allow ACE|All|Write Property|`msExchMailboxSecurityDescriptor`||
|Exchange Servers|Allow ACE|All|Write Property|`msExchUMServerWritableFlags`||
|Exchange Servers|Allow ACE|All|Read Property|`Exchange Personal Information`||
|Exchange Servers|Allow ACE|All|Read Property|`Exchange Information`||
|Exchange Servers|Allow ACE|All|Write Property|`msExchUserCultulre`||
|Exchange Servers|Allow ACE|All|Read Property|`memberOf`||
|Exchange Servers|Allow ACE|All|Read Property|`garbageCollPeriod`||
|Exchange Servers|Allow ACE|All|Read Property|`userAccountControl`||
|Exchange Servers|Allow ACE|All|Read Property|`canonicalName`||
|Exchange Servers|Allow ACE|All|Replication Synchronization||Extended right|
|Exchange Servers|Allow ACE|All|Create Child <br><br> Delete Chile <br><br> List Children|`msExchActiveSyncDevices / User`||
|Exchange Servers|Allow ACE|All|Create Child <br><br> Delete Child <br><br> List Children|`msExchActiveSyncDevices / inetOrgPerson`||
|Exchange Servers|Allow ACE|All|Write Property|`msExchSafeSendersHash`||
|Exchange Servers|Allow ACE|All|Write Property|`msExchPublicDelegates`||
|Exchange Servers|Allow ACE|All|Write Property|`msExchMobileMailboxFlags`||
|Exchange Servers|Allow ACE|All|Write Property|`msExchSafeRecipientsHash`||
|Exchange Servers|Allow ACE|All|Write Property|`userCertificate`||
|Exchange Servers|Allow ACE|All|Write Property|`msExchUMDtmfMap`||
|Exchange Servers|Allow ACE|All|Write Property|`msExchBlockedSendersHash`||
|Exchange Servers|Allow ACE|All|Write Property|`msExchUMSpokenName`||
|Exchange Servers|Allow ACE|All|Write Property|`msExchUMPinChecksum`||
|Exchange Servers|Allow ACE|All|Write Property|`thumbnailPhoto`||
|Organization Management|Allow ACE|All|Read <br><br> List Object|||
|Organization Management|Allow ACE|All|Write Property|`Exchange Information`||
|Organization Management|Allow ACE|All|Write Property|`garbageCollPeriod`||
|Organization Management|Allow ACE|All|Write Property|`legacyExchangeDN`||
|Organization Management|Allow ACE|All|Write Property|`msExchPublicDelegates`||
|Organization Management|Allow ACE|All|Write Property|`textEncodedORAddress`||
|Organization Management|Allow ACE|All|Write Property|`proxyAddresses`||
|Organization Management|Allow ACE|All|Write Property|`mail`||
|Organization Management|Allow ACE|All|Write Property|`displayNamePrintable`||
|Organization Management|Allow ACE|All|Write Property|`showInAddressBook`||
|Organization Management|Allow ACE|All|Write Property|`Exchange Personal Information`||
|Organization Management|Allow ACE|All|Full Control|`/ msExchDynamicDistributionList`||
|Organization Management|Allow ACE|All|Write Property|`adminDisplayName`||
|Organization Management|Allow ACE|All|Write Property|`displayName`||
|Exchange Trusted Subsystem|Allow ACE|All|Read <br><br> List Object|||
|Exchange Trusted Subsystem|Allow ACE|All|Write Property|`displayName`||
|Exchange Trusted Subsystem|Allow ACE|All|Write Property|`Public Information`||
|Exchange Trusted Subsystem|Allow ACE|All|Write Property|`msExchPublicDelegates`||
|Exchange Trusted Subsystem|Allow ACE|All|Write Property|`adminDisplayName`||
|Exchange Trusted Subsystem|Allow ACE|All|Full Control|`/ msExchDynamicDistributionList`||
|Exchange Trusted Subsystem|Allow ACE|All|Write Property|`Exchange Information`||
|Exchange Trusted Subsystem|Allow ACE|All|Write Property|`Exchange Personal Information`||
|Exchange Trusted Subsystem|Allow ACE|All|Write Property|`garbageCollPeriod`||
|Exchange Trusted Subsystem|Allow ACE|All|Write Property|`textEncodedORAddress`||
|Exchange Trusted Subsystem|Allow ACE|All|Write Property|`showInAddressBook`||
|Exchange Trusted Subsystem|Allow ACE|All|Write Property|`legacyExchangeDN`||
|Exchange Trusted Subsystem|Allow ACE|All|Write Property|`Personal Information`||
|Exchange Trusted Subsystem|Allow ACE|All|Write Property|`proxyAddresses`||
|Exchange Trusted Subsystem|Allow ACE|All|Write Property|`displayNamePrintable`||
|Exchange Trusted Subsystem|Allow ACE|All|Write Property|`mail`||
|Exchange Windows Permissions|Allow ACE|All|Write Property|`pwdLastSet`||
|Exchange Windows Permissions|Allow ACE|All|WriteDACL|`/ user`||
|Exchange Windows Permissions|Allow ACE|All|WriteDACL|`/ inetOrgPerson`||
|Exchange Windows Permissions|Allow ACE|All|Delete Tree|`/ user`||
|Exchange Windows Permissions|Allow ACE|All|Delete Tree|`/ inetOrgPerson`||
|Exchange Windows Permissions|Allow ACE|All|Write Property|`sAMAccountName`||
|Exchange Windows Permissions|Allow ACE|All|Create Child <br><br> Delete|`/ contact`||
|Exchange Windows Permissions|Allow ACE|All|Create Child <br><br> Delete|`/ inetOrgPerson`||
|Exchange Windows Permissions|Allow ACE|All|Create Child <br><br> Delete|`/ user`||
|Exchange Windows Permissions|Allow ACE|All|Create Child <br><br> Delete|`/ organizationUnit`||
|Exchange Windows Permissions|Allow ACE|All|Create Child <br><br> Delete|`/ group`||
|Exchange Windows Permissions|Allow ACE|All|Create Child <br><br> Delete Child|`/ computer`||
|Exchange Windows Permissions|Allow ACE|All|Write Property|`Member`||
|Exchange Windows Permissions|Allow ACE|All|Write Property|`wwwHomePage`||
|Exchange Windows Permissions|Allow ACE|All|Write Property|`countryCode`||
|Exchange Windows Permissions|Allow ACE|All|Write Property|`userAccountControl`||
|Exchange Windows Permissions|Allow ACE|All|Write Property|`managedBy`||
|Exchange Windows Permissions|Allow ACE|All|Reset Password on Next Logon||Extended right|
|Exchange Windows Permissions|Allow ACE|All|Change Password|` / user`|Extended right|
|Delegated Setup|Allow ACE|All|Read Property|`User Account Restrictions`||

### Distinguished name of the object: CN=AdminSDHolder,CN=System,DC=\<domain\>

|Account|ACE type|Inheritance|Permissions|On property/ Applies to|Comments|
|---|---|---|---|---|---|
|Authenticated Users|Allow ACE|All|Read Property|`Exchange Information`||
|NT AUTHORITY\NETWORK|Allow ACE|All|Read Property|`Exchange Personal Information`|Grants Transport service read permissions.|
|Exchange Servers|Allow ACE|All|Write Property|`groupType`||
|Exchange Servers|Allow ACE|All|Write Property|`msExchMailboxSecurityDescriptor`||
|Exchange Servers|Allow ACE|All|Write Property|`msExchUMServerWritableFlags`||
|Exchange Servers|Allow ACE|All|Read Property|`Exchange Personal Information`||
|Exchange Servers|Allow ACE|All|Read Property|`Exchange Information`||
|Exchange Servers|Allow ACE|All|Write Property|`msExchUserCultulre`||
|Exchange Servers|Allow ACE|All|Read Property|`memberOf`||
|Exchange Servers|Allow ACE|All|Read Property|`garbageCollPeriod`||
|Exchange Servers|Allow ACE|All|Read Property|`userAccountControl`||
|Exchange Servers|Allow ACE|All|Read Property|`canonicalName`||
|Exchange Servers|Allow ACE|All|Replication Synchronization||Extended right|
|Exchange Servers|Allow ACE|All|Create Child <br><br> Delete Chile <br><br> List Children|`msExchActiveSyncDevices / User`||
|Exchange Servers|Allow ACE|All|Create Child <br><br> Delete Child <br><br> List Children|`msExchActiveSyncDevices / inetOrgPerson`||
|Exchange Servers|Allow ACE|All|Write Property|`msExchSafeSendersHash`||
|Exchange Servers|Allow ACE|All|Write Property|`msExchPublicDelegates`||
|Exchange Servers|Allow ACE|All|Write Property|`msExchMobileMailboxFlags`||
|Exchange Servers|Allow ACE|All|Write Property|`msExchSafeRecipientsHash`||
|Exchange Servers|Allow ACE|All|Write Property|`userCertificate`||
|Exchange Servers|Allow ACE|All|Write Property|`msExchUMDtmfMap`||
|Exchange Servers|Allow ACE|All|Write Property|`msExchBlockedSendersHash`||
|Exchange Servers|Allow ACE|All|Write Property|`msExchUMSpokenName`||
|Exchange Servers|Allow ACE|All|Write Property|`msExchUMPinChecksum`||
|Exchange Servers|Allow ACE|All|Write Property|`thumbnailPhoto`||
|Organization Management|Allow ACE|All|Read <br><br> List Object|||
|Organization Management|Allow ACE|All|Write Property|`Exchange Information`||
|Organization Management|Allow ACE|All|Write Property|`garbageCollPeriod`||
|Organization Management|Allow ACE|All|Write Property|`legacyExchangeDN`||
|Organization Management|Allow ACE|All|Write Property|`msExchPublicDelegates`||
|Organization Management|Allow ACE|All|Write Property|`textEncodedORAddress`||
|Organization Management|Allow ACE|All|Write Property|`proxyAddresses`||
|Organization Management|Allow ACE|All|Write Property|`mail`||
|Organization Management|Allow ACE|All|Write Property|`displayNamePrintable`||
|Organization Management|Allow ACE|All|Write Property|`showInAddressBook`||
|Organization Management|Allow ACE|All|Write Property|`Exchange Personal Information`||
|Organization Management|Allow ACE|All|Full Control|`/ msExchDynamicDistributionList`||
|Organization Management|Allow ACE|All|Write Property|`adminDisplayName`||
|Organization Management|Allow ACE|All|Write Property|`displayName`||
|Exchange Trusted Subsystem|Allow ACE|All|Read <br><br> List Object|||
|Exchange Trusted Subsystem|Allow ACE|All|Write Property|`displayName`||
|Exchange Trusted Subsystem|Allow ACE|All|Write Property|`Public Information`||
|Exchange Trusted Subsystem|Allow ACE|All|Write Property|`msExchPublicDelegates`||
|Exchange Trusted Subsystem|Allow ACE|All|Write Property|`adminDisplayName`||
|Exchange Trusted Subsystem|Allow ACE|All|Full Control|`/ msExchDynamicDistributionList`||
|Exchange Trusted Subsystem|Allow ACE|All|Write Property|`Exchange Information`||
|Exchange Trusted Subsystem|Allow ACE|All|Write Property|`Exchange Personal Information`||
|Exchange Trusted Subsystem|Allow ACE|All|Write Property|`garbageCollPeriod`||
|Exchange Trusted Subsystem|Allow ACE|All|Write Property|`textEncodedORAddress`||
|Exchange Trusted Subsystem|Allow ACE|All|Write Property|`showInAddressBook`||
|Exchange Trusted Subsystem|Allow ACE|All|Write Property|`legacyExchangeDN`||
|Exchange Trusted Subsystem|Allow ACE|All|Write Property|`Personal Information`||
|Exchange Trusted Subsystem|Allow ACE|All|Write Property|`proxyAddresses`||
|Exchange Trusted Subsystem|Allow ACE|All|Write Property|`displayNamePrintable`||
|Exchange Trusted Subsystem|Allow ACE|All|Write Property|`mail`||
|Exchange Windows Permissions|Allow ACE|All|Write Property|`pwdLastSet`||
|Exchange Windows Permissions|Allow ACE|All|Write Property|`sAMAccountName`||
|Exchange Windows Permissions|Allow ACE|All|Write Property|`Member`||
|Exchange Windows Permissions|Allow ACE|All|Write Property|`wwwHomePage`||
|Exchange Windows Permissions|Allow ACE|All|Write Property|`countryCode`||
|Exchange Windows Permissions|Allow ACE|All|Write Property|`userAccountControl`||
|Exchange Windows Permissions|Allow ACE|All|Write Property|`managedBy`||
|Delegated Setup|Allow ACE|All|Read Property|`User Account Restrictions`||

### Distinguished name of the object: CN=Deleted Objects,DC=\<domain\>

|Account|ACE type|Inheritance|Permissions|On property/ Applies to|
|---|---|---|---|---|
|Exchange Servers|Allow ACE|All|List Contents||

### Distinguished name of the object: CN=Microsoft Exchange System Objects,DC=\<domain\>

|Account|ACE type|Inheritance|Permissions|On property/ Applies to|
|---|---|---|---|---|
|NT AUTHORITY\NETWORK|Allow ACE|All|Read Property <br><br> List Contents <br><br> Read Permissions||
|Authenticated Users|Allow ACE|All|Read Permissions||
|Authenticated Users|Allow ACE|All|Read Property|`garbageCollPeriod`|
|Authenticated Users|Allow ACE|All|Read Property|`adminDisplayName`|
|Authenticated Users|Allow ACE|All|Read Property|`modifyTimeStamp`|
|Exchange Servers|Deny ACE|All|Delete Tree||
|Exchange Servers|Allow ACE|All|Read Permissions <br><br> List Contents <br><br> Read PropertyDelete Tree||
|Exchange Servers|Allow ACE|All|Create Child|`/ msExchSystemMailbox`|
|Exchange Servers|Allow ACE|All|Create Child <br><br> Delete Child|`/ publicFolder`|
|Exchange Servers|Allow ACE|All|Create Child|`/ user`|
|Exchange Servers|Allow ACE|All|Delete Child|`/ msExchSystemMailbox`|
|Exchange Servers|Allow ACE|All|Delete Child|`/ user`|
|Exchange Servers|Allow ACE|Desc|Write Property|`/ publicFolder`|
|Exchange Servers|Allow ACE|Desc|Write Property|`/ msExchSystemMailbox`|
|Exchange Servers|Allow ACE|Desc|Write Property|`/ user`|
|Exchange Servers|Allow ACE|Desc|Change Password <br><br> Reset Password on Next Logon|`/ user`|
|Organization Management|Allow ACE|All|Read Permissions <br><br> List Contents <br><br> Read Property||
|Organization Management|Allow ACE|Desc|Write Property|`/ msExchSystemMailbox`|
|Organization Management|Allow ACE|All|Create Child <br><br> Delete Child|`/ msExchSystemMailbox`|
|Organization Management|Allow ACE|Desc|Write Property|`/ user`|
|Organization Management|Allow ACE|All|Create Child <br><br> Delete Child|`/ user`|
|Organization Management|Allow ACE|Desc|Read Property <br><br> Write Property|`mail / publicFolder`|
|Organization Management|Allow ACE|Desc|Read Property <br><br> Write Property|`displayNamePrintable / publicFolder`|
|Organization Management|Allow ACE|Desc|Read Property <br><br> Write Property|`displayName / publicFolder`|
|Organization Management|Allow ACE|Desc|Read Property <br><br> Write Property|`textEncodedORAddress / publicFolder`|
|Organization Management|Allow ACE|Desc|Read Property <br><br> Write Property|`proxyAddresses / publicFolder`|
|Organization Management|Allow ACE|Desc|Read Property <br><br> Write Property|`cn / publicFolder`|
|Organization Management|Allow ACE|Desc|Read Property <br><br> Write Property|`showInAddressBook / publicFolder`|
|Organization Management|Allow ACE|Desc|Read Property <br><br> Write Property|`Exchange Information / publicFolder`|
|Organization Management|Allow ACE|Desc|Read Property <br><br> Write Property|legacyExchangeDN / publicFolder|
|Organization Management|Allow ACE|Desc|Read Property <br><br> Write Property|`Exchange Personal Information / publicFolder`|
|Organization Management|Allow ACE|Desc|Read Property <br><br> Write Property|`msDSPhoneticDisplayName / publicFolder`|
|Organization Management|Allow ACE|Desc|Read Property <br><br> Write Property|`msExchPFContacts / publicFolder`|
|Organization Management|Allow ACE|Desc|Read Property <br><br> Write Property|`garbageCollPeriod / publicFolder`|
|Organization Management|Allow ACE|Desc|Read Property <br><br> Write Property|`name / publicFolder`|
|Organization Management|Allow ACE|Desc|Read Property <br><br> Write Property|`msExchPublicDelegates / publicFolder`|
|Public Folder Management|Allow ACE|All|Read Permissions <br><br> List Contents <br><br> Read Property||
|Public Folder Management|Allow ACE|Desc|Read Property <br><br> Write Property|`mail / publicFolder`|
|Public Folder Management|Allow ACE|Desc|Read Property <br><br> Write Property|`displayNamePrintable / publicFolder`|
|Public Folder Management|Allow ACE|Desc|Read Property <br><br> Write Property|`displayName / publicFolder`|
|Public Folder Management|Allow ACE|Desc|Read Property <br><br> Write Property|`textEncodedORAddress / publicFolder`|
|Public Folder Management|Allow ACE|Desc|Read Property <br><br> Write Property|`proxyAddresses / publicFolder`|
|Public Folder Management|Allow ACE|Desc|Read Property <br><br> Write Property|`cn / publicFolder`|
|Public Folder Management|Allow ACE|Desc|Read Property <br><br> Write Property|`showInAddressBook / publicFolder`|
|Public Folder Management|Allow ACE|Desc|Read Property <br><br> Write Property|`Exchange Information / publicFolder`|
|Public Folder Management|Allow ACE|Desc|Read Property <br><br> Write Property|`legacyExchangeDN / publicFolder`|
|Public Folder Management|Allow ACE|Desc|Read Property <br><br> Write Property|`Exchange Personal Information / publicFolder`|
|Public Folder Management|Allow ACE|Desc|Read Property <br><br> Write Property|`msDSPhoneticDisplayName / publicFolder`|
|Public Folder Management|Allow ACE|Desc|Read Property <br><br> Write Property|`msExchPFContacts / publicFolder`|
|Public Folder Management|Allow ACE|Desc|Read Property <br><br> Write Property|`garbageCollPeriod / publicFolder`|
|Public Folder Management|Allow ACE|Desc|Read Property <br><br> Write Property|`name / publicFolder`|
|Public Folder Management|Allow ACE|Desc|Read Property <br><br> Write Property|`msExchPublicDelegates / publicFolder`|
|Exchange Trusted Subsystem|Allow ACE|All|Read Permissions <br><br> List Contents <br><br> Read Property||
|Exchange Trusted Subsystem|Allow ACE|Desc|Read Property <br><br> Write Property|`mail / publicFolder`|
|Exchange Trusted Subsystem|Allow ACE|Desc|Read Property <br><br> Write Property|`displayNamePrintable / publicFolder`|
|Exchange Trusted Subsystem|Allow ACE|Desc|Read Property <br><br> Write Property|`displayName / publicFolder`|
|Exchange Trusted Subsystem|Allow ACE|Desc|Read Property <br><br> Write Property|`textEncodedORAddress / publicFolder`|
|Exchange Trusted Subsystem|Allow ACE|Desc|Read Property <br><br> Write Property|`proxyAddresses / publicFolder`|
|Exchange Trusted Subsystem|Allow ACE|Desc|Read Property <br><br> Write Property|`cn / publicFolder`|
|Exchange Trusted Subsystem|Allow ACE|Desc|Read Property <br><br> Write Property|`showInAddressBook / publicFolder`|
|Exchange Trusted Subsystem|Allow ACE|Desc|Read Property <br><br> Write Property|`Exchange Information / publicFolder`|
|Exchange Trusted Subsystem|Allow ACE|Desc|Read Property <br><br> Write Property|`legacyExchangeDN / publicFolder`|
|Exchange Trusted Subsystem|Allow ACE|Desc|Read Property <br><br> Write Property|`Exchange Personal Information / publicFolder`|
|Exchange Trusted Subsystem|Allow ACE|Desc|Read Property <br><br> Write Property|`msDSPhoneticDisplayName / publicFolder`|
|Exchange Trusted Subsystem|Allow ACE|Desc|Read Property <br><br> Write Property|`msExchPFContacts / publicFolder`|
|Exchange Trusted Subsystem|Allow ACE|Desc|Read Property <br><br> Write Property|`garbageCollPeriod / publicFolder`|
|Exchange Trusted Subsystem|Allow ACE|Desc|Read Property <br><br> Write Property|`name / publicFolder`|
|Exchange Trusted Subsystem|Allow ACE|Desc|Read Property <br><br> Write Property|`msExchPublicDelegates / publicFolder`|

### Distinguished name of the object: CN=Exchange Install Domain Servers,CN=Microsoft Exchange System Objects,DC=\<domain\>

|Account|ACE type|Inheritance|Permissions|On property/ Applies to|
|---|---|---|---|---|
|Organization Management|Allow ACE|All|Full Control||

## Server Role Installation

During installation of the Client Access and Mailbox server roles, Setup adds the Organization Management USG to the administrator security group on the local computer so that members of the management role group named Organization Management can manage the server.

The following permissions table shows the permissions set when you install the Client Access or Mailbox server roles.

### Distinguished name of the object: CN=\<server\>,CN=Servers,CN=\<admin group\>,CN=Administrative Groups,CN=\<organization\>

|Account|ACE type|Inheritance|Permissions|On property/ Applies to|Comments|
|---|---|---|---|---|---|
|MACHINE$|Allow ACE|All|Read Permissions <br><br> List Contents <br><br> Read Property <br><br> List Object|||
|MACHINE$|Allow ACE|None|Write Property|`msExchServerSite` <br><br> `msExchEdgeSyncCredential`||
|Exchange Servers|Allow ACE|All|Store Transport Access <br><br> Store Constrained Delegation <br><br> Store Read Only Access <br><br> Store Read and Write Access||Extended rights|
|NT AUTHORITY\NETWORK|Allow ACE|All|Exchange Web Services Token Serialization||Extended right <br><br> Only granted on Mailbox server role objects.|
|NT AUTHORITY\NETWORK|Allow ACE|All|Read Permissions <br><br> List Contents <br><br> Read Property <br><br> List Object|||
|Local System|Allow ACE|All|Read Permissions <br><br> List Contents <br><br> Read Property <br><br> List Object|||
|Delegated Setup|Allow ACE|All|Full Control|||
|Delegated Setup|Deny ACE|All|Create Child <br><br> Delete Child|`/ msExchPublicMDB`||
|Authenticated Users|Allow ACE|All|Read Property|||
|Delegated Setup|Deny ACE|All|Receive As <br><br> Send As||Extended right|

## Database Availability Groups

The permissions tables in this section show the permissions set with regards to the database availability groups and its members.

### Distinguished name of the object: CN=\<DAGName\>,CN=Database Availability Groups,CN=\<admin group\>,CN=Administrative Groups,CN=\<organization\>

|Account|ACE type|Inheritance|Permissions|On property/ Applies to|
|---|---|---|---|---|
|Authenticated Users|Allow ACE|None|Read Property||

## Edge Transport

If you install an Edge Transport server and establish an Edge Subscription with the Exchange organization, the permissions in the following permissions table are set when the Edge Transport server is instantiated into the organization.

### Distinguished name of the object in Edge Transport: CN=\<server\>,CN=Servers,CN=\<admin group\>,CN=Administrative Groups,CN=\<organization\>

|Account|ACE type|Inheritance|Permissions|On property/ Applies to|Comments|
|---|---|---|---|---|---|
|Exchange Servers|Allow ACE|All|Write Property|||
|Authenticated Users|Allow ACE|None|Read Properties||ACE is defined in schema for `msExchExchangeServer` class objects `defaultSecurityDescriptor`.|

## Mailbox Server Installation

During installation of the first Mailbox server, the following containers are created, if they do not already exist. The following permissions table shows the permissions that are applied.

### Distinguished name of the object: CN=Availability Configuration,CN=\<organization\>

|Account|ACE type|Inheritance|Permissions|On property/ Applies to|Comments|
|---|---|---|---|---|---|
|Exchange Servers|Allow ACE|Desc|Read Property|`msExchAvailabilityUserPassword / msExchAvailabilityAddressSpaceObjects`|Extended right|

### Distinguished name of the object: CN=Default \<Server\>,CN=SMTP Receive Connectors,CN=Protocols,CN=\<Server\>,CN=Servers,CN=\<admin group\>,CN=\<organization\>

|Account|ACE type|Inheritance|Permissions|On property/ Applies to|Comments|
|---|---|---|---|---|---|
|ExchangeLegacyInterop|Deny ACE|All|Accept Forest Headers|||
|ExchangeLegacyInterop|Deny ACE|All|Accept Organization Headers|||
|Exchange Servers|Allow ACE|All|Accept Any Sender|||
|ExchangeLegacyInterop|Allow ACE|All|Accept Any Sender|||
|S-1-9-1419165041-1139599005-3936102811-1022490595-21|Allow ACE|All|Accept Any Sender||This is the well-known security identifier (SID) for Mailbox servers.|
|S-1-9-1419165041-1139599005-3936102811-1022490595-22|Allow ACE|All|Accept Any Sender||This is the well-known SID for Edge Transport servers.|
|S-1-9-1419165041-1139599005-3936102811-1022490595-23|Allow ACE|All|Accept Any Sender||This is the well-known SID for externally secured servers.|
|Exchange Servers|Allow ACE|All|Accept EXCH50|||
|ExchangeLegacyInterop|Allow ACE|All|Accept EXCH50|||
|S-1-9-1419165041-1139599005-3936102811-1022490595-21|Allow ACE|All|Accept EXCH50||This is the well-known SID for Mailbox servers.|
|S-1-9-1419165041-1139599005-3936102811-1022490595-22|Allow ACE|All|Accept EXCH50||This is the well-known SID for Edge Transport servers.|
|S-1-9-1419165041-1139599005-3936102811-1022490595-23|Allow ACE|All|Accept EXCH50||This is the well-known SID for externally secured servers.|
|Exchange Servers|Allow ACE|All|Submit Messages to any Recipient|||
|ExchangeLegacyInterop|Allow ACE|All|Submit Messages to any Recipient|||
|S-1-9-1419165041-1139599005-3936102811-1022490595-21|Allow ACE|All|Submit Messages to any Recipient||This is the well-known SID for Mailbox servers.|
|S-1-9-1419165041-1139599005-3936102811-1022490595-22|Allow ACE|All|Submit Messages to any Recipient||This is the well-known SID for Edge Transport servers.|
|S-1-9-1419165041-1139599005-3936102811-1022490595-23|Allow ACE|All|Submit Messages to any Recipient||This is the well-known SID for externally secured servers.|
|Exchange Servers|Allow ACE|All|Accept XShadow|||
|S-1-9-1419165041-1139599005-3936102811-1022490595-22|Allow ACE|All|Accept XShadow||This is the well-known SID for Edge Transport servers.|
|Exchange Servers|Allow ACE|All|Accept Routing Headers|||
|ExchangeLegacyInterop|Allow ACE|All|Accept Routing Headers|||
|S-1-9-1419165041-1139599005-3936102811-1022490595-21|Allow ACE|All|Accept Routing Headers||This is the well-known SID for Mailbox servers.|
|S-1-9-1419165041-1139599005-3936102811-1022490595-22|Allow ACE|All|Accept Routing Headers||This is the well-known SID for Edge Transport servers.|
|S-1-9-1419165041-1139599005-3936102811-1022490595-23|Allow ACE|All|Accept Routing Headers||This is the well-known SID for externally secured servers.|
|Exchange Servers|Allow ACE|All|Accept XSessionParams|||
|S-1-9-1419165041-1139599005-3936102811-1022490595-21|Allow ACE|All|Accept XSessionParams||This is the well-known SID for Mailbox servers.|
|S-1-9-1419165041-1139599005-3936102811-1022490595-22|Allow ACE|All|Accept XSessionParams||This is the well-known SID for Mailbox servers.|
|Exchange Servers|Allow ACE|All|Accept Forest Headers|||
|S-1-9-1419165041-1139599005-3936102811-1022490595-21|Allow ACE|All|Accept Forest Headers||This is the well-known SID for Mailbox servers.|
|S-1-9-1419165041-1139599005-3936102811-1022490595-22|Allow ACE|All|Accept Forest Headers||This is the well-known SID for Edge Transport servers.|
|Exchange Servers|Allow ACE|All|Accept xAttr|||
|S-1-9-1419165041-1139599005-3936102811-1022490595-21|Allow ACE|All|Accept xAttr||This is the well-known SID for Mailbox servers.|
|S-1-9-1419165041-1139599005-3936102811-1022490595-22|Allow ACE|All|Accept xAttr||This is the well-known SID for Edge Transport servers.|
|Exchange Servers|Allow ACE|All|Accept XProxyFrom|||
|S-1-9-1419165041-1139599005-3936102811-1022490595-21|Allow ACE|All|Accept Forest XProxyFrom||This is the well-known SID for Mailbox servers.|
|S-1-9-1419165041-1139599005-3936102811-1022490595-22|Allow ACE|All|Accept Forest XProxyFrom||This is the well-known SID for Edge Transport servers.|
|Exchange Servers|Allow ACE|All|Accept XSysProbe|||
|S-1-9-1419165041-1139599005-3936102811-1022490595-21|Allow ACE|All|Accept Forest XSysProbe||This is the well-known SID for Mailbox servers.|
|S-1-9-1419165041-1139599005-3936102811-1022490595-22|Allow ACE|All|Accept Forest XSysProbe||This is the well-known SID for Edge Transport servers.|
|Exchange Servers|Allow ACE|All|Send XMessageContext Extended Properties|||
|S-1-9-1419165041-1139599005-3936102811-1022490595-21|Allow ACE|All|Send XMessageContext Extended Properties||This is the well-known SID for Mailbox servers.|
|S-1-9-1419165041-1139599005-3936102811-1022490595-22|Allow ACE|All|Send XMessageContext Extended Properties||This is the well-known SID for Edge Transport servers.|
|Exchange Servers|Allow ACE|All|Send XMessageContext Fast Index|||
|S-1-9-1419165041-1139599005-3936102811-1022490595-21|Allow ACE|All|Send XMessageContext Fast Index||This is the well-known SID for Mailbox servers.|
|S-1-9-1419165041-1139599005-3936102811-1022490595-22|Allow ACE|All|Send XMessageContext Fast Index||This is the well-known SID for Edge Transport servers.|
|Exchange Servers|Allow ACE|All|Send XMessageContext AD Recipient Cache|||
|S-1-9-1419165041-1139599005-3936102811-1022490595-21|Allow ACE|All|Send XMessageContext AD Recipient Cache||This is the well-known SID for Mailbox servers.|
|S-1-9-1419165041-1139599005-3936102811-1022490595-22|Allow ACE|All|Send XMessageContext AD Recipient Cache||This is the well-known SID for Edge Transport servers.|
|Exchange Servers|Allow ACE|All|Accept Authentication Flag|||
|ExchangeLegacyInterop|Allow ACE|All|Accept Authentication Flag|||
|S-1-9-1419165041-1139599005-3936102811-1022490595-21|Allow ACE|All|Accept Authentication Flag||This is the well-known SID for Mailbox servers.|
|S-1-9-1419165041-1139599005-3936102811-1022490595-22|Allow ACE|All|Accept Authentication Flag||This is the well-known SID for Edge Transport servers.|
|S-1-9-1419165041-1139599005-3936102811-1022490595-23|Allow ACE|All|Accept Authentication Flag||This is the well-known SID for externally secured servers.|
|Exchange Servers|Allow ACE|All|Bypass Anti-Spam|||
|ExchangeLegacyInterop|Allow ACE|All|Bypass Anti-Spam|||
|S-1-9-1419165041-1139599005-3936102811-1022490595-21|Allow ACE|All|Bypass Anti-Spam||This is the well-known SID for Mailbox servers.|
|S-1-9-1419165041-1139599005-3936102811-1022490595-22|Allow ACE|All|Bypass Anti-Spam||This is the well-known SID for Edge Transport servers.|
|S-1-9-1419165041-1139599005-3936102811-1022490595-23|Allow ACE|All|Bypass Anti-Spam||This is the well-known SID for externally secured servers.|
|Exchange Servers|Allow ACE|All|Bypass Message Size Limit|||
|ExchangeLegacyInterop|Allow ACE|All|Bypass Message Size Limit|||
|S-1-9-1419165041-1139599005-3936102811-1022490595-21|Allow ACE|All|Bypass Message Size Limit||This is the well-known SID for Mailbox servers.|
|S-1-9-1419165041-1139599005-3936102811-1022490595-22|Allow ACE|All|Bypass Message Size Limit||This is the well-known SID for Edge Transport servers.|
|S-1-9-1419165041-1139599005-3936102811-1022490595-23|Allow ACE|All|Bypass Message Size Limit||This is the well-known SID for externally secured servers.|
|Exchange Servers|Allow ACE|All|Accept Organization Headers|||
|S-1-9-1419165041-1139599005-3936102811-1022490595-21|Allow ACE|All|Accept Organization Headers||This is the well-known SID for Mailbox servers.|
|S-1-9-1419165041-1139599005-3936102811-1022490595-22|Allow ACE|All|Accept Organization Headers||This is the well-known SID for Edge Transport servers.|
|Exchange Servers|Allow ACE|All|Submit Messages to Server|||
|ExchangeLegacyInterop|Allow ACE|All|Submit Messages to Server|||
|S-1-9-1419165041-1139599005-3936102811-1022490595-21|Allow ACE|All|Submit Messages to Server||This is the well-known SID for Mailbox servers.|
|S-1-9-1419165041-1139599005-3936102811-1022490595-22|Allow ACE|All|Submit Messages to Server||This is the well-known SID for Edge Transport servers.|
|S-1-9-1419165041-1139599005-3936102811-1022490595-23|Allow ACE|All|Submit Messages to Server||This is the well-known SID for externally secured servers.|
|Exchange Servers|Allow ACE|All|Accept Authoritative Domain Sender|||
|ExchangeLegacyInterop|Allow ACE|All|Accept Authoritative Domain Sender|||
|S-1-9-1419165041-1139599005-3936102811-1022490595-21|Allow ACE|All|Accept Authoritative Domain Sender||This is the well-known SID for Mailbox servers.|
|S-1-9-1419165041-1139599005-3936102811-1022490595-22|Allow ACE|All|Accept Authoritative Domain Sender||This is the well-known SID for Edge Transport servers.|
|S-1-9-1419165041-1139599005-3936102811-1022490595-23|Allow ACE|All|Accept Authoritative Domain Sender||This is the well-known SID for externally secured servers.|
|Authenticated Users|Allow ACE|All|Submit Messages to any Recipient|||
|Authenticated Users|Allow ACE|All|Accept Routing Headers|||
|Authenticated Users|Allow ACE|All|Bypass Anti-Spam|||
|Authenticated Users|Allow ACE|All|Submit Messages to Server|||

### Distinguished name of the object: CN=Client \<Server\>,CN=SMTP Receive Connectors,CN=Protocols,CN=\<Server\>,CN=Servers,CN=\<admin group\>,CN=\<organization\>

|Account|ACE type|Inheritance|Permissions|On property/ Applies to|Comments|
|---|---|---|---|---|---|
|Authenticated Users|Allow ACE|All|Submit Messages to any Recipient|||
|Authenticated Users|Allow ACE|All|Accept Routing Headers|||
|Authenticated Users|Allow ACE|All|Bypass Anti-Spam|||
|Authenticated Users|Allow ACE|All|Submit Messages to Server|||
|Exchange Servers|Allow ACE|All|Accept XSessionParams|||
|S-1-9-1419165041-1139599005-3936102811-1022490595-21|Allow ACE|All|Accept XSessionParams||This is the well-known SID for Mailbox servers.|
|S-1-9-1419165041-1139599005-3936102811-1022490595-22|Allow ACE|All|Accept XSessionParams||This is the well-known SID for Mailbox servers.|
|Exchange Servers|Allow ACE|All|Accept Any Sender|||
|S-1-9-1419165041-1139599005-3936102811-1022490595-21|Allow ACE|All|Accept Any Sender||This is the well-known security identifier (SID) for Mailbox servers.|
|S-1-9-1419165041-1139599005-3936102811-1022490595-22|Allow ACE|All|Accept Any Sender||This is the well-known SID for Edge Transport servers.|
|S-1-9-1419165041-1139599005-3936102811-1022490595-23|Allow ACE|All|Accept Any Sender||This is the well-known SID for externally secured servers.|
|S-1-9-1419165041-1139599005-3936102811-1022490595-21|Allow ACE|All|Accept Exch50||This is the well-known SID for Mailbox servers.|
|S-1-9-1419165041-1139599005-3936102811-1022490595-22|Allow ACE|All|Accept Exch50||This is the well-known SID for Edge Transport servers.|
|S-1-9-1419165041-1139599005-3936102811-1022490595-23|Allow ACE|All|Accept Exch50||This is the well-known SID for externally secured servers.|
|Exchange Servers|Allow ACE|All|Accept Exch50|||
|Exchange Servers|Allow ACE|All|Submit Messages to any Recipient|||
|ExchangeLegacyInterop|Allow ACE|All|Submit Messages to any Recipient|||
|S-1-9-1419165041-1139599005-3936102811-1022490595-21|Allow ACE|All|Submit Messages to any Recipient||This is the well-known SID for Mailbox servers.|
|S-1-9-1419165041-1139599005-3936102811-1022490595-22|Allow ACE|All|Submit Messages to any Recipient||This is the well-known SID for Edge Transport servers.|
|S-1-9-1419165041-1139599005-3936102811-1022490595-23|Allow ACE|All|Submit Messages to any Recipient||This is the well-known SID for externally secured servers.|
|Exchange Servers|Allow ACE|All|Accept XShadow|||
|S-1-9-1419165041-1139599005-3936102811-1022490595-22|Allow ACE|All|Accept XShadow||This is the well-known SID for Edge Transport servers.|
|Exchange Servers|Allow ACE|All|Accept Routing Headers|||
|ExchangeLegacyInterop|Allow ACE|All|Accept Routing Headers|||
|S-1-9-1419165041-1139599005-3936102811-1022490595-21|Allow ACE|All|Accept Routing Headers||This is the well-known SID for Mailbox servers.|
|S-1-9-1419165041-1139599005-3936102811-1022490595-22|Allow ACE|All|Accept Routing Headers||This is the well-known SID for Edge Transport servers.|
|S-1-9-1419165041-1139599005-3936102811-1022490595-23|Allow ACE|All|Accept Routing Headers||This is the well-known SID for externally secured servers.|
|Exchange Servers|Allow ACE|All|Accept Forest Headers|||
|S-1-9-1419165041-1139599005-3936102811-1022490595-21|Allow ACE|All|Accept Forest Headers||This is the well-known SID for Mailbox servers.|
|S-1-9-1419165041-1139599005-3936102811-1022490595-22|Allow ACE|All|Accept Forest Headers||This is the well-known SID for Edge Transport servers.|
|Exchange Servers|Allow ACE|All|Accept xAttr|||
|S-1-9-1419165041-1139599005-3936102811-1022490595-21|Allow ACE|All|Accept xAttr||This is the well-known SID for Mailbox servers.|
|S-1-9-1419165041-1139599005-3936102811-1022490595-22|Allow ACE|All|Accept xAttr||This is the well-known SID for Edge Transport servers.|
|Exchange Servers|Allow ACE|All|Accept XProxyFrom|||
|S-1-9-1419165041-1139599005-3936102811-1022490595-21|Allow ACE|All|Accept Forest XProxyFrom||This is the well-known SID for Mailbox servers.|
|S-1-9-1419165041-1139599005-3936102811-1022490595-22|Allow ACE|All|Accept Forest XProxyFrom||This is the well-known SID for Edge Transport servers.|
|Exchange Servers|Allow ACE|All|Accept Authentication Flag|||
|S-1-9-1419165041-1139599005-3936102811-1022490595-21|Allow ACE|All|Accept Authentication Flag||This is the well-known SID for Mailbox servers.|
|S-1-9-1419165041-1139599005-3936102811-1022490595-22|Allow ACE|All|Accept Authentication Flag||This is the well-known SID for Edge Transport servers.|
|S-1-9-1419165041-1139599005-3936102811-1022490595-23|Allow ACE|All|Accept Authentication Flag||This is the well-known SID for externally secured servers.|
|Exchange Servers|Allow ACE|All|Accept XSysProbe|||
|S-1-9-1419165041-1139599005-3936102811-1022490595-21|Allow ACE|All|Accept Forest XSysProbe||This is the well-known SID for Mailbox servers.|
|S-1-9-1419165041-1139599005-3936102811-1022490595-22|Allow ACE|All|Accept Forest XSysProbe||This is the well-known SID for Edge Transport servers.|
|S-1-9-1419165041-1139599005-3936102811-1022490595-23|Allow ACE|All|Accept Authentication Flag||This is the well-known SID for externally secured servers.|
|Exchange Servers|Allow ACE|All|Bypass Anti-Spam|||
|S-1-9-1419165041-1139599005-3936102811-1022490595-21|Allow ACE|All|Bypass Anti-Spam||This is the well-known SID for Mailbox servers.|
|S-1-9-1419165041-1139599005-3936102811-1022490595-22|Allow ACE|All|Bypass Anti-Spam||This is the well-known SID for Edge Transport servers.|
|S-1-9-1419165041-1139599005-3936102811-1022490595-23|Allow ACE|All|Bypass Anti-Spam||This is the well-known SID for externally secured servers.|
|Exchange Servers|Allow ACE|All|Send XMessageContext Extended Properties|||
|S-1-9-1419165041-1139599005-3936102811-1022490595-21|Allow ACE|All|Send XMessageContext Extended Properties||This is the well-known SID for Mailbox servers.|
|S-1-9-1419165041-1139599005-3936102811-1022490595-22|Allow ACE|All|Send XMessageContext Extended Properties||This is the well-known SID for Edge Transport servers.|
|Exchange Servers|Allow ACE|All|Send XMessageContext Fast Index|||
|S-1-9-1419165041-1139599005-3936102811-1022490595-21|Allow ACE|All|Send XMessageContext Fast Index||This is the well-known SID for Mailbox servers.|
|S-1-9-1419165041-1139599005-3936102811-1022490595-22|Allow ACE|All|Send XMessageContext Fast Index||This is the well-known SID for Edge Transport servers.|
|Exchange Servers|Allow ACE|All|Bypass Message Size Limit|||
|S-1-9-1419165041-1139599005-3936102811-1022490595-21|Allow ACE|All|Bypass Message Size Limit||This is the well-known SID for Mailbox servers.|
|S-1-9-1419165041-1139599005-3936102811-1022490595-22|Allow ACE|All|Bypass Message Size Limit||This is the well-known SID for Edge Transport servers.|
|S-1-9-1419165041-1139599005-3936102811-1022490595-23|Allow ACE|All|Bypass Message Size Limit||This is the well-known SID for externally secured servers.|
|Exchange Servers|Allow ACE|All|Accept Organization Headers|||
|S-1-9-1419165041-1139599005-3936102811-1022490595-21|Allow ACE|All|Accept Organization Headers||This is the well-known SID for Mailbox servers.|
|S-1-9-1419165041-1139599005-3936102811-1022490595-22|Allow ACE|All|Accept Organization Headers||This is the well-known SID for Edge Transport servers.|
|Exchange Servers|Allow ACE|All|Send XMessageContext AD Recipient Cache|||
|S-1-9-1419165041-1139599005-3936102811-1022490595-21|Allow ACE|All|Send XMessageContext AD Recipient Cache||This is the well-known SID for Mailbox servers.|
|S-1-9-1419165041-1139599005-3936102811-1022490595-22|Allow ACE|All|Send XMessageContext AD Recipient Cache||This is the well-known SID for Edge Transport servers.|
|Exchange Servers|Allow ACE|All|Submit Messages to Server|||
|S-1-9-1419165041-1139599005-3936102811-1022490595-21|Allow ACE|All|Submit Messages to Server||This is the well-known SID for Mailbox servers.|
|S-1-9-1419165041-1139599005-3936102811-1022490595-22|Allow ACE|All|Submit Messages to Server||This is the well-known SID for Edge Transport servers.|
|S-1-9-1419165041-1139599005-3936102811-1022490595-23|Allow ACE|All|Submit Messages to Server||This is the well-known SID for externally secured servers.|
|Exchange Servers|Allow ACE|All|Accept Authoritative Domain Sender|||
|S-1-9-1419165041-1139599005-3936102811-1022490595-21|Allow ACE|All|Accept Authoritative Domain Sender||This is the well-known SID for Mailbox servers.|
|S-1-9-1419165041-1139599005-3936102811-1022490595-22|Allow ACE|All|Accept Authoritative Domain Sender||This is the well-known SID for Edge Transport servers.|
|S-1-9-1419165041-1139599005-3936102811-1022490595-23|Allow ACE|All|Accept Authoritative Domain Sender||This is the well-known SID for externally secured servers.|

## SMTP Send Connector Creation

The following table shows the permissions set when you create Send connectors.

### Distinguished name of the object: CN=\<Connector Name\>,CN=Connections,CN=\<routing group\>,CN=Routing Groups, CN=\<admin group\>,CN=\<organization\>

|Account|ACE type|Inheritance|Permissions|On property/ Applies to|Comments|
|---|---|---|---|---|---|
|NT AUTHORITY\ANONYMOUS LOGON|Allow ACE|All|Send Routing Headers|||
|Exchange Servers|Allow ACE|All|Send Organization Headers|||
|S-1-9-1419165041-1139599005-3936102811-1022490595-21|Allow ACE|All|Send Organization Headers||This is the well-known SID for Mailbox servers.|
|S-1-9-1419165041-1139599005-3936102811-1022490595-22|Allow ACE|All|Send Organization Headers||This is the well-known SID for Edge Transport servers.|
|Exchange Servers|Allow ACE|All|Send Forest Headers||This is the well-known SID for Mailbox servers.|
|S-1-9-1419165041-1139599005-3936102811-1022490595-21|Allow ACE|All|Send Forest Headers||This is the well-known SID for Mailbox servers.|
|S-1-9-1419165041-1139599005-3936102811-1022490595-22|Allow ACE|All|Send Forest Headers||This is the well-known SID for Edge Transport servers.|
|Exchange Servers|Allow ACE|All|Send XShadow|||
|S-1-9-1419165041-1139599005-3936102811-1022490595-21|Allow ACE|All|Send XShadow||This is the well-known SID for Mailbox servers.|
|S-1-9-1419165041-1139599005-3936102811-1022490595-22|Allow ACE|All|Send XShadow||This is the well-known SID for Edge Transport servers.|
|Exchange Servers|Allow ACE|All|Send Routing Headers|||
|S-1-9-1419165041-1139599005-3936102811-1022490595-10|Allow ACE|All|Send Routing Headers||This is the well-known SID for partner servers.|
|S-1-9-1419165041-1139599005-3936102811-1022490595-21|Allow ACE|All|Send Routing Headers||This is the well-known SID for Mailbox servers.|
|S-1-9-1419165041-1139599005-3936102811-1022490595-22|Allow ACE|All|Send Routing Headers||This is the well-known SID for Edge Transport servers.|
|S-1-9-1419165041-1139599005-3936102811-1022490595-23|Allow ACE|All|Send Routing Headers||This is the well-known SID for externally secured servers.|
|S-1-9-1419165041-1139599005-3936102811-1022490595-24|Allow ACE|All|Send Routing Headers||This is the well-known SID for Legacy Exchange Servers.|
|Exchange Servers|Allow ACE|All|Send Exch50|||
|S-1-9-1419165041-1139599005-3936102811-1022490595-21|Allow ACE|All|Send Exch50||This is the well-known SID for Mailbox servers.|
|S-1-9-1419165041-1139599005-3936102811-1022490595-22|Allow ACE|All|Send Exch50||This is the well-known SID for Edge Transport servers.|
|S-1-9-1419165041-1139599005-3936102811-1022490595-23|Allow ACE|All|Send Exch50||This is the well-known SID for externally secured servers.|
|S-1-9-1419165041-1139599005-3936102811-1022490595-24|Allow ACE|All|Send Exch50||This is the well-known SID for Legacy Exchange Servers.|
