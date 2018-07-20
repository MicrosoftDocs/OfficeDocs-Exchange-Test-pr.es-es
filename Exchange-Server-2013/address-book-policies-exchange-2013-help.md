---
title: 'Directivas de la libreta de direcciones: Exchange 2013 Help'
TOCTitle: Directivas de la libreta de direcciones
ms:assetid: d0a916a1-e3ed-49ae-b116-a559be0dcce6
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Hh529948(v=EXCHG.150)
ms:contentKeyID: 49895926
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Directivas de la libreta de direcciones

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_

Aprenda cómo se puede segmentar la lista global de direcciones en grupos específicos para crear LGD personalizadas en Outlook y Outlook Web App.

La segmentación de la lista global de direcciones (LGD) (también denominada *segregación de LGD*) es el proceso por el que los administradores pueden segmentar usuarios en cantidades específicas para proporcionarles vistas personalizadas de la LGD de la organización. Las directivas de libretas de direcciones (ABP) le permiten segmentar usuarios en grupos específicos para proporcionarles vistas personalizadas de la lista global de direcciones (LGD) de la organización. Al crear una ABP, asigna una GAL, una libreta de direcciones sin conexión (OAB), una lista de salas y una o varias listas de direcciones a la directiva. Después puede asignar la ABP a usuarios de los buzones y proporcionarles acceso a una GAL personalizada en Outlook y Outlook Web App. El objetivo es proporcionar un mecanismo más sencillo para cumplir la segmentación de GAL para organizaciones locales que necesiten varias GAL. .


> [!NOTE]
> Las ABP pretenden optimizar la LGD y las listas de direcciones para cada grupo de usuarios, facilitar la visualización del resto de usuarios o la comunicación con otros usuarios en la organización. Las ABP solo crean una separación virtual de usuarios desde una perspectiva de directorio, no una separación legal.



**Contenido**

Cómo funcionan las ABP

Ejemplo de ABP

Entourage, Outlook para Mac y ABP

## Cómo funcionan las ABP

Las ABP contienen las listas siguientes:

  - Una LGD

  - Una OAB

  - Una lista de salas (para fines de reserva)

  - Una o más listas de direcciones

En la siguiente figura, la directiva de libreta de direcciones A consta de un subconjunto de varios objetos de dirección que existen en la organización (se muestra en la parte inferior de la figura). El ámbito que resulta de una ABP equivale al de la LGD contenida en la directiva, en el caso LGD1. Cuando se crea y se asigna la LGD a un usuario, los objetos de dirección en la LGD se convierten en el ámbito de los objetos que el usuario puede ver.

![Información general sobre directivas de libreta de direcciones](images/Hh529948.68084064-7319-431b-be3b-0cce761258b1(EXCHG.150).gif "Información general sobre directivas de libreta de direcciones")

Puede usar los siguientes métodos para asignar ABP a usuarios de correo individuales:


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>¿Buzón nuevo o existente?</th>
<th>Consola</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Nuevo</p></td>
<td><p>Cmdlet <a href="https://technet.microsoft.com/es-es/library/aa997663(v=exchg.150)">New-Mailbox</a> con el parámetro <em>AddressBookPolicy</em></p></td>
</tr>
<tr class="even">
<td><p>Existente</p></td>
<td><p>Cmdlet <a href="https://technet.microsoft.com/es-es/library/bb123981(v=exchg.150)">Set-Mailbox</a> con el parámetro <em>AddressBookPolicy</em></p>
<p></p></td>
</tr>
</tbody>
</table>


Las ABP surten efecto cuando la aplicación cliente de un usuario se conecta a un servidor de acceso de cliente en Exchange 2013. Si cambia la ABP, la ABP actualizada no surtirá efecto hasta que el usuario vuelva a iniciar o a conectar su cliente o hasta que usted reinicie los servidores de acceso de cliente de RPC en el servidor de buzón de Exchange 2013.

## Agente de enrutamiento de directivas de libretas de direcciones

