---
title: 'Understanding management role scope filters: Exchange 2013 Help'
TOCTitle: Understanding management role scope filters
ms:assetid: 6acc2922-ee9c-41f1-8a0f-10a541e8c273
ms:mtpsurl: https://technet.microsoft.com/library/Dd298043(v=EXCHG.150)
ms:contentKeyID: 49289288
ms.reviewer: 
ms.topic: article
description: Understand management role scope filters in Microsoft Exchange Server
manager: serdars
ms.author: serdars
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# Understanding management role scope filters

_**Applies to:** Exchange Server 2013_

Management role scope filters can be used to define management scopes that are highly customizable. Using scope filters, you can create a scope that matches how you segment your recipients, databases, and servers so that administrators can manage only those objects they should have access to. Scope filters can use nearly any recipient, database, or server object property.

To use management role scope filters, you must be familiar with management role scopes. For more information about management role scopes, see [Understanding management role scopes](understanding-management-role-scopes-exchange-2013-help.md).

Filtered custom scopes in Microsoft Exchange Server 2013 are created by using the **New-ManagementScope** cmdlet. The two types of filtered scopes, recipient and configuration (which consists of server and database scopes), are divided into regular scopes and exclusive scopes. The following list shows which parameter on the **New-ManagementScope** cmdlet to use to create each type of filtered scope:

- **Recipient regular filtered scope**: To create this type of filtered scope, use the _RecipientRestrictionFilter_ parameter.
- **Recipient exclusive filtered scope**: To create this type of filtered scope, use the _RecipientRestrictionFilter_ parameter along with the _Exclusive_ switch.
- **Server-based configuration regular filtered scope**: To create this type of filtered scope, use the _ServerRestrictionFilter_ parameter.
- **Server-based configuration exclusive filtered scope**: To create this type of filtered scope, use the _ServerRestrictionFilter_ parameter along with the _Exclusive_ switch.
- **Database-based configuration regular filtered scope**: To create this type of filtered scope, use the _DatabaseRestrictionFilter_ parameter.
- **Database-based configuration exclusive filtered scope**: To create this type of filtered scope, use the _DatabaseRestrictionFilter_ parameter along with the _Exclusive_ switch.

When you create a filtered custom scope, the scope attempts to match the filter with any objects accessible within the implicit read scope of the management role. If an object is found, it's included in the results returned by the filter, and the object is made available to the management role by the custom scope. A filter can't return results that are outside of the implicit read scope of the management role.

If you specify a recipient filter using the _RecipientRestrictionFilter_ parameter, you can use the _RecipientRoot_ parameter to specify an organizational unit (OU) to restrict the filter to. When you specify an OU in the _RecipientRoot_ parameter, the recipient filter attempts to match recipients that reside in that OU only, rather than within the entire implicit read scope.

To create a management scope using the filterable properties included in this topic, see [Create a regular or exclusive scope](create-a-regular-or-exclusive-scope-exchange-2013-help.md).

## Filter syntax

Both recipient and configuration filters use the same syntax to create a filter query. All filter queries must have, at minimum, the following components:

- **Opening bracket**: The opening brace ({) indicates the start of the filter query.

- **Property to examine**: The property is the value on an object that you want to test. For example, this can be the city or department on a recipient object, an Active Directory site name or server name on a server configuration object, or a database name on a database configuration object.

- **Comparison operator**: The comparison operator directs how the query should evaluate the value that you specify against the value that's stored in the property. For example, comparison operators can be **Eq**, which means equal to; **Ne**, which means not equal to; **Like**, which means similar to, and so on. For a full list of operators that you can use in the Exchange Management Shell, see [Comparison operators](/powershell/module/microsoft.powershell.core/about/about_comparison_operators).

- **Value to compare**: The value you specify in the filter query will be compared to the value that's stored in the property you specified. The value you specify must be enclosed in quotation marks ("). If you want to specify a partial string, you can enclose the string you provide in wildcard characters (\*) and use a comparison operator that supports wildcard characters, such as **Like**. Any string that contains the partial string will match the filter query.

- **Closing bracket**: The closing brace (}) indicates the end of the filter query.

The following components are optional and enable you to create more complex filter queries:

- **Parentheses**: As in mathematics, parentheses, ( ), in a filter query enable you to force the order in which an operation occurs. Innermost parentheses are evaluated first and the filter query works outward to the outermost parentheses.

