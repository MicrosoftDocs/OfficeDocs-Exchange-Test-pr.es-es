---
title: 'No encontrar service_RUSMissing actualización destinatarios Exchange 2013 Help | Microsoft Docs'
TOCTitle: No se encuentra un servicio de actualización de destinatarios_RUSMissing
ms:assetid: 920fbf51-d5e4-4ac6-869f-7f1c5d9a3024
ms:mtpsurl: https://technet.microsoft.com/es-es/library/ms.exch.setupreadiness.rusmissing(v=EXCHG.150)
ms:contentKeyID: 48268420
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# No se encuentra un servicio de actualización de destinatarios\_RUSMissing

 

_**Se aplica a:** Exchange Server_

_**Última modificación del tema:** 2016-12-15_

El contenido de este tema no se ha actualizado para Microsoft Exchange Server 2013. Aun así, se puede aplicar a Exchange 2013. Si necesita más ayuda, consulte los siguientes recursos de la comunidad.

¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Microsoft® Exchange Server 2007 o Exchange Server 2010 Setup no puede continuar porque no se encontró el Servicio de actualización de destinatarios (RUS) responsable de un dominio en la organización Exchange existente.

La instalación de Microsoft Exchange requiere que cada dominio de la organización Exchange existente tenga una instancia del Servicio de actualización de destinatarios.

Si falta una instancia del Servicio de actualización de destinatarios de un dominio, los objetos de usuario nuevos que se creen en el dominio no recibirán las direcciones de correo electrónico que se les remitan.

Para resolver este problema, compruebe que existe una instancia del Servicio de actualización de destinatarios para cada dominio y cree una instancia de dicho Servicio para los dominios que no tienen ninguno y, a continuación, vuelva a ejecutar la instalación de Microsoft Exchange.


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Para crear una instancia del Servicio de actualización de destinatarios para un dominio</p></td>
</tr>
<tr class="even">
<td><ol>
<li><p>Abra el Administrador del sistema de Exchange.</p></li>
<li><p>Expanda <strong>Destinatarios</strong>.</p></li>
<li><p>Haga clic con el botón secundario en el nodo <strong>Servicios de actualización de destinatarios</strong>, haga clic en <strong>Nuevo</strong> y, a continuación, en <strong>Servicio de actualización de destinatarios.</strong></p></li>
<li><p>En la ventana Nuevo objeto, haga clic en <strong>Examinar</strong> para buscar el nombre del dominio.</p></li>
<li><p>Seleccione el nombre del dominio y haga clic en <strong>Aceptar</strong>.</p></li>
<li><p>En la ventana Nuevo objeto, haga clic en <strong>Siguiente</strong> y, a continuación, en <strong>Finalizar</strong>.</p></li>
</ol></td>
</tr>
</tbody>
</table>


Para obtener más información acerca del Servicio de actualización de destinatarios, consulte los artículos siguientes de Microsoft Knowledge Base:

  - "Cómo el Servicio de actualización de destinatarios aplica directivas de destinatarios" ([https://go.microsoft.com/fwlink/?linkid=3052\&kbid=328738](https://go.microsoft.com/fwlink/?linkid=3052&kbid=328738)).

  - "Cómo llena las listas de direcciones el Servicio de actualización de destinatarios" ([https://go.microsoft.com/fwlink/?linkid=3052\&kbid=253828](https://go.microsoft.com/fwlink/?linkid=3052&kbid=253828)).

  - "Cómo comprobar el progreso del Servicio de actualización de destinatarios de Exchange" ([https://go.microsoft.com/fwlink/?linkid=3052\&kbid=246127](https://go.microsoft.com/fwlink/?linkid=3052&kbid=246127)).

  - "Tareas realizadas por el Servicio de actualización de destinatarios de Exchange" ([https://go.microsoft.com/fwlink/?linkid=3052\&kbid=253770](https://go.microsoft.com/fwlink/?linkid=3052&kbid=253770)).

