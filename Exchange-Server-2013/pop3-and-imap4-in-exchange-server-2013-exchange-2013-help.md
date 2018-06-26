---
title: 'POP3 e IMAP4 en Exchange Server 2013: Exchange 2013 Help'
TOCTitle: POP3 e IMAP4
ms:assetid: a7dc91ee-2919-4db3-ae9c-cd665d2e09ea
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ657728(v=EXCHG.150)
ms:contentKeyID: 49895820
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# POP3 e IMAP4 en Exchange Server 2013

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2016-08-16_

Obtenga información sobre las diferencias entre los protocolos POP3 e IMAP4 en Exchange Server 2013 y cómo configurar las opciones de acceso a buzones de Exchange 2013 desde distintos programas de correo.

De forma predeterminada, POP3 e IMAP4 están deshabilitados en Exchange Server 2013. Para admitir clientes POP3 que siguen dependiendo de estos protocolos, debe iniciar dos servicios POP3: el servicio POP3 de Microsoft Exchange y el servicio back-end POP3 de Microsoft Exchange. Para admitir clientes IMAP4 que siguen dependiendo de estos protocolos, necesita iniciar dos servicios IMAP4: el servicio IMAP4 de Microsoft Exchange y el servicio back-end IMAP4 de Microsoft Exchange.

Para obtener los pasos detallados sobre cómo habilitar los servicios POP3 y IMAP4, consulte [Habilitar POP3 en Exchange 2013](enable-pop3-in-exchange-2013-exchange-2013-help.md) y [Habilitar IMAP4 en Exchange 2016](enable-imap4-in-exchange-2013-exchange-2013-help.md).

De forma predeterminada, los usuarios que tienen buzones en equipos que ejecutan Exchange 2013 pueden obtener acceso a sus buzones mediante Outlook o Outlook Web App, Exchange ActiveSync o Outlook Voice Access. Outlook, Outlook Web App y Outlook Voice Access permiten que los usuarios de correo electrónico usen el completo conjunto de características que están a disposición de los usuarios que tienen buzones en servidores de Exchange 2016.

**Contenido**

Información general sobre la funcionalidad de POP3 e IMAP4

Conectividad entre sitios de POP3 e IMAP4

Uso de cuentas no estándar con POP3 e IMAP4

Descripción de las diferencias entre POP3 e IMAP4

Enviar y recibir opciones para aplicaciones de correo electrónico POP3 e IMAP4

Aplicaciones POP3 e IMAP4

Configuración del usuario para configurar el acceso POP3 o IMAP4 a los buzones de Exchange 2013

## Información general sobre la funcionalidad de POP3 e IMAP4

En esta sección se describe la funcionalidad de POP3 e IMAP4 en Exchange 2013.

Los protocolos POP3 e IMAP4 presentan las siguientes ventajas y limitaciones:

  - **POP3**   POP3 se diseñó para permitir el procesamiento de correo electrónico sin conexión. Con POP3, los mensajes de correo electrónico se quitan del servidor y se almacenan en el cliente POP3 local, salvo en el caso de que el cliente se haya configurado para mantener el correo en el servidor. Esto sitúa la responsabilidad de la seguridad y administración de datos en manos del usuario. POP3 no ofrece características avanzadas de colaboración como calendarios, contactos y tareas.

  - **IMAP4**   IMAP4 ofrece acceso en línea y sin conexión pero, al igual que POP3, IMAP4 no ofrece características de colaboración avanzadas, como calendarios, contactos y tareas.

Las aplicaciones de correo de POP3 e IMAP4 no usan POP3 e IMAP4 para enviar mensajes al servidor de correo, sino que emplean el protocolo SMTP para enviar los mensajes. El conector que recibe los envíos de correo de las aplicaciones cliente que usan POP3 o IMAP4 se crea automáticamente con la instalación de Exchange. Para más información sobre los conectores, consulte [Conectores de recepción](receive-connectors-exchange-2013-help.md).


