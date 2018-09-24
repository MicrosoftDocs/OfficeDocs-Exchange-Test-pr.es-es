---
title: 'Actualizar la mensajería unificada (UM) de Exchange 2010 a la mensajería unificada de Exchange 2013: Exchange 2013 Help'
TOCTitle: Actualizar la mensajería unificada (UM) de Exchange 2010 a la mensajería unificada de Exchange 2013
ms:assetid: 01aa5dab-689b-4738-afab-0d2f11a60b39
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn169226(v=EXCHG.150)
ms:contentKeyID: 54652427
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Actualizar la mensajería unificada (UM) de Exchange 2010 a la mensajería unificada de Exchange 2013

 

_**Se aplica a:** Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2016-12-09_

Al actualizar una organización de Microsoft Exchange 2010 con Mensajería unificada (UM) a Mensajería unificada de Exchange 2013, hay algunos pasos que se deben llevar a cabo y otros que ya se completaron al implementar Mensajería unificada de Exchange 2010. En función del entorno de telefonía y de los componentes de UM que se crearon y configuraron para admitir Mensajería unificada en Exchange 2010, puede que tenga que implementar equipos de telefonía adicionales, como puertas de enlace de voz sobre IP (VoIP), centrales de conmutación (PBX) de IP o PBX tradicionales o con SIP habilitado, y luego crear y configurar los componentes de UM necesarios para Mensajería unificada de Exchange 2013.

## ¿Qué necesito saber antes de empezar?

  - Tiempo estimado para finalizar esta tarea: 45-90 minutos.

  - Compruebe que tiene los permisos apropiados en la organización de Exchange 2010 y Exchange 2013 para crear y configurar todos los componentes necesarios.

  - Compruebe si ha implementado y ha configurado los componentes telefónicos, incluyendo puertas de enlace VoIP y PBX, IP PBX o PBX habilitadas para Protocolo de inicio de sesión (SIP).

  - Compruebe que instaló y configuró correctamente los servidores de acceso de cliente que ejecutan el servicio de enrutador de llamadas de mensajería unificada de Microsoft Exchange (enrutador de llamadas de UM) y los servidores de buzones de correo que ejecutan el servicio de mensajería unificada (UM) de Microsoft Exchange. Para más información sobre los servicios de Mensajería unificada, vea [Servicios de mensajería unificada](um-services-exchange-2013-help.md).
    

    > [!WARNING]
    > Debe implementar al menos un servidor de buzones de Exchange 2013 en su organización antes de configurar las puertas de enlace VoIP o las centrales de conmutación (PBX) de IP para enviar protocolos de inicio de sesión (SIP) de UM y tráfico RTP a los servidores de acceso de cliente de Exchange 2013.



  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Cómo realiza esto?

## Paso 1: Descargar e instalar los paquetes de idioma de mensajería unificada requeridos

Los paquetes de idioma de mensajería unificada permiten a las personas que llaman y a los usuarios de Outlook Voice Access interactuar con el sistema de correo de voz en varios idiomas. Tras instalar un idioma adicional en un servidor de buzones de correo de Exchange 2013, las personas que llaman y los usuarios de Outlook Voice Access podrán escuchar mensajes de correo electrónico e interactuar con el sistema de correo de voz en dicho idioma. Sin embargo, para hacer que el idioma esté disponible para todas las llamadas entrantes, debe instalar los paquetes necesarios de idiomas de mensajería unificada en todos los servidores de buzón de Exchange 2013. Esto se debe a que cada servidor de buzón de Exchange 2013 puede responder llamadas entrantes para mensajería unificada.

De manera predeterminada, al instalar un servidor de buzones de correo de Exchange 2013, se instala el paquete de idioma de inglés de Estados Unidos (en-US). Es la única opción de idioma disponible para el plan de marcado a menos que instale otro paquete de idioma de mensajería unificada. (No se puede eliminar el paquete de idioma de inglés de EE. UU. a no ser que elimine el servidor de buzones del equipo). Tras instalar un paquete de idioma de mensajería unificada en un servidor de buzón de correo de Exchange 2013, el idioma asociado al paquete de idioma también aparecerá como opción disponible al configurar el idioma predeterminado del plan de marcado. De manera predeterminada, como un operador automático de mensajería unificada se vincula a un plan de marcado de mensajería unificada cuando se crea, usa la configuración de idioma predeterminada del plan de marcado de mensajería unificada al que está vinculado. Sin embargo, es posible cambiar esta configuración después de crear el operador automático de mensajería unificada.


> [!NOTE]
> Si el inglés de EE. UU. es el único idioma que quiere poner en el plan de marcado, puede omitir este paso e ir al paso 2.



