---
title: 'Exchange 2013 Active Directory schema changes: Exchange 2013 Help'
TOCTitle: Exchange 2013 Active Directory schema changes
ms:assetid: 7e879e4e-1124-4a41-94d2-c64500beb24e
ms:mtpsurl: https://technet.microsoft.com/library/Bb738144(v=EXCHG.150)
ms:contentKeyID: 49289322
ms.reviewer:
ms.topic: article
description: Active Directory schema changes in Exchange Server 2013 
manager: serdars
ms.author: serdars
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# Exchange 2013 Active Directory schema changes

_**Applies to:** Exchange Server 2013_

Microsoft Exchange Server 2013 adds new and modifies existing Active Directory schema classes and attributes. This reference topic provides a summary of the Active Directory schema changes that are made when you install the release to manufacturing (RTM) version of Exchange 2013 or any of its cumulative updates or service packs. Refer to the .ldf files for more information about changes to the Active Directory schema. The .ldf files are located in the \\amd64\\Setup\\Data\\ directory in the Exchange installation files.

Exchange 2013 schema updates are cumulative. Each release includes all of the changes included in previous releases. This means that if you skip a release, you may still need to apply schema updates even if the release you're installing doesn't include its own changes. The following table gives examples of when your Active Directory will be updated, and when it's already up-to-date.

|Current Exchange 2013 release installed|New Exchange 2013 release being installed|Are schema updates required?|
|---|---|---|
|Service Pack 1|Cumulative Update 8 <br> through <br> Cumulative Update 21|**Yes**, schema updates are required. <br> You need to apply the CU5, CU6, and CU7 schema updates.|
|Cumulative Update 6|Cumulative Update 8 <br> through <br> Cumulative Update 21|**Yes**, schema updates are required. <br> You need to apply the CU7 schema updates.|
|Cumulative Update 7|Cumulative Update 8 <br> through <br> Cumulative Update 21|**No**, no schema updates are required. <br> No schema changes are made in CU7 through CU21.|

> [!NOTE]
> The Active Directory schema changes identified in this topic may not apply to all editions of an Exchange Server version.
>
> To verify that Active Directory has been successfully prepared, see the "How do you know this worked?" section in [Prepare Active Directory and domains](prepare-active-directory-and-domains-exchange-2013-help.md).

## Exchange 2013 CU23 Active Directory schema changes

No changes are made to the Active Directory schema in Exchange 2013 CU23.

## Exchange 2013 CU22 Active Directory schema changes

No changes are made to the Active Directory schema in Exchange 2013 CU22.

