---
title: 'Servicio de disponibilidad en Exchange 2013: Exchange 2013 Help'
TOCTitle: Servicio de disponibilidad en Exchange 2013
ms:assetid: 9722dea2-2bf8-437c-85c0-3ab65b8a07b9
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb232134(v=EXCHG.150)
ms:contentKeyID: 52062050
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Servicio de disponibilidad en Exchange 2013

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_

El servicio de disponibilidad de Exchange 2013 pone la información de disponibilidad a disposición de los clientes de Microsoft Outlook y Outlook Web App. El servicio de disponibilidad mejora la experiencia de calendario y programación de reuniones de los trabajadores de información facilitando información de disponibilidad segura, coherente y actualizada.

Outlook y Outlook Web App usan el servicio de disponibilidad para realizar las siguientes tareas:

  - Recuperar información actualizada de tiempo libre y ocupado para buzones de correo de Exchange 2013

  - Recuperar información actualizada de tiempo libre y ocupado desde otras organizaciones de Exchange 2013

  - Recuperar información de disponibilidad publicada desde carpetas públicas de buzones de correo en servidores que tengan versiones anteriores de Exchange

  - Ver horas laborables de asistentes

  - Mostrar sugerencias de hora de reunión

**Contenido**

Información general del servicio de disponibilidad

Información acerca del estado ausente

API del servicio de disponibilidad

Servicio de disponibilidad para el equilibrio de carga de red

Métodos usados para recuperar información de disponibilidad

## Información general del servicio de disponibilidad

El servicio de disponibilidad recupera la información de disponibilidad directamente de los buzones de correo de destino de los usuarios de Exchange 2013, Exchange 2010 o Exchange 2007 y puede configurarse para recuperar la información de disponibilidad de los usuarios de versiones anteriores de Exchange. En las topologías que tienen buzones de correo de Exchange 2007, Exchange 2010 o Exchange 2013 en las que todos los clientes ejecutan Outlook 2007 o superior, el servicio de disponibilidad se usa para recuperar la información de disponibilidad.

Outlook usa el servicio Detección automática de Exchange para obtener la URL del servicio de disponibilidad. Para obtener más información acerca del servicio de detección automática, vea [Servicio Detección automática](autodiscover-service-for-exchange-2013.md).

Para configurar el servicio de disponibilidad puede usar el Shell de administración de Exchange. No se puede usar el Centro de administración (EAC) de Exchange para configurar dicho servicio.

## Información acerca del estado ausente

El servicio de disponibilidad también proporciona acceso a mensajes de respuesta automática que los usuarios envían cuando no se encuentran en la oficina o están ausentes durante un período prolongado.

Los trabajadores de la información usan la característica Respuestas automáticas (anteriormente denominada Fuera de la oficina) de Outlook y Outlook Web App para avisar cuando no pueden responder a mensajes de correo electrónico. Esta funcionalidad permite a los trabajadores de la información y a los administradores establecer y administrar mensajes de respuesta automática con facilidad.

## API del servicio de disponibilidad

El servicio de disponibilidad forma parte de la interfaz de programación de Exchange 2013. Está disponible como servicio web para que los desarrolladores puedan programar herramientas de terceros con fines de integración.

## Servicio de disponibilidad para el equilibrio de carga de red

El uso del Equilibrio de carga de red (NLB) en los servidores de acceso de cliente que ejecutan el servicio de disponibilidad puede mejorar el rendimiento y la confiabilidad para los usuarios que dependen de la información de disponibilidad. Outlook detecta la dirección URL del servicio de disponibilidad mediante el servicio Detección automática. Para usar el equilibrio de carga de red con el servicio de Disponibilidad, debe realizar cambios en su configuración.

La dirección URL interna se usa desde la intranet, y la dirección URL externa se usa desde Internet. Si desea usar la misma dirección URL para el tráfico interno y el tráfico externo, asegúrese de que DNS está configurado correctamente para enrutar el tráfico interno directamente a la dirección URL interna. Además, debe asegurarse de que se pueda obtener acceso a la dirección URL, tanto interna como externamente. Para que los servicios de disponibilidad y Detección automática funcionen, el DNS debe estar configurado para que mail.\<*NombreDeDominio*\>.com y autodiscover.mail.\<*NombreDeDominio*\>.com hagan referencia a la matriz IP virtual (VIP) de su solución de equilibrio de carga, donde \<*NombreDeDominio*\> es el nombre de su dominio.


> [!NOTE]
> Para obtener más información, vea el artículo sobre la <A href="https://go.microsoft.com/fwlink/p/?linkid=45959">referencia técnica de equilibrio de carga de red</A> y <A href="https://go.microsoft.com/fwlink/p/?linkid=49315">Clústeres de Equilibrio de carga de red</A>. También puede buscar información en sitios web sobre software de equilibrio de carga de otros fabricantes.



## Métodos usados para recuperar información de disponibilidad

En la siguiente tabla se enumeran los distintos métodos usados para recuperar la información de disponibilidad en diversas topologías de bosque único.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Cliente</th>
<th>El buzón de correo que recupera la información de disponibilidad ejecuta</th>
<th>El buzón de correo de destino ejecuta</th>
<th>Método de recuperación de información de disponibilidad</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook 2013</p></td>
<td><p>Exchange 2013, Exchange 2010 o Exchange 2007</p></td>
<td><p>Exchange 2013, Exchange 2010 o Exchange 2007</p></td>
<td><p>El servicio de disponibilidad lee la información de disponibilidad en el buzón de correo de destino.</p></td>
</tr>
<tr class="even">
<td><p>Outlook 2007</p></td>
<td><p>Exchange 2013, Exchange 2010 o Exchange 2007</p></td>
<td><p>Exchange 2010 o Exchange 2007</p></td>
<td><p>El servicio de disponibilidad lee la información de disponibilidad en el buzón de correo de destino.</p></td>
</tr>
<tr class="odd">
<td><p>Outlook 2007</p></td>
<td><p>Exchange 2010 o Exchange 2007</p></td>
<td><p>Exchange 2003</p></td>
<td><p>El servicio de disponibilidad establece conexiones HTTP con el /directorio virtual público del buzón de correo de Exchange 2003.</p></td>
</tr>
<tr class="even">
<td><p>Outlook Web App</p></td>
<td><p>Exchange 2013, Exchange 2010 o Exchange 2007</p></td>
<td><p>Exchange 2013, Exchange 2010 o Exchange 2007</p></td>
<td><p>Outlook Web App en Exchange 2010 o Outlook Web Access en Exchange 2007 llama a la API del servicio de disponibilidad, que lee la información de disponibilidad del buzón de correo de destino.</p></td>
</tr>
</tbody>
</table>

