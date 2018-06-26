---
title: 'Notas de la versión de Exchange 2013: Exchange 2013 Help'
TOCTitle: Notas de la versión de Exchange 2013
ms:assetid: 1879fd5e-3d63-4264-9cc2-9c050c6ab3c5
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ150489(v=EXCHG.150)
ms:contentKeyID: 48267840
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Notas de la versión de Exchange 2013

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2018-04-16_

Bienvenido a Microsoft Exchange Server 2013. Este tema contiene información importante que debe conocer para implementar correctamente Exchange 2013. Lea todo este tema antes de comenzar con la implementación.

En este tema se presentan las siguientes secciones:

  - Instalación e implantación

  - Shell de administración de Exchange

  - Buzón

  - Carpetas públicas

  - Flujo de correo

  - Conectividad de clientes

  - Coexistencia de Exchange 2010

## Instalación e implantación

  - **msExchProductId no refleja la versión de Exchange 2013 que está instalada** Después de que Exchange extiende el esquema de Active Directory y prepara Active Directory para Exchange, se actualizan varias propiedades para mostrar que la preparación está completa. Una de estas propiedades es *msExchangeProductId* en el contenedor `CN=<your organization>, CN=Microsoft Exchange, CN=Services, CN=Configuration, DC=<domain>` en el contexto de nomenclatura `Configuration`. Si no se introducen cambios en el esquema de Active Directory en la versión de Exchange 2013 que se va a instalar, esta propiedad no se actualizará o podrá mostrar un valor inesperado. Esto podría provocar confusión si el valor no coincide con la versión de Exchange 2013 que se va a instalar.
    
    Se espera este comportamiento ya que el valor de *msExchProductId* no refleja la versión de Exchange 2013 que se va a instalar. Esta propiedad refleja la versión de Exchange 2013 que realizó cambios por última vez en el esquema de Active Directory. Para evitar confusiones, le recomendamos que siga los pasos de la sección [How do you know this worked?](prepare-active-directory-and-domains-exchange-2013-help.md) de [Preparar Active Directory y los dominios](prepare-active-directory-and-domains-exchange-2013-help.md) para comprobar que Active Directory se ha actualizado y está listo para la versión de Exchange 2013 que se va a instalar.

  - **La instalación solicita incorrectamente .NET Framework 4.0**   Si intenta instalar Exchange 2013 sin tener instalado .NET Framework en el equipo, la instalación solicitará de manera incorrecta que instale .NET Framework 4.0 cuando lo que en realidad se requiere es .NET Framework 4.5 o posterior.
    
    Para solucionar este problema, instale .NET Framework 4.5 o posterior. No es necesario instalar .NET Framework 4.0. Para obtener una lista completa de requisitos previos, consulte [Requisitos previos de Exchange 2013](exchange-2013-prerequisites-exchange-2013-help.md).

  - Los archivos de configuración de la aplicación XML de **Exchange se sobrescriben durante la instalación de una actualización acumulativa**   Las configuraciones personalizadas referentes al servidor que lleve a cabo en los archivos de configuración de la aplicación XML de Exchange XML, por ejemplo, los archivos web.config en los servidores de acceso de cliente o el archivo EdgeTransport.exe.config en los servidores de buzones de correo, se sobrescribirán al instalar la actualización acumulativa o el Service Pack de Exchange. Asegúrese de guardar esta información para que pueda volver a configurar fácilmente su servidor tras la instalación. Vuelva a establecer estas configuraciones después de instalar una actualización acumulativa o Service Pack de Exchange.

  - **La instalación de Exchange con permisos de administrador delegado producirá un error en el programa de instalación** Cuando un usuario que solamente es miembro del grupo de funciones Configuración delegada intente instalar Exchange en un servidor aprovisionado previamente, el programa de instalación producirá un error. Esto sucede porque el grupo de Configuración delegada carece de los permisos necesarios para crear y configurar ciertos objetos en Active Directory.
    
    Para solucionar este problema, siga uno de estos procedimientos:
    
      - Agregue el usuario que instala Exchange al grupo de seguridad Administradores de dominio de Active Directory.
    
      - Instale Exchange con un usuario que sea miembro del grupo de funciones de administración de la organización.

Para obtener más información acerca de cómo instalar Exchange 2013, consulte [Planificación e implementación](planning-and-deployment-for-exchange-2013-installation-instructions.md).

