---
title: 'Information Rights Management: Exchange 2013 Help'
TOCTitle: Information Rights Management
ms:assetid: 6ea3a695-3ddd-4d53-b3c6-90041f44ef64
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd638140(v=EXCHG.150)
ms:contentKeyID: 49895700
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Information Rights Management

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_

Los trabajadores de la información usan el correo electrónico todos los días para intercambiar información confidencial como informes y datos financieros, contratos legales, información confidencial de productos, informes y proyecciones de ventas, análisis competitivos, información de investigación y patentes e información sobre clientes y empleados. Debido a que las personas pueden obtener acceso a su correo electrónico desde prácticamente cualquier lugar, los buzones de correo se han transformado en depósitos que contienen grandes cantidades de información que puede ser confidencial. Como resultado, las fugas de información constituyen una amenaza grave para las organizaciones. Para ayudar a evitar las fugas de información, Exchange Server 2013 de Microsoft incluye características de Information Rights Management (IRM) que ofrecen protección permanente con y sin conexión para los mensajes de correo electrónico y los datos adjuntos.

**Contenido**

¿Qué es la fuga de información?

Soluciones tradicionales para la fuga de información

IRM en Exchange 2013

Aplicar la protección de IRM a mensajes

Escenarios para la protección de IRM

Descifrar mensajes protegidos con IRM para exigir el cumplimiento de directivas de mensajería

Licencia previa

Agentes de IRM

Requisitos de IRM

Configuración y prueba de IRM

Extender Rights Management con el conector Rights Management

## ¿Qué es la fuga de información?

La fuga de información que puede ser confidencial representa un costo para una organización en varios aspectos y puede producir un impacto de amplio espectro en la organización y sus negocios, empleados, clientes y asociados. Las normativas locales e industriales regulan cada vez más la manera de almacenar, transmitir y proteger determinados tipos de información. A fin de evitar la infracción a las normativas vigentes, las organizaciones deben protegerse contra la fuga de información intencionada, inadvertida o accidental.

Éstas son algunas consecuencias que resultan de la fuga de información:

  - **Daños financieros**   Según el tamaño, la industria o las normativas locales, la fuga de información también puede dar como resultado un impacto financiero debido a la pérdida de negocios o a multas y daños punitivos que impongan los tribunales o las autoridades reguladoras. Las sociedades públicas corren el riesgo adicional de perder capitalización del mercado debido a la difusión desfavorable en los medios de comunicación.

  - **Daños en la imagen y la credibilidad**   La fuga de información puede dañar la imagen y la credibilidad de una empresa para sus clientes. Asimismo y según sea la índole de la comunicación, los mensajes de correo electrónico perdidos pueden generar situaciones vergonzosas para el remitente y la organización.

  - **Pérdida de la ventaja competitiva**   Una de las amenazas más serias que surgen de la fuga de información es la pérdida de la ventaja competitiva en el negocio. La divulgación de planes estratégicos o información sobre fusiones y adquisiciones puede conducir a la pérdida de ingresos o de capitalización del mercado. Otras amenazas incluyen la pérdida de información sobre la investigación, los datos analíticos y otra propiedad intelectual.

¿Qué es la fuga de información?

## Soluciones tradicionales para la fuga de información

Aunque las soluciones tradicionales para la fuga de información pueden proteger el acceso inicial a los datos, con frecuencia no ofrecen protección continua. En la tabla siguiente se enumeran algunas de las soluciones tradicionales y sus limitaciones.

