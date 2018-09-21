---
title: 'Actualizar la UM de Exchange 2010 a la UM de Exchange 2013: Exchange 2013 Help'
TOCTitle: Actualizar la mensajería UNIFICADA de Exchange 2007 para la mensajería UNIFICADA de Exchange de 2013
ms:assetid: 642c922d-7e85-40f0-bb9b-0f20da692be3
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn169227(v=EXCHG.150)
ms:contentKeyID: 54652433
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Actualizar la mensajería UNIFICADA de Exchange 2007 para la mensajería UNIFICADA de Exchange de 2013

 

_**Se aplica a:** Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2016-12-09_

Cuando actualiza de una organización de Microsoft Exchange 2007 con mensajería unificada a mensajería unificada de Exchange 2013, existen pasos obligatorios y otros pasos que ya se completaron como parte de la implementación de mensajería unificada de Exchange 2007. Dependiendo del entorno de telefonía y de los componentes de mensajería unificada creados y configurados para admitir la mensajería unificada en Exchange 2007, puede que sea necesario implementar equipo adicional de telefonía, incluidas puertas de enlace de voz sobre IP (VoIP) o centrales de conmutación (PBX) IP, o PBX tradicionales o habilitadas para SIP, y, a continuación, crear y configurar los componentes de mensajería unificada adicionales necesarios para mensajería unificada de Exchange 2013.

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar esta tarea: 45 a 90 minutos.

  - Compruebe que tiene los permisos adecuados en la organización de Exchange 2007 y de Exchange 2013 para crear y configurar todos los componentes necesarios.

  - Compruebe que implementó y configuró correctamente los componentes de telefonía, incluidas las puertas de enlace VoIP y PBX, IP-PBX o PBX habilitadas para Protocolo de inicio de sesión (SIP).

  - Compruebe que instaló y configuró correctamente los servidores de acceso de cliente que ejecutan el servicio de enrutador de llamadas de mensajería unificada de Microsoft Exchange y los servidores de buzones de correo que ejecutan el servicio de mensajería unificada de Microsoft Exchange. Para obtener más información acerca de los servicios de mensajería unificada, consulte [Servicios de mensajería unificada](um-services-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Cómo realiza esto?

## Paso 1: Descargar e instalar los paquetes de idioma de mensajería unificada requeridos

Los paquetes de idioma de mensajería unificada permiten a las personas que llaman y a los usuarios de Outlook Voice Access interactuar con el sistema de correo de voz en varios idiomas. Tras instalar un idioma adicional en un servidor de buzones de correo de Exchange 2013, las personas que llaman y los usuarios de Outlook Voice Access podrán escuchar mensajes de correo electrónico e interactuar con el sistema de correo de voz en dicho idioma. Sin embargo, para hacer que el idioma esté disponible para todas las llamadas entrantes, debe instalar los paquetes necesarios de idiomas de mensajería unificada en todos los servidores de buzón de Exchange 2013. Esto se debe a que cada servidor de buzón de Exchange 2013 puede responder llamadas entrantes para mensajería unificada.

De manera predeterminada, al instalar un servidor de buzones de correo de Exchange 2013, se instala el paquete de idioma de inglés de Estados Unidos (en-US). Es la única opción de idioma disponible para el plan de marcado a menos que instale otro paquete de idioma de mensajería unificada. (No se puede eliminar el paquete de idioma de inglés de EE. UU. a no ser que elimine el servidor de buzones del equipo). Tras instalar un paquete de idioma de mensajería unificada en un servidor de buzón de correo de Exchange 2013, el idioma asociado al paquete de idioma también aparecerá como opción disponible al configurar el idioma predeterminado del plan de marcado. De manera predeterminada, como un operador automático de mensajería unificada se vincula a un plan de marcado de mensajería unificada cuando se crea, usa la configuración de idioma predeterminada del plan de marcado de mensajería unificada al que está vinculado. Sin embargo, es posible cambiar esta configuración después de crear el operador automático de mensajería unificada.


> [!NOTE]
> Si inglés de EE. UU. es el único idioma que desea proporcionar para su plan de marcado, puede omitir este paso e ir al paso 2.



Puede agregar paquetes de idioma de mensajería UNIFICADA mediante el comando setup.exe o ejecutando el programa de instalación .exe *\<UMLanguagePack\>*una vez que haya descargado el paquete de idioma de mensajería UNIFICADA de [Exchange Server 2013 UM paquetes de idioma](https://go.microsoft.com/fwlink/p/?linkid=266542). Para obtener más información, consulte [Instalar un paquete de idioma de mensajería unificada](install-a-um-language-pack-exchange-2013-help.md).

Este ejemplo usa setup.exe para instalar el paquete de idioma de mensajería unificada de japonés (ja-JP).

```powershell
setup.exe /AddUmLanguagePack:ja-JP /s:d:\Exchange\UMLanguagePacks /IAcceptExchangeServerLicenseTerms
```

## Paso 2: Mover los saludos, anuncios, menús y mensajes personalizados de Exchange 2007 al buzón del sistema de Exchange 2013.

Los operadores automáticos y planes de marcado de mensajería unificada usan los saludos, anuncios, menús y mensajes personalizados. El buzón del sistema denominado {e0dc1c29-89c3-4034-b678-e6c29d823ed9} se crea cuando instala Exchange 2007 o Exchange 2013 y se usa para admitir características, como aprobación de mensajes y búsqueda en varios buzones de correo. El buzón de correo del sistema también se usa para almacenar saludos, anuncios, menús y mensajes personalizados del plan de marcado y del operador automático. Si el buzón de correo del sistema no existe, puede usar el comando **Setup /PrepareAD** para crearlo.

De manera predeterminada, los buzones de correo del sistema no están visibles en el Centro de administración de Exchange (EAC). Puede obtener una lista de los buzones de correo del sistema al ejecutar una de las siguientes alternativas:

Este comando devuelve una lista de todos los buzones de correo del sistema.

```powershell
Get-Mailbox -Arbitration
```

Este comando devuelve una lista de los buzones de correo del sistema y sus propiedades u opciones de configuración individuales.

```powershell
Get-Mailbox -Arbitration |fl
```

Cuando importa saludos, anuncios, menús y mensajes personalizados de Exchange 2007 a Exchange 2013, debe usar el script MigrateUMCustomPrompts.ps1. No puede usar el EAC para importar saludos, anuncios, menús y mensajes personalizados. El script MigrateUMCustomPrompts.ps1 migra una copia de todos los saludos, anuncios, menús y mensajes personalizados de mensajería unificada de Exchange Server 2007 a mensajería unificada de Exchange 2013. De manera predeterminada, el script MigrateUMCustomPrompts.ps1 se encuentra en la carpeta *\<Archivos de programa\>*\\Microsoft\\Exchange Server\\V15\\Scripts en un servidor de buzón de Exchange 2013 y debe ejecutarse desde un servidor de buzón de Exchange 2013. Para ejecutar el script:

1.  Haga clic en **Inicio** \> **Todos los programas** \> **Microsoft Exchange Server 2013** \> **Consola de administración de Exchange**.

2.  En el Shell de administración de Exchange, en el símbolo del sistema, escriba la ruta de acceso al script. Por ejemplo, escriba **cd "D:\\Archivos de programa\\Microsoft\\Exchange Server\\V15\\Scripts"** y, a continuación, presione Entrar.

3.  En el símbolo del sistema del Shell, escriba **".\\MigrateUMCustomPrompts"** y, a continuación, presione Entrar.


> [!NOTE]
> También se pueden importar mensajes personalizados individualmente usando el cmdlet <STRONG>Import-UMPrompt</STRONG>. El cmdlet <STRONG>Copy-UMCustomPrompt</STRONG> de mensajería unificada de Exchange 2007 no es compatible con la copia de mensajes personalizados a mensajería unificada de Exchange 2013.



Cuando ejecuta el script MigrateUMCustomPrompts.ps1 desde el servidor de Exchange 2013, el script realiza una búsqueda de identificador de objeto o GUID para el plan de marcado u operador automático en Active Directory y lo consulta para determinar si existen saludos, anuncios, menús o mensajes personalizados. Si se encuentran, los saludos, anuncios, menús y mensajes personalizados se importarán al buzón del sistema denominado {e0dc1c29-89c3-4034-b678-e6c29d823ed9}.

Al usar este buzón del sistema, es posible realizar una copia de seguridad de los saludos, anuncios, menús y mensajes personalizados, y restaurar la copia de seguridad junto con otros buzones en una base de datos. Esto reduce la cantidad de recursos necesarios. El almacenamiento de saludos, anuncios, menús y mensajes personalizados en un buzón del sistema elimina toda posible incoherencia que pudiera haber existido. Para conocer más detalles acerca de cómo mover buzones, consulte [Movimientos de buzones de Exchange 2013](mailbox-moves-in-exchange-2013-exchange-2013-help.md).

## Paso 3: Exportar e importar certificados

Si usa planes de marcado protegidos por SIP o protegidos en la organización de Exchange 2007, deberá exportar e importar los certificados utilizados a los servidores de buzón y de acceso de cliente de Exchange 2013. La Seguridad de la capa de transporte mutua (TLS mutua) se usa para cifrar datos enviados entre los servidores de Exchange 2013 y las puertas de enlace VoIP, IP-PBX e IP-PBX habilitadas para SIP. Los certificados enlazan la identidad del propietario del certificado con un par de claves electrónicas (pública y privada) que se utilizan para cifrar y firmar la información digitalmente. Puede usar uno de los siguientes certificados para los servicios de enrutador de llamadas de mensajería unificada y de mensajería unificada:

  - Un certificado autofirmado (Exchange)

  - Un certificado de infraestructura de clave pública (PKI) interno

  - Un certificado comercial de otros fabricantes

De manera predeterminada, cuando instala Exchange 2013, se crean dos certificados autofirmados: **Certificado de autenticación de Microsoft Exchange Server** y **Microsoft Exchange**. El certificado autofirmado de **Microsoft Exchange** puede usarse para que la mensajería unificada cifre datos, pero usted debe asignar el certificado a los servicios de enrutador de llamadas de mensajería unificada y de mensajería unificada. Este certificado autofirmado se puede copiar y luego importar en las puertas de enlace VoIP, IP-PBX e IP-PBX habilitadas para SIP. Sin embargo, no se puede usar cuando integra mensajería unificada con Microsoft Lync Server.

Para que la mensajería unificada pueda cifrar datos enviados entre servidores de Exchange 2013 y puertas de enlace VoIP, IP-PBX e IP-PBX habilitadas para SIP, haga lo siguiente:

  - Use un certificado existente autofirmado de mensajería unificada, cree un certificado de Exchange autofirmado, envíe una solicitud de certificado a una autoridad de certificación interna para un certificado PKI o compre un certificado comercial de otros fabricantes que pueda usar para TLS mutua entre los servidores de acceso de cliente y de buzón de Exchange 2013 y las puertas de enlace VoIP, IP-PBX y PBX habilitada para SIP.
    
    Cree un certificado autofirmado de Exchange con el EAC de la siguiente manera:
    
    1.  En el EAC, vaya a **Servidores** \> **Certificados** y, a continuación, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").
    
    2.  En la página **Nuevo certificado de Exchange**, elija **Crear un certificado autofirmado** y seleccione **Siguiente**.
    
    3.  Escriba un nombre descriptivo para el certificado y luego seleccione **Siguiente**.
    
    4.  Haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") para seleccionar los servidores de Exchange a los que desee aplicar este certificado. A continuación, haga clic en **Siguiente**.
    
    5.  Especifique los dominios que desee incluir en el certificado y, a continuación, seleccione **Siguiente**. Si desea agregar un dominio para un servicio, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").
    
    6.  Compruebe que los nombres de los dominios incluidos sean correctos y luego seleccione **Finalizar**.
    

    > [!IMPORTANT]
    > Cuando use el EAC para crear un certificado, no se le solicitará que habilite los servicios para el certificado. Tras la creación del certificado, puede usar el EAC para habilitar los servicios. Para obtener más información acerca de cómo habilitar un certificado para servicios, consulte <A href="assign-a-certificate-to-the-um-and-um-call-router-services-exchange-2013-help.md">Asignar un certificado a los servicios de mensajería unificada y llamar al enrutador de mensajería unificada</A>.

    
    Cree un certificado autofirmado de Exchange al ejecutar el siguiente comando en el Shell.
    
        New-ExchangeCertificate -Services 'UM, UMCallRouter' -DomainName '*.northwindtraders.com' -FriendlyName 'UMSelfSigned' -SubjectName 'C=US,S=WA,L=Redmond,O=Northwindtraders,OU=Servers,CN= Northwindtraders.com' -PrivateKeyExportable $true
    

    > [!TIP]
    > Si especifica los servicios que desea habilitar mediante el parámetro <EM>Services</EM>, se le solicitará que habilite los servicios para el certificado que creó. En este ejemplo, se le solicitará que habilite el certificado para los servicios de enrutador de llamadas de mensajería unificada y de mensajería unificada. Para obtener más información acerca de cómo habilitar un certificado para servicios, consulte <A href="assign-a-certificate-to-the-um-and-um-call-router-services-exchange-2013-help.md">Asignar un certificado a los servicios de mensajería unificada y llamar al enrutador de mensajería unificada</A>.



  - Importe el certificado que se utilizará en todos los servidores de acceso de cliente y servidores de buzones de Exchange 2013 en su organización. Si usa el certificado autofirmado de Exchange 2013, deberá copiar el certificado y luego importarlo en las puertas de enlace VoIP, IP-PBX o PBX habilitada para SIP. Si usa el certificado autofirmado de Exchange 2007, el nombre alternativo del firmante (SAN) debe contener los nombres de los equipos de todos los servidores de Exchange 2013. Si tiene servidores de mensajería unificada de Exchange 2007 en la organización, puede usar el certificado autofirmado de Exchange 2013, pero debe agregar los nombres de los equipos de los servidores de mensajería unificada de Exchange 2007 al SAN en el certificado de Exchange 2013.

  - Habilite o asigne el certificado que se usará a los servicios de enrutador de llamadas de mensajería unificada y de mensajería unificada en los servidores de acceso de cliente y de buzón en la organización.
    
    Habilite el servicio de mensajería unificada y el servicio de enrutador de llamadas de mensajería unificada en todos los servidores de Exchange 2013 para usar el certificado autofirmado de Exchange mediante el uso del EAC de la siguiente manera:
    
    1.  En el EAC, vaya a **Servidores** \> **Certificados**, seleccione el certificado en el que desee habilitar servicios y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").
    
    2.  En la página **Procedimiento**, seleccione **Servicios**, **Mensajería unificada** y, a continuación, seleccione **Enrutador de llamadas de mensajería unificada**.
    
    Habilite un certificado autofirmado de Exchange ejecutando el siguiente comando en el Shell.
    
        Enable-ExchangeCertificate -Thumbprint 5113ae0233a72fccb75b1d0198628675333d010e -Services 'UM, UMCallRouter'

  - Configure cualquier plan de marcado nuevo o existente de mensajería unificada como protegido por SIP o protegido.

  - Configure el modo de inicio de la mensajería unificada en los servidores de acceso de cliente y de buzones en su organización.

  - Cree y configure puertas de enlace IP de mensajería unificada nuevas o existentes con un nombre de dominio completo (FQDN).

  - Configure el puerto de escucha en las puertas de enlace IP de mensajería unificada para usar el puerto 5061 TLS.

  - Reinicie el servidor de enrutador de llamadas de mensajería unificada en todos los servidores de acceso de cliente de Exchange 2013 y reinicie el servicio de mensajería unificada en todos los servidores de buzón de Exchange 2013. Para obtener más información acerca de los servicios de mensajería unificada, consulte [Servicios de mensajería unificada](um-services-exchange-2013-help.md).

## Paso 4: Configurar el modo de inicio de mensajería unificada en todos los servidores de acceso de cliente de Exchange 2013

Si usa planes de marcado protegidos por SIP o protegidos, debe configurar el modo de inicio de mensajería unificada en los servidores de acceso de cliente de Exchange 2013. Puede especificar el modo de inicio de mensajería unificada para el servicio de enrutador de llamadas de mensajería unificada en un servidor de acceso de cliente de Exchange 2013 mediante el EAC o el Shell. De manera predeterminada, el servidor de acceso de cliente de Exchange 2013 se iniciará en el modo TCP, pero si utiliza Seguridad de la capa de transporte (TLS) para cifrar el tráfico de voz sobre IP (VoIP), debe configurar el servidor de acceso de cliente de Exchange 2013 para que utilice el modo Dual o TLS. Le recomendamos configurar todos los servidores de acceso de cliente de Exchange 2013 para que usen el modo Dual como modo de inicio de mensajería unificada. Esto se debe a que todos los servidores de acceso de cliente de Exchange 2013 pueden responder a las llamadas entrantes para todos los planes de marcado de mensajería unificada, y esos planes de marcado pueden tener una configuración de seguridad distinta. Si cambia el modo de inicio de mensajería unificada, debe reiniciar el servicio de enrutador de llamadas de mensajería unificada para que el cambio surta efecto. Para obtener más información acerca de los servicios de mensajería unificada, consulte [Servicios de mensajería unificada](um-services-exchange-2013-help.md).

Configure el modo de inicio de mensajería unificada en un servidor de acceso de cliente de Exchange 2013 mediante el EAC de la siguiente manera:

1.  En el EAC, desplácese hasta **Servidores** \> **Servidores**.

2.  En la vista de lista, seleccione el servidor de Exchange que desea modificar y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Exchange Server**, haga clic en **Mensajería unificada**.

4.  En **Configuración de enrutador de llamadas de mensajería unificada** \> **Modo de inicio de mensajería unificada**, seleccione una de las siguientes opciones de la lista desplegable:
    
      - **TCP** Utilice esta opción si no utiliza mTLS y utiliza únicamente planes de marcado no seguros.
    
      - **TLS**   Utilice esta opción si utiliza mTLS y utiliza únicamente planes de marcado protegidos por SIP o protegidos.
    
      - **DUAL**   Utilice esta opción si utiliza mTLS y utiliza planes de marcado no protegidos, protegidos por SIP y protegidos.

5.  Después de seleccionar el modo de inicio de mensajería unificada, haga clic en **Guardar**.

Configure el modo de inicio de mensajería unificada en un servidor de acceso de cliente de Exchange 2013 mediante el Shell de la siguiente manera:

```powershell
Set-UMCallRouterSettings -Server MyUMCallRouter.northwindtraders.com -UMStartupMode Dual
```

## Paso 5: Configurar el modo de inicio de mensajería unificada en todos los servidores de buzón de Exchange 2013

Si usa planes de marcado protegidos por SIP o protegidos, debe configurar el modo de inicio de mensajería unificada en los servidores de buzón de Exchange 2013. Puede especificar el modo de inicio de mensajería unificada para el servicio de mensajería unificada en un servidor de buzón de Exchange 2013 mediante el EAC o el Shell. De manera predeterminada, el servidor de buzones de Exchange 2013 se iniciará en el modo TCP, pero si usa Seguridad de la capa de transporte (TLS) para cifrar el tráfico de voz sobre IP (VoIP), debe configurar el servidor de buzones de Exchange 2013 para que use el modo Dual o TLS. Le recomendamos configurar todos los servidores de buzones de Exchange 2013 para que usen el modo Dual como modo de inicio de mensajería unificada. Esto se debe a que todos los servidores de buzones de Exchange 2013 pueden responder a las llamadas entrantes para todos los planes de marcado de mensajería unificada, y esos planes de marcado pueden tener una configuración de seguridad distinta. Si cambia el modo de inicio de mensajería unificada, debe reiniciar el servicio de mensajería unificada para que el cambio surta efecto. Para obtener más información acerca de los servicios de mensajería unificada, consulte [Servicios de mensajería unificada](um-services-exchange-2013-help.md).

Configure el modo de inicio de mensajería unificada en un servidor de buzones de Exchange 2013 mediante el EAC de la siguiente manera:

1.  En el EAC, desplácese hasta **Servidores** \> **Servidores**.

2.  En la vista de lista, seleccione el servidor de Exchange que desea modificar y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Exchange Server**, haga clic en **Mensajería unificada**.

4.  En **Configuración del servicio de mensajería unificada** \> **Modo de inicio de mensajería unificada**, seleccione una de las siguientes opciones de la lista desplegable:
    
      - **TCP** Utilice esta opción si no utiliza mTLS y utiliza únicamente planes de marcado no seguros.
    
      - **TLS**   Utilice esta opción si utiliza mTLS y utiliza únicamente planes de marcado protegidos por SIP o protegidos.
    
      - **DUAL**   Utilice esta opción si utiliza mTLS y utiliza planes de marcado no protegidos, protegidos por SIP y protegidos.

5.  Después de seleccionar el modo de inicio de mensajería unificada, haga clic en **Guardar**.

Configure el modo de inicio de mensajería unificada en un servidor de buzón de Exchange 2013 al ejecutar el siguiente comando en el Shell.

    Set-UMService -Identity MyUMServer -ExternalHostFqdn host.external.contoso.com -IPAddressFamily Any -UMStartupMode Dual

## Paso 6: Crear o configurar planes de marcado de mensajería unificada existentes

Según la implementación de Exchange 2007 existente, es posible que deba crear planes de marcado de mensajería unificada o que deba configurar los planes de marcado existentes. Un plan de marcado de mensajería unificada representa un conjunto de centrales de conmutación (PBX), IP-PBX o PBX tradicionales o habilitadas para SIP que comparten números de extensión de usuarios en común. Todas las extensiones de usuarios hospedadas en PBX o IP-PBX tradicionales o habilitadas para SIP en un plan de marcado contienen la misma cantidad de dígitos. Los usuarios pueden marcar otra extensión de teléfono sin anexar un número especial a la extensión o sin marcar un número de teléfono completo.

Los planes de marcado de mensajería unificada se usan en la mensajería unificada para garantizar que las extensiones telefónicas de los usuarios son únicas. En algunas redes de telefonía, existen varias IP-PBX, PBX tradicionales o PBX habilitadas para SIP. En estas redes de telefonía, pueden existir dos usuarios que tengan el mismo número de extensión telefónica. Los planes de marcado de mensajería unificada resuelven esta situación. Al poner a dos usuarios en dos planes de marcado de mensajería unificada separados, las extensiones son únicas. Para obtener más información, consulte [Planes de marcado de mensajería unificada](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/set-up-client-voice-mail-features/set-the-voice-mail-preview-partner-address).

Si es necesario, puede crear un plan de marcado de mensajería unificada con el EAC:

1.  En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada** y, a continuación, haga clic en **Nuevo**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").

2.  En la página **Nuevo plan de marcado de mensajería unificada**, complete las siguiente información:
    
      - **Nombre**   Escriba el nombre del plan de marcado. El nombre de un plan de marcado de mensajería unificada es necesario y debe ser exclusivo. Sin embargo, el nombre que escriba se usará solo para la visualización en el EAC y en el Shell. La longitud máxima del nombre de un plan de marcado de mensajería unificada es de 64 caracteres y puede incluir espacios. No obstante, no pueden incluirse ninguno de los caracteres siguientes: " / \\ \[ \] : ; | = , + \* ? \< \>.
        
        Aunque en el cuadro del nombre del plan de marcado se pueden escribir hasta 64 caracteres, el nombre no debe tener más de 49. Si intenta crear un nombre de plan de marcado que contenga más de 49 caracteres, recibirá un mensaje de error. El mensaje dirá que la directiva de buzón de mensajería unificada no se pudo generar porque el nombre del plan de marcado de mensajería unificada es demasiado largo. Esto sucede porque, cuando crea un plan de marcado, también se crea una directiva predeterminada de buzón de mensajería unificada con el nombre **Directiva predeterminada***\<nombrePlanMarcado\>*. Cuando los 15 caracteres de la directiva predeterminada se agregan al nombre del plan de marcado, los caracteres totales superan el límite. El parámetro *name* tanto para el plan de marcado de mensajería unificada como para la directiva de buzones de mensajería unificada puede tener un máximo de 64 caracteres. No obstante, si el nombre del plan de marcado tiene 49 caracteres, el nombre de la directiva de buzones de mensajería unificada tendrá más de 64 caracteres y el sistema no lo permitirá.
    
      - **Longitud de la extensión (dígitos)**   Escriba el número de dígitos para los números de extensión en el plan de marcado. El número de dígitos para números de extensión se basa en el plan de marcado de telefonía que se crea en una central de conmutación (PBX). Por ejemplo, si un usuario asociado con un plan de marcado de telefonía marca una extensión de 4 dígitos para llamar a otro usuario del mismo plan de marcado de telefonía, debe seleccionar 4 como el número de dígitos de la extensión.
        
        Este es un cuadro obligatorio que tiene un intervalo de valores entre 1 y 20. La longitud típica oscila entre 3 y 7. Si el entorno de telefonía existente incluye números de extensión, debe especificar el número de dígitos de dichas extensiones.
        
        Al crear un plan de marcado de extensión telefónica, debe escribir un número de extensión para el usuario si está vinculado a un plan de marcado de extensión telefónica. También se requiere un número de extensión con los planes de marcado de Protocolo de inicio de sesión (SIP) o E.164 cuando un usuario habilitado para mensajería unificada está vinculado a un plan de marcado de URI de SIP o E.164. El número de extensión lo usan los usuarios de Outlook Voice Access para obtener acceso al buzón de correo de Exchange.
    
      - UNRESOLVED\_TOKENBLOCK\_VAL(Tipo UI\_URI)
    
      - UNRESOLVED\_TOKENBLOCK\_VAL(Seguridad UI\_VoIP)
    
      - **Código de país o región**   Use este cuadro para escribir el código de país o región que se usará para las llamadas salientes. Este número se antepondrá automáticamente al número de teléfono que se marque. En este cuadro se pueden escribir de 1 a 4 dígitos. Por ejemplo, en Estados Unidos el código de país o región es 1. En el Reino Unido es 44.

3.  Haga clic en **Guardar**.

Si es necesario, puede crear un plan de marcado de mensajería unificada al ejecutar el siguiente comando en el Shell.

```powershell
New-UMDialplan -Name MyUMDialPlan -URIType E164 -NumberOfDigitsInExtension 5 -VoIPSecurity Secured
```

Si es necesario, puede configurar un plan de marcado existente de mensajería unificada con el EAC:

1.  En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**.

2.  En la vista de lista, seleccione el plan de marcado de mensajería unificada que desee ver o modificar y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Plan de marcado de mensajería unificada**, haga clic en **Configurar**. Use las opciones de configuración para ver la configuración específica del plan de marcado y para habilitar o deshabilitar características.

Si es necesario, puede configurar un plan existente de marcado de mensajería unificada al ejecutar el siguiente comando en el Shell.

    Set-UMDialplan -Identity MyDialPlan -AccessTelephoneNumbers 4255551234 -AudioCodec Wma -CallAnsweringRulesEnabled $false -OutsideLineAccessCode 9 -VoIPSecurity SIPSecured

Cuando implementó la mensajería unificada de Exchange 2007, tuvo que agregar un servidor de mensajería unificada a un plan de marcado de mensajería unificada para que respondiera las llamadas entrantes. Esto ya no es necesario. En Exchange 2013, los servidores de buzón y de acceso de cliente no pueden estar vinculados con una extensión telefónica o un plan de marcado E.164, sino que deben estar vinculados con planes de marcado de URI de SIP. Los servidores de buzones de correo y de acceso de cliente responderán todas las llamadas entrantes para todos los tipos de planes de marcado.

## Paso 7: Crear o configurar puertas de enlace IP existentes de mensajería unificada

Según la implementación de Exchange 2007 existente, es posible que deba crear puertas de enlace IP de mensajería unificada o que deba configurar las existentes. Si usa planes de marcado protegidos por SIP o protegidos, debe crear una puerta de enlace IP de mensajería unificada con un FQDN y usar el Shell para configurarla para que escuche en el puerto 5061. Para puertas de enlace IP existentes de mensajería unificada, compruebe que estén configuradas con un FQDN y que escuchen en el puerto 5061. Si la puerta de enlace IP de mensajería unificada no usa un FQDN, use el EAC o el Shell para cambiar la dirección. Si la puerta de enlace IP de mensajería unificada no usa el puerto 5061, use el Shell para cambiar el puerto. Puede ver la configuración de una puerta de enlace IP de mensajería unificada con el cmdlet **Get-UMIPGateway**.

Una puerta de enlace IP de mensajería unificada representa una puerta de enlace de voz sobre IP (VoIP), IP-PBX o PBX habilitada para SIP físicas. Antes de usar una puerta de enlace VoIP, IP-PBX, o PBX habilitada para SIP para responder a llamadas entrantes y enviar llamadas salientes a usuarios de correo de voz, debe crearse una puerta de enlace IP de mensajería unificada en el servicio de directorio.

La combinación de la puerta de enlace IP de mensajería unificada y un grupo de extensiones de mensajería unificada establece un vínculo entre una puerta de enlace VoIP, IP-PBX o PBX habilitada para SIP y un plan de marcado de mensajería unificada. Mediante la creación de varios grupos de extensiones de mensajería unificada, puede asociar una única puerta de enlace IP a varios planes de marcado de mensajería unificada. Para obtener más información, consulte [Puertas de enlace IP de mensajería unificada](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/connect-voice-mail-system/um-ip-gateways).

Si es necesario, puede crear una puerta de enlace IP de mensajería unificada con el EAC de la siguiente manera:

1.  En el EAC, vaya a **Mensajería unificada** \> **Puertas de enlace IP de mensajería unificada** y, a continuación, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").

2.  En la página **Nueva puerta de enlace IP de mensajería unificada**, especifique la siguiente información:
    
      - **Nombre**   Use este cuadro para especificar un nombre exclusivo para la puerta de enlace IP de mensajería unificada. Se trata de un nombre para mostrar que aparecerá en el EAC. Si debe cambiar el nombre para mostrar de la puerta de enlace IP de mensajería unificada una vez creada, primero debe eliminar la puerta de enlace IP de mensajería unificada existente y, a continuación, crear otra puerta de enlace IP de mensajería unificada con el nombre adecuado. El nombre de puerta de enlace IP de mensajería unificada es necesario, pero solo se usa para su visualización. Como la organización puede usar varias puertas de enlace IP de mensajería unificada, es recomendable el uso de nombres significativos para designar las puertas de enlace IP de mensajería unificada. La longitud máxima que puede tener un nombre de puerta de enlace IP de mensajería unificada es de 64 caracteres y puede incluir espacios. No obstante, no pueden incluirse ninguno de los caracteres siguientes: " / \\ \[ \] : ; | = , + \* ? \< \>.
    
      - **Dirección**   Puede configurar una puerta de enlace IP de mensajería unificada con una dirección IPv4 o IPv6, o un FQDN. Use este cuadro para indicar la dirección IP o el FQDN configurados en la puerta de enlace VoIP, IP-PBX o PBX habilitada para SIP. En este cuadro solo se admiten FQDN válidos y con el formato correcto.
        
        Puede escribir caracteres alfabéticos y numéricos. Se admiten direcciones IPv4, IPv6 y FQDN. Si desea usar TLS mutua entre una puerta de enlace IP de mensajería unificada y un plan de marcado que funciona en modo protegido por SIP o protegido, debe configurar la puerta de enlace IP de mensajería unificada con un FQDN. También debe configurarla para que escuche en el puerto 5061, y compruebe si se configuraron puertas de enlace VoIP o IP-PBX para escuchar las solicitudes de TLS mutua en el puerto 5061. Para configurar una puerta de enlace IP de mensajería unificada, ejecute el siguiente comando en el Shell: `Set-UMIPGateway -identity MyUMIPGateway -Port 5061`
        
        Si se usa un FQDN, debe asegurarse de que se haya configurado correctamente un registro de host DNS para la puerta de enlace VoIP, IP-PBX o PBX habilitada para SIP, de modo que el nombre del host se resuelva correctamente en una dirección IP. Asimismo, si utiliza un FQDN en lugar de una dirección IP y se modifica la configuración de DNS para la puerta de enlace IP de mensajería unificada, deberá deshabilitar la puerta de enlace IP de mensajería unificada y habilitarla después para asegurarse de que la información de configuración de dicha puerta de enlace se actualiza correctamente.
    
      - **Plan de marcado de mensajería unificada**   Haga clic en **Examinar** para seleccionar el plan de marcado de mensajería unificada que desea asociar a la puerta de enlace IP de mensajería unificada. Cuando seleccione un plan de marcado de mensajería unificada con una puerta de enlace IP de mensajería unificada, también se creará un grupo de extensiones de mensajería unificada predeterminado y se asociará con el plan de marcado de mensajería unificada seleccionado. Si no selecciona un plan de marcado de mensajería unificada, deberá crear manualmente un grupo de extensiones de mensajería unificada y, a continuación, asociar dicho grupo con una puerta de enlace IP de mensajería unificada que haya creado.

3.  Haga clic en **Guardar**.

Si es necesario, puede crear una puerta de enlace de mensajería unificada al ejecutar el siguiente comando en el Shell.

```powershell
New-UMIPGateway -Identity MyUMIPGateway -Address "MyUMIPGateway.contoso.com"
```

Si es necesario, puede configurar una puerta de enlace existente de mensajería unificada con el EAC:

1.  En el EAC, vaya a **Mensajería unificada** \> **Puertas de enlace IP de mensajería unificada** y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

2.  En la página **Puerta de enlace IP de mensajería unificada**, haga clic en **Configurar**. Use las opciones de configuración para ver la configuración específica de la puerta de enlace IP de mensajería unificada y para habilitar o deshabilitar características.

Si es necesario, puede configurar una puerta de enlace IP existente de mensajería unificada al ejecutar el siguiente comando en el Shell.

    Set-UMIPGateway -Identity MyUMIPGateway -Address fe80::39bd:88f7:6969:d223%11 -IPAddressFamily Any -Status Disabled -OutcallsAllowed $false

## Paso 8: Crear un grupo de extensiones de mensajería unificada

Según la implementación de Exchange 2007 existente, es posible que deba crear grupos de extensiones de mensajería unificada. Un grupo de extensiones de telefonía proporciona una forma de distribuir las llamadas telefónicas desde un solo número a varias extensiones o números de teléfono. En la mensajería unificada, un grupo de extensiones de mensajería unificada es una representación lógica de un grupo de extensiones de telefonía y vincula una puerta de enlace IP de mensajería unificada con un plan de marcado de mensajería unificada.

Debe tener, como mínimo, un grupo de extensiones de mensajería unificada para cada grupo de extensiones de IP PBX o PBX. Cuando finalice el siguiente procedimiento, se creará un grupo de extensiones de mensajería unificada de manera predeterminada. Si tiene más de un grupo de extensiones de IP PBX o PBX, debe crear grupos de extensiones de mensajería unificada adicionales. Para obtener más información acerca de los grupos de extensiones de mensajería unificada, consulte [Grupos de búsqueda de mensajería unificada](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/connect-voice-mail-system/um-hunt-groups).

Si es necesario, puede crear un grupo de extensiones de mensajería unificada con el EAC:

1.  En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**. En la vista de lista, seleccione el plan de marcado de mensajería unificada que desea modificar y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

2.  En la página **Plan de marcado de mensajería unificada**, en **Grupos de extensiones de mensajería unificada**, haga clic en **Nuevo**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").

3.  En la página **Nuevo grupo de extensiones de mensajería unificada**, especifique la siguiente información:
    
      - **Nombre**   Use este cuadro para crear el nombre para mostrar del grupo de extensiones de mensajería unificada. Se requiere un nombre de grupo de extensiones de mensajería unificada exclusivo, que solo se usará para mostrar en el EAC y en el Shell. Si tiene que cambiar el nombre para mostrar del grupo de extensiones después de crearlo, antes debe eliminar el grupo de extensiones existente y, a continuación, crear otro grupo de extensiones con el nombre adecuado. Si la organización usa varios grupos de extensiones, es recomendable que use nombres significativos. La longitud máxima de un nombre de grupo de extensiones de mensajería unificada es de 64 caracteres y puede incluir espacios. No obstante, no pueden incluirse ninguno de los caracteres siguientes: " / \\ \[ \] : ; | = , + \* ? \< \>.
    
      - **Puerta de enlace IP de mensajería unificada**   Use este cuadro para seleccionar una puerta de enlace IP de mensajería unificada. Este cuadro muestra el nombre de la puerta de enlace IP de mensajería unificada que se vinculará al grupo de extensiones de mensajería unificada. Para vincular una puerta de enlace IP de mensajería unificada a un grupo de extensiones de mensajería unificada, haga clic en **Examinar**.
    
      - **Identificador piloto**   Use este cuadro para especificar una cadena que identifique exclusivamente al identificador piloto configurado en la PBX o IP-PBX. Puede usar un número de extensión o un Identificador uniforme de recursos (URI) de SIP en este cuadro. Este cuadro admite caracteres alfanuméricos. Para PBX heredadas, se usa un valor numérico como identificador piloto. Sin embargo, algunas IP-PBX y PBX habilitadas para SIP pueden usar URI de SIP.

4.  Haga clic en **Guardar**.

Si es necesario, puede crear un grupo de extensiones de mensajería unificada al ejecutar el siguiente comando en el Shell.

    New-UMHuntGroup -Name MyUMHuntGroup -PilotIdentifier 5551234,55555 -UMDialPlan MyUMDialPlan -UMIPGateway MyUMIPGateway


> [!TIP]
> No puede configurar o cambiar las opciones de configuración para un grupo de extensiones de mensajería unificada. Si desea cambiar las opciones de configuración para un grupo de extensiones de mensajería unificada, debe eliminarlo y agregar un nuevo grupo de extensiones de mensajería unificada con las opciones de configuración correctas.



## Paso 9: Crear o configurar operadores automáticos de mensajería unificada

Según la implementación de Exchange 2007 existente, es posible que deba crear operadores automáticos de mensajería unificada. Puede usar operadores automáticos de mensajería unificada para crear un sistema de menú de voz que permita a quienes realizan llamadas, tanto internas como externas, usar el sistema de menú de operadores automáticos de mensajería unificada para buscar personas, realizar o transferir llamadas a los usuarios o departamentos de la empresa en una organización. Para obtener más información, consulte [Contestar y enrutar automáticamente las llamadas entrantes](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/automatically-answer-and-route-calls/automatically-answer-and-route-calls).

En implementaciones más pequeñas, es posible que solo desee implementar la mensajería unificada para que los autores de las llamadas puedan dejar correo de voz para usuarios. En estas implementaciones, la creación de un operador automático no es necesaria. Sin embargo, en la mayoría de los casos, el uso de operadores automáticos es muy útil para quienes realizan llamadas externas cuando llaman a su organización.

Si es necesario, puede crear un operador automático de mensajería unificada con el EAC de la siguiente manera:

1.  En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**. Seleccione el plan de marcado de mensajería unificada en el que desea configurar el operador automático y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

2.  En la página **Plan de marcado de mensajería unificada**, en **Operadores automáticos de mensajería unificada**, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").

3.  En la página **Nuevo operador automático de mensajería unificada**, complete las casillas siguientes:
    
      - **Nombre**   Use esta casilla para crear el nombre para mostrar del operador automático de mensajería unificada. El nombre de un operador automático de mensajería unificada es necesario y debe ser exclusivo. Sin embargo, se usa solamente para la visualización en el EAC y en el Shell. Si tiene que cambiar el nombre para mostrar del operador automático después de haberlo creado, primero deberá eliminar el operador automático de mensajería unificada existente y crear otro operador automático que tenga el nombre apropiado. Si su organización usa varios operadores automáticos de mensajería unificada, es recomendable usar nombres significativos para los operadores automáticos de mensajería unificada. La longitud máxima del nombre de un operador automático de mensajería unificada es de 64 caracteres y puede contener espacios.
        
        Aunque puede asignar un nombre que contenga espacios a un nuevo operador automático de mensajería unificada, si integra la mensajería unificada con Lync Server, el nombre del operador automático no podrá contener espacios. Por lo tanto, si ha creado un operador automático con espacios en el nombre para mostrar y está integrándolo con Lync Server, primero tendrá que eliminar el operador automático y, a continuación, crear otro que no incluya espacios en el nombre para mostrar.
    
      - **Crear este operador automático como habilitado**   Seleccione esta casilla para habilitar al operador automático para que responda las llamadas entrantes cuando termine de crear el operador automático de mensajería unificada. De forma predeterminada, los nuevos operadores automáticos se crean como deshabilitados. Si decide crear el operador automático de mensajería unificada como deshabilitado, puede usar el EAC o el Shell para habilitarlo una vez creado.
    
      - **Configurar el operador automático para responder a los comandos de voz**    Seleccione esta casilla para habilitar el operador automático de mensajería unificada para voz. Si se habilita el operador automático para voz, las personas que llamen podrán responder con entradas de voz o marcación por tonos a los mensajes de asistencia por voz personalizados o del sistema que use el operador automático de mensajería unificada. De forma predeterminada, cuando los operadores automáticos se crean, no están habilitados para voz. Para que las personas que llaman usen un operador automático habilitado para voz en otro idioma que no sea inglés de EE. UU. (en-US), debe instalar el paquete de idioma de mensajería unificada correspondiente y configurar las propiedades del operador automático para que use ese idioma. El paquete de idioma de mensajería unificada de en-US se instala de manera predeterminada al instalar un servidor de buzones de correo de Exchange 2013.
    
      - **Números de extensión**   Escriba los números de extensión o los números telefónicos que usarán las personas que llamen para establecer contacto con el operador automático. Escriba un número de extensión o un número telefónico en el cuadro y, a continuación, haga clic en **Agregar** para agregar el número a la lista. El número de dígitos del número de extensión o de teléfono que proporcione no tiene que coincidir con el número de dígitos de un número de extensión configurado en el plan de marcado de mensajería unificada asociado. El motivo es que se permiten las llamadas directas a los operadores automáticos de mensajería unificada.
        
        La cantidad de números de extensión o números de acceso que puede especificar es ilimitada. Sin embargo, puede crear el operador automático nuevo sin indicar un número de extensión o número telefónico. No es necesario un número de extensión o de teléfono. Puede editar o quitar un número de extensión existente o un identificador piloto. Para editar un número de extensión existente o un número telefónico, haga clic en **Editar**. Para quitar un número de extensión existente o un número telefónico de la lista, haga clic en **Quitar**.

4.  Haga clic en **Guardar**.

Si es necesario, puede crear un operador automático de mensajería unificada al ejecutar el siguiente comando en el Shell.

    New-UMAutoAttendant -Name MyUMAutoAttendant -UMDialPlan MyUMDialPlan -PilotIdentifierList 56000,56100 -SpeechEnabled $true -Status Enabled

Si es necesario, puede configurar un operador automático existente con el EAC:

1.  En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada** y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

2.  En la página **Plan de marcado de mensajería unificada**, bajo **Operadores automáticos de mensajería unificada**, seleccione el operador automático de mensajería unificada que desee ver o configurar y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar"). Use las opciones de configuración para ver la configuración específica del operador automático y para habilitar o deshabilitar características.

Si es necesario, puede configurar un operador automático existente al ejecutar el siguiente comando en el Shell.

    Set-UMAutoAttendant -Identity MySpeechEnabledAA -DTMFFallbackAutoAttendant MyDTMFAA -OperatorExtension 50100 -AfterHoursTransferToOperatorEnabled $true -StaroutToDialPlanEnabled $true

## Paso 10: Crear o configurar directivas de buzón de mensajería unificada

Según la implementación de Exchange 2007 existente, es posible que deba crear directivas de buzón de mensajería unificada o configurar directivas de buzón de mensajería unificada existentes. Las directivas de buzón de mensajería unificada son necesarias cuando habilita usuarios para la mensajería unificada. El buzón de cada usuario habilitado para mensajería unificada debe estar vinculado a una única directiva de buzón de mensajería unificada. Una vez creada una directiva de buzón de mensajería unificada, debe vincular uno o más buzones habilitados para mensajería unificada a la directiva de buzón de mensajería unificada. Esto permite controlar las opciones de seguridad del PIN, como el número mínimo de dígitos del PIN o el número máximo de intentos de inicio de sesión de los usuarios habilitados para mensajería unificada que están vinculados a la directiva de buzón de mensajería unificada. Para obtener más información, consulte [directivas de buzón de mensajería unificada](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/set-up-voice-mail/um-mailbox-policies).

Si es necesario, puede crear una directiva de buzón de mensajería unificada con el EAC:

1.  En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**. En la vista de lista, seleccione el plan de marcado de mensajería unificada que desea modificar y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

2.  En la página **Plan de marcado de mensajería unificada**, en **Directivas de buzón de mensajería unificada**, haga clic en **Agregar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Nueva directiva de buzón de mensajería unificada**, en el cuadro **Nombre**, escriba el nombre de la nueva directiva de buzón de mensajería unificada.
    

    > [!NOTE]
    > Use esta casilla para especificar un nombre único para la directiva de buzones de mensajería unificada. Se trata de un nombre para mostrar que aparecerá en el EAC. Si debe cambiar el nombre para mostrar de la directiva de buzones de mensajería unificada después de haberla creado, primero debe eliminar la directiva existente y, a continuación, crear otra con el nombre adecuado. No puede eliminar una directiva de buzón de mensajería unificada si algún usuario habilitado para mensajería unificada está asociado con la directiva. El nombre de la directiva de mensajería unificada es obligatorio, pero se usa únicamente con fines de visualización. Se recomienda usar nombres con un significado concreto para las directivas de buzones de mensajería unificada, ya que la organización puede usar varias directivas de este tipo. La longitud máxima de un nombre de directiva de buzones de mensajería unificada es de 64 caracteres y puede incluir espacios. No obstante, no pueden incluirse ninguno de los caracteres siguientes: " / \ [ ] : ; | = , + * ? &lt; &gt;.



4.  Haga clic en **Guardar**.
    

    > [!NOTE]
    > Cuando guarda la directiva de buzón de mensajería unificada, se habilitan todas las opciones de configuración predeterminadas, incluida la configuración de las directivas de PIN, las características de buzón de voz y el correo de voz protegido. Si desea personalizar o cambiar alguna opción predeterminada para la directiva de buzón de mensajería unificada que acaba de crear, use el cmdlet <STRONG>Set-UMMailbox</STRONG> o el EAC.



Si es necesario, puede crear una directiva de buzón de mensajería unificada en el Shell al ejecutar el siguiente comando.

```powershell
New-UMMailboxPolicy -Name MyUMMailboxPolicy -UMDialPlan MyUMDialPlan
```

Si es necesario, puede configurar una directiva de buzón existente de mensajería unificada con el EAC:

1.  En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada** y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

2.  En la página **Plan de marcado de mensajería unificada**, en **Directivas de buzón de mensajería unificada**, seleccione la directiva de buzón de mensajería unificada que desea ver o configurar y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar"). Use las opciones de configuración para ver la configuración específica de la directiva de buzón de mensajería unificada y para habilitar o deshabilitar características.

Si es necesario, puede configurar una directiva de buzón existente de mensajería unificada al ejecutar el siguiente comando en el Shell.

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -LogonFailuresBeforePINReset 8 -MaxLogonAttempts 12 -MinPINLength 8 -PINHistoryCount 10 -PINLifetime 60 -ResetPINText "The PIN used to allow you access to your mailbox using Outlook Voice Access has been reset."

## Paso 11: Mover buzones de correo existentes habilitados para mensajería unificada a Exchange 2013

En la mensajería unificada de Exchange 2007, después de habilitar los usuarios dentro de la organización para que usen correo de voz, se aplica un conjunto predeterminado de propiedades de mensajería unificada al usuario para que pueda usar características de mensajería unificada. Para obtener más información, consulte [Correo de voz para usuarios](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/run-voice-mail-call-reports/review-voice-mail-calls-for-user).

Durante el proceso de actualización, habrá un período de tiempo durante el cual tendrá buzones habilitados para mensajería unificada tanto en los servidores de buzón de Exchange 2007 como en los servidores de buzón de Exchange 2013. Sin embargo, si mueve todos los usuarios habilitados para mensajería unificada a servidores de buzón de Exchange 2013, debe usar el EAC o el cmdlet **New-MoveRequest** en el Shell de un servidor de Exchange 2013 para conservar todas las propiedades y opciones de configuración, incluido el PIN del usuario.

Una solicitud de movimiento es el proceso de movimiento de un buzón de una base de datos de buzones a otra. Una solicitud de movimiento local es una acción de movimiento de buzones que se produce dentro de un mismo bosque. Para obtener más información acerca de los movimientos de buzones de correo, consulte:

  - [Movimientos de buzones de Exchange 2013](mailbox-moves-in-exchange-2013-exchange-2013-help.md)

  - [New-MoveRequest](https://technet.microsoft.com/es-es/library/dd351123\(v=exchg.150\))

  - [New-MigrationBatch](https://technet.microsoft.com/es-es/library/jj219166\(v=exchg.150\))

  - [Mover buzones](https://go.microsoft.com/fwlink/p/?linkid=296351)

Para mover un buzón de Exchange 2007 a un servidor de buzón de Exchange 2013 con el EAC:

1.  En el EAC, vaya a **Destinatarios** \> **Migración** y, a continuación, haga clic en **Agregar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

2.  En el Asistente para **nuevo movimiento de buzón local**, seleccione el usuario que desee mover y haga clic en **Aceptar** y, a continuación, haga clic en **Siguiente**.

3.  En la página **Mover configuración** especifique un nombre para el nuevo lote. Seleccione las opciones que desee para el buzón de archivo y la ubicación de la base de datos de buzones y haga clic en **Nuevo**.

Para mover un buzón de Exchange 2007 a un servidor de buzón de Exchange 2013 con el Shell, ejecute el siguiente comando.

```powershell
New-MoveRequest -Identity 'tony@alpineskihouse.com' -TargetDatabase "DB01"
```

## Paso 12: Habilitar nuevos usuarios para mensajería unificada o configurar las opciones para un usuario existente habilitado para mensajería unificada

Un usuario debe tener un buzón para que se lo pueda habilitar para mensajería unificada. De manera predeterminada, los usuarios que tienen un buzón no están habilitados para mensajería unificada. Después de habilitar a los usuarios para mensajería unificada, podrá administrar, modificar y configurar las propiedades de mensajería unificada y las características de correo de voz para ellos. Puede habilitar un usuario para mensajería unificada mediante el EAC o el Shell. Para obtener más información, vea [Correo de voz para usuarios](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/run-voice-mail-call-reports/review-voice-mail-calls-for-user).

Cuando habilita un usuario para mensajería unificada, debe definir al menos un número de extensión que la mensajería unificada usará cuando el correo de voz se envíe al buzón del usuario y para permitir al usuario utilizar Outlook Voice Access. Una vez habilitado el usuario para mensajería unificada, se pueden agregar números de extensión secundarios para el buzón del usuario, así como modificarlos o quitarlos al configurar la dirección proxy de mensajería unificada de Exchange (EUM) en el buzón del usuario o al agregar o quitar extensiones adicionales o secundarias para el usuario en el EAC. Para agregar, modificar o quitar números de extensión, números E.164 o direcciones SIP, consulte [Procedimientos de usuario habilitado para correo de voz](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/set-up-voice-mail/voice-mail-enabled-user-procedures).

Para habilitar un usuario para mensajería unificada con el EAC:

1.  En el EAC, haga clic en **Destinatarios**.

2.  En la vista de lista, seleccione el usuario cuyo buzón desee habilitar para la mensajería unificada.

3.  En el panel de detalles, en **Características de voz y teléfono**, haga clic en **Habilitar**.

4.  En la página **Habilitar el buzón de correo de mensajería unificada**, haga clic en el botón **Explorar** al lado de la **Directiva de buzón de correo de mensajería unificada**, ubique en la lista la directiva de buzones de correo de mensajería unificada que va a asignar al usuario y luego haga clic en **Aceptar**.

5.  En la página **Habilitar el buzón de correo de mensajería unificada**, complete los siguientes campos:
    
      - **Dirección SIP o número de E.164**   Especifique la dirección SIP o el número de E.164 para el usuario. Estas opciones están disponibles si el usuario que habilitó para mensajería unificada está asignado a la directiva de buzones de correo de mensajería unificada vinculada a un plan de marcado URI de SIP o E.164. Una dirección SIP o número de E.164 no está disponible para ser agregada a un usuario si el usuario está asociado con un plan de marcado de extensión telefónica. Cuando asigna el usuario a una directiva de buzón de correo de mensajería unificada vinculada a un plan de marcado de E.164 o URI de SIP, también debe escribir un número de extensión para el usuario. El número de extensión se usa cuando los usuarios obtienen acceso al buzón con Outlook Voice Access. El número de dígitos que se configura en esta casilla debe coincidir con el número de dígitos configurados en el plan de marcado URI de SIP o E.164.
    
      - **Número de extensión**   Especifique el número de extensión para el usuario que va a habilitar para mensajería unificada.
        
        Deberá proporcionar un número de extensión válido para el usuario y deberá coincidir con el número de dígitos especificado en el plan de marcado. Solo puede escribir caracteres numéricos o dígitos del 1 al 20. El número de extensión típico es de 3 a 7 dígitos de largo. El número de dígitos en la extensión se configura en el plan de marcado que está vinculado a la directiva de buzones de correo de mensajería unificada asignada al usuario.
    
      - En **Configuración de PIN**, complete lo siguiente:
        
          - **Generar un PIN automáticamente**   Haga clic en este botón para generar de forma automática un PIN para que el usuario habilitado para mensajería unificada use el acceso al correo de voz por medio de Outlook Voice Access. Esta es la configuración predeterminada. Cuando hace clic en este botón, se genera automáticamente un PIN de acuerdo con las directivas de PIN configuradas en la directiva de buzón de correo de mensajería unificada asignada al usuario. Se recomienda utilizar esta opción para ayudar a proteger el PIN del usuario. El PIN se envía al usuario en el mensaje de bienvenida que este recibe después de su habilitación para mensajería unificada. De manera predeterminada, tendrá que cambiar este PIN la primera vez que inicie sesión en el buzón de correo para obtener el correo de voz.
        
          - **Escribir un PIN**   Haga clic en este botón para especificar de forma manual un PIN que el usuario utilizará para acceder al sistema de correo de voz. El PIN debe cumplir con las configuraciones de directivas de PIN establecidas en la directiva de buzones de correo de mensajería unificada asociada con el usuario habilitado para mensajería unificada. Por ejemplo, si la directiva de buzón de correo de mensajería unificada está configurada para aceptar solamente PIN que contengan siete o más dígitos, el PIN que escriba en este cuadro debe tener al menos siete dígitos.
        
          - **Pedir que el usuario restablezca su PIN la primera vez que inicia sesión**   Seleccione esta casilla para obligar al usuario a que restablezca su PIN de correo de voz cuando acceda por primera vez al sistema de correo de voz desde un teléfono mediante el uso de Outlook Voice Access. Se le solicitará que escriba un PIN con el que esté familiarizado. Hacer que los usuarios habilitados para mensajería unificada cambien el PIN la primera vez que inician sesión es un procedimiento recomendado de seguridad que los ayuda a protegerse contra el acceso no autorizado a sus datos y a su Bandeja de entrada. Esta casilla está activada de forma predeterminada.

6.  En la página **Habilitar el buzón de correo de mensajería unificada**, revise las configuraciones. Haga clic en **Finalizar** para habilitar al usuario para el uso de la mensajería unificada. Haga clic en **Atrás** para realizar cambios de configuración.

Para habilitar un usuario para mensajería unificada en el Shell, ejecute el siguiente comando.

    Enable-UMMailbox -Identity tonysmith@contoso.com -UMMailboxPolicy MyUMMailboxPolicy -Extensions 51234 -PIN 5643892 -NotifyEmail administrator@contoso.com -PINExpired $true

Si es necesario, puede configurar un usuario habilitado para mensajería unificada con el EAC:

1.  En el EAC, vaya a **Destinatarios** \> **Buzones**.

2.  En la vista de lista, seleccione el buzón de correo para el que desee cambiar la directiva de buzón de mensajería unificada.

3.  En el panel de detalles, bajo **Funciones de teléfono y voz** \> **Mensajería unificada**, haga clic en **Ver detalles**.

4.  En la página **Buzón de mensajería unificada**, haga clic en **Configuración de buzón de mensajería unificada** para ver o cambiar las siguientes propiedades de mensajería unificada de un usuario habilitado con mensajería unificada:
    
      - **Estado de PIN**   Este cuadro de solo visualización muestra el estado del buzón del usuario. De forma predeterminada, cuando un usuario tiene habilitada la mensajería unificada, el estado de PIN aparece como **No bloqueado**. Sin embargo, si el usuario ha escrito varias veces un PIN de Outlook Voice Access incorrecto, el estado se muestra como **Bloqueado**.
    
      - **Directiva de buzón de mensajería unificada**   Este cuadro muestra el nombre de la directiva de buzón de mensajería unificada asociada al usuario con mensajería unificada habilitada. Puede hacer clic en **Explorar** para localizar y especificar la directiva de mensajería unificada que desea asociar a este buzón de mensajería unificada.
    
      - **Extensión de operador personal**   Utilice este cuadro para especificar el número de extensión del operador para el usuario. De forma predeterminada, no está configurado un número de extensión. La longitud del número de extensión puede ser de 1 a 20 caracteres. Esto permite que las llamadas entrantes del usuario habilitado con mensajería unificada se reenvíen al número de extensión que ha especificado en este cuadro.
        
        Puede configurar otros tipos de números de extensión del operador en planes de marcado y operadores automáticos. Sin embargo, estas extensiones están generalmente destinadas a recepcionistas u operadores de toda una compañía. La opción de extensión de operador personal se puede utilizar cuando un asistente administrativo o ayudante personal responde a las llamadas entrantes para un usuario específico.

5.  En la página **Buzón de mensajería unificada**, bajo **Otras extensiones**, puede agregar, cambiar y ver los números de extensión del usuario.
    
      - Para agregar un número de extensión, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono"). En la página **Agregar otra extensión**, utilice el botón **Explorar** para seleccionar el plan de marcado de mensajería unificada y, a continuación, escriba el número de extensión en el cuadro **Número de extensión**.
    
      - Para quitar un número de extensión, seleccione el que desea quitar y, a continuación, haga clic en **Quitar**![Icono de quitar](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icono de quitar").

6.  Si realiza cualquier cambio, haga clic en **Guardar**.

Si es necesario, puede configurar un usuario habilitado para mensajería unificada en el Shell al ejecutar el siguiente comando.

    Set-UMMailbox -Identity tony@contoso.com -CallAnsweringAudioCodec Wma -CallAnsweringRulesEnabled $false -FaxEnabled $false -UMSMSNotificationOption VoiceMail

## Paso 13: Configurar las puertas de enlace VoIP, IP-PBX y PBX habilitadas para SIP para enviar todas las llamadas entrantes a los servidores de acceso de cliente de Exchange 2013

Cuando se instalan servidores de acceso de clientes y de buzones de Exchange 2013, se habilitan automáticamente para que puedan responder a las llamadas de voz entrantes y salientes, y para que enruten los mensajes de correo de voz a los destinatarios adecuados. Cuando se instalan servidores de acceso de clientes o de buzones de Exchange 2013 y se implementa la mensajería unificada, no es necesario vincular ni agregar servidores de acceso de clientes ni de buzones de Exchange 2013 a los planes de marcado de mensajería unificada. Los servidores de acceso de clientes y de buzones de Exchange 2013 responden a todas las llamadas entrantes y, a continuación, usan los planes de marcado de mensajería unificada para encontrar usuarios.

El servidor de acceso de clientes de Exchange 2013 representa el punto de entrada para las llamadas entrantes o solicitudes del protocolo de inicio de sesión (SIP) para la mensajería unificada. El servicio que se encarga de las solicitudes SIP en un servidor de acceso de cliente de Exchange 2013 es el servicio de enrutador de llamadas de mensajería unificada y se ejecuta en cada servidor de acceso de cliente de Exchange 2013 de la organización.

Cuando actualiza a la mensajería unificada de Exchange 2013, debe tener previamente instaladas y configuradas una o varias puertas de enlace VoIP para conectarse a las PBX de la red de telefonía, o instaladas y configuradas IP-PBX o PBX habilitadas para protocolo de inicio de sesión (SIP).

El último paso en el proceso de actualizar a mensajería unificada de Exchange 2013 es configurar las puertas de enlace VoIP, IP-PBX o PBX habilitadas para SIP para enviar llamadas entrantes a los servidores de acceso de cliente de Exchange 2013. (Se incluyen autores de llamadas que desean dejar un correo de voz para un usuario, llamadas de usuarios habilitados para mensajería unificada que llaman a Outlook Voice Access y llamadas de personas que llaman a un operador automático de mensajería unificada). Todas estas llamadas son recibidas primero por una puerta de enlace VoIP, IP-PBX o PBX habilitadas para SIP y luego son reenviadas a los servidores de acceso de cliente de Exchange 2013 de la organización de Exchange 2013. Para obtener más información, vea los recursos siguientes:

  -  [Servicios de mensajería unificada](um-services-exchange-2013-help.md)

  -  [Notas para la configuración de puertas de enlace de VoIP, IP PBX y PBX compatibles](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/telephone-system-integration-with-um/configuration-notes-for-voip-gateways)

  -  [Asesor de telefonía para Exchange 2013](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/telephone-system-integration-with-um/telephony-advisor-for-exchange-2013)

## Paso 14: Deshabilitar el contestador automático en un servidor de mensajería unificada de Exchange 2007

Puede deshabilitar el contestador automático al deshabilitar la mensajería unificada en un servidor de mensajería unificada de Exchange 2007 o al eliminar el servidor de mensajería unificada de un plan de marcado. Cuando deshabilita la mensajería unificada, impide que el servidor de mensajería unificada responda a las llamadas entrantes. Puede elegir entre desconectar todas las llamadas inmediatamente o esperar a que se procesen las llamadas existentes antes de deshabilitar el servidor de mensajería unificada. Querrá deshabilitar el contestador automático antes de eliminar el servidor de un plan de marcado de modo que termine de procesar todas las llamadas entrantes.

Para deshabilitar la mensajería unificada en un servidor de mensajería unificada de Exchange 2007 mediante la Consola de administración de Exchange:

1.  En el árbol de la EMC, desplácese hasta **Configuración del servidor** \> **Mensajería unificada**.

2.  En el panel de resultados, seleccione el servidor de mensajería unificada que va a deshabilitar.

3.  En el panel de acciones, haga clic en una de las siguientes opciones:
    
    1.  Cuando seleccione la opción **Deshabilitar inmediatamente**, el servidor de mensajería unificada desconectará todas las llamadas que se hayan conectado al servidor de mensajería unificada.
    
    2.  Si selecciona la opción **Deshabilitar tras terminar las llamadas**, el servidor de mensajería unificada no aceptará nuevas llamadas y no se deshabilitará hasta que se hayan procesado todas las llamadas.

4.  En el cuadro de diálogo de confirmación, haga clic en **Sí** para continuar.

Para deshabilitar la mensajería unificada en un servidor de mensajería unificada de Exchange 2007 mediante el Shell, ejecute el siguiente comando.

```powershell
Disable-UMServer -Identity MyUMServer -Immediate $true
```


> [!TIP]
> Puede usar el cmdlet <STRONG>Disable-UMServer</STRONG> desde un servidor de mensajería unificada de Exchange 2007 o el cmdlet <STRONG>Disable-UMService</STRONG> desde un servidor de buzón de Exchange 2013 para deshabilitar el contestador automático.



## Paso 15: Eliminar un servidor de mensajería unificada de Exchange 2007 de un plan de marcado

Para procesar llamadas, tendrá que agregar un servidor de mensajería unificada de Exchange 2007 a un plan de marcado de mensajería unificada como mínimo. Se puede agregar un servidor de mensajería unificada a varios planes de marcado de mensajería unificada. Puede eliminar un servidor de mensajería unificada de Exchange 2007 de un plan de marcado de mensajería unificada. Cuando elimina un servidor de mensajería unificada de un plan de marcado, el servidor de mensajería unificada deja de responder a llamadas o procesar llamadas de mensajería unificada para usuarios habilitados para mensajería unificada.

Para eliminar un servidor de mensajería unificada de Exchange 2007 de un plan de marcado mediante la Consola de administración de Exchange:

1.  En el árbol de la EMC, desplácese hasta **Configuración del servidor** \> **Mensajería unificada**.

2.  En el panel de resultados, seleccione el servidor de mensajería unificada.

3.  En el panel de acciones, haga clic en **Propiedades**.

4.  En la ficha **Configuración de mensajería unificada** en la sección **Planes de marcado asociados**, haga clic en **Quitar**.

5.  En el cuadro de diálogo de confirmación, haga clic en **Sí** para confirmar la eliminación del servidor de mensajería unificada de Exchange 2007 del plan de marcado de mensajería unificada.

6.  Haga clic en **Aceptar** para cerrar la ventana de propiedades.

Para eliminar un servidor de mensajería unificada de Exchange 2007 de un plan de marcado mediante el Shell, ejecute el siguiente comando.

    $dp= Get-UMDialPlan "MySIPDialPlan"
    $s=Get-UMServer -id MyUMServer
    $s.dialplans-=$dp.identity
    Set-UMServer -id MyUMServer -dialplans:$s.dialplans

En este ejemplo, existen tres planes de marcado de URI de SIP: SipDP1, SipDP2 y SipDP3. En este ejemplo, se elimina el servidor de mensajería unificada denominado `MyUMServer` del plan de marcado SipDP3.

```powershell
Set-UMServer -id MyUMServer -DialPlans SipDP1,SipDP2
```

En este ejemplo, existen dos planes de marcado de URI de SIP: SipDP1 y SipDP2. En este ejemplo, se elimina el servidor de mensajería unificada denominado `MyUMServer` del plan de marcado SipDP2.

```powershell
Set-UMServer -id MyUMServer -DialPlans SipDP1
```


> [!TIP]
> Puede usar el cmdlet <STRONG>Set-UMServer</STRONG> en el Shell en un servidor de mensajería unificada de Exchange 2007 o el cmdlet <STRONG>Set-UMService</STRONG> en un servidor de buzón de Exchange 2013 para eliminar un servidor de mensajería unificada de Exchange 2007 de un plan de marcado o varios planes de marcado. Por ejemplo, para eliminar un servidor de mensajería unificada de todos los planes de marcado, ejecute el siguiente comando: <CODE>Set-UMServer -identity MyUMServer -DialPlan $null</CODE>



## ¿Cómo saber si el proceso se ha completado correctamente?

Después de configurar la mensajería unificada, compruebe lo siguiente para asegurarse de que funcione correctamente:

  - Un usuario que ha habilitado para el correo de voz puede iniciar sesión en Outlook Web App u Outlook y ver el mensaje de bienvenida para la mensajería unificada.

  - Los usuarios de mensajería unificada pueden recibir mensajes de voz.

  - Los usuarios de mensajería unificada pueden llamar a un número de Outlook Voice Access para escuchar el correo electrónico, los elementos de calendario y el correo de voz.

  - La mensajería unificada enruta llamadas desde afuera de la organización, y usted puede realizar una llamada.