En una organización de Exchange que no usa ABP, se produce lo siguiente al crear un correo electrónico en Outlook o en Outlook Web App y enviarlo a otro destinatario de la organización de Exchange:

1.  La dirección de correo electrónico se resuelve. Por ejemplo, si escribe **kweku@contoso.com** en el campo **Para**, la dirección de correo electrónico SMTP resolvería que el nombre para mostrar del usuario es **Kweku Ako-Adjei**.

2.  Puede ver la tarjeta de contacto de la otra persona. Cuando el nombre se ha resuelto, puede hacer doble clic en el nombre del usuario y ver su información de contacto, como la oficina y el número de teléfono.

Si usa ABP y no quiere que los usuarios de diferentes organizaciones virtuales vean la información potencialmente confidencial del otro, puede activar el agente de enrutamiento de directivas de libretas de direcciones. El agente de enrutamiento de ABP es un agente de transporte que controla cómo se resuelven los destinatarios en su organización. Cuando el agente de enrutamiento de ABP se instala y configura, los usuarios asignados a diferentes LGD aparecen como destinatarios externos que no pueden ver las tarjetas de contacto de los destinatarios externos.

Para más información sobre cómo activar el agente de enrutamiento de ABP en [Activar el enrutamiento de directivas de la libreta de direcciones](https://technet.microsoft.com/es-es/library/jj891095\(v=exchg.150\)), consulte Exchange Online.

Para más información sobre cómo activar el agente de enrutamiento de ABP en Exchange Server, vea [Instalar y configurar al agente de enrutamiento de directivas de libretas de direcciones](install-and-configure-the-address-book-policy-routing-agent-exchange-2013-help.md).

## Ejemplo de ABP

En el siguiente diagrama, Fabrikam y Tailspin Toys comparten la organización de Exchange y el presidente ejecutivo. El presidente ejecutivo es el único empleado común a ambas empresas.

![Dos empresas, un director general](images/JJ657455.c87a5654-d456-4688-acb2-0be15ba1cda6(EXCHG.150).gif "Dos empresas, un director general")

Esta configuración contiene tres ABP:

  - Una incluye los empleados de Fabrikam y el presidente ejecutivo

  - Una incluye los empleados de Tailspin Toys y el presidente ejecutivo

  - Una incluye solo el presidente ejecutivo

Las ABP cumplen con las siguientes reglas:

  - Los usuarios de Tailspin Toys solo pueden visualizar a los empleados de Tailspin Toys y al presidente ejecutivo cuando examinan la LGD.

  - Los usuarios de Fabrikam solo pueden visualizar a los empleados de Fabrikam y al presidente ejecutivo cuando examinan la LGD.

  - El presidente ejecutivo puede ver a todos los empleados de Fabrikam y Tailspin Toys cuando examina la LGD.

  - Los usuarios que ven los miembros del grupo del presidente ejecutivo solo pueden ver grupos dentro de su misma empresa. No ven grupos que existen en la otra empresa.

## Entourage, Outlook para Mac y ABP

Las ABP no funcionan para usuarios de Entourage o de Outlook para Mac que estén conectados a la red corporativa. Cuando se encuentran en la red corporativa, los clientes de Entourage y de Outlook para Mac se conectan directamente al servidor del catálogo global y consultan directamente Active Directory, en lugar de usar el servidor de acceso de cliente. No obstante, los clientes de Outlook para Mac 2011 que se conectan desde Internet pueden usar una OAB o los Servicios web de Exchange (EWS). Como resultado, estos clientes pueden realizar búsquedas en la LGD basada en la ABP asignada. Para obtener más información sobre la administración de Outlook para Mac 2011, vea [Planeamiento de Outlook para Mac 2011](https://go.microsoft.com/fwlink/p/?linkid=231878)

## Más información

[Caso: implementación de directivas de libretas de direcciones](scenario-deploying-address-book-policies-exchange-2013-help.md)

[Procedimientos de directivas de libreta de direcciones](https://technet.microsoft.com/es-es/library/jj891096\(v=exchg.150\)) en Exchange Online

