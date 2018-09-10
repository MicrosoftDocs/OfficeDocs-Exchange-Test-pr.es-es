---
title: 'Protección del correo de voz: Exchange 2013 Help'
TOCTitle: Protección del correo de voz
ms:assetid: a88d41d5-2e70-4193-bcd3-dec50dff412b
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd351041(v=EXCHG.150)
ms:contentKeyID: 52061923
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Protección del correo de voz

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2016-12-09_

Algunos sistemas de telefonía heredados de central de conmutación (PBX) e IP PBX permiten al autor de la llamada marcar un mensaje de correo de voz como privado, evitando que el destinatario deseado pueda reenviarlo. En sistemas de correo de voz integrados es posible tener acceso de diversos modos a un mensaje de voz, lo que hace más difícil evitar que otras personas tengan acceso a mensajes de voz marcados como privados.

Puede utilizar la mensajería unificada para usar Active Directory Rights Management Services (AD RMS) para proteger los mensajes de voz de una organización. Esta característica se conoce como correo de voz protegido.

Cuando un mensaje de voz está protegido, no solo se impide que el destinatario reenvíe el mensaje, sino que la mensajería unificada garantiza que solo los destinatarios designados tienen acceso al contenido del mensaje. Se tiene acceso a los mensajes de voz protegidos usando MicrosoftOutlook 2010 o posterior, Outlook Web App o Outlook Voice Access.

**Contenido**

Introducción al correo de voz protegido

Introducción a Active Directory Rights Management Services

Características de usuario final y de asistencia al cliente

Estructura de mensajes de voz protegidos

Componer un mensaje de correo de voz protegido

directivas de buzón de mensajería unificada

Notificaciones de mensaje de texto y correo de voz protegido

## Introducción al correo de voz protegido

La característica correo de voz protegido está disponible con la mensajería unificada de Exchange 2010 y versiones posteriores de mensajería unificada. Se puede configurar en una directiva de buzón de mensajería unificada y todos los parámetros de correo de voz protegido se pueden configurar con la consola de administración de Exchange o el Shell en Exchange 2010 o usando el centro de administración (EAC) de Exchange o los cmdlets en el Shell en Exchange 2013.

El correo de voz protegido se implementa aplicando Information Rights Management (IRM) a los mensajes de voz. Cuando los mensajes de voz están protegidos por la mensajería unificada:

  - Los usuarios pueden responder a mensajes de voz protegidos.

  - Los destinatarios de un mensaje de voz no pueden reenviarlo.

  - Los usuarios no pueden guardar una copia del mensaje de voz.

  - Los usuarios no pueden guardar ni copiar el audio adjunto del mensaje de voz.

  - Solo el destinatario o los destinatarios deseados pueden abrir los mensajes de correo de voz.

Los mensajes de voz de contestador automático y los mensajes de voz interpersonales (los que se envían a un usuario mediante Outlook Voice Access) se pueden proteger mediante mensajería unificada. Sin embargo, la protección no se aplicará a los siguientes tipos de mensaje:

  - Mensajes de fax.

  - Mensajes que no son de voz. Por ejemplo, mensajes de correo electrónico o convocatorias de reunión, aunque se hayan creado con Outlook Voice Access (respuestas de voz).

Volver al principio

## Introducción a Active Directory Rights Management Services

AD RMS, un componente de Windows Server 2008 y versiones posteriores, está disponible para ayudar a proteger a los archivos de forma que solo puedan verlos los usuarios indicados por el remitente. AD RMS protege los archivos especificando los derechos que un usuario necesita para tener acceso a ellos. Es posible configurar los derechos para permitir que los usuarios abran, modifiquen, impriman, reenvíen o realicen otras acciones con la información cuyos derechos se administran. Con AD RMS puede proteger datos al distribuirlos fuera de su red.

Un sistema AD RMS tiene un componente servidor y un componente cliente, que incluyen lo siguiente:

  - Un servidor que tenga Windows Server 2008 R2 o una versión posterior instalada que ejecute el rol de servidor de Rights Management Services Active Directory instalado, que administre certificados y licencias.

  - Un servidor de base de datos.

  - El cliente AD RMS. La última versión del cliente AD RMS se incluye como parte de los sistemas operativos Windows 7 y Windows 8.