- **Logical operators**: Logical operators tie together one or more comparison operations and require the filter query to evaluate the entire statement. For example, logical operators include **And**, **Or**, and **Not**.

When put together, a simple query looks like `{ City -Eq "Vancouver" }`. This filter matches any recipient where the value in the property **City** equals the string "Vancouver".

Another, more complex, query is `{((City -Eq "Vancouver") -And (Department -Eq "Sales")) -Or (Title -Like "*Manager*")}`. The filter query is evaluated in the following order:

1. The properties **City** and **Department** are evaluated. Each is set to either `True` or `False`, depending on the values stored in each property.

2. The results of the **City** and **Department** statements are then evaluated. If both are `True`, the entire **And** statement becomes `True`. If one or both are `False`, the entire **And** statement becomes `False`. The following applies:

   - If the **And** statement evaluates as `True`, the entire filter query becomes `True` because the **Or** operator indicates that one side of the query, or the other, must be `True`. The object is exposed to the role assignment.
   - If the **And** statement is `False`, the filter query continues on to evaluate the **Title** property.

3. The **Title** property is then evaluated. It's set to `True` or `False`, depending on the value that's stored in the **Title** property. The following applies:

   - If the **Title** property evaluates as `True`, the entire filter query becomes `True` because the **Or** operator indicates that one side of the query, or the other, must be `True`. The object is exposed to the role assignment.
   - If the **Title** property evaluates as `False`, the entire filter query evaluates as `False`, and the object isn't exposed to the role assignment.

The following table shows an example with values, which indicates when the complex query would evaluate as `True`, and when it would evaluate as `False`.

### Complex query

|City|Department|Title|Result|
|---|---|---|---|
|Vancouver (True)|Sales (True)|CEO (False)|True because both **City** and **Department** evaluated as True. **Title** isn't evaluated because the filter query conditions are already satisfied.|
|Seattle (False)|Sales (True)|IT Manager (True)|True because **Title** evaluated as True. The results of the **City** and **Department** comparison are discarded because **Title** evaluated as True, which satisfied the filter query conditions. <br/><br/> **Note**: IT Manager matches the filter query because the **Like** comparison operator was used, which matches partial strings when wildcard characters (\*) are used in the filter query.|
|Vancouver (True)|Marketing (False)|Writer (False)|False because **City** and **Department** didn't both evaluate as True, and **Title** also didn't evaluate as True.|

## Filterable recipient properties

You can use almost any property on a recipient object when you create a recipient filter. For a list of filterable recipient properties, see [Filterable properties for the -RecipientFilter parameter](/powershell/exchange/recipientfilter-properties). Although this topic discusses the properties that can be used with the _RecipientFilter_ parameter on other cmdlets, most of these properties also work with the _RecipientRestrictionFilter_ parameter on the **New-ManagementScope** cmdlet.

## Filterable server properties

You can use the following server properties when you create a management scope with the _ServerRestrictionFilter_ parameter:

- **CurrentServerRole**
- **CustomerFeedbackEnabled**
- **DataPath**
- **DistinguishedName**
- **ExchangeLegacyDN**
- **ExchangeLegacyServerRole**
- **ExchangeVersion**
- **Fqdn**
- **Guid**
- **InternetWebProxy**
- **Name**
- **NetworkAddress**
- **ObjectCategory**
- **ObjectClass**
- **ProductID**
- **ServerRole**
- **ServerSite**
- **WhenChanged**
- **WhenChangedUTC**
- **WhenCreated**
- **WhenCreatedUTC**

## Filterable database properties

You can use the following database properties when you create a management scope with the _DatabaseRestrictionFilter_ parameter:

- **AdminDisplayName**
- **AllowFileRestore**
- **BackgroundDatabaseMaintenance**
- **CircularLoggingEnabled**
- **DatabaseCreated**
- **DeletedItemRetention**
- **Description**
- **DistinguishedName**
- **EdbFilePath**
- **EventHistoryRetentionPeriod**
- **ExchangeLegacyDN**
- **ExchangeVersion**
- **Guid**
- **IssueWarningQuota**
- **LogFilePrefix**
- **LogFileSize**
- **LogFolderPath**
- **MasterServerOrAvailabilityGroup**
- **MountAtStartup**
- **Name**
- **ObjectCategory**
- **ObjectClass**
- **RetainDeletedItemsUntilBackup**
- **Server**
- **WhenChanged**
- **WhenChangedUTC**
- **WhenCreated**
- **WhenCreatedUTC**
