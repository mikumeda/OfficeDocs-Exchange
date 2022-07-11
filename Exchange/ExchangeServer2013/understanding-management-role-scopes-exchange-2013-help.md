---
title: 'Understanding management role scopes: Exchange 2013 Help'
TOCTitle: Understanding management role scopes
ms:assetid: 24ed4a38-438a-4223-9f9c-5d4dea4b046b
ms:mtpsurl: https://technet.microsoft.com/library/Dd335146(v=EXCHG.150)
ms:contentKeyID: 49289199
ms.reviewer: 
ms.topic: article
description: About management role scopes in Microsoft Exchange Server
manager: serdars
ms.author: serdars
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# Understanding management role scopes

_**Applies to:** Exchange Server 2013_

_Management role scopes_ enable you to define the specific scope of impact or influence of a management role when a management role assignment is created. When you apply a scope, the role assignee assigned to the role can only modify the objects contained within that scope. A role assignee can be a management role group, management role, management role assignment policy, user, or universal security group (USG). For more information about management roles, see [Understanding Role Based Access Control](understanding-role-based-access-control-exchange-2013-help.md).

> [!NOTE]
> This topic focuses on advanced RBAC functionality. If you want to manage basic Exchange 2013 permissions, such as using the Exchange admin center (EAC) to add and remove members to and from role groups, create and modify role groups, or create and modify role assignment policies, see [Permissions](permissions-exchange-2013-help.md).

Every management role, whether it's a built-in role or a custom role, has management scopes. Management scopes can be either of the following:

- **Regular**: A _regular scope_ isn't exclusive. It determines where, in Active Directory, objects can be viewed or modified by users assigned the management role. In general, a management role indicates what you can create or modify, and a management role scope indicates where you can create or modify. Regular scopes can be either implicit or explicit scopes, both of which are discussed later in this topic.

- **Exclusive**: An _exclusive scope_ behaves almost the same as a regular scope. The key difference is that it enables you to deny users access to objects contained within the exclusive scope if those users aren't assigned a role associated with the exclusive scope. All exclusive scopes are explicit scopes, which are discussed later in this topic.

    For more information about exclusive scopes, see [Understanding exclusive scopes](understanding-exclusive-scopes-exchange-2013-help.md).

Scopes can be inherited from the management role, specified as a predefined relative scope on a management role assignment, or created using custom filters and added to a management role assignment. Scopes inherited from management roles are called _implicit scopes_ while predefined and custom scopes are called _explicit scopes_. The following sections describe each type of scope:

- Implicit Scopes
- Explicit Scopes
- Predefined Relative Scopes
- Custom Scopes
  - Recipient Filter Scopes
  - Configuration Scopes

Each role can have the following types of scopes:

- **Recipient read scope**: The implicit recipient read scope determines what recipient objects the user assigned the management role is allowed to read from Active Directory.
- **Recipient write scope**: The implicit recipient write scope determines what recipient objects the user assigned the management role is allowed to modify in Active Directory.
- **Configuration read scope**: The implicit configuration read scope determines what configuration objects the user assigned the management role is allowed to read from Active Directory.
- **Configuration write scope**: The implicit configuration write scope determines what organizational, database, and server objects the user assigned the management role is allowed to modify in Active Directory.

Recipient objects include mailboxes, distribution groups, mail enabled users, and other objects. Configuration objects include servers running Microsoft Exchange Server 2013, and databases located on servers running Exchange. Each type of scope can be either an implicit scope or explicit scope.

## Implicit scopes

Implicit scopes are the default scopes that apply to a management role type. Because implicit scopes are associated with a management role type, all of the parent and child management roles with the same role type also have the same implicit scopes. Implicit scopes apply to both built-in management roles and also to custom management roles. For more information about management roles and management role types, see [Understanding management roles](understanding-management-roles-exchange-2013-help.md).

The following tables list all of the implicit scopes that can be defined on management roles.

