---
title: 'Registro de protocolo para POP3 e IMAP4: Exchange 2013 Help'
TOCTitle: Registro de protocolo para POP3 e IMAP4
ms:assetid: 212ed3d5-0c98-4346-a860-1cfcac5d73c4
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd335141(v=EXCHG.150)
ms:contentKeyID: 50556749
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Registro de protocolo para POP3 e IMAP4

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-03-09_

Puede usar el registro de protocolos para revisar las conexiones POP3 y IMAP4 en su entorno Exchange. Puede resultar útil al solucionar problemas relacionados con el rendimiento de POP3 o IMAP4.

## Habilitación del registro de protocolo POP3 e IMAP4

Puede habilitar, deshabilitar o cambiar el registro de protocolo mediante el Shell de administración de Exchange. Si habilita el registro de protocolo mediante el Shell, se usará la configuración predeterminada del registro de protocolo. En la mayoría de los casos, la configuración predeterminada será suficiente.

De lo contrario, puede habilitar, deshabilitar y modificar las opciones de registro de protocolo si edita los archivos de configuración Microsoft.Exchange.Pop3.exe.config y Microsoft.Exchange.Imap4.exe.config ubicados en el servidor de acceso de cliente de Microsoft Exchange Server 2013. Para obtener más información sobre cómo administrar la configuración de POP3 e IMAP4, consulte [Configurar del registro de protocolo para POP3 e IMAP4](configure-protocol-logging-for-pop3-and-imap4-exchange-2013-help.md).

## Revisión del registro de protocolos

Los archivos de registro de protocolos son archivos de texto que contienen datos en el formato de archivo de valores separados por comas (CSV). El registro de protocolo almacena cada evento de protocolo en una sola línea. La información almacenada en cada línea se organiza por campos. Estos campos se separan con comas. En la siguiente tabla, se describen los campos que se usan para clasificar cada uno de los eventos del protocolo.

### Campos utilizados para clasificar cada evento de protocolo

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Nombre del campo</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>fecha-hora</p></td>
<td><p>La fecha y hora del evento del protocolo. El valor tiene la forma <em>aaaa-mm-ddhh:mm:ss.fffZ</em>, en donde <em>aaaa</em> = año, <em>mm</em> = mes, <em>dd</em> = día, <em>hh</em> = hora, <em>mm</em> = minuto, <em>ss</em> = segundo,<em>fff</em> = fracciones de segundo y <em>Z</em> significa Zulú. Zulú es otra forma de indicar la Hora universal coordinada (UTC).</p></td>
</tr>
<tr class="even">
<td><p>connector-id</p></td>
<td><p>Este campo no se usa en el registro de los protocolos POP3 e IMAP4.</p></td>
</tr>
<tr class="odd">
<td><p>session-id</p></td>
<td><p>Un GUID que identifique de manera única la sesión de SMTP asociada con un evento de protocolo.</p></td>
</tr>
<tr class="even">
<td><p>sequence-number</p></td>
<td><p>Contador que se inicia en 0 y que aumenta para cada evento dentro de la misma sesión.</p></td>
</tr>
<tr class="odd">
<td><p>local-endpoint</p></td>
<td><p>El extremo local de una sesión de POP3 o IMAP4. Esto consiste de una dirección IP y un número de puerto TCP con el siguiente formato: <em>&lt;Dirección IP&gt;</em>:<em>&lt;puerto&gt;</em>.</p></td>
</tr>
<tr class="even">
<td><p>remote-endpoint</p></td>
<td><p>El extremo remoto de una sesión de POP3 o IMAP4. Esto consiste de una dirección IP y un número de puerto TCP con el siguiente formato: <em>&lt;Dirección IP&gt;</em>:<em>&lt;puerto&gt;</em>.</p></td>
</tr>
<tr class="odd">
<td><p>evento</p></td>
<td><p>Un único carácter que representa el evento del protocolo. Los valores posibles para el evento son los siguientes:</p>
<ul>
<li><p>+   Conectar</p></li>
<li><p>-   Desconectar</p></li>
<li><p>&gt;   Enviar</p></li>
<li><p>&lt;   Recibir</p></li>
<li><p>*   Información</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>datos</p></td>
<td><p>Información de texto asociada al evento de POP3 o IMAP4.</p></td>
</tr>
<tr class="odd">
<td><p>contexto</p></td>
<td><p>Este campo no se usa en el registro de los protocolos POP3 e IMAP4.</p></td>
</tr>
</tbody>
</table>

