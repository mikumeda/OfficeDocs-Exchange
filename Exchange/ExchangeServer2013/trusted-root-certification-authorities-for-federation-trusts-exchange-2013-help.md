---
title: 'Trusted root certification authorities for federation trusts'
TOCTitle: Trusted root certification authorities for federation trusts
ms:assetid: d4224bf5-69b3-484c-8a70-4f230d3dbdd9
ms:mtpsurl: https://technet.microsoft.com/library/Ee332350(v=EXCHG.150)
ms:contentKeyID: 48385572
ms.reviewer: 
manager: serdars
ms.author: serdars
ms.topic: article
description: Trusted root certification authorities for federation trusts in Microsoft Exchange Server
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# Trusted root certification authorities for federation trusts

_**Applies to:** Exchange Server 2013_

To establish a federation trust between your Microsoft Exchange Server 2013 organization and the [Azure Active Directory authentication system](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/gg638824(v=ws.11)), you need a digital certificate installed on the Exchange server used to create the trust. We strongly recommend using a self-signed certificate. A self-signed certificate is created and installed automatically when using the **Enable federation trust** wizard in the Exchange admin center (EAC).

If you don't want to use the recommended self-signed certificate, you should request and install an X.509 Secure Sockets Layer (SSL) certificate from a certification authority (CA) trusted by Microsoft. Although certificates issued by other CAs may also be used to establish a federation trust with the Azure AD authentication system, they aren't certified by Microsoft to date.

The following table lists CAs currently trusted Microsoft. These CAs have been tested for use with Exchange 2013.

|CA friendly name|Issued by|Intended purposes|
|---|---|---|
|Autoridade Certificadora Raiz Brasileira|Autoridade Certificadora Raiz Brasileira|Server authentication, client authentication|
|Comodo|Comodo Certification Authority|Server authentication, client authentication|
|CyberTrust|Baltimore CyberTrust Root Certificate Authority|Server authentication, client authentication|
|Digicert|Digicert Global Root Certification Authority|Server authentication, client authentication|
|Digicert High Assurance EV|Digicert Global Root Certification Authority|Server authentication, client authentication|
|Entrust|Entrust.net Secure Server Certification Authority|Server authentication, client authentication|
|Entrust (2048)|Entrust.net Secure Server Certification Authority|Server authentication, client authentication|
|Equifax|Equifax Secure Certification Authority|Server authentication, client authentication|
|GlobalSign|GlobalSign Certification Authority|Server authentication, client authentication|
|Go Daddy|Go Daddy Class 2 Certification Authority|Server authentication, client authentication|
|Network Solutions|Network Solutions Certification Authority|Server authentication, client authentication|
|PositiveSSL|Comodo Certification Authority|Server authentication, client authentication|
|SECOM|SECOM Trust Systems Certification Authority|Server authentication, client authentication|
|UTN-UserFirst-Hardware|Comodo Certification Authority|Server authentication, client authentication|
|VeriSign|Class 3 Public Primary Certification Authority|Server authentication, client authentication|
|VeriSign|VeriSign Trust Network|Server authentication, client authentication|

For more information about certificate requirements for Federation, see [Federation](federation-exchange-2013-help.md).
