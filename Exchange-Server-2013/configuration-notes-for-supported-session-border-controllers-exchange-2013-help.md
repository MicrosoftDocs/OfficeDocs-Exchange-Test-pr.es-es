---
title: 'Notas de configuración de los controladores de borde de sesión admitidos: Exchange 2013 Help'
TOCTitle: Notas de configuración de los controladores de borde de sesión admitidos
ms:assetid: d161f94a-a243-4294-93b3-2bf1dc17b59f
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ673565(v=EXCHG.150)
ms:contentKeyID: 50556889
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Notas de configuración de los controladores de borde de sesión admitidos

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2017-07-25_

Los controladores de borde de sesión (SBC) permiten conectar la red de telefonía local a un centro de datos de Microsoft a través de una conexión WAN pública dedicada. Los SBC se ubican en el borde de la red IP local y se conectan a un segundo SBC en un centro de datos de Microsoft.

Los SBC requieren el uso de certificados digitales para cifrar todo el tráfico entre la organización local y el centro de datos de Microsoft. Debe obtener un certificado digital para el elemento de borde de red, como un controlador de borde de sesión, que esté usando para comunicarse con las implementaciones en línea e híbridas de Exchange. Los certificados digitales establecen la confianza entre la organización local y el centro de datos de Microsoft, y habilitan la Seguridad de la capa de transporte mutua (Mutual TLS). Una vez establecida esta confianza, los elementos de borde de red de la organización local y del centro de datos de Microsoft intercambian claves de sesión y usan estas claves para cifrar el tráfico de datos posterior.

En implementaciones en línea o híbridas, la puerta de enlace IP de mensajería unificada representa un SBC. El nombre de asunto común en el certificado debe coincidir con el valor del nombre de dominio completo (FQDN) del campo Dirección de la puerta de enlace IP de mensajería unificada que se cree. Por ejemplo, si especifica la dirección FQDN sbcexternal.contoso.com en la puerta de enlace IP de mensajería unificada, asegúrese de que el nombre de sujeto y el nombre alternativo del firmante del certificado contengan el mismo valor: sbcexternal.contoso.com. El nombre que use distingue mayúsculas de minúsculas, por lo que debe asegurarse de usar lo mismo en el certificado y en la puerta de enlace IP de mensajería unificada. Si utiliza un SBC Acme Packet y el nombre común no coincide con el FQDN de la puerta de enlace IP de mensajería unificada, la llamada se rechazará con el error 403.


> [!NOTE]
> Dado que los SBC están diseñados para colocarse en el perímetro de la red, también funcionan como un firewall. La configuración de un SBC detrás del firewall de la organización puede causar problemas de configuración y no se admite para la conexión con Office 365.



## Controladores de borde de sesión compatibles

La interoperabilidad de los siguientes SBC se ha probado con resultados satisfactorios en implementaciones en línea e híbridas de Exchange. Tenga en cuenta que las capacidades y compatibilidades de los SBC pueden variar, y la forma en la que se configuran puede ser diferente en función de otros equipos de la red. Vea con el fabricante del SBC para saber si hay notas de configuración específicas para la mensajería unificada en una implementación en línea o híbrida.


> [!NOTE]
> En línea MU compatibilidad con sistemas PBX de terceros a través de conexiones directas desde cliente operado SBCs terminará en julio de 2018. Consulte el blog del equipo de Exchange <A href="https://blogs.technet.microsoft.com/exchange/2017/07/18/discontinuation-of-support-for-session-border-controllers-in-exchange-online-unified-messaging/">mensajería unificada de descontinuación de la compatibilidad con controladores de límite de sesión de Exchange Online</A> para obtener más información.




<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Proveedor</strong></p></td>
<td><p><strong>Modelo</strong></p></td>
<td><p><strong>Notas de configuración</strong></p></td>
<td><p><strong>Comments</strong></p></td>
</tr>
<tr class="even">
<td><p><a href="http://www.acmepacket.com">Acme Packet</a></p></td>
<td><p>Net-Net 3820 o 4500</p></td>
<td><p><strong>Póngase en contacto con el proveedor del hardware para obtener instrucciones actualizadas acerca de cómo configurar el dispositivo.</strong></p></td>
<td><p>SBC dedicado</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://www.audiocodes.com">AudioCodes</a></p></td>
<td><p>Mediant 1000B MSBG</p></td>
<td><p><strong>Póngase en contacto con el proveedor del hardware para obtener instrucciones actualizadas acerca de cómo configurar el dispositivo.</strong></p></td>
<td><p>SBC dedicado</p></td>
</tr>
<tr class="even">
<td><p><a href="https://www.audiocodes.com">AudioCodes</a></p></td>
<td><p>Mediant 1000B MSBG</p></td>
<td><p><strong>Póngase en contacto con el proveedor del hardware para obtener instrucciones actualizadas acerca de cómo configurar el dispositivo.</strong></p></td>
<td><p>Puerta de enlace IP y SBC</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://www.cisco.com/c/dam/en/us/solutions/collateral/enterprise-networks/unified-access/cube-asr-release-10-0.pdf">Cisco</a></p></td>
<td><p>ASR 1000</p>

> [!NOTE]
> Debe tener instalado IOS 15.4(3)S3 o versiones posteriores.


</td>
<td><p><strong>Póngase en contacto con el proveedor del hardware para obtener instrucciones actualizadas acerca de cómo configurar el dispositivo.</strong></p></td>
<td><p>SBC dedicado</p></td>
</tr>
<tr class="even">
<td><p><a href="https://www.ingate.com/">Ingate</a></p></td>
<td><p>SIParator</p></td>
<td><p><strong>Póngase en contacto con el proveedor del hardware para obtener instrucciones actualizadas acerca de cómo configurar el dispositivo.</strong></p></td>
<td><p>SBC dedicado</p></td>
</tr>
<tr class="odd">
<td><p><a href="http://www.net.com">NET</a></p></td>
<td><p>VX1200 &amp; VX1800</p></td>
<td><p><strong>Póngase en contacto con el proveedor del hardware para obtener instrucciones actualizadas acerca de cómo configurar el dispositivo.</strong></p></td>
<td><p>Opción SBC para un producto de puerta de enlace VoIP</p></td>
</tr>
<tr class="even">
<td><p><a href="http://www.sonus.net/">Sonus</a></p></td>
<td><p>SBC 1000/2000 2.2.1 o posterior</p></td>
<td><p><strong>Póngase en contacto con el proveedor del hardware para obtener instrucciones actualizadas acerca de cómo configurar el dispositivo.</strong></p></td>
<td><p>SBC dedicado</p></td>
</tr>
</tbody>
</table>