### Soluciones tradicionales

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Solución</th>
<th>Descripción</th>
<th>Limitaciones</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Seguridad de la capa de transporte (TLS)</p></td>
<td><p>TLS es un protocolo estándar de Internet que se usa para asegurar las comunicaciones a través de una red por medio del cifrado. En un entorno de mensajería, se usa TLS para asegurar las comunicaciones entre servidores o entre el cliente y el servidor.</p>
<p>De forma predeterminada, Exchange 2010 usa TLS para todas las transferencias internas de mensajes. También se habilita la TLS oportunista de forma predeterminada para las sesiones con hosts externos. En primer lugar, Exchange intenta usar el cifrado TLS para la sesión; pero si no es posible establecer una conexión TLS con el servidor de destino, Exchange usa SMTP. Además puede configurar la seguridad de dominio para exigir el uso de TLS mutua a las organizaciones externas.</p></td>
<td><p>TLS solo protege la sesión SMTP entre dos hosts SMTP. En otras palabras, TLS protege la información en movimiento y no brinda protección en el nivel del mensaje o para la información quieta. A menos que los mensajes estén cifrados con otro método, los mensajes en los buzones del remitente y del destinatario estarán desprotegidos. Puede solicitar TLS solo en el primer salto para el correo electrónico que se envíe fuera de la organización. Después de que un host SMTP remoto externo a la organización recibe el mensaje, lo puede retransmitir a otro host SMTP mediante una sesión no cifrada. Como TLS es una tecnología de capa de transporte, no puede ofrecer control para lo que el destinatario haga con el mensaje.</p></td>
</tr>
<tr class="even">
<td><p>Cifrado de correo electrónico</p></td>
<td><p>Los usuarios pueden usar tecnologías como S/MIME para cifrar los mensajes.</p></td>
<td><p>Los usuarios deciden si se cifrará un mensaje determinado. Hay costos adicionales para la implementación de una infraestructura de clave pública (PKI) y la consiguiente sobrecarga de administración de certificados para los usuarios y la protección de claves privadas. Luego que se descifra un mensaje, no hay control sobre lo que el destinatario puede hacer con la información. La información descifrada se puede copiar, imprimir o reenviar. De forma predeterminada, los datos adjuntos guardados no están protegidos.</p>
<p>La organización no puede tener acceso a los mensajes cifrados con tecnologías como S/MIME. La organización no puede inspeccionar el contenido de los mensajes y, por consiguiente, no puede exigir el cumplimiento de directivas de mensajería, examinar mensajes para detectar virus o contenidos malintencionados ni tomar cualquier otra acción que requiera obtener acceso al contenido.</p></td>
</tr>
</tbody>
</table>


Por último, las soluciones tradicionales no cuentan con herramientas de cumplimiento que apliquen directivas de mensajería uniforme a fin de evitar la fuga de información. Por ejemplo, un usuario envía un mensaje que contiene información confidencial y lo marca como **Confidencial de la compañía** y con la indicación **No reenviar**. Después de enviar el mensaje al destinatario, el remitente o la organización ya no tienen control sobre la información. El destinatario puede reenviar el mensaje (con características tales como reglas de reenvío automático) a cuentas de correo electrónico externas de forma intencionada o inadvertida y exponer a la organización a riesgos de fuga de información considerables.

¿Qué es la fuga de información?

## IRM en Exchange 2013

En Exchange 2013, puede usar las características de IRM para aplicar protección persistente a mensajes y datos adjuntos. IRM usa Active Directory Rights Management Services (AD RMS), una tecnología de protección de información en Windows Server 2008 o posterior. Con las características de IRM en Exchange 2013, su organización y sus usuarios pueden controlar los derechos que tienen los destinatarios para el correo electrónico. IRM también contribuye a permitir o restringir las acciones de los destinatarios como reenviar un mensaje, imprimir un mensaje o los datos adjuntos o extraer el contenido de un mensaje o los datos adjuntos mediante copiar y pegar. Los usuarios de Microsoft Outlook o Microsoft Office Outlook Web App también pueden aplicar la protección IRM, o basarse en las directivas de mensajería de la organización y luego aplicarse mediante reglas de protección de transporte o reglas de protección de Outlook. A diferencia de otras soluciones de cifrado de correo electrónico, IRM permite además que la organización descifre el contenido protegido a fin de exigir el cumplimiento de directivas.

