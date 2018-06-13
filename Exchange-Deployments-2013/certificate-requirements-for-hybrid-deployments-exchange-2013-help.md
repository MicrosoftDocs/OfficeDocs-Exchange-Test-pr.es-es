---
title: 'Requisitos de certificados para implementaciones híbridas: Exchange 2013 Help'
TOCTitle: Requisitos de certificados para implementaciones híbridas
ms:assetid: 48d532cc-29f9-4009-9d2d-f19a9c13c320
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Hh563848(v=EXCHG.150)
ms:contentKeyID: 48268930
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Requisitos de certificados para implementaciones híbridas

 

_**Se aplica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2016-12-09_

En una implementación híbrida, los certificados digitales son un componente importante para asegurar la comunicación entre la organización de Exchange local y Office 365. Los certificados le permiten a cada organización de Exchange confiar en las identidades de otros. Los certificados también permiten asegurar que cada organización de Exchange se está comunicando con la fuente correcta.

En una implementación híbrida, varios servicios usan certificados:

  - **Azure Active Directory Connect (Azure AD Connect) con Servicios de federación de Active Directory (AD FS)**   Si elige implementar Azure AD Connect con AD FS como parte de su implementación híbrida, se usa un certificado emitido por una entidad de certificación de confianza de terceros para establecer una confianza entre los clientes web y los proxy del servidor de federación, para firmar tokens de seguridad y para descifrar tokens de seguridad.
    
    Obtenga más información en [Certificados](http://go.microsoft.com/fwlink/p/?linkid=205993).

  - **Federación de Exchange**   Un certificado autofirmado se usa para crear una conexión segura entre los servidores locales de Exchange y el sistema de autenticación de Azure Active Directory.
    
    Para obtener más información, vea [Uso compartido](https://technet.microsoft.com/es-es/library/dd638083\(v=exchg.150\)).

  - **Servicios de Exchange**   Los certificados emitidos por una entidad de certificación de terceros de confianza se usan para ayudar a mantener la seguridad de la comunicación de Capa de sockets seguros (SSL) entre los servidores de Exchange y los clientes. Los servicios que usan certificados incluyen Outlook en la web, Exchange ActiveSync, Outlook Anywhere y el transporte seguro de mensajes.

  - **Servidores de Exchange**   Los servidores existentes de Exchange pueden usar los certificados para ayudar a mantener la seguridad de las comunicaciones de Outlook en la web, el transporte de mensajes y demás. Depende de cómo use los certificados en los servidores de Exchange, puede usar certificados autofirmados o certificados emitidos por un CA de terceros de confianza.

## Requisitos de certificados para una implementación híbrida

Al configurar una implementación híbrida, debe usar y configurar los certificados que ha comprado de una entidad de certificación de terceros de confianza. El certificado usado para el transporte seguro de correo híbrido se debe instalar en los servidores de buzones locales (Exchange 2016 y versiones más recientes), y en los servidores de buzones y de acceso de clientes (Exchange 2013 y versiones anteriores).


> [!IMPORTANT]
> Si está configurando una implementación híbrida en una organización que contiene servidores de Exchange implementados en varios bosques de Active Directory, deberá usar un certificado CA de terceros independiente para <EM>cada</EM> bosque de Active Directory.




> [!NOTE]
> Cuando los servidores de transporte perimetral de Exchange se implementan en una organización local, este certificado también debe instalarse en todos los servidores de transporte perimetral. Para que el correo híbrido seguro funcione correctamente, cada servidor de transporte debe usar un certificado que comparta la misma entidad de certificación emisora y el mismo asunto.



Varios servicios, como AD FS, Exchange la federación, los servicios y Exchange, todos requieren certificados. Según la organización, es posible que decida realizar una de las siguientes opciones:

  - Usar un certificado de terceros que utilizan todos los servicios a través de varios servidores.

  - Usar un certificado de terceros para cada servidor que proporciona servicios.

La elección del mismo certificado para todos los servicios o de un certificado para cada servicio, depende de la organización y del servicio que se está implementando. Aquí hay algunas cosas a tener en cuenta acerca de cada opción:

  - **Certificado de terceros en varios servidores**   Los certificados de terceros usados por los servicios de varios servidores pueden ser un poco más económicos, pero pueden complicar la renovación y el reemplazo. La complicación ocurre porque, cuando es necesario reemplazar un certificado, debe reemplazar el certificado en todos los servidores donde está instalado.

  - **Certificado de terceros para cada servidor**   Mediante el uso de un certificado dedicado para cada servidor que hospeda servicios puede configurar el certificado específicamente para los servicios de ese servidor. Si necesita reemplazar el certificado o renovarlo, solamente necesita reemplazarlo en el servidor donde se instalaron los servicios. No se afectan otros servidores.

Recomendamos usar un certificado de terceros exclusivo para cualquier servidor de AD FS opcional, otro certificado para los servicios de Exchange para su implementación híbrida y, si es necesario, otro certificado en sus servidores de Exchange para otros servicios o características necesarios. La confianza de federación local configurada como parte del uso compartido federado en una implementación híbrida usa un certificado autofirmado de forma predeterminada. A menos que tenga requisitos específicos, no hay necesidad de usar un certificado de terceros con la confianza federada como parte de la implementación híbrida.

Los servicios instalados en un único servidor pueden requerir que configure varios nombres de dominio completos (FQDN) para el servidor. Debería adquirir un certificado que permita el número máximo requerido de nombres de dominio completos. Los certificados consisten en un firmante (también denominado nombre principal) y uno o más nombres alternativos del firmante (SAN). El nombre del firmante es el FQDN para el que se ha emitido el certificado y debería usar el dominio SMTP principal compartido entre las organizaciones locales y de Exchange Online. Los SAN son FQDN adicionales que se pueden agregar a un certificado además del nombre del firmante. Si necesita que un certificado admita cinco FQDN, adquiera un certificado que permita agregar cinco dominios al certificado: un nombre de firmante y cuatro SAN.

La tabla a continuación detalla los nombres de dominio completo (FQDN) mínimos sugeridos que se deberían incluir en los certificados configurados para su uso en una implementación híbrida.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Servicio</th>
<th>FQDN sugerido</th>
<th>Campo</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Dominio SMTP compartido principal</p></td>
<td><p>contoso.com</p></td>
<td><p>Nombre de sujeto</p></td>
</tr>
<tr class="even">
<td><p>Detección automática</p></td>
<td><p>Etiqueta que hace coincidir el FQDN de detección automática de su servidor Acceso de cliente de Exchange 2013, como autodiscover.contoso.com</p></td>
<td><p>Nombre alternativo de sujeto</p></td>
</tr>
<tr class="odd">
<td><p>Transporte</p></td>
<td><p>Etiqueta que coincide con el FQDN externo de sus servidores de transporte perimetral, como edge.contoso.com</p></td>
<td><p>Nombre alternativo de sujeto</p></td>
</tr>
</tbody>
</table>

