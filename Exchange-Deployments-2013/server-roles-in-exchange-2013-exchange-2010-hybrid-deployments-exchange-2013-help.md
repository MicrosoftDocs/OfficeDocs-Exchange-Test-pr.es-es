---
title: 'Roles de servidor en implementaciones híbridas de Exchange 2013/Exchange 2010: Exchange 2013 Help'
TOCTitle: Roles de servidor en implementaciones híbridas de Exchange 2013/Exchange 2010
ms:assetid: 7d774948-94f9-4405-af2b-0c67c0405c0f
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn393966(v=EXCHG.150)
ms:contentKeyID: 59637148
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Roles de servidor en implementaciones híbridas de Exchange 2013/Exchange 2010

Este tema se está redactando.  

_**Se aplica a:**Exchange Online, Exchange Server, Exchange Server 2013_

_**Última modificación del tema:**2017-02-16_

Cuando configura una implementación híbrida en una organización de Exchange 2010, debe instalar al menos un servidor de Exchange 2013 con los roles de servidores Buzón de correo y Acceso de clientes en la organización de Exchange 2010 existente. Los servidores de buzones de correo y de acceso de cliente de Exchange 2013 coordinan comunicaciones entre la organización local de Exchange 2010 existente y la organización de Exchange Online. Esta comunicación incluye las características de mensajería y transporte de mensajes entre las organizaciones locales y de Exchange Online.

Recomendamos instalar más de un servidor de Exchange 2013 en la organización local a fin de aumentar la confiabilidad y la disponibilidad de las características de implementación híbrida.

## Roles del servidor en una implementación híbrida