AD RMS usa certificados y licencias basados en lenguaje de marcado con derechos extensible (XrML) para certificar equipos y usuarios, y para proteger el contenido. Cuando se protegen contenidos tales como documentos o mensajes con AD RMS, se adjunta una licencia XrML que contiene los derechos que los usuarios autorizados tienen con respecto al contenido. A fin de obtener acceso al contenido protegido con IRM, las aplicaciones habilitadas para AD RMS deben obtener una licencia de uso para el usuario autorizado del clúster de AD RMS.


> [!NOTE]
> En Exchange&nbsp;2013, el agente de licencia previa adjunta una licencia de uso a los mensajes protegidos con el clúster de AD RMS en la organización. Para obtener más información, vea Licencia previa más adelante en este tema.



Las aplicaciones que se usan para crear contenido deben estar habilitadas para RMS a fin de aplicar protección permanente al contenido con AD RMS. Las aplicaciones de Microsoft Office, como Word, Excel, PowerPoint y Outlook están habilitadas para RMS y se pueden usar para crear y consumir contenido protegido.

IRM le ayuda a hacer lo siguiente:

  - Impedir que un destinatario autorizado para contenido protegido con IRM reenvíe, modifique, imprima, envíe por fax, guarde o corte y pegue el contenido.

  - Proteger los formatos de archivo adjunto compatibles con el mismo nivel de protección que el del mensaje.

  - Admitir expiración de mensajes y datos adjuntos protegidos con IRM para que no se puedan visualizar después de un período específico.

  - Impedir que se pueda copiar el contenido protegido con IRM por medio de Recortes de Windows de Microsoft.

Sin embargo, IRM no puede impedir que la información se copie mediante los métodos siguientes:

  - Programas de captura de pantalla de terceros

  - Uso de dispositivos de imágenes como cámaras para fotografiar el contenido protegido con IRM que se muestra en la pantalla

  - Usuarios que recuerdan o transcriben la información de forma manual

