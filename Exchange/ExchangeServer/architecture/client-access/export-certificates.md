---
ms.localizationpriority: medium
description: 'Summary: Learn how to export a certificate from an Exchange server 2016 or 2019.'
ms.topic: article
author: JoanneHendrickson
ms.author: jhendr
ms.assetid: 7e4c4013-8a2b-4c25-a287-b367c65e48aa
ms.reviewer:
title: Export a certificate from an Exchange server
ms.collection:
- Strat_EX_Admin
- exchange-server
f1.keywords:
- NOCSH
audience: ITPro
ms.prod: exchange-server-it-pro
manager: serdars

---

# Export a certificate from an Exchange server

You can export a certificate from an Exchange server as a backup or to import the certificate on other clients, devices or servers. You can export certificates in the Exchange admin center (EAC) or in the Exchange Management Shell. The resulting certificate file is a password-protected binary PKCS #12 file that contains the certificate's private key, and is suitable for importing (installing) on other servers.

## What do you need to know before you begin?

- Estimated time to complete: 5 minutes.

- In the EAC, you need to export the certificate file to a UNC path (`\\<Server>\<Share>\` or `\\<LocalServerName>\c$\`). In the Exchange Management Shell, you can specify a local path.

- To learn how to open the Exchange Management Shell in your on-premises Exchange organization, see [Open the Exchange Management Shell](/powershell/exchange/open-the-exchange-management-shell).

- You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Client Access services security" entry in the [Clients and mobile devices permissions](../../permissions/feature-permissions/client-and-mobile-device-permissions.md) topic.

- For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](../../about-documentation/exchange-admin-center-keyboard-shortcuts.md).

> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at: [Exchange Server](https://social.technet.microsoft.com/forums/office/home?category=exchangeserver), [Exchange Online](/answers/topics/office-exchange-server-itpro.html), or [Exchange Online Protection](https://social.technet.microsoft.com/forums/forefront/home?forum=FOPE).

## Use the EAC to export a certificate

1. Open the EAC and navigate to **Servers** \> **Certificates**.

2. In the **Select server** list, select the Exchange server that contains the certificate, click **More options** ![More Options icon.](../../media/ITPro_EAC_MoreOptionsIcon.png), and select **Export Exchange certificate**.

3. On the **Export Exchange certificate** page that opens, enter the following information:

   - **File to export to**: Enter the UNC path and file name of the certificate file. For example, `\\FileServer01\Data\Fabrikam.pfx`

   - **Password**: When you export the certificate with its private key, you need to specify a password. Exporting the certificate with its private key allows you to import the certificate on other servers.

   When you're finished, click **OK**.

## Use the Exchange Management Shell to export a certificate

To export a binary certificate file that you can import on other clients or servers, use the following syntax:

```powershell
$cert = Export-ExchangeCertificate -Thumbprint <Thumbprint> -BinaryEncoded -Password (ConvertTo-SecureString -String '<Password>' -AsPlainText -Force) [-Server <ServerIdentity>]
[System.IO.File]::WriteAllBytes('<FilePathOrUNCPath>\<FileName>.pfx', $cert.FileData)
```

This example exports a certificate from the local Exchange server to a file with the following settings:

- The certificate that has the thumbprint value `5113ae0233a72fccb75b1d0198628675333d010e` is exported to the file `C:\Data\Fabrikam.pfx` on the same server where you're running the command.
- The exported certificate file is encoded by DER (not Base64).
- The password for the certificate file is `P@ssw0rd1`.

```powershell
$cert = Export-ExchangeCertificate -Thumbprint 5113ae0233a72fccb75b1d0198628675333d010e -BinaryEncoded -Password (ConvertTo-SecureString -String 'P@ssw0rd1' -AsPlainText -Force)
[System.IO.File]::WriteAllBytes('C:\Data\Fabrikam.pfx', $cert.FileData)
```

To export a pending certificate request (also known as a certificate signing request or CSR), use the following syntax:

```powershell
$txtcert = Export-ExchangeCertificate -Thumbprint <Thumbprint> [-Server <ServerName>]
[System.IO.File]::WriteAllBytes('<FilePathOrUNCPath>\<FileName>.req', [System.Text.Encoding]::Unicode.GetBytes($txtcert))
```

This example exports a pending certificate request from the local Exchange server to a file with the following settings:

- The certificate that has the thumbprint value `72570529B260E556349F3403F5CF5819D19B3B58` is exported to the file `\\FileServer01\Data\Fabrikam.req`.
- The exported certificate file is Base64 encoded.

```powershell
$txtcert = Export-ExchangeCertificate -Thumbprint 72570529B260E556349F3403F5CF5819D19B3B58
[System.IO.File]::WriteAllBytes('\\FileServer01\Data\Fabrikam.req', [System.Text.Encoding]::Unicode.GetBytes($txtcert))
```

For detailed syntax and parameter information, see [Export-ExchangeCertificate](/powershell/module/exchange/export-exchangecertificate).

**Notes**:

- You can export a pending certificate request if you need to resubmit the certificate request to the certification authority and you can't find the original certificate request file.
- When you export a certificate request, you typically don't need to use the _Password_ parameter or the _BinaryEncoded_ switch, and you save the request to a .req file.
- You can't import an exported pending certificate request on another server.

## How do you know this worked?

To verify that you have successfully exported a certificate from an Exchange server, try importing the certificate file on another server. For more information, see [Import or install a certificate on an Exchange server](import-certificates.md).
