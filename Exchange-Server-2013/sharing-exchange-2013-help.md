---
title: 'Uso compartido: Exchange 2013 Help'
TOCTitle: Uso compartido
ms:assetid: 09e6732a-4e99-44d0-801d-9463fdc57a9b
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd638083(v=EXCHG.150)
ms:contentKeyID: 48267781
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Uso compartido

 

_**Se aplica a:** Exchange Server 2013, Outlook 2013_

_**Última modificación del tema:** 2015-02-27_

Puede que tenga que coordinar programas con personas de otras organizaciones, con amigos o con familiares para, de este modo, poder trabajar juntos en proyectos o planear eventos sociales. Con Exchange 2013, los administradores pueden configurar distintos niveles de acceso a calendario para permitir que las empresas colaboren con otras empresas y permitir que los usuarios compartan sus programas con otros. El uso compartido de calendario de negocio a negocio se configura creando *relaciones de organización*. El uso compartido de calendario de negocio a negocio se configura aplicando *directivas de uso compartido*.


> [!IMPORTANT]
> Esta característica de Exchange Server 2013 no es totalmente compatible con Office 365 operado por 21Vianet en China y pueden aplicarse ciertas limitaciones en las características. Para obtener más información, consulte <A href="https://go.microsoft.com/fwlink/?linkid=313640">Acerca de Office 365 operado por 21Vianet</A>.



**Contenido**

Escenarios de uso compartido en Exchange 2013

Limitaciones del uso compartido de la disponibilidad

Consideraciones de firewall para el uso compartido federado

Coexistencia con Exchange 2010

Coexistencia con Exchange 2007

Uso compartido de documentos

## Escenarios de uso compartido en Exchange 2013

Los siguientes escenarios de uso compartido se admiten en Exchange 2013:


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Finalidad del uso compartido</th>
<th>Qué opción usar</th>
<th>Requisitos</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Compartir calendarios con una organización de Office 365</p></td>
<td><p>Relaciones entre organizaciones</p></td>
<td><p>La organización de Office 365 está lista para configurarse. El administrador de Exchange local debe configurar una relación de autenticación con la nube (denominada también “federación”) y cumplir una serie de requisitos de software mínimos. Para obtener más información acerca de la configuración de una federación, vea <a href="federation-exchange-2013-help.md">Federación</a>.</p></td>
</tr>
<tr class="even">
<td><p>Compartir calendarios con otra organización de Exchange local</p></td>
<td><p>Relaciones entre organizaciones</p></td>
<td><p>Las organizaciones de Exchange local deben configurar la federación y cumplir una serie de requisitos de software mínimos</p></td>
</tr>
<tr class="odd">
<td><p>Compartir el calendario de un usuario de Exchange con un usuario de Internet</p></td>
<td><p>Directivas de uso compartido</p></td>
<td><p>Ninguno, está listo para configurarse</p></td>
</tr>
<tr class="even">
<td><p>Compartir el calendario de un usuario de Exchange con otro usuario de Exchange local</p></td>
<td><p>Directivas de uso compartido</p></td>
<td><p>Las organizaciones de Exchange local deben configurar la federación y cumplir una serie de requisitos de software mínimos.</p></td>
</tr>
</tbody>
</table>


La siguiente tabla enumera las diferencias entre las relaciones de organizaciones y las directivas de uso compartido.

### Comparación de las relaciones de organizaciones con las directivas de uso compartido

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Funcionalidad</th>
<th>Relación de organización</th>
<th>Directiva de uso compartido</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Requiere una confianza de federación para su organización</p></td>
<td><p>Sí</p></td>
<td><p>Sí en el caso de uso compartido con organizaciones de dominio federado. No se requiere para directivas de uso compartido de Internet.</p></td>
</tr>
<tr class="even">
<td><p>Recomienda que el dominio externo esté federado</p></td>
<td><p>Sí</p></td>
<td><p>Sí en el caso de uso compartido con organizaciones de dominio federado. No se requiere para directivas de uso compartido de Internet.</p></td>
</tr>
<tr class="odd">
<td><p>Permite el uso compartido de información de disponibilidad (incluido el asunto y la ubicación) con organizaciones externas para un grupo de varios usuarios.</p></td>
<td><p>Sí</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Permite el uso compartido de carpetas de calendario con información de disponibilidad</p></td>
<td><p>No</p></td>
<td><p>Sí</p></td>
</tr>
<tr class="odd">
<td><p>Permite el uso compartido de carpetas de calendario con información de disponibilidad, incluido el asunto y el cuerpo</p></td>
<td><p>No</p></td>
<td><p>Sí</p></td>
</tr>
<tr class="even">
<td><p>Requiere que los usuarios envíen una invitación de uso compartido a los destinatarios externos</p></td>
<td><p>No</p></td>
<td><p>Sí</p></td>
</tr>
<tr class="odd">
<td><p>Proporciona un método de acceso</p></td>
<td><p>Su servidor de acceso de cliente tiene acceso al servidor de acceso de cliente de la organización externa y recupera la información de disponibilidad para el usuario externo cuando se lo solicita.</p></td>
<td><p>El servidor de acceso de cliente tiene acceso al servidor de acceso de cliente de la organización externa y se suscribe a la carpeta de calendario del usuario externo. Para las directivas de uso compartido de Internet, los usuarios externos tienen acceso a una dirección URL restringida o pública en el servidor de acceso de cliente.</p></td>
</tr>
<tr class="even">
<td><p>Puede aplicarse a todos los dominios externos</p></td>
<td><p>No (relación de uno a uno entre dos organizaciones de Exchange 2013)</p></td>
<td><p>Sí</p></td>
</tr>
<tr class="odd">
<td><p>Proporciona a los usuarios distintas experiencias de uso compartido con destinatarios externos</p></td>
<td><p>No</p></td>
<td><p>Sí, en función de la directiva de uso compartido que se aplica</p></td>
</tr>
<tr class="even">
<td><p>Deshabilita el uso compartido para algunos usuarios</p></td>
<td><p>Sí, mediante la especificación de un grupo de distribución de seguridad para la relación de organización</p></td>
<td><p>Sí, mediante la deshabilitación de la directiva de uso compartido que se aplica</p></td>
</tr>
<tr class="odd">
<td><p>Requiere que el buzón de correo se encuentre en un servidor de buzones de correo de Exchange 2013</p></td>
<td><p>No</p></td>
<td><p>Sí</p></td>
</tr>
</tbody>
</table>


