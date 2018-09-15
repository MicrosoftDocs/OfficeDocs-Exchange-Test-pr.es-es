---
title: 'Buzones de correo del sitio: Exchange 2013 Help'
TOCTitle: Buzones de correo del sitio
ms:assetid: 2c4393f4-d274-4e6c-bd09-9577e68c5a33
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ150499(v=EXCHG.150)
ms:contentKeyID: 48267933
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Buzones de correo del sitio

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_

El correo electrónico y los documentos se mantienen tradicionalmente en dos repositorios de datos únicos e independientes. La mayoría de las organizaciones colaboran usando ambos medios. El desafío es que pueda accederse al correo electrónico y a los documentos mediante clientes diferentes. Normalmente se traduce en una reducción en la productividad del usuario y en una mala experiencia de usuario.

El *buzón de correo del sitio* es un nuevo concepto en Microsoft Exchange 2013 que intenta solventar este problema. Los buzones en el sitio mejoran la colaboración y la productividad del usuario al conceder acceso a documentos de Microsoft SharePoint 2013 correo electrónico de Exchange mediante el uso de la misma interfaz de cliente. Un buzón de correo del sitio incluye funcionalmente pertenencia al sitio de SharePoint 2013 (propietarios y miembros), almacenamiento compartido a través del buzón de correo de Exchange 2013 para mensajes de correo electrónico y un sitio de SharePoint 2013 para documentos, y una interfaz administrada que satisface las necesidades de ciclo de vida y aprovisionamiento.

