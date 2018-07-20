---
title: 'Recreating arbitration mailboxes: Exchange 2013 Help'
TOCTitle: Recreating arbitration mailboxes
ms:assetid: bb6b8524-aaee-4be8-a04e-e61cd2ab3465
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Mt829264(v=EXCHG.150)
ms:contentKeyID: 74518126
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Recreating arbitration mailboxes

 

_**Última modificación del tema:** 2018-01-17_

**Resumen:**  acerca de los buzones de arbitraje en Exchange 2013 y cómo volver a crearlos.

Exchange 2013 incluye cinco buzones de sistema conocidos como *buzones de arbitraje*. Buzones de correo de arbitraje se utilizan para almacenar diferentes tipos de datos del sistema y administrar el flujo de trabajo de mensajería aprobación. El siguiente gráfico enumera cada tipo de buzón de arbitraje y sus responsabilidades.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Nombre de buzón de arbitraje</th>
<th>Nombre para mostrar</th>
<th>Capacidades persistentes</th>
<th>Función</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>FederatedEmail.4c1f4d8b-8179-4148-93bf-00a95fa1e042</p></td>
<td><p>Buzón de Microsoft Exchange federación</p></td>
<td><p>{}</p></td>
<td><p>Este buzón almacena los datos que se utiliza para mantener la federación entre distintas organizaciones de Exchange. Esto incluye servicios de Rights Management, sondeos de supervisión de flujo de correo entre local y respuestas, notificaciones, archivos en línea, administración de registros de mensajería y local entre la información de disponibilidad.</p></td>
</tr>
<tr class="even">
<td><p>SystemMailbox{1f05a927-9350-4efe-a823-5529c2d64109}</p></td>
<td><p>Asistente de aprobación de Microsoft Exchange</p></td>
<td><p>{}</p></td>
<td><p>Este buzón se aprovisiona para su uso por el marco de trabajo de aprobación de Exchange destinatario moderación y auto group las solicitudes de aprobación.</p></td>
</tr>
<tr class="odd">
<td><p>Migration.8f3e7716-2011-43e4-96b1-aba62d229136</p></td>
<td><p>Migración de Microsoft Exchange</p></td>
<td><p>{OrganizationCapabilityManagement}</p></td>
<td><p>Almacena los datos para el servicio de migración de Exchange utilizar al mover buzones en lotes.</p></td>
</tr>
<tr class="even">
<td><p>SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9}</p></td>
<td><p>Microsoft Exchange</p></td>
<td><p>{OrganizationCapabilityUMDataStorage}</p></td>
<td><p>Buzón del sistema de detección.</p>
<p>Configurado para su uso por la característica de e-Discovery, que se utiliza por los funcionarios de cumplimiento de normas para buscar mensajes que coincidan con los criterios de selección especificados. Este buzón también se utiliza mensajería unificada para almacenar consola de mensajería unificada que asisten a los archivos y otra información.</p></td>
</tr>
<tr class="odd">
<td><p>SystemMailbox{bb558c35-97f1-4cb9-8ff7-d53741dc928c}</p></td>
<td><p>Microsoft Exchange</p></td>
<td><p>{OrganizationCapabilityUMGrammarReady, OrganizationCapabilityPstProvider, OrganizationCapabilityMessageTracking, OrganizationCapabilityMailRouting, OrganizationCapabilityClientExtensions, OrganizationCapabilityGMGen, OrganizationCapabilityOABGen, OrganizationCapabilityUMGrammar}</p></td>
<td><p>Esto se conoce como un buzón de la organización. Se utiliza para crear libretas de direcciones sin conexión (OAB). A la generación de OAB de equilibrio de carga en toda la organización, incluyendo en sitios separados geográficamente, puede crear buzones de correo de organización adicionales.</p></td>
</tr>
</tbody>
</table>


Si necesita volver a crear uno o varios de estos buzones de arbitraje, consulte las instrucciones que siguen.

