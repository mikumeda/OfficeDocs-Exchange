---
title: "Hybrid Configuration wizard"
ms.author: serdars
author: msdmaguire
manager: serdars
f1.keywords:
- NOCSH
audience: ITPro
ms.topic: article
ms.prod: exchange-server-it-pro
ms.localizationpriority: medium
ms.collection:
- Strat_EX_EXOBlocker
- Ent_O365_Hybrid
- Hybrid
- M365-email-calendar
ms.assetid: 2e6ed294-ee74-4038-8b71-b61786372ba4
ms.reviewer:
description: "Admins can learn about Exchange Hybrid configuration and the Hybrid Configuration wizard."
---

# Hybrid Configuration wizard

This article gives you an overview of the Exchange hybrid deployment process using the Hybrid Configuration Wizard.

For more information about hybrid deployments, check out [Exchange Server Hybrid Deployments](exchange-hybrid.md).

## Hybrid configuration process
<a name="BKMK_HybridConfigProcess"> </a>

Here's a quick overview of what the Hybrid Configuration Wizard does:

1. Create the **HybridConfiguration** object in your on-premises Active Directory. This object stores the hybrid configuration information for the hybrid deployment.
2. Complete the following steps:
   1. Gather existing on-premises Exchange and Active Directory topology configuration data, cloud organization data, and Exchange Online configuration data.
   2. Define several organization parameters.
   3. Run an extensive sequence of configuration tasks in both on-premises Exchange and Exchange Online.

> [!IMPORTANT]
> There are several important considerations and prerequisites that you need to complete before you use the Hybrid Configuration wizard. These requirements are describe in [Hybrid deployment prerequisites](hybrid-deployment-prerequisites.md). After you meet all of these requirements, you'll be ready to use the Hybrid Configuration wizard.

The general phases of the hybrid deployment configuration process are described in the following:

1. **Verify prerequisites and do topology checks**: Verify that your on-premises and Exchange Online organizations can support a hybrid deployment. For example, the following items are checked:

   - On-premises Exchange server versions.
   - Exchange Online version.
   - Active Directory synchronization presence and configuration.
   - Federated and accepted domains.
   - Existing federation trust and organization relationships.
   - Web Services virtual directories.
   - Exchange certificates.

2. **Test account credentials**: Verify that the on-premises and cloud accounts have the appropriate permissions to connect to both environments. Hybrid deployment management accounts require the following role group memberships:
   - Organization Management role group in on-premises Exchange
   - Global admins in Microsoft 365.

3. **Hybrid deployment configuration changes**: Make the required configuration changes to create and enable the hybrid deployment. All changes are automatically logged in the hybrid configuration log. By default, the hybrid configuration log is located on the on-premises Mailbox server at `%UserProfile%\AppData\Roaming\Microsoft\Exchange Hybrid Configuration`.

    > [!IMPORTANT]
    > Inbound mail flow is controlled by your organization's MX record. Inbound internet mail for a hybrid deployment isn't configured by the Hybrid Configuration wizard.

## Hybrid configuration features
<a name="BKMK_HybridConfigFeatures"> </a>

By default, the Hybrid Configuration wizard automatically enables all hybrid deployment features each time it runs. To disable specific hybrid configuration features, you need to use the **Set-HybridConfiguration** in the Exchange Management Shell. By default, the following hybrid deployment features are enabled by the wizard:

- **Free/busy sharing**: Enables calendar information to be shared between on-premises and Exchange Online users. Free/busy sharing is enabled as part of the federated sharing and organization relationship configuration for on-premises and cloud environments. Learn more at [Sharing](../ExchangeServer2013/sharing-exchange-2013-help.md).

- **MailTips**: MailTips are informative messages that users see as they compose messages. Users can adjust messages before they're sent to avoid undesirable situations or non-delivery reports (NDRs). For more information, see [MailTips in Exchange](../ExchangeServer2013/mailtips-exchange-2013-help.md) and [MailTips in Exchange Online](../ExchangeOnline/clients-and-mobile-in-exchange-online/mailtips/mailtips.md).

- **Online archiving**: Exchange Online host user email archive for both on-premises and cloud users. For more information, see [Configure Exchange Online Archiving](/microsoft-365/compliance/enable-archive-mailboxes).

- **Outlook on the web redirection**: Provides one URL to access both on-premises and Exchange Online mailboxes via Outloo on the web (formerly known as Outlook Web App or OWA). Client Access servers automatically redirect requests to on-premises mailbox servers or provide the link to Exchange Online mailboxes.