### Implicit scopes defined on management roles

|Implicit scopes|Description|
|---|---|
|`Organization`|If `Organization` is present in the role's recipient write scope, the role can create or modify recipient objects across the Exchange organization. <br><br> If `Organization` is present in the role's recipient read scope, roles can view any recipient object across the Exchange organization. <br><br> This scope is used only with recipient read and write scopes.|
|`MyGAL`|If `MyGAL` is present in the role's recipient write scope, the role can view the properties of any recipient within the current user's global address list (GAL). <br><br> If `MyGAL` is present in the role's recipient read scope, the role can view the properties of any recipient within the current GAL. <br><br> This scope is used only with recipient read scopes.|
|`Self`|If `Self` is present in the role's recipient write scope, the role can modify only the properties of the current user's mailbox. <br><br> If `Self` is present in the role's recipient read scope, the role can view only the properties of the current user's mailbox. <br><br> This scope is used only with recipient read and write scopes.|
|`MyDistributionGroups`|If `MyDistributionGroups` is present in the role's recipient write scope, the role can create or modify distribution list objects owned by the current user. <br><br> If `MyDistributionGroups` is present in the role's recipient read scope, the role can view distribution list objects owned by the current user. <br><br> This scope is used only with recipient read and write scopes.|
|`OrganizationConfig`|If `OrganizationConfig` is present in the role's configuration write scope, the role can create or modify any server or database configuration object across the Exchange organization. <br><br> If `OrganizationConfig` is present in the role's configuration read scope, the role can view any server or database configuration object across the Exchange organization. <br><br> This scope is used only with configuration read and write scopes.|
|`None`|If `None` is in a scope, that scope isn't available to the role. For example, a role that has `None` in the recipient write scope can't modify recipient objects in the Exchange organization.|

If a role is assigned to a role assignee and no predefined or custom scopes are specified, the implicit scopes defined on the role are used to control the recipient or organization objects the user can view or modify.

The implicit write scope of a role is always equal to, or less than, the implicit read scope. This means that a role can never modify objects that can't be seen by the scope.

You can't change the implicit scopes defined on management roles. You can, however, override the implicit write scope and configuration scope on a management role. When a predefined relative scope or custom scope is used on a role assignment, the implicit write scope of the role is overridden, and the new scope takes precedence. The implicit read scope of a role can't be overridden and always applies. For more information, see Predefined Relative Scopes and Custom Scopes.

Expand the following table to see a list of all the built-in management roles and their implicit scopes. For more information about each built-in role, see [Built-in management roles](built-in-management-roles-exchange-2013-help.md).

## Built-in management role implicit scopes