## Qué necesita saber antes de comenzar

  - Tiempo estimado para completar: 10 minutos por procedimiento.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Sección "Permisos de aprovisionamiento de destinatarios" en el tema [Permisos de destinatarios](recipients-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## Utilice Shell de administración de Exchange para volver a crear un buzón de arbitraje

Utilice las siguientes instrucciones para volver a crear un tipo concreto de buzón de arbitraje.


> [!NOTE]
> Todos los pasos en las secciones siguientes se deben ejecutar desde el mismo directorio donde extrajo el medio de instalación de Exchange.



## Volver a crear el buzón de Microsoft Exchange federación

Volver a crear el buzón de arbitraje FederatedEmail.4c1f4d8b-8179-4148-93bf-00a95fa1e042:

1.  Si faltan los buzones de arbitraje, ejecute el siguiente comando:
    
        .\Setup /preparead /IAcceptExchangeServerLicenseTerms

2.  En Shell de administración de Exchange, ejecute lo siguiente:
    
        Enable-Mailbox -Arbitration -Identity "FederatedEmail.4c1f4d8b-8179-4148-93bf-00a95fa1e042"

## Volver a crear el buzón de Microsoft Exchange Approval Assistant

Volver a crear el buzón SystemMailbox {1f05a927-9350-4efe-a823-5529c2d64109} de arbitraje:

1.  Si faltan los buzones de arbitraje, ejecute el siguiente comando:
    
        .\Setup /preparead /IAcceptExchangeServerLicenseTerms

2.  En Shell de administración de Exchange, ejecute lo siguiente:
    
        Get-User | Where-Object {$_.Name -like "SystemMailbox{1f05a927-7709-4e35-9dbe-d0f608fb781a}"} | Enable-Mailbox -Arbitration

## Volver a crear el buzón de migración de Microsoft Exchange

Volver a crear el buzón de arbitraje Migration.8f3e7716-2011-43e4-96b1-aba62d229136:

1.  Si faltan los buzones de arbitraje, ejecute el siguiente comando:
    
        .\Setup /preparead /IAcceptExchangeServerLicenseTerms

2.  En Shell de administración de Exchange, ejecute lo siguiente:
    
        Enable-Mailbox -Arbitration -Identity "Migration.8f3e7716-2011-43e4-96b1-aba62d229136"

3.  En Shell de administración de Exchange, defina las funciones conservan (msExchCapabilityIdentifiers) ejecutando el siguiente comando:
    
        Set-Mailbox "Migration.8f3e7716-2011-43e4-96b1-aba62d229136" -Arbitration -Management:$True -Force

## Volver a crear el buzón del sistema de detección de Microsoft Exchange

Volver a crear el buzón SystemMailbox {e0dc1c29-89c3-4034-b678-e6c29d823ed9} de arbitraje:

1.  Ejecute el siguiente comando:
    
        .\Setup /preparead /IAcceptExchangeServerLicenseTerms

## Volver a crear el buzón de la organización de Microsoft Exchange para OAB

Volver a crear el buzón SystemMailbox {bb558c35-97f1-4cb9-8ff7-d53741dc928c} de arbitraje:

1.  Si faltan los buzones de arbitraje, ejecute el siguiente comando:
    
        .\Setup /preparead /IAcceptExchangeServerLicenseTerms

2.  En Shell de administración de Exchange, ejecute lo siguiente:
    
        Enable-Mailbox -Arbitration -Identity "SystemMailbox{bb558c35-97f1-4cb9-8ff7-d53741dc928c}"

3.  En Shell de administración de Exchange, defina las funciones conservan (msExchCapabilityIdentifiers) ejecutando el siguiente comando:
    
        Get-Mailbox "SystemMailbox{bb558c35-97f1-4cb9-8ff7-d53741dc928c}" -Arbitration | Set-Mailbox -Arbitration -UMGrammar:$True -OABGen:$True -GMGen:$True -ClientExtensions:$True -MessageTracking:$True -PstProvider:$True -MaxSendSize 1GB -Force

Cuando haya terminado, si ejecuta el comando `$OABMBX = Get-Mailbox "SystemMailbox{bb558c35-97f1-4cb9-8ff7-d53741dc928c}" -Arbitration (Get-ADUser $OABMBX.SamAccountName -Properties *).msExchCapabilityIdentifiers` , verá que faltan 46, 47 y 51. Ejecute el siguiente comando para agregar todas las capacidades de nuevo:

    Set-ADUser $OABMBX.SamAccountName -Add @{"msExchCapabilityIdentifiers"="40","42","43","44","47","51","52","46"}

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que vuelve a creó correctamente el buzón de arbitraje, utilice el cmdlet **Get-Mailbox** con el modificador *Arbitration* para recuperar los buzones del sistema.

    Get-Mailbox -Arbitration | Format-Table Name, DisplayName

Ver los resultados del comando para comprobar que ese buzón de sistema adecuados, ya sea por nombre o nombre para mostrar de la tabla anterior, vuelve a crear.


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.


