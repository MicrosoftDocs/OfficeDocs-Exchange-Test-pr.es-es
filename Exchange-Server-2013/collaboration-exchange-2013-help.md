---
title: 'Colaboración: Exchange 2013 Help'
TOCTitle: Colaboración
ms:assetid: f45c1be1-2a66-4610-a28d-4adc6d212769
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ218725(v=EXCHG.150)
ms:contentKeyID: 49116624
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Colaboración

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-03-09_

Exchange 2013 ofrece las siguientes características avanzadas que permitirán a los usuarios finales colaborar de manera sencilla en el correo electrónico:

  - Buzones del sitio

  - Carpetas públicas

  - Buzones compartidos

  - Grupos de distribución

Cada una de estas características tiene un conjunto de funciones y una experiencia de usuario diferentes, y deben establecerse según lo que el usuario necesite lograr y lo que su organización pueda ofrecer. Por ejemplo, los buzones de sitio proporcionan magníficas características de colaboración de documentación. No obstante, los buzones de sitio dependen de SharePoint Server 2013, por lo que si piensa implementar SharePoint, deberá usar carpetas públicas para compartir documentos.

En este tema, se comparan estas características de colaboración para permitirle decidir qué características ofrecer a los usuarios.

## Buzones del sitio

Funcionalmente, un buzón de sitio está compuesto por la pertenencia a un sitio de SharePoint 2013 (propietarios y miembros), un almacenamiento compartido a través de un buzón de Exchange 2013 para mensajes de correo electrónico y un sitio de SharePoint 2013 para compartir y en el que almacenar. En realidad, los buzones de sitio reúnen los documentos de SharePoint y el correo electrónico de Exchange. Para los usuarios, un buzón de sitio actúa como un archivo contenedor central para el proyecto, y ofrece un lugar para archivar los documentos y correos electrónicos del proyecto a los que solamente pueden tener acceso los miembros del sitio y que solo pueden ser editados por ellos. Además, los buzones de sitio tienen un ciclo de vida específico y están optimizados para su uso en proyectos que tengan una fecha de inicio y de finalización. Para implementar completamente los buzones de sitio, los usuarios finales deben usar Outlook 2013.

Para obtener más información, consulte [Buzones de correo del sitio](site-mailboxes-exchange-2013-help.md).

## Carpetas públicas

Las carpetas públicas están diseñadas para un acceso compartido y ofrecen una manera fácil y efectiva de obtener, organizar y compartir información con otras personas de su grupo de trabajo u organización.

Las carpetas públicas organizan el contenido en una jerarquía profunda que es fácil de examinar. Los usuarios detectan contenido interesante y relevante al examinar las ramificaciones de la jerarquía que les resultan relevantes. Los usuarios siempre ven la jerarquía completa en la vista de carpetas de Outlook. Las carpetas públicas son una gran tecnología para el archivado de grupos de distribución. Una carpeta pública puede habilitarse para correo y agregarse como miembro del grupo de distribución. El correo electrónico enviado al grupo de distribución se agrega automáticamente a la carpeta pública para una referencia posterior. Las carpetas públicas también ofrecen el uso compartido simple de documentos y no requieren la instalación de SharePoint Server 2013 en la organización. Por último, los usuarios finales pueden usar carpetas públicas con los siguientes clientes de Outlook admitidos: Outlook 2007, Outlook 2010 y Outlook 2013.

Para obtener más información, consulte [Carpetas públicas](public-folders-exchange-2013-help.md).

## Buzones compartidos

Un buzón compartido es un buzón al que varios usuarios designados tienen acceso para leer y enviar mensajes de correo electrónico y para compartir un calendario común. Los buzones de correo compartidos pueden proporcionar una dirección de correo electrónico genérica (como info@contoso.com o ventas@contoso.com) que los clientes pueden usar para realizar consultas sobre su empresa. Si el buzón compartido tienen asignado el permiso Enviar como cuando un usuario delegado responde el mensaje de correo electrónico, puede parecer que el buzón de correo (por ejemplo, ventas@contoso.com) está respondiendo, y no el usuario real.