Volver al principio

## Limitaciones del uso compartido de la disponibilidad

Las limitaciones siguientes se aplican cuando se comparte información de disponibilidad entre organizaciones de Exchange:

1.  **Outlook Web Access 2003**   Cuando un usuario de una organización de Exchange 2003 usa Outlook Web para acceder a la disponibilidad de usuarios en una organización de Exchange 2013 remota, la solicitud da un resultado erróneo. Las conexiones de Outlook Web Access desde Exchange 2003 no pueden efectuar conexiones WebDAV (de sistema distribuido de creación y control basado en web) con una carpeta del sistema de disponibilidad para recuperar la información de disponibilidad de los usuarios remotos. Debido a que Exchange 2013 no es compatible con las conexiones WebDAV, el servidor Exchange 2003 no se puede conectar a Externa (FYDIBOHF25SPDLT) en el servidor CAS de Exchange 2013 para las solicitudes de Outlook Web Access. Los clientes de Outlook no experimentan esta limitación debido a que usan MAPI en lugar de WebDAV al conectarse a "Externa" (FYDIBOHF25SPDLT).

2.  **Latencia de la red de área extensa (WAN)**   En las organizaciones de Exchange 2003, las réplicas de todas las carpetas de disponibilidad deben residir en los servidores de buzones de correo de Exchange 2010 SP2 o superior. En los entornos en los que las bases de datos de carpetas públicas de Exchange 2003 se ubican en varios sitios físicos, es posible que se produzcan problemas de latencia excesiva y de rendimiento, si las consultas de disponibilidad interna tienen que atravesar vínculos WAN para acceder a las bases de datos de carpetas públicas de Exchange 2010 que no se encuentran en el mismo sitio físico.

3.  **Período de información de disponibilidad**   Las solicitudes de información de disponibilidad efectuadas a una organización de Exchange 2007 desde una organización de Exchange 2013 pueden dar un resultado erróneo debido a un error de coincidencia en el período de información de disponibilidad solicitado. De forma predeterminada, Exchange 2007 acepta solicitudes de disponibilidad de 42 días de información de disponibilidad y Exchange 2013 puede solicitar 62 días de información de disponibilidad. Si la solicitud sobrepasa el límite de 42 predeterminado impuesto por Exchange 2007, la solicitud será errónea.
    
    Ejecute los pasos siguientes para configurar los servidores CAS de Exchange 2007 para que acepten solicitudes de información de disponibilidad por un período más largo:
    
    1.  En todos los servidores CAS de Exchange 2007, abra el archivo siguiente con un editor de texto como el Bloc de notas: \<Ruta de instalación de Exchange\>\\V14\\ClientAccess\\ExchWeb\\EWS\\web.config
        

        > [!WARNING]
        > Antes de realizar cambios en el archivo web.config, haga una copia y guárdela en un lugar seguro.

    
    2.  Busque la sección **appSettings** en el archivo web.config.
    
    3.  Agregar una nueva clave"\<add key="maximumQueryIntervalDays" value="62" /\>" y guarde el archivo web.config.
        

        > [!NOTE]
        > El valor maximumQueryIntervalDays no está presente de forma predeterminada. Cuando este valor no está presente, Exchange 2007 emplea el intervalo predeterminado de 42 días.

    
    4.  Detenga y reinicie Microsoft Internet Information Services (IIS) en todos los servidores CAS de Exchange 2007.

