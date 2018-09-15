---
title: 'Implementar mensajería unificada de Exchange 2013: Exchange 2013 Help'
TOCTitle: Implementar mensajería unificada de Exchange 2013
ms:assetid: d147d4b1-32d7-476b-b76f-ee3c0b35ba49
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ673564(v=EXCHG.150)
ms:contentKeyID: 49895931
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Implementar mensajería unificada de Exchange 2013

 

_**Se aplica a:** Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2016-12-09_

La mensajería unificada (MU) requiere que integre la implementación de Exchange Server con el sistema telefónico que haya en la organización. Una implementación correcta requiere un análisis cuidadoso de la infraestructura telefónica existente y la realización de los pasos de planificación adecuados para implementar y administrar el correo de voz en la mensajería unificada.

**Contenido**

Antes de implementar

Implementación de la mensajería unificada

Tareas posteriores a la implementación de la mensajería unificada

## Antes de implementar

Antes de implementar la mensajería unificada, le recomendamos familiarizarse con los conceptos de los temas siguientes:

  - [Planes de marcado de mensajería unificada](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/set-up-client-voice-mail-features/set-the-voice-mail-preview-partner-address)

  - [Puertas de enlace IP de mensajería unificada](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/connect-voice-mail-system/um-ip-gateways)

  - [Servicios de mensajería unificada](um-services-exchange-2013-help.md)

  - [Grupos de búsqueda de mensajería unificada](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/connect-voice-mail-system/um-hunt-groups)

  - [Contestar y enrutar automáticamente las llamadas entrantes](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/automatically-answer-and-route-calls/automatically-answer-and-route-calls)

  - [directivas de buzón de mensajería unificada](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/set-up-voice-mail/um-mailbox-policies)

  - [Correo de voz para usuarios](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/run-voice-mail-call-reports/review-voice-mail-calls-for-user)

## Implementación de la mensajería unificada

Independientemente de que implemente la mensajería unificada mediante centrales de conmutación de IP (IP PBX), puertas de enlace VoIP o Microsoft Lync Server, todas las opciones de implementación de mensajería unificada tienen varios pasos en común. Estos pasos son necesarios para crear un sistema escalable de alta disponibilidad que admita grandes cantidades de usuarios de mensajería unificada. Estos pasos son los siguientes:

1.  Implementar y configurar los componentes de telefonía para la mensajería unificada.

2.  Compruebe que instaló correctamente el servidor de acceso de cliente que ejecuta el servicio de enrutador de llamadas de mensajería unificada de Microsoft Exchange y el servidor de buzones de correo que ejecuta el servicio de mensajería unificada de Microsoft Exchange.

3.  Cree y configure los componentes necesarios de la mensajería unificada.

4.  Realice las tareas posteriores a la implementación de la mensajería unificada.

## Implementar y configurar los componentes de telefonía

Para implementar correctamente la mensajería unificada en una organización de Exchange, el administrador de Exchange debe tener conocimiento acerca de los conceptos de redes de datos y la terminología y los conceptos de telefonía, y ser capaz de configurar los componentes de telefonía necesarios para la mensajería unificada de manera correcta. Se necesitan amplios conocimientos de redes de telefonía y de mensajería unificada para realizar una nueva implementación o actualizar un sistema de correo de voz heredado.

Normalmente, debe completar tres tareas para configurar correctamente los componentes de telefonía necesarios para la mensajería unificada:

1.  **Aprovisionar líneas de PBX**   El primer paso para implementar una solución de MU escalable es aprovisionar líneas de PBX.

2.  **Organizar canales**   Después de aprovisionar canales de voz basados en PBX, puede organizarlos como grupos de extensiones.

3.  **Implementar puertas de enlace VoIP**   Después de organizar los canales de voz como grupos de extensiones, estos canales deben terminar en las puertas de enlace VoIP. Las puertas de enlace VoIP se usan junto a una PBX heredada para convertir los protocolos de conmutación de circuitos de una red de telefonía en protocolos de conmutación de paquetes basados en IP.