Aquí se muestra un descripción general rápida de los roles de servidor de Exchange 2013 en una implementación híbrida:

  - **Rol de servidor Acceso de clientes**   El rol de servidor Acceso de clientes de Exchange 2013 continúa proporcionando muchas de las mismas funciones que se brindan en los servidores de acceso de clientes de Exchange 2010 en su organización con algunas adiciones necesarias para admitir una implementación híbrida y la coexistencia con Exchange 2010. El servidor de acceso de cliente también administra los mensajes de correo seguros enviados desde la organización de Exchange Online a la organización local, así como reglas de transporte, directivas de registro y entrega de mensajes a los servidores de buzones de correo en una implementación híbrida. Se configura un conector de recepción dedicado en el servidor Acceso de cliente para admitir el transporte de correo híbrido seguro. Toda la conectividad de cliente, incluido el acceso de cliente de Outlook, Outlook Web App y Outlook en cualquier lugar pasa por el rol de servidor Acceso de clientes. El rol de servidor Acceso de clientes también administra las características de relación entre la organización local y la organización de Exchange Online, como el uso compartido de la disponibilidad.
    
    Para obtener más información, vea [Servidor de acceso de cliente](https://technet.microsoft.com/es-es/library/dd298114\(v=exchg.150\)).

  - **Rol de servidor Buzón de correo**   El rol de servidor Buzón de correo de Exchange 2013 administra los mensajes de correo seguros enviados a la organización de Exchange Online desde la organización local. Si bien no es lo más común, también puede hospedar buzones de destinatarios locales y comunicarse con la organización de Exchange Online por proxy mediante el servidor de acceso de cliente local. Se configura un conector de envío dedicado de manera predeterminada en el rol de servidor Buzón de correo para admitir el transporte de correo híbrido seguro.
    
    Para obtener más información, vea [Servidor de buzones de correo](https://technet.microsoft.com/es-es/library/jj150491\(v=exchg.150\)).

Según la configuración de implementación híbrida que quiera, un servidor de Exchange 2013 requerirá la instalación de uno o ambos roles de servidor:

  - **Servidor de Exchange único**   Si elige instalar un único servidor de Exchange en su organización local, deberá instalar el rol de servidor Acceso de clientes así como el rol de servidor Buzón de correo en ese único servidor.

  - **Más de un servidor de Exchange**   Si elige instalar más de un servidor de Exchange en su organización local, podrá instalar los roles de servidor en servidores independientes en la organización local. Por ejemplo, puede instalar un servidor de Exchange 2013 que tenga los roles Acceso de clientes y Buzón de correo instalados e instalar también otro servidor de Exchange que solamente tenga instalado el rol de servidor Acceso de clientes. Sin embargo, los procedimientos recomendados y la configuración de servidor recomendada consiste en instalar los roles de servidor Acceso de clientes y Buzón de correo en *todos* los servidores de Exchange 2013 implementados en la organización local.

Obtenga más información acerca del planeamiento de capacidad de Exchange en [Descripción de varias configuraciones del rol del servidor en la planificación de capacidad](https://technet.microsoft.com/library/dd298121\(exchg.141\).aspx).

## Funciones del servidor de Exchange en implementaciones híbridas

Los servidores de Exchange proporcionan varias funciones importantes a su organización local en una implementación híbrida:

  - **Federación**   Los servidores de Exchange 2013 y Exchange 2010 permiten crear una confianza de federación para la organización local con Microsoft Federation Gateway. Microsoft Federation Gateway es un servicio gratuito basado en la nube ofrecido por Microsoft que funciona como agente de confianza entre la organización local y la organización inquilina de Office 365. La federación es un requisito para crear una relación entre organizaciones entre la organización local y la organización de Exchange Online.
    
    Para obtener más información, vea [Federación](https://technet.microsoft.com/es-es/library/dd335047\(v=exchg.150\)).

  - **Relaciones de organización**   Los servidores de Exchange 2013 con el rol de servidor Acceso de clientes permiten la creación de relaciones de organización entre la organización local y la organización de Exchange Online. Las relaciones de organización se requieren para muchos otros servicios en una implementación híbrida, incluido el uso compartido de información de disponibilidad en el calendario, el seguimiento de mensajes y los movimientos de buzones entre las organizaciones locales y de Exchange Online.
    
    Para más información, vea [Uso compartido](https://technet.microsoft.com/es-es/library/dd638083\(v=exchg.150\)).

  - **Transporte de mensajes**   Los servidores de Exchange 2013 con los roles de servidor Buzón de correo y Acceso de clientes son responsables del transporte de mensajes en una implementación híbrida. Cuando se usan conectores de envío y recepción, estos actúan como los extremos de conexión para los mensajes externos entrantes y también entregan los mensajes salientes a Internet y a la organización de Exchange Online.
    
    Para obtener más información, vea [Opciones de transporte en las implementaciones híbridas de Exchange 2013/Exchange 2010](transport-options-in-exchange-2013-exchange-2010-hybrid-deployments-exchange-2013-help.md).

  - **Seguridad de transporte de mensajes**   Los servidores de Exchange 2013 con los roles de servidor Acceso de clientes y Buzón de correo permiten garantizar la comunicación de mensajes entre la organización local y la organización de Exchange Online mediante la función de seguridad de dominio de Exchange 2013. Es posible aumentar la seguridad mediante el cifrado y la autenticación de seguridad de capa de transporte mutua para las comunicaciones de mensajes.
    
    Obtenga más información en [Descripción de la seguridad de dominio](https://technet.microsoft.com/es-es/library/bb124392\(exchg.141\).aspx).

  - **Outlook Web App**   Los servidores de Exchange 2013 con el rol de servidor Acceso de clientes admiten la configuración de un único extremo de dirección URL para conexiones externas a buzones locales y de Exchange Online. En los buzones locales, los servidores de acceso de cliente se configuran para atender las solicitudes de Outlook Web App. En los buzones de correo de una organización de Exchange Online, los servidores de acceso de cliente se configuran para mostrar automáticamente un vínculo al extremo de Outlook Web App en la organización de Exchange Online.
    
    Para más información, vea [Outlook Web App](https://technet.microsoft.com/es-es/library/jj657718\(v=exchg.150\)).

## Topología de servidores de Exchange

Si decide agregar servidores de Exchange 2013 adicionales para admitir la implementación híbrida, el servidor de Exchange se implementa al igual que cualquier otro servidor de Exchange en su organización de Exchange 2010 existente. La configuración de una organización local de Exchange 2010 existente para una implementación híbrida no requiere ninguna topología de servidor de Exchange especial. Sin embargo, debe instalar Exchange 2010 Service Pack 3 (SP3) en los servidores de Exchange 2010 y también debe instalar el paquete de actualización acumulativa 1 (CU1) o posterior de Exchange 2013 para habilitar la compatibilidad y la función híbrida total de Office 365.

En la tabla siguiente se describen brevemente los cambios aplicados en los servicios después de configurar una implementación híbrida.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Servicio</th>
<th>Antes de configurar una implementación híbrida</th>
<th>Después de configurar una implementación híbrida</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Transporte de mensajes (entrantes y salientes)</p></td>
<td><p>Servidor de acceso de cliente de Exchange 2010</p></td>
<td><p>Servidor de acceso de cliente de Exchange 2013 o Exchange Online Protection (EOP) incluidos con Office 365</p></td>
<td><p>El registro MX (agente de intercambio de correo) del dominio permanecerá igual o se actualizará para apuntar a EOP.</p></td>
</tr>
<tr class="even">
<td><p>Dirección URL pública de Outlook Web App</p></td>
<td><p>Servidor de acceso de cliente de Exchange 2010</p></td>
<td><p>Servidor de acceso de cliente de Exchange 2013</p></td>
<td><p>Los servidores de acceso de cliente de Exchange 2013 enviarán mediante proxy solicitudes de Outlook Web App para los buzones locales a los servidores de acceso de clientes de Exchange 2010. Las solicitudes de Outlook Web App para buzones hospedados en Exchange Online se suministran con un vínculo a la dirección URL de Outlook Web App de Exchange Online.</p></td>
</tr>
</tbody>
</table>


## Software de servidores de Exchange

La actualización acumulativa 1 (o posterior) de Exchange 2013 habilita la función de implementación híbrida por medio del asistente de configuración híbrida. Se puede usar cualquier medio de actualización acumulativa 1 (o posterior) de Exchange 2013 cuando se instalen más servidores de Exchange 2013.

Para obtener información acerca de cómo descargar la versión más reciente de Exchange 2013, consulte [Actualizaciones para Exchange 2016](https://technet.microsoft.com/library/jj907309).


> [!IMPORTANT]
> Necesitará licenciar su servidor híbrido al configurar una implementación híbrida con Exchange 2013 o 2010 y Office 365. Para obtener una clave de producto de Exchange Server gratuita para usarla en la configuración de su implementación híbrida, use la <A href="https://aka.ms/hybridkey">herramienta de claves de producto de la edición híbrida</A>.