- **Exchange ActiveSync redirection**: Most Exchange ActiveSync clients will now be automatically reconfigured when the mailbox is moved to Exchange Online. For more information, see [Exchange ActiveSync device settings with Exchange hybrid deployments](activesync-settings.md).

- **Secure mail**: Uses Transport Layer Security (TLS) for secure mail delivery between the on-premises and cloud environments. On-premises Exchange and Exchange Online are mutually authenticated through digital certificate subjects and email headers. Rich-text message formatting is preserved across the organizations.

## Hybrid configuration options
<a name="BKMK_HybridConfigOptions"> </a>

The Hybrid Configuration wizard allows a lot of customization for the hybrid deployment. To update a hybrid configuration setting after you initially configured hybrid, you can the Hybrid Configuration wizard or the Exchange Management Shell.

The following table describes the major options:

|Configuration area|Description|
|---|---|
|Domains|Adds Exchange Online as accepted domain to on-premises Exchange for hybrid mail flow and Autodiscover requests. By default, this domain is `<domain>.mail.onmicrosoft.com`, and is called the _coexistence domain_. The coexistence domain is used for secondary email addresses (proxy addresses) in any email address policies that contain the domains you specified in the Hybrid Configuration Wizard. <p> You can view the accepted domain by running the following command Exchange Online PowerShell: `Get-AcceptedDomain | Format-List DomainName, IsCoexistenceDomain`.|
|Secure mail certificate|Select certificate that was issued by a trusted third-party Certificate Authority (CA). This certificate is used to authenticate and secure mail sent between the on-premises and Exchange Online organizations.|
|Exchange federated sharing|If an existing OAuth relationship or federation trust between Azure Active Directory and on-premises Exchange is found, that OAuth relationship or trust is used for the hybrid deployment. If not, the wizard configures OAuth authentication or creates a federation trust between Azure Active Directory and on-premises Exchange. Any domains that you selected in the Hybrid Configuration Wizard are added to the federation trust as needed. <p> The wizard also creates and configures organizational relationships for both the on-premises and Exchange Online organizations. These organization relationships allow the wizard to enable several hybrid deployment features: <ul><li>Free/busy sharing</li><li>Outlook on the web redirection</li><li>MailTIps</li></ul> <p> **Note**: GCC High and DoD environments require a different value for the _MetadataUrl_ parameter on the **Set-FederationTrust** cmdlet. For more information, see [Set-FederationTrust](/powershell/module/exchange/set-federationtrust).|
|Mail flow|Client Access servers</li><li>Exchange 2010: Hub Transport servers</li></ul> <p> The wizard configures any new and existing connectors as required: <ul><li>On-premises Exchange: Send connectors and Receive connectors</li><li>Exchange Online: Inbound and Outbound connectors</li></ul> <p> For Exchange Online, you choose how to route outbound messages to the internet: <ul><li>Direct</li><li>Routed through your on-premises Exchange servers</li></ul> <p> **Important**: Mail flow form the internet to recipients in your domain is controlled by the domain's MX record in DNS, not by the Hybrid Configuration wizard.|

## Hybrid Configuration Engine
<a name="BKMK_RecommendedToolsAndServices"> </a>

The Hybrid Configuration Engine runs the core actions for configuring and updating a hybrid deployment, based on the `Update-HybridConfiguration` cmdlet. The Hybrid Configuration Engine compares the state of the _HybridConfiguration_ Active Directory object with current on-premises Exchange and Exchange Online configuration settings. Tasks are run to match the deployment configuration settings to the parameters that are defined in the _HybridConfiguration_ Active Directory object. No changes are made if the current configuration states already match what's defined in the _HybridConfiguration_ Active Directory object.

The Hybrid Configuration Engine does the following steps to compare and update an existing hybrid deployment:

1. The _Update-HybridConfiguration_ cmdlet triggers the Hybrid Configuration Engine to start.
2. The Hybrid Configuration Engine reads the "desired state" stored on the `HybridConfiguration` Active Directory object.
3. The Hybrid Configuration Engine discovers topology data and current configuration from the on-premises Exchange organization.
4. The Hybrid Configuration Engine discovers topology data and current configuration from the Exchange Online organization.
5. The Hybrid Configuration Engine establishes the "difference" between the on-premises Exchange and Exchange Online organizations.
6. The Hybrid Configuration Engine runs configuration tasks to establish the desired state.

The following figure describes how the Hybrid Configuration Engine retrieves and modifies configuration settings during the hybrid deployment process.

![Hybrid Configuration Engine flow.](media/HybridConfigurationEngine.gif)