> [!NOTE]
> Cada vez que un usuario usa un programa de correo electrónico basado en POP o IMAP para abrir su correo electrónico de Office 365, es posible que experimente un retraso de varios segundos. El retraso se debe al uso de un servidor proxy, que introduce un salto adicional para la autenticación. El servidor proxy busca primero el servidor pod asignado (servidor de acceso de cliente) y, después, realiza la autenticación con él.



## Conectividad entre sitios de POP3 e IMAP4

En versiones anteriores de Exchange, había que realizar un paso de configuración manual para que los clientes de POP3 e IMAP4 pudieran conectarse a su correo desde un sitio de la organización que no era donde se ubicaba su buzón de correo. De manera predeterminada, Exchange 2013 usa automáticamente un proxy desde un servidor de acceso de cliente de un sitio para tener acceso al servidor correcto.

## Uso de cuentas no estándar con POP3 e IMAP4

La cuenta Anónima y la cuenta Invitado no se pueden usar para iniciar sesión en un buzón de Exchange 2016 a través de POP3 o IMAP4. Las cuentas anónimas se bloquean porque, al usar cuentas no estándar para el acceso a POP3 e IMAP4, se vulnera la seguridad. Además, no es posible conectarse al buzón Administrador a través de POP3 o IMAP4. Esta limitación de Exchange 2013 se introdujo de forma deliberada para incrementar la seguridad del buzón Administrador. Para tener acceso al buzón del administrador, debe usar Outlook o Outlook Web App.

## Descripción de las diferencias entre POP3 e IMAP4

**POP3** POP3 es un protocolo de Internet para correo electrónico que se usa con mucha frecuencia. De forma predeterminada, cuando las aplicaciones de correo electrónico POP3 descargan mensajes de correo electrónico en un equipo cliente, los mensajes descargados se quitan del servidor. Si no se conserva una copia del correo electrónico del usuario en el servidor de correo electrónico, el usuario no podrá obtener acceso a los mismos mensajes de correo electrónico desde varios equipos. Pero algunas aplicaciones de correo electrónico POP3 se pueden configurar para que conserven copias de los mensajes en el servidor de manera que se pueda obtener acceso a los mismos mensajes desde otro equipo. Las aplicaciones cliente POP3 solo se pueden usar para descargar mensajes del servidor de correo electrónico en una única carpeta (generalmente en la Bandeja de entrada) del equipo cliente. El protocolo POP3 no puede sincronizar varias carpetas del servidor de correo electrónico con varias carpetas del equipo cliente.

**IMAP4** Las aplicaciones cliente de correo electrónico que usan IMAP4 son más flexibles y generalmente ofrecen más características que las que usan POP3. De forma predeterminada, cuando las aplicaciones de correo electrónico IMAP4 descargan mensajes en un equipo cliente, una copia de los mensajes descargados permanece en el servidor de correo electrónico. De este modo, el usuario puede obtener acceso al mismo mensaje desde varios equipos. Con el correo electrónico IMAP4, el usuario puede obtener acceso y crear varias carpetas de correo electrónico en el servidor de correo electrónico. Después, los usuarios pueden obtener acceso a cualquiera de sus mensajes del servidor desde equipos situados en distintas ubicaciones. Por ejemplo, la mayoría de las aplicaciones IMAP4 se pueden configurar para que conserven en el servidor una copia de los elementos enviados por el usuario, de tal modo que éste pueda ver los elementos enviados desde cualquier otro equipo. IMAP4 admite características adicionales que son compatibles con la mayoría de las aplicaciones IMAP4. Por ejemplo, algunas aplicaciones IMAP4 incluyen una característica que permite al usuario ver solo los encabezados de los mensajes de correo electrónico del servidor (quién ha enviado el mensaje y el asunto) y descargar solo aquellos mensajes que desee leer. IMAP4 tampoco es compatible con el acceso a carpetas públicas.


> [!NOTE]
> Los clientes IMAP4 y POP3 tienen acceso limitado a la información de calendario para Exchange. Para obtener más información, consulte <A href="configure-calendar-options-for-pop3-exchange-2013-help.md">Configurar las opciones de calendario para POP3</A> y <A href="configure-calendar-options-for-imap4-exchange-2013-help.md">Configurar opciones de calendario para IMAP4</A>.



