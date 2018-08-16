---
title: 'Eliminar y volver a crear buzón correo detección predeterminado en Exchange'
TOCTitle: Eliminar y volver a crear el buzón de correo de detección predeterminado en Exchange
ms:assetid: 4bde0b00-bdf7-44b4-ba64-aa062bc10ca2
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn750894(v=EXCHG.150)
ms:contentKeyID: 62371350
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Eliminar y volver a crear el buzón de correo de detección predeterminado en Exchange

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2016-05-04_

Puede usar el Shell de administración de Exchange para eliminar el buzón de correo de detección predeterminado, volver a crearlo y luego asignarle permisos.

## ¿En qué circunstancias querría hacer esto?

En Exchange Server 2013 y Exchange Online, el tamaño máximo del buzón de correo de detección predeterminado es de 50 GB. Se utiliza para almacenar los resultados de la búsqueda de la exhibición de documentos electrónicos local. Antes de que se cambie el límite de tamaño, las organizaciones podrían aumentar la cuota de almacenamiento de información a más de 50 GB. Como consecuencia, los buzones de correo de detección podrían crecer a más de 50 GB. Hay tres problemas con un buzón de correo de detección predeterminado que tiene un tamaño mayor que 50 GB:

  - No se admite.

  - No se puede migrar a Office 365.

  - Si es el buzón de correo de detección predeterminado en Exchange Server 2010, no se puede actualizar a Exchange Server 2013.

La forma de resolver esto depende de si desea guardar los resultados de la búsqueda de un buzón de correo de detección predeterminado que ha superado los 50 GB.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>¿Desea guardar los resultados de la búsqueda?</th>
<th>Haga esto…</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>No</p></td>
<td><p>Siga los pasos de este tema para eliminar y luego volver a crear el buzón de correo de detección predeterminado.</p></td>
</tr>
<tr class="even">
<td><p>Sí</p></td>
<td><p>Siga los pasos descritos en <a href="reduce-the-size-of-a-discovery-mailbox-in-exchange-exchange-2013-help.md">Reducir el tamaño de un buzón de correo de detección en Exchange</a>.</p></td>
</tr>
</tbody>
</table>


## Usar el Shell de administración de Exchange para eliminar y volver a crear el buzón de correo de detección predeterminado


> [!NOTE]
> No puede usar el Centro de administración de Exchange (EAC) porque los buzones de correo de detección no se muestran en el mismo.



1.  Ejecute el siguiente comando para eliminar el buzón de correo de detección predeterminado.
    
        Remove-Mailbox "DiscoverySearchMailbox{D919BA05-46A6-415f-80AD-7E09334BB852}"

2.  En el mensaje que le pide que confirme que desea eliminar el buzón y el correspondiente objeto de usuario de Active Directory, escriba **Y** y luego presione Entrar.
    
    Al crear el buzón de correo de detección en el paso siguiente, se crea un nuevo objeto de usuario en Active Directory.

3.  Ejecute el siguiente comando para volver a crear el buzón de correo de detección predeterminado.
    
        New-Mailbox -Name "DiscoverySearchMailbox{D919BA05-46A6-415f-80AD-7E09334BB852}" -Alias "DiscoverySearchMailbox{D919BA05-46A6-415f-80AD-7E09334BB852}" -DisplayName "Discovery Search Mailbox" -Discovery

4.  Ejecute el siguiente comando para asignar permisos de grupo del rol de administración de detección para abrir el buzón de correo de detección predeterminado y ver los resultados de la búsqueda.
    
        Add-MailboxPermission "DiscoverySearchMailbox{D919BA05-46A6-415f-80AD-7E09334BB852}" -User "Discovery Management" -AccessRights FullAccess -InheritanceType all

