---
title: 'Movimientos de buzones de Exchange 2013: Exchange 2013 Help'
TOCTitle: Movimientos de buzones de Exchange 2013
ms:assetid: 9c0a0bc9-2a39-4cf0-aa6e-6e5ef3fd38b5
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ150543(v=EXCHG.150)
ms:contentKeyID: 48268477
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Movimientos de buzones de Exchange 2013

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-04-07_

Cuando mueve un buzón de correo, lo hace de una *base de datos de buzones de origen* a una *base de datos de buzones de destino*. La base de datos de buzones de correo de destino puede estar ubicada en el mismo servidor, en otro servidor, en un dominio diferente, en un sitio de Active Directory diferente o en otro bosque.

## Motivos para mover buzones de correo

Es posible que necesite mover los buzones en las siguientes situaciones:

  - **Actualización**   Cuando actualiza de una organización de Microsoft Exchange Server 2007 o Exchange Server 2010 existente a Exchange Server 2013, debe mover los buzones de correo de los servidores existentes de Exchange a un servidor de Buzones de correo de Exchange 2013.

  - **Realineación**   Puede mover buzones con fines de realineación. Por ejemplo, quizá desee mover un buzón de correo desde una base de datos a otra que tenga un límite de tamaño mayor para el buzón.

  - **Investigar un problema**   Si necesita investigar un problema con un buzón de correo, puede mover el buzón de correo a un servidor diferente. Por ejemplo, puede mover todos los buzones de correo que tienen gran actividad a otro servidor.

  - **Buzones de correo dañados**   Si detecta buzones dañados, puede mover los buzones a un servidor o una base de datos diferente. No se moverán los mensajes dañados.

  - **Cambios de ubicación física**   Puede mover buzones de correo a un servidor que se encuentre en un sitio diferente de Active Directory. Por ejemplo, si un usuario se mueve a una ubicación física distinta, puede mover el buzón de correo de dicho usuario a un servidor que se encuentre más cerca de la nueva ubicación.

  - **Separación de roles administrativos**   Quizá desee separar la administración de Exchange de la administración de cuentas de Windows. Para hacerlo, puede mover buzones de correo desde un bosque único a una situación de bosque del recurso. Con esta situación, los buzones de Exchange residen en un bosque y las cuentas de usuario asociadas de Windows residen en un bosque separado.

  - **Delegar la administración de correo electrónico**   Puede delegar la administración de correo electrónico y conservar la administración de cuentas de usuario de Windows. Para hacerlo, puede mover buzones de correo desde un bosque único a una situación de bosque del recurso.

  - **Integrar la administración de correo electrónico y cuentas de usuario**   Quizá desee cambiar un modelo de administración separado o delegado de correo electrónico por un modelo en el que las cuentas de usuario y el correo electrónico se puedan administrar dentro del mismo bosque. Para hacerlo, puede mover buzones de correo desde un bosque de recursos a una situación de bosque único. Con esta situación, los buzones de correo de Exchange y cuentas de usuario de Windows residen en el mismo bosque.

## Movimientos en Exchange 2013

Microsoft Exchange Server 2013 introduce el concepto de *movimientos en lote* y *extremos de migración*. Los extremos de migración son objetos de administración que describe el servidor remoto y las conexiones que pueden estar asociados con uno o más lotes. Además, la nueva arquitectura de movimientos de lotes mejora en movimientos de Servicio de replicación de buzones (MRS) gracias a una mayor capacidad de administración. La arquitectura de movimientos de lotes en Exchange 2013 cuenta con las siguientes capacidades:

  - Capacidad para mover varios buzones en lotes grandes.

  - Notificación por correo electrónico durante el movimiento con informes.

  - Reintento automático y priorización automática de movimientos.

  - Los buzones de correo de archivo principal y personal pueden moverse en forma conjunta o independiente.

  - Opción de finalización de solicitud de movimiento manual, que permite revisar el movimiento antes de finalizarlo.

  - Sincronizaciones incrementales periódicas para actualizar los cambios de migración.