## Enviar y recibir opciones para aplicaciones de correo electrónico POP3 e IMAP4

Las aplicaciones de correo electrónico POP3 e IMAP4 permiten a los usuarios elegir cuándo desean conectarse al servidor para enviar y recibir correo electrónico. En esta sección se analizan algunas de las opciones de conectividad más frecuentes y se indican algunos factores que el usuario debe tener en cuenta al seleccionar opciones de conexión disponibles en las aplicaciones de correo electrónico POP3 e IMAP4.

## Opciones de configuración habituales

Tres de las opciones de conexión más comunes que se pueden configurar en la aplicación cliente POP3 o IMAP4 son:

  - Enviar y recibir mensajes cada vez que se inicia la aplicación de correo. Si se usa esta opción, solo se envía y se recibe correo cuando el usuario inicia la aplicación de correo.

  - Enviar y recibir mensajes de forma manual. Si se usa esta opción, solo se envían y se reciben mensajes cuando el usuario hace clic en una opción "enviar y recibir" de la interfaz de usuario del cliente.

  - Enviar y recibir mensajes después de un número de minutos definido. Cuando el usuario configura esta opción, la aplicación cliente se conecta al servidor después de un número de minutos definido para enviar y descargar nuevos mensajes.

Para obtener información acerca de cómo configurar estas opciones para la aplicación de correo electrónico que esté usando, consulte la documentación de ayuda que viene con la aplicación de correo electrónico.

## Consideraciones sobre la configuración de opciones de envío y recepción

Si el dispositivo o el equipo que ejecuta la aplicación de correo POP3 o IMAP4 está siempre conectado a Internet, es posible que los usuarios quieran configurar la aplicación de correo para que envíe y reciba mensajes después de un número de minutos establecido. La conexión al servidor a intervalos frecuentes permite al usuario mantener actualizada la aplicación de correo con la información más reciente del servidor. Pero si el dispositivo o el equipo que ejecuta la aplicación de correo POP3 o IMAP4 no está siempre conectado a Internet, es posible que el usuario prefiera configurar la aplicación de correo para que envíe y reciba los mensajes manualmente.


> [!NOTE]
> Si el usuario usa una aplicación de correo electrónico compatible con IMAP4 que admite el comando IMAP4 IDLE, podrá enviar y recibir correo electrónico desde su buzón de correo de Exchange casi en tiempo real. Para que este método de conexión funcione, tanto la aplicación de servidor de correo electrónico como la aplicación cliente deben admitir el comando IMAP4 IDLE. En la mayoría de los casos, los usuarios no necesitan configurar ninguna opción de la aplicación IMAP4 para usar este método de conexión.



## Aplicaciones POP3 e IMAP4

Como Exchange 2013 admite POP3 e IMAP4, los usuarios pueden usar cualquier aplicación que admita aplicaciones cliente POP3 e IMAP4 para conectarse a Exchange 2013. Entre estas aplicaciones, se incluyen Outlook, Outlook Web App, Windows Live Mail, Outlook Express, Entourage y muchas aplicaciones de otros fabricantes, como Gmail, Mozilla Thunderbird y Eudora. Las características admitidas son diferentes en cada aplicación cliente de correo electrónico. Para obtener información acerca de las características específicas de cada aplicación cliente POP3 e IMAP4, consulte la documentación que se suministra con cada aplicación.

## Configuración del usuario para configurar el acceso POP3 o IMAP4 a los buzones de Exchange 2013

Después de habilitar el acceso de clientes POP3 e IMAP4, deberá proporcionar a los usuarios la información que necesitan para conectar los programas de correo al buzón de Exchange 2016.

Para conectar una red corporativa desde adentro, los usuarios necesitan la siguiente información:

  - Nombre del servidor POP3 o IMAP4 interno

  - Número del puerto POP3 o IMAP4 interno

  - Método de cifrado de POP3 o IMAP4 interno

  - Nombre del (servidor de salida) SMPT interno

  - Número del puerto SMTP (servidor de salida) interno

  - Método de cifrado del (servidor de salida) SMPT interno

