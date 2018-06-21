---
title: 'Asistente de configuración híbrida: Exchange 2013 Help'
TOCTitle: Asistente de configuración híbrida
ms:assetid: 2e6ed294-ee74-4038-8b71-b61786372ba4
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Hh529921(v=EXCHG.150)
ms:contentKeyID: 48268933
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Asistente de configuración híbrida

 

_<strong>Se aplica a:</strong>Exchange Online, Exchange Server 2013, Exchange Server 2016_

_<strong>Última modificación del tema:</strong>2016-12-09_

El tema a continuación le ofrece un breve resumen del proceso de configuración de implementación híbrida de Exchange, las características y opciones disponibles para una implementación híbrida y el motor de configuración híbrida, que ejecuta las acciones esenciales tanto para la configuración como para la actualización de una implementación híbrida.

Para obtener más información sobre las implementaciones híbridas, vea [Implementaciones híbridas de Exchange Server](exchange-server-hybrid-deployments-exchange-2013-help.md).

**Contenido**

Proceso de configuración híbrida

Características de configuración híbrida

Opciones de configuración híbrida

Motor de la configuración híbrida

## Proceso de configuración híbrida

A continuación verá un breve resumen del proceso del Asistente de configuración híbrida. Primero, el asistente crea el objeto **HybridConfiguration** en su Active Directory local. Este objeto Active Directory almacena la información de configuración híbrida para la implementación híbrida y se actualiza mediante el uso del Asistente de administración de configuración híbrida. A continuación, el asistente reúne todos los datos de configuración de topología de Exchange y del Directorio Activo disponibles localmente, los datos de configuración de Office 365 inquilino y de configuración de Exchange Online, define varios parámetros de organización, y finalmente ejecuta una vasta secuencia de tareas de configuración tanto a nivel local como en organizaciones Exchange Online.


> [!IMPORTANT]
> Existen varias consideraciones y requisitos previos importantes que se deben completar antes de usar el Asistente para la configuración híbrida. Debe cumplir los requisitos para las implementaciones híbridas descritos en <A href="hybrid-deployment-prerequisites-exchange-2013-help.md">Requisitos previos de implementación híbrida</A>. Entonces podrá usar el Asistente para la configuración híbrida para configurar la organización de Exchange para la implementación híbrida.



Las fases generales del proceso de configuración de implementación híbrida son:

1.  **Verificar requisitos previos y realizar comprobaciones de topología**   El Asistente para la configuración híbrida verifica que las organizaciones locales y de Exchange Online admitan una implementación híbrida. Algunos de los elementos que el Asistente verifica y comprueba en las organizaciones locales y de Exchange Online son:
    
      - Las versiones de servidores de Exchange local
    
      - Versión Exchange Online
    
      - Configuración y presencia de sincronización de Active Directory
    
      - Dominios federados y aceptados
    
      - Relaciones de confianza de federación y de organización existentes
    
      - Directorios virtuales de servicios Web
    
      - Certificados de Exchange

2.  **Prueba de las credenciales de la cuenta**   Las cuentas de administración híbrida de la organización local y de Office 365 acceden a las organizaciones locales y de Exchange Online para reunir la información de verificación de los requisitos previos y realizar cambios de configuración de parámetros de la organización a fin de habilitar la funcionalidad de implementación híbrida. El Asistente para la configuración híbrida comprueba que las cuentas tengan las credenciales apropiadas y puedan conectarse a las organizaciones locales y de Exchange Online. Las cuentas de administración de implementación híbrida para las organizaciones locales y las organizaciones de Office 365 deben formar parte del grupo de roles de administración de la organización a fin de que el Asistente para la configuración híbrida complete estas tareas de forma correcta.

3.  **Realizar cambios en la configuración de la implementación híbrida**   Después de probar las cuentas de la administración híbrida, realizar las comprobaciones de topología y verificación, y reunir la información de configuración definida en el proceso del asistente, el Asistente para la configuración híbrida realiza los cambios de configuración para crear y habilitar la implementación híbrida. Todos los cambios en la configuración híbrida se registran automáticamente en el registro de configuración híbrida. De manera predeterminada, el registro de configuración híbrida se encuentra en la siguiente ubicación del servidor de buzones local: `%UserProfile%\AppData\Roaming\Microsoft\Exchange Hybrid Configuration`.
    

    > [!IMPORTANT]
    > El flujo de correo entrante está controlado por el registro MX de su organización. El correo electrónico entrante de Internet para una implementación híbrida no está configurado por el asistente de configuración híbrida.