## Shell de administración de Exchange

  - **El Shell carga inesperadamente los cmdlets de Exchange 2007 o Exchange 2010** Antes, cuando se abría el Shell en un servidor de Exchange de 2013, el Shell abría una conexión con el servidor local o con otro servidor que ejecutase Exchange de 2013. Cuando se realizaba la conexión, se cargaban los cmdlets de Exchange 2013. A partir de Exchange 2013 CU11, el Shell se conectará al servidor de Exchange donde se encuentra el buzón del usuario conectado. Si el usuario conectado no tiene buzón, el Shell se conectará al servidor donde se encuentra el buzón de arbitraje SystemMailbox{bb558c35-97f1-4cb9-8ff7-d53741dc928c}. El servidor de destino puede ser cualquier versión compatible de Exchange. Esto significa que, si el buzón del usuario conectado (o el buzón de arbitraje si el usuario no tiene buzón) se encuentra en un servidor de Exchange 2010, el Shell se conectará a ese servidor y cargará los cmdlets de Exchange 2010. Esto puede impedirle realizar ciertas tareas, ya que los cmdlets de Exchange 2010 no pueden administrar la configuración ni los servidores de Exchange 2013.
    
    A partir de Exchange 2013 CU11, este comportamiento es intencionado. Para asegurarse de que el Shell cargue los cmdlets de Exchange 2013, mueva el buzón del usuario conectado a Exchange 2013. Si el usuario conectado no tiene buzón, mueva el buzón de arbitraje SystemMailbox{bb558c35-97f1-4cb9-8ff7-d53741dc928c} a un servidor de Exchange 2013.
    
    Para obtener información sobre cómo mover el buzón de arbitraje, vea [Shell de administración de Exchange y delimitación de buzones](https://go.microsoft.com/fwlink/?linkid=717722) en el blog del equipo de Exchange.

## Buzón

  - **Los servidores de buzones que ejecutan versiones distintas de Exchange pueden agregarse al mismo grupo de disponibilidad de base de datos** El cmdlet **Add-DatabaseAvailabilityGroupServer** y el Centro de administración de Exchange permiten erróneamente añadir un servidor de Exchange 2013 a un grupo de disponibilidad de base de datos basado en Exchange 2016 (DAG) y viceversa. Exchange solo admite agregar servidores de buzones que ejecutan la misma versión (Exchange 2013 frente a Exchange 2016, por ejemplo) a un DAG. Además, el Centro de administración de Exchange muestra los dos servidores Exchange 2013 y Exchange 2016 en la lista de servidores disponibles para agregar a un DAG. Así se podría permitir a un administrador agregar inadvertidamente un servidor que ejecuta una versión incompatible de Exchange a un DAG (por ejemplo, agregar un servidor Exchange 2013 a un DAG basado en Exchange 2016).
    
    Actualmente no hay ninguna solución alternativa para este problema. Los administradores deben ser diligentes al agregar un servidor de buzones a un DAG. Agregue solo servidores Exchange 2013 a DAG basados en Exchange 2013 y solo servidores Exchange 2016 a DAG basados en Exchange 2016. Es posible distinguir cada una de las versiones de Exchange examinando la columna de la **Versión** en la lista de servidores del Centro de administración de Exchange. Las siguientes son las versiones de servidor de Exchange 2013 y Exchange 2016:
    
      - **Exchange 2013** 15.0 (Compilación xxx.xx)
    
      - **Exchange 2016** 15.1 (Compilación xxx.xx)

  - **Incremento del tamaño del buzón de correo al migrar de versiones anteriores de Exchange**   Cuando mueve un buzón de correo de una versión anterior de Exchange a Exchange 2013, el tamaño del buzón de correo notificado se incrementa de un 30 a un 40 por ciento. El espacio de disco que usa la base de datos de buzón no se ha incrementado, sólo ha aumentado la atribución del espacio que usa cada buzón de correo. El incremento en el tamaño del buzón de correo es debido a la inclusión de todas las propiedades de los elementos en los cálculos de la cuota, que proporciona un cómputo más preciso del espacio que usan los elementos dentro de su buzón de correo. Este incremento puede provocar que algunos usuarios excedan sus cuotas de tamaño de buzón de correo cuando éste se mueve a Exchange 2013.
    
    Para evitar que los usuarios excedan sus cuotas de tamaño de buzón de correo, incremente los valores de la base de datos o de las cuotas del buzón de correo para acomodar el cálculo de la nueva cuota. Para configurar los valores de la base de datos o de la cuota del buzón de correo, use los parámetros *IssueWarningQuota*, *ProhibitSendQuota* y *ProhibitSendReceiveQuota* en los cmdlets **Set-MailboxDatabase** y **Set-Mailbox**, respectivamente.

  - Es posible que los clientes de **Outlook 2007 y Outlook 2010 no puedan descargar la Libreta de direcciones sin conexión**   Si no se puede acceder a la Libreta de direcciones sin conexión (OAB) desde Internet, es posible que los clientes de Outlook 2007 y Outlook 2010 no puedan descargar la OAB.
    
    Para solucionar este problema con los clientes de Outlook 2007 y Outlook 2010, haga que se pueda acceder a la URL interna de la OAB desde Internet. Este problema no afecta a Outlook 2013.

  - **Instalar Exchange 2013 en una organización de Exchange existente puede provocar que todos los clientes se descarguen la OAB**   Instalar el primer servidor Exchange 2013 en una organización de Exchange 2007 o Exchange 2010 existente puede provocar que todos los clientes de la organización se descarguen una nueva copia de la OAB, lo que daría lugar a una saturación de la red y a problemas de rendimiento en el servidor. Este problema se produce porque Exchange 2013 crea una nueva OAB predeterminada en la organización que sustituye a la OAB de Exchange 2007 o de Exchange 2010. Los buzones que no tengan una OAB concreta asignada o que se encuentren en una base de datos de buzones de correo sin una OAB concreta asignada se bajarán la nueva OAB predeterminada.
    
    Para evitar que los clientes se bajen una nueva copia de la OAB cuando se instala Exchange 2013, asigne una OAB a cada buzón o a la base de datos de buzones de correo donde se encuentran los buzones. Deberá realizar este paso antes de instalar Exchange 2013 en la organización.

  - **Puede enrutarse a los usuarios a un buzón de generación de OAB que no sea responsable de la OAB solicitada**Exchange 2013 CU5 y las CU posteriores han cambiado el modo en que se vinculan las OAB con los buzones de generación de OAB. Este cambio permite enrutar un usuario a un buzón de generación de OAB que no es responsable de la OAB que el usuario está solicitando. Esto puede pasar si se cumplen todas las condiciones siguientes:
    
      - Cuenta con más de un buzón de generación de OAB en su organización.
    
      - Actualiza los servidores de buzones de correo que hospedan los buzones de generación de OAB antes de actualizar los servidores de acceso de cliente.
    
      - Está actualizando sus servidores Exchange 2013 de una versión anterior a CU5 a una versión posterior (por ejemplo, actualización de Exchange 2013 CU3 a Exchange 2013 CU6).
    
      - Los servidores de acceso de cliente están ejecutando una versión anterior a CU5.
    
    Para solucionar este problema, asegúrese de actualizar sus servidores de acceso de cliente a Exchange 2013 CU6 o posterior antes de actualizar los servidores de buzones de correo. De este modo se asegurará de que los servidores de acceso de cliente sepan cómo usar un proxy para las solicitudes del buzón de generación de OAB que es responsable de generar la OAB del usuario.
    
    Para obtener más información sobre los cambios de la OAB en Exchange 2013 CU5, vea [Mejoras de la OAB en la actualización acumulativa 5 de Exchange 2013](https://go.microsoft.com/fwlink/p/?linkid=400642).

## Carpetas públicas

  - **Los remitentes no autorizados ya no pueden enviar mensajes a las carpetas públicas habilitadas para correo**   Antes de Exchange 2013 CU6, los remitentes no autorizados podían enviar mensajes a las carpetas públicas habilitadas para correo. Esto permitía la posibilidad de que los remitentes externos enviaran correo a carpetas públicas habilitadas para correo, independientemente de los permisos establecidos en la carpeta pública.
    
    A partir de Exchange 2013 CU6, si desea que los remitentes externos envíen correo a carpetas públicas habilitadas para correo, se debe conceder al menos el permiso **Crear elementos** al usuario **Anónimo**. Si ha configurado las carpetas públicas habilitadas para correo y no ha hecho esto, los remitentes externos recibirán una notificación de error de entrega y no se entregarán los mensajes a la carpeta pública habilitada para correo.
    
    Puede usar el Shell o Outlook para establecer los permisos para el usuario Anónimo. Para leer más sobre cómo establecer permisos en el usuario Anónimo, consulte [Habilitar o deshabilitar el correo para una carpeta pública](mail-enable-or-mail-disable-a-public-folder-exchange-2013-help.md).

  - El número máximo de carpetas públicas que se pueden migrar a Exchange 2013 desde los servidores de Exchange heredados es 500.000. Para obtener más información acerca de la migración de carpetas públicas, consulte [Usar migración por lotes para migrar carpetas públicas a Exchange 2013 desde versiones anteriores](use-batch-migration-to-migrate-public-folders-to-exchange-2013-from-previous-versions-exchange-2013-help.md).

## Flujo de correo

  - **Los cmdlets TransportAgent de los servidores de acceso de cliente requieren Windows PowerShell local**   Existe un problema con los cmdlets **\*-TransportAgent** que impiden la instalación, desinstalación y administración de agentes de transporte en servidores de acceso de cliente usando el Shell de administración de Exchange. Para instalar, desinstalar y administrar los agentes de transporte en los servidores de acceso de cliente, debe cargar manualmente el complemento ExchangeWindows PowerShell y, a continuación, ejecutar los cmdlets **\*-TransportAgent**. Si intenta instalar, desinstalar o administrar agentes de transporte usando el Shell de administración de Exchange, sus cambios se aplicarán al servidor de buzones de correo de Exchange 2013 al que esté conectado.
    
    Para instalar, desinstalar o administrar los agentes de transporte en los servidores de acceso de clientes, haga lo siguiente en el servidor de acceso de clientes que desee administrar:
    

    > [!WARNING]
    > La carga del complemento <CODE>Microsoft.Exchange.Management.PowerShell.SnapIn</CODE>Windows PowerShell y la ejecución de otros cmdlets distintos a los cmdlets <STRONG>*-TransportAgent</STRONG> no es compatible y puede resultar en un daño irreparable en su implementación de Exchange.<BR>Debe ser un administrador local en el servidor de acceso de clientes donde desee instalar, desinstalar o administrar agentes de transporte. La modificación de las listas de control de acceso (ACL) no es compatible en los archivos y directorios de Exchange o en los objetos de Active Directory.

    

    > [!IMPORTANT]
    > Realice el siguiente procedimiento sólo en servidores de acceso de clientes. No es necesario cargar el complemento de ExchangeWindows PowerShell si desea administrar los agentes de transporte en los servidores de buzones de correo.

    
    1.  Abra una nueva ventana de Windows PowerShell.
    
    2.  Ejecute el siguiente comando.
        
            Add-PSSnapin Microsoft.Exchange.Management.PowerShell.SnapIn
    
    3.  Realice las tareas de administración del agente de transporte de la forma habitual.
    
    4.  Repita este procedimiento en cada servidor de acceso de clientes que desee administrar.

## Conectividad de clientes

  - **Error en la autenticación NTLM para clientes que no pertenecen a un dominio**   Se puede producir un error en la autenticación entre un cliente, como Windows Live Mail y Exchange 2013, cuando se cumplen las siguientes condiciones:
    
      - El método de autenticación utilizado por el cliente es NTLM.
    
      - El equipo no está conectado al dominio.
    
    Para evitar este problema, puede realizar una de las siguientes acciones:
    
      - Conecte al dominio el equipo en el que se ejecuta el cliente.
    
      - Cambie el tipo de autenticación que el cliente usa de NTLM a autenticación básica a través de TLS.

  - **Se produce un error en la autenticación GSSAPI si se utiliza con el cmdlet Send-MailMessage**   Se puede producir un error en la autenticación GSSAPI (Generic Security Service Application Program Interface) si se utiliza el cmdlet **Send-MailMessage**, incluido en las instalaciones de manera predeterminada, Windows PowerShell, para enviar correo autenticado a Exchange 2013. Cuando esto sucede, verá una entrada en el registro de eventos de la **Aplicación** en el servidor de acceso de cliente de Exchange 2013 que recibió la conexión con la siguiente información:
    
      - **Origen**   MSExchangeFrontEndTransport
    
      - **Id. de evento**   1035
    
      - **Descripción**   Error de autenticación entrante `IllegalMessage` para front-end de cliente de conector de recepción \<*nombre de servidor*\>. El mecanismo de autenticación es Gssapi. La dirección IP de origen del cliente que intentó autenticar en Exchange es \[\<*dirección IP del cliente*\>\].
    
    Para solucionar este problema, es necesario quitar el método de autenticación `Integrated` del conector de recepción del cliente en los servidores de acceso de cliente de Exchange 2013. Para quitar el método de autenticación `Integrated` de un conector de recepción de cliente, ejecute el siguiente comando en cada servidor de acceso de cliente de Exchange 2013 que podría recibir conexiones desde equipos que ejecutan el cmdlet **Send-MailMessage**:
    
        Set-ReceiveConnector "<server name>\Client Frontend <server name>" -AuthMechanism Tls, BasicAuth, BasicAuthRequireTLS

  - **Puede que MAPI sobre HTTP experimente un bajo nivel de rendimiento al actualizar a Exchange 2013 SP1**   Si actualiza desde una actualización acumulativa de Exchange 2013 a Exchange 2013 SP1 y habilita MAPI sobre HTTP, los clientes que se conecten a un servidor de Exchange 2013 SP1 usando el protocolo pueden experimentar un bajo nivel de rendimiento. El motivo es que no se configuran las opciones necesarias durante una actualización acumulativa a Exchange 2013 SP1. Este problema no se produce si se actualiza a Exchange 2013 SP1 desde Exchange 2013 RTM o si se instala un nuevo servidor Exchange 2013 SP1 o posterior.
    

    > [!NOTE]
    > Esto supone un problema únicamente si el protocolo MAPI sobre HTTP está habilitado en los servidores de acceso de cliente. Está deshabilitado de forma predeterminada. Si MAPI sobre HTTP está deshabilitado, los clientes usan en su lugar el protocolo RPC sobre HTTP.

    
    Para resolver este problema, realice los siguientes pasos:
    
    1.  En servidores que ejecutan el rol de servidor de acceso de cliente, ejecute los siguientes comandos en un símbolo del sistema de Windows:
        
            set AppCmdLocation=%windir%\System32\inetsrv
            set ExchangeLocation=%ProgramFiles%\Microsoft\Exchange Server\V15
            
            %AppCmdLocation%\appcmd.exe SET AppPool "MSExchangeMapiFrontEndAppPool" /CLRConfigFile:"%ExchangeLocation%\bin\MSExchangeMapiFrontEndAppPool_CLRConfig.config"
            %AppCmdLocation%\appcmd.exe RECYCLE AppPool "MSExchangeMapiFrontEndAppPool"
    
    2.  En servidores que ejecutan el rol de servidor de buzón de correo, ejecute los siguientes comandos en un símbolo del sistema de Windows:
        
            set AppCmdLocation=%windir%\System32\inetsrv
            set ExchangeLocation=%ProgramFiles%\Microsoft\Exchange Server\V15
            
            %AppCmdLocation%\appcmd.exe SET AppPool "MSExchangeMapiMailboxAppPool" /CLRConfigFile:"%ExchangeLocation%\bin\MSExchangeMapiMailboxAppPool_CLRConfig.config"
            %AppCmdLocation%\appcmd.exe RECYCLE AppPool "MSExchangeMapiMailboxAppPool"
            
            %AppCmdLocation%\appcmd.exe SET AppPool "MSExchangeMapiAddressBookAppPool" /CLRConfigFile:"%ExchangeLocation%\bin\MSExchangeMapiAddressBookAppPool_CLRConfig.config"
            %AppCmdLocation%\appcmd.exe RECYCLE AppPool "MSExchangeMapiAddressBookAppPool"

## Coexistencia de Exchange 2010

  - **Es posible que las solicitudes para acceder a los buzones de correo de Exchange 2010 no funcionen cuando se redirijan mediante proxy a través de los servidores de acceso de cliente de Exchange 2013**   En algunos casos, es posible que la solicitud de proxy entre los servidores de acceso de cliente de Exchange 2013 y Exchange 2010 Service Pack 3 (SP3) sin ningún paquete acumulativo de actualizaciones instalado no funcione correctamente y que genere un error. Esto puede pasar si se cumplen todas las condiciones siguientes:
    
      - Un usuario con un buzón de correo de Exchange 2013 intenta abrir un buzón de correo de Exchange 2010 mediante uno de los siguientes métodos:
        
          - La opción **Abrir otro buzón** de Outlook Web App**- o-**
        
          - La opción **Otro usuario** del centro de administración de Exchange
    
      - El servidor de acceso de cliente al que se conecta el usuario está ejecutando Exchange 2013.
    
      - El servidor de acceso de cliente de Exchange 2010 se ha actualizado a Exchange 2010 SP3 desde la versión RTM de Exchange 2010 o un Service Pack anterior de Exchange 2010.
    
    Si se cumplen todas las condiciones anteriores, el usuario no podrá acceder a las opciones de Exchange 2010Outlook Web App del otro usuario y aparecerá una página en blanco.
    
    Para solucionar este problema, instale el Paquete acumulativo de actualizaciones 1 o posterior de Exchange 2010 en cada servidor de Exchange 2010.