Para obtener más información, consulte [Buzones compartidos](shared-mailboxes-exchange-2013-help.md).

## Grupos

Los grupos (también denominados grupos de distribución) son una colección de dos o más destinatarios que aparecen en la libreta de direcciones compartida. Cuando un mensaje de correo electrónico se envía a un grupo, todos sus miembros lo reciben. Los grupos de distribución pueden organizarse mediante un asunto de debate determinado, como (“Amantes de perros”), o mediante usuarios que comparten una estructura de trabajo común que requiere que se comuniquen con frecuencia.

Para obtener más información, consulte [Destinatarios](recipients-exchange-2013-help.md).

## ¿Cuál utilizar?

En la siguiente tabla, se ofrece una vista rápida de cada una de las características de colaboración que lo ayudarán a decidir cuál utilizar.


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th></th>
<th>Buzones del sitio</th>
<th>Carpetas públicas</th>
<th>Buzones compartidos</th>
<th>Grupos</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Tipo de grupo</strong></p></td>
<td><p>Usuarios que trabajan juntos en equipo en un proyecto específico con fechas de inicio y de finalización definidas.</p></td>
<td><p>Con los permisos adecuados, todos los usuarios de la organización pueden tener acceso a las carpetas públicas y buscar en ellas. Las carpetas públicas son ideales para mantener conversaciones de grupos de distribución o historiales.</p></td>
<td><p>Delega el trabajo en nombre de una identidad virtual y puede responder a un correo electrónico como esa identidad de buzón compartido. Ejemplo: soporte@tailspintoys.com</p></td>
<td><p>Usuarios que necesitan enviar un correo electrónico a un grupo de destinatarios con una característica o interés común.</p></td>
</tr>
<tr class="even">
<td><p><strong>Tamaño ideal del grupo</strong></p></td>
<td><p>Pequeño</p></td>
<td><p>Organización de</p></td>
<td><p>Pequeño</p></td>
<td><p>Organización de</p></td>
</tr>
<tr class="odd">
<td><p><strong>Acceso</strong></p></td>
<td><p>Propietarios y miembros del buzón compartido.</p></td>
<td><p>Cualquier usuario de la organización puede tener acceso.</p></td>
<td><p>Los usuarios pueden obtener los permisos Acceso completo o Enviar como. Si se les otorga el permiso Acceso completo, los usuarios también deben agregar el buzón compartido al perfil de Outlook para acceder al buzón compartido.</p></td>
<td><p>Para los grupos de distribución, los miembros deben agregarse manualmente. Para los grupos de distribución dinámica, los miembros se agregan sobre la base de criterios de filtrado.</p></td>
</tr>
<tr class="even">
<td><p><strong>¿Calendario compartido?</strong></p></td>
<td><p>No</p></td>
<td><p>Sí</p></td>
<td><p>Sí</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p><strong>¿Llega el correo electrónico a la bandeja de entrada personal del usuario?</strong></p></td>
<td><p>No. El correo electrónico llega al buzón del sitio.</p></td>
<td><p>No. El correo electrónico llega a la carpeta pública.</p></td>
<td><p>No. El correo electrónico llega a la bandeja de entrada del buzón compartido.</p></td>
<td><p>Sí. El correo electrónico llega a la bandeja de entrada de un miembro del grupo de distribución.</p></td>
</tr>
<tr class="even">
<td><p><strong>Clientes soportados</strong></p></td>
<td><ul>
<li><p>Outlook 2013</p></li>
<li><p>SharePoint 2013</p></li>
</ul></td>
<td><ul>
<li><p>Outlook 2013</p></li>
<li><p>Outlook 2010</p></li>
<li><p>Outlook 2007</p></li>
</ul></td>
<td><ul>
<li><p>Outlook 2013</p></li>
<li><p>Outlook Web App</p></li>
<li><p>Outlook 2010</p></li>
<li><p>Outlook 2007</p></li>
</ul></td>
<td><ul>
<li><p>Outlook 2013</p></li>
<li><p>Outlook Web App</p></li>
<li><p>Outlook 2010</p></li>
<li><p>Outlook 2007</p></li>
</ul></td>
</tr>
</tbody>
</table>

