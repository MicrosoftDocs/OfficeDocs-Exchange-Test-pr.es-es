---
title: 'Resumen de implementación de Mensajería unificada de Exchange 2013 y Lync Server: Exchange 2013 Help'
TOCTitle: Resumen de implementación de Mensajería unificada de Exchange 2013 y Lync Server
ms:assetid: 96fcb0dd-79ee-4e55-9e59-3ee7fbe3c4a1
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb676409(v=EXCHG.150)
ms:contentKeyID: 49895793
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Resumen de implementación de Mensajería unificada de Exchange 2013 y Lync Server

 

_**Se aplica a:** Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2016-12-09_

La mensajería unificada (MU) y Microsoft Lync Server se pueden implementar conjuntamente para ofrecer mensajería de voz, mensajería instantánea, presencia de usuario mejorada, conferencias de audio y vídeo, y una experiencia de mensajería y correo electrónico integrados para los usuarios de su organización. La mensajería unificada se usa para ofrecer servicios de contestador automático, de Outlook Voice Access y de operador automático. Microsoft Lync Server admite características más avanzadas presentes en Enterprise Voice, como la mensajería instantánea (IM), conferencia y llamadas entrantes y salientes. En este tema se describe cómo configurar la mensajería unificada y Microsoft Lync Server para que admitan estas características.


> [!TIP]
> Microsoft Office Communications Server 2007 R2 también se puede implementar junto con la mensajería unificada. En este tema, “Microsoft Lync Server” se refiere a Microsoft Lync Server 2010 o Microsoft Lync Server 2013.