However, a reduction in Active Directory permissions is made: The "Allow" Access Control Entry (ACE) that grants the "Exchange Windows Permissions" group the "Write DACL" right to the "User" and "INetOrgPerson" inherited object types is updated to include the "Inherit Only" flag on the domain root object. For more information, see [KB 4490059](https://support.microsoft.com/help/4490059/using-shared-permissions-model-to-run-exchange-server).

## Exchange 2013 CU21 Active Directory schema changes

No changes are made to the Active Directory schema in Exchange 2013 CU21.

## Exchange 2013 CU20 Active Directory schema changes

No changes are made to the Active Directory schema in Exchange 2013 CU20.

## Exchange 2013 CU19 Active Directory schema changes

No changes are made to the Active Directory schema in Exchange 2013 CU19.

## Exchange 2013 CU18 Active Directory schema changes

No changes are made to the Active Directory schema in Exchange 2013 CU18.

## Exchange 2013 CU17 Active Directory schema changes

No changes are made to the Active Directory schema in Exchange 2013 CU17.

## Exchange 2013 CU16 Active Directory schema changes

No changes are made to the Active Directory schema in Exchange 2013 CU16.

## Exchange 2013 CU15 Active Directory schema changes

No changes are made to the Active Directory schema in Exchange 2013 CU15.

## Exchange 2013 CU14 Active Directory schema changes

No changes are made to the Active Directory schema in Exchange 2013 CU14.

## Exchange 2013 CU13 Active Directory schema changes

No changes are made to the Active Directory schema in Exchange 2013 CU13.

## Exchange 2013 CU12 Active Directory schema changes

No changes are made to the Active Directory schema in Exchange 2013 CU12.

## Exchange 2013 CU11 Active Directory schema changes

No changes are made to the Active Directory schema in Exchange 2013 CU11.

## Exchange 2013 CU10 Active Directory schema changes

No changes are made to the Active Directory schema in Exchange 2013 CU10.

## Exchange 2013 CU9 Active Directory schema changes

No changes are made to the Active Directory schema in Exchange 2013 CU9.

## Exchange 2013 CU8 Active Directory schema changes

No changes are made to the Active Directory schema in Exchange 2013 CU8.

## Exchange 2013 CU7 Active Directory schema changes

This section summarizes the changes that are made to the Active Directory schema when you install Exchange 2013 CU7. This section includes the following subsections:

- Classes modified by Exchange 2013 CU7
- Attributes added by Exchange 2013 CU7

## Classes modified by Exchange 2013 CU7

This section contains the classes modified in Exchange 2013 CU7.

|Class|Change|Attribute/Class|
|---|---|---|
|Mail-Recipient|add: mayContain|msExchStsRefreshTokensValidFrom|
|ms-Exch-Base-Class|add: mayContain|msExchMultiMailboxGUIDs|
|ms-Exch-Base-Class|add: mayContain|msExchMultiMailboxLocationsLink|
|Group|add: auxiliaryClass|msExchMailStorage|

## Attributes added by Exchange 2013 CU7

This section contains the attributes added in Exchange 2013 CU7.

- ms-Exch-Multi-Mailbox-GUID
- ms-Exch-Sts-Refresh-Tokens-Valid-From
- ms-Exch-Multi-Mailbox-Locations-Link

## Exchange 2013 CU6 Active Directory schema changes

This section summarizes the changes that are made to the Active Directory schema when you install Exchange 2013 CU6. This section includes the following subsections:

- Classes modified by Exchange 2013 CU6
- Attributes added by Exchange 2013 CU6
- Attributes modified by Exchange 2013 CU6

## Classes modified by Exchange 2013 CU6

This section contains the classes modified in Exchange 2013 CU6.

|Class|Change|Attribute/Class|
|---|---|---|
|Mail-Recipient|add: mayContain|msExchAuxMailboxParentObjectIdLink|
|Top|add: mayContain|msExchAuxMailboxParentObjectIdBL|

## Attributes added by Exchange 2013 CU6

This section contains the attributes added in Exchange 2013 CU6.

- ms-Exch-Aux-Mailbox-Parent-Object-Id-Link
- ms-Exch-Aux-Mailbox-Parent-Object-Id-BL

## Attributes modified by Exchange 2013 CU6

This section contains the attributes modified in Exchange 2013 CU6.

|Attribute|Change|Value|
|---|---|---|
|ms-Exch-Smtp-TLS-Certificate|replace: rangeUpper|1024|

## Exchange 2013 CU5 Active Directory schema changes

This section summarizes the changes that are made to the Active Directory schema when you install Exchange 2013 CU5. This section includes the following subsections:

- Classes added by Exchange 2013 CU5
- Attributes added by Exchange 2013 CU5
- Attributes modified by Exchange 2013 CU5

## Classes added by Exchange 2013 CU5

This section contains the classes added in Exchange 2013 CU5.

|Class|Change|
|---|---|
|ms-Exch-Unified-Policy|ntdsSchemaAdd|
|ms-Exch-Unified-Rule|ntdsSchemaAdd|

## Attributes added by Exchange 2013 CU5

This section contains the attributes added in Exchange 2013 CU5.

- ms-Exch-UG-Member-Link
- ms-Exch-UG-Member-BL

## Attributes modified by Exchange 2013 CU5

This section contains the attributes modified in Exchange 2013 CU5.

|Attribute|Change|Value|
|---|---|---|
|ms-Exch-Smtp-Receive-Tls-Certificate-Name|Replace: rangeUpper|1024|
|Mail-Recipient|Replace: mayContain|msExchUGMemberLink|
|Top|Replace: mayContain|msExchUGMemberBL|

## Exchange 2013 SP1 Active Directory schema changes

This section summarizes the changes that are made to the Active Directory schema when you install Exchange 2013 Service Pack 1 (SP1). This section includes the following subsections:

- Classes added by Exchange 2013 SP1
- Classes modified by Exchange 2013 SP1
- Attributes added by Exchange 2013 SP1
- Global catalog attributes added by Exchange 2013 SP1
- Attributes modified by Exchange 2013 SP1

## Classes added by Exchange 2013 SP1

This section contains the classes added in Exchange 2013 SP1.

|Class|Change|
|---|---|
|ms-Exch-Intra-Organization-Connector|ntdsSchemaModify|
|ms-Exch-Client-Access-Rule|ntdsSchemaModify|

## Classes modified by Exchange 2013 SP1

This section contains the attributes added in Exchange 2013 SP1.

|Class|Change|Attribute/Class|
|---|---|---|
|ms-Exch-Mail-Storage|add: mayContain|msExchMailboxContainerGuid|
|ms-Exch-Mail-Storage|add: mayContain|msExchUnifiedMailbox|
|ms-Exch-OAB|add: mayContain|msExchOABGeneratingMailboxLink|
|Top|add: mayContain|msExchOABGeneratingMailboxBL|

## Attributes added by Exchange 2013 SP1

This section contains the attributes added in Exchange 2013 SP1.

- ms-Exch-OAB-Generating-Mailbox-Link
- ms-Exch-OAB-Generating-Mailbox-BL

## Global catalog attributes added by Exchange 2013 SP1

The following global catalog attributes are added by Exchange 2013 SP1:

- ms-Exch-Mailbox-Container-Guid
- ms-Exch-Unified-Mailbox

## Attributes modified by Exchange 2013 SP1

This section contains the attributes modified in Exchange 2013 SP1.

|Attribute|Change|Value|
|---|---|---|
|Ms-exch-schema-version-pt|rangeUpper|15292|

## Exchange 2013 CU3 Active Directory schema changes

This section summarizes the changes that are made to the Active Directory schema when you install Exchange 2013 CU3. This section includes the following subsections:

- Classes added by Exchange 2013 CU3
- Attributes added by Exchange 2013 CU3
- Attributes modified by Exchange 2013 CU3

## Classes added by Exchange 2013 CU3

This section contains the classes added in Exchange 2013 CU3.

|Class|Change|
|---|---|
|msExchThrottlingPolicy|ntdsSchemaModify|

## Attributes added by Exchange 2013 CU3

This section contains the attributes added in Exchange 2013 CU3.

- ms-Exch-Encryption-Throttling-Policy-State-Ex

## Attributes modified by Exchange 2013 CU3

This section contains the attributes modified in Exchange 2013 CU3.

|Attribute|Change|Value|
|---|---|---|
|ms-Exch-Coexistence-Secure-Mail-Certificate-Thumbprintms-Exch-Sync-Cookie|rangeUpper|1024|

## Exchange 2013 CU2 Active Directory schema changes

This section summarizes the changes that are made to the Active Directory schema when you install Exchange 2013 CU2. This section includes the following subsections:

- Classes added by Exchange 2013 CU2
- Classes modified by Exchange 2013 CU2
- Attributes added by Exchange 2013 CU2
- Attributes modified by Exchange 2013 CU2

## Classes added by Exchange 2013 CU2

This section contains the classes added in Exchange 2013 CU2.

|Class|Change|
|---|---|
|ms-Exch-Config-Settings|ntdsSchemaAdd|
|ms-Exch-Encryption-Virtual-Directory|ntdsSchemaAdd|

## Classes modified by Exchange 2013 CU2

This section contains the classes modified in Exchange 2013 CU2.

|Class|Change|Attribute/Class|
|---|---|---|
|ms-Exch-Base-Class|Add:mayContain|msExchTenantCountry|
|ms-Exch-Base-Class|Add:mayContain|msExchConfigurationXML|
|ms-Exch-Account-Forest|Add:mayContain|msExchPartnerId|

## Attributes added by Exchange 2013 CU2

This section contains the attributes added in Exchange 2013 CU2.

- ms-Exch-Tenant-Country

## Attributes modified by Exchange 2013 CU2

This section contains the attributes modified in Exchange 2013 CU2.

|Attribute|Change|Value|
|---|---|---|
|ms-Exch-Sync-Cookie|rangeUpper|262144|
|ms-Exch-Schema-Version-Pt|rangeUpper|15281|

## Object IDs added by Exchange 2013 CU2

The following class object IDs are added when you install Exchange 2013 CU1:

- 1.2.840.113556.1.5.7000.62.50204
- 1.2.840.113556.1.5.7000.62.50205

The following attribute object IDs are added when you install Exchange 2013 CU1:

- 1.2.840.113556.1.4.7000.102.52130

## Exchange 2013 CU1 Active Directory schema changes

This section summarizes the changes that are made to the Active Directory schema when you install Exchange 2013 CU1. This section includes the following subsections:

- Classes modified by Exchange 2013 CU1
- Classes added by Exchange 2013 CU1
- Attributes modified by Exchange 2013 CU1
- Object IDs added by Exchange 2013 CU1
- Indexed attributes added by Exchange 2013 CU1
- Property sets modified by Exchange 2013 CU1
- Global catalog attributes added by Exchange 2013 CU1

## Classes modified by Exchange 2013 CU1

This section contains the classes modified in Exchange 2013 CU1.

|Class|Change|Attribute/Class|
|---|---|---|
|Exch-Configuration-Unit-Container|add:mayContain|msExchArchiveRelease|
|Exch-Configuration-Unit-Container|add:mayContain|msExchMailboxRelease|
|Exch-Exchange-Server|add:mayContain|msExchArchiveRelease|
|Exch-Exchange-Server|add:mayContain|msExchMailboxRelease|
|Exch-OAB|add:mayContain|msExchLastUpdateTime|
|Exch-Accepted-Domain|add:mayContain|msExchOfflineOrgIdHomeRealmRecord|
|Exch-Base-Class|add:mayContain|msExchCapabilityIdentifiers|
|Exch-Base-Class|add:mayContain|msExchObjectID|
|Exch-Base-Class|add:mayContain|msExchProvisioningTags|
|Exch-Organization-Container|add:mayContain|msExchMaxABP|
|Exch-Organization-Container|add:mayContain|msExchMaxOAB|
|Exch-Organization-Container|add:mayContain|pFContacts|
|Exch-Team-Mailbox-Provisioning-Policy|add:mayContain|msExchConfigurationXML|
|Exch-MDB-Availability-Group|add:mayContain|msExchEvictedMembersLink|
|Top|add:mayContain|msExchEvictedMembersBL|
|Exch-On-Premises-Organization|add:mayContain|msExchTrustedDomainLink|
|Exch-OWA-Mailbox-Policy|add:mayContain|msExchConfigurationXML|
|Exch-OWA-Virtual-Directory|add:mayContain|msExchConfigurationXML|

## Classes added by Exchange 2013 CU1

This section contains the classes modified in Exchange 2013 CU1.

|Class|Change|
|---|---|
|Exch-Mapi-Virtual-Directory|ntdsSchemaAdd|
|Exch-Push-Notifications-App|ntdsSchemaAdd|

## Attributes modified by Exchange 2013 CU1

This section contains the attributes modified in Exchange 2013 CU1.

|Class|Change|Attribute/Class|
|---|---|---|
|Exch-Mailflow-Policy-Transport-Rules-Template-Xml|rangeUpper|256000|
|Exch-Configuration-Unit-Container|rangeUpper|15254|

## Object IDs added by Exchange 2013 CU1

The following attribute object IDs are added when you install Exchange 2013 CU1:

- 1.2.840.113556.1.4.7000.102.52109
- 1.2.840.113556.1.4.7000.102.52110
- 1.2.840.113556.1.4.7000.102.52127
- 1.2.840.113556.1.4.7000.102.52126
- 1.2.840.113556.1.4.7000.102.52128
- 1.2.840.113556.1.4.7000.102.52129

The following class object IDs are added when you install Exchange 2013 CU1:

- 1.2.840.113556.1.5.7000.62.50202
- 1.2.840.113556.1.5.7000.62.50203

## Indexed attributes added by Exchange 2013 CU1

The following table lists the attributes that are added to the list of indexed attributes when you install Exchange 2013 CU1.

|Attribute|Search flag value|
|---|---|
|ms-Exch-Provisioning-Tags|1|

## Property sets modified by Exchange 2013 CU1

The following property sets are modified when you install Exchange 2013 CU1:

- Exchange-Information

## Global catalog attributes added by Exchange 2013 CU1

The following global catalog attributes are added by Exchange 2013 CU1:

- ms-Exch-Offline-OrgId-Home-Realm-Record
- ms-Exch-EvictedMembers-Link
- ms-Exch-EvictedMembers-BL

## Exchange 2013 RTM Active Directory schema changes

This section summarizes the changes that are made to the Active Directory schema when you install Exchange 2013 RTM. This section includes the following subsections:

- Classes modified by Exchange 2013 RTM
- Attributes modified by Exchange 2013 RTM
- Classes added by Exchange 2013 RTM
- Attributes added by Exchange 2013 RTM
- MAPI IDs added by Exchange 2013 RTM
- Extended rights added by Exchange 2013 RTM
- Object IDs added by Exchange 2013 RTM
- Indexed attributes added by Exchange 2013 RTM
- Global catalog attributes added by Exchange 2013 RTM

## Classes modified by Exchange 2013 RTM

This section contains the classes modified in Exchange 2013 RTM.

|Class|Change|Attribute/Class|
|---|---|---|
|Mail-Recipient|add:mayContain|msExchLocalizationFlags|
|Mail-Recipient|add:mayContain|msExchRoleGroupType|
|ms-Exch-Base-Class|add:mayContain|msExchDirsyncAuthorityMetadata|
|ms-Exch-Base-Class|add:mayContain|msExchDirsyncStatusAck|
|ms-Exch-Base-Class|add:mayContain|msExchEdgeSyncConfigFlags|
|ms-Exch-Base-Class|add:mayContain|msExchHABRootDepartmentLink|
|ms-Exch-Base-Class|add:mayContain|msExchDefaultPublicFolderMailbox|
|ms-Exch-Base-Class|add:mayContain|msExchForestModeFlag|
|ms-Exch-Configuration-Unit-Container|add:mayContain|msExchDirsyncStatus|
|ms-Exch-Configuration-Unit-Container|add:mayContain|msExchIsDirsyncStatusPending|
|ms-Exch-Mail-Storage|add:mayContain|msExchPreviousArchiveDatabase|
|ms-Exch-Configuration-Unit-Container|add:mayContain|msExchDirSyncServiceInstance|
|ms-Exch-Configuration-Unit-Container|add:mayContain|msExchOrganizationUpgradePolicyLink|
|ms-Exch-OWA-Mailbox-Policy|add:mayContain|msExchOWASetPhotoURL|
|ms-Exch-OWA-Virtual-Directory|add:mayContain|msExchOWASetPhotoURL|
|ms-Exch-Exchange-Server|add:mayContain|msExchWorkloadManagementPolicyLink|
|Mail-Recipient|add:mayContain|ms-DS-GeoCoordinates-Altitude|
|Mail-Recipient|add:mayContain|ms-DS-GeoCoordinates-Latitude|
|Mail-Recipient|add:mayContain|ms-DS-GeoCoordinates-Longitude|
|ms-Exch-Resource-Policy|add:mayContain|msExchCustomerExpectationCritical|
|ms-Exch-Resource-Policy|add:mayContain|msExchDiscretionaryCritical|
|ms-Exch-Resource-Policy|add:mayContain|msExchInternalMaintenanceCritical|
|ms-Exch-Resource-Policy|add:mayContain|msExchUrgentCritical|
|ms-Exch-Availability-Address-Space|add:mayContain|msExchFedTargetAutodiscoverEPR|
|ms-Exch-Private-MDB|add:mayContain|msExchMailboxDatabaseTransportFlags|
|Mail-Recipient|add:mayContain|msExchRecipientSoftDeletedStatus|
|Mail-Recipient|add:mayContain|msExchWhenSoftDeletedTime|
|ms-Exch-Custom-Attributes|add:mayContain|msExchExtensionCustomAttribute1|
|ms-Exch-Custom-Attributes|add:mayContain|msExchExtensionCustomAttribute2|
|ms-Exch-Custom-Attributes|add:mayContain|msExchExtensionCustomAttribute3|
|ms-Exch-Custom-Attributes|add:mayContain|msExchExtensionCustomAttribute4|
|ms-Exch-Custom-Attributes|add:mayContain|msExchExtensionCustomAttribute5|
|ms-Exch-Virtual-Directory|add:mayContain|msExchMRSProxyFlags|
|ms-Exch-Virtual-Directory|add:mayContain|msExchMRSProxyMaxConnections|
|ms-Exch-Active-Sync-Device|add:mayContain|msExchDeviceClientType|
|ms-Exch-Exchange-Server|add:mayContain|msExchMalwareFilteringDeferAttempts|
|ms-Exch-Exchange-Server|add:mayContain|msExchMalwareFilteringDeferWaitTime|
|ms-Exch-Exchange-Server|add:mayContain|msExchMalwareFilteringFlags|
|ms-Exch-Exchange-Server|add:mayContain|msExchMalwareFilteringPrimaryUpdatePath|
|ms-Exch-Exchange-Server|add:mayContain|msExchMalwareFilteringSecondaryUpdatePath|
|ms-Exch-Exchange-Server|add:mayContain|msExchMalwareFilteringUpdateFrequency|
|ms-Exch-Exchange-Server|add:mayContain|msExchMalwareFilteringUpdateTimeout|
|ms-Exch-Mail-Storage|add:mayContain|msExchTeamMailboxExpiration|
|ms-Exch-Mail-Storage|add:mayContain|msExchTeamMailboxOwners|
|ms-Exch-Mail-Storage|add:mayContain|msExchTeamMailboxSharePointLinkedBy|
|ms-Exch-Mail-Storage|add:mayContain|msExchTeamMailboxSharePointUrl|
|ms-Exch-Mail-Storage|add:mayContain|msExchTeamMailboxShowInClientList|
|ms-Exch-Mail-Storage|add:mayContain|msExchCalendarLoggingQuota|
|ms-Exch-MSO-Sync-Service-Instance|add:mayContain|msExchMSOForwardSyncNonRecipientCookie|
|ms-Exch-MSO-Sync-Service-Instance|add:mayContain|msExchMSOForwardSyncRecipientCookie|
|ms-Exch-MSO-Sync-Service-Instance|add:mayContain|msExchMSOForwardSyncReplayList|
|ms-Exch-MSO-Sync-Service-Instance|add:mayContain|msExchAccountForestLink|
|Top|add:mayContain|msExchAccountForestBL|
|Top|add:mayContain|msExchTrustedDomainBL|
|Top|add:mayContain|msExchAcceptedDomainBL|
|Top|add:mayContain|msExchHygieneConfigurationMalwareBL|
|Top|add:mayContain|msExchHygieneConfigurationSpamBL|
|ms-Exch-Base-Class|add:mayContain|msExchELCMailboxFlags|
|Mail-Recipient|add:mayContain|msExchHomeMTASL|
|Mail-Recipient|add:mayContain|msExchMailboxMoveSourceArchiveMDBLinkSL|
|Mail-Recipient|add:mayContain|msExchMailboxMoveSourceMDBLinkSL|
|Mail-Recipient|add:mayContain|msExchMailboxMoveTargetArchiveMDBLinkSL|
|Mail-Recipient|add:mayContain|msExchMailboxMoveTargetMDBLinkSL|
|ms-Exch-Accepted-Domain|add:mayContain|msExchHygieneConfigurationLink|
|ms-Exch-Accepted-Domain|add:mayContain|msExchTransportResellerSettingsLinkSL|
|ms-Exch-Configuration-Unit-Container|add:mayContain|msExchManagementSiteLinkSL|
|ms-Exch-Configuration-Unit-Container|add:mayContain|msExchOrganizationUpgradePolicyLinkSL|
|ms-Exch-Fed-OrgId|add:mayContain|msExchFedDelegationTrustSL|
|ms-Exch-Mail-Gateway|add:mayContain|msExchHomeMDBSL|
|ms-Exch-Mail-Gateway|add:mayContain|msExchHomeMTASL|
|ms-Exch-Mail-Storage|add:mayContain|msExchArchiveDatabaseLinkSL|
|ms-Exch-Mail-Storage|add:mayContain|msExchDisabledArchiveDatabaseLinkSL|
|ms-Exch-Mail-Storage|add:mayContain|msExchHomeMDBSL|
|ms-Exch-Mail-Storage|add:mayContain|msExchMailboxMoveTargetMDBLinkSL|
|ms-Exch-Mail-Storage|add:mayContain|msExchPreviousArchiveDatabaseSL|
|ms-Exch-Mail-Storage|add:mayContain|msExchPreviousHomeMDBSL|
|ms-Exch-MRS-Request|add:mayContain|msExchMailboxMoveSourceMDBLinkSL|
|ms-Exch-MRS-Request|add:mayContain|msExchMailboxMoveStorageMDBLinkSL|
|ms-Exch-MRS-Request|add:mayContain|msExchMailboxMoveTargetMDBLinkSL|
|ms-Exch-OAB|add:mayContain|msExchOffLineABServerSL|
|ms-Exch-Routing-Group-Connector|add:mayContain|msExchHomeMTASL|
|ms-Exch-Site-Connector|add:mayContain|msExchHomeMTASL|
|ms-Exch-Tenant-Perimeter-Settings|add:mayContain|msExchTransportResellerSettingsLinkSL|
|ms-Exch-Domain-Content-Config|add:mayContain|msExchContentByteEncoderTypeFor7BitCharsets|
|ms-Exch-Domain-Content-Config|add:mayContain|msExchContentPreferredInternetCodePageForShiftJis|
|ms-Exch-Domain-Content-Config|add:mayContain|msExchContentRequiredCharSetCoverage|
|ms-Exch-Coexistence-Relationship|add:mayContain|msExchCoexistenceOnPremisesSmartHost|
|ms-Exch-Coexistence-Relationship|add:mayContain|msExchCoexistenceSecureMailCertificateThumbprint|
|ms-Exch-Coexistence-Relationship|add:mayContain|msExchCoexistenceTransportServers|
|Mail-Recipient|add:mayContain|ms-exch-group-external-member-count|
|Mail-Recipient|add:mayContain|ms-exch-group-member-count|
|Ms-Exch-Organization-Container|add:mayContain|ms-exch-organization-flags-2|
|Mail-Recipient|add:mayContain|msExchGroupExternalMemberCount|
|Mail-Recipient|add:mayContain|msExchGroupMemberCount|
|Mail-Recipient|add:mayContain|msExchShadowWhenSoftDeletedTime|
|ms-Exch-Organization-Container|add:mayContain|msExchOrganizationFlags2|
|ms-Exch-Organization-Container|add:mayContain|msExchUMAvailableLanguages|
|ms-Exch-Control-Point-Config|add:mayContain|msExchRMSOnlineCertificationLocationUrl|
|ms-Exch-Control-Point-Config|add:mayContain|msExchRMSOnlineKeySharingLocationUrl|
|ms-Exch-Control-Point-Config|add:mayContain|msExchRMSOnlineLicensingLocationUrl|
|ms-Exch-Throttling-Policy|add:mayContain|msExchThrottlingPolicyFlags|
|ms-Exch-Exchange-Server|add:mayContain|msExchMalwareFilteringScanTimeout|
|ms-Exch-Hosted-Content-Filter-Config|add:mayContain|msExchSpamCountryBlockList|
|ms-Exch-Hosted-Content-Filter-Config|add:mayContain|msExchSpamLanguageBlockList|
|ms-Exch-Hosted-Content-Filter-Config|add:mayContain|msExchSpamNotifyOutboundRecipients|
|ms-Exch-Malware-Filter-Config|add:mayContain|msExchMalwareFilterConfigExternalSenderAdminAddress|
|ms-Exch-Malware-Filter-Config|add:mayContain|msExchMalwareFilterConfigInternalSenderAdminAddress|
|ms-Exch-MSO-Sync-Service-Instance|add:mayContain|msExchActiveInstanceSleepInterval|
|ms-Exch-MSO-Sync-Service-Instance|add:mayContain|msExchPassiveInstanceSleepInterval|
|ms-Exch-MSO-Sync-Service-Instance|add:mayContain|msExchSyncDaemonMaxVersion|
|ms-Exch-MSO-Sync-Service-Instance|add:mayContain|msExchSyncDaemonMinVersion|
|Mail-Recipient|add:mayContain|msExchPublicFolderMailbox|
|Mail-Recipient|add:mayContain|msExchPublicFolderSmtpAddress|
|ms-Exch-Hosted-Content-Filter-Config|add:mayContain|msExchSpamDigestFrequency|
|ms-Exch-Hosted-Content-Filter-Config|add:mayContain|msExchSpamQuarantineRetention|
|ms-Exch-Organization-Container|add:mayContain|msExchWACDiscoveryEndpoint|
|ms-Exch-Organization-Container|add:mayContain|msExchAdfsAuthenticationRawConfiguration|
|ms-Exch-Organization-Container|add:mayContain|msExchServiceEndPointURL|
|ms-Exch-Public-Folder|add:mayContain|msExchPublicFolderEntryId|
|ms-Exch-Transport-Rule|add:mayContain|msExchTransportRuleImmutableId|
|ms-Exch-Transport-Settings|add:mayContain|msExchTransportMaxRetriesForLocalSiteShadow|
|ms-Exch-Transport-Settings|add:mayContain|msExchTransportMaxRetriesForRemoteSiteShadow|
|ms-Exch-Transport-Settings|add:mayContain|msExchConfigurationXML|
|ms-Exch-Account-Forest|possSuperiors|msExchContainer|
|ms-Exch-Base-Class|add:mayContain|msExchCanaryData0|
|ms-Exch-Base-Class|add:mayContain|msExchCanaryData1|
|ms-Exch-Base-Class|add:mayContain|msExchCanaryData2|
|ms-Exch-Base-Class|add:mayContain|msExchCorrelationId|
|ms-Exch-Configuration-Unit-Container|add:mayContain|msExchRelocateTenantCompletionTargetVector|
|ms-Exch-Configuration-Unit-Container|add:mayContain|msExchRelocateTenantFlags|
|ms-Exch-Configuration-Unit-Container|add:mayContain|msExchRelocateTenantSafeLockdownSchedule|
|ms-Exch-Configuration-Unit-Container|add:mayContain|msExchRelocateTenantSourceForest|
|ms-Exch-Configuration-Unit-Container|add:mayContain|msExchRelocateTenantStartLockdown|
|ms-Exch-Configuration-Unit-Container|add:mayContain|msExchRelocateTenantStartRetired|
|ms-Exch-Configuration-Unit-Container|add:mayContain|msExchRelocateTenantStartSync|
|ms-Exch-Configuration-Unit-Container|add:mayContain|msExchRelocateTenantStatus|
|ms-Exch-Configuration-Unit-Container|add:mayContain|msExchRelocateTenantTargetForest|
|ms-Exch-Configuration-Unit-Container|add:mayContain|msExchRelocateTenantTransitionCounter|
|ms-Exch-Configuration-Unit-Container|add:mayContain|msExchSyncCookie|
|ms-Exch-Throttling-Policy|add:mayContain|msExchAnonymousThrottlingPolicyStateEx|
|ms-Exch-Throttling-Policy|add:mayContain|msExchEASThrottlingPolicyStateEx|
|ms-Exch-Throttling-Policy|add:mayContain|msExchEWSThrottlingPolicyStateEx|
|ms-Exch-Throttling-Policy|add:mayContain|msExchGeneralThrottlingPolicyStateEx|
|ms-Exch-Throttling-Policy|add:mayContain|msExchIMAPThrottlingPolicyStateEx|
|ms-Exch-Throttling-Policy|add:mayContain|msExchOWAThrottlingPolicyStateEx|
|ms-Exch-Throttling-Policy|add:mayContain|msExchPOPThrottlingPolicyStateEx|
|ms-Exch-Throttling-Policy|add:mayContain|msExchPowershellThrottlingPolicyStateEx|
|ms-Exch-Throttling-Policy|add:mayContain|msExchRCAThrottlingPolicyStateEx|
|ms-Exch-Mailflow-Policy|add:mayContain|msExchImmutableId|
|ms-Exch-MDB|add:mayContain|msExchCalendarLoggingQuota|
|ms-Exch-Transport-Rule|add:mayContain|msExchImmutableId|
|ms-Exch-MSO-Sync-Service-Instance|add:mayContain|msExchSyncServiceInstanceNewTenantMaxVersion|
|ms-Exch-MSO-Sync-Service-Instance|add:mayContain|msExchSyncServiceInstanceNewTenantMinVersion|

## Attributes modified by Exchange 2013 RTM

This section contains the attributes modified in Exchange 2013 RTM.

|Class|Change|Value|
|---|---|---|
|ms-Exch-Schema-Version-Pt|rangeUpper|15137|
|ms-Exch-HAB-Root-Department-Link|replace: isMemberOfPartialAttributeSet|TRUE|
|ms-Exch-Archive-GUID|replace: searchFlags|9|
|ms-Exch-Accepted-Domain-Name|replace: searchFlags|9|
|ms-Exch-Bypass-Audit|replace: searchFlags|19|
|ms-Exch-Mailbox-Audit-Enable|replace: searchFlags|19|
|ms-Exch-Extension-Custom-Attribute-1|isMemberOfPartialAttributeSet:|TRUE|
|ms-Exch-Extension-Custom-Attribute-2|isMemberOfPartialAttributeSet:|TRUE|
|ms-Exch-Extension-Custom-Attribute-3|isMemberOfPartialAttributeSet:|TRUE|
|ms-Exch-Extension-Custom-Attribute-4|isMemberOfPartialAttributeSet:|TRUE|
|ms-Exch-Extension-Custom-Attribute-5|isMemberOfPartialAttributeSet|TRUE|
|ms-Exch-Coexistence-On-Premises-Smart-Host|ntdsSchemaAdd|attributeID: 1.2.840.113556.1.4.7000.102.51992 isMemberOfPartialAttributeSet: FALSE (not in global catalogue) searchFlags: 0 (no index)|
|ms-Exch-Coexistence-Secure-Mail-Certificate-Thumbprint|ntdsSchemaAdd|attributeID: 1.2.840.113556.1.4.7000.102.51991 isMemberOfPartialAttributeSet: FALSE (not in global catalogue) searchFlags: 0 (no index)|
|ms-Exch-Coexistence-Transport-Servers|ntdsSchemaAdd|attributeID: 1.2.840.113556.1.4.7000.102.51990 isMemberOfPartialAttributeSet: FALSE (not in global catalogue) searchFlags: 0 (no index)|
|ms-Exch-ELC-Mailbox-Flags|replace: attributeSecurityGuid|F6SzsVXskUGzJ7cuM+OK8g==|
|ms-Exch-Malware-Filtering-Update-Frequency|rangeUpper|38880|
|ms-Exch-MSO-Forward-Sync-Non-Recipient-Cookie|rangeUpper|20480|
|ms-Exch-MSO-Forward-Sync-Recipient-Cookie|rangeUpper|20480|
|ms-Exch-Role-Entries|rangeUpper|8192|
|ms-Exch-Group-External-Member-Count|ntdsSchemaModify|isMemberOfPartialAttributeSet: TRUE MAPIID:36066|
|ms-Exch-Group-Member-Count|ntdsSchemaModify|replace: isMemberOfPartialAttributeSetisMemberOfPartialAttributeSet: TRUE MAPIID: 36067|

## Classes added by Exchange 2013 RTM

The following classes are added when you install Exchange 2013 RTM:

- ms-Exch-ActiveSync-Device-Autoblock-Threshold
- ms-Exch-MSO-Forward-Sync-Divergence
- ms-Exch-MSO-Sync-Service-Instance
- ms-Exch-Organization-Upgrade-Policy
- ms-Exch-Workload-Policy
- ms-Exch-Resource-Policy
- ms-Exch-Team-Mailbox-Provisioning-Policy
- ms-Exch-Account-Forest
- ms-Exch-Hosted-Content-Filter-Config
- ms-Exch-Hygiene-Configuration
- ms-Exch-Malware-Filter-Config
- ms-Exch-Protocol-Cfg-SIP-Container
- ms-Exch-Protocol-Cfg-SIP-FE-Server
- ms-Exch-Exchange-Transport-Server
- ms-Exch-Auth-Auth-Config
- ms-Exch-Auth-Auth-Server
- ms-Exch-Auth-Partner-Application
- ms-Exch-Mailflow-Policy-Collection
- ms-Exch-Mailflow-Policy

## Attributes added by Exchange 2013 RTM

The following attributes encompass a set of changes required for new features and are added when you install Exchange 2013 RTM:

- ms-Exch-ActiveSync-Device-AutoBlock-Duration
- ms-Exch-ActiveSync-Device-Autoblock-Threshold-Incidence-Duration
- ms-Exch-ActiveSync-Device-Autoblock-Threshold-Incidence-Limit
- ms-Exch-ActiveSync-Device-Autoblock-Threshold-Type
- ms-Exch-Dirsync-Authority-Metadata
- ms-Exch-Dirsync-Status
- ms-Exch-Dirsync-Status-Ack
- ms-Exch-Edge-Sync-Config-Flags
- ms-Exch-Is-Dirsync-Status-Pending,
- ms-Exch-Localization-Flags
- ms-Exch-Previous-Archive-Database
- ms-Exch-RoleGroup-Type
- ms-Exch-External-Directory-Object-Class
- ms-Exch-MSO-Forward-Sync-Divergence-Count
- ms-Exch-MSO-Forward-Sync-Divergence-Timestamp
- ms-Exch-MSO-Forward-Sync-Divergence-Related-Object-Link
- ms-Exch-Default-Public-Folder-Mailbox
- ms-Exch-Forest-Mode-Flag
- ms-Exch-Dir-Sync-Service-Instance
- ms-Exch-Organization-Upgrade-Policy-Date
- ms-Exch-Organization-Upgrade-Policy-Enabled
- ms-Exch-Organization-Upgrade-Policy-MaxMailboxes
- ms-Exch-Organization-Upgrade-Policy-Priority
- ms-Exch-Organization-Upgrade-Policy-Source-Version
- ms-Exch-Organization-Upgrade-Policy-Status
- ms-Exch-Organization-Upgrade-Policy-Target-Version
- ms-Exch-OWA-Set-Photo-URL
- ms-Exch-Organization-Upgrade-Policy-Link
- ms-Exch-Organization-Upgrade-Policy-BL
- ms-Exch-Workload-Classification
- ms-Exch-Workload-Management-Is-Enabled
- ms-Exch-Workload-Type
- ms-Exch-Workload-Management-Policy-Link
- ms-Exch-Workload-Management-Policy-BL
- ms-Exch-Workload-Management-Policy
- ms-Exch-Customer-Expectation-Overloaded
- ms-Exch-Customer-Expectation-Underloaded
- ms-Exch-Discretionary-Overloaded
- ms-Exch-Discretionary-Underloaded
- ms-Exch-Internal-Maintenance-Overloaded
- ms-Exch-Internal-Maintenance-Underloaded
- ms-Exch-Resource-Type
- ms-Exch-Urgent-Overloaded
- ms-Exch-Urgent-Underloaded
- ms-DS-GeoCoordinates-Altitude
- ms-DS-GeoCoordinates-Latitude
- ms-DS-GeoCoordinates-Longitude
- ms-Exch-Customer-Expectation-Critical
- ms-Exch-Discretionary-Critical
- ms-Exch-Internal-Maintenance-Critical
- ms-Exch-Urgent-Critical
- ms-Exch-Mailbox-Database-Transport-Flags
- ms-Exch-Extension-Custom-Attribute-1
- ms-Exch-Extension-Custom-Attribute-2
- ms-Exch-Extension-Custom-Attribute-3
- ms-Exch-Extension-Custom-Attribute-4
- ms-Exch-Extension-Custom-Attribute-5
- ms-Exch-MRS-Proxy-Flags
- ms-Exch-MRS-Proxy-Max-Connections
- ms-Exch-Recipient-SoftDeleted-Status
- ms-Exch-When-Soft-Deleted-Time
- ms-Exch-Device-Client-Type
- ms-Exch-Malware-Filtering-Defer-Attempts
- ms-Exch-Malware-Filtering-Defer-Wait-Time
- ms-Exch-Malware-Filtering-Flags
- ms-Exch-Malware-Filtering-Primary-Update-Path
- ms-Exch-Malware-Filtering-Secondary-Update-Path
- ms-Exch-Malware-Filtering-Update-Frequency
- ms-Exch-Malware-Filtering-Update-Timeout
- ms-Exch-Team-Mailbox-Expiration
- ms-Exch-Team-Mailbox-Expiry-Days
- ms-Exch-Team-Mailbox-Owners
- ms-Exch-Team-Mailbox-SharePoint-Linked-By
- ms-Exch-Team-Mailbox-SharePoint-Url
- ms-Exch-Team-Mailbox-Show-In-Client-List
- ms-Exch-Account-Forest-Link
- ms-Exch-Account-Forest-BL
- ms-Exch-Trusted-Domain-Link
- ms-Exch-Trusted-Domain-BL
- ms-Exch-Archive-Database-Link-SL
- ms-Exch-Disabled-Archive-Database-Link-SL
- ms-Exch-Fed-Delegation-Trust-SL
- ms-Exch-Home-MDB-SL
- ms-Exch-Home-MTA-SL
- ms-Exch-Mailbox-Move-Source-Archive-MDB-Link-SL
- ms-Exch-Mailbox-Move-Source-MDB-Link-SL
- ms-Exch-Mailbox-Move-Storage-MDB-Link-SL
- ms-Exch-Mailbox-Move-Target-Archive-MDB-Link-SL
- ms-Exch-Mailbox-Move-Target-MDB-Link-SL
- ms-Exch-Malware-Filter-Config-Alert-Text
- ms-Exch-Malware-Filter-Config-External-Body
- ms-Exch-Malware-Filter-Config-External-Subject
- ms-Exch-Malware-Filter-Config-Flags
- ms-Exch-Malware-Filter-Config-From-Address
- ms-Exch-Malware-Filter-Config-From-Name
- ms-Exch-Malware-Filter-Config-Internal-Body
- ms-Exch-Malware-Filter-Config-Internal-Subject
- ms-Exch-Management-Site-Link-SL
- ms-Exch-Off-Line-AB-Server-SL
- ms-Exch-Organization-Upgrade-Policy-Link-SL
- ms-Exch-Previous-Archive-Database-SL
- ms-Exch-Previous-Home-MDB-SL
- ms-Exch-RMS-Computer-Accounts-Link-SL
- ms-Exch-Spam-Add-Header
- ms-Exch-Spam-Asf-Settings
- ms-Exch-Spam-Asf-Test-Bcc-Address
- ms-Exch-Spam-False-Positive-Cc
- ms-Exch-Spam-Flags
- ms-Exch-Spam-Modify-Subject
- ms-Exch-Spam-Outbound-Spam-Cc
- ms-Exch-Spam-Redirect-Address
- ms-Exch-Transport-Reseller-Settings-Link-SL
- ms-Exch-Hygiene-Configuration-Link
- ms-Exch-Accepted-Domain-BL
- ms-Exch-Malware-Filter-Config-Link
- ms-Exch-Hygiene-Configuration-Malware-BL
- ms-Exch-Hosted-Content-Filter-Config-Link
- ms-Exch-Hygiene-Configuration-Spam-BL
- ms-Exch-Content-Byte-Encoder-Type-For-7-Bit-Charsets
- ms-Exch-Content-Preferred-Internet-Code-Page-For-Shift-Jis
- ms-Exch-Content-Required-Char-Set-Coverage
- ms-Exch-Group-External-Member-Count
- ms-Exch-Group-Member-Count
- ms-Exch-Organization-Flags-2
- ms-Exch-RMSOnline-Certification-Location-Url
- ms-Exch-RMSOnline-Key-Sharing-Location-Url
- ms-Exch-RMSOnline-Licensing-Location-Url
- ms-Exch-Shadow-When-Soft-Deleted-Time
- ms-Exch-Throttling-Policy-Flags
- ms-Exch-Malware-Filter-Config-External-Sender-Admin-Address
- ms-Exch-Malware-Filter-Config-Internal-Sender-Admin-Address
- ms-Exch-Malware-Filtering-Scan-Timeout
- ms-Exch-Spam-Country-Block-List
- ms-Exch-Spam-Language-Block-List
- ms-Exch-Spam-Notify-Outbound-Recipients
- ms-Exch-Auth-App-Secret
- ms-Exch-Auth-Application-Identifier
- ms-Exch-Auth-Auth-Server-Type
- ms-Exch-Auth-Authorization-Url
- ms-Exch-Auth-Certificate-Data
- ms-Exch-Auth-Certificate-Thumbprint
- ms-Exch-Auth-Flags
- ms-Exch-Auth-Issuer-Name
- ms-Exch-Auth-Issuing-Url
- ms-Exch-Auth-Linked-Account
- ms-Exch-Auth-Metadata-Url
- ms-Exch-Auth-Realm
- ms-Exch-Mailflow-Policy-Countries
- ms-Exch-Mailflow-Policy-Keywords
- ms-Exch-Mailflow-Policy-Publisher-Name
- ms-Exch-Mailflow-Policy-Transport-Rules-Template-Xml
- ms-Exch-Mailflow-Policy-Version
- ms-Exch-Public-Folder-EntryId
- ms-Exch-Public-Folder-Mailbox
- ms-Exch-Public-Folder-Smtp-Address
- ms-Exch-Spam-Digest-Frequency
- ms-Exch-Spam-Quarantine-Retention
- ms-Exch-Transport-MaxRetriesForLocalSiteShadow
- ms-Exch-Transport-MaxRetriesForRemoteSiteShadow
- ms-Exch-Transport-Rule-Immutable-Id
- ms-Exch-WAC-Discovery-Endpoint
- ms-Exch-Anonymous-Throttling-Policy-State-Ex
- ms-Exch-Canary-Data-0
- ms-Exch-Canary-Data-1
- ms-Exch-Canary-Data-2
- ms-Exch-Correlation-Id
- ms-Exch-EAS-Throttling-Policy-State-Ex
- ms-Exch-EWS-Throttling-Policy-State-Ex
- ms-Exch-General-Throttling-Policy-State-Ex
- ms-Exch-IMAP-Throttling-Policy-State-Ex
- ms-Exch-OWA-Throttling-Policy-State-Ex
- ms-Exch-POP-Throttling-Policy-State-Ex
- ms-Exch-Powershell-Throttling-Policy-State-Ex
- ms-Exch-RCA-Throttling-Policy-State-Ex
- ms-Exch-Relocate-Tenant-Completion-Target-Vector
- ms-Exch-Relocate-Tenant-Flags
- ms-Exch-Relocate-Tenant-Safe-Lockdown-Schedule
- ms-Exch-Relocate-Tenant-Source-Forest
- ms-Exch-Relocate-Tenant-Start-Lockdown
- ms-Exch-Relocate-Tenant-Start-Retired
- ms-Exch-Relocate-Tenant-Start-Sync
- ms-Exch-Relocate-Tenant-Status
- ms-Exch-Relocate-Tenant-Target-Forest
- ms-Exch-Relocate-Tenant-Transition-Counter
- ms-Exch-Sync-Cookie
- ms-Exch-Adfs-Authentication-Raw-Configuration
- ms-Exch-Service-End-Point-URL
- ms-Exch-Sync-Service-Instance-New-Tenant-Max-Version
- ms-Exch-Sync-Service-Instance-New-Tenant-Min-Version

## MAPI IDs added by Exchange 2013 RTM

The following MAPI IDs are added when you install Exchange 2013 RTM:

- 36066
- 36067

## Extended rights added by Exchange 2013 RTM

The following table lists the extended rights that are added when you install Exchange 2013 RTM. Installing Exchange 2013 RTM doesn't modify any existing extended rights.

|Identifier|Values|
|---|---|
|CN=ms-Exch-SMTP-Accept-XProxyFrom,CN=Extended-Rights,&lt;ConfigurationContainerDN&gt;|changetype: ntdsSchemaAdd</p><p>displayName: Accept XProxyFrom</p><p>objectClass: controlAccessRight</p><p>rightsGuid: 5bee2b72-50d7-49c7-ba66-39a25daa1e92</p><p>validAccesses: 256|

## Object IDs added by Exchange 2013 RTM

The following attribute object IDs are added when you install Exchange 2013 RTM:

- 1.2.840.113556.1.4.7000.102.51794
- 1.2.840.113556.1.4.7000.102.51795
- 1.2.840.113556.1.4.7000.102.51792
- 1.2.840.113556.1.4.7000.102.51791
- 1.2.840.113556.1.4.7000.102.51789
- 1.2.840.113556.1.4.7000.102.51787
- 1.2.840.113556.1.4.7000.102.51788
- 1.2.840.113556.1.4.7000.102.51786
- 1.2.840.113556.1.4.7000.102.51790
- 1.2.840.113556.1.4.7000.102.51774
- 1.2.840.113556.1.4.7000.102.51773
- 1.2.840.113556.1.4.7000.102.51775
- 1.2.840.113556.1.4.7000.102.51798
- 1.2.840.113556.1.4.7000.102.51801
- 1.2.840.113556.1.4.7000.102.51800
- 1.2.840.113556.1.4.7000.102.51799
- 1.2.840.113556.1.4.7000.102.51805
- 1.2.840.113556.1.4.7000.102.51796
- 1.2.840.113556.1.4.7000.102.51797
- 1.2.840.113556.1.4.7000.102.51814
- 1.2.840.113556.1.4.7000.102.51813
- 1.2.840.113556.1.4.7000.102.51815
- 1.2.840.113556.1.4.7000.102.51816
- 1.2.840.113556.1.4.7000.102.51818
- 1.2.840.113556.1.4.7000.102.51812
- 1.2.840.113556.1.4.7000.102.51819
- 1.2.840.113556.1.4.7000.102.51806
- 1.2.840.113556.1.4.7000.102.51820
- 1.2.840.113556.1.4.7000.102.51821
- 1.2.840.113556.1.4.7000.102.51811
- 1.2.840.113556.1.4.7000.102.51807
- 1.2.840.113556.1.4.7000.102.51810
- 1.2.840.113556.1.4.7000.102.51808
- 1.2.840.113556.1.4.7000.102.51809
- 1.2.840.113556.1.4.7000.102.51830
- 1.2.840.113556.1.4.7000.102.51829
- 1.2.840.113556.1.4.7000.102.51824
- 1.2.840.113556.1.4.7000.102.51823
- 1.2.840.113556.1.4.7000.102.51827
- 1.2.840.113556.1.4.7000.102.51826
- 1.2.840.113556.1.4.7000.102.51822
- 1.2.840.113556.1.4.7000.102.51833
- 1.2.840.113556.1.4.7000.102.51832
- 1.2.840.113556.1.4.2183
- 1.2.840.113556.1.4.2184
- 1.2.840.113556.1.4.2185
- 1.2.840.113556.1.4.7000.102.51838
- 1.2.840.113556.1.4.7000.102.51836
- 1.2.840.113556.1.4.7000.102.51837
- 1.2.840.113556.1.4.7000.102.51839
- 1.2.840.113556.1.4.7000.102.51840
- 1.2.840.113556.1.4.7000.102.51876
- 1.2.840.113556.1.4.7000.102.51877
- 1.2.840.113556.1.4.7000.102.51878
- 1.2.840.113556.1.4.7000.102.51879
- 1.2.840.113556.1.4.7000.102.51880
- 1.2.840.113556.1.4.7000.102.51851
- 1.2.840.113556.1.4.7000.102.51852
- 1.2.840.113556.1.4.7000.102.51859
- 1.2.840.113556.1.4.7000.102.51860
- 1.2.840.113556.1.4.7000.102.51861
- 1.2.840.113556.1.4.7000.102.51864
- 1.2.840.113556.1.4.7000.102.51863
- 1.2.840.113556.1.4.7000.102.51862
- 1.2.840.113556.1.4.7000.102.51865
- 1.2.840.113556.1.4.7000.102.51866
- 1.2.840.113556.1.4.7000.102.51867
- 1.2.840.113556.1.4.7000.102.51868
- 1.2.840.113556.1.4.7000.102.51871
- 1.2.840.113556.1.4.7000.102.51870
- 1.2.840.113556.1.4.7000.102.51872
- 1.2.840.113556.1.4.7000.102.51875
- 1.2.840.113556.1.4.7000.102.51874
- 1.2.840.113556.1.4.7000.102.51873
- 1.2.840.113556.1.4.7000.102.51869
- 1.2.840.113556.1.4.7000.102.51915
- 1.2.840.113556.1.4.7000.102.51883
- 1.2.840.113556.1.4.7000.102.51914
- 1.2.840.113556.1.4.7000.102.51931
- 1.2.840.113556.1.4.7000.102.51932
- 1.2.840.113556.1.4.7000.102.51939
- 1.2.840.113556.1.4.7000.102.51930
- 1.2.840.113556.1.4.7000.102.51940
- 1.2.840.113556.1.4.7000.102.51933
- 1.2.840.113556.1.4.7000.102.51934
- 1.2.840.113556.1.4.7000.102.51935
- 1.2.840.113556.1.4.7000.102.51936
- 1.2.840.113556.1.4.7000.102.51952
- 1.2.840.113556.1.4.7000.102.51923
- 1.2.840.113556.1.4.7000.102.51927
- 1.2.840.113556.1.4.7000.102.51926
- 1.2.840.113556.1.4.7000.102.51922
- 1.2.840.113556.1.4.7000.102.51929
- 1.2.840.113556.1.4.7000.102.51928
- 1.2.840.113556.1.4.7000.102.51925
- 1.2.840.113556.1.4.7000.102.51924
- 1.2.840.113556.1.4.7000.102.51941
- 1.2.840.113556.1.4.7000.102.51942
- 1.2.840.113556.1.4.7000.102.51937
- 1.2.840.113556.1.4.7000.102.51943
- 1.2.840.113556.1.4.7000.102.51944
- 1.2.840.113556.1.4.7000.102.51938
- 1.2.840.113556.1.4.7000.102.51882
- 1.2.840.113556.1.4.7000.102.51881
- 1.2.840.113556.1.4.7000.102.51921
- 1.2.840.113556.1.4.7000.102.51918
- 1.2.840.113556.1.4.7000.102.51920
- 1.2.840.113556.1.4.7000.102.51916
- 1.2.840.113556.1.4.7000.102.51919
- 1.2.840.113556.1.4.7000.102.51917
- 1.2.840.113556.1.4.7000.102.51945
- 1.2.840.113556.1.4.7000.102.51946
- 1.2.840.113556.1.4.7000.102.51948
- 1.2.840.113556.1.4.7000.102.51949
- 1.2.840.113556.1.4.7000.102.51947
- 1.2.840.113556.1.4.7000.102.51950
- 1.2.840.113556.1.4.7000.102.51951
- 1.2.840.113556.1.4.7000.102.51954
- 1.2.840.113556.1.4.7000.102.51955
- 1.2.840.113556.1.4.7000.102.51953
- 1.2.840.113556.1.4.7000.102.51993
- 1.2.840.113556.1.4.7000.102.51995
- 1.2.840.113556.1.4.7000.102.51994
- 1.2.840.113556.1.4.7000.102.51998
- 1.2.840.113556.1.4.7000.102.51997
- 1.2.840.113556.1.4.7000.102.52004
- 1.2.840.113556.1.4.7000.102.52003
- 1.2.840.113556.1.4.7000.102.52002
- 1.2.840.113556.1.4.7000.102.52001
- 1.2.840.113556.1.4.7000.102.52005
- 1.2.840.113556.1.4.7000.102.52007
- 1.2.840.113556.1.4.7000.102.52006
- 1.2.840.113556.1.4.7000.102.51996
- 1.2.840.113556.1.4.7000.102.52008
- 1.2.840.113556.1.4.7000.102.52017
- 1.2.840.113556.1.4.7000.102.52014
- 1.2.840.113556.1.4.7000.102.52021
- 1.2.840.113556.1.4.7000.102.52020
- 1.2.840.113556.1.4.7000.102.52012
- 1.2.840.113556.1.4.7000.102.52011
- 1.2.840.113556.1.4.7000.102.52013
- 1.2.840.113556.1.4.7000.102.52018
- 1.2.840.113556.1.4.7000.102.52019
- 1.2.840.113556.1.4.7000.102.52022
- 1.2.840.113556.1.4.7000.102.52015
- 1.2.840.113556.1.4.7000.102.52016
- 1.2.840.113556.1.4.7000.102.52029
- 1.2.840.113556.1.4.7000.102.52030
- 1.2.840.113556.1.4.7000.102.52039
- 1.2.840.113556.1.4.7000.102.52041
- 1.2.840.113556.1.4.7000.102.52037
- 1.2.840.113556.1.4.7000.102.52035
- 1.2.840.113556.1.4.7000.102.52034
- 1.2.840.113556.1.4.7000.102.52036
- 1.2.840.113556.1.4.7000.102.52032
- 1.2.840.113556.1.4.7000.102.52033
- 1.2.840.113556.1.4.7000.102.52031
- 1.2.840.113556.1.4.7000.102.52024
- 1.2.840.113556.1.4.7000.102.52040
- 1.2.840.113556.1.4.7000.102.52023
- 1.2.840.113556.1.4.7000.102.52042
- 1.2.840.113556.1.4.7000.102.52051
- 1.2.840.113556.1.4.7000.102.52052
- 1.2.840.113556.1.4.7000.102.52053
- 1.2.840.113556.1.4.7000.102.52065
- 1.2.840.113556.1.4.7000.102.52043
- 1.2.840.113556.1.4.7000.102.52044
- 1.2.840.113556.1.4.7000.102.52045
- 1.2.840.113556.1.4.7000.102.52046
- 1.2.840.113556.1.4.7000.102.52047
- 1.2.840.113556.1.4.7000.102.52048
- 1.2.840.113556.1.4.7000.102.52049
- 1.2.840.113556.1.4.7000.102.52050
- 1.2.840.113556.1.4.7000.102.52063
- 1.2.840.113556.1.4.7000.102.52061
- 1.2.840.113556.1.4.7000.102.52059
- 1.2.840.113556.1.4.7000.102.52058
- 1.2.840.113556.1.4.7000.102.52055
- 1.2.840.113556.1.4.7000.102.52056
- 1.2.840.113556.1.4.7000.102.52054
- 1.2.840.113556.1.4.7000.102.52060
- 1.2.840.113556.1.4.7000.102.52057
- 1.2.840.113556.1.4.7000.102.52062
- 1.2.840.113556.1.4.7000.102.52064

The following class object IDs are added when you install Exchange 2013 RTM:

- 1.2.840.113556.1.5.7000.62.50161
- 1.2.840.113556.1.5.7000.62.50162
- 1.2.840.113556.1.5.7000.62.50163
- 1.2.840.113556.1.5.7000.62.50166
- 1.2.840.113556.1.5.7000.62.50164
- 1.2.840.113556.1.5.7000.62.50165
- 1.2.840.113556.1.5.7000.62.50167
- 1.2.840.113556.1.5.7000.62.50170
- 1.2.840.113556.1.5.7000.62.50172
- 1.2.840.113556.1.5.7000.62.50171
- 1.2.840.113556.1.5.7000.62.50173
- 1.2.840.113556.1.5.7000.62.50178
- 1.2.840.113556.1.5.7000.62.50174
- 1.2.840.113556.1.5.7000.62.50176
- 1.2.840.113556.1.5.7000.62.50177
- 1.2.840.113556.1.5.7000.62.50187
- 1.2.840.113556.1.5.7000.62.50188
- 1.2.840.113556.1.5.7000.62.50190
- 1.2.840.113556.1.5.7000.62.50189
- 1.2.840.113556.1.5.7000.62.50191
- 1.2.840.113556.1.5.7000.62.50192

## Indexed attributes added by Exchange 2013 RTM

The following table lists the attributes that are added to the list of indexed attributes when you install Exchange 2013 RTM.

|Attribute|Search flag value|
|---|---|
|ms-Exch-Is-Dirsync-Status-Pending|1|
|ms-Exch-Archive-GUID|9|
|ms-Exch-Accepted-Domain-Name|9|
|ms-Exch-Bypass-Audit|9|
|ms-Exch-Mailbox-Audit-Enable|19|
|ms-Exch-Default-Public-Folder-Mailbox|19|
|ms-Exch-OWA-Set-Photo-URL|16|
|ms-Exch-Organization-Upgrade-Policy-Link|1|
|ms-DS-GeoCoordinates-Altitude|1|
|ms-DS-GeoCoordinates-Latitude|1|
|ms-DS-GeoCoordinates-Longitude|1|
|ms-Exch-Mailbox-Database-Transport-Flags|16|
|ms-Exch-Extension-Custom-Attribute-1|1|
|ms-Exch-Extension-Custom-Attribute-2|1|
|ms-Exch-Extension-Custom-Attribute-3|1|
|ms-Exch-Extension-Custom-Attribute-4|1|
|ms-Exch-Extension-Custom-Attribute-5|1|
|ms-Exch-Recipient-SoftDeleted-Status|27|
|ms-Exch-When-Soft-Deleted-Time|17|
|ms-Exch-Device-Client-Type|1|
|ms-Exch-Team-Mailbox-Expiration|16|
|ms-Exch-Team-Mailbox-Expiry-Days|16|
|ms-Exch-Team-Mailbox-Owners|16|
|ms-Exch-Team-Mailbox-SharePoint-Linked-By|16|
|ms-Exch-Team-Mailbox-SharePoint-Url|16|
|ms-Exch-Team-Mailbox-Show-In-Client-List|16|
|ms-Exch-Home-MDB-SL|1|
|ms-Exch-Home-MTA-SL|1|
|ms-Exch-Mailbox-Move-Source-Archive-MDB-Link-SL|1|
|ms-Exch-Mailbox-Move-Source-MDB-Link-SL|1|
|ms-Exch-Mailbox-Move-Target-Archive-MDB-Link-SL|1|
|ms-Exch-Organization-Upgrade-Policy-Link-SL|1|
|ms-Exch-Previous-Archive-Database-SL|8|
|ms-Exch-Previous-Home-MDB-SL|8|
|ms-Exch-Auth-Issuer-Name|1|
|ms-Exch-Auth-Application-Identifier|1|
|ms-Exch-Transport-Rule-Immutable-Id|1|
|ms-Exch-Public-Folder-EntryId|24|
|ms-Exch-Public-Folder-Mailbox|24|
|ms-Exch-Public-Folder-Smtp-Address|24|
|ms-Exch-Relocate-Tenant-Completion-Target-Vector|8|
|ms-Exch-Relocate-Tenant-Flags|8|
|ms-Exch-Relocate-Tenant-Safe-Lockdown-Schedule|8|
|ms-Exch-Relocate-Tenant-Start-Lockdown|8|
|ms-Exch-Relocate-Tenant-Start-Retired|8|
|ms-Exch-Relocate-Tenant-Start-Sync|8|
|ms-Exch-Relocate-Tenant-Transition-Counter|8|
|ms-Exch-Sync-Cookie|8|
|ms-Exch-Relocate-Tenant-Source-Forest|9|
|ms-Exch-Relocate-Tenant-Status,|9|
|ms-Exch-Relocate-Tenant-Target-Forest|9|

## Global catalog attributes added by Exchange 2013 RTM

The following global catalog attributes are added by Exchange 2013 RTM:

- ms-Exch-Dirsync-Authority-Metadata
- ms-Exch-Dirsync-Status
- ms-Exch-Dirsync-Status-Ack
- ms-Exch-Edge-Sync-Config-Flags
- ms-Exch-Is-Dirsync-Status-Pending
- ms-Exch-Localization-Flags
- ms-Exch-Previous-Archive-Database
- ms-Exch-RoleGroup-Type
- ms-Exch-HAB-Root-Department-Link
- ms-Exch-Default-Public-Folder-Mailbox
- ms-Exch-Team-Mailbox-Expiration
- ms-Exch-Team-Mailbox-Expiry-Days
- ms-Exch-Team-Mailbox-Owners
- ms-Exch-Team-Mailbox-SharePoint-Linked-By
- ms-Exch-Team-Mailbox-SharePoint-Url
- ms-Exch-Team-Mailbox-Show-In-Client-List
- ms-Exch-Recipient-SoftDeleted-Status
- ms-Exch-When-Soft-Deleted-Time
- ms-Exch-Device-Client-Type
- ms-Exch-Extension-Custom-Attribute-1
- ms-Exch-Extension-Custom-Attribute-2
- ms-Exch-Extension-Custom-Attribute-3
- ms-Exch-Extension-Custom-Attribute-4
- ms-Exch-Extension-Custom-Attribute-5
- ms-Exch-Archive-Database-Link-SL
- ms-Exch-Disabled-Archive-Database-Link-SL
- ms-Exch-Home-MDB-SL
- ms-Exch-Home-MTA-SL
- ms-Exch-Mailbox-Move-Source-Archive-MDB-Link-SL
- ms-Exch-Mailbox-Move-Source-MDB-Link-SL
- ms-Exch-Mailbox-Move-Storage-MDB-Link-SL
- ms-Exch-Mailbox-Move-Target-Archive-MDB-Link-SL
- ms-Exch-Mailbox-Move-Target-MDB-Link-SL
- ms-Exch-Previous-Archive-Database-SL
- ms-Exch-Previous-Home-MDB-SL
- ms-Exch-RMS-Computer-Accounts-Link-SL
- ms-Exch-Group-Member-Count
- ms-Exch-Group-External-Member-Count
- ms-Exch-Correlation-Id
- ms-Exch-Relocate-Tenant-Completion-Target-Vector,
- ms-Exch-Relocate-Tenant-Flags
- ms-Exch-Relocate-Tenant-Safe-Lockdown-Schedule
- ms-Exch-Relocate-Tenant-Source-Forest
- ms-Exch-Relocate-Tenant-Start-Lockdown
- ms-Exch-Relocate-Tenant-Start-Retired
- ms-Exch-Relocate-Tenant-Start-Sync
- ms-Exch-Relocate-Tenant-Status
- ms-Exch-Relocate-Tenant-Target-Forest
- ms-Exch-Relocate-Tenant-Transition-Counter
- ms-Exch-Sync-Cookie
