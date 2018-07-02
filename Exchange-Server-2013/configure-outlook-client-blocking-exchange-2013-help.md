---
title: 'Configurar el bloqueo del cliente de Outlook: Exchange 2013 Help'
TOCTitle: Configurar el bloqueo del cliente de Outlook
ms:assetid: 3a579c83-8bc7-4adc-a25c-8eb6eed7220c
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd335207(v=EXCHG.150)
ms:contentKeyID: 51406491
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurar el bloqueo del cliente de Outlook

 

_**Se aplica a:** Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013_

_**Última modificación del tema:** 2015-03-09_

En Exchange Server 2013, puede usar directivas de retención o carpetas administradas para la administración de registros de mensajes (MRM). Solo los usuarios que ejecutan Microsoft Outlook 2010 y versiones posteriores tienen acceso a todas las características de cliente de las directivas de retención. No obstante, el Asistente para carpeta administrada aplica las directivas de retención al servidor de buzones de correo independientemente de la versión de cliente de Outlook que tenga el usuario. Los clientes más antiguos de Outlook no exponen la funcionalidad MRM de estas características. Por ejemplo, dado que Outlook 2007 no admite directivas de retención, los usuarios no pueden aplicar etiquetas personales a elementos o carpetas.

Puede bloquear los usuarios que ejecuten versiones más antiguas de Outlook para que no puedan obtener acceso a sus buzones de Exchange. También puede bloquear el acceso por buzón de correo o por servidor de acceso de cliente.

Para información sobre otras tareas administrativas relacionadas con MRM, vea [Procedimientos de administración de registros de mensajería](messaging-records-management-procedures-exchange-2013-help.md).

## Disponibilidad de la característica de MRM por aplicación de cliente y versión

En la siguiente tabla, se enumeran las características de MRM disponibles en distintas aplicaciones de cliente y versiones.

### Características de MRM

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Aplicación de cliente</th>
<th>Características de cliente de MRM disponibles</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook 2013 y Outlook 2010</p></td>
<td><p>Todas</p></td>
</tr>
<tr class="even">
<td><p>Outlook 2007</p></td>
<td><p>Carpetas administradas</p></td>
</tr>
<tr class="odd">
<td><p>Outlook 2003 y versiones anteriores</p></td>
<td><p>No se admite</p></td>
</tr>
<tr class="even">
<td><p>Otro software de cliente de correo electrónico</p></td>
<td><p>Ninguno</p></td>
</tr>
</tbody>
</table>


En la siguiente tabla, se muestran los números de versión de Outlook.

### Versiones de Outlook

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Versión de Outlook</th>
<th>Número de versión</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook 2013</p></td>
<td><p>15</p></td>
</tr>
<tr class="even">
<td><p>Outlook 2010</p></td>
<td><p>14</p></td>
</tr>
<tr class="odd">
<td><p>Outlook 2007</p></td>
<td><p>12</p></td>
</tr>
<tr class="even">
<td><p>Outlook 2003</p></td>
<td><p>11</p></td>
</tr>
<tr class="odd">
<td><p>Outlook 2002</p></td>
<td><p>10</p></td>
</tr>
<tr class="even">
<td><p>Outlook 2000</p></td>
<td><p>9</p></td>
</tr>
<tr class="odd">
<td><p>Outlook 98</p></td>
<td><p>8,5</p></td>
</tr>
<tr class="even">
<td><p>Outlook 97</p></td>
<td><p>8</p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> Antes de realizar cualquier cambio, tenga en cuenta que las revisiones y las versiones de Service Pack pueden afectar la cadena de versión del cliente. Tenga cuidado al restringir el acceso de cliente, ya que los componentes de servidor de Exchange también deben usar MAPI para iniciar sesión. Algunos componentes indican su versión de cliente como el nombre de componente (por ejemplo, SMTP u OLE&nbsp;DB), mientras que otros indican el número de compilación de Exchange (por ejemplo, 6.0.4712.0). Por este motivo, evite las restricciones de clientes cuyos números de versión comiencen con 6.&lt;<EM>x</EM>.<EM>x</EM>.&gt;. Por ejemplo, para impedir por completo el acceso MAPI, en lugar de indicar <STRONG>0.0.0-6.5535.65535.65535</STRONG>, defina los dos intervalos, de modo que los componentes del servidor puedan iniciar sesión. Por ejemplo, especifique lo siguiente: <STRONG>0.0.0-5.9.9; 7.0.0-</STRONG>.



Después de realizar estos procedimientos, tenga en cuenta que cuando se bloquea el acceso de los usuarios a sus buzones de correo, estos recibirán el siguiente mensaje de advertencia.


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Su administrador de Exchange Server ha bloqueado la versión de Outlook que está usando. Póngase en contacto con el administrador para obtener ayuda.</p></td>
</tr>
</tbody>
</table>


Para omitir la advertencia de que para los clientes de correo electrónico que estén ejecutando versiones de Outlook anteriores a Outlook 2010 no se admiten características de MRM, puede usar el parámetro *ManagedFolderMailboxPolicyAllowed* de los cmdlets **New-Mailbox**, **Enable-Mailbox** y **Set-Mailbox** en el Shell. Cuando una directiva de buzón de carpeta administrada se asigna a un buzón mediante el parámetro *ManagedFolderMailboxPolicy*, la advertencia se muestra de manera predeterminada, a menos que se use el parámetro *ManagedFolderMailboxPolicyAllowed*.

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 1 minuto.

  - No puede usar el Centro de administración de Exchange (EAC) para hacer estas tareas. Debe usar el Shell.

  - Los procedimientos descritos en este tema requieren permisos específicos. Vea cada procedimiento para ver la información de permisos.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

## ¿Qué desea hacer?

## Bloquear las versiones de Outlook según el buzón

Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el el contenido "buzones de usuario" en el tema [Permisos de destinatarios](recipients-permissions-exchange-2013-help.md).

Este ejemplo bloquea todas las versiones de Outlook anteriores a la versión 11.8010.8036.

    Set-CASMailbox -Identity adam@contoso.com -MAPIBlockOutlookVersions "-11.8010.8036"

En este ejemplo, se restaura el acceso a un buzón que fue bloqueado por una versión de Outlook.

    Set-CASMailbox -Identity adam@contoso.com -MAPIBlockOutlookVersions $null

Para obtener información detallada acerca de la sintaxis y los parámetros, vea [Set-CASMailbox](https://technet.microsoft.com/es-es/library/bb125264\(v=exchg.150\)).

## Bloquear las versiones de Outlook en un servidor de acceso de cliente

Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Configuración de Acceso de cliente RPC" en el tema [Permisos de dispositivos móviles y clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md).

En este ejemplo se bloquean los clientes de Outlook anteriores a la versión 12.0.0 para que no puedan acceder al buzón de Exchange 2010 ni a un servidor de acceso de cliente posterior.


> [!IMPORTANT]
> Los valores usados con el parámetro <EM>BlockedClientVersions</EM> son solo ejemplos. Para determinar las versiones de software de cliente adecuadas, analice los archivos de registro de Acceso de cliente de RPC que se encuentran en <CODE>%ExchangeInstallPath%Logging\RPC Client Access</CODE>.



    Set-RpcClientAccess -Server CAS01 -BlockedClientVersions "0.0.0-5.65535.65535;7.0.0;8.02.4-11.65535.65535"

Para conocer la definición detallada de la sintaxis y los parámetros, vea [Set-RpcClientAccess](https://technet.microsoft.com/es-es/library/dd351072\(v=exchg.150\)).