|Management role|Recipient read scope|Recipient write scope|Configuration read scope|Configuration write scope|
|---|---|---|---|---|
|`Active Directory Permissions`|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|`Address Lists`|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|`ApplicationImpersonation`|`Organization`|`Organization`|`None`|`None`|
|`ArchiveApplication`|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|`Audit Logs`|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|`Cmdlet Extension Agents`|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|`Data Loss Prevention`|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|`Database Availability Groups`|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|`Database Copies`|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|`Databases`|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|`Disaster Recovery`|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|`Distribution Groups`|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|`Edge Subscriptions`|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|`E-Mail Address Policies`|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|`Exchange Connectors`|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|`Exchange Server Certificates`|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|`Exchange Servers`|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|`Exchange Virtual Directories`|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|`Federated Sharing`|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|`Information Rights Management`|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|`Journaling`|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|`Legal Hold`|`Organization`|`Organization`|`OrganizationConfig`|`None`|
|`LegalHoldApplication`|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|`Mail Enabled Public Folders`|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|`Mail Recipient Creation`|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|`Mail Recipients`|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|`Mail Tips`|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|`Mailbox Import Export`|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|`Mailbox Search`|`Organization`|`Organization`|`None`|`None`|
|`MailboxSearchApplication`|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|`Message Tracking`|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|`Migration`|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|`Monitoring`|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|`Move Mailboxes`|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|`OfficeExtensionApplication`|`Self`|`Self`|`OrganizationConfig`|`OrganizationConfig`|
|`My Custom Apps`|`Self`|`Self`|`OrganizationConfig`|`OrganizationConfig`|
|`My Marketplace Apps`|`Self`|`Self`|`OrganizationConfig`|`OrganizationConfig`|
|`MyAddressInformation`|`Self`|`Self`|`OrganizationConfig`|`OrganizationConfig`|
|`MyBaseOptions`|`Self`|`Self`|`OrganizationConfig`|`OrganizationConfig`|
|`MyContactInformation`|`Self`|`Self`|`OrganizationConfig`|`OrganizationConfig`|
|`MyDiagnostics`|`Self`|`Self`|`OrganizationConfig`|`OrganizationConfig`|
|`MyDisplayName`|`Self`|`Self`|`OrganizationConfig`|`OrganizationConfig`|
|`MyDistributionGroupMembership`|`MyGAL`|`MyGAL`|`None`|`None`|
|`MyDistributionGroups`|`MyGAL`|`MyDistributionGroups`|`OrganizationConfig`|`None`|
|`MyMobileInformation`|`Self`|`Self`|`OrganizationConfig`|`OrganizationConfig`|
|`MyName`|`Self`|`Self`|`OrganizationConfig`|`OrganizationConfig`|
|`MyPersonalInformation`|`Self`|`Self`|`OrganizationConfig`|`OrganizationConfig`|
|`MyProfileInformation`|`Self`|`Self`|`OrganizationConfig`|`OrganizationConfig`|
|`MyRetentionPolicies`|`Self`|`Self`|`OrganizationConfig`|`OrganizationConfig`|
|`MyTeamMailboxes`|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|`MyTextMessaging`|`Self`|`Self`|`OrganizationConfig`|`OrganizationConfig`|
|`MyVoiceMail`|`Self`|`Self`|`OrganizationConfig`|`OrganizationConfig`|
|`Organization Client Access`|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|`Organization Configuration`|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|`Organization Transport Settings`|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|`POP3 And IMAP4 Protocols`|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|`Public Folders`|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|`Receive Connectors`|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|`Recipient Policies`|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|`Remote and Accepted Domains`|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|`Reset Password`|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|`Retention Management`|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|`Role Management`|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|`Security Group Creation and Membership`|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|`Send Connectors`|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|`Support Diagnostics`|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|`TeamMailboxLifecycleApplication`|`Self`|`Self`|`OrganizationConfig`|`OrganizationConfig`|
|`Transport Agents`|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|`Transport Hygiene`|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|`Transport Queues`|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|`Transport Rules`|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|`UM Mailboxes`|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|`UM Prompts`|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|`Unified Messaging`|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|`UnScoped Role Management`|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|`UserApplication`|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|`User Options`|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|`View-Only Audit Logs`|`Organization`|`None`|`OrganizationConfig`|`None`|
|`View-Only Configuration`|`Organization`|`None`|`OrganizationConfig`|`None`|
|`View-Only Recipients`|`Organization`|`None`|`OrganizationConfig`|`None`|
|`WorkloadManagement`|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|

## Explicit scopes

Explicit scopes are scopes that you set yourself to control which objects a management role can modify. Although implicit scopes are defined on a management role, explicit scopes are defined on a management role assignment. This enables the implicit scopes to be applied consistently across all management roles unless you choose to use an overriding explicit scope. For more information about management role assignments, see [Understanding management role assignments](understanding-management-role-assignments-exchange-2013-help.md).

Explicit scopes override the implicit write and configuration scopes of a management role. They don't override the implicit read scope of a management role. The implicit read scope continues to define what objects the management role can read.