El componente del servidor consta de diversos servicios Web ejecutados en un servidor de Microsoft, como Windows Server 2008. El componente cliente puede ejecutarse en un sistema operativo cliente o servidor; asimismo, incluye funciones con las cuales una aplicación puede cifrar y descifrar contenido, recuperar plantillas y listas de revocación, y obtener licencias y certificados de un servidor.

Con AD RMS y el cliente AD RMS, se puede fortalecer la estrategia de seguridad de una organización protegiendo información mediante políticas constantes de uso que siguen unidas a la información con independencia de adónde se mueva. Puede utilizar AD RMS para evitar que informes financieros, especificaciones de productos, datos de clientes y mensajes de correo electrónico o mensajes de voz confidenciales acaben en las manos equivocadas, intencionada o accidentalmente. Para obtener más información, vea [Introducción a AD RMS](https://go.microsoft.com/fwlink/p/?linkid=199436).

En la mensajería unificada de Exchange, puede usar las características de Information Rights Management (IRM) para aplicar protección permanente a mensajes y datos adjuntos.

Al usar las características de IRM y correo de voz protegido, la organización y los usuarios pueden controlar los derechos de los destinatarios para tener acceso a los mensajes de correo electrónico y de correo de voz. IRM también puede usarse para restringir las acciones de los destinatarios como reenviar un mensaje, imprimir un mensaje o los datos adjuntos o extraer el contenido de un mensaje o los datos adjuntos mediante copiar y pegar.

## Requisitos de IRM

Antes de poder implementar IRM en Exchange, instale y configure la infraestructura AD RMS. Para obtener más información, vea [Servicios de administración de Active Directory Rights](https://go.microsoft.com/fwlink/p/?linkid=199439). Para implementar IRM con el fin de admitir correo de voz protegido en la organización de Exchange, la organización debe cumplir con los requisitos siguientes.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Servidor</th>
<th>Requisito</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Clúster de AD RMS</p></td>
<td><ul>
<li><p>Windows Server 2008 R2 Standard o Enterprise con SP1 o Windows Server 2012 Standard o Datacenter. Para obtener más información acerca de los requisitos del sistema, vea <a href="exchange-2013-system-requirements-exchange-2013-help.md">Requisitos del sistema para Exchange 2013</a>.</p></li>
<li><p><strong>Punto de conexión de servicio (SCP)</strong>   Las aplicaciones compatibles con Exchange 2013 y AD RMS usan el SCP registrado en Active Directory para detectar el clúster de AD RMS y las URL. AD RMS permite registrar el SCP desde la instalación de AD RMS. Si la cuenta que se usa para configurar AD RMS no es miembro del grupo de seguridad Admins. de empresas, se puede realizar el registro de SCP después de la instalación. Este es el único SCP para AD RMS en un bosque de Active Directory.</p></li>
<li><p><strong>Permisos</strong>   Se deben asignar permisos de lectura y ejecución a los servidores en el grupo de servidores de Exchange o los servidores Exchange individuales en la canalización de certificación del servidor AD RMS. La ruta predeterminada es \inetpub\wwwroot\_wmcs\certification\ServerCertification.asmx en los servidores AD RMS.</p></li>
<li><p><strong>Superusuarios de AD RMS</strong>   Para habilitar el descifrado de transporte, el descifrado de informe de diario, IRM en Outlook Web App e IRM para Exchange Search, debe agregar el buzón de entrega federada, un buzón del sistema creado por el programa de instalación de Exchange, al grupo de superusuarios en el clúster de AD RMS. Para obtener información, vea <a href="add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md">Agregar el buzón de la federación para el grupo de usuarios de AD RMS Super</a>.</p></li>
</ul></td>
</tr>
</tbody>
</table>


## Configuración y prueba de IRM

Para configurar las características de IRM debe usar el Shell. Para configurar las características de IRM, use el cmdlet [Set-IRMConfiguration](https://technet.microsoft.com/es-es/library/dd979792\(v=exchg.150\)). Para obtener más información acerca de cómo configurar las características IRM, vea [Procedimientos de Information Rights Management](information-rights-management-procedures-exchange-2013-help.md).

Después de configurar el servidor de Exchange, puede usar el cmdlet [Test-IRMConfiguration](https://technet.microsoft.com/es-es/library/dd979798\(v=exchg.150\)) para realizar pruebas de un extremo a otro de la implementación de IRM. Este cmdlet comprueba la configuración IRM para una organización y debe ejecutarse antes de activar el correo de voz protegido. El cmdlet **Test-IRMConfiguration** realiza las siguientes pruebas:

  - Inspecciona la configuración de IRM para la organización de Exchange.

  - Comprueba el servidor de AD RMS para obtener información sobre la versión y la revisión.

  - Comprueba si RMS puede activar un servidor Exchange al recuperar un certificado de cuenta de derechos y un certificado de emisor de licencias de cliente (CLC).

  - Obtiene plantillas de directiva de derechos de AD RMS desde el servidor de AD RMS.

  - Comprueba si el remitente especificado puede enviar mensajes protegidos con IRM.

  - Recupera una licencia de uso de superusuario para el destinatario especificado.

  - Obtiene una licencia previa para el destinatario especificado.

Volver al principio

## Características de usuario final y de asistencia al cliente

El software de cliente de correo electrónico que se usa para escuchar un mensaje de correo de voz debe ser compatible con IRM y saber cómo leer un mensaje de voz protegido por mensajería unificada. Los clientes de correo electrónico compatibles incluyen MicrosoftOutlook 2010 o versiones posteriores, Outlook Web App y Outlook Voice Access. La siguiente tabla contiene una lista de clientes de correo electrónico e indica si son compatibles.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Cliente de correo electrónico</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook</p></td>
<td><ul>
<li><p>Los mensajes de voz protegidos son compatibles en Outlook 2010 y versiones posteriores.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Outlook Web App</p></td>
<td><ul>
<li><p>Outlook Web App en Exchange 2010 o versiones posteriores son compatibles con los mensajes de correo de voz protegido. Las versiones anteriores de Outlook Web App, conocidas como Outlook Web Access, no los admiten.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Outlook Voice Access</p></td>
<td><ul>
<li><p>Outlook Voice Access en Exchange 2010 y versiones posteriores admiten correo de voz protegido. Outlook Voice Access que se incluye con Exchange 2007 no es compatible con correo de voz protegido.</p></li>
<li><p>El buzón de correo del usuario debe residir en un servidor de buzones de correo en Exchange 2010 o una versión posterior.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Windows Mobile o Windows Phone</p></td>
<td><ul>
<li><p>Windows Mobile no es compatible con el correo de voz protegido. Sin embargo, Windows Phone 7 y Windows Phone 8 son compatibles con el correo de voz protegido.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Exchange ActiveSync</p></td>
<td><ul>
<li><p>El correo de voz protegido es compatible con Exchange 2010 SP1 y versiones posteriores.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Otros clientes de correo electrónico</p></td>
<td><ul>
<li><p>No se admite correo de voz protegido.</p></li>
</ul></td>
</tr>
</tbody>
</table>


Volver al principio

## Estructura de mensajes de voz protegidos

En cada mensaje de correo de voz protegido intervienen realmente dos mensajes. El primer mensaje es el mensaje externo, que no está cifrado. Contiene un archivo de datos adjuntos llamado message.rpmsg. Los datos adjuntos contienen el mensaje de voz protegido por IRM y datos de control de administración de derechos internos. Los datos de control de administración de derechos incluyen una clave de contenido e información de derechos que especifican quién tiene acceso al mensaje de voz y cómo puede hacerlo.

Los mensajes de voz protegidos se muestran en la bandeja de entrada del usuario, en la carpeta de búsqueda **Correo de voz**. El usuario puede escuchar los mensajes de voz utilizando el reproductor de sonido integrado como si fuera un mensaje de voz normal, con la excepción de que el botón de reenviar está desactivado y se muestra una nota en la parte superior del mensaje indicando que está protegido y que no puede reenviarse.

En los clientes de correo electrónico que no admite el correo de voz protegido, se muestra el cuerpo del mensaje externo. Los administradores pueden incluir texto cuando el software del cliente no admita el correo de voz protegido usando las directivas de buzones de correo de mensajería unificada. Puede personalizar el texto predefinido que se incluye en el mensaje de correo electrónico configurando una directiva de buzones de correo de mensajería unificada. Por ejemplo, podría configurar la directiva de buzón de mensajería unificada con texto predefinido como *"No puede abrir este mensaje de voz porque está protegido. Para ver o escuchar este mensaje de voz, inicie sesión en su buzón de https://mail.contoso.com o llame al +1 (425) 555-1234 para llamar a Outlook Voice Access"*.

Volver al principio

## Componer un mensaje de correo de voz protegido

Hay dos situaciones en las que se pueden crear mensajes de voz protegidos:

  - **Contestador automático**   El contestador automático se activa cuando un autor de llamada llama a un usuario con mensajería unificada que no puede responder o que deriva la llamada directamente al buzón de voz. En este caso, el sistema de correo de voz reproducirá una serie de instrucciones después de que el autor de la llamada grabe su mensaje de voz.
    
    Podrá elegir entre diferentes opciones, como la posibilidad de marcar el mensaje de voz como privado presionando la tecla almohadilla (\#). Si el autor de la llamada presiona la tecla \#, puede seguir las instrucciones de la mensajería unificada para marcar el mensaje como privado, quitarle la marca de privado o marcarlo como mensaje de importancia alta. En el siguiente diagrama se exponen las opciones del menú a disposición del autor de la llamada al dejar un mensaje de voz privado para un usuario.
    

    > [!NOTE]
    > En las llamadas de contestador automático, la mensajería unificada usa la configuración del correo de voz protegido de las directivas de buzones de correo de mensajería unificada del destinatario del mensaje, porque no se comprueba la identidad del autor de la llamada.

    
    **Crear un mensaje de correo de voz protegido mediante contestador automático**
    
    ![Crear un correo de voz protegido usando respuesta de llamada](images/Dd351041.4e9f50bf-5066-4d0a-b3eb-0515a2fc4560(EXCHG.150).jpg "Crear un correo de voz protegido usando respuesta de llamada")  

  - **Outlook Voice Access**   Outlook Voice Access permite que los usuarios habilitados para mensajería unificada tengan acceso a su buzón de correo mediante teléfonos analógicos, digitales o móviles marcando su número de Outlook Voice Access. Existen dos interfaces de usuario de mensajería unificada disponibles para los usuarios que tienen habilitada la mensajería unificada: la interfaz de usuario de teléfono (TUI) y la interfaz de usuario de voz (VUI).
    
    Los usuarios de Outlook Voice Access pueden buscar contactos en el directorio y enviarles mensajes de voz. Si se activa el correo de voz protegido para usuarios con mensajería unificada habilitada, el autor de la llamada puede marcar los mensajes como privados después de grabarlos. Alternativamente, los administradores pueden configurar una directiva de buzón de mensajería unificada para garantizar que todos los mensajes de voz enviados por usuarios autenticados están protegidos por mensajería unificada.
    

    > [!NOTE]
    > Si se autentica el autor de la llamada, se aplican los ajustes de correo de voz protegido de su directiva de buzones de correo de mensajería unificada, independientemente de los ajustes del destinatario del mensaje de voz.

    
    **Creación de un mensaje de correo de voz protegido mediante la interfaz de usuario de voz**
    
    ![Crear correo de voz protegido mediante la interfaz de voz](images/Dd351041.6b425ee4-5171-4a63-961f-bdbc6c79e1be(EXCHG.150).jpg "Crear correo de voz protegido mediante la interfaz de voz")  
    
    **Creación de un mensaje de correo de voz protegido mediante la interfaz de usuario de teléfono**
    
    ![Crear un correo de voz protegido mediante marcación por tonos](images/Dd351041.dd58fd38-c4c3-437c-adc1-497deb3c8a9f(EXCHG.150).jpg "Crear un correo de voz protegido mediante marcación por tonos")  

Volver al principio

## directivas de buzón de mensajería unificada

Puede crear una directiva de buzones de correo de mensajería unificada para aplicar un conjunto común de opciones de directiva de mensajería unificada, como opciones de directiva del PIN, restricciones de marcado y ajustes de correo de voz protegido para una serie de buzones de correo con mensajería unificada habilitada. Para obtener más información acerca de directivas de buzón de mensajería unificada, vea [Administrar una directiva de buzones de correo de mensajería unificada](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/set-up-voice-mail/manage-um-mailbox-policy).

Puede usar el EAC o el cmdlet **Set-UMMailboxPolicy** en el Shell para configurar las opciones de correo de voz protegido. En la siguiente tabla se muestra la configuración del correo de voz protegido que puede definirse.

**Ajustes de correo de voz protegido**


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Parámetro de Shell</th>
<th>¿La configuración está disponible en el EAC?</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>ProtectAuthenticatedVoiceMail</em></p></td>
<td><p>Sí</p></td>
<td><p>El parámetro <em>ProtectAuthenticatedVoiceMail</em> especifica si un usuario habilitado para mensajería unificada puede usar comandos de voz cuando usa Outlook Voice Access para tener acceso al buzón. El valor predeterminado es <code>None</code>. Esto indica que no se aplica protección al componer el mensaje de voz y que el autor de la llamada no puede marcarlo como privado. Si el valor se establece en <code>Private</code>, solo se protegen los mensajes que el autor marca como privados. Si el valor se establece en <code>All</code>, se protegen todos los mensajes de correo de voz, independientemente de lo que indique el autor.</p></td>
</tr>
<tr class="even">
<td><p><em>ProtectUnauthenticatedVoiceMail</em></p></td>
<td><p>Sí</p></td>
<td><p>El parámetro <em>ProtectUnauthenticatedVoiceMail</em> especifica si los servidores de buzones de correo que contestan a las llamadas de los usuarios habilitados para mensajería unificada asociados con una directiva de buzones de correo de mensajería unificada crean mensajes de correo de voz protegidos. Esto también se aplica cuando se envía un mensaje desde un operador automático de mensajería unificada a un usuario habilitado para UM. El valor predeterminado es <code>None</code>. Esto indica que no se aplica protección a los mensajes de voz y que el autor de la llamada no puede marcarlo como privado. Si el valor se establece en <code>Private</code>, solo se protegen los mensajes que el autor marca como privados. Si el valor se establece en <code>All</code>, se protegen todos los mensajes de correo de voz, independientemente de si el autor lo ha marcado como privado.</p></td>
</tr>
<tr class="odd">
<td><p><em>ProtectedVoiceMailText</em></p></td>
<td><p>Sí</p></td>
<td><p>El parámetro <em>ProtectedVoiceMailText</em> especifica el texto que se debe incluir en el cuerpo del mensaje externo de un correo de voz protegido. El texto se mostrará en todos los clientes de correo electrónico que no admitan mensajes de correo de voz protegido. Si la propiedad está establecida en <code>Null</code> o vacía, la mensajería unificada proporciona un mensaje predefinido.</p></td>
</tr>
<tr class="even">
<td><p><em>RequireProtectedPlayOnPhone</em></p></td>
<td><p>Sí</p></td>
<td><p>El parámetro <em>RequireProtectedPlayOnPhone</em> especifica si los usuarios asociados con la directiva de buzones de mensajería unificada tienen que escuchar los mensajes de correo de voz protegidos por teléfono (usando Reproducir en teléfono). El valor predefinido es <code>$false.</code>. Si el valor se establece en <code>$true</code>, el reproductor de audio de correo de voz protegido de Outlook o Outlook Web App aparece deshabilitado. Observe que el texto de vista previa del mensaje de voz está accesible en todo momento. El usuario no puede reproducir el archivo de audio con ningún reproductor de medios ni utilizar el reproductor de medios insertado para escuchar el mensaje de voz.</p></td>
</tr>
<tr class="odd">
<td><p><em>AllowVoiceResponseToOtherMessageTypes</em></p></td>
<td><p>Sí</p></td>
<td><p>El parámetro <em>AllowVoiceResponseToOtherMessageTypes</em> especifica si los usuarios autenticados en Outlook Voice Access para tener acceso al correo electrónico pueden crear una respuesta de voz para mensajes de correo electrónico y convocatorias de reunión.</p></td>
</tr>
</tbody>
</table>


Para obtener más información sobre cómo administrar la configuración del correo de voz protegido, consulte [Procedimientos de correo de voz protegidos](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/set-up-client-voice-mail-features/protected-voice-mail-procedures) o [Set-UMMailboxPolicy](https://technet.microsoft.com/es-es/library/bb124903\(v=exchg.150\)).

Volver al principio

## Notificaciones de mensaje de texto y correo de voz protegido

Los usuarios que configuran la cuenta de mensajería unificada para enviar notificaciones de mensaje de texto (conocidas como notificaciones SMS) a su teléfono móvil cada vez que se reciben mensajes de voz recibirán también una transcripción (vista previa del correo de voz) como parte del mensaje de texto. Esto supone un problema de seguridad para los mensajes de voz protegidos, porque el contenido de los mensajes de voz debería estar siempre protegido.

Cuando la mensajería unificada crea una notificación de mensaje de texto para un mensaje de voz protegido, comprueba si el mensaje de voz está marcado como privado. Si lo está, no incluirá la transcripción del texto de audio en el mensaje de texto que se envía al teléfono móvil. En su lugar, aparecerá el siguiente texto: "Utilice Outlook Voice Access para tener acceso a este mensaje de correo de voz protegido."

Volver al principio