En Exchange 2013 debe mover buzones de correo entre Exchange 2007 y Exchange 2010 y Exchange 2013 desde el Centro de administración de Exchange 2013 (EAC) y el Shell de administración de Exchange.


> [!NOTE]
> Aún puede realizar movimientos únicos de buzón de correo en Exchange&nbsp;2013 de manera similar a Exchange Server 2010 utilizando el EAC o los cmdlets de solicitud de movimiento o lote de migración.




> [!NOTE]
> No se pueden mover buzones locales de Exchange Server 2003 a Exchange&nbsp;2013.



Para obtener más información acerca de la administración de grupos de almacenamiento y bases de datos, consulte [Administración de movimientos locales](manage-on-premises-moves-exchange-2013-help.md).

## Extremos de migración

Los extremos de migración detectan la información de servidores remotos y almacenan las credenciales necesarias para migrar los datos y la configuración de limitación de origen. Puede usar los extremos de migración para configurar las opciones de los movimientos remotos y de otro bosque. Los movimientos locales no requieren el uso de un extremo. (Los movimientos locales mueven buzones entre dos diferentes bases de datos de Exchange locales.)

La siguiente lista muestra los tipos de movimientos que admiten los extremos de migración:

  - **Movimiento entre bosques**   Mueve buzones entre dos diferentes bosques de Exchange locales. Los movimientos entre bosques requieren el uso de un extremo de RemoteMove de Exchange.

  - **Movimiento remoto**   En una implementación híbrida, un movimiento remoto implica migraciones *de incorporación* o *de baja de servicio*. Los movimientos remotos requieren el uso de un extremo de RemoteMove. La incorporación mueve los buzones de una organización de Exchange local a Exchange Online en Microsoft Office 365 y utiliza un extremo de RemoteMove como el extremo de origen del lote de migración. La baja de servicio mueve los buzones de una organización de Exchange Online en Office 365 a una organización de Exchange local y utiliza un extremo de RemoteMove de Exchange como el extremo de destino del lote de migración.

En la siguiente tabla se muestran los tipos y los valores de extremos de migración que puede administrar en Exchange 2013.

### Valores de tipos de extremo de migración

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Exchange RemoteMove</th>
<th>Exchange LocalMove</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MaxConcurrentMigrations</p></td>
<td><p>MaxConcurrentMigrations</p></td>
</tr>
<tr class="even">
<td><p>RemoteServer</p></td>
<td><p>Site</p></td>
</tr>
<tr class="odd">
<td><p>ArchiveDomain</p></td>
<td><p>Database</p></td>
</tr>
<tr class="even">
<td><p>BadItemLimit</p></td>
<td><p>ArchiveDatabase</p></td>
</tr>
<tr class="odd">
<td><p>LargeItemLimit</p></td>
<td><p>BadItemLimit</p></td>
</tr>
<tr class="even">
<td><p>Databases</p></td>
<td><p>LargeItemLimit</p></td>
</tr>
<tr class="odd">
<td><p>TargetDeliveryDomain</p></td>
<td><p>PrimaryOnly</p></td>
</tr>
<tr class="even">
<td><p>PrimaryOnly</p></td>
<td><p>ArchiveDatabase</p></td>
</tr>
<tr class="odd">
<td><p>ArchiveDatabase</p></td>
<td><p>DAG</p></td>
</tr>
<tr class="even">
<td><p>ArchiveOnly</p></td>
<td><p>Forest</p></td>
</tr>
</tbody>
</table>


Para obtener más información acerca de los extremos de migración, consulte la interfaz de usuario **Migración** en el EAC y [New-MigrationEndpoint](https://technet.microsoft.com/es-es/library/jj218611\(v=exchg.150\)).

Para obtener más información acerca de la administración de grupos de almacenamiento y bases de datos, consulte [Administración de movimientos locales](manage-on-premises-moves-exchange-2013-help.md).

