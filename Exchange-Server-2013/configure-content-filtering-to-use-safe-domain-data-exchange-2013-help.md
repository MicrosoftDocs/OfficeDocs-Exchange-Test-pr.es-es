---
title: 'Configurar filtrado contenido para usar dato dominio seguro Exchange 2013 Help | Microsoft Docs'
TOCTitle: Configurar el filtrado de contenido para usar datos de dominio seguro
ms:assetid: 1ee2b663-b4f3-4fef-8954-986f2d820924
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn467930(v=EXCHG.150)
ms:contentKeyID: 59637132
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar el filtrado de contenido para usar datos de dominio seguro

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2014-12-16_

Los datos de dominio seguro son un dominio completo (por ejemplo, @contoso.com) que se almacena en la lista de remitentes seguros de un usuario. De manera predeterminada, el agente de filtrado de contenido no usa datos de dominio seguro para identificar a los remitentes que tienen permiso para eludir el filtrado de contenido.

Este valor predeterminado ayuda a reducir la cantidad de correo no deseado que se entrega en su organización. Por ejemplo, un usuario podría agregar el dominio de un proveedor de correo electrónico a su lista de remitentes seguros. Si los spammers usan o suplantan la identidad de este dominio con frecuencia, y si el filtrado de contenido está configurado para usar datos de dominio seguro y marcar los mensajes como seguros, los mensajes de cualquier remitente en dicho dominio se entregarán a los destinatarios de la organización.

Le recomendamos que no modifique el valor predeterminado en la mayoría de los casos. Sin embargo, puede configurar los datos de dominio seguro de los usuarios para que se almacenen en Active Directory y se usen en el filtrado de contenido para marcar los mensajes como seguros. Para ello, debe modificar el archivo de configuración de aplicación XML MSExchangeMailboxAssistants.exe.config que está asociado con el servicio Asistentes de buzón de Microsoft Exchange, como se detalla más adelante en este tema. Al realizar este cambio de configuración, a los datos de dominio seguro se les aplica un algoritmo hash y se almacenan en el atributo de objeto de usuario **msExchSafeSenderHash** de cada usuario en Active Directory como parte de la agregación de listas seguras. A continuación, el agente de filtrado de contenido puede usar los datos de dominio seguro para marcar los mensajes de los remitentes de esos dominios como seguros. Para obtener más información acerca de la agregación de listas seguras, vea [Agregación de lista segura](safelist-aggregation-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 10 minutos

  - Los permisos de Exchange no se aplican a los procedimientos de este tema. Estos procedimientos se realizan en el sistema operativo de Exchange Server.

  - Los cambios que guarda en el archivo MSExchangeMailboxAssistants.exe.config se aplican después de reiniciar el servicio Asistentes de buzón de Microsoft Exchange.

  - Las configuraciones personalizadas referentes al servidor que lleve a cabo en los archivos de configuración de la aplicación XML de Exchange, por ejemplo, los archivos web.config en los servidores de acceso de cliente o el archivo EdgeTransport.exe.config en los servidores de buzones de correo, se sobrescribirán al instalar la actualización acumulativa o el Service Pack de Exchange. Asegúrese de guardar esta información para que pueda volver a configurar fácilmente su servidor tras la instalación. Vuelva a establecer estas configuraciones después de instalar una actualización acumulativa de Exchange.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Usar un símbolo del sistema para configurar el filtrado de contenido para usar datos de dominio seguro

1.  En la ventana del símbolo del sistema, abra el archivo MSExchangeMailboxAssistants.exe.config en el Bloc de notas ejecutando el comando siguiente:
    
        Notepad %ExchangeInstallPath%Bin\MSExchangeMailboxAssistants.exe.config

2.  Busque la clave *\</appsettings\>* al final del archivo y copie la siguiente clave antes de la clave *\</appsettings\>*:
    
        <add key="IncludeSafeDomains" value="true" />

3.  Cuando haya terminado, guarde y cierre el archivo MSExchangeMailboxAssistants.exe.config.

4.  Reinicie el servicio Asistentes de buzón de Microsoft Exchange ejecutando el siguiente comando:
    
        net stop MSExchangeMailboxAssistants && net start MSExchangeMailboxAssistants

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que haya configurado correctamente el filtrado de contenido para usar datos de dominio seguro, siga estos pasos:

1.  Compruebe que al agregar un dominio a la lista de remitentes seguros de un usuario se actualiza el atributo **msExchSafeSenderHash** del usuario en Active Directory. Para ello, vea el atributo en ADSIEdit.exe o LDP.exe, abra el buzón del usuario en Outlook, agregue un dominio a la lista de remitentes seguros, ejecute el comando `Update-Safelist <username>` y compruebe que los valores originales y actuales de **msExchSafeSenderHash** sean diferentes.

2.  Una vez que haya comprobado que los datos de dominio seguro están almacenados en Active Directory, envíe un mensaje de prueba desde un remitente externo en ese dominio a un usuario en la organización. Compruebe que el mensaje está marcado como seguro examinando los campos de encabezado contra correo no deseado en el encabezado del mensaje.

