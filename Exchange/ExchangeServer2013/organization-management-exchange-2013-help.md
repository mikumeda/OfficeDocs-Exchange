---
title: 'Organization Management: Exchange 2013 Help'
TOCTitle: Organization Management
ms:assetid: 0bfd21c1-86ac-4369-86b7-aeba386741c8
ms:mtpsurl: https://technet.microsoft.com/library/Dd335087(v=EXCHG.150)
ms:contentKeyID: 49289160
ms.topic: article
description: Organization Management management role group is part of RBAC.
ms.reviewer: 
manager: serdars
ms.author: serdars
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# Organization Management

_**Applies to:** Exchange Server 2013_

The Organization Management management role group is one of several built-in role groups that make up the Role Based Access Control (RBAC) permissions model in Microsoft Exchange Server 2013. Role groups are assigned one or more management roles that contain the permissions required to perform a given set of tasks. The members of a role group are granted access to the management roles assigned to the role group. For more information about role groups, see [Understanding management role groups](understanding-management-role-groups-exchange-2013-help.md).

Administrators that are members of the Organization Management role group have administrative access to the entire Exchange 2013 organization and can perform almost any task against any Exchange 2013 object, with some exceptions. By default, members of this role group can't perform mailbox searches and management of unscoped top-level management roles. For more information, see the "Delegating Only Role Assignments" section later in this topic.

> [!IMPORTANT]
> The Organization Management role group is a very powerful role and as such, only users or universal security groups (USGs) that perform organizational-level administrative tasks that can potentially impact the entire Exchange organization should be members of this role group.

This role group is equivalent to the Exchange Organization Administrators role in Exchange Server 2007.

For more information about RBAC, see [Understanding Role Based Access Control](understanding-role-based-access-control-exchange-2013-help.md).

## Role group membership

By default, the account that's used to install Exchange 2013 in the organization is added as a member of the Organization Management role group. This account can then add other members to the role group as needed.

If you want to add or remove members to or from this role group, see [Manage role group members](manage-role-group-members-exchange-2013-help.md).

By default, only members of the Organization Management role group can add or remove members from this role group. For more information about how to add additional role group delegates, see the "Add or remove a role group delegate" section in [Manage role groups](manage-role-groups-exchange-2013-help.md).

You can use the following command to view a list of users or USGs that are members of this role group.

```powershell
Get-RoleGroupMember "Organization Management"
```

For more information about the members of a role group, see [Manage role groups](manage-role-groups-exchange-2013-help.md).

## Role group customization

This role group is assigned management roles by default. The roles that are included are listed in the "Management Roles Assigned to this Role Group" section. You can add or remove role assignments to or from this role group to match the needs of your organization.

The role groups provided with Exchange 2013 are designed to match more granular tasks. By assigning roles to a role group, you enable the members of that role group to perform the tasks associated with the role. For example, the Journaling role enables the management of the Journaling agent and journaling rules. For more information about how roles are assigned to role groups, see [Understanding management role assignments](understanding-management-role-assignments-exchange-2013-help.md).

The roles assigned to this role group are given default management scopes. Management scopes determine what Exchange objects can be viewed or modified by the members of a role group. You can change the scopes associated with assignments between roles and role groups. For example, you might want to do this if you only want members of a role group to be able to change recipients that are under a specific organizational unit or in a specific location. For more information about management scopes, see [Understanding management role scopes](understanding-management-role-scopes-exchange-2013-help.md).

For more information about how to customize this role group, see the following topics:

- [Manage role groups](manage-role-groups-exchange-2013-help.md)
- [Manage role group members](manage-role-group-members-exchange-2013-help.md)

If you want to create a role group and assign some of the roles that are assigned to this role group to the new role group, see the "Create a role group" section in [Manage role groups](manage-role-groups-exchange-2013-help.md).

The following are some ways you might want to customize this role:

