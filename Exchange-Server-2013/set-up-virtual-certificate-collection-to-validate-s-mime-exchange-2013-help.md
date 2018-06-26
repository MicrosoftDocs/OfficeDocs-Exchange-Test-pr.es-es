---
title: 'Configurar una colección de certificados virtuales para validar S/MIME: Exchange 2013 Help'
TOCTitle: Configurar una colección de certificados virtuales para validar S/MIME
ms:assetid: 04a616e6-197c-490c-ae8c-c8d5f0f0b3dd
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn626155(v=EXCHG.150)
ms:contentKeyID: 61212721
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurar una colección de certificados virtuales para validar S/MIME

 

_**Se aplica a:**Exchange Online, Exchange Server 2013_

_**Última modificación del tema:**2016-12-09_

Como administrador de inquilinos tendrá que configurar una colección de certificados virtuales que se usará para validar certificados S/MIME. Esta colección de certificados virtuales se configura como un tipo de archivo de almacén de certificados con una extensión de nombre de archivo SST. El archivo SST contiene todos los certificados raíz e intermedios que se usan al validar un certificado S/MIME.

## Crear y guardar un SST

Solo puede usar el Shell para realizar este procedimiento.Para obtener información sobre cómo abrir el Shell de administración de Exchange en su organización local Exchange, vea [Abrir el Shell](https://technet.microsoft.com/es-es/library/dd638134\(v=exchg.150\)).Para obtener información sobre cómo usar Windows PowerShell para conectarse a Exchange Online, vea [Conexión a Exchange Online PowerShell](https://go.microsoft.com/fwlink/p/?linkid=396554).

Como administrador, puede crear este archivo SST exportando los certificados desde un equipo de confianza mediante el cmdlet `Export-Certificate` y especificando el tipo como SST. Para obtener más información sobre el cmdlet `Export-Certificate`, consulte el tema de referencia [Export-Certificate](https://technet.microsoft.com/es-es/library/hh848628.aspx).

Una vez que se genere el archivo SST, use el cmdlet `Set-Smimeconfig` para guardarlo en el almacén de certificados virtuales mediante el parámetro *-SMIMECertificateIssuingCA*. Por ejemplo: `Set-SmimeConfig -SMIMECertificateIssuingCA (Get-Content filename.sst -Encoding Byte)`

## Garantizar que un certificado es válido

Exchange 2013 SP1 primero comprueba el archivo SST y valida el certificado. Si se produce un error en la validación, examinará el almacén de certificados del equipo local para validar el certificado. Este comportamiento es nuevo para Exchange 2013 SP1 y diferente de las versiones anteriores de Exchange. En Exchange Online solo se usará el SST para la validación.

## Más información

[S/MIME para la firma y el cifrado de mensajes](s-mime-for-message-signing-and-encryption-exchange-2013-help.md)

[Get-SmimeConfig](https://technet.microsoft.com/es-es/library/dn554257\(v=exchg.150\))