Para obtener más información sobre AD RMS, consulte [Active Directory Rights Management Services](https://go.microsoft.com/fwlink/p/?linkid=129823).

## Plantillas de directiva de derechos de AD RMS

AD RMS usa plantillas de directiva de derechos basadas en XrML para permitir que las aplicaciones habilitadas para IRM compatibles apliquen directivas de protección coherentes. En Windows Server 2008 o posterior, el servidor de AD RMS presenta un servicio web que se puede usar para enumerar y adquirir plantillas. Exchange 2013 incluye la plantilla No reenviar. Cuando se aplica la plantilla No reenviar a un mensaje, solo los destinatarios del mensaje pueden descifrarlo. Los destinatarios no pueden reenviar el mensaje, copiar el contenido del mensaje ni imprimirlo. Puede crear plantillas RMS adicionales en el servidor de AD RMS de la organización a fin de cumplir con los requisitos de protección de IRM.

La protección de IRM se establece al aplicar una plantilla de directiva de derechos de AD RMS. Con las plantillas de directivas, puede controlar los permisos que los destinatarios tienen con respecto a un mensaje. Es posible controlar acciones como responder, responder a todos, reenviar, extraer información de un mensaje, o guardar o imprimir un mensaje si se aplica la plantilla de directiva de derechos adecuada al mensaje.

Para obtener más información sobre las plantillas de directiva de derechos, consulte [Consideraciones sobre las plantillas de directiva de AD RMS](https://go.microsoft.com/fwlink/p/?linkid=179455).

Para obtener más información sobre cómo crear plantillas de directiva de derechos de AD RMS, consulte [Guía paso a paso para la creación e implementación de plantillas de directiva de permisos de Active Directory Rights Management Services](https://go.microsoft.com/fwlink/p/?linkid=136593).

¿Qué es la fuga de información?

## Aplicar la protección de IRM a mensajes

En Exchange 2010, se puede aplicar la protección IRM a los mensajes usando los siguientes métodos:

  - **De forma manual por parte de los usuarios de Outlook**   Los usuarios de Outlook pueden proteger los mensajes con IRM mediante las plantillas de directiva de derechos de AD RMS que tienen a su disposición. Este proceso usa la funcionalidad de IRM de Outlook, no de Exchange. En cambio, puede usar Exchange para obtener acceso a los mensajes y puede tomar acciones (como aplicar reglas de transporte) para cumplir con la directiva de mensajería de la organización. Para obtener más información sobre el uso de IRM en Outlook, consulte [Introducción a IRM para los mensajes de correo electrónico](https://go.microsoft.com/fwlink/p/?linkid=166897).

  - **De forma manual por parte de los usuarios de Outlook Web App**   Cuando IRM está habilitado en Outlook Web App, los usuarios pueden proteger los mensajes que envían con IRM y ver los mensajes protegidos con IRM que reciben. En Exchange 2013 con la actualización acumulativa 1 (CU1), los usuarios de Outlook Web App también puede ver los datos adjuntos protegidos con IRM mediante la Presentación de documentos WebReady. Para obtener más información acerca de IRM en Outlook Web App, vea [Information Rights Management en Outlook Web App](information-rights-management-in-outlook-web-app-exchange-2013-help.md).

  - **Manualmente con los usuarios de dispositivos con Windows Mobile y Exchange ActiveSync**   En la versión RTM de Exchange 2010, los usuarios de dispositivos con Windows Mobile pueden ver y crear mensajes protegidos con IRM. Esto requiere que los usuarios conecten sus dispositivos móviles compatibles con Windows Mobile a un equipo y activarlos para IRM. En Exchange 2010 SP1, puede habilitar IRM en Exchange ActiveSync de Microsoft para permitir a los usuarios de los dispositivos Exchange ActiveSync (inclusive los dispositivos móviles Windows) para ver, responder, reenviar y crear mensajes protegidos con IRM. Para obtener más información acerca de IRM en Exchange ActiveSync, vea [Information Rights Management en Exchange ActiveSync](information-rights-management-in-exchange-activesync-exchange-2013-help.md).

  - **De forma automática en Outlook 2010 o posterior**   Puede crear reglas de protección de Outlook para aplicar la protección de IRM automática a los mensajes en Outlook 2010 o posterior. Las reglas de protección de Outlook se implementan de forma automática en los clientes de Outlook 2010 y Outlook 2010 aplica la protección de IRM cuando el usuario redacta un mensaje. Para obtener más información acerca de las reglas de protección de Outlook, vea [Reglas de protección de Outlook](outlook-protection-rules-exchange-2013-help.md).

  - **De forma automática en los servidores de buzones de correo**   Puede crear reglas de protección de transporte que apliquen de forma automática la protección de IRM a los mensajes en los servidores de buzones de correo de Exchange 2013. Para obtener más información acerca de las reglas de protección de transporte, vea [Reglas de protección de transporte](transport-protection-rules-exchange-2013-help.md).
    

    > [!NOTE]
    > La protección de IRM no se aplica nuevamente a los mensajes que ya están protegidos con IRM. Por ejemplo, si un usuario protege un mensaje con IRM en Outlook o Outlook Web App, la protección IRM no se aplica al mensaje mediante la regla de protección de transporte.



¿Qué es la fuga de información?

## Escenarios para la protección de IRM

Los escenarios para la protección IRM se describen en la siguiente tabla.

### Escenarios para la protección de IRM

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Cómo enviar mensajes protegidos con IRM</th>
<th>Se admite</th>
<th>Requisitos</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Dentro de la misma implementación local de Exchange 2013</p></td>
<td><p>Sí</p></td>
<td><p>Para conocer los requerimientos, vea Requisitos de IRM más adelante en este tema.</p></td>
</tr>
<tr class="even">
<td><p>Entre los diferentes bosques en una implementación local</p></td>
<td><p>Sí</p></td>
<td><p>Para conocer los requerimientos, consulte <a href="https://go.microsoft.com/fwlink/p/?linkid=199009">Cómo configurar AD RMS para integrarlo con Exchange Server 2010 en varios bosques</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Entre la implementación local de Exchange 2013 y una organización basada en nube de Exchange</p></td>
<td><p>Sí</p></td>
<td><ul>
<li><p>Use un servidor AD RMS local.</p></li>
<li><p>Exporte el dominio de publicación de confianza desde su servidor AD RMS local.</p></li>
<li><p>Importe el dominio de publicación de confianza en su organización basada en nube.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Para remitentes externos</p></td>
<td><p>No</p></td>
<td><p>Exchange 2010 no incluye una solución para enviar mensajes protegidos con IRM a los remitentes externos en una organización no federada. AD RMS ofrece soluciones mediante el uso de directivas de confianza. Puede configurar una directiva de confianza entre un clúster de AD RMS y una cuenta de Microsoft (antes conocida como Windows Live ID). Para los mensajes enviados entre dos organizaciones, puede crear una confianza federada entre dos bosques de Active Directory mediante Active Directory Federation Services (AD FS). Para obtener más información, consulte <a href="https://go.microsoft.com/fwlink/p/?linkid=182909">Descripción de las directivas de confianza de AD RMS</a>.</p></td>
</tr>
</tbody>
</table>


¿Qué es la fuga de información?

## Descifrar mensajes protegidos con IRM para exigir el cumplimiento de directivas de mensajería

Es necesario que pueda obtener acceso al contenido cifrado del mensaje a fin de exigir el cumplimiento de directivas de mensajería y para el cumplimiento de las reglamentaciones. A fin de cumplir con los requisitos de detección debido a litigios, auditorías reglamentarias o investigaciones internas, es necesario que pueda buscar mensajes cifrados. Para ayudar con estas tareas, Exchange 2013 incluye las siguientes características de IRM:

  - **Descifrado de transporte**   Los agentes de transporte como el agente de reglas de transporte, deben tener acceso al contenido del mensaje a fin de aplicar las directivas de mensajería. El descifrado de transporte permite que los agentes de transporte instalados en los servidores de Exchange 2013 tengan acceso al contenido del mensaje. Para obtener más información, vea [Descifrado de transporte](transport-decryption-exchange-2013-help.md).

  - **Descifrado de informe de diario**   Las organizaciones pueden usar Registro en diario para conservar el contenido del mensaje a fin de cumplir con requisitos de cumplimiento o de negocios. El agente de registro en diario crea un informe de diario para los mensajes enviados al registro en el diario e incluye metadatos acerca del mensaje en el informe. El mensaje original se adjunta al informe de diario. Si el mensaje de un informe de diario está protegido con IRM, el descifrado del informe de diario adjunta una copia del texto del mensaje sin cifrar en el informe de diario. Para obtener más información, vea [Descifrado de informe de diarios](journal-report-decryption-exchange-2013-help.md).

  - **Descifrado IRM para Exchange Search**   ExchangeSearch puede indizar el contenido de mensajes protegidos con IRM con el descifrado IRM para Exchange Search. Cuando un administrador de detección realiza una búsqueda de exhibición de documentos electrónicos en contexto, los mensajes protegidos con IRM que se indizaron se devuelven en los resultados de la búsqueda. Para obtener más información, vea [Exhibición de documentos electrónicos en contexto](in-place-ediscovery-exchange-2013-help.md).
    

    > [!NOTE]
    > En Exchange 2010 SP1 o posterior, los miembros del grupo de roles de administración de detección pueden obtener acceso a mensajes protegidos mediante IRM obtenidos gracias a una búsqueda de detección y que residen en un buzón de correo de detección. Para habilitar esta funcionalidad, use el parámetro <EM>EDiscoverySuperUserEnabled</EM> con el cmdlet <A href="https://technet.microsoft.com/es-es/library/dd979792(v=exchg.150)">Set-IRMConfiguration</A>. Para obtener más información, vea <A href="configure-irm-for-exchange-search-and-in-place-ediscovery-exchange-2013-help.md">Configurar IRM para la búsqueda y la exhibición de documentos electrónicos local de Exchange</A>.



Para habilitar estas características de descifrado, los servidores de Exchange deben tener acceso al mensaje. Esto se logra al agregar el buzón de correo de federación, un buzón del sistema creado por el programa de instalación de Exchange, al grupo de superusuarios del servidor de AD RMS. Para obtener detalles, vea [Agregar el buzón de la federación para el grupo de usuarios de AD RMS Super](add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md).

¿Qué es la fuga de información?

## Licencia previa

Para ver los mensajes y los datos adjuntos protegidos con IRM, Exchange 2013 adjunta una licencia previa automática a los mensajes protegidos. Esto evita que el cliente deba realizar varios recorridos al servidor de AD RMS para recuperar una licencia de uso y habilita, además, la visualización sin conexión de los mensajes y los datos adjuntos protegidos con IRM. La licencia previa también permite que los mensajes protegidos por IRM se visualicen en Outlook Web App. La licencia previa se habilita de forma predeterminada al habilitar las características de IRM.

¿Qué es la fuga de información?

## Agentes de IRM

En Exchange 2013, la función de IRM se habilita mediante los agentes de transporte en el servicio de transporte de los servidores de buzones de correo. El programa de instalación de Exchange instala los agentes de IRM en un servidor de buzones de correo. No se puede controlar a los agentes IRM mediante las tareas de administración para los agentes de transporte.


> [!NOTE]
> En Exchange&nbsp;2013, los agentes de IRM son agentes integrados. Los agentes integrados no están incluidos en la lista de agentes que devuelve el cmdlet <STRONG>Get-TransportAgent</STRONG>. Para obtener más información, vea <A href="transport-agents-exchange-2013-help.md">Agentes de transporte</A>.



En la tabla siguiente se enumeran a los agentes de IRM implementados en el servicio de transporte en servidores de buzones de correo.

### Agentes IRM en el servicio de transporte en servidores de buzones de correo

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Agente</th>
<th>Evento</th>
<th>Función</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Agente de descifrado de RMS</p></td>
<td><p>OnEndOfData (SMTP) y OnSubmittedMessage</p></td>
<td><p>Descifra los mensajes para permitir el acceso a los agentes de transporte.</p></td>
</tr>
<tr class="even">
<td><p>Agente de reglas de transporte</p></td>
<td><p>OnRoutedMessage</p></td>
<td><p>Marca los mensajes que coinciden con las condiciones de la regla de protección de transporte para que el agente de cifrado de RMS aplique la protección de IRM.</p></td>
</tr>
<tr class="odd">
<td><p>Agente de cifrado de RMS</p></td>
<td><p>OnRoutedMessage</p></td>
<td><p>Aplica la protección IRM a los mensajes que marcó el agente de reglas de transporte y vuelve a cifrar los mensajes descifrados de transporte.</p></td>
</tr>
<tr class="even">
<td><p>Agente de licencias previas</p></td>
<td><p>OnRoutedMessage</p></td>
<td><p>Adjunta una licencia previa a los mensajes protegidos con IRM.</p></td>
</tr>
<tr class="odd">
<td><p>Agente de descifrado de informes de diario</p></td>
<td><p>OnCategorizedMessage</p></td>
<td><p>Descifra los mensajes protegidos con IRM adjuntos a los informes de diario e inserta versiones de texto sin cifrar junto con los mensajes cifrados originales.</p></td>
</tr>
</tbody>
</table>


Para obtener más información acerca de los agentes de transporte, vea [Agentes de transporte](transport-agents-exchange-2013-help.md).

¿Qué es la fuga de información?

## Requisitos de IRM

Para implementar IRM en su organización de Exchange 2013, su implementación debe cumplir con los requisitos descritos en la siguiente tabla.

### Requisitos de IRM

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Servidor</th>
<th>Requisitos</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Clúster de AD RMS</p></td>
<td><ul>
<li><p><strong>Sistema operativo</strong>   Se requiere Windows Server 2012, Windows Server 2008 R2 o Windows Server 2008 SP2 con la revisión del <a href="http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=973247">rol de Active Directory Rights Management Services en Windows Server 2008</a>.</p></li>
<li><p><strong>Punto de conexión de servicio</strong>   Las aplicaciones compatibles con Exchange 2010 y AD RMS usan el punto de conexión de servicio registrado en Active Directory para detectar el clúster de AD RMS y las direcciones URL. AD RMS permite registrar el punto de conexión de servicio desde el programa de instalación de AD RMS. Si la cuenta que se usa para configurar AD RMS no es miembro del grupo de seguridad Administradores de empresas, se puede realizar el registro de punto de conexión de servicio después de completar la instalación. Solamente hay disponible un punto de conexión de servicio para AD RMS en un bosque de Active Directory.</p></li>
<li><p><strong>Permisos</strong>   Los permisos para leer y ejecutar del canal de certificación del servidor AD RMS (archivo <code>ServerCertification.asmx</code> en los servidores AD RMS) se deben asignar a lo siguiente:</p>
<ul>
<li><p>Grupos de servidores Exchange o servidores individuales Exchange</p></li>
<li><p>Grupo de servicio AD RMS en los servidores AD RMS</p></li>
</ul>
<p>De manera predeterminada, el archivo ServerCertification.asmx está ubicado en la carpeta <code>\inetpub\wwwroot\_wmcs\certification\</code> en los servidores AD RMS. Para obtener más detalles, consulte <a href="https://go.microsoft.com/fwlink/p/?linkid=186951">Establecer permisos en la canalización de certificación del servidor de AD RMS</a>.</p></li>
<li><p><strong>Superusuarios de AD RMS</strong>   Para habilitar el descifrado de transporte, el descifrado de informe de diarios, IRM en Outlook Web App e IRM para Exchange Search, debe agregar el buzón de correo de la federación, un buzón del sistema creado por el programa de instalación de Exchange 2013, al grupo de superusuarios en el clúster de AD RMS. Para obtener información más detallada, vea <a href="add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md">Agregar el buzón de la federación para el grupo de usuarios de AD RMS Super</a>.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Exchange</p></td>
<td><ul>
<li><p>Se requiere Exchange 2010 o posterior.</p></li>
<li><p>La revisión <a href="http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=973136">FIX: mensaje de error de excepción ArgumentNullException si una aplicación basada en .NET Framework 2.0 SP2 intenta procesar una respuesta con contenido de longitud cero para una solicitud de servicio Web ASP.NET asincrónico: Se recomienda &quot;El valor no puede ser nulo&quot;</a> para Microsoft .NET Framework 2.0 SP2.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Outlook</p></td>
<td><ul>
<li><p>Los usuarios pueden proteger con IRM los mensajes en Outlook. Al comenzar con Outlook 2003, son compatibles las plantillas AD RMS para los mensajes de protección con IRM.</p></li>
<li><p>Las reglas de protección de Outlook son una característica de Exchange 2010 y Outlook 2010. Las versiones anteriores de Outlook no admiten esta característica.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Exchange ActiveSync</p></td>
<td><ul>
<li><p>Los dispositivos compatibles con el protocolo de Exchange ActiveSync versión 14.1, incluidos los dispositivos con Windows Mobile, pueden admitir IRM en Exchange ActiveSync. La aplicación de correo electrónico móvil en un dispositivo debe ser compatible con la etiqueta <strong>RightsManagementInformation</strong> definida en el protocolo Exchange ActiveSync versión 14.1. En Exchange 2013, IRM en Exchange ActiveSync permite a los usuarios con dispositivos compatibles ver, responder, reenviar y crear mensajes protegidos con IRM sin que sea necesario que el usuario conecte el dispositivo a un equipo y lo active para IRM. Para obtener información más detallada, vea <a href="information-rights-management-in-exchange-activesync-exchange-2013-help.md">Information Rights Management en Exchange ActiveSync</a>.</p></li>
</ul></td>
</tr>
</tbody>
</table>



> [!NOTE]
> El término <EM>clúster deAD RMS</EM> es el que se usa para la implementación de AD RMS en la organización, incluso para la implementación en un solo servidor. AD RMS es un servicio web. No necesita la configuración de un clúster de conmutación por error de Windows Server. Para lograr máxima disponibilidad y equilibrio de carga, puede implementar varios servidores de AD RMS en el clúster y usar equilibrio de carga de red.




> [!IMPORTANT]
> En un entorno de producción, no se admite la instalación de AD RMS y de Exchange en el mismo servidor.



Las características de IRM de Exchange 2013 son compatibles con los formatos de archivo de Microsoft Office. Puede ampliar la protección IRM a otros formatos de archivo mediante la implementación de protectores personalizados. Para obtener más información sobre los protectores personalizados, consulte Protección de información y asociados de control en [Proveedores de software independientes](https://go.microsoft.com/fwlink/p/?linkid=210336).

¿Qué es la fuga de información?

## Configuración y prueba de IRM

Para configurar las características de IRM en Exchange 2013 debe usar el Shell de administración de Exchange. Para configurar las características de IRM, use el cmdlet [Set-IRMConfiguration](https://technet.microsoft.com/es-es/library/dd979792\(v=exchg.150\)). Puede habilitar o deshabilitar IRM para los mensajes internos, el descifrado de transporte, el descifrado de informes de diario, Exchange Search y Outlook Web App. Para obtener más información acerca de la configuración de las características de IRM, vea [Procedimientos de Information Rights Management](information-rights-management-procedures-exchange-2013-help.md).

Después de configurar el servidor de Exchange 2013, puede usar el cmdlet [Test-IRMConfiguration](https://technet.microsoft.com/es-es/library/dd979798\(v=exchg.150\)) para realizar pruebas de un extremo a otro de la implementación de IRM. Estas pruebas resultan útiles para comprobar la funcionalidad de IRM de inmediato después de la configuración inicial de IRM y de forma continuada. El cmdlet realiza las siguientes pruebas:

  - Inspecciona la configuración de IRM para la organización de Exchange 2013.

  - Comprueba el servidor de AD RMS para obtener información sobre la versión y la revisión.

  - Comprueba si RMS puede activar un servidor de Exchange al recuperar un certificado de cuenta de derechos (RAC) y un certificado de emisor de licencias de cliente.

  - Obtiene plantillas de directiva de derechos de AD RMS desde el servidor de AD RMS.

  - Comprueba si el remitente especificado puede enviar mensajes protegidos con IRM.

  - Recupera una licencia de uso de superusuario para el destinatario especificado.

  - Obtiene una licencia previa para el destinatario especificado.

¿Qué es la fuga de información?

## Extender Rights Management con el conector Rights Management

El conector Microsoft Rights Management (conector RMS) es una aplicación opcional que mejora la protección de datos del servidor de Exchange 2013 mediante servicios de Microsoft Rights Management en la nube. Una vez instalado, el conector RMS proporciona protección de datos continua mientras dure la información y, como estos servicios son personalizables, puede definir el nivel de protección que necesita. Por ejemplo, puede limitar el acceso a los mensajes de correo electrónico a determinados usuarios o establecer permisos de solo vista en ciertos mensajes.

Para obtener más información sobre el conector RMS y sobre cómo instalarlo, consulte [Conector Rights Management](https://technet.microsoft.com/es-es/library/dn375964.aspx).