Cuando integre la telefonía de la organización y las redes de datos durante la implementación de la mensajería unificada, debe configurar la telefonía y los componentes de redes de datos correctamente. También debe configurar los siguientes componentes o interfaces para implementar la mensajería unificada correctamente:

  - **Configure la conexión de las PBX de la organización para comunicarse con las puertas de enlace VoIP.**   Para más información, vea [Conectar una puerta de enlace VoIP para comunicarse con una PBX](connect-a-voip-gateway-to-communicate-with-a-pbx-exchange-2013-help.md).

  - **Configure la conexión de la interfaz de la puerta de enlace VoIP a la PBX.**   Para más información sobre cómo configurar la interfaz de su PBX para comunicarse con su puerta de enlace VoIP compatible, vea la documentación del producto específico de su PBX o vea [Conectar una puerta de enlace VoIP para comunicarse con una PBX](connect-a-voip-gateway-to-communicate-with-a-pbx-exchange-2013-help.md).

  - **Configure la conexión desde la interfaz de la puerta de enlace VoIP para los servidores de buzones de correo y de acceso de cliente.**   Para más información, vea [Conectar una puerta de enlace VoIP, IP PBX o un controlador de borde de sesión a mensajería unificada](connect-a-voip-gateway-ip-pbx-or-session-border-controller-to-um-exchange-2013-help.md).

  - **Configure la conexión desde los servidores de correo de voz y de acceso de cliente a la interfaz de la puerta de enlace VoIP.**   Para más información, vea [Conectar la mensajería unificada a una puerta de enlace VoIP compatible](connect-um-to-a-supported-voip-gateway-exchange-2013-help.md).

Antes de implementar

## Instalar los servidores de buzones de correo y de acceso de cliente

Existen rutas de acceso de implementación diferentes disponibles para las organizaciones que planean implementar la mensajería unificada de Exchange. Aunque estas rutas conducen al mismo resultado final, una implementación satisfactoria de la mensajería unificada, cada ruta presenta una leve diferencia porque cada necesidad y punto de inicio de los clientes es diferente. Sin embargo, existen puntos de inicio y rutas comunes que, por lo general, cubren todas las situaciones de implementación compatibles, incluidas las instalaciones y las actualizaciones nuevas. Siga estos pasos para implementar sus servidores de buzones de correo y de acceso de cliente:

1.  Compruebe que su infraestructura existente cumple ciertos requisitos previos. Para obtener información más detallada, consulte [Requisitos previos de Exchange 2013](exchange-2013-prerequisites-exchange-2013-help.md).

2.  Implemente su nueva organización de Exchange 2013. Para obtener información detallada, consulte [Instalar Exchange 2013 utilizando el asistente de configuración](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md).
    

    > [!WARNING]
    > Debe implementar al menos un servidor de buzones de Exchange 2013 en su organización antes de configurar las puertas de enlace VoIP o las centrales de conmutación (PBX) de IP para enviar protocolos de inicio de sesión (SIP) de UM y tráfico RTP a los servidores de acceso de cliente de Exchange 2013.



3.  Compruebe que ha instalado correctamente los servidores de buzones de correo y de acceso de cliente. Después de instalar los servidores, le recomendamos comprobar la instalación y revisar los registros de instalación del servidor. Para obtener información más detallada, consulte [Comprobar una instalación de Exchange 2013](verify-an-exchange-2013-installation-exchange-2013-help.md).

## Agregar los paquetes de idioma de mensajería unificada requeridos

Los paquetes de idioma de mensajería unificada permiten a las personas que llaman y a los usuarios de Outlook Voice Access interactuar con el sistema de correo de voz en varios idiomas. Tras instalar un paquete idioma adicional en un servidor de buzones de correo, los autores de las llamadas y los usuarios de Outlook Voice Access podrán escuchar mensajes de correo electrónico e interactuar con el sistema de correo de voz en dicho idioma.

Cuando se instala Exchange U.S. English por primera vez, el inglés de Estados Unidos es el idioma predeterminado y el único idioma disponible para el plan de marcado. Tras instalar un paquete de idioma de mensajería unificada en un servidor Buzón de correo, el idioma asociado al paquete de idioma también aparecerá como opción disponible al configurar el idioma predeterminado del plan de marcado. De manera predeterminada, dado que los operadores automáticos de mensajería unificada están asociados con un plan de marcado de mensajería unificada cuando se crean, usarán la configuración de idioma predeterminada del plan de marcado de mensajería unificada asociado. Sin embargo, es posible cambiar esta configuración después de crear el operador automático de mensajería unificada.