Explicit scopes are useful when the implicit write scope of a management role doesn't meet the needs of your business. You can add an explicit scope to include nearly anything you want as long as the new scope doesn't exceed the bounds of the implicit read scope. The cmdlets that are part of a management role must be able to read information about the objects or containers that contain objects for the cmdlets to create or modify objects. For example, if the implicit read scope on a management role is set to `Self`, you can't add an explicit write scope of `Organization` because the explicit write scope exceeds the bounds of the implicit read scope.

For more information, see the following sections:

- Predefined Relative Scopes

- Custom Scopes

## Predefined relative scopes

Exchange 2013 provides several predefined relative write scopes that you can use to modify scope of a management role. Predefined relative scopes provide an easy way for you to more closely match the needs of your business without having to create custom scopes manually. They're called relative scopes because they're relative to the role assignee to which the associated role assignment is assigned. For example, the `Self` predefined relative scope restricts that write scope to the current user only. The `MyDistributionGroups` predefined relative scope restricts the write scope to the distribution group the current user owns only. Predefined relative scopes can only be used to scope recipient objects. Predefined relative scopes can't be used to scope configuration objects. The following table lists the predefined relative scopes that you can use.

### Predefined relative scopes

|Implicit scopes|Description|
|---|---|
|`Organization`|If `Organization` is present in the role's recipient write scope, the role can create or modify recipient objects across the Exchange organization. <br><br> If `Organization` is present in the role's recipient read scope, roles can view any recipient object across the Exchange organization. <br><br> This scope is used only with recipient read and write scopes.|
|`Self`|If `Self` is present in the role's recipient write scope, the role can modify only the properties of the current user's mailbox. <br><br> If `Self` is present in the role's recipient read scope, the role can view only the properties of the current user's mailbox. <br><br> This scope is used only with recipient read and write scopes.|
|`MyDistributionGroups`|If `MyDistributionGroups` is present in the role's recipient write scope, the role can create or modify distribution list objects owned by the current user. <br><br> If `MyDistributionGroups` is present in the role's recipient read scope, the role can view distribution list objects owned by the current user. <br><br> This scope is used only with recipient read and write scopes.|

Predefined relative scopes are applied when you create a new management role assignment. During the creation of the role assignment, using the **New-ManagementRoleAssignment** cmdlet, you can specify a predefined relative scope using the _RecipientRelativeWriteScope_ parameter. When the new role assignment is created, the new predefined role overrides the implicit write scope of the management role. You can't specify a custom recipient scope when you create a role assignment with a predefined relative scope. You can, however, specify a custom configuration scope if needed.

For more information about how to add a management role assignment with a predefined relative scope, see [Add a role to a user or USG](add-a-role-to-a-user-or-usg-exchange-2013-help.md).

## Custom scopes

Custom scopes are needed when neither the implicit write scope nor the predefined relative scopes meet the needs of your business. Custom scopes enable you to define, at a granular level, the scope to which your management role will be applied. For example, you might want to target a specific organizational unit (OU), a specific type of recipient, or both. Or, you might only want to allow a group of administrators to be able to manage a specific set of mailbox databases.

As with predefined relative scopes, custom scopes override the implicit write and organization configuration scopes defined on management roles. The implicit read scope on management roles continue to apply and the resulting custom scope must not exceed the boundaries of the implicit read scope. You can create the following three types of custom scopes:

- **OU scope**: An OU scope, which is the simplest custom scope, is created using the _RecipientOrganizationalUnitScope_ parameter on the **New-ManagementRoleAssignment** cmdlet. By specifying an OU scope when a role is assigned, the role assignee assigned the role can modify only recipient objects within that OU. For more information about how to add a management role assignment with an OU scope, see [Add a role to a user or USG](add-a-role-to-a-user-or-usg-exchange-2013-help.md).

- **Recipient filter scope**: Recipient filter scopes use filters to target specific recipients based on recipient type or other recipient properties such as department, manager, location, and more. For more information, see the Recipient Filter Scopes section.