Para conectar desde Internet, se necesita la siguiente información:

  - Nombre del servidor POP3 o IMAP4 externo

  - Número del puerto POP3 o IMAP4 externo

  - Método de cifrado de POP3 o IMAP4 externo

  - Nombre del (servidor de salida) SMPT externo

  - Número del puerto SMTP (servidor de salida) externo

  - Método de cifrado del (servidor de salida) SMPT externo

Esta configuración puede estar disponible para los usuarios mediante el correo electrónico u otros métodos de comunicación manual. Puede configurar Exchange para que los usuarios puedan usar Outlook Web App y buscar su propia configuración.

**Configurar Exchange para que los usuarios puedan buscar su configuración del servidor POP3, IMAP4 y SMTP**

De forma predeterminada, los usuarios no pueden buscar la configuración del servidor POP3, IMAP4 y SMTP usando Outlook Web App. Para permitir que los usuarios puedan buscarla, debe usar los cmdlets **Set-PopSettings** y **Set-ImapSettings**. Para permitir que los usuarios busquen la configuración del servidor SMTP (de salida), debe usar el cmdlet **Set-ReceiveConnector**.

Siga estos paso para permitir que los usuarios busquen su propia configuración de POP3, IMAP4 y SMTP:

  - **Configuración de POP3**   Ejecute el cmdlet **Set-POPSettings** con el parámetro *ExternalConnectionSettings*. Use el formato `Set-POPSettings -ExternalConnectionSetting {<FQDN>:995:SSL}`. Por ejemplo, ejecute `Set-PopSettings -ExternalConnectionSetting {Dublin01.Contoso.com:995:SSL}` si quiere que los clientes que se conectan por medio del servidor con FQDN Dublin01.Contoso.com puedan buscar su propia configuración de POP.
    
    Debe reiniciar IIS después de aplicar esta configuración.

  - **Configuración de IMAP4**   Ejecute el cmdlet **Set-IMAPSettings** con el parámetro *ExternalConnectionSettings*. Use el formato `Set-ImapSettings -ExternalConnectionSetting {<FQDN>:993:SSL}`. Por ejemplo, ejecute `Set-IMAPSettings -ExternalConnectionSetting {Dublin01.Contoso.com:993:SSL}` si quiere que los clientes que se conectan por medio del servidor con FQDN Dublin01.Contoso.com puedan buscar su propia configuración de IMAP.
    
    Debe reiniciar IIS después de aplicar esta configuración.

  - **Configuración de SMTP**   Ejecute el cmdlet **Set-ReceiveConnector** con el parámetro *AdvertiseClientSettings*. Use el formato `Set-ReceiveConnector "Client Frontend <Server Name>" -AdvertiseClientSettings $True -FQDN <FQDN>`. Por ejemplo, ejecute `Set-ReceiveConnector "Client Frontend <Server Name>" -AdvertiseClientSettings $True -FQDN Dublin01.Contoso.com` si quiere que los clientes que se conectan por medio del servidor con FQDN Dublin01.Contoso.com puedan buscar su propia configuración SMTP.
    
    Debe reiniciar IIS después de aplicar esta configuración.

Después de cambiar la configuración predeterminada al ejecutar los cmdlets **Set-POPSettings**, **Set-IMAPSettings** y **Set-ReceiveConnector**, los usuarios pueden buscar las configuraciones del servidor POP, IMAP y SMTP externos en Outlook Web App al hacer clic en **Configuración** \> **Opciones** \> **Cuenta** \> **Mi cuenta** \> **Configuración para el acceso POP o IMAP**.

**Dejar una copia de los mensajes en el servidor**

La configuración predeterminada de algunos programas de correo electrónico consiste en eliminar los mensajes en el servidor una vez que se recuperan. Asegúrese de recomendar a los usuarios que configuren el programa de correo para que guarde una copia de todos los mensajes que el cliente recupera en el servidor. De este modo, los usuarios pueden tener acceso a los mensajes desde otro programa de correo.