Los buzones de correo del sitio requieren la integración y la configuración de Exchange 2013 y de SharePoint Server 2013. Para obtener más información acerca de cómo configurar su organización de Exchange 2013 para que funcione con su organización de SharePoint Server 2013, consulte los temas siguientes:

  - [Configurar buzones de sitio en SharePoint Server 2013](https://go.microsoft.com/fwlink/p/?linkid=258264).

  - [Integración con SharePoint y Lync](integration-with-sharepoint-and-lync-exchange-2013-help.md)

Para obtener más información acerca del tratamiento de las características de colaboración en Exchange Server 2013, consulte [Colaboración](collaboration-exchange-2013-help.md).

**Contenido**

¿Cómo funcionan los buzones de sitios?

Directivas de aprovisionamiento de buzones del sitio

## ¿Cómo funcionan los buzones de sitios?

Cuando un miembro del proyecto archiva correo o documentos con el buzón de correo del sitio, todos los miembros del proyecto tendrán acceso a dicho contenido. Los buzones de sitio aparecen en Outlook 2013 y le brindan al usuario fácil acceso al correo electrónico y los documentos para los proyectos importantes. Asimismo, se puede acceder al mismo tipo de contenido directamente desde el propio sitio SharePoint. Con los buzones de correo del sitio, este contenido se mantiene donde pertenece. Exchange almacena el correo electrónico, brindándole al usuario la misma vista de mensaje para las conversaciones por correo electrónico que utilizan cada día en sus propios buzones. Mientras tanto, SharePoint almacena los documentos, permitiendo la coautoría y la posibilidad de crear versiones de un documento. Exchange sincroniza la cantidad suficiente de metadatos de SharePoint para crear la vista de documentos en Outlook (p. ej. título del documento, fecha de última modificación, último autor modificado, tamaño).

![Diagrama de uso y almacenamiento de buzones de sitio](images/JJ150499.b98be571-d2e0-4ebd-9fe2-440a14e91e35(EXCHG.150).gif "Diagrama de uso y almacenamiento de buzones de sitio")

## Directivas de aprovisionamiento de buzones del sitio

Las cuotas de buzones del sitio se pueden establecer con los cmdlets **SiteMailboxProvisioningPolicy** en el Shell de administración de Exchange. Las directivas de aprovisionamiento del buzón del sitio solo se aplican al correo electrónico que se envía a y desde el buzón del sitio y el tamaño del buzón del sitio en el servidor Exchange. La configuración de repositorio de documentos se configura en SharePoint. Aunque puede crear varias directivas de aprovisionamiento de buzones del sitio con el cmdlet **New-SiteMailboxProvisioningPolicy**, sólo se aplicará la política de aprovisionamiento predeterminada a todos los buzones del sitio. No se pueden aplicar varias directivas en la organización. Las políticas de aprovisionamiento permiten establecer las siguientes cuotas:


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Cuota</th>
<th>Descripción</th>
<th>Valor predeterminado</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>IssueWarningQuota</p></td>
<td><p>El parámetro <em>IssueWarningQuota</em> especifica el tamaño del buzón de sitio que activa el envío de un mensaje de advertencia al buzón del sitio</p></td>
<td><p>4,5 GB</p></td>
</tr>
<tr class="even">
<td><p>MaxReceiveSize</p></td>
<td><p>El parámetro <em>MaxReceiveSize</em> indica el tamaño máximo de los mensajes de correo electrónico que puede recibir el buzón de sitio.</p></td>
<td><p>36 MB</p></td>
</tr>
<tr class="odd">
<td><p>ProhibitSendReceiveQuota</p></td>
<td><p>El parámetro <em>ProhibitSendReceiveQuota</em> especifica el tamaño al cual el buzón de sitio no podrá seguir enviando o recibiendo mensajes.</p></td>
<td><p>5 GB</p></td>
</tr>
</tbody>
</table>


Para obtener más información acerca de cómo configurar directivas de aprovisionamiento de buzones del sitio, consulte [Administrar el buzón de sitio políticas de provisioning](manage-site-mailbox-provisioning-policies-exchange-2013-help.md).

¿Cómo funcionan los buzones de sitios?

## Retención y directiva del ciclo de vida

El ciclo de vida de un buzón del sitio se administra mediante un SharePoint. Es a través del SharePoint que debería realizar todas las tareas buzón del sitio como la creación o eliminación de buzones del sitio. Además, puede crear una directiva de ciclo de vida de SharePoint para administrar el ciclo de vida de un buzón del sitio. Por ejemplo, puede crear una directiva del ciclo de vida en SharePoint que cierre automáticamente todos los buzones del sitio tras 6 meses. Si el usuario todavía requiere el uso del buzón del sitio, el usuario puede reactivar el buzón del sitio a través de SharePoint. Le recomendamos que utilice el ciclo de vida de aplicación en la granja. La eliminación manual de buzones del sitio activo desde Exchange generará buzones del sitio huérfanos. .

Cuando la aplicación del ciclo de vida de SharePoint cierra un buzón del sitio, el buzón del sitio se retiene durante el período establecido en la directiva del ciclo de vida en el estado cerrado. Entonces, el usuario final o un administrador de SharePoint puede reactivar el buzón de correo. Tras el período de retención, se añadirá **MDEL:**  al nombre del buzón de correo de Exchange alojado en la base de datos de buzones. para indicar que se ha marcado para su eliminación. Deberá eliminar manualmente estos buzones del sitio de la base de datos de buzones para liberar espacio de almacenamiento y el alias. Si no tiene la directiva de ciclo de vida de SharePoint habilitada, perderá la capacidad de determinar los buzones del sitio que se marcan para ser eliminados. Hasta que un administrador no haya eliminado el buzón del sitio, su contenido se puede recuperar.

Puede usar el siguiente comando para buscar y eliminar buzones de correo que se hayan marcado para ser eliminados.

    Get-Mailbox MDEL:* | ?{$_.RecipientTypeDetails -eq "TeamMailbox"} | Remove-Mailbox -Confirm:$false

Los buzones de sitio no permiten la retención a nivel de elementos. La retención funciona a nivel de proyecto para los buzones del sitio, de manera que si se elimina todo el buzón del sitio, los elementos retenidos se eliminarán.

## Cumplimiento

Con la Consola de exhibición de documentos electrónicos en SharePoint, los buzones del sitio pueden formar parte del ámbito de la búsqueda de Exhibición de documentos electrónicos en contexto ya que puede realizar búsquedas de palabras clave en buzones de usuarios o en buzones del sitio. Además, puede colocar un buzón del sitio en retención legal. Para obtener más información, consulte [Exhibición de documentos electrónicos en contexto](https://docs.microsoft.com/es-es/exchange/security-and-compliance/data-loss-prevention/integrate-sensitive-information-rules).


> [!NOTE]
> Para colocar un buzón del sitio en suspensión legal en Office 365, debe tener asignada una licencia de Exchange Online (plan 2). Si un buzón del sitio tiene asignada una licencia de Exchange Online (plan 1), deberá asignarle una licencia independiente de Archivado de Exchange Online para aplicarle la suspensión.



¿Cómo funcionan los buzones de sitios?

## Copia de seguridad y restauración

La copia de seguridad y la restauración de los buzones del sitio de Exchange alojados en un servidor de buzones de correo usará el mismo método de copia de seguridad y restauración que usa para todos los buzones de correo de Exchange. Para obtener más información, consulte [Grupos de disponibilidad de base de datos (DAG)](database-availability-groups-dags-exchange-2013-help.md).

Para los documentos de SharePoint, debería realizar copias de seguridad y restauraciones en el mismo sitio. Si restaura su contenido de SharePoint en las mismas URL, el buzón del sitio continuará trabajando y no será necesario realizar ninguna configuración adicional. Si restaura en otra URL, deberá ejecutar el cmdlet **Set-SiteMailbox** para actualizar la propiedad *SharePointURL*. Le recomendamos que no restaure SharePoint en un nuevo bosque.

