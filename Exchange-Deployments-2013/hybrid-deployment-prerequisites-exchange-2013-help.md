---
title: 'Requisitos previos de implementación híbrida: Exchange 2013 Help'
TOCTitle: Requisitos previos de implementación híbrida
ms:assetid: e7454db0-fed4-4662-8890-9501126b1ba2
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Hh534377(v=EXCHG.150)
ms:contentKeyID: 48268940
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Requisitos previos de implementación híbrida

 

_<strong>Se aplica a:</strong>Exchange Online, Exchange Server 2013, Exchange Server 2016_

_<strong>Última modificación del tema:</strong>2017-07-25_

**Resumen:**   Lo que necesita su entorno de Exchange antes de configurar una implementación híbrida.

Antes de crear y configurar una implementación híbrida con el Asistente para la configuración híbrida, su organización existente local de Exchange debe cumplir unos requisitos determinados. Si no cumple estos requisitos, no podrá completar los pasos del Asistente para la configuración híbrida y, por lo tanto, no podrá configurar una implementación híbrida entre su organización local de Exchange y Exchange Online.

## Requisitos previos para la implementación híbrida

Para configurar una implementación híbrida, se requieren los siguientes requisitos previos:

  - **Organización local de Exchange**   Las implementaciones híbridas se pueden configurar para las organizaciones locales basadas en Exchange 2007 o posteriores.
    
    La versión de Exchange que haya instalado en la organización local determina la versión de implementación híbrida que puede instalar. Normalmente, debe configurar la versión de implementación híbrida más reciente que se admita en su organización. Por ejemplo, si la organización local ejecuta Exchange 2007, debe configurar una implementación híbrida basada en Exchange 2013. Para obtener una lista completa de versiones de Exchange Server y Office 365 compatibles con la implementación híbrida en organizaciones, vea la siguiente tabla.
    
    
    <table>
    <colgroup>
    <col style="width: 25%" />
    <col style="width: 25%" />
    <col style="width: 25%" />
    <col style="width: 25%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Entorno local</th>
    <th>Implementación híbrida basada en Exchange 2016</th>
    <th>Implementación híbrida basada en Exchange 2013</th>
    <th>Implementación híbrida basada en Exchange 2010</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>Exchange 2016</p></td>
    <td><p>Compatible</p></td>
    <td><p>No compatible</p></td>
    <td><p>No se admite</p></td>
    </tr>
    <tr class="even">
    <td><p>Exchange 2013</p></td>
    <td><p>Compatible</p></td>
    <td><p>Se admite</p></td>
    <td><p>No se admite</p></td>
    </tr>
    <tr class="odd">
    <td><p>Exchange 2010</p></td>
    <td><p>Se admite</p></td>
    <td><p>Admitido</p></td>
    <td><p>Compatible</p></td>
    </tr>
    <tr class="even">
    <td><p>Exchange 2007</p></td>
    <td><p>No se admite</p></td>
    <td><p>Compatible</p></td>
    <td><p>Compatible</p></td>
    </tr>
    </tbody>
    </table>


  - **Versiones de Exchange locales** Las implementaciones híbridas requieren la actualización acumulativa o el paquete acumulativo de actualizaciones más recientes que estén disponibles para la versión de Exchange instalada en la organización local. Si no puede instalar la actualización acumulativa o el paquete acumulativo de actualizaciones más recientes, también se admite la versión inmediatamente anterior. No se admiten actualizaciones acumulativas o paquetes acumulativos de actualizaciones más antiguos.
    
    Por ejemplo, suponga que ha instalado la Actualización acumulativa 8 de Exchange 2013 en la organización local y que la última versión disponible de Exchange 2013 es la Actualización acumulativa 10. Para continuar en una configuración híbrida compatible, debe actualizar los servidores de Exchange 2013 como mínimo a la Actualización acumulativa 9. Sin embargo, le recomendamos que actualice a la Actualización acumulativa 10.
    
    Las actualizaciones acumulativas y los paquetes acumulativos de actualizaciones se publican con una frecuencia trimestral, por lo que el hecho de mantener los servidores en la actualización acumulativa o el paquete acumulativo de actualizaciones más recientes aporta cierta flexibilidad adicional si periódicamente necesita más tiempo para completar las actualizaciones.

  - **Roles de servidor local** Los roles de servidor que debe instalar en su organización local dependen de la versión de Exchange que haya instalado.
    
      - **Exchange 2010** Al menos un servidor con los roles de servidor Buzón de correo, Transporte de concentradores y Acceso de cliente instalados. Aunque es posible instalar los roles Buzón de correo, Transporte de concentradores y Acceso de cliente en servidores independientes, le recomendamos que los instale todos en cada servidor para proporcionar mayor confiabilidad y mejor rendimiento.
    
      - **Exchange 2013** Al menos un servidor con los roles de servidor Buzón de correo y Acceso de cliente instalados. Aunque es posible instalar los roles Buzón de correo y Acceso de cliente en servidores independientes, le recomendamos que instale los dos en cada servidor para proporcionar mayor confiabilidad y mejor rendimiento.
    
      - **Exchange 2016 y versiones más recientes** Al menos un servidor que tenga instalado el rol de servidor de buzón de correo.
    
    Las implementaciones híbridas también admiten los servidores de Exchange que ejecutan el rol de servidor de transporte perimetral. Los servidores de transporte perimetral también deben actualizarse a la última actualización acumulativa o paquete acumulativo de actualizaciones que estén disponibles para la versión de Exchange que haya instalado. Se recomienda implementar los servidores de transporte perimetral en una red perimetral. Los servidores de buzón de correo y de acceso de cliente no se pueden implementar en una red perimetral.

  - **Office 365**   Las implementaciones híbridas se admiten en todos los planes de Office 365 que admiten Sincronización de Azure Active Directory. Todos los planes de Office 365 Enterprise, Administración Pública, Académico y Mediana Empresa admiten las implementaciones híbridas. Los planes de Office 365 Pequeña Empresa y Hogar no admiten las implementaciones híbridas.
    
    Para obtener más información, consulte [Registro en Office 365](https://go.microsoft.com/fwlink/p/?linkid=203981).

  - **Dominios personalizados**   Registre los dominios personalizados que desee usar en una implementación híbrida con Office 365. Para ello, puede utilizar el portal administrativo de Office 365 o configurar de manera opcional los Servicios de federación de Active Directory (AD FS) en su organización local.
    
    Para obtener más información, consulte [Agregar un dominio y usuarios a Office 365](https://go.microsoft.com/fwlink/p/?linkid=229238).

  - **Sincronización de Active Directory**   Implemente la herramienta de Azure Active Directory Connect para la sincronización de Active Directory con la organización local.
    
    Encontrará más información en: [Opciones para el inicio de sesión de los usuarios en Azure AD Connect](http://go.microsoft.com/fwlink/p/?linkid=723514)

  - **Registros de DNS de Autodiscover**   Configure los registros de DNS públicos de Autodiscover para los dominios de SMTP existentes para que apunten a un servidor local de acceso de cliente de Exchange 2013.

  - **Organización de Office 365 en el Centro de Administración de Exchange (EAC)**   El nodo de la organización de Office 365 se incluye de forma predeterminada en el EAC local, pero debe conectar el EAC a su organización de Office 365 con las credenciales del administrador de Office 365 para poder usar el asistente para la configuración híbrida. Esto también le permite administrar organizaciones de Exchange locales y Online desde una única consola de administración.
    
    Para obtener más información, vea [Administración híbrida en las implementaciones híbridas de Exchange](hybrid-management-in-exchange-hybrid-deployments-exchange-2013-help.md).

  - 
    
    **Certificados**   Instale y asigne servicios de Exchange a un certificado digital válido adquirido de una entidad emisora de certificados (CA) públicos de confianza. Aunque deben usarse certificados autofirmados para la confianza de federación local con Microsoft Federation Gateway, estos certificados no pueden usarse para los servicios de Exchange en una implementación híbrida. La instancia de Internet Information Services (IIS) en los servidores de Exchange configurada en la implementación híbrida debe tener un certificado digital válido adquirido de una entidad emisora de certificados (CA) de confianza. Además, la dirección URL externa de EWS y el extremo de detección automática especificado en el DNS público deben estar incluidos en el Nombre alternativo del firmante (SAN) del certificado. Todo certificado instalado en los servidores Exchange usado para el transporte de correo en la implementación híbrida debe usar el mismo certificado (es decir, uno emitido por la misma CA y con el mismo firmante).
    
    Para obtener más información, vea [Requisitos de certificados para implementaciones híbridas](certificate-requirements-for-hybrid-deployments-exchange-2013-help.md).

  - **EdgeSync**   Si ha implementado los servidores de transporte perimetral en su organización local y desea configurar el servidor de transporte perimetral para transporte de correo seguro, tendrá que configurar EdgeSync antes de usar el asistente para la configuración híbrida. También deberá ejecutar EdgeSync cada vez que aplique una nueva actualización acumulativa o un paquete acumulativo de actualizaciones en un servidor de transporte perimetral.
    

    > [!IMPORTANT]
    > Aunque EdgeSync es un requerimiento para la implementación de servidores de transporte perimetral, se necesitarán configuraciones de transporte manuales adicionales cuando configure servidores de transporte perimetral para el transporte de correo híbrido seguro.

    
    Para obtener más información, vea [Servidores de transporte perimetral con implementaciones híbridas](edge-transport-servers-with-hybrid-deployments-exchange-2013-help.md).

  - **Buzones habilitados para mensajería unificada (UM)** Si tiene buzones habilitados para mensajería unificada y quiere moverlos a Office 365, necesita lo siguiente, además de una implementación híbrida de Exchange. Estos requisitos deben cumplirse **antes** de mover a Office 365 ningún buzón habilitado para mensajería unificada.
    
      - Lync Server 2010, Lync Server 2013 o Skype Empresarial Server 2015 o posterior integrado con su sistema de telefonía local **o**
    
      - Skype Empresarial Online integrado con su sistema de telefonía local **o**
    
      - Una solución PBX o IP-PBX local tradicional.
    
      - Directivas de buzón de mensajería unificada creadas en Exchange Online que reflejen los nombres de las directivas de buzón de mensajería unificada de su organización local.
        

        > [!NOTE]
        > Puede asignar varias directivas de buzón de mensajería unificada locales a una directiva de buzón de mensajería unificada de Exchange Online. Si quiere hacer esto, debe usar el Shell de administración de Exchange para asignar manualmente cada directiva de buzón de mensajería unificada local a una directiva de Exchange Online.

    
    Para obtener más información, consulte [Integración del sistema telefónico con mensajería unificada](https://technet.microsoft.com/es-es/library/jj673558\(v=exchg.150\)), [Asesor de telefonía para Exchange 2013](https://technet.microsoft.com/es-es/library/ee364753\(v=exchg.150\)) y [Configurar el correo de voz de PBX en la nube](https://go.microsoft.com/fwlink/p/?linkid=826207).

## Protocolos de implementación híbrida, puertos y extremos

Los componentes y las características de implementación híbrida requieren determinados protocolos entrantes, puertos y extremos de conexión para que sean accesibles en Office 365 y para que funcionen correctamente. Antes de configurar la implementación híbrida, compruebe que la configuración de seguridad y red local admitan las características y componentes de la siguiente tabla. Además de permitir extremos, puertos y protocolos específicos de entrada, los equipos de la red deben tener también acceso a las direcciones IP, puertos, y direcciones URL mencionadas en [URL de Office 365 e intervalos de direcciones IP](https://go.microsoft.com/fwlink/?linkid=823100).


<table>
<colgroup>
<col style="width: 12%" />
<col style="width: 12%" />
<col style="width: 12%" />
<col style="width: 12%" />
<col style="width: 12%" />
<col style="width: 12%" />
<col style="width: 12%" />
<col style="width: 12%" />
</colgroup>
<thead>
<tr class="header">
<th>Protocolo de transporte</th>
<th>Protocolo de nivel superior</th>
<th>Característica/componente</th>
<th>Extremo local</th>
<th>Ruta de acceso local</th>
<th>Proveedor de autenticación</th>
<th>Método de autorización</th>
<th>¿Preautenticación admitida?</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>TCP 25 (SMTP)</p></td>
<td><p>SMTP/TLS</p></td>
<td><p>Flujo de correo entre Office 365 y local</p></td>
<td><p>Exchange 2016 Mailbox/Edge</p>
<p>Exchange 2013 CAS/EDGE</p>
<p>Exchange 2010 HUB/EDGE</p></td>
<td><p>N/D</p></td>
<td><p>N/D</p></td>
<td><p>Basado en certificados</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>TCP 443 (HTTPS)</p></td>
<td><p>Detección automática</p></td>
<td><p>Detección automática</p></td>
<td><p>Buzón de Exchange 2016</p>
<p>Exchange 2013/2010 CAS</p></td>
<td><p>/autodiscover/autodiscover.svc/wssecurity</p>
<p>/autodiscover/autodiscover.svc</p></td>
<td><p>Sistema de autenticación de Azure AD</p></td>
<td><p>Autenticación WS-Security</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>TCP 443 (HTTPS)</p></td>
<td><p>EWS</p></td>
<td><p>Libre/ocupado, Sugerencias de correo electrónico, Seguimiento de mensajes</p></td>
<td><p>Buzón de Exchange 2016</p>
<p>Exchange 2013/2010 CAS</p></td>
<td><p>/ews/exchange.asmx/wssecurity</p></td>
<td><p>Sistema de autenticación de Azure AD</p></td>
<td><p>Autenticación WS-Security</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>TCP 443 (HTTPS)</p></td>
<td><p>EWS</p></td>
<td><p>Búsqueda en varios buzones de correo</p></td>
<td><p>Buzón de Exchange 2016</p>
<p>Exchange 2013/2010 CAS</p></td>
<td><p>/ews/exchange.asmx/wssecurity</p>
<p>/autodiscover/autodiscover.svc/wssecurity</p>
<p>/autodiscover/autodiscover.svc</p></td>
<td><p>Servidor de autenticación</p></td>
<td><p>Autenticación WS-Security</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>TCP 443 (HTTPS)</p></td>
<td><p>EWS</p></td>
<td><p>Migraciones de buzón</p></td>
<td><p>Buzón de Exchange 2016</p>
<p>Exchange 2013/2010 CAS</p></td>
<td><p>/ews/mrsproxy.svc</p></td>
<td><p>NTLM</p></td>
<td><p>Basic</p></td>
<td><p>Sí</p></td>
</tr>
<tr class="even">
<td><p>TCP 443 (HTTPS)</p></td>
<td><p>Detección automática</p>
<p>EWS</p></td>
<td><p>OAuth</p></td>
<td><p>Buzón de Exchange 2016</p>
<p>Exchange 2013/2010 CAS</p></td>
<td><p>/ews/exchange.asmx/wssecurity</p>
<p>/autodiscover/autodiscover.svc/wssecurity</p>
<p>/autodiscover/autodiscover.svc</p></td>
<td><p>Servidor de autenticación</p></td>
<td><p>Autenticación WS-Security</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>TCP 443 (HTTPS)</p></td>
<td><p>N/D</p></td>
<td><p>AD FS (incluido con Windows)</p></td>
<td><p>Windows 2008/2012 Server</p></td>
<td><p>/adfs/*</p></td>
<td><p>Sistema de autenticación de Azure AD</p></td>
<td><p>Varía según configuración</p></td>
<td><p>2 factores</p></td>
</tr>
<tr class="even">
<td><p>TCP 443 (HTTPS)</p></td>
<td><p>N/D</p></td>
<td><p>Azure Active Directory Connect con AD FS</p></td>
<td><p>Windows 2012 R2 Server</p></td>
<td><p>/adfs/*</p></td>
<td><p>Sistema de autenticación de Azure AD</p></td>
<td><p>Varía según configuración</p></td>
<td><p>2 factores</p></td>
</tr>
</tbody>
</table>


## Herramientas y servicios recomendados

Además de los requisitos previos descritos anteriormente, hay otras herramientas y servicios que son beneficiosos a la hora de configurar implementaciones híbridas con los asistentes para configuraciones híbridas:

  - **Asistente de implementación de Exchange Server**   El Asistente de implementación de Exchange Server es una herramienta gratuita basada en web que le ayuda a implementar Exchange en la organización local, configurar una implementación híbrida entre la organización local y Office 365, o migrar por completo a Office 365. La herramienta hace un conjunto pequeño de preguntas sencillas y, según las respuestas, crea una lista de comprobación personalizada con instrucciones para implementar o configurar Exchange Server. El Asistente de implementación le proporciona exactamente la información que necesita para configurar la implementación híbrida.
    
    Para obtener más información, consulte [Asistente para la implementación de Exchange Server](https://technet.microsoft.com/exdeploy2013).
    
     

  - **Herramienta Analizador de conectividad remota**   La herramienta Analizador de conectividad remota de Microsoft comprueba la conectividad externa de su organización local de Exchange y garantiza que esté lista para configurar una implementación híbrida. Le recomendamos encarecidamente que compruebe su organización local con la herramienta Analizador de conectividad remota antes de configurar la implementación híbrida con el asistente para configuraciones híbridas.
    
    Obtenga más información en [Exchange Remote Connectivity Analyzer](https://testconnectivity.microsoft.com).
    
     

  - **Inicio de sesión único**   El inicio de sesión único permite a los usuarios obtener acceso tanto a la organización local como a la organización de Exchange Online con un solo nombre de usuario y contraseña. Los usuarios están familiarizados con el proceso y los administradores pueden controlar con facilidad las políticas para las cuentas de los buzones de la organización de Exchange Online mediante herramientas de administración local de Active Directory.
    
    Tiene dos opciones al implementar el inicio de sesión único: la sincronización de contraseña y los Servicios de federación de Active Directory. Azure Active Directory Connect proporciona ambas opciones. La sincronización de contraseña permite implementar fácilmente el inicio de sesión único en prácticamente cualquier organización, independientemente de su tamaño. Por esta razón, y debido a que la experiencia del usuario en una implementación híbrida es significativamente mejor cuando está habilitado el inicio de sesión único, se recomienda su implementación. Para las organizaciones muy grandes, como las que tienen varios bosques de Active Directory que es necesario combinar con la implementación híbrida, se requieren los Servicios de federación de Active Directory.
    
    Encontrará más información en: [Inicio de sesión único con implementaciones híbridas](single-sign-on-with-hybrid-deployments-exchange-2013-help.md)