Puede agregar paquetes de idioma de mensajería unificada mediante el comando Setup.exe o la ejecución del programa de instalación *\<UMLanguagePack\>*.exe después de haber descargado el paquete de idioma de mensajería unificada desde los [paquetes de idioma de mensajería unificada para Exchange Server 2013](https://go.microsoft.com/fwlink/p/?linkid=266542). Sin embargo, debe usar el comando Setup.exe para quitar un paquete de idioma de mensajería unificada. No existe ningún cmdlet del Shell de administración de Exchange para agregar o quitar idiomas de un servidor de buzones de correo. Para obtener más información acerca de cómo instalar un paquete de idioma de UM, consulte [Instalar un paquete de idioma de mensajería unificada](install-a-um-language-pack-exchange-2013-help.md).


> [!NOTE]
> De manera predeterminada, al instalar un servidor de buzones de correo, se instala el idioma inglés de los Estados Unidos (en-US). No se puede eliminar a no ser que elimine el servidor Buzón de correo del equipo.



Antes de implementar

## Crear y configurar componentes de mensajería unificada

Varios componentes de mensajería unificada son necesarios para la implementación y el funcionamiento de la mensajería unificada. Los componentes de la mensajería unificada conectan la infraestructura de telefonía con el entorno de mensajería unificada. Después de instalar correctamente los servidores de buzones de correo y de acceso de cliente, siga estos pasos.

## Paso 1: Crear y configurar los planes de marcado de MU

Los planes de marcado de mensajería unificada son importantes para el funcionamiento de la mensajería unificada y son necesarios para implementarla en su red correctamente. Una vez que haya instalado correctamente los servidores de buzones de correo y de acceso de cliente, un plan de marcado de mensajería unificada será el primer componente que creará.

De manera predeterminada, los planes de marcado de mensajería unificada y los servidores de buzones de correo y de acceso de cliente que están asociados al plan de marcado envían y reciben datos sin usar cifrado. En Modo no seguro, el tráfico de VoIP y de SIP no estará cifrado. Cuando crea el plan de marcado o después de haberlo crearlo, puede configurar el plan de marcado para que cifre el tráfico de VoIP y de SIP por medio de Seguridad de la capa de transporte (TLS) mutua. Si va a usar TLS mutua, establecerá el plan de marcado a protegido con SIP o protegido, el modo de inicio de mensajería unificada a TLS o dual, y creará y distribuirá un certificado de confianza a los servidores de Exchange y las puertas de enlace VoIP, IP PBX o los controladores de borde de sesión (SBC). Después de configurar los ajustes de seguridad de VoIP, deberá configurar el modo de inicio de los servidores de buzones de correo y de acceso de cliente. Para obtener información detallada, consulte [Configurar el modo de inicio en un servidor de buzones](configure-the-startup-mode-on-a-mailbox-server-exchange-2013-help.md) o [Configurar el modo de inicio en un servidor de acceso de cliente](configure-the-startup-mode-on-a-client-access-server-exchange-2013-help.md).

Realice el siguiente procedimiento para crear un nuevo plan de marcado de mensajería unificada.

## Crear un plan de marcado de mensajería unificada

1.  En el Centro de administración de Exchange (EAC), vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada** y haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").

2.  En la página **Nuevo plan de marcado de mensajería unificada**, complete los siguientes cuadros:
    
      - **Nombre**   Escriba el nombre del plan de marcado. El nombre de un plan de marcado de mensajería unificada es obligatorio y debe ser exclusivo. El nombre que escriba se usará solo para la visualización en el EAC y en el Shell. La longitud máxima del nombre de un plan de marcado de MU es de 64 caracteres y puede incluir espacios. No obstante, no pueden incluirse ninguno de los caracteres siguientes: " / \\ \[ \] : ; | = , + \* ? \< \>.
        

        > [!IMPORTANT]
        > Aunque en el cuadro del nombre del plan de marcado se pueden escribir hasta 64 caracteres, el nombre no debe tener más de 49 caracteres. Esto se debe a que, al crear un plan de marcado de llamadas, también se crea una directiva de buzón de MU predeterminada que tiene el nombre Directiva predeterminada de <EM>&lt;NombreDePlanDeMarcado&gt;</EM>. El parámetro <EM>name</EM> tanto para el plan de marcado de MU como para la directiva de buzón de MU puede tener un máximo de 64 caracteres.

    
      - **Longitud de la extensión (dígitos)**   Escriba el número de dígitos para los números de extensión en el plan de marcado. El número de dígitos para números de extensión se basa en el plan de marcado de telefonía que se crea en una central de conmutación (PBX). Por ejemplo, si un usuario asociado con un plan de marcado de telefonía marca una extensión de cuatro dígitos para llamar a otro usuario del mismo plan de marcado, deberá seleccionar 4 como el número de dígitos de la extensión.
        
        Este es un cuadro obligatorio que tiene un intervalo de valores entre 1 y 20. La longitud típica oscila entre 3 y 7. Si el entorno de telefonía existente incluye números de extensión, debe especificar el número de dígitos de dichas extensiones.
        
        Al crear un plan de marcado de extensión telefónica, debe escribir un número de extensión para el usuario cuando está vinculado a un plan de marcado de extensión telefónica. También se requiere un número de extensión con los planes de marcado de Protocolo de inicio de sesión (SIP) o E.164 cuando un usuario habilitado para mensajería unificada está vinculado a un plan de marcado de URI de SIP o E.164. Este número de extensión lo usan los usuarios de Outlook Voice Access para obtener acceso al buzón de correo de Exchange.
    
      - UNRESOLVED\_TOKENBLOCK\_VAL(Tipo UI\_URI)
    
      - UNRESOLVED\_TOKENBLOCK\_VAL(Seguridad UI\_VoIP)
    
      - **Código de país o región**   Use este cuadro para escribir el código de país o región que se usará para las llamadas salientes. Este número se antepondrá automáticamente al número de teléfono que se marque. En este cuadro se pueden escribir de 1 a 4 dígitos. Por ejemplo, en Estados Unidos el código de país o región es 1. En el Reino Unido es 44.

3.  Haga clic en **Guardar**.
    

    > [!IMPORTANT]
    > En las versiones anteriores de Exchange, el servidor de mensajería unificada se tenía que agregar a un plan de marcado de mensajería unificada. En Exchange&nbsp;2013, los servidores de buzones de correo y de acceso de cliente no se pueden asociar con un plan de marcado de extensión telefónica o E.164. Los servidores de buzones de correo y de acceso de cliente responderán todas las llamadas entrantes para todos los tipos de planes de marcado. Sin embargo, si usted integra la mensajería unificada con Microsoft Lync Server, debe agregar todos los servidores de buzones de correo y de acceso de cliente a todos los planes de marcado de URI de SIP para habilitar el correcto funcionamiento del enrutamiento de llamadas con Lync Server.



Antes de implementar

## Paso 2: Crear y configurar las puertas de enlace IP de MU

Una puerta de enlace IP de mensajería unificada representa un dispositivo de hardware de puerta de enlace VoIP o un IP PBX. La combinación de la puerta de enlace IP de mensajería unificada y un grupo de extensiones de mensajería unificada establece un vínculo entre una puerta de enlace VoIP o IP PBX y un plan de marcado de mensajería unificada.

Si creó o habilitó la seguridad de VoIP en un plan de marcado, la puerta de enlace IP de mensajería unificada que cree con uno de los procedimientos siguientes se asociará con un plan de marcado de mensajería unificada que usa seguridad de VoIP. En tal caso, debe usar un nombre de dominio completo (FQDN) para crear la puerta de enlace IP de MU en lugar de una dirección IP. También debe configurar la puerta de enlace IP de MU para que escuche en el puerto TCP 5061. Para configurar la puerta de enlace IP de MU para que escuche en el puerto TCP 5061, ejecute el siguiente comando: `Set-UMIPGateway -identity MyUMIPGateway -Port 5061`. También debe comprobar que se han configurado todas las puertas de enlace VoIP o IP PBX para escuchar el puerto 5061 para TLS mutua.

Realice el siguiente procedimiento para crear una nueva puerta de enlace IP de mensajería unificada.

## Cree una puerta de enlace IP de mensajería unificada

1.  
    
    En el EAC, vaya a **Mensajería unificada** \> **Puertas de enlace IP de mensajería unificada** y, luego, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").

2.  En la página **Nueva puerta de enlace IP de mensajería unificada**, escriba la siguiente información:
    
      - **Nombre**   Use este cuadro para especificar un nombre exclusivo para la puerta de enlace IP de mensajería unificada. Se trata de un nombre para mostrar que aparecerá en la Consola de administración de Exchange. Si debe cambiar el nombre para mostrar de la puerta de enlace IP de mensajería unificada una vez creada, primero debe eliminar la puerta de enlace IP de mensajería unificada existente y, a continuación, crear otra puerta de enlace IP de mensajería unificada con el nombre adecuado. El nombre de puerta de enlace IP de mensajería unificada es necesario, pero solo se usa para su visualización. Como la organización puede usar varias puertas de enlace IP de mensajería unificada, es recomendable el uso de nombres significativos para designar las puertas de enlace IP de mensajería unificada. La longitud máxima que puede tener un nombre de puerta de enlace IP de mensajería unificada es de 64 caracteres y puede incluir espacios. No obstante, no pueden incluirse ninguno de los caracteres siguientes: " / \\ \[ \] : ; | = , + \* ? \< \>.
    
      - **Dirección**   Puede configurar una puerta de enlace IP de mensajería unificada con una dirección IP o un nombre de dominio completo (FQDN). Use este cuadro para indicar la dirección IP configurada en la puerta de enlace VoIP, un PBX habilitado para SIP, un IP PBX, un SBC o un FQDN. En este cuadro solo se admiten FQDN válidos y con el formato correcto.
        
        Puede escribir caracteres alfabéticos y numéricos en este cuadro. Se admiten direcciones IPv4, IPv6 y FQDN. Si desea usar TLS mutua entre una puerta de enlace IP de mensajería unificada y un plan de marcado funcionando en modo SIP protegida o Protegida, debe configurar la puerta de enlace IP de mensajería unificada con un FQDN. También debe configurarla para que escuche en el puerto 5061 y compruebe si también se configuraron puertas de enlace VoIP o IP PBX para escuchar las solicitudes TLS mutuas en el puerto 5061. Para configurar una puerta de enlace IP de mensajería unificada, ejecute el siguiente comando: `Set-UMIPGateway -identity MyUMIPGateway -Port 5061`.
        
        Si se usa un FQDN, debe asegurarse de que se haya configurado correctamente un registro de host DNS para la puerta de enlace VoIP, de modo que el nombre del host se resuelva correctamente en una dirección IP. Asimismo, si utiliza un FQDN en lugar de una dirección IP, y se modifica la configuración de DNS para la puerta de enlace IP de mensajería unificada, deberá deshabilitar la puerta de enlace IP de mensajería unificada y habilitarla después para asegurarse de que la información de configuración de dicha puerta de enlace se actualiza correctamente
    
      - **Plan de marcado de mensajería unificada**   Haga clic en **Examinar** para seleccionar el plan de marcado de mensajería unificada que desea asociar con la puerta de enlace IP de mensajería unificada. Cuando seleccione un plan de marcado de mensajería unificada con una puerta de enlace IP de mensajería unificada, también se creará un grupo de extensiones de mensajería unificada predeterminado y se asociará con el plan de marcado de mensajería unificada seleccionado. Si no selecciona un plan de marcado de mensajería unificada, deberá crear manualmente un grupo de extensiones de MU y, a continuación, asociar dicho grupo con la puerta de enlace IP de mensajería unificada que cree.

3.  
    
    Haga clic en **Guardar**.

## Paso 3: Crear y configurar grupos de extensiones de MU (opcional)

*Grupo de extensiones* es un término que se usa para describir un grupo de recursos de PBX o de IP PBX, o bien números de extensión que comparten los usuarios. Los grupos de extensiones se usan para distribuir las llamadas de forma eficaz dentro o fuera de una unidad de negocio determinada.

Si creó una puerta de enlace IP de mensajería unificada y la asoció con un plan de marcado de mensajería unificada, se crea un grupo de extensiones de mensajería unificada predeterminado. Puede asociar otro grupo de extensiones de MU con la misma puerta de enlace IP de MU o con una diferente, de acuerdo con la cantidad de puertas de enlace IP de MU que haya creado.

Al crear un grupo de extensiones de mensajería unificada, permite que todos los servidores de buzones de correo especificados en el plan de marcado de mensajería unificada se comuniquen con una puerta de enlace VoIP. Para obtener información detallada, consulte [Grupos de búsqueda de mensajería unificada](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/connect-voice-mail-system/um-hunt-groups).

## Crear un grupo de extensiones de mensajería unificada

1.  En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**. En la vista de lista, seleccione el plan de marcado de mensajería unificada que desea cambiar y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

2.  En la página **Plan de marcado de mensajería unificada**, en **Grupos de extensiones de mensajería unificada**, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").

3.  En la página **Nuevo grupo de extensiones mensajería unificada**, complete los cuadros siguientes:
    
      - **Puerta de enlace IP de mensajería unificada asociada**   Este cuadro de solo lectura muestra el nombre de la puerta de enlace IP de mensajería unificada que se asociará al grupo de extensiones de mensajería unificada.
    
      - **Nombre**   Use este cuadro para crear el nombre para mostrar del grupo de extensiones de mensajería unificada. Se requiere un nombre de grupo de extensiones de mensajería unificada exclusivo, que solo se usará para mostrar en el EAC y en el Shell. Si tiene que cambiar el nombre para mostrar del grupo de extensiones después de crearlo, antes debe eliminar el grupo de extensiones existente y, a continuación, crear otro grupo de extensiones con el nombre adecuado.
        
        Si la organización usa varios grupos de extensiones, es recomendable que use nombres significativos. La longitud máxima de un nombre de grupo de extensiones de MU es de 64 caracteres y puede incluir espacios. No obstante, no pueden incluirse ninguno de los caracteres siguientes: " / \\ \[ \] : ; | = , + \* ? \< \>.
    
      - **Plan de marcado**   Haga clic en **Examinar** para seleccionar el plan de marcado que se asociará con el grupo de extensiones de mensajería unificada. Es necesario asociar un grupo de extensiones con un plan de marcado. Un grupo de extensiones de mensajería unificada sólo se puede asociar con una puerta de enlace IP de mensajería unificada y un plan de marcado de mensajería unificada.
    
      - **Identificador piloto**   Use este cuadro para especificar una cadena que identifique exclusivamente al identificador piloto o al Id. piloto configurado en la PBX o IP PBX.
        
        Puede usar un número de extensión o un Identificador uniforme de recursos (URI) del Protocolo de inicio de sesión (SIP) en este cuadro. Este cuadro admite caracteres alfanuméricos. Para PBX heredadas, se usa un valor numérico como identificador piloto. Sin embargo, algunas IP PBX pueden usar URI de SIP.

4.  Haga clic en **Guardar**.

Antes de implementar

## Paso 4: Crear y configurar una directiva de buzón de MU

Las directivas de buzón de mensajería unificada son necesarias cuando habilita usuarios para la mensajería unificada. El buzón de cada usuario habilitado para mensajería unificada debe estar vinculado a una única directiva de buzón de mensajería unificada. Una vez creada una directiva de buzón de UM, debe vincular uno o más buzones habilitados para UM a la directiva de buzón de UM. Esto permite controlar las opciones de seguridad del PIN, como el número mínimo de dígitos del PIN o el número máximo de intentos incorrectos de inicio de sesión de los usuarios habilitados para MU que están asociados a la directiva de buzón de MU.

Cada vez que crea un plan de marcado de MU, también se crea una directiva de buzón de MU. Esta directiva de buzón de MU se denominará Directiva predeterminada \<*DialPlanName*\>. Sin embargo, si debe crear una nueva directiva de buzones de correo de mensajería unificada, realice el siguiente procedimiento.

## Crear una directiva de buzón de mensajería unificada

1.  
    
    En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**. En la vista de lista, seleccione el plan de marcado de mensajería unificada que desea modificar y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

2.  En la página **Plan de marcado de mensajería unificada**, en **Directivas de buzón de correo de mensajería unificada**, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").

3.  En la página **Nueva directiva de buzón de mensajería unificada**, en el cuadro de texto **Nombre**, escriba el nombre de la nueva directiva de buzón de mensajería unificada.
    
    Use esta casilla para especificar un nombre único para la directiva de buzones de mensajería unificada. Se trata de un nombre para mostrar que aparecerá en la Consola de administración de Exchange. Si debe cambiar el nombre para mostrar de la directiva de buzón de mensajería unificada después de haberla creado, primero deberá eliminar la directiva actual y, a continuación, crear otra con el nombre adecuado. No puede eliminar una directiva de buzón de mensajería unificada si algún usuario habilitado para mensajería unificada está asociado a ella.
    
    El nombre de la directiva de mensajería unificada es obligatorio, pero solo se usa para mostrarlo. Se recomienda usar nombres con significado para las directivas de buzón de mensajería unificada, ya que la organización puede usar varias directivas de este tipo. La longitud máxima de un nombre de directiva de buzón de MU es de 64 caracteres y puede incluir espacios. No obstante, no pueden incluirse ninguno de los caracteres siguientes: " / \\ \[ \] : ; | = , + \* ? \< \>.

4.  Haga clic en **Guardar** para guardar la nueva directiva de buzón de mensajería unificada. Cuando guarda la directiva de buzón de mensajería unificada, se habilitan todas las opciones de configuración predeterminadas, incluida la configuración de las directivas de PIN, las características de buzón de voz y el correo de voz protegido. Si desea personalizar o cambiar alguna opción predeterminada, use el cmdlet **Set-UMMailbox** para cambiar la configuración de la directiva de buzón de mensajería unificada que acaba de crear.

## Paso 5: Crear y configurar operadores automáticos de MU (opcional)

La mensajería unificada le permite crear uno o más operadores automáticos de mensajería unificada, según las necesidades de la organización. Cuando crea un operador automático de MU, crea un sistema de menús de voz para la organización. Las personas que realizan llamadas dentro o fuera de la organización pueden desplazarse por el sistema de menús para buscar usuarios o departamentos de la organización y realizar o transferir llamadas a esos usuarios o departamentos.

Las personas que llaman pueden desplazarse por el sistema de menús por medio del tono de marcado multifrecuencia (DTMF), conocido también como entrada de tonos o por entradas de voz. Debe habilitar para voz al operador automático de mensajería unificada para que el reconocimiento automático de voz (ASR) funcione y los usuarios puedan usar las entradas de voz.

La creación y el uso de operadores automáticos son opcionales en la mensajería unificada. Sin embargo, si desea crear un nuevo operador automático de mensajería unificada, realice el siguiente procedimiento.

## Crear un operador automático de mensajería unificada

1.  
    
    En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**, seleccione el plan de marcado de mensajería unificada para el cual desea agregar un operador automático y, luego, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar") .

2.  En la página **Plan de marcado de mensajería unificada**, en **Operadores automáticos de mensajería unificada**, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").

3.  En la página **Nuevo operador automático de mensajería unificada**, complete las casillas siguientes:
    
      - **Nombre**   Use esta casilla para crear el nombre para mostrar del operador automático de mensajería unificada. El nombre de un operador automático de mensajería unificada es obligatorio y debe ser exclusivo. Sin embargo, se usa solamente para la visualización en el EAC y en el Shell.
        
        Si tiene que cambiar el nombre para mostrar del operador automático después de haberlo creado, primero, deberá eliminar el operador automático de mensajería unificada existente y crear otro operador automático que tenga el nombre apropiado. Si su organización usa varios operadores automáticos de mensajería unificada, es recomendable usar nombres significativos para los operadores automáticos de mensajería unificada. La longitud máxima del nombre de un operador automático de mensajería unificada es de 64 caracteres y puede contener espacios.
        
        Aunque puede asignar un nombre que contenga espacios a un nuevo operador automático de mensajería unificada, si integra la mensajería unificada en Office Communications Server 2007 R2 o Microsoft Lync Server, el nombre del operador automático no podrá contener espacios. Por lo tanto, si ha creado un operador automático con espacios en el nombre para mostrar y está integrándolo con Office Communications Server 2007 R2 o Lync Server, primero tendrá que eliminar el operador automático y, a continuación, crear otro operador automático que no incluya espacios en el nombre para mostrar.
    
      - **Crear este operador automático como habilitado**   Seleccione esta casilla para habilitar al operador automático para que responda las llamadas entrantes cuando termine de crear el operador automático de mensajería unificada. De forma predeterminada, los nuevos operadores automáticos se crean como deshabilitados.
        
        Si decide crear el operador automático de mensajería unificada como deshabilitado, puede usar el EAC o el Shell para habilitar el operador automático después de terminar de crear el operador automático.
    
      - **Configurar el operador automático para responder a los comandos de voz**    Seleccione esta casilla para habilitar el operador automático de mensajería unificada para voz. Si se habilita el operador automático para voz, las personas que llamen podrán responder con entradas de voz o marcación por tonos a los mensajes de asistencia por voz personalizados o del sistema que use el operador automático de mensajería unificada. De forma predeterminada, cuando los operadores automáticos se crean, no están habilitados para voz.
        
        Para que las personas que llaman usen un operador automático habilitado para voz en otro idioma que no sea el idioma inglés de los EE. UU. (en-US), debe instalar el paquete de idioma de mensajería unificada correspondiente y configurar las propiedades del operador automático para que use ese idioma. El paquete de idioma de mensajería unificada de en-US se instala de manera predeterminada al instalar un servidor de buzones de correo.
    
      - **Números de extensión**   Use este cuadro para escribir el número de extensión o los números telefónicos que usarán las personas que llamen para establecer contacto con el operador automático. Escriba un número de extensión o un número telefónico en el cuadro y, a continuación, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") para agregar el número a la lista. El número de dígitos del número de extensión o de teléfono que proporcione no tiene que coincidir con el número de dígitos de un número de extensión configurado en el plan de marcado de mensajería unificada asociado. El motivo es que se permiten las llamadas directas a los operadores automáticos de mensajería unificada.
        
        La cantidad de números de extensión o identificadores piloto que puede especificar es ilimitada. Sin embargo, puede crear el operador automático nuevo sin indicar un número de extensión o número telefónico. No es necesario un número de extensión o de teléfono.
        
        Puede editar o quitar un número de extensión existente o un identificador piloto. Para editar un número de extensión existente o un número telefónico, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar"). Para quitar un número de extensión existente o un número telefónico de la lista, haga clic en **Quitar**![Icono de quitar](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icono de quitar").