- **Permissions owner**: If the permissions in your organization are controlled by a specific group other than the Exchange administrators, you can create a role group and move the regular and delegating role assignments for the Role Management role to the new role group. Doing so prevents members of the Organization Management role group from managing any RBAC permissions.
- **Active Directory split permissions**: If the creation of security principals in your organization, such as user accounts, is controlled by a specific group other than the Exchange administrators, you can create a role group and move the regular and delegating role assignments for the Mail Recipient Creation role and the Security Group Creation and Membership role to the new role group. Doing so prevents members of the Organization Management role group from creating Active Directory objects. They can, however, continue to mail-enable the new Active Directory objects. For more information about split permissions, see [Understanding split permissions](understanding-split-permissions-exchange-2013-help.md).

## Customization limitations

Any role can be added to or removed from this role group, with the following limitations:

- Every role must have at least one delegating role assignment to a role group or USG before the delegating role assignment can be removed from this role group.
- The Role Management role must have at least one regular role assignment to a role group or USG before the regular role assignment can be removed from this role group.

These limitations are intended to help prevent you from inadvertently locking yourself out of the system. By requiring that at least one delegating role assignment exists between every role and one or more role groups or USGs, you will always be able to assign roles to role assignees. By requiring that at least one regular role assignment exists between the Role Management role and one or more role groups or USGs, you will always be able to configure role groups and role assignments.

> [!IMPORTANT]
> These limitations require that role groups or USGs be the targets of the delegating and regular role assignments. You can't remove a delegating role assignment or the regular assignment for the Role Management role if the last assignment is to a user.

## Delegating only role assignments

Some role assignments between the Organization Management role group and management roles, such as Mailbox Search and Unscoped Role Management, are delegating only role assignments. These roles allow access to sensitive or personal information, such as the contents of mailboxes, or enable the creation of powerful unscoped management roles.

Delegating only role assignments enable members of the Organization Management role group only to assign the associated roles to other role groups, management role assignment policies, users, or USGs. Members of the Organization Management role group aren't given, by default, any permissions that the roles provide. This helps avoid accidental exposure to personal information or accidental elevation of privileges.

Members of the Organization Management role group can, however, assign themselves any role, in effect enabling them to perform any task. For example, a member of the Organization Management role group can assign the Mailbox Search role to the Organization Management role group. After this role assignment is made, members of the Organization Management role group can perform tasks enabled by the Mailbox Search role.

For more information about delegating role assignments, see [Understanding management role assignments](understanding-management-role-assignments-exchange-2013-help.md).

## Additional permissions

The permissions granted to members of the Organization Management role group are primarily determined by the management roles assigned to the role group. However, not all tasks that you need to perform are covered by management roles. Some tasks occur outside of the Exchange management tools, and therefore the RBAC permissions model doesn't apply. For these tasks, permissions are provided by adding the Organization Management role group to the access control lists (ACLs) of certain Active Directory objects.

The following tasks are granted permissions by way of ACLs on Active Directory objects and not by management roles assigned to the Organization Management role group:

- Running DomainPrep and ForestPrep using Setup.exe
- Deploying additional servers in the organization

## Management roles assigned to this role group

The following table lists all the management roles that are assigned to this role group and the following attributes of each role assignment:

- **Regular assignment**: Enables members of the role group to access the management role entries made available by the associated management role.
- **Delegating assignment**: Gives members of the role group the ability to assign the specified role to other role groups, role assignment policies, users, or USGs.
- **Recipient read scope**: Determines what recipient objects members of the role group are allowed to read from Active Directory.
- **Recipient write scope**: Determines what recipient objects members of the role group are allowed to modify in Active Directory.
- **Configuration read scope**: Determines what configuration and server objects members of the role group are allowed to read from Active Directory.
- **Configuration write scope**: Determines what organizational and server objects members of the role group are allowed to modify in Active Directory.

For more information about role assignments and management scopes, see the following topics:

- [Understanding management role assignments](understanding-management-role-assignments-exchange-2013-help.md)
- [Understanding management role scopes](understanding-management-role-scopes-exchange-2013-help.md)