- **Configuration scope**: Configuration scopes use filters or lists to target specific servers based on server lists or filterable properties that can be defined on servers, such as an Active Directory site or a server role. Configuration scopes can also use database scopes to target specific databases based on database lists or filterable database properties. For more information, see the Configuration Scopes section.

Simple and broad or complex and granular recipient and configuration custom scopes can be created by using the **New-ManagementScope** cmdlet. When you create either a recipient or configuration scope, only the recipient, server, or database objects that match their respective scopes are returned. When these scopes are applied to a role assignment using the **New-ManagementRoleAssignment** or **Set-ManagementRoleAssignment** cmdlets, only the objects that match the scopes can be modified by the role assignees who are assigned the role. After a custom scope has been created, you can't change the scope type. A recipient scope is always a recipient scope and a configuration scope is always a configuration scope.

By default, a custom scope enables a role assignee to access a set of objects that match the scopes you define. However, they don't actively exclude access to other role assignees who aren't also assigned the same or equivalent scope. Any custom scope can access the same objects if the lists or filters on those scopes match the same objects. There might be objects where this behavior isn't wanted, such as in the case of executives. For these objects, you can define exclusive scopes. Exclusive scopes use filters or lists in the same way as regular scopes but unlike regular scopes, deny access to objects included in the scope to anyone who isn't part of the same or equivalent exclusive scope. For more information about exclusive scopes, see [Understanding exclusive scopes](understanding-exclusive-scopes-exchange-2013-help.md).

## Recipient filter scopes

Recipient filter scopes enable you to control which recipient objects role assignees can manage by evaluating one or more properties on a recipient object against a value that you specify in a filter statement. Recipients included in recipient scopes are mailboxes, mail-enabled users, distribution groups and mail contacts. Only the recipients that match the filter you specify can be managed by the role assignees assigned that role assignment. An example of a filter statement is `{ Name -Eq "David" }` where **Name** is the property on the recipient object that's being evaluated and **David** is the value you want to evaluate against the property. The **-Eq** comparison operator indicates that the value stored in the property must be equal to the value that was specified for the filter to be true. If the filter is true, that recipient is included in scope.

Recipient filter scopes are created by specifying the recipient filter to use with the _RecipientRestrictionFilter_ parameter on the **New-ManagementScope** cmdlet. By default, the **New-ManagementScope** cmdlet creates regular scopes. If you want to create an exclusive scope, include the _Exclusive_ switch along with the _RecipientRestrictionFilter_ parameter.

When you create a recipient restriction filter, Exchange evaluates the filter you provided against every recipient object in the organization by default. If you want to limit which recipients the scope evaluates, you can use the _RecipientRoot_ parameter along with the _RecipientRestrictionFilter_ parameter. The _RecipientRoot_ parameter accepts an OU. When you use the _RecipientRoot_ parameter, Exchange evaluates only the recipients included in the specified OU against the filter you provided.

When you add a recipient filter scope to a role assignment, specify the name of the recipient scope in the _CustomRecipientWriteScope_ parameter on the **New-ManagementRoleAssignment** if you're creating a new role assignment, or the **Set-ManagementRoleAssignment** cmdlet if you're updating an existing role assignment. Each role assignment can have one recipient scope, including predefined relative scopes. You can add one configuration scope to the same role assignment you added a recipient scope to.

For more information about filter syntax and for a full list of filterable recipient properties on recipients, see [Understanding management role scope filters](understanding-management-role-scope-filters-exchange-2013-help.md).

## Configuration scopes

The following are the two types of configuration scopes offered in Exchange 2013:

- **Server scopes**: There are two types of server scopes, server filter scopes and server list scopes. Server configuration, including Receive connectors, transport queues, server certificates, virtual directories, and so on, can be managed if a server object is included in a server scope.

  - **Server filter scopes**: Server filter scopes enable you to control which server objects role assignees can manage by evaluating one or more properties on a server object against a value that you specify in a filter statement. To create a server filter scope, use the _ServerRestrictionFilter_ parameter on the **New-ManagementScope** cmdlet.

  - **Server list scopes**: Server list scopes enable you to control which server objects role assignees can manage by defining a list of servers that a role assignee can access. To create a server list scope, use the _ServerList_ parameter on the **New-ManagementScope** cmdlet.

- **Database scopes**: There are two types of database scopes, database filter scopes and database list scopes. Database configuration that can be managed if a database object is included in a database scope include database quota limits, database maintenance, public folder replication, whether a database is mounted, and so on. In addition to database configuration, database scopes can also be used to control which databases recipients can be created in. If you have pre-Exchange 2010 SP1 servers in your organization, see the Database scopes and previous versions of Exchange section later in this topic.

  - **Database filter scopes**: Database filter scopes enable you to control which database objects role assignees can manage by evaluating one or more properties on a database object against a value that you specify in a filter statement. To create a database filter scope, use the _DatabaseRestrictionFilter_ parameter on the **New-ManagementScope** cmdlet.

  - **Database list scopes**: Database list scopes enable you to control which database objects role assignees can manage by defining a list of databases that a role assignee can access. To create a database list scope, use the _DatabaseList_ parameter on the **New-ManagementScope** cmdlet.

For more information about filter syntax and for a full list of filterable server and database properties, see [Understanding management role scope filters](understanding-management-role-scope-filters-exchange-2013-help.md).

Server and database lists can be defined by specifying each server and database you want to include in their respective scopes. Multiple servers or databases can be specified in their respective scopes by separating the server and database names with commas.

When you add a server or database configuration scope to a role assignment, specify the name of the server or database configuration scope in the _CustomConfigWriteScope_ parameter on the **New-ManagementRoleAssignment** cmdlet if you're creating a new role assignment, or the **Set-ManagementRoleAssignment** cmdlet if you're updating an existing role assignment. Each role assignment can only have one configuration scope.

In addition to controlling which databases role assignees can manage, database scopes also enable you to control which databases role assignees can create mailboxes on. This is separate from controlling which recipients a role assignee can manage. If a role assignee has permissions to create a new mailbox, mail-enable an existing user, or move mailboxes, you can further refine their permissions by using database scopes to control the database on which the mailbox is created, or which database a mailbox is moved to. Controlling which recipients a role assignee can manage is done using a recipient scope specified in the _CustomRecipientWriteScope_ parameter on the **New-ManagementRoleAssignment** or **Set-ManagementRoleAssignment** cmdlet. Controlling which databases a mailbox can be created on or moved to is controlled using a database scope specified in the _CustomConfigurationWriteScope_ parameter on the same cmdlets.

> [!NOTE]
> Automatic mailbox distribution can be controlled using database scopes.

Exchange features may require either server scopes, database scopes, or both, to be managed. If a feature requires both server and database scopes to be managed, two role assignments must be created and assigned to the role assignee that should have access to manage the feature. One role assignment should be associated with the server scope, and one role assignment should be associated with the database scope.

Some cmdlets may use configuration scopes that aren't immediately obvious. The following table includes a list of cmdlets and the configuration scopes that you can use to control their usage. For cmdlets included in the recipients feature area, configuration scopes enable you to control on which databases recipients can be created. They don't control which recipients can be managed. The **Required scopes** column can contain the following:

- **Database**: To run the cmdlet, the role assignee must be assigned a role assignment with a database scope that includes the database to be managed or the role's implicit configuration write scope must include the database to be managed.

- **Server**: To run the cmdlet, the role assignee must be assigned a role assignment with a server scope that includes the server to be managed or the role's implicit configuration write scope must include the server to be managed.

- **Server or database**: To run the cmdlet, the role assignee must be assigned a role assignment where either a database scope includes the database being managed, or where a server scope includes the server where the database is located. Or, the role's implicit configuration write scope must contain the database to be managed, or contain the server where the database is located, and the role assignment can't have a custom write scope.