4.  Haga clic en **Guardar**.

Antes de implementar

## Tareas posteriores a la implementación de la mensajería unificada

Después de completar una nueva instalación de los servidores de buzones de correo y de acceso de cliente, y de haber implementado correctamente la mensajería unificada, debe realizar las tareas posteriores a la implementación. Estas tareas lo ayudarán a habilitar usuarios para mensajería unificada, asegurarán la implementación de MU e implementarán la funcionalidad de fax entrante para los usuarios habilitados para MU.

## Habilitar a los usuarios de correo de voz

Después de implementar las puertas de enlace VoIP o IP PBX, instalar los servidores de buzones de correo y de acceso de cliente, y crear los componentes necesarios para mensajería unificada, debe habilitar a los usuarios para la mensajería unificada. Para obtener información detallada, consulte [Habilitar a un usuario para el correo de voz](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/set-up-voice-mail/enable-a-user-for-voice-mail).

## Protección del correo de voz

Puede usar la mensajería unificada para usar Active Directory Rights Management Services (AD RMS) para proteger los mensajes de voz de una organización. Esta característica se conoce como correo de voz protegido. Cuando un mensaje de voz está protegido, no solo se impide que el destinatario reenvíe el mensaje, sino que la mensajería unificada garantiza que solo los destinatarios designados tienen acceso al contenido del mensaje. Puede tener acceso a los mensajes de voz protegidos mediante Microsoft Outlook 2010 o posterior, Outlook Web App o Outlook Voice Access. Para obtener información detallada, consulte [Protección del correo de voz](protect-voice-mail-exchange-2013-help.md).

