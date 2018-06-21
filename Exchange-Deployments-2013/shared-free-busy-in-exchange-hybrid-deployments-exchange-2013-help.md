---
title: 'Información de disponibilidad compartida en implementaciones híbridas de Exchange: Exchange 2013 Help'
TOCTitle: Información de disponibilidad compartida en implementaciones híbridas de Exchange
ms:assetid: bd3884de-80ee-4ff2-a8a3-eacd5aa3e51b
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ650274(v=EXCHG.150)
ms:contentKeyID: 49895008
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Información de disponibilidad compartida en implementaciones híbridas de Exchange

 

_<strong>Se aplica a:</strong>Exchange Server 2013, Exchange Server 2016_

_<strong>Última modificación del tema:</strong>2016-04-29_

Una de las principales ventajas de una implementación híbrida es el uso compartido de información de disponibilidad (disponibilidad de calendario) entre los usuarios de la organización local y los de la organización de Exchange Online. Los usuarios de ambas organizaciones pueden ver los calendarios de ambos como si estuvieran ubicados en la misma ubicación física. Esto hace que la programación de reuniones y recursos sea sencilla y eficaz.

Se requieren varios componentes en una implementación híbrida para habilitar la característica de información de disponibilidad compartida entre la organización de Exchange local y Exchange Online.

  - **Confianza de federación**   Tanto las organizaciones locales como las del servicio de Office 365 deben tener una confianza de federación establecida con el sistema de autenticación de Azure AD. Una confianza de federación en una relación de uno a uno con el sistema de autenticación de Azure AD que define los parámetros para su organización de Exchange. El sistema usa estos parámetros cuando actúa como agente de confianza entre la organización local y la del servicio de Office 365 para intercambiar información de disponibilidad entre los usuarios de la organización local y los de la organización de Exchange Online.
    
    Una confianza de federación con el sistema se configura de forma automática para la organización del servicio de Office 365 cuando se crea la cuenta. El Asistente para configuración híbrida comprueba automáticamente si existe alguna confianza de federación con el sistema de autenticación de Azure AD para la organización local. Si existe, la confianza de federación existente se usa para admitir la implementación híbrida. Si no existe, el asistente crea una confianza de federación para la organización local con el sistema de autenticación de Azure AD. Asimismo, el asistente agrega cualquier dominio seleccionado dentro del Asistente para configuración híbrida a la confianza de federación de la organización local.
    
    Para obtener más información, vea [Uso compartido](https://technet.microsoft.com/es-es/library/dd638083\(v=exchg.150\)).

  - **Relaciones de organización**   Las relaciones de organización son necesarias para la organización local y la organización de Exchange Online y se configuran automáticamente mediante el asistente para la configuración híbrida. Una relación de la organización define el nivel de información de disponibilidad compartida para una organización.
    
    De manera predeterminada, el nivel de uso compartido de acceso a datos de disponibilidad es **Acceso con tiempo, asunto y ubicación de disponibilidad** para las relaciones de organizaciones locales y de Exchange Online. Si desea modificar el acceso de uso compartido de disponibilidad entre los usuarios de la organización local y los de la organización de Exchange Online, configure manualmente el nivel de acceso de relación de la organización una vez completado del asistente para la configuración híbrida.
    
    Para obtener más información, vea [Uso compartido](https://technet.microsoft.com/es-es/library/dd638083\(v=exchg.150\)).

Al configurar una implementación híbrida en su organización, la configuración del acceso compartido del calendario de disponibilidad se configura automáticamente mediante el asistente para la configuración híbrida en todos los casos posibles. Los requisitos de una implementación híbrida son crear una confianza de federación con el sistema de autenticación de Azure AD y configurar relaciones para la organización local y la organización de Exchange Online. Si no desea permitir el uso compartido de información de disponibilidad entre los usuarios de la organización local y los de la organización de Exchange Online en la implementación híbrida, deshabilite manualmente el uso compartido de información de disponibilidad mediante el Shell de administración de Exchange y el cmdlet [Set-HybridConfiguration](https://technet.microsoft.com/es-es/library/hh529932\(v=exchg.150\)) una vez completado el asistente para la configuración híbrida.

Las características de una implementación híbrida que se muestran en la tabla siguiente tienen dependen de las confianzas de federación y de las relaciones de organización.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Área de mensajes</th>
<th>Característica</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Cliente de correo electrónico</p></td>
<td><ul>
<li><p>Seguimiento de mensajes</p></li>
<li><p>Sugerencias de correo electrónico</p></li>
<li><p>Búsqueda en varios buzones de correo</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Cumplimiento</p></td>
<td><ul>
<li><p>Archivado de Exchange Online</p></li>
<li><p>Exhibición de documentos electrónicos en contexto de Exchange</p></li>
</ul></td>
</tr>
</tbody>
</table>