|Management role|Regular assignment|Delegating assignment|Recipient read scope|Recipient write scope|Configuration read scope|Configuration write scope|
|---|:---:|:---:|---|---|---|---|
|[Active Directory Permissions role](active-directory-permissions-role-exchange-2013-help.md)|X|X|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|[Address Lists role](address-lists-role-exchange-2013-help.md)|X|X|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|[ApplicationImpersonation role](applicationimpersonation-role-exchange-2013-help.md)||X|`Organization`|`Organization`|`None`|`None`|
|[ArchiveApplication role](archiveapplication-role-exchange-2013-help.md)|X|X|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|[Audit Logs role](audit-logs-role-exchange-2013-help.md)|X|X|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|[Cmdlet Extension Agents role](cmdlet-extension-agents-role-exchange-2013-help.md)|X|X|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|[Data Loss Prevention role](data-loss-prevention-role-exchange-2013-help.md)|X|X|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|[Database Availability Groups role](database-availability-groups-role-exchange-2013-help.md)|X|X|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|[Database Copies role](database-copies-role-exchange-2013-help.md)|X|X|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|[Databases role](databases-role-exchange-2013-help.md)|X|X|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|[Disaster Recovery role](disaster-recovery-role-exchange-2013-help.md)|X|X|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|[Distribution Groups role](distribution-groups-role-exchange-2013-help.md)|X|X|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|[Edge Subscriptions role](edge-subscriptions-role-exchange-2013-help.md)|X|X|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|[E-Mail Address Policies role](e-mail-address-policies-role-exchange-2013-help.md)|X|X|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|[Exchange Connectors role](exchange-connectors-role-exchange-2013-help.md)|X|X|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|[Exchange Server Certificates role](exchange-server-certificates-role-exchange-2013-help.md)|X|X|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|[Exchange Servers role](exchange-servers-role-exchange-2013-help.md)|X|X|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|[Exchange Virtual Directories role](exchange-virtual-directories-role-exchange-2013-help.md)|X|X|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|[Federated Sharing role](federated-sharing-role-exchange-2013-help.md)|X|X|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|[Information Rights Management role](information-rights-management-role-exchange-2013-help.md)|X|X|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|[Journaling role](journaling-role-exchange-2013-help.md)|X|X|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|[Legal Hold role](legal-hold-role-exchange-2013-help.md)|X|X|`Organization`|`Organization`|`OrganizationConfig`|`None`|
|[LegalHoldApplication role](legalholdapplication-role-exchange-2013-help.md)||X|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|[Mail Enabled Public Folders role](mail-enabled-public-folders-role-exchange-2013-help.md)|X|X|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|[Mail Recipient Creation role](mail-recipient-creation-role-exchange-2013-help.md)|X|X|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|[Mail Recipients role](mail-recipients-role-exchange-2013-help.md)|X|X|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|[Mail Tips role](mail-tips-role-exchange-2013-help.md)|X|X|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|[Mailbox Import Export role](mailbox-import-export-role-exchange-2013-help.md)||X|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|[Mailbox Search role](mailbox-search-role-exchange-2013-help.md)||X|`Organization`|`Organization`|`None`|`None`|
|[MailboxSearchApplication role](mailboxsearchapplication-role-exchange-2013-help.md)||X|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|[Message Tracking role](message-tracking-role-exchange-2013-help.md)|X|X|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|[Migration role](migration-role-exchange-2013-help.md)|X|X|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|[Monitoring role](monitoring-role-exchange-2013-help.md)|X|X|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|[Move Mailboxes role](move-mailboxes-role-exchange-2013-help.md)|X|X|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|[OfficeExtensionApplication role](officeextensionapplication-role-exchange-2013-help.md)||X|`Self`|`Self`|`OrganizationConfig`|`OrganizationConfig`|
|[Organization Client Access role](organization-client-access-role-exchange-2013-help.md)|X|X|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|[Organization Configuration role](organization-configuration-role-exchange-2013-help.md)|X|X|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|[Organization Transport Settings role](organization-transport-settings-role-exchange-2013-help.md)|X|X|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|[POP3 and IMAP4 Protocols role](pop3-and-imap4-protocols-role-exchange-2013-help.md)|X|X|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|[Public Folders role](public-folders-role-exchange-2013-help.md)|X|X|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|[Receive Connectors role](receive-connectors-role-exchange-2013-help.md)|X|X|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|[Recipient Policies role](recipient-policies-role-exchange-2013-help.md)|X|X|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|[Remote and Accepted Domains role](remote-and-accepted-domains-role-exchange-2013-help.md)|X|X|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|[Reset Password role](reset-password-role-exchange-2013-help.md)||X|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|[Retention Management role](retention-management-role-exchange-2013-help.md)|X|X|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|[Role Management role](role-management-role-exchange-2013-help.md)|X|X|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|[Security Group Creation and Membership role](security-group-creation-and-membership-role-exchange-2013-help.md)|X|X|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|[Send Connectors role](send-connectors-role-exchange-2013-help.md)|X|X|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|[Support Diagnostics role](support-diagnostics-role-exchange-2013-help.md)||X|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|[TeamMailboxLifecycleApplication role](teammailboxlifecycleapplication-role-exchange-2013-help.md)||X|`Self`|`Self`|`OrganizationConfig`|`OrganizationConfig`|
|[Transport Agents role](transport-agents-role-exchange-2013-help.md)|X|X|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|[Transport Hygiene role](transport-hygiene-role-exchange-2013-help.md)|X|X|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|[Transport Queues role](transport-queues-role-exchange-2013-help.md)|X|X|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|[Transport Rules role](transport-rules-role-exchange-2013-help.md)|X|X|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|[UM Mailboxes role](um-mailboxes-role-exchange-2013-help.md)|X|X|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|[UM Prompts role](um-prompts-role-exchange-2013-help.md)|X|X|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|[Unscoped Role Management role](unscoped-role-management-role-exchange-2013-help.md)||X|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|[Unified Messaging role](unified-messaging-role-exchange-2013-help.md)|X|X|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|[UserApplication role](userapplication-role-exchange-2013-help.md)||X|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|[User Options role](user-options-role-exchange-2013-help.md)|X|X|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|[View-Only Audit Logs role](view-only-audit-logs-role-exchange-2013-help.md)|X|X|`Organization`|`None`|`OrganizationConfig`|`None`|
|[View-Only Configuration role](view-only-configuration-role-exchange-2013-help.md)|X|X|`Organization`|`None`|`OrganizationConfig`|`None`|
|[View-Only Recipients role](view-only-recipients-role-exchange-2013-help.md)|X|X|`Organization`|`None`|`OrganizationConfig`|`None`|
|[WorkloadManagement role](workloadmanagement-role-exchange-2013-help.md)|X|X|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|[My Custom Apps role](my-custom-apps-role-exchange-2013-help.md)||X|`Self`|`Self`|`OrganizationConfig`|`OrganizationConfig`|
|[My Marketplace Apps role](my-marketplace-apps-role-exchange-2013-help.md)||X|`Self`|`Self`|`OrganizationConfig`|`OrganizationConfig`|
|[MyBaseOptions role](mybaseoptions-role-exchange-2013-help.md)||X|`Self`|`Self`|`OrganizationConfig`|`OrganizationConfig`|
|[MyContactInformation role](mycontactinformation-role-exchange-2013-help.md)||X|`Self`|`Self`|`OrganizationConfig`|`OrganizationConfig`|
|[MyDiagnostics role](mydiagnostics-role-exchange-2013-help.md)||X|`Self`|`Self`|`OrganizationConfig`|`OrganizationConfig`|
|[MyDistributionGroupMembership role](mydistributiongroupmembership-role-exchange-2013-help.md)||X|`MyGAL`|`MyGAL`|`None`|`None`|
|[MyDistributionGroups role](mydistributiongroups-role-exchange-2013-help.md)||X|`MyGAL`|`MyDistributionGroups`|`OrganizationConfig`|`None`|
|[MyProfileInformation role](myprofileinformation-role-exchange-2013-help.md)||X|`Self`|`Self`|`OrganizationConfig`|`OrganizationConfig`|
|[MyRetentionPolicies role](myretentionpolicies-role-exchange-2013-help.md)||X|`Self`|`Self`|`OrganizationConfig`|`OrganizationConfig`|
|[MyTeamMailboxes role](myteammailboxes-role-exchange-2013-help.md)||X|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|[MyTextMessaging role](mytextmessaging-role-exchange-2013-help.md)||X|`Self`|`Self`|`OrganizationConfig`|`OrganizationConfig`|
|[MyVoiceMail role](myvoicemail-role-exchange-2013-help.md)||X|`Self`|`Self`|`OrganizationConfig`|`OrganizationConfig`|