- **Server and database**: To run this cmdlet, the role assignee must be assigned two role assignments. The first role assignment must include a database scope that includes the database to be managed. The second role assignment must include a server scope that includes the server where the database is located. The role assignments can have custom configuration scopes defined, or the role assignments can inherit the implicit configuration write scope from the role. To inherit the implicit write scope from the role, the role assignment can't have a custom write scope.

### Feature areas and applicable database and server scopes

|Feature area|Cmdlet|Required scopes|
|---|---|---|
|Databases|**Dismount-Database**|Database|
|Databases|**Mount-Database**|Database|
|Databases|**Move-DatabasePath**|Server and database|
|Databases|**Remove-MailboxDatabase**|Server or database|
|Databases|**Set-MailboxDatabase**|Database|
|High availability|**Add-DatabaseAvailabilityGroupServer**|Server|
|High availability|**Add-MailboxDatabaseCopy**|Server|
|High availability|**Move-ActiveMailboxDatabase**|Server|
|High availability|**Remove-DatabaseAvailabilityGroupServer**|Server|
|High availability|**Remove-MailboxDatabaseCopy**|Server or database|
|High availability|**Resume-MailboxDatabaseCopy**|Server or database|
|High availability|**Set-MailboxDatabaseCopy**|Server or database|
|High availability|**Suspend-MailboxDatabaseCopy**|Server or database|
|High availability|**Update-MailboxDatabaseCopy**|Server or database|
|Recipients|**Connect-Mailbox**|Database|
|Recipients|**Enable-Mailbox**|Database|
|Recipients|**New-Mailbox**|Database|
|Recipients|**New-MoveRequest**|Database|
|Troubleshooting|**Test-MapiConnectivity**|Database|

## Database scopes and previous versions of Exchange

Database scopes were first introduced in Microsoft Exchange 2010 Service Pack 1 (SP1) and continue to be supported in Exchange 2013. Versions of Exchange prior to Exchange 2010 SP1 support only recipient scopes and server configuration scopes. When you create a new database scope on an Exchange 2010 SP1 or later server, you'll receive the following warning:

```console
WARNING: Database management scopes will only be applied when a user connects to a server running Exchange 2010 SP1 or later. Servers running a version of Exchange prior to Exchange 2010 SP1 won't apply any roles from a role assignment linked to a database scope. Database management scopes also won't be visible to the Get-ManagementScope cmdlet when it's run from a pre-Exchange 2010 SP1 server.
```

When you create a database scope, it's only applied to users who connect to servers running Exchange 2010 SP1 or later. Users who connect to pre-Exchange 2010 SP1 servers won't have any role assignments associated with database scopes applied to them. This means that any permissions provided by these role assignments won't be granted to users when they connect to pre-Exchange 2010 SP1 servers. Database scopes can't be created, removed, modified, or viewed from pre-Exchange 2010 SP1 servers.

A database scope can include any database in your Exchange organization. This includes Exchange Server 2007, Exchange 2010, and Exchange 2013 servers. This enables you to control which databases, regardless of Exchange version, that users can manage. As with other database scopes, role assignments associated with database scopes that contain Exchange 2007 and Exchange 2010 databases are only applied to users when they connect to an Exchange 2010 SP1 or later server.

Users who connect to a pre-Exchange 2010 SP1 server can view and modify role assignments associated with database scopes. This includes changing the configuration scope on an existing role assignment to a server scope if it's currently associated with a database scope. However, if the configuration scope on a role assignment is changed to a server scope and a user later wants to change it back to a database scope, or if the user wants to change the configuration scope to another database scope, the user must make the change while connected to an Exchange 2010 SP1 or later server. Users can only specify server scopes when they change the configuration scope on a role assignment if they're connected to a pre-Exchange 2010 SP1 server.