## TLS mutua para MU

Para usar TLS mutua para cifrar el tráfico SIP y el Protocolo de transporte en tiempo real (RTP) que envían y reciben los servidores de buzones de correo y de acceso de cliente, realice las siguientes tareas:

  - Ejecute el Asistente para certificados de Exchange. Para obtener información detallada, consulte [Implementación de certificados para mensajería unificada](deploying-certificates-for-um-exchange-2013-help.md).

  - Importe el certificado de los servidores de buzones de correo y de acceso de cliente.

  - Importe los certificados necesarios a las puertas de enlace VoIP e IP PBX y a los servidores de buzones de correo y de acceso de cliente de la organización.

  - Configure la seguridad de VoIP en los planes de marcado de MU. Para obtener información detallada, consulte [Establecer la configuración de seguridad de VoIP](https://docs.microsoft.com/es-es/exchange/recipients-in-exchange-online/manage-user-mailboxes/manage-user-mailboxes).

  - Configure el modo de inicio en los servidores de buzones de correo y de acceso de cliente. Para obtener información detallada, consulte [Configurar el modo de inicio en un servidor de buzones](configure-the-startup-mode-on-a-mailbox-server-exchange-2013-help.md) y [Configurar el modo de inicio en un servidor de acceso de cliente](configure-the-startup-mode-on-a-client-access-server-exchange-2013-help.md).

  - Configure las puertas de enlace IP de MU para que escuchen en el puerto 5061. Para obtener información detallada, consulte [Configurar el puerto de escucha](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/connect-voice-mail-system/configure-listening-port).

## Establecer directivas de PIN para usuarios habilitados para mensajería unificada

En la mensajería unificada, las directivas de PIN se definen y se configuran en una directiva de buzón de mensajería unificada. Cuando se habilita a un usuario para la mensajería unificada, se lo asocia a una directiva de buzón de mensajería unificada existente. Las directivas de PIN de MU que se configuran en la directiva de buzón de MU deben basarse en los requisitos de seguridad de la organización. Para obtener más información acerca del modo de configurar el PIN para usuarios habilitados para mensajería unificada, consulte [Configurar la seguridad del PIN de Outlook Voice Access](https://docs.microsoft.com/es-es/exchange/collaboration-exo/public-folders/set-up-public-folders).

## Configurar características de correo de voz de cliente

Después de haber implementado los servidores y los componentes necesarios de mensajería unificada, hay varias características relacionadas con el correo de voz opcionales que puede configurar. Para obtener más información al respecto, vea lo siguiente:

  - [Configuración de Outlook Voice Access](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/connect-voice-mail-system/delete-um-hunt-group)

  - [Permitir usuarios de mail reenviar llamadas de voz](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/set-up-client-voice-mail-features/allow-voice-mail-users-to-forward-calls)

  - [Permitir a los usuarios ver una transcripción de correo de voz](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/set-up-client-voice-mail-features/disable-missed-call-notifications)

  - [Permitir que los usuarios de correo de voz reciban faxes](enable-voice-mail-users-to-receive-faxes-exchange-2013-help.md)


> [!IMPORTANT]
> Si está integrando su entorno de mensajería unificada en Microsoft Lync Server, hay que añadir más consideraciones en la planificación. Para obtener información detallada, consulte <A href="deploying-exchange-2013-um-and-lync-server-overview-exchange-2013-help.md">Resumen de implementación de Mensajería unificada de Exchange 2013 y Lync Server</A>.



Antes de implementar