Puede agregar paquetes de idioma de mensajería unificada (UM) usando el comando setup.exe o ejecutando el programa de instalación *\<UMLanguagePack\>*.exe después de bajar el paquete de idioma de mensajería unificada (UM) de [Exchange Server 2013 UM Language Packs - Español](https://go.microsoft.com/fwlink/p/?linkid=266542). Para más información, vea [Instalar un paquete de idioma de mensajería unificada](install-a-um-language-pack-exchange-2013-help.md).

En este ejemplo se usa setup.exe para instalar el paquete de idioma de mensajería unificada del japonés (ja-JP).

```powershell
setup.exe /AddUmLanguagePack:ja-JP /s:d:\Exchange\UMLanguagePacks /IAcceptExchangeServerLicenseTerms
```

## Paso 2: Mover el buzón del sistema de Exchange 2010 que se usa para saludos personalizados, anuncios, menús y avisos a Exchange 2013

Los operadores automáticos y los planes de marcado de Mensajería unificada usan saludos personalizados, anuncios, menús y avisos. El buzón del sistema denominado {e0dc1c29-89c3-4034-b678-e6c29d823ed9} se crea cuando instala Exchange 2010 o Exchange 2013, y se usa para admitir características como la aprobación de mensajes y la búsqueda en varios buzones de correo. El buzón del sistema también se usa para almacenar saludos personalizados, anuncios, menús y avisos de planes de marcado y operadores automáticos. Si el buzón del sistema no existe, puede usar el comando **Setup /PrepareAD** para crearlo.

De manera predeterminada, los buzones del sistema no están visibles en el Centro de administración de Exchange (EAC). Puede ver la lista de los buzones del sistema ejecutando uno de los comandos siguientes:

Este comando devuelve una lista de todos los buzones de correo del sistema.

```powershell
Get-Mailbox -Arbitration
```

Este comando devuelve la lista de los buzones del sistema y sus propiedades o configuraciones individuales.

```powershell
Get-Mailbox -Arbitration |fl
```

Al usar este buzón del sistema, se puede hacer una copia de seguridad de saludos personalizados, anuncios, menús y avisos con otros buzones de una base de datos; estos elementos también se pueden restaurar. De este modo, la cantidad de recursos necesarios se reduce. Almacenar saludos personalizados, anuncios, menús y avisos en un buzón del sistema elimina las posibles incoherencias que puedan haber surgido. Para más información sobre los movimientos de buzones, vea [Movimientos de buzones de Exchange 2013](mailbox-moves-in-exchange-2013-exchange-2013-help.md).

## Opcional: Exportar e importar manualmente saludos personalizados, anuncios, menús y avisos de planes de marcado y operadores automáticos

En algunos casos puede que el buzón del sistema de Exchange 2010 se haya movido, pero aún necesita exportar e importar los saludos personalizados, anuncios, menús y avisos que se usan con los planes de marcado de mensajería unificada y los operadores automáticos del buzón desde el sistema de Exchange 2010 al buzón del sistema de Exchange 2013. El buzón del sistema tiene el nombre {e0dc1c29-89c3-4034-b678-e6c29d823ed9} en ambas versiones.

Los saludos personalizados, anuncios, menús y avisos son archivos de audio (en formato .wav o .wma) que la mensajería unificada (UM) usa con varios fines:

  - En los planes de marcado de mensajería unificada (UM), los archivos de audio se usan para saludos de bienvenida personalizados y anuncios informativos. Se reproducen cuando los usuarios de Outlook Voice Access llaman a un número de Outlook Voice Access.

  - En los operadores automáticos de mensajería unificada (UM), los archivos de audio se usan para saludos personalizados dentro o fuera del horario comercial, anuncios informativos, avisos de menús y menús de navegación. Se reproducen cuando los llamadores llaman a un operador automático de mensajería unificada (UM).

Al exportar e importar saludos personalizados, anuncios, menús y avisos de Exchange 2010 a Exchange 2013, hay que usar los cmdlets **Export-UMPrompt** y **Import-UMPrompt**. No se puede usar el EAC para exportar o importar avisos personalizados. En un servidor de Exchange 2010, use el cmdlet **Export-UMPrompt** para exportar los avisos del operador automático y el plan de marcado de Exchange 2010. Después de exportar los avisos, puede importarlos al servidor de buzones de Exchange 2013. Al ejecutar el cmdlet **Export-UMPrompt** desde el servidor de Exchange 2010, el comando hace una búsqueda de GUID o identificador de objeto para el plan de marcado o el operador automático en Active Directory y lo consulta para saber si hay saludos personalizados, anuncios, menús o avisos. Si los hay, los saludos personalizados, anuncios, menús o avisos se guardarán en el directorio que indique. Después de exportar todos los saludos personalizados, anuncios, menús y avisos, use el cmdlet **Import-UMPrompt** para importar los avisos al buzón del sistema de Exchange 2013.

En este ejemplo se exporta el saludo de bienvenida del plan de marcado de mensajería unificada (UM) `MyUMDialPlan` y se guarda en el archivo `welcomegreeting.wav`.

```powershell
$prompt = Export-UMPrompt -PromptFileName "customgreeting.wav" -UMDialPlan MyUMDialPlan
set-content -Path "d:\DialPlanPrompts\welcomegreeting.wav" -Value $prompt.AudioData -Encoding Byte
```

En este ejemplo se importa el saludo de bienvenida `welcomegreeting.wav` desde d:\\UMPrompts al plan de marcado de mensajería unificada (UM) `MyUMDialPlan`.

```powershell
[byte[]]$c = Get-content -Path "d:\UMPrompts\welcomegreeting.wav" -Encoding Byte -ReadCount 0
Import-UMPrompt -UMDialPlan MyUMDialPlan -PromptFileName "welcomegreeting.wav" -PromptFileData $c
```

En este ejemplo se exporta un saludo personalizado para el operador automático de mensajería unificada (UM) `MyUMAutoAttendant` y se guarda en el archivo `welcomegreetingbackup.wav`.

```powershell
Export-UMPrompt -PromptFileName "welcomegreeting.wav" -UMAutoAttendant MyUMAutoAttendant
set-content -Path "e:\UMPromptsBackup\welcomegreeting.wav" -Value $prompt.AudioData -Encoding Byte
```

En este ejemplo se importa el saludo de bienvenida `welcomegreeting.wav` desde d:\\UMPrompts al operador automático de mensajería unificada (UM) `MyUMAutoAttendant`.

```powershell
[byte[]]$c = Get-content -Path "d:\UMPrompts\welcomegreeting.wav" -Encoding Byte -ReadCount 0
Import-UMPrompt -UMAutoAttendant MyUMAutoAttendant -PromptFileName "welcomegreeting.wav" -PromptFileData $c
```

Para más información sobre los avisos personalizados de mensajería unificada (M), vea:

  - [Importar y exportar saludos personalizados, anuncios, menús y avisos](import-and-export-custom-greetings-announcements-menus-and-prompts-exchange-2013-help.md)

  - [Import-UMPrompt](https://technet.microsoft.com/es-es/library/dd876899\(v=exchg.150\))

  - [Export-UMPrompt](https://technet.microsoft.com/es-es/library/dd876882\(v=exchg.150\))

  - [Idiomas, mensajes y saludos de mensajería unificada](um-languages-prompts-and-greetings-exchange-2013-help.md)

## Paso 4: Exportar e importar certificados

Si usa planes de marcado en el modo "SIP protegida" o "Protegida" en la organización de Exchange 2010, tendrá que exportar e importar a los servidores de acceso de cliente y de buzones de Exchange 2013 los certificados que se usaron. La Seguridad de la capa de transporte mutua (TLS mutua) se usa para cifrar los datos enviados entre los servidores de Exchange 2013 y las puertas de enlace de VoIP, las IP PBX y las PBX con SIP habilitado. Los certificados enlazan la identidad del propietario del certificado con un par de claves electrónicas (pública y privada) que se usan para cifrar y firmar la información digitalmente. En los servicios de mensajería unificada (UM) y de enrutador de llamadas de UM, puede usar uno de los certificados siguientes:

  - Un certificado autofirmado (de Exchange)

  - Un certificado de infraestructura de clave pública (PKI) interno

  - Un certificado comercial de otros fabricantes

De manera predeterminada, cuando instala Exchange 2013, se crean dos certificados autofirmados: **Certificado de autenticación de Microsoft Exchange Server** y **Microsoft Exchange**. El certificado autofirmado de **Microsoft Exchange** puede usarse para que la mensajería unificada cifre datos, pero usted debe asignar el certificado a los servicios de enrutador de llamadas de mensajería unificada y de mensajería unificada. Este certificado autofirmado se puede copiar y luego importar en las puertas de enlace VoIP, IP-PBX e IP-PBX habilitadas para SIP. Sin embargo, no se puede usar cuando integra mensajería unificada con Microsoft Lync Server.

Para que la mensajería unificada (UM) pueda cifrar los datos enviados entre los servidores de Exchange 2013 y las puertas de enlace VoIP, las IP PBX y las PBX con SIP habilitado, hay que hacer lo siguiente:

  - Use un certificado autofirmado existente de mensajería unificada (UM), cree un certificado autofirmado de Exchange, envíe una solicitud de certificado de PKI a una autoridad de certificación interna o compre un certificado comercial de otro proveedor que pueda usar para la TLS mutua entre los servidores de buzones y de acceso de cliente de Exchange 2013, y las puertas de enlace de VoIP, las IP PBX y las PBX con SIP habilitado.
    
    Para crear un certificado autofirmado de Exchange desde el EAC:
    
    1.  En el EAC, vaya a **Servidores** \> **Certificados** y, a continuación, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").
    
    2.  En la página **Nuevo certificado de Exchange**, elija **Crear un certificado autofirmado** y seleccione **Siguiente**.
    
    3.  Escriba un nombre descriptivo para el certificado y seleccione **Siguiente**.
    
    4.  Haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") para seleccionar los servidores de Exchange que quiera aplicar al certificado y luego seleccione **Siguiente**.
    
    5.  Especifique los dominios que desee incluir en el certificado y, a continuación, seleccione **Siguiente**. Si desea agregar un dominio para un servicio, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").
    
    6.  Compruebe que los nombres de los dominios incluidos sean correctos y luego seleccione **Finalizar**.
    

    > [!IMPORTANT]
    > Cuando use el EAC para crear un certificado, no se le solicitará que habilite los servicios para el certificado. Tras la creación del certificado, puede usar el EAC para habilitar los servicios. Para obtener más información acerca de cómo habilitar un certificado para servicios, consulte <A href="assign-a-certificate-to-the-um-and-um-call-router-services-exchange-2013-help.md">Asignar un certificado a los servicios de mensajería unificada y llamar al enrutador de mensajería unificada</A>.

    
    Cree un certificado autofirmado de Exchange al ejecutar el siguiente comando en el Shell.
    
    ```powershell
    New-ExchangeCertificate -Services 'UM, UMCallRouter' -DomainName '*.northwindtraders.com' -FriendlyName 'UMSelfSigned' -SubjectName 'C=US,S=WA,L=Redmond,O=Northwindtraders,OU=Servers,CN= Northwindtraders.com' -PrivateKeyExportable $true
    ```
    

    > [!NOTE]
    > Si especifica los servicios que quiere habilitar usando el parámetro <EM>Services</EM>, se le pedirá que habilite los servicios para el certificado que creó. En este ejemplo, se le pide que habilite el certificado para los servicios Mensajería unificada y Enrutador de llamadas de mensajería unificada. Para más información sobre cómo habilitar un certificado para servicios, vea <A href="assign-a-certificate-to-the-um-and-um-call-router-services-exchange-2013-help.md">Asignar un certificado a los servicios de mensajería unificada y llamar al enrutador de mensajería unificada</A>.



  - Importe el certificado que se usará en todos los servidores de acceso de cliente y de buzones de Exchange 2013 en la organización. Si usa el certificado autofirmado de Exchange 2013, tiene que copiar el certificado e importarlo a las puertas de enlace de VoIP, a las IP PBX o a las PBX con SIP habilitado. Si usa el certificado autofirmado de Exchange 2010, el nombre alternativo del firmante (SAN) debe contener los nombres de las máquinas de todos los servidores de Exchange 2013. Si tiene servidores de Mensajería unificada de Exchange 2010 en la organización, puede usar el certificado autofirmado de Exchange 2013, pero tiene que agregar los nombres de las máquinas de los servidores de mensajería unificada (UM) de Exchange 2010 al SAN en el certificado de Exchange 2013.

  - Habilite o asigne el certificado que se usará a los servicios Mensajería unificada o Enrutador de llamadas de mensajería unificada en los servidores de acceso de cliente y buzones de la organización.
    
    Habilite el servicio Mensajería unificada y el servicio Enrutador de llamadas de mensajería en todos los servidores de Exchange 2013 que usarán el certificado autofirmado de Exchange desde el EAC como se detalla a continuación:
    
    1.  En el EAC, vaya a **Servidores** \> **Certificados**, seleccione el certificado en el que quiere habilitar los servicios y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").
    
    2.  En la página **Procedimiento**, seleccione **Servicios**, **Mensajería unificada** y **Enrutador de llamadas de mensajería unificada**.
    
    Habilite un certificado autofirmado de Exchange ejecutando el comando siguiente en el Shell.
    
    ```powershell
    Enable-ExchangeCertificate -Thumbprint 5113ae0233a72fccb75b1d0198628675333d010e -Services 'UM, UMCallRouter'
    ```

  - Configure los planes de marcado nuevos o existentes de mensajería unificada (UM) en el modo "SIP protegida" o "Protegida".

  - Configure el modo de inicio de la mensajería unificada en los servidores de acceso de cliente y de buzones en su organización.

  - Cree y configure puertas de enlace IP de mensajería unificada nuevas o existentes con un nombre de dominio completo (FQDN).

  - Configure el puerto de escucha en las puertas de enlace IP de mensajería unificada para usar el puerto 5061 TLS.

  - Reinicie el servicio Enrutador de llamadas de mensajería unificada en todos los servidores de acceso de cliente de Exchange 2013 y reinicie el servicio Mensajería unificada en todos los servidores de buzones de Exchange 2013. Para más información sobre los servicios de Mensajería unificada, vea [Servicios de mensajería unificada](um-services-exchange-2013-help.md).

## Paso 5: Configurar el modo de inicio de Mensajería unificada en todos los servidores de acceso de cliente de Exchange 2013

Si usa planes de marcado de tipo "SIP protegida" o "Protegida", tiene que configurar el modo de inicio de Mensajería unificada en los servidores de acceso de cliente de Exchange 2013. Puede indicar el modo de inicio de Mensajería unificada para el servicio Enrutador de llamadas de mensajería unificada en un servidor de acceso de cliente de Exchange 2013 usando el EAC o el Shell de administración de Exchange. De manera predeterminada, el servidor de acceso de cliente se iniciará en el modo TCP, pero si usa Seguridad de la capa de transporte (TLS) para cifrar el tráfico de Voz sobre IP (VoIP), debe configurar el servidor de acceso de cliente de Exchange 2013 para que use el modo Dual o TLS. Le recomendamos configurar los servidores de acceso de cliente de Exchange 2013 para que usen Dual como modo de inicio. Esto se debe a que los servidores de acceso de cliente de Exchange 2013 pueden responder a las llamadas entrantes de todos los planes de marcado de mensajería unificada, y estos planes de marcado pueden tener configuraciones de seguridad de distintas. Si cambia el modo de inicio de Mensajería unificada, debe reiniciar el servicio Enrutador de llamadas de mensajería unificada para que el cambio surta efecto. Para más información sobre los servicios de Mensajería unificada, vea [Servicios de mensajería unificada](um-services-exchange-2013-help.md).

Para configurar el modo de inicio de Mensajería unificada en un servidor de acceso de cliente de Exchange 2013 desde el EAC:

1.  En el EAC, desplácese hasta **Servidores** \> **Servidores**.

2.  En la vista de lista, seleccione el servidor de Exchange que desea modificar y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Exchange Server**, haga clic en **Mensajería unificada**.

4.  En **Configuración de enrutador de llamadas de mensajería unificada** \> **Modo de inicio de mensajería unificada**, seleccione una de las siguientes opciones de la lista desplegable:
    
      - **TCP**: elija esta opción si no tiene mTLS y solo usa planes de marcado de tipo "No protegido".
    
      - **TLS**: elija esta opción si tiene mTLS y solo usa planes de marcado de tipo "SIP protegida" o "Protegida".
    
      - **DUAL**: elija esta opción si tiene mTLS y usa planes de marcado de tipo "No protegido", "SIP protegida" y "Protegida"

5.  Después de seleccionar el modo de inicio de mensajería unificada, haga clic en **Guardar**.

Configure el modo de inicio de Mensajería unificada en un servidor de acceso de cliente de Exchange 2013 ejecutando el siguiente comando en el Shell.

```powershell
Set-UMCallRouterSettings -Server MyUMCallRouter.northwindtraders.com -UMStartupMode Dual
```

## Paso 6: Configurar el modo de inicio de Mensajería unificada en todos los servidores de buzones de Exchange 2013

Si usa planes de marcado de tipo "SIP protegida" o "Protegida", tiene que configurar el modo de inicio de Mensajería unificada en los servidores de buzones de Exchange 2013. Puede indicar el modo de inicio de Mensajería unificada para el servicio Mensajería unificada en un servidor de buzones de Exchange 2013 usando el EAC o el Shell. De manera predeterminada, un servidor de buzones de Exchange 2013 se iniciará en el modo TCP, pero si usa Seguridad de la capa de transporte (TLS) para cifrar el tráfico de voz sobre IP (VoIP), debe configurar el servidor de buzones de Exchange 2013 para que use el modo Dual o TLS. Le recomendamos que configure todos los servidores de buzones de Exchange 2013 para que usen Dual como modo de inicio. Esto se debe a que los servidores de buzones de Exchange 2013 pueden responder a las llamadas entrantes de todos los planes de marcado de mensajería unificada, y estos planes de marcado pueden tener configuraciones de seguridad de distintas. Si cambia el modo de inicio de Mensajería unificada, debe reiniciar el servicio Mensajería unificada para que el cambio surta efecto. Para más información sobre los servicios de Mensajería unificada, vea [Servicios de mensajería unificada](um-services-exchange-2013-help.md).

Configure el modo de inicio de mensajería unificada en un servidor de buzones de Exchange 2013 mediante el EAC de la siguiente manera:

1.  En el EAC, desplácese hasta **Servidores** \> **Servidores**.

2.  En la vista de lista, seleccione el servidor de Exchange que desea modificar y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Exchange Server**, haga clic en **Mensajería unificada**.

4.  En **Configuración del servicio de mensajería unificada** \> **Modo de inicio de mensajería unificada**, seleccione una de las siguientes opciones de la lista desplegable:
    
      - **TCP**: elija esta opción si no tiene mTLS y solo usa planes de marcado de tipo "No protegido".
    
      - **TLS**: elija esta opción si tiene mTLS y solo usa planes de marcado de tipo "SIP protegida" o "Protegida".
    
      - **DUAL**: elija esta opción si tiene mTLS y usa planes de marcado de tipo "No protegido", "SIP protegida" y "Protegida"

5.  Después de seleccionar el modo de inicio de mensajería unificada, haga clic en **Guardar**.

Configure el modo de inicio de Mensajería unificada en un servidor de buzones de Exchange 2013 ejecutando el siguiente comando en el Shell.

```powershell
Set-UMService -Identity MyUMServer -ExternalHostFqdn host.external.contoso.com -IPAddressFamily Any -UMStartupMode Dual
```

## Paso 7: Crear planes de marcado de Mensajería unificada o configurar los existentes

En función de la implementación de Exchange 2010 actual, puede ser necesario crear planes de marcado de Mensajería unificada o configurar los ya existentes. Un plan de marcado de mensajería unificada representa un conjunto de centrales de conmutación (PBX) tradicionales, con SIP habilitado o IP PBX que comparten números de extensión de usuarios comunes. Todas las extensiones de usuarios hospedadas en PBX tradicionales, con SIP habilitado o IP PBX en un plan de marcado contienen la misma cantidad de dígitos. Los usuarios pueden marcar otra extensión de teléfono sin tener que anexar un número especial a la extensión ni marcar un número de teléfono completo.

Los planes de marcado de mensajería unificada se usan en la mensajería unificada para garantizar que las extensiones telefónicas de los usuarios sean únicas. En algunas redes de telefonía, pueden existir varias PBX o IP PBX. En estas redes de telefonía, puede haber dos usuarios que tengan el mismo número de extensión telefónica. Los planes de marcado de Mensajería unificada resuelven esta situación. Al poner a dos usuarios en dos planes de marcado de Mensajería unificada distintos, las extensiones son únicas. Para más información, vea [Planes de marcado de mensajería unificada](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/connect-voice-mail-system/um-dial-plans).

Si es necesario, puede crear un plan de marcado de Mensajería unificada desde el EAC:

1.  En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada** y haga clic en **Nuevo**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").

2.  En la página **Nuevo plan de marcado de mensajería unificada**, rellene los siguientes cuadros:
    
      - **Nombre**: escriba el nombre del plan de marcado. El nombre del plan de marcado de mensajería unificada es obligatorio y debe ser único, pero solo se verá el EAC y en el Shell. La longitud máxima del nombre del plan de marcado de mensajería unificada es de 64 caracteres y puede incluir espacios. No puede incluir ninguno de los caracteres siguientes: " / \\ \[ \] : ; | = , + \* ? \< \>.
        
        Aunque en el cuadro del nombre del plan de marcado se pueden escribir hasta 64 caracteres, el nombre no debe tener más de 49 caracteres. Si intenta crear un nombre de plan de marcado que contenga más de 49 caracteres, recibirá un mensaje de error. En el mensaje pondrá que la directiva de buzones de Mensajería unificada no se pudo generar porque el nombre del plan de marcado de Mensajería unificada es demasiado largo. Esto sucede porque, al crear un plan de marcado, también se crea una directiva de buzones de mensajería unificada predeterminada que se llama **Directiva predeterminada de***\<DialPlanName\>*. Cuando los 15 caracteres de la directiva predeterminada se agregan al nombre del plan de marcado, el total de caracteres supera el límite. El parámetro *name* puede tener un máximo de 64 caracteres tanto para el plan de marcado de Mensajería unificada como para la directiva de buzones de Mensajería unificada. Sin embargo, si el nombre del plan de marcado tiene más de 49 caracteres, el nombre de la directiva de buzones de Mensajería unificada tendrá más de 64 caracteres y el sistema no lo permitirá.
    
      - **Longitud de la extensión (dígitos)**: escriba el número de dígitos para los números de extensión del plan de marcado. El número de dígitos de los números de extensión depende del plan de marcado de telefonía que se crea en una PBX. Por ejemplo, si un usuario asociado con un plan de marcado de telefonía marca una extensión de 4 dígitos para llamar a otro usuario del mismo plan de marcado de telefonía, hay que seleccionar 4 como el número de dígitos de la extensión.
        
        Este es un cuadro obligatorio que tiene un intervalo de valores entre 1 y 20. La longitud típica oscila entre 3 y 7. Si el entorno de telefonía existente incluye números de extensión, debe especificar el número de dígitos de dichas extensiones.
        
        Al crear un plan de marcado de extensión telefónica, debe escribir un número de extensión para el usuario si está vinculado a un plan de marcado de extensión telefónica. También se requiere un número de extensión con los planes de marcado de Protocolo de inicio de sesión (SIP) o E.164 cuando un usuario habilitado para mensajería unificada está vinculado a un plan de marcado de URI de SIP o E.164. El número de extensión lo usan los usuarios de Outlook Voice Access para obtener acceso al buzón de correo de Exchange.
    
      - UNRESOLVED\_TOKENBLOCK\_VAL(Tipo UI\_URI)
    
      - UNRESOLVED\_TOKENBLOCK\_VAL(Seguridad UI\_VoIP)
    
      - **Código de país o región**   Use este cuadro para escribir el código de país o región que se usará para las llamadas salientes. Este número se antepondrá automáticamente al número de teléfono que se marque. En este cuadro se pueden escribir de 1 a 4 dígitos. Por ejemplo, en Estados Unidos el código de país o región es 1. En el Reino Unido es 44.

3.  Haga clic en **Guardar**.

Si es necesario, puede crear un plan de marcado de Mensajería unificada ejecutando el comando siguiente en el Shell.

```powershell
New-UMDialplan -Name MyUMDialPlan -URIType E164 -NumberOfDigitsInExtension 5 -VoIPSecurity Secured
```

Si es necesario, puede configurar un plan de marcado existente de Mensajería unificada desde el EAC del modo siguiente:

1.  En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**.

2.  En la vista de lista, seleccione el plan de marcado de mensajería unificada que desee ver o modificar y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Plan de marcado de mensajería unificada**, haga clic en **Configurar**. Use las opciones de configuración para ver configuraciones concretas del plan de marcado y habilitar o deshabilitar características.

Si es necesario, puede configurar un plan de marcado existente de Mensajería unificada usando el Shell:

```powershell
Set-UMDialplan -Identity MyDialPlan -AccessTelephoneNumbers 4255551234 -AudioCodec Wma -CallAnsweringRulesEnabled $false -OutsideLineAccessCode 9 -VoIPSecurity SIPSecured
```

Cuando implementó Mensajería unificada de Exchange 2010, tuvo que agregar un servidor de Mensajería unificada a un plan de marcado de UM para que respondiese a las llamadas entrantes. Esto ya no es necesario. En Exchange 2013, los servidores de acceso de cliente y de buzones no se pueden vincular con planes de marcado de extensión telefónica ni E.164, sino que se deben vincular a planes de marcado URI de SIP. Los servidores de buzones y de acceso de cliente responderán a todas las llamadas entrantes en todos los tipos de planes de marcado.

## Paso 8: Crear puertas de enlace IP de Mensajería unificada o configurar las existentes

En función de la implementación de Exchange 2010 actual, puede ser necesario crear puertas de enlace IP de Mensajería unificada o configurar las existentes. Si usa planes de marcado de tipo "SIP protegida" o "Protegida", debe crear una puerta de enlace IP de Mensajería unificada con un FQDN y usar el Shell para configurarla de modo que escuche en el puerto 5061. Para puertas de enlace IP de Mensajería unificada existentes, compruebe que estén configuradas con un FQDN y que escuchen en el puerto 5061. Si la puerta de enlace IP de Mensajería unificada no usa un FQDN, use el EAC o el Shell para cambiar la dirección. Si la puerta de enlace IP de Mensajería unificada no usa el puerto 5061, cambie el puerto con el Shell. Puede ver la configuración de una puerta de enlace IP de Mensajería unificada usando el cmdlet **Get-UMIPGateway**.

Una puerta de enlace IP de UM representa una puerta de enlace de voz sobre IP (VoIP), una IP PBX o una PBX con SIP habilitado físicas. Antes de usar una puerta de enlace VoIP, IP PBX, o PBX con SIP habilitado para responder a llamadas entrantes y enviar llamadas salientes a usuarios de correo de voz, debe crearse una puerta de enlace IP de UM en el servicio de directorio.

La combinación de la puerta de enlace IP de mensajería unificada y un grupo de extensiones de mensajería unificada establece un vínculo entre una puerta de enlace VoIP, IP-PBX o PBX habilitada para SIP y un plan de marcado de mensajería unificada. Mediante la creación de varios grupos de extensiones de mensajería unificada, puede asociar una única puerta de enlace IP a varios planes de marcado de mensajería unificada. Para obtener más información, consulte [Puertas de enlace IP de mensajería unificada](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/connect-voice-mail-system/um-ip-gateways).

Si es necesario, puede crear una puerta de enlace IP de mensajería unificada con el EAC de la siguiente manera:

1.  En el EAC, vaya a **Mensajería unificada** \> **Puertas de enlace IP de mensajería unificada** y, a continuación, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").

2.  En la página **Nueva puerta de enlace IP de mensajería unificada**, especifique la siguiente información:
    
      - **Nombre**   Use este cuadro para especificar un nombre exclusivo para la puerta de enlace IP de mensajería unificada. Se trata de un nombre para mostrar que aparecerá en el EAC. Si debe cambiar el nombre para mostrar de la puerta de enlace IP de mensajería unificada una vez creada, primero debe eliminar la puerta de enlace IP de mensajería unificada existente y, a continuación, crear otra puerta de enlace IP de mensajería unificada con el nombre adecuado. El nombre de puerta de enlace IP de mensajería unificada es necesario, pero solo se usa para su visualización. Como la organización puede usar varias puertas de enlace IP de mensajería unificada, es recomendable el uso de nombres significativos para designar las puertas de enlace IP de mensajería unificada. La longitud máxima que puede tener un nombre de puerta de enlace IP de mensajería unificada es de 64 caracteres y puede incluir espacios. No obstante, no pueden incluirse ninguno de los caracteres siguientes: " / \\ \[ \] : ; | = , + \* ? \< \>.
    
      - **Dirección**: puede configurar una puerta de enlace IP de UM con un FQDN o con una dirección IPv4 o IPv6. Indique aquí la dirección IP o el FQDN configurados en la puerta de enlace VoIP, la IP PBX o la PBX con SIP habilitado. En este cuadro solo se admiten FQDN válidos y con el formato correcto.
        
        Puede escribir caracteres alfabéticos y numéricos. Se admiten direcciones IPv4 e IPv6, así como FQDN. Si desea usar TLS mutua entre una puerta de enlace IP de mensajería unificada y un plan de marcado en modo "SIP protegida" o "Protegida", debe configurar la puerta de enlace IP de UM con un FQDN. Además, debe configurarla para que escuche en el puerto 5061 y comprobar si también se configuraron puertas de enlace VoIP o IP PBX para escuchar las solicitudes TLS mutuas en el puerto 5061. Para configurar una puerta de enlace IP de mensajería unificada, ejecute el siguiente comando en el Shell: `Set-UMIPGateway -identity MyUMIPGateway -Port 5061`
        
        Si se usa un FQDN, debe asegurarse de que se haya configurado correctamente un registro de host DNS para la puerta de enlace VoIP, la IP PBX o la PBX con SIP habilitado, de modo que el nombre del host se resuelva correctamente en una dirección IP. Además, si usa un FQDN en lugar de una dirección IP y se modifica la configuración de DNS para la puerta de enlace IP de UM, deberá deshabilitar la puerta de enlace IP de UM y luego habilitarla para asegurarse de que la información de configuración de esta puerta de enlace se actualice correctamente.
    
      - **Plan de marcado de mensajería unificada**   Haga clic en **Examinar** para seleccionar el plan de marcado de mensajería unificada que desea asociar a la puerta de enlace IP de mensajería unificada. Cuando seleccione un plan de marcado de mensajería unificada con una puerta de enlace IP de mensajería unificada, también se creará un grupo de extensiones de mensajería unificada predeterminado y se asociará con el plan de marcado de mensajería unificada seleccionado. Si no selecciona un plan de marcado de mensajería unificada, deberá crear manualmente un grupo de extensiones de mensajería unificada y, a continuación, asociar dicho grupo con una puerta de enlace IP de mensajería unificada que haya creado.

3.  Haga clic en **Guardar**.

Si es necesario, puede crear una puerta de enlace IP de UM ejecutando el comando siguiente.

```powershell
New-UMIPGateway -Identity MyUMIPGateway -Address "MyUMIPGateway.contoso.com"
```

Para configurar una puerta de enlace IP de UM existente desde el EAC:

1.  En el EAC, vaya a **Mensajería unificada** \> **Puertas de enlace IP de mensajería unificada** y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

2.  En la página **Puerta de enlace IP de mensajería unificada**, haga clic en **Configurar**. Use las opciones de configuración para ver configuraciones concretas de la puerta de enlace IP de UM y habilitar o deshabilitar características.

Para configurar una puerta de enlace IP de UM existente en el Shell, ejecute el siguiente comando en el Shell.

```powershell
Set-UMIPGateway -Identity MyUMIPGateway -Address fe80::39bd:88f7:6969:d223%11 -IPAddressFamily Any -Status Disabled -OutcallsAllowed $false
```

## Paso 9: Crear un grupo de extensiones de mensajería unificada

En función de la implementación actual de Exchange 2010, puede ser necesario crear un grupo de extensiones de mensajería unificada. Un grupo de extensiones de telefonía ofrece una forma de distribuir las llamadas telefónicas desde un solo número a varias extensiones o números de teléfono. En Mensajería unificada, un grupo de extensiones de UM es una representación lógica de un grupo de extensiones de telefonía que vincula una puerta de enlace IP de UM a un plan de marcado de UM.

Debe tener, como mínimo, un grupo de extensiones de UM para cada grupo de extensiones de IP PBX o PBX. Cuando termine el proceso siguiente, se creará un grupo de extensiones de UM de manera predeterminada. Si tiene más de un grupo de extensiones de IP PBX o PBX, debe crear grupos de extensiones de UM adicionales. Para más información sobre los grupos de extensiones de UM, vea [Grupos de búsqueda de mensajería unificada](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/connect-voice-mail-system/um-hunt-groups).

Si es necesario, puede crear un grupo de extensiones de UM desde el EAC:

1.  En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**. En la vista de lista, seleccione el plan de marcado de UM que quiere modificar y luego haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

2.  En la página **Plan de marcado de mensajería unificada**, en **Grupos de extensiones de mensajería unificada**, haga clic en **Nuevo**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").

3.  En la página **Nuevo grupo de extensiones de mensajería unificada**, especifique la siguiente información:
    
      - **Nombre**   Use este cuadro para crear el nombre para mostrar del grupo de extensiones de mensajería unificada. Se requiere un nombre de grupo de extensiones de mensajería unificada exclusivo, que solo se usará para mostrar en el EAC y en el Shell. Si tiene que cambiar el nombre para mostrar del grupo de extensiones después de crearlo, antes debe eliminar el grupo de extensiones existente y, a continuación, crear otro grupo de extensiones con el nombre adecuado. Si la organización usa varios grupos de extensiones, es recomendable que use nombres significativos. La longitud máxima de un nombre de grupo de extensiones de mensajería unificada es de 64 caracteres y puede incluir espacios. No obstante, no pueden incluirse ninguno de los caracteres siguientes: " / \\ \[ \] : ; | = , + \* ? \< \>.
    
      - **Puerta de enlace IP de mensajería unificada**   Use este cuadro para seleccionar una puerta de enlace IP de mensajería unificada. Este cuadro muestra el nombre de la puerta de enlace IP de mensajería unificada que se vinculará al grupo de extensiones de mensajería unificada. Para vincular una puerta de enlace IP de mensajería unificada a un grupo de extensiones de mensajería unificada, haga clic en **Examinar**.
    
      - **Identificador piloto**   Use este cuadro para especificar una cadena que identifique exclusivamente al identificador piloto configurado en la PBX o IP-PBX. Puede usar un número de extensión o un Identificador uniforme de recursos (URI) de SIP en este cuadro. Este cuadro admite caracteres alfanuméricos. Para PBX heredadas, se usa un valor numérico como identificador piloto. Sin embargo, algunas IP-PBX y PBX habilitadas para SIP pueden usar URI de SIP.

4.  Haga clic en **Guardar**.

Si es necesario, puede crear un grupo de extensiones de mensajería unificada al ejecutar el siguiente comando en el Shell.

```powershell
New-UMHuntGroup -Name MyUMHuntGroup -PilotIdentifier 5551234,55555 -UMDialPlan MyUMDialPlan -UMIPGateway MyUMIPGateway
```


> [!TIP]
> La configuración de un grupo de extensiones de UM no se puede definir ni cambiar. Si quiere cambiar las opciones de configuración de un grupo de extensiones de UM, tiene que eliminarlo y agregar otro grupo nuevo con la configuración correcta.



## Paso 10: Crear o configurar operadores automáticos de mensajería unificada

En función de la implementación actual de Exchange 2010, puede ser necesario crear operadores automáticos de mensajería unificada. Puede usar operadores automáticos de mensajería unificada para crear un sistema de menú de voz que permita a llamadores internos y externos usar el sistema de menú de operadores automáticos de mensajería unificada para buscar personas y hacer o transferir llamadas a los usuarios de una compañía o los departamentos de una organización. Para más información, vea [Contestar y enrutar automáticamente las llamadas entrantes](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/automatically-answer-and-route-calls/automatically-answer-and-route-calls).

En implementaciones pequeñas, puede que solo quiera implementar Mensajería unificada para que los llamadores puedan dejar correos de voz a los usuarios. En estas implementaciones, no es necesario crear un operador automático. Sin embargo, en la mayoría de los casos, el uso de operadores automáticos es muy útil para los llamadores externos que llaman a la organización.

Si es necesario, puede crear un operador automático de UM desde el EAC:

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

Si es necesario, puede crear un operador automático de mensajería unificada ejecutando el comando siguiente en el Shell.

```powershell
New-UMAutoAttendant -Name MyUMAutoAttendant -UMDialPlan MyUMDialPlan -PilotIdentifierList 56000,56100 -SpeechEnabled $true -Status Enabled
```

Si es necesario, puede configurar un operador automático existente desde el EAC:

1.  En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada** y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

2.  En la página **Plan de marcado de mensajería unificada**, bajo **Operadores automáticos de mensajería unificada**, seleccione el operador automático de mensajería unificada que desee ver o configurar y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar"). Use las opciones de configuración para ver la configuración específica del operador automático y para habilitar o deshabilitar características.

Si es necesario, puede configurar un operador automático existente ejecutando el comando siguiente en el Shell.

```powershell
Set-UMAutoAttendant -Identity MySpeechEnabledAA -DTMFFallbackAutoAttendant MyDTMFAA -OperatorExtension 50100 -AfterHoursTransferToOperatorEnabled $true -StaroutToDialPlanEnabled $true
```

## Paso 11: Crear o configurar directivas de buzón de mensajería unificada

En función de la implementación actual de Exchange 2010, puede ser necesario crear directivas de buzón de mensajería unificada o configurar las existentes. Las directivas de buzón de mensajería unificada son necesarias cuando habilita usuarios para Mensajería unificada. El buzón de cada usuario habilitado para mensajería unificada debe estar vinculado a una única directiva de buzón de UM. Una vez creada una directiva de buzón de UM, debe vincular uno o más buzones habilitados para UM a la directiva de buzón de UM. Esto permite controlar las opciones de seguridad del PIN, como el número mínimo de dígitos del PIN o el número máximo de intentos de inicio de sesión de los usuarios habilitados para UM que están vinculados a la directiva de buzón de UM. Para más información, vea [directivas de buzón de mensajería unificada](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/set-up-voice-mail/um-mailbox-policies).

Si es necesario, puede crear una directiva de buzón de mensajería unificada desde el EAC:

1.  En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**. En la vista de lista, seleccione el plan de marcado de mensajería unificada que desea modificar y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

2.  En la página **Plan de marcado de mensajería unificada**, en **Directivas de buzón de mensajería unificada**, haga clic en **Agregar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Nueva directiva de buzón de mensajería unificada**, en el cuadro **Nombre**, escriba el nombre de la nueva directiva de buzón de mensajería unificada.
    

    > [!NOTE]
    > Use esta casilla para especificar un nombre único para la directiva de buzones de mensajería unificada. Se trata de un nombre para mostrar que aparecerá en el EAC. Si debe cambiar el nombre para mostrar de la directiva de buzones de mensajería unificada después de haberla creado, primero debe eliminar la directiva existente y, a continuación, crear otra con el nombre adecuado. No puede eliminar una directiva de buzón de mensajería unificada si algún usuario habilitado para mensajería unificada está asociado con la directiva. El nombre de la directiva de mensajería unificada es obligatorio, pero se usa únicamente con fines de visualización. Se recomienda usar nombres con un significado concreto para las directivas de buzones de mensajería unificada, ya que la organización puede usar varias directivas de este tipo. La longitud máxima de un nombre de directiva de buzones de mensajería unificada es de 64 caracteres y puede incluir espacios. No obstante, no pueden incluirse ninguno de los caracteres siguientes: " / \ [ ] : ; | = , + * ? &lt; &gt;.



4.  Haga clic en **Guardar**.
    

    > [!NOTE]
    > Cuando guarda la directiva de buzón de mensajería unificada, se habilitan todas las configuraciones predeterminadas, incluida la configuración de las directivas de PIN, de las características de correo de voz y del correo de voz protegido. Si quiere personalizar o cambiar alguna opción predeterminada de la directiva de buzón de mensajería unificada que acaba de crear, use el cmdlet <STRONG>Set-UMMailbox</STRONG> o el EAC.



Si es necesario, puede crear una directiva de buzón de mensajería unificada ejecutando el comando siguiente en el Shell.

```powershell
New-UMMailboxPolicy -Name MyUMMailboxPolicy -UMDialPlan MyUMDialPlan
```

Si es necesario, puede configurar una directiva de buzón existente de mensajería unificada desde el EAC:

1.  En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada** y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

2.  En la página **Plan de marcado de mensajería unificada**, en **Directivas de buzón de mensajería unificada**, seleccione la directiva de buzón de mensajería unificada que desea ver o configurar y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar"). Use las opciones de configuración para ver la configuración específica de la directiva de buzón de mensajería unificada y para habilitar o deshabilitar características.

Si es necesario, puede configurar una directiva de buzón de UM existente ejecutando el comando siguiente en el Shell.

```powershell
Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -LogonFailuresBeforePINReset 8 -MaxLogonAttempts 12 -MinPINLength 8 -PINHistoryCount 10 -PINLifetime 60 -ResetPINText "The PIN used to allow you access to your mailbox using Outlook Voice Access has been reset."
```

## Paso 12: Mover los buzones habilitados para UM existentes a Exchange 2013

En Mensajería unificada de Exchange 2010, después de habilitar a los usuarios de la organización para el uso del correo de voz, se aplica al usuario un conjunto predeterminado de propiedades de UM para que pueda usar las características de UM. Para más información, vea [Correo de voz para usuarios](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/set-up-voice-mail/voice-mail-for-users).

Durante el proceso de actualización, habrá un período de tiempo en el que los buzones habilitados para UM estarán en los servidores de buzones de Exchange 2010 y de Exchange 2013. Sin embargo, si va a mover todos los usuarios habilitados para UM a los servidores de buzones de Exchange 2013, tiene que usar el EAC o el cmdlet **New-MoveRequest** del Shell desde un servidor de Exchange 2013 para conservar todas las propiedades y configuraciones, incluido el PIN del usuario.

Una solicitud de movimiento es el proceso de mover un buzón de una base de datos de buzones a otra. Una solicitud de movimiento local es un traslado de buzones que se produce dentro de un mismo bosque. Para más información sobre los movimiento de buzones, vea:

  - [Movimientos de buzones de Exchange 2013](mailbox-moves-in-exchange-2013-exchange-2013-help.md)

  - [New-MoveRequest](https://technet.microsoft.com/es-es/library/dd351123\(v=exchg.150\))

  - [New-MigrationBatch](https://technet.microsoft.com/es-es/library/jj219166\(v=exchg.150\))

  - [Administración de solicitudes de movimiento](https://go.microsoft.com/fwlink/p/?linkid=296352)

Para mover un buzón de Exchange 2010 a un servidor de buzones de Exchange 2013 desde el EAC:

1.  En el EAC, haga clic en **Destinatarios** \> **Migración** y luego haga clic en **Agregar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

2.  En el Asistente para **nuevo movimiento de buzón local**, seleccione el usuario que desee mover y haga clic en **Aceptar** y, a continuación, haga clic en **Siguiente**.

3.  En la página **Mover configuración**, especifique un nombre para el nuevo lote. Seleccione las opciones que quiere para el buzón de archivo y la ubicación de la base de datos de buzones, y haga clic en **Nuevo**.

Para mover un buzón de Exchange 2010 a un servidor de buzones de Exchange 2013 usando el Shell, ejecute el comando siguiente.

```powershell
New-MoveRequest -Identity 'tony@alpineskihouse.com' -TargetDatabase "DB01"
```

## Paso 13: Habilitar a usuarios nuevos para Mensajería unificada o definir la configuración de un usuario ya habilitado para UM

Un usuario debe tener un buzón para que se le pueda habilitar para Mensajería unificada. De forma predeterminada, los usuarios que tienen buzón no están habilitados para Mensajería unificada. Después de habilitar a los usuarios para UM, podrá administrar, modificar y configurar sus propiedades de Mensajería unificada y características del correo de voz. Puede habilitar a un usuario para Mensajería unificada usando el EAC o el Shell. Para más información, vea [Correo de voz para usuarios](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/set-up-voice-mail/voice-mail-for-users).

Cuando habilita un usuario para mensajería unificada, debe definir al menos un número de extensión que la mensajería unificada usará cuando el correo de voz se envíe al buzón del usuario y para permitir al usuario utilizar Outlook Voice Access. Una vez habilitado el usuario para mensajería unificada, se pueden agregar números de extensión secundarios para el buzón del usuario, así como modificarlos o quitarlos al configurar la dirección proxy de mensajería unificada de Exchange (EUM) en el buzón del usuario o al agregar o quitar extensiones adicionales o secundarias para el usuario en el EAC. Para agregar, modificar o quitar números de extensión, números E.164 o direcciones SIP, consulte [Procedimientos de usuario habilitado para correo de voz](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/set-up-voice-mail/voice-mail-enabled-user-procedures).

Para habilitar un usuario para mensajería unificada con el EAC:

1.  En el EAC, haga clic en **Destinatarios**.

2.  En la vista de lista, seleccione el usuario cuyo buzón desee habilitar para la mensajería unificada.

3.  En el panel de detalles, en **Características de voz y teléfono**, haga clic en **Habilitar**.

4.  En la página **Habilitar el buzón de correo de mensajería unificada**, haga clic en el botón **Explorar** al lado de la **Directiva de buzón de correo de mensajería unificada**, ubique en la lista la directiva de buzones de correo de mensajería unificada que va a asignar al usuario y luego haga clic en **Aceptar**.

5.  En la página **Habilitar el buzón de correo de mensajería unificada**, rellene los siguientes cuadros:
    
      - **Dirección SIP o número E.164**: escriba la dirección SIP o el número E.164 del usuario. Estas opciones están disponibles si el usuario que habilitó para mensajería unificada está asignado a una directiva de buzón de Mensajería unificada vinculada a un plan de marcado URI de SIP o E.164. A un usuario no se le puede agregar una dirección SIP o número E.164 si el usuario está asociado con un plan de marcado de extensión telefónica. Cuando asigna el usuario a una directiva de buzón de UM vinculada a un plan de marcado de E.164 o URI de SIP, también debe introducir un número de extensión para el usuario. Este número de extensión se usa cuando los usuarios acceden a su buzón desde Outlook Voice Access. El número de dígitos que se configura en este cuadro debe coincidir con el número de dígitos configurados en el plan de marcado URI de SIP o E.164.
    
      - **Número de extensión**: escriba el número de extensión del usuario que va a habilitar para mensajería unificada.
        
        Deberá proporcionar un número de extensión válido para el usuario y deberá coincidir con el número de dígitos especificado en el plan de marcado. Solo puede escribir caracteres numéricos o dígitos del 1 al 20. El número de extensión típico es de 3 a 7 dígitos de largo. El número de dígitos en la extensión se configura en el plan de marcado que está vinculado a la directiva de buzones de correo de mensajería unificada asignada al usuario.
    
      - En **Configuración de PIN**, complete lo siguiente:
        
          - **Generar un PIN automáticamente**   Haga clic en este botón para generar de forma automática un PIN para que el usuario habilitado para mensajería unificada use el acceso al correo de voz por medio de Outlook Voice Access. Esta es la configuración predeterminada. Cuando hace clic en este botón, se genera automáticamente un PIN de acuerdo con las directivas de PIN configuradas en la directiva de buzón de correo de mensajería unificada asignada al usuario. Se recomienda utilizar esta opción para ayudar a proteger el PIN del usuario. El PIN se envía al usuario en el mensaje de bienvenida que este recibe después de su habilitación para mensajería unificada. De manera predeterminada, tendrá que cambiar este PIN la primera vez que inicie sesión en el buzón de correo para obtener el correo de voz.
        
          - **Escribir un PIN**   Haga clic en este botón para especificar de forma manual un PIN que el usuario utilizará para acceder al sistema de correo de voz. El PIN debe cumplir con las configuraciones de directivas de PIN establecidas en la directiva de buzones de correo de mensajería unificada asociada con el usuario habilitado para mensajería unificada. Por ejemplo, si la directiva de buzón de correo de mensajería unificada está configurada para aceptar solamente PIN que contengan siete o más dígitos, el PIN que escriba en este cuadro debe tener al menos siete dígitos.
        
          - **Pedir que el usuario restablezca su PIN la primera vez que inicia sesión**   Seleccione esta casilla para obligar al usuario a que restablezca su PIN de correo de voz cuando acceda por primera vez al sistema de correo de voz desde un teléfono mediante el uso de Outlook Voice Access. Se le solicitará que escriba un PIN con el que esté familiarizado. Hacer que los usuarios habilitados para mensajería unificada cambien el PIN la primera vez que inician sesión es un procedimiento recomendado de seguridad que los ayuda a protegerse contra el acceso no autorizado a sus datos y a su Bandeja de entrada. Esta casilla está activada de forma predeterminada.

6.  En la página **Habilitar el buzón de correo de mensajería unificada**, revise las configuraciones. Haga clic en **Finalizar** para habilitar al usuario para el uso de Mensajería unificada. Haga clic en **Atrás** para hacer cambios de configuración.

Para habilitar a un usuario para Mensajería unificada usando el Shell, ejecute el comando siguiente.

```powershell
Enable-UMMailbox -Identity tonysmith@contoso.com -UMMailboxPolicy MyUMMailboxPolicy -Extensions 51234 -PIN 5643892 -NotifyEmail administrator@contoso.com -PINExpired $true
```

Si es necesario, puede configurar a un usuario que se haya habilitado para UM desde el EAC:

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

Si es necesario, puede configurar a un usuario que se haya habilitado para UM en el Shell ejecutando el comando siguiente.

```powershell
Set-UMMailbox -Identity tony@contoso.com -CallAnsweringAudioCodec Wma -CallAnsweringRulesEnabled $false -FaxEnabled $false -UMSMSNotificationOption VoiceMail
```

## Paso 14: Configurar las puertas de enlace VoIP, las IP PBX y las PBX con SIP habilitado para enviar todas las llamadas entrantes a los servidores de acceso de cliente de Exchange 2013

Cuando se instalan servidores de acceso de clientes y de buzones de Exchange 2013, se habilitan automáticamente para que puedan responder a las llamadas de voz entrantes y salientes, y para que enruten los mensajes de correo de voz a los destinatarios adecuados. Cuando se instalan servidores de acceso de clientes y de buzones de Exchange 2013, y se implementa la mensajería unificada, no es necesario vincular ni agregar servidores de acceso de clientes ni de buzones de Exchange 2013 a los planes de marcado de mensajería unificada. Los servidores de acceso de clientes y de buzones de Exchange 2013 responden a todas las llamadas entrantes y luego usan los planes de marcado de mensajería unificada para encontrar a los usuarios.

El servidor de acceso de clientes de Exchange 2013 representa el punto de entrada para las llamadas entrantes o solicitudes del protocolo de inicio de sesión (SIP) para la mensajería unificada. El servicio que se encarga de las solicitudes SIP en un servidor de acceso de cliente de Exchange 2013 es el servicio de enrutador de llamadas de mensajería unificada y se ejecuta en cada servidor de acceso de cliente de Exchange 2013 de la organización.

Cuando actualiza a la mensajería unificada de Exchange 2013, debe tener previamente instaladas y configuradas una o varias puertas de enlace VoIP para conectarse a las PBX de la red de telefonía, o instaladas y configuradas IP-PBX o PBX habilitadas para protocolo de inicio de sesión (SIP).

El último paso en el proceso de actualizar a mensajería unificada de Exchange 2013 es configurar las puertas de enlace VoIP, IP-PBX o PBX habilitadas para SIP para enviar llamadas entrantes a los servidores de acceso de cliente de Exchange 2013. (Se incluyen autores de llamadas que desean dejar un correo de voz para un usuario, llamadas de usuarios habilitados para mensajería unificada que llaman a Outlook Voice Access y llamadas de personas que llaman a un operador automático de mensajería unificada). Todas estas llamadas son recibidas primero por una puerta de enlace VoIP, IP-PBX o PBX habilitadas para SIP y luego son reenviadas a los servidores de acceso de cliente de Exchange 2013 de la organización de Exchange 2013. Para obtener más información, vea los recursos siguientes:

  -  [Servicios de mensajería unificada](um-services-exchange-2013-help.md)

  -  [Notas para la configuración de puertas de enlace de VoIP, IP PBX y PBX compatibles](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/telephone-system-integration-with-um/configuration-notes-for-voip-gateways)

  -  [Asesor de telefonía para Exchange 2013](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/telephone-system-integration-with-um/telephony-advisor-for-exchange-2013)

## Paso 15: Deshabilitar el contestador automático en un servidor de Mensajería unificada de Exchange 2010

Para deshabilitar el contestador automático, hay que deshabilitar la UM en un servidor de Mensajería unificada de Exchange 2010 o quitar el servidor de UM de un plan de marcado. Al deshabilitar Mensajería unificada, se impide que el servidor de Mensajería unificada responda a las llamadas entrantes. Puede desconectar todas las llamadas inmediatamente o esperar a que se procesen las llamadas en curso antes de deshabilitar el servidor de mensajería unificada. El contestador automático se debe deshabilitar antes de quitar el servidor de un plan de marcado para que las llamadas entrantes terminen de procesarse.

Para deshabilitar Mensajería unificada en un servidor de Mensajería unificada de Exchange 2010 usando la Consola de administración de Exchange:

1.  En el árbol de consola de la EMC, vaya a **Configuración del servidor** \> **Mensajería unificada**.

2.  En el panel de resultados, seleccione el servidor de mensajería unificada que va a deshabilitar.

3.  En el panel de acciones, haga clic en una de las siguientes opciones:
    
      - Cuando seleccione la opción **Deshabilitar inmediatamente**, el servidor de mensajería unificada desconectará todas las llamadas que se hayan conectado al servidor de mensajería unificada.
    
      - Si selecciona la opción **Deshabilitar tras terminar las llamadas**, el servidor de mensajería unificada no aceptará nuevas llamadas y no se deshabilitará hasta que se hayan procesado todas las llamadas.

4.  En el cuadro de diálogo de confirmación, haga clic en **Sí** para continuar.

Para deshabilitar Mensajería unificada en un servidor de Mensajería unificada de Exchange 2010 usando el Shell, ejecute el comando siguiente:

```powershell
Disable-UMServer -Identity MyUMServer -Immediate $true
```


> [!TIP]
> Puede usar el cmdlet <STRONG>Disable-UMServer</STRONG> desde un servidor de Mensajería unificada de Exchange 2010 o el cmdlet <STRONG>Disable-UMService</STRONG> desde un servidor de buzones de Exchange 2013 para deshabilitar el contestador automático.



## Paso 16: Quitar un servidor de Mensajería unificada de Exchange 2010 de un plan de marcado

Para procesar llamadas, tendrá que agregar un servidor de mensajería unificada de Exchange 2010 a al menos un plan de marcado de mensajería unificada. Un servidor de mensajería unificada se puede agregar a varios planes de marcado de mensajería unificada. Los servidores de mensajería unificada de Exchange 2010 se pueden quitar de un plan de marcado de mensajería unificada. Al quitar un servidor de mensajería unificada de un plan de marcado, el servidor de UM dejará de contestar llamadas y procesar las llamadas de mensajería unificada de los usuarios habilitados para UM.

Para quitar un servidor de Mensajería unificada de Exchange 2010 de un plan de marcado usando la Consola de administración de Exchange:

1.  En el árbol de consola de la EMC, vaya a **Configuración del servidor** \> **Mensajería unificada**.

2.  En el panel de resultados, seleccione el servidor de mensajería unificada.

3.  En el panel de acciones, haga clic en **Propiedades**.

4.  En la ficha **Configuración de mensajería unificada** en la sección **Planes de marcado asociados**, haga clic en **Quitar**.

5.  En el cuadro de diálogo de confirmación, haga clic en **Sí** para confirmar la eliminación del servidor de Exchange 2010 del plan de marcado de mensajería unificada.

6.  Haga clic en **Aceptar** para cerrar la ventana de propiedades.

Para quitar de un plan de marcado un servidor de Mensajería unificada de Exchange 2010 usando el Shell, ejecute el comando siguiente.

```powershell
$dp= Get-UMDialPlan "MySIPDialPlan"
$s=Get-UMServer -id MyUMServer
$s.dialplans-=$dp.identity
Set-UMServer -id MyUMServer -dialplans:$s.dialplans
```

En este ejemplo, hay tres planes de marcado URI de SIP: SipDP1, SipDP2 y SipDP3. En este ejemplo se quita el servidor de mensajería unificada denominado `MyUMServer` del plan de marcado SipDP3.

```powershell
Set-UMServer -id MyUMServer -DialPlans SipDP1,SipDP2
```

En este ejemplo, hay dos planes de marcado URI de SIP: SipDP1 y SipDP2. En este ejemplo se quita el servidor de mensajería unificada denominado `MyUMServer` del plan de marcado SipDP2.

```powershell
Set-UMServer -id MyUMServer -DialPlans SipDP1
```


> [!TIP]
> Puede usar el cmdlet <STRONG>Set-UMServer</STRONG> del Shell en un servidor de Mensajería unificada de Exchange 2010 o el cmdlet <STRONG>Set-UMService</STRONG> en un servidor de buzones de Exchange 2013 para quitar un servidor de Mensajería unificada de Exchange 2010 de uno o de varios planes de marcado. Por ejemplo, para quitar un servidor de Mensajería unificada de todos los planes de marcado, ejecute el comando siguiente: <CODE>Set-UMServer -identity MyUMServer -DialPlans $null</CODE>



## ¿Cómo saber si el proceso se ha completado correctamente?

Después de configurar la mensajería unificada, compruebe lo siguiente para asegurarse de que funcione correctamente:

  - Un usuario que ha habilitado para el correo de voz puede iniciar sesión en Outlook Web App u Outlook y ver el mensaje de bienvenida para la mensajería unificada.

  - Los usuarios de mensajería unificada pueden recibir mensajes de voz.

  - Los usuarios de mensajería unificada pueden llamar a un número de Outlook Voice Access para escuchar el correo electrónico, los elementos de calendario y el correo de voz.

  - La mensajería unificada enruta llamadas desde afuera de la organización, y usted puede realizar una llamada.