¿Busca más información acerca de Microsoft Lync Server? Vea [Microsoft Lync Server](https://go.microsoft.com/fwlink/p/?linkid=265752).

**Contenido**

Implementar la mensajería unificada de Exchange y Lync Server resumen

Recomendaciones para la configuración de certificados

Pasos para la implementación

Más información

## Implementar la mensajería unificada de Exchange y Lync Server resumen

La mensajería unificada combina mensajería de voz y correo electrónico en una misma infraestructura de mensajería. Microsoft Lync Server Enterprise Voice saca provecho de la infraestructura de mensajería unificada para proporcionar correo de voz, Outlook Voice Access, avisos de llamadas y operadores automáticos.

La siguiente lista muestra los pasos simplificados de implementación para mensajería unificada y Lync Server. Detalles sobre cada paso se incluyen más adelante en este tema.

1.  Instale Microsoft Lync Server en la misma topología en la que se instalarán los servidores de acceso de cliente en los que se ejecutará el servicio de Enrutador de llamada de mensajería unificada de Microsoft Exchange y los servidores de buzones de correo en los que se ejecutará el servicio de mensajería unificada de Microsoft Exchange. Confirme que se crea al menos un grupo de Lync.

2.  Instale un certificado válido y firmado por una entidad pública o privada de certificación (AC) en la que confíe Lync Server.

3.  Instale los servidores de acceso de cliente y servidores de buzones de correo. Verifique la instalación.

4.  Instale un certificado válido y firmado por la misma AC que el certificado que ha instalado en los servidores Lync.

5.  Cree y configure un plan de marcado URI de protocolo de inicio de sesión (SIP).

6.  Añada todos los servidores Acceso de cliente y Buzón de correo al plan de marcado URI de SIP. No obstante, si dispone de varios planes de marcado URI de SIP, deberá agregar todos los servidores Acceso de cliente y Buzón de correo en todos los planes de marcado URI de SIP.

7.  Ejecute el script ExchUcUtil.ps1 desde la \<carpeta de instalación de Exchange\>\\Exchange Server\\Script en un servidor de Buzón de correo.
    

    > [!IMPORTANT]
    > El script ExchUcUtil.ps1 crea una o más puertas de enlace IP de Mensajería unificada para la integración de Lync. Debe deshabilitar las llamadas salientes en todas las puertas de enlace IP de Mensajería unificada excepto una puerta de enlace que creó la secuencia de comandos. Esto incluye deshabilitar las llamadas salientes de las puertas de enlace IP de Mensajería unificada que se crearon antes de ejecutar el script. Para deshabilitar las llamadas salientes en una puerta de enlace IP de Mensajería unificada, vea <A href="disable-outgoing-calls-on-um-ip-gateways-exchange-2013-help.md">Deshabilitar las llamadas salientes de puertas de enlace IP de mensajería unificada</A>.



8.  Ejecute **OcsUmUtil.exe** desde la carpeta %CommonProgramFiles%\\Microsoft Lync Server 2013\\Support en un servidor Lync.

9.  Implemente el servidor de mediación y las puertas de enlace de medios.

10. Instale un certificado en el Servidor de mediación válido y firmado por la misma AC que el certificado que ha instalado en los servidores Lync.

11. Habilite a los usuarios de mensajería unificada y Enterprise Voice.

## Recomendaciones para la configuración de certificados

Debe disponer de un certificado que sea de confianza para los equipos en los que se ejecuta Exchange y aquellos en los que se ejecuta Lync Server. En un entorno que cuente con Lync Server y mensajería unificada, use las siguientes pautas para implementar un certificado de confianza:

  - En sus servidores Lync, servidores de Acceso de cliente, servidores de buzones de correo, servidor de mediación y puertas de enlace de medios, importe un certificado que sea válido y que esté firmado por una AC pública o privada. Debería tratarse de un certificado de confianza de terceras partes o de un certificado de Infraestructura de clave pública (PKI).

  - Es menos complejo si importa el mismo certificado comercial de terceros o PKI en cada servidor de Exchange. Instale también el mismo certificado de confianza en cada equipo que ejecuta un servidor Lync y un servidor de mediación. De esta forma, la implementación del certificado será menos complicada y reducirá la sobrecarga administrativa asociada con la implementación de certificados. No obstante, asegúrese de que obtiene un certificado de confianza que admita nombres alternativos del sujeto (SAN).
    
    Cuando implemente Seguridad de la capa de transporte (TLS) con mensajería unificada, los certificados que se utilizan en el servidor de acceso de cliente y el servidor de buzones de correo deberán contener el nombre de dominio completo (FQDN) del equipo local en el nombre de firmante del certificado. Para solventar esta cuestión, use un certificado público e impórtelo en todos los servidores de acceso de cliente y buzón de correo, todas las puertas de enlace de VoIP, IP PBX y en todos los servidores Lync.
    
    Si la implementación incluye puertas de enlace VoIP o IP PBX y utiliza un SIP protegido o un plan de marcado Protegido, necesitará un certificado de confianza entre los servidores de acceso de cliente y buzón de correo y las puertas de enlace VoIP o IP PBX. También se requiere un certificado de confianza si se usa una conexión directa de SIP. Si usa un SIP protegido o un plan de marcado protegido, puede utilizar el mismo certificado de confianza en los servidores Lync y Exchange que usa en las puertas de enlace VoIP o IP PBX.

  - Cuando conecta servidores de acceso de cliente y buzón de correo a los servidores de Microsoft Lync o a puertas de enlace SIP de terceros o a un equipo telefónico de central de conmutación (PBX), debe usar un certificado que sea válido y firmado por una entidad de certificación de terceros, interna o pública para establecer sesiones seguras. Puede usar un único certificado en todos los servidores de acceso de cliente y buzón de correo siempre que el certificado tenga los FQDN de todos los servidores de acceso de cliente y buzón de correo de la lista de SAN. También puede generar un certificado distinto para cada servidor de acceso de cliente y buzón de correo, con el FQDN del equipo local presente en el nombre común (CN) de firmante o lista SAN del certificado para dicho servidor. La mensajería unificada de Exchange no admite certificados comodín con Microsoft Lync Server.
    
    Es obligatorio proporcionar un nombre de firmante sin comodín para que Lync Server y Exchange funcionen conjuntamente. La mensajería unificada y Lync Server emplean el nombre de firmante para indicar que son interlocutores SIP de confianza. Lync Server también necesita un nombre de firmante sin comodines en algunas situaciones de enrutamiento de llamadas. El FQDN debe utilizarse como el valor de "Emitido a".
    
    En la mensajería unificada de Exchange, no se admiten los comodines en el nombre de certificado. Sin embargo, usted puede poner un comodín en el SAN.

En la siguiente tabla se muestran los requisitos de certificado para instalar y configurar certificados en mensajería unificada de Exchange.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Topología</th>
<th>Configuración de certificados</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Acceso de cliente y buzón de correo en el mismo servidor (sin Lync 2010 o 2013; planes de marcado no habilitados para SIP)</p></td>
<td><p>Un certificado es requerido entre servidores acceso de cliente y buzón de correo. Se trata del mismo certificado que se utiliza entre los servidores de acceso de cliente y buzón de correo y la puerta de enlace VoIP, IP PBX o SBC.</p></td>
</tr>
<tr class="even">
<td><p>Acceso de cliente y buzón de correo en diferentes servidores (sin Lync 2010 o 2013; planes de marcación no habilitados para SIP)</p></td>
<td><p>Se requiere un certificado. El certificado debe coincidir en los servidores de acceso de cliente y buzón de correo. También se necesita un certificado entre los servidores de acceso de cliente y buzón de correo y la puerta de enlace VoIP, IP PBX o SBC. Puede tratarse del mismo certificado o de otro distinto al que se utiliza entre los servidores de acceso de cliente y buzón de correo. En los servidores de acceso de cliente y buzón de correo, puede ejecutar el cmdlet <strong>Create-ExchangeCertificate</strong> desde cualquiera de los servidores.</p></td>
</tr>
<tr class="odd">
<td><p>Acceso de cliente y buzón de correo en el mismo servidor (con Lync 2010 o 2013; planes de marcado no habilitados para SIP)</p></td>
<td><p>Se requiere un certificado. Los servidores de acceso de cliente y buzón de correo deben tener el mismo certificado raíz que los servidores Lync 2010 o 2013.</p></td>
</tr>
<tr class="even">
<td><p>Acceso de cliente y buzón de correo en diferentes servidores (con Lync 2010 o 2013 y planes de marcación SIP)</p></td>
<td><p>Se requiere un certificado. Los servidores de acceso de cliente y buzón de correo deben tener el mismo certificado raíz que los servidores Lync 2010 o 2013.</p></td>
</tr>
</tbody>
</table>


Volver al principio

## Pasos para la implementación

Después de instalar los servidores necesarios en su organización, es necesario realizar una secuencia recomendada de pasos en su Exchange implementación de mensajería unificada y Lync Server para implementar correctamente Enterprise Voice para sus usuarios.

Para obtener más información acerca de Microsoft Lync Server, vea [Microsoft Lync Server](https://go.microsoft.com/fwlink/p/?linkid=265752).

Deberá realizar los siguientes pasos para configurar la mensajería unificada de manera que funcione con las características de Enterprise Voice de Lync Server:

1.  Cree uno o más planes de marcado URI de SIP de la mensajería unificada, de manera que cada uno de ellos lleve a un perfil de ubicación de Lync Server correspondiente. Debe crear un perfil de ubicación de Enterprise Voice para cada plan de marcado de mensajería unificada de Exchange. Puede usar el cmdlet **Get-UMDialPlan** para obtener el FQDN de un plan de marcado URI de SIP. Para obtener más información acerca de cómo crear un plan de marcado URI de SIP, vea [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).
    

    > [!IMPORTANT]
    > Al integrar la mensajería unificada de Exchange y Lync Server, probablemente considere innecesario configurar las reglas de marcado o los grupos de reglas de marcado en la mensajería unificada de Exchange. Lync Server está diseñado para efectuar el enrutamiento de llamadas y la traducción de los números de los usuarios de su organización y seguirá haciéndolo cuando la mensajería unificada realice las llamadas en nombre de los usuarios.



2.  Instale un certificado en los servidores de acceso de cliente y buzón de correo válido y firmado por una AC privada o pública. Se trata de la misma AC que fue utilizada en los servidores de Lync.

3.  Cifrar el tráfico de voz sobre IP (VoIP) mediante la configuración del plan de marcado URI de SIP en el modo SIP protegida o Protegida.
    

    > [!WARNING]
    > Si ajusta la configuración de seguridad en SIP Protegida para que el cifrado sea únicamente obligatorio en el tráfico SIP, esta configuración será insuficiente en un plan de marcado si el grupo de servidores front-end está configurado para que requiera cifrado (lo que significa que el grupo requiere cifrado para tráfico SIP y RTP). Cuando el plan de marcado y la configuración de seguridad del grupo no son compatibles, todas las llamadas a la mensajería unificada de Exchange desde el grupo de servidores front-end serán erróneas, y darán lugar a un error que indicará que tiene una “configuración de seguridad no compatible”.

    
    Aunque un plan de marcado de MU puede configurarse en el modo SIP protegida o Protegida, se recomienda usar el modo Protegida para permitir que los dispositivos Lync Phone Edition funcionen correctamente. Se recomienda esta opción dada la configuración del nivel de cifrado por defecto de Lync Server. Los dispositivos Lync Phone Edition solo funcionan si la configuración de cifrado se muestra en la siguiente tabla. En esta tabla, se muestra la relación entre la configuración de cifrado de los planes de marcado de Lync Server y de mensajería unificada.
    
    **Configuración de cifrado para Lync Phone Edition**
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Lync Server</th>
    <th>Plan de marcado de mensajería unificada</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>Se requiere cifrado (predeterminado)</p></td>
    <td><p>Protegida</p></td>
    </tr>
    <tr class="even">
    <td><p>Cifrado opcional</p></td>
    <td><p>SIP protegida/Protegida</p></td>
    </tr>
    <tr class="odd">
    <td><p>Sin cifrado</p></td>
    <td><p>SIP protegida</p></td>
    </tr>
    </tbody>
    </table>


4.  Agregar todos los servidores Acceso de cliente y Buzón de correo al plan de marcado SIP. Para permitir que el servidor responda a las llamadas entrantes, deberá agregar todos los servidores Exchange a un plan de marcado si desea que respondan a llamadas desde Lync Server.

5.  Configure el modo de inicio y el puerto de escucha de TLS en los servidores de acceso de cliente y buzón de correo que se añadan al plan de marcado URI de SIP y, a continuación, reinicie el servicio de MicrosoftExchange mensajería unificada en cada servidor de buzones de correo y el servicio de MicrosoftExchange Enrutador de llamada de mensajería unificada de cada servidor de acceso de cliente.

6.  Cree y configure un nuevo operador automático de mensajería unificada. Para obtener información más detallada, vea [Configuración de un operador automático de mensajería unificada](set-up-a-um-auto-attendant-exchange-2013-help.md).

7.  Cuando habilite los usuarios para el correo de voz, cree una dirección SIP para los usuarios que utilizarán Enterprise Voice. En la mayoría de casos, la dirección SIP coincidirá con la misma dirección SIP que se empleará cuando un usuario está habilitado para Enterprise Voice. Para obtener información más detallada, vea [Habilitar a un usuario para el correo de voz](enable-a-user-for-voice-mail-exchange-2013-help.md).
    

    > [!IMPORTANT]
    > Los usuarios asociados con un plan de marcado URI de SIP no pueden recibir mensajes de fax entrantes. Esto se debe a que las llamadas entrantes de voz y fax se enrutan mediante un servidor de mediación y la funcionalidad de fax no es compatible cuando se usa un servidor de mediación.



8.  Abra el Shell de administración de Exchange y ejecute el script exchucutil.ps1 ubicado en la carpeta %Archivos de programa%\\Microsoft\\Exchange Server\\V15\\Scripts. El script exchucutil.ps1 hace lo siguiente:
    
      - Concede permiso a Lync Server para leer componentes Exchange MU Active Directory, concretamente el plan de marcado URI de SIP que se ha creado en la tarea anterior. Para obtener más información acerca de cómo utilizar permisos en Active Directory, vea [Cómo utilizar la edición de ADSI para aplicar permisos](https://go.microsoft.com/fwlink/p/?linkid=82751).
    
      - Crea una puerta de enlace IP de MU para todos los grupos de Lync Server o para todos los servidores que ejecuten Lync Server Standard Edition y que alojen usuarios habilitados para Enterprise Voice. Para obtener información más detallada, vea [Cree una puerta de enlace IP de mensajería unificada](create-a-um-ip-gateway-exchange-2013-help.md).
    
      - Cree un grupo de extensiones de MU de Exchange para cada puerta de enlace IP de MU. El identificador piloto del grupo de extensiones será el nombre del plan de marcado asociado con la puerta de enlace IP de la mensajería unificada correspondiente. El grupo de extensiones deberá especificar el plan de marcado SIP de mensajería unificada que se usará con la puerta de enlace IP de mensajería unificada.

9.  Habilite a los usuarios de correo de voz. Cuando los habilite, asegúrese de indicar una dirección SIP válida para el usuario y enlácelo con un plan de marcado SIP. Para obtener información más detallada, vea [Habilitar a un usuario para el correo de voz](enable-a-user-for-voice-mail-exchange-2013-help.md).

También debe completar las siguientes tareas para configurar Lync Server y que funcione con la mensajería unificada:

  - Cree perfiles de ubicación o planes de marcación de Lync. El nombre del perfil de ubicación no tiene por qué coincidir con el FQDN de los planes de marcado de UM correspondientes.

  - Asigne perfiles de ubicación para los grupos de Lync Server.

  - Implemente y configure puertas de enlace de medios y servidores de mediación. También deberá importar un certificado desde la misma AC de confianza que se utilizó para los certificados en los servidores de acceso de cliente y buzón de correo y Lync Server.

  - Defina usos telefónicos, cree y asigne directivas de voz y rutas de llamadas salientes.

  - Configure los usuarios de Enterprise Voice y agregue URI de TEL e identificador de SIP.

  - Ejecute **ocsumutil.exe**, que crea los objetos de contacto para Outlook Voice Access y para el operador automático.
    

    > [!NOTE]
    > Al instalar Lync Server, el atributo <STRONG>msRTC-SIPLine</STRONG> se agrega a Active Directory. Si no ha instalado Lync Server en su entorno, este atributo no se agregará a Active Directory y la resolución de nombre del Id. de la persona que llama mediante planes de marcado en un único bosque y en escenarios entre bosques no funcionará adecuadamente, a menos que configure las direcciones proxy de mensajería unificada para usuarios no habilitados para MU.



Cuando haya configurado los servidores de Lync Server y mensajería unificada, debe habilitar al usuario para que use Lync Server e instalar Lync en el equipo cliente del usuario.


> [!IMPORTANT]
> Al integrar la mensajería unificada en Lync Server, las notificaciones de llamadas perdidas no estarán disponibles para los usuarios que tengan un buzón en un servidor de buzones de correo de Exchange 2007 o Exchange 2010. Las notificaciones de llamadas perdidas se generan cuando un usuario se desconecta antes de que la llamada se envíe a un servidor de buzones de correo.



Volver al principio

## Más información

Para obtener más información acerca de cómo realizar las tareas que deben completarse para Microsoft Lync Server, vea [Microsoft Lync Server](https://go.microsoft.com/fwlink/p/?linkid=265752).