## Características de configuración híbrida

El Asistente para la configuración híbrida habilita automáticamente todas las características de implementación híbrida de forma predeterminada cada vez que se ejecuta. Si desea deshabilitar características de configuración híbridas específicas, debe usar el Shell de administración de Exchange y el cmdlet **Set-HybridConfiguration**. Las siguientes características de implementación híbrida están habilitadas de forma predeterminada por el asistente:

  - **Uso compartido de disponibilidad**   La característica de uso compartido de disponibilidad permite compartir la información del calendario entre los usuarios de organizaciones locales y de Exchange Online. La característica de uso compartido de disponibilidad se habilita como parte de la configuración de relaciones de la organización y compartición federada para las organizaciones locales y de Exchange Online. Para obtener más información, vea [Uso compartido](https://technet.microsoft.com/es-es/library/dd638083\(v=exchg.150\)).

  - **Sugerencias de correo electrónico**   Las sugerencias de correo electrónico son mensajes informativos que se muestran a los usuarios mientras éstos escriben un mensaje. Al habilitar las sugerencias de correo electrónico en la implementación híbrida, los remitentes locales y de Exchange Online pueden ajustar el mensaje que están redactando para evitar situaciones no deseadas o informes de no entrega (NDR) entre las organizaciones. Para obtener más información, vea [MailTips](https://technet.microsoft.com/es-es/library/jj649091\(v=exchg.150\)).

  - **Archivo en línea**  El archivo en línea permite que la organización de Exchange Online aloje los archivos de correo electrónico de usuario para los usuarios locales y los de Exchange Online. Obtenga más información en [Configurar Exchange Online Archiving](http://go.microsoft.com/fwlink/p/?linkid=266565).

  - **Redireccionamiento de Outlook en la web**   El redireccionamiento de Outlook en la web ofrece una URL única y común para obtener acceso a los buzones de correo de locales y de Exchange Online. Los servidores de acceso de clientes redirigen automáticamente las solicitudes de Outlook en la web a los servidores de buzones de correo locales, o bien proporcionan un vínculo a los usuarios para sus buzones de correo en la organización de Exchange Online.

  - **Redireccionamiento de Exchange ActiveSync**  Al mover un buzón de su organización local de Exchange a Exchange Online, todos los clientes que acceden al buzón deben actualizarse para poder usar Exchange Online. Esto incluye los dispositivos de Exchange ActiveSync. La mayoría de los clientes de Exchange ActiveSync se volverán a configurar automáticamente al mover el buzón a Exchange Online. Para obtener más información, vea [Configuración de un dispositivo de Exchange ActiveSync con implementaciones híbridas de Exchange](exchange-activesync-device-settings-with-exchange-hybrid-deployments-exchange-2013-help.md).

  - **Correo seguro**    La característica de correo seguro habilita la entrega segura de mensajes entre la organización local y de Exchange Online mediante el protocolo Seguridad de la capa de transporte (TLS). Las organizaciones locales y de Exchange Online se autentican mutuamente mediante asuntos de certificado digital; los encabezados de correo electrónico y el formato de mensajes de texto enriquecido se preservan en toda la organización.

## Opciones de configuración híbrida

El Asistente para la configuración híbrida le permite seleccionar opciones específicas en varias áreas para la implementación híbrida. Si desea actualizar opciones de configuración híbrida específicas después de configurar inicialmente su implementación híbrida, puede usar el Asistente para la configuración híbrida o el Shell de administración de Exchange para seleccionar distintas opciones de configuración.

En la siguiente tabla, se detallan las opciones principales que el Asistente para la configuración híbrida modifica y configura.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Área de configuración</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Dominios</p></td>
<td><p>El asistente agrega el dominio aceptado a la organización local para flujo del correo híbrido y las solicitudes de detección automática para la organización basada en la nube. Este dominio, denominado el <em>dominio de coexistencia</em>, se agrega como un dominio proxy secundario a cualquier directiva de dirección de correo electrónico que tenga plantillas <em>PrimarySmtpAddress</em> para los dominios seleccionados en el Asistente para configuración híbrida. De manera predeterminada, es &lt;domain&gt;.mail.onmicrosoft.com.</p>
<p>Puede ver el dominio aceptado ejecutando el siguiente comando en el Shell de administración de Exchange de Exchange Online.</p>
<pre><code>Get-AcceptedDomain | FL DomainName, IsCoexistenceDomain</code></pre></td>
</tr>
<tr class="even">
<td><p>Certificado de correo seguro</p></td>
<td><p>El asistente requiere que seleccione un certificado específico emitido por una entidad de certificación (CA) de terceros que se usa para autenticar y proteger los mensajes de correo electrónico enviados entre las organizaciones locales y de Exchange Online.</p></td>
</tr>
<tr class="odd">
<td><p>Compartición federada de Exchange</p></td>
<td><p>El asistente comprueba si existe alguna relación de autenticación de OAuth o una confianza de federación existente con el sistema de autenticación de Azure Active Directory para la organización local. Si existen, la confianza de federación o la autenticación de OAuth existentes se usan para admitir la implementación híbrida. Si no están presentes, el asistente configura la autenticación de OAuth o crea una confianza de federación para la organización local con el sistema de autenticación de Azure AD, según el tipo de configuración local de Exchange. Asimismo, el asistente agrega cualquier dominio seleccionado dentro del Asistente para la configuración híbrida a la confianza de federación, si es necesario.</p>
<p>Además de la configuración de la confianza de federación o la autenticación de OAuth, el asistente también crea y configura las relaciones de organización para las organizaciones locales y de Exchange Online. Estas relaciones de organización permiten al asistente habilitar varias características de implementación híbrida, que incluyen uso compartido de disponibilidad, redireccionamiento de Outlook en la web y sugerencias de correo electrónico.</p></td>
</tr>
<tr class="even">
<td><p>Flujo de correo</p></td>
<td><p>El asistente le permite seleccionar y configurar qué servidores de Exchange van a controlar el transporte de correo seguro entre las organizaciones locales y de Exchange Online. En Exchange 2010, es un servidor Transporte de concentradores. En Exchange 2013, es un servidor de acceso de cliente. En Exchange 2016 y versiones más recientes, es un servidor de buzones de correo.</p>
<p>El asistente configura la organización local de Exchange y Exchange Online para el enrutamiento del correo híbrido. Al configurar los conectores de envío y recepción nuevos y existentes en la organización local y los conectores entrantes y salientes en Exchange Online, el asistente le permite elegir si los mensajes salientes se enviarán a Internet desde la organización de Exchange Online, se enviarán directamente a los destinatarios de correo externo o se enrutarán mediante los servidores de Exchange locales incluidos en la implementación híbrida.</p>

> [!IMPORTANT]
> El flujo de correo entrante está controlado por el registro MX de su organización. El correo electrónico entrante de Internet para una implementación híbrida no está configurado por el asistente de configuración híbrida.


</td>
</tr>
</tbody>
</table>


## Motor de la configuración híbrida

El motor de la configuración híbrida ejecuta las acciones centrales necesarias para configurar y actualizar una implementación híbrida. El motor de configuración híbrida, responsable del procesamiento de las acciones del cmdlet `Update-HybridConfiguration`, compara el estado del objeto *HybridConfiguration*Active Directory con las opciones de configuración actuales de Exchange local y Exchange Online y, a continuación, ejecuta tareas para hacer coincidir las opciones de configuración de implementación con los parámetros definidos en el objeto *HybridConfiguration*Active Directory. Si los estados de configuración de implementación de Exchange local y Exchange Online actuales ya coinciden con las opciones definidas en el objeto *HybridConfiguration*Active Directory, l motor de configuración híbrida no realiza cambios en las organizaciones de Exchange Online o locales.

Al actualizar una implementación híbrida existente, el motor de configuración híbrida realiza los siguientes pasos:

1.  El cmdlet *Update-HybridConfiguration* desencadena el inicio del motor de configuración híbrida.

2.  El motor de configuración híbrida lee el "estado deseado" almacenado en el objeto `HybridConfiguration`Active Directory.

3.  El motor de configuración híbrida detecta los datos de topología y la configuración actual en la organización Exchange local.

4.  El motor de configuración híbrida detecta los datos de topología y la configuración actual en la organización Exchange Online.

5.  En base al estado deseado, los datos de topología y la configuración actual, el motor de configuración híbrida establece la “diferencia” entre la organización local Exchange y Exchange Online y a continuación ejecuta las tareas de configuración para establecer el “estado deseado”.

La siguiente ilustración muestra un resumen de la forma en que el motor de configuración híbrida recupera y modifica el servidor Exchange local y Exchange Online en las opciones de configuración durante el proceso de implementación híbrida.

![Flujo del motor de configuración híbrida](images/Hh529921.7e01b239-b978-4377-9eac-aa5bc4561866(EXCHG.150).gif "Flujo del motor de configuración híbrida")