4.  **Organizaciones de Exchange que tengan tanto usuarios locales como usuarios de nube**   Si configura el uso compartido de calendario con otra organización de Exchange que está configurada en una implementación híbrida con Microsoft Office 365, las búsquedas de disponibilidad (libre/ocupado) para usuarios basados en Office 365 o remotos que se han desplazado a la nube serán erróneas. Dado que la relación de organización para su organización de Exchange está establecida con la organización de Exchange local remota, y no en la organización de Exchange Online basada en Office 365, la solicitud de disponibilidad no puede consultar a los usuarios basados en Office 365. Exchange 2013 no admite la funcionalidad para enviar por proxy estas solicitudes de disponibilidad mediante la organización local al servicio de Office 365.

Para obtener información acerca de cómo configurar el uso compartido de disponibilidad entre las implementaciones comunes de Exchange, vea [Configuración del uso compartido federado entre organizaciones de Exchange](configuring-federated-sharing-between-exchange-organizations-exchange-2013-help.md).

## Consideraciones de firewall para el uso compartido federado

Las características del uso compartido federado requieren que los servidores de acceso de cliente de la organización tengan acceso saliente a Internet con HTTPS. Debe permitir el acceso HTTPS saliente (puerto 443 para TCP) a todos los servidores de buzones de correo de Exchange 2013 de la organización.

Para permitir que una organización externa tenga acceso a la información de disponibilidad de su organización, debe publicar un servidor de acceso de cliente en Internet como mínimo. Esto requiere acceso HTTPS entrante de Internet al servidor de acceso de cliente. Los servidores de acceso de cliente de los sitios de Active Directory que no tienen un servidor de acceso de cliente publicado en Internet pueden usar servidores de acceso de cliente de otros sitios de Active Directory a los que tengan acceso mediante Internet. Los servidores de acceso de cliente que no se publican en Internet deben tener la URL externa del directorio virtual de servicios que se establece con la URL que es visible a las organizaciones externas.

Volver al principio

## Coexistencia con Exchange 2010

En organizaciones que contienen servidores de Exchange 2010 y Exchange 2013, los usuarios que cuentan con un buzón de correo en un servidor Buzón de correo de Exchange 2010 pueden usar las relaciones de organizaciones para compartir información de disponibilidad con destinatarios de organizaciones de dominio federado externas de Exchange 2013. Los servidores de buzones de correo y de acceso de clientes de Exchange 2010 deben ejecutar SP2 o superior, y deben tener al menos un servidor de acceso de clientes de Exchange 2013 en la organización de Exchange 2010.

## Coexistencia con Exchange 2007

En organizaciones que contienen servidores de Exchange 2013 y Exchange 2007, los usuarios que cuentan con un buzón de correo en un servidor Buzón de correo de Exchange 2007 pueden usar las relaciones de organizaciones para compartir información de disponibilidad con destinatarios de organizaciones de dominio federado externas. El servidor Buzón de correo debe ejecutar Exchange 2007 SP2 o superior, y usted debe tener al menos un servidor de acceso de cliente de Exchange 2013 en la organización de Exchange. Puede usar las relaciones de organizaciones mediante la introducción de un solo servidor de acceso de cliente de Exchange 2013 en la organización, a fin de brindar una solución más sólida que las soluciones que sincronizan la información de disponibilidad y requieren sincronización de la LGD.

Al usar Outlook 2010 o Outlook Web App para programar una reunión en un servidor de Exchange 2007, un usuario que tenga un buzón de correo en un servidor de Exchange 2007 podrá ver la información de disponibilidad de un usuario de una organización externa. La información de disponibilidad para buzones de Exchange 2007 es visible para los destinatarios de la organización externa.

Las directivas de uso compartido se asignan a los usuarios de buzones de Exchange 2013. Para usar directivas de uso compartido, un buzón de correo debe estar ubicado en un servidor de buzones de correo de Exchange 2013. Solo los clientes de Outlook 2010 y Outlook Web App se pueden usar para generar o responder invitaciones de uso compartido.

Volver al principio

## Uso compartido de documentos

La tabla siguiente contiene vínculos a temas que le ayudarán a aprender acerca de y a administrar la mensajería unificada en Exchange 2013.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Tema</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="federation-exchange-2013-help.md">Federación</a></p></td>
<td><p>Más información acerca de la infraestructura de confianza subyacente que es compatible con el uso compartido, un método sencillo para que los usuarios compartan información de calendario con los destinatarios externos.</p></td>
</tr>
<tr class="even">
<td><p><a href="organization-relationships-exchange-2013-help.md">Relaciones entre organizaciones</a></p></td>
<td><p>Más información acerca de las relaciones de uno a uno entre las organizaciones de Exchange que habilitan el uso compartido de disponibilidad del calendario.</p></td>
</tr>
<tr class="odd">
<td><p><a href="sharing-policies-exchange-2013-help.md">Directivas de uso compartido</a></p></td>
<td><p>Más información acerca de las directivas de persona a persona que permiten el uso compartido.</p>
<p></p></td>
</tr>
</tbody>
</table>

