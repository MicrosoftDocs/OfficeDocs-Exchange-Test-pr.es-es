---
title: 'Administrar un plan de marcado de mensajería unificada: Exchange Online Help'
TOCTitle: Administrar un plan de marcado de mensajería unificada
ms:assetid: a89735e4-36ec-49fb-ad0f-192fad37e801
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb124090(v=EXCHG.150)
ms:contentKeyID: 49895825
ms.date: 04/27/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Servers.UnifiedMessaging.DialPlanGeneralPropertyPage
ms.translationtype: HT
---

# Administrar un plan de marcado de mensajería unificada

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2018-04-26_

Después de crear un plan de marcado de mensajería unificada (UM), es posible ver y configurar una amplia variedad de opciones. Por ejemplo, es posible configurar el nivel de seguridad de voz sobre IP (VoIP), el códec de audio y las restricciones de marcado. Las opciones que configure en el plan de marcado de mensajería unificada afectarán a los usuarios que estén enlazados al plan de marcado a través de la directiva de buzones de correo de mensajería unificada.

Para otras tareas de administración relacionadas con los planes de marcado de mensajería unificada, consulte [Procedimientos de plan de marcado de mensajería unificada](um-dial-plan-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el la entrada "Planes de marcado de mensajería unificada" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Uso de la EAC para ver o establecer las configuraciones del plan de marcado de mensajería unificada

1.  En la EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**.

2.  En la vista de lista, seleccione el plan de marcado de mensajería unificada que desee ver o modificar y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Plan de marcado de mensajería unificada**, haga clic en **Configurar**. Utilice las opciones de configuración para ver las configuraciones del plan de marcado específico y para habilitar o deshabilitar características según lo descrito en los siguientes pasos.

4.  **General**   Use esta página para ver las configuraciones del plan de marcado específico o habilitar y deshabilitar funciones para los usuarios habilitados para la mensajería unificada:
    
      - **Nombre**   Este es el nombre con el que fue creado el plan de marcado. La longitud máxima del nombre de un plan de marcado de MU es de 64 caracteres y puede incluir espacios. No obstante, no pueden incluirse ninguno de los caracteres siguientes: " / \\ \[ \] : ; | = , + \* ? \< \>.
    
      - Aunque es posible incluir espacios en el nombre de un plan de marcado de mensajería unificada, si integra la mensajería unificada en Office Communications Server 2007 R2 o Microsoft Lync Server, el nombre del plan de marcado no podrá contener espacios. Por lo tanto, si ha creado un plan de marcado con espacios en el nombre para mostrar y está integrándolo con Office Communications Server 2007 R2 o Lync Server, primero tendrá que eliminar el plan de marcado y, a continuación, crear otro plan de marcado que no incluya espacios en el nombre para mostrar.
        

        > [!IMPORTANT]
        > Aunque en el cuadro del nombre del plan de marcado se pueden escribir hasta 64 caracteres, el nombre no debe tener más de 49 caracteres. Si intenta crear un nombre de plan de marcado que contenga más de 49 caracteres, recibirá un mensaje de error. Este mensaje le informará de que no es posible generar la directiva de buzones de correo de mensajería unificada porque el nombre del plan de marcado es demasiado largo. Esto ocurre porque, como ya hemos mencionado, al crear un plan de marcado también se crea una directiva de buzones de correo de mensajería instantánea predeterminada con el nombre Directiva predeterminada <EM>&lt;DialPlanName&gt;</EM>. Cuando se agregan los 15 caracteres de la Directiva predeterminada al nombre del plan de marcado, el total supera el límite establecido. El parámetro <EM>name</EM> tanto para el plan de marcado de MU como para la directiva de buzones de MU puede tener un máximo de 64 caracteres. No obstante, si el nombre del plan de marcado tiene más de 49 caracteres, el nombre de la directiva de buzones de MU tendrá más de 64 caracteres y el sistema no lo permitirá.

    
      - **Longitud de la extensión (dígitos)**   Este es el número de dígitos en los números de extensión para los usuarios que están asociados a este plan de marcado. Por ejemplo, si un usuario asociado a un plan de marcado determinado marca una extensión de 4 dígitos para llamar a otro usuario del mismo plan, debe seleccionar 4 como el número de dígitos de la extensión.
        
        El número de dígitos para números de extensión se basa en el plan de marcado de telefonía que se crea en un IP PBX o PBX. Este campo es obligatorio y tiene un intervalo de valores de 1 a 20. La longitud de extensión estándar es de 3 a 7 dígitos. Si el entorno de telefonía existente incluye números de extensión, debe especificar el número de dígitos de dichas extensiones al crear el plan de marcado de mensajería unificada.
    
      - **Tipo de plan de marcado**   Un Identificador uniforme de recursos (URI) es una cadena de caracteres que identifica o da nombre a un recurso. La finalidad principal de esta identificación es habilitar dispositivos VoIP y PBX para la comunicación con otros dispositivos a través de una red mediante protocolos específicos. Los URI se definen en esquemas, que a su vez definen una sintaxis y un formato concretos, así como los protocolos para la llamada. En pocas palabras, este formato se transfiere desde el IP PBX o la PBX y el tipo de plan de marcado que se vaya a crear deberá coincidir con este formato. Después de crear un plan de marcado de mensajería unificada, no podrá cambiar el tipo de plan; deberá eliminarlo y volver a crear un plan de marcado con el tipo correcto. Puede seleccionar uno de los tipos de plan de marcado siguientes:
        
          - **Extensión telefónica**   Es el tipo de plan de marcado más frecuente. La información sobre la parte llamante y la llamada desde la puerta de enlace VolP o IP PBX se indica en uno de los formatos siguientes: Tel.: 512345 ó 512345@\<*Dirección IP*\>. Se trata del tipo predeterminado para planes de marcado.
        
          - **URI de SIP**   Use este tipo de plan de marcado si debe tener un plan de marcado de protocolo de inicio de sesión (SIP), como IP PBX (que admite el enrutamiento SIP), PBX con SIP habilitado o bien si integra Microsoft Office Communications Server 2007 R2 o el servidor Microsoft Lync y la mensajería unificada. La información sobre la parte llamante y la llamada desde la puerta de enlace VolP. IP PBX, PBX con SIP habilitado o Communications Server 2007 R2 o Lync Server está listado como una dirección SIP en el siguiente formato: sip:\<*nombre de usuario*\>@\<*dominio* o *dirección IP*\>:puerto.
        
          - **E.164**   E.164 es un plan de numeración internacional para sistemas de teléfono público en el que cada número asignado incluye un código de país, un código de destino nacional y un número de suscriptor. La información del autor y del destinatario de la llamada enviada desde la puerta de enlace VolP, IP PBX o PBX se indica en el formato siguiente: Tel.:+14255550123.
        

        > [!NOTE]
        > Después de crear un plan de marcado, no podrá cambiar el tipo de plan; deberá eliminarlo y volver a crear un plan de marcado con el tipo correcto.

    
      - **Modo de seguridad VoIP**   Use esta lista desplegable para elegir la configuración de seguridad de VoIP para el plan de marcado de mensajería unificada. Puede elegir una de las configuraciones de seguridad siguientes para el plan de marcado:
        
          - **No protegido**   De manera predeterminada, cuando crea un plan de marcado de mensajería unificada, está establecido para no cifrar la señalización de SIP o el tráfico de RTP. En modo No protegida, el servidor Exchange asociado con el plan de marcado de mensajería unificada envía y recibe datos de puertas de enlace VoIP, IP PBX, SBC y otros servidores Exchange que no usan cifrado. En modo no protegido, no se cifra ni el canal de medios del protocolo de transporte en tiempo real (RTP) ni la información de señalización de SIP.
        
          - **SIP seguro**   Cuando se elige **SIP seguro**, solo se cifra el tráfico de señalización de SIP, mientras que los canales de medios RTP seguirán utilizando TCP, que no está cifrado. Con SIP protegido, la Seguridad de la capa de transporte mutua (MTLS) se utiliza para cifrar el tráfico de señalización SIP y los datos VolP.
        
          - **Protegida**    Al seleccionar **Protegida**, se cifran tanto el tráfico de señalización SIP como los canales de medios RTP. El canal de medios de señalización seguro que usa el Protocolo de transporte en tiempo real seguro (SRTP) y el tráfico de señalización SIP también usará la TLS mutua para cifrar los datos de VoIP.

5.  **Códigos de marcado**   Use esta página para configurar los códigos de marcado de un plan de marcado de mensajería unificada. Se pueden configurar varios códigos de marcado en un plan de marcado. Incluyen opciones de llamadas entrantes y salientes. Se pueden realizar las siguientes configuraciones:
    
      - **Códigos de marcado para las llamadas salientes**   Use estas configuraciones para especificar los códigos de marcado para las llamadas salientes que pueden realizar los usuarios habilitados para mensajería unificada. Estas llamadas salientes son llamadas que se realizan mediante el uso de Outlook Voice Access o desde un mensaje de correo de voz.
        
          - **Código de acceso a línea externa**   Use este campo para escribir el número o números que se usan para tener acceso a un número de teléfono externo para llamadas externas salientes. Este número se antepondrá al número de teléfono que se marque. También se conoce como un código de acceso troncal. Este campo acepta de 1 a 16 dígitos. Para muchas organizaciones, este número es 9. De forma predeterminada, este campo está vacío.
            
            A menudo, esta configuración se usa en entornos de telefonía que disponen de PBX o IP PBX in situ o que se mantienen en una organización. Puede que no se tenga que configurar si una compañía o proveedor externo se encarga del entorno de telefonía de la organización.
        
          - **Código de acceso internacional**   Use este campo para escribir el código que se usa para tener acceso a números de teléfono internacionales para llamadas externas. Este número se antepondrá al número de teléfono que se marque. De forma predeterminada, este campo no está lleno. Este campo acepta de 1 a 4 dígitos. Por ejemplo, el código de acceso internacional para Estados Unidos es 011; para Europa, es 00.
        
          - **Prefijo numérico nacional**   Use este campo para escribir el código que se usa para marcar números de teléfono fuera de un código de área dentro del país/región. Este número se antepondrá al número de teléfono que se marque. De forma predeterminada, este campo no está lleno. Este campo acepta de 1 a 4 dígitos. Por ejemplo, 0 se usa en Europa y 1 en Norteamérica.
        
          - **Código de país o región**   Use este campo para escribir el código de país o región que se usa para llamadas salientes. Este número se antepondrá al número de teléfono que se marque. De forma predeterminada, este campo no está lleno. Este campo acepta de 1 a 4 dígitos. Por ejemplo, en Estados Unidos el código de país o región es 1. En el Reino Unido es 44.
    
      - **Formatos de número para marcar entre planes de marcado de mensajería unificada**   Use estas configuraciones para configurar las llamadas entre los usuarios de planes de marcado separados cuando realicen llamadas entre los planes de marcado.
        
          - **Formato de número nacional/regional**   Use este campo para especificar cómo debe marcar el servidor Exchange un número de teléfono de un usuario en un plan de marcado diferente, pero con el mismo código de país. Esto se usa con operadores automáticos o cuando un usuario de Outlook Voice Access busca un usuario en el directorio e intenta llamarlo.
            
            La entrada consiste en un prefijo numérico y un número variable de caracteres (por ejemplo: 020*xxxxxxx*). Para determinar el número de teléfono, la mensajería unificada anexará los últimos *x* dígitos del número de teléfono especificado en el directorio al prefijo especificado.
        
          - **Formato de número internacional**   Use este campo para especificar cómo debe marcar la mensajería unificada un número de teléfono de un usuario en planes de marcado diferentes con códigos de país diferentes. Esto se usa con operadores automáticos o cuando un usuario de Outlook Voice Access busca un usuario en el directorio e intenta llamarlo.
            
            Esta entrada está compuesta de un prefijo numérico y un número variable en cuanto a caracteres (por ejemplo, 4420*xxxxxxx*). Para determinar el número de teléfono, la mensajería unificada anexará los últimos *x* dígitos del número de teléfono que se especifica en el directorio al prefijo indicado.
        
          - **Formatos de números para llamadas entrantes dentro del mismo plan de marcado**   Use este campo para agregar o quitar un formato de número de las llamadas entrantes que se realizan entre los usuarios en el mismo plan de marcado. Este campo acepta números y la letra “x” como carácter comodín. No se puede utilizar ninguna otra letra en este campo.
            
            Para las llamadas entrantes en el mismo plan de marcado, se agrega un formato de número. Por ejemplo: para agregar un formato de número de extensiones de 5 dígitos, ingrese 142570xxxxx y haga clic en ![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono"). Para eliminar un formato de número, haga clic en ![Icono de quitar](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icono de quitar").

6.  **Outlook Voice Access**   Use esta página para establecer las configuraciones de Outlook Voice Access para el plan de marcado de mensajería unificada. Outlook Voice Access permite que los usuarios obtengan acceso a sus buzones personales para recuperar correos electrónicos, mensajes de voz, contactos e información del calendario mediante un teléfono. Puede ver o configurar lo siguiente:
    
      - **Saludo de bienvenida**   Este campo de solo lectura muestra el nombre del archivo de sonido que se usará para el saludo de bienvenida.
        
          - **Saludo predeterminado**   El saludo de bienvenida se usa cuando un usuario de Outlook Voice Access u otro autor de la llamada llama al número de Outlook Voice Access y hace una búsqueda de directorio. Este archivo de audio es el saludo predeterminado de un plan de marcado de mensajería unificada. Sin embargo, es posible que desee cambiar este saludo de bienvenida por otro específico de su empresa, como "Bienvenido a Outlook Voice Access para Contoso, Ltd."
            
            Si decide personalizar este saludo, primero debe grabar un saludo personalizado, guardarlo como archivo .wav y luego configurar el plan de marcado para que use este saludo personalizado. El nombre de archivo y la ruta no pueden superar los 255 caracteres.
            
            Puede agregar un saludo personalizado al hacer clic en **Cambiar** y luego en **Explorar** para seleccionar un saludo personalizado grabado anteriormente y especificar el archivo de audio (.wav) que se utilizará para el saludo de bienvenida. Si no especifica ningún archivo de audio, los usuarios de Outlook Voice Access que llamen escucharán un saludo de bienvenida predeterminado que dice: "Bienvenido, se ha conectado a Microsoft Exchange."
    
      - **Mensaje informativo**   Cuando está habilitada, esta grabación opcional se reproduce inmediatamente después del saludo de bienvenida de horario comercial y no comercial. Un mensaje informativo puede indicar las directivas de seguridad de la organización para acceder al sistema, por ejemplo: "Cuando acceda a nuestro sistema mediante el uso de Outlook Voice Access estará de acuerdo con los términos de nuestro contrato de negocio y todas las directivas de seguridad de nuestra organización que apliquen. El acceso a nuestro sistema está monitoreado y si accede ilegalmente será penado." Un anuncio informativo puede proporcionar también información necesaria para el cumplimiento de las directivas de la empresa, por ejemplo: “Se pueden controlar las llamadas con fines formativos.” Si es importante que las personas que llaman escuchen todo el mensaje informativo, puede marcarlo como ininterrumpible.
        
        De forma predeterminada, no hay ningún mensaje informativo configurado en los planes de marcado de mensajería unificada. Para habilitar un mensaje informativo y usar un archivo de audio personalizado específico de su organización, haga clic en **Cambiar** y luego en **Explorar**.
    
      - **Permitir la interrupción del anuncio**   Seleccione esta casilla para permitir que el usuario de Outlook Voice Access interrumpa el mensaje informativo. Debe hacer esto si tiene anuncios informativos largos. Los usuarios de Outlook Voice Access se pueden frustrar si el mensaje informativo es largo y pueden interrumpirlo para acceder a las opciones proporcionadas por el plan de marcado de mensajería unificada.
    
      - **Números de Outlook Voice Access**   Use este campo para agregar un número de teléfono o extensión o un URI de SIP al que llamará el usuario de Outlook Voice Access para acceder al sistema de correo de voz mediante el uso de Outlook Voice Access. En la mayoría de casos, escribirá un número de extensión o un número de teléfono externo. Sin embargo, debido a que este campo acepta todos los caracteres alfanuméricos, se puede usar un SIP de URI si está usando IP PBX, Office Communications Server 2007 R2 o Microsoft Lync Server.
        
        De forma predeterminada, cuando se crea un plan de marcado, no se definen números de Outlook Voice Access. Para habilitar usuarios de Outlook Voice Access para que llamen a Outlook Voice Access, debe configurar por lo menos un número de teléfono. El número de caracteres alfanuméricos no puede superar los 20.
        
        Cuando configure este número en el plan de marcado, el número se visualizará en Microsoft Office Outlook 2007 o versiones posteriores y Outlook Web App para las opciones de correo de voz.
        
        Para agregar un nuevo número de Outlook Voice Access, ingrese el número en la casilla y haga clic en ![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono"). Para eliminar un número de Outlook Voice Access, haga clic en ![Icono de quitar](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icono de quitar").

7.  **Configuraciones**   Use esta página para establecer las configuraciones del plan de marcado para la mensajería unificada. Cuando establezca las configuraciones en esta página, puede controlar cómo van a llamar los usuarios de Outlook Voice Access y los autores de llamadas externos a un operador automático vinculado al plan de marcado para localizar a los usuarios en la organización, el códec de audio que se utiliza para los mensajes de correo de voz, el número de intentos fallidos de inicio de sesión y los valores de tiempo de espera. Se pueden realizar las siguientes configuraciones:
    
      - **Forma principal de buscar nombres**   Use esta lista para seleccionar la forma principal en que los autores de llamadas pueden localizar a un usuario cuando marquen en el sistema.
        
        De forma predeterminada, la opción **Apellido Nombre** está seleccionada. Esto significa que, cuando los usuarios busquen a otro usuario en el directorio, escribirán primero el apellido de ese usuario y, a continuación, su nombre.
        
        Cuando un usuario de Outlook Voice Access llama a un número de Outlook Voice Access para acceder a su buzón de correo, un llamante llama a un número de Outlook Voice Access para realizar una búsqueda de directorio, o un llamante llama a un operador automático vinculado a un plan de marcado de mensajería unificada, pueden buscar a un usuario en el directorio indicando su nombre o alias.
        
        Debe seleccionar uno de los métodos permitidos para poder utilizar el método principal de marcado por nombre. Se permiten los métodos siguientes:
        
          - **Apellidos Nombre (opción predeterminada)**
        
          - **Nombre Apellidos**
        
          - **Dirección SMTP**
    
      - **Forma secundaria de buscar nombres**   Use esta lista para seleccionar la forma secundaria en que los autores de llamadas pueden localizar a un usuario cuando marquen en el sistema.
        
        La opción seleccionada de forma predeterminada es **Dirección SMTP**. Esto significa que cuando los usuarios busquen a un usuario en el directorio, ingresarán el alias de correo electrónico o la dirección SMTP del usuario.
        
        Cuando un usuario de Outlook Voice Access llama a un número de Outlook Voice Access para acceder a su buzón de correo, un llamante llama a un número de Outlook Voice Access para realizar una búsqueda de directorio, o un llamante llama a un operador automático vinculado a un plan de marcado de mensajería unificada, pueden buscar a un usuario en el directorio indicando su nombre o alias. Cuando seleccione una de estas opciones, los autores de llamadas pueden usar la forma principal o la forma secundaria para buscar nombres para así localizar los usuarios en el directorio.
        
        No es necesario seleccionar uno de los cuatro métodos permitidos. Sin embargo, si no selecciona una forma secundaria de buscar usuario, a los autores de llamadas solamente se les proporcionará una forma de buscar un usuario. Están disponibles las opciones siguientes:
        
          - **Apellidos Nombre**
        
          - **Nombre Apellidos**
        
          - **Dirección SMTP** (predeterminado)
        
          - **Ninguno**
    
      - **Códec de audio**   Utilice esta lista para seleccionar el códec de audio que se empleará en el plan de marcado. Cuando un autor de la llamada realiza una llamada a un usuario que está asociado a un plan de marcado y deja un mensaje de voz, la mensajería unificada utiliza el códec de audio seleccionado en esta lista para grabar los mensajes de voz que se enviarán a los usuarios que tengan habilitado el correo de voz. Se permiten los códecs de audio siguientes:
        
          - **MP3** (predeterminado)
        
          - **WMA** (Windows Media Audio)
        
          - **G711** (PCM Linear)
        
          - **GSM** (Group System Mobile 06.10)
        
        El formato MP3 está seleccionado de forma predeterminada. El formato MP3 es un formato de archivo de audio habitual que se usa para reducir considerablemente el tamaño de los archivos de audio; se trata del formato de audio que usan la mayoría de dispositivos de audio personales y reproductores MP3. MP3 es un códec de audio multiplataforma que se usa para obtener compatibilidad con una amplia variedad de teléfonos móviles, dispositivos y sistemas operativos.
        
        Se utiliza WMA porque está muy comprimido y tiene propiedades de formato de alta calidad. G.711 PCM Linear es un formato de códec de audio de calidad telefónica que es la menos comprimida y tiene el formato de calidad inferior. El formato de códec de audio GSM 06.10 es el estándar utilizado por los fabricantes de teléfonos móviles y las operadoras de telefonía móvil.
        
        Si prevé que el espacio de disco asignado a los usuarios puede ser un problema, seleccione WMA. Los archivos de voz guardados en formato .wma ocupan aproximadamente la mitad que las grabaciones realizadas con cualquier otro códec de audio.
    
      - **Extensión de operador**   Use este cuadro de texto para escribir el número de teléfono o la extensión correspondiente al operador del plan de marcado. Es diferente de una extensión de operador que está configurado en un operador automático de mensajería unificada. Sin embargo, puede colocar en el mismo número de teléfono o extensión ambos tipos de operadores.
        
        Si configura esta opción, podrá transferir llamadas a un operador automático (si tiene uno configurado) a un operador humano, a un número de teléfono externo o a una extensión.
        
        Cuando alguien realiza una llamada usando un teclado telefónico y presiona 0, o dice "recepción" u "operador", o supera el umbral del **Número de errores de entrada antes de desconectar**, la llamada se transferirá al número de teléfono o extensión que especifique en este cuadro de texto.
        
        Este número de teléfono puede ser uno externo a la organización o una extensión interna. Si, por ejemplo, el número de extensión del recepcionista u operador es 81964 y su organización tiene un solo plan de marcado, escriba 81964.
        
        De manera predeterminada, esta opción está en blanco. Si no escribe ningún número en este cuadro de texto, la función de transferir llamadas al operador quedará desactivada y las personas que llamen recibirán un aviso de que se las debe desconectar porque no hay nadie para atender la llamada.
        
        Se recomienda rellenar este cuadro de texto con un número de teléfono para transferir a un operador aquellas llamadas en las que no sea posible localizar a un usuario determinado en el directorio.
    
      - **Número de errores de inicio de sesión antes de desconectar**   Use este cuadro de texto para ingresar el número de errores de inicio de sesión secuenciales permitidos antes de que se desconecte al autor de llamada.
        
        El valor de este parámetro puede estar entre 1 y 20. Si configura un valor demasiado bajo, puede frustrar a los usuarios. Para la mayoría de las organizaciones, este valor se debería establecer en los tres intentos predeterminados.
    
      - **Períodos de espera y reintentos**   Estas configuraciones aplican para los usuarios de Outlook Voice Access y los autores de llamadas externos que llaman al operador automático de mensajería unificada.
        
          - **Duración máxima de la llamada (minutos)**   Use este cuadro de texto para ingresar el número máximo de minutos que puede estar conectada una llamada entrante en el sistema sin que sea transferida a un número de extensión válido antes de que finalice la llamada. Para la mayoría de las organizaciones, este valor se debería establecer en los 30 minutos.
            
            Esta opción se aplica a todo tipo de llamadas. Esto incluye las llamadas entrantes de Outlook Voice Access, las llamadas de voz internas de la organización y las llamadas de voz y fax externas a la organización.
            
            El valor de este parámetro puede estar entre 10 y 120. Si configura este valor demasiado bajo, puede provocar que las llamadas entrantes se desconecten antes de completarse. Por ejemplo, si su organización recibe muchos mensajes de fax de larga duración, puede que le interese aumentar este valor del predeterminado para así recibir todas las páginas de los mensajes de fax.
        
          - **Duración máxima de grabación (minutos)**   Use este cuadro de texto para ingresar el número máximo de minutos permitidos para cada grabación de voz cuando un autor de la llamada deja un mensaje de correo de voz. Para la mayoría de las organizaciones, este valor se debería establecer en los 20 minutos.
            
            El valor de este parámetro se encuentra entre 1 y 100. Si configura este valor demasiado bajo, es posible que los mensajes de voz largos se desconecten antes de completarse. Si especifica un valor demasiado alto, los usuarios podrán guardar mensajes de voz de larga duración en su bandeja de entrada.
            
            Esta opción es importante si ha fijado cuotas de disco muy estrictas para los usuarios. Este valor debe ser menor que el valor establecido para la configuración **Duración máxima de la llamada (minutos)**.
        
          - **Tiempo de espera de inactividad de grabación (segundos)**   Use este cuadro de texto para ingresar el número de segundos de silencio que permite el sistema cuando se está grabando un mensaje de voz antes de que finalice la llamada. Para la mayoría de las organizaciones, este valor se debería establecer en los 5 segundos predeterminados.
            
            El valor de este parámetro puede estar entre 2 y 10. Si configura este valor demasiado bajo, puede provocar que el sistema desconecte a los que realicen llamadas antes de que dejen sus mensajes de voz. Si especifica un valor demasiado alto, los mensajes podrían incluir silencios prolongados.
        
          - **Número de errores de entrada antes de desconectar**   Use este cuadro de texto para configurar el número de veces que los autores de llamadas pueden ingresar opciones de menú incorrectas antes de que sean desconectados. Para la mayoría de las organizaciones, este valor se debería establecer en los tres intentos predeterminados. Esta opción es muy importante para los planes de marcado de UM habilitados para voz.
            
            Algunos ejemplos de datos incorrectos son la solicitud de un número de extensión que no se encuentra en el sistema, que el sistema no pueda encontrar el número de extensión del usuario para transferir la llamada o que la persona que llama presione una opción de menú no válida.
            
            El valor de este parámetro puede estar entre 1 y 20. Si configura un valor demasiado bajo, puede desconectar antes de lo debido al que realiza la llamada.
    
      - **Idioma de audio**   Use esta lista para especificar el idioma predeterminado que usan los usuarios de Outlook Voice Access. Esta configuración no aplica a la configuración del idioma en un operador automático de mensajería unificada. Puede establecer que el idioma utilizado para Outlook Voice Access sea igual o diferente del idioma que se utiliza en un operador automático de mensajería unificada. Cuando un usuario realiza una llamada a un usuario vinculado a un plan de marcado, el idioma de audio es el idioma predeterminado que utiliza el operador grabado de voz. Las instrucciones del sistema también estarán en el mismo idioma. El idioma que se escoja en el plan de marcado de mensajería unificada se usará para leer el correo electrónico, el correo de voz y los elementos del calendario; decir el nombre del usuario si el saludo personal no se ha grabado; transcribir un mensaje de voz usando la característica Vista previa de correo de voz y habilitar el reconocimiento de voz automático (ASR) para trabajar correctamente.
        
        En las implementaciones locales, agregar otros idiomas permite que Outlook Voice Access use un idioma que no es el inglés de EE. UU. Por ejemplo, si un usuario de Outlook Voice Access llama a un número de Outlook Voice Access desde un teléfono de escritorio, el usuario será saludado con la voz de un operador grabada previamente en inglés. Aunque el mismo usuario seleccione un idioma distinto en Outlook Web App, como francés, los menús continuarán apareciendo en inglés (Estados Unidos). Para que el usuario pueda escuchar el mensaje de los menús en francés, es necesario instalar el paquete del idioma apropiado.
        

        > [!NOTE]
        > En Exchange Online están disponibles todos los idiomas.



8.  **Reglas de marcado**   Use esta página para especificar las reglas de marcado para llamadas nacionales/regionales e internacionales realizadas por usuarios habilitados para la mensajería unificada. Cada entrada definida en la regla de marcado determina los tipos de llamadas que pueden realizar los usuarios de un grupo de reglas de marcado específico. Después de usar la página **Reglas de marcado** para configurar las reglas de marcado, debe configurar el plan de marcado de mensajería unificada, una directiva de buzón de mensajería unificada o un operador automático de mensajería unificada para usar la regla de marcado apropiado. Después de configurar la directiva de buzón de mensajería unificada para usar un grupo de reglas de marcado, las restricciones de marcado configuradas se aplicarán a todos los usuarios habilitados de mensajería unificada que estén asociados con la directiva de buzón de mensajería unificada. Por ejemplo, puede configurar un grupo de reglas de marcado para el que no sea necesario que los usuarios asociados al plan de marcado marquen un código de acceso de línea externo cuando llamen a un número de teléfono nacional o regional. Se pueden realizar las siguientes configuraciones:
    
      - **Reglas de marcado nacionales o regionales**   Use esta casilla para agregar, quitar o editar grupos de reglas de marcado nacionales o regionales usadas por las directivas de buzón de mensajería unificada. Para crear una regla de marcado, haga clic en ![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono"). Para editar una regla existente de marcado, haga clic en ![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar"). Para quitar una regla de marcado, haga clic en ![Icono de quitar](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icono de quitar"). Cuando cree una regla de marcado, agregue la siguiente información en la página **Nueva regla de marcado**:
        
          - **Nombre de la regla de marcado**   Use el cuadro de texto para escribir el nombre de la regla de marcado que esté creando. Puede usar el mismo nombre para recopilar varias reglas en un grupo y después habilitar o deshabilitarlas en **Autorización de marcado**. El nombre puede tener hasta 32 caracteres.
        
          - **Patrón de número para transformar (máscara de número)**   Use el cuadro de texto para escribir el patrón de número para transformar antes de marcar, por ejemplo 91425xxxxxxx. Si un usuario escribe un número que coincide con el patrón, la mensajería unificada transformará el marcado del número en un número marcado antes de realizar la llamada. Sólo puede introducir números y el carácter comodín, ”x”.
        
          - **Número marcado**   Use este cuadro de texto para ingresar el número que quiere marcar que coincide con el patrón del número que estableció en el **Patrón de número para transformar (máscara de número)**. El número marcado se usa para determinar la cadena de marcado real que se envía a la puerta de enlace VoIP o a IP PBX. Este número puede ser diferente al número que obtiene la mensajería unificada para la llamada saliente. Sin embargo, la PBX o IP PBX también se puede configurar para omitir el código de área para las llamadas locales y para planes de numeración de voz privados. Todos los caracteres comodín (*x*) de la cadena de marcado se sustituyen por los dígitos del número original que coinciden con la máscara de número en la regla de marcado. Un ejemplo de un número marcado válido es 9*xxxxxxx*. Este campo solo puede contener números y el carácter *x*.
        
          - **Comentario**   Use este cuadro de texto para introducir un comentario o una descripción para la regla de marcado que esté agregando o modificando. De forma predeterminada, este cuadro de texto está en blanco.
            

            > [!NOTE]
            > Si está integrando con Office Communications Server 2007 R2 o Microsoft Lync Server, probablemente encontrará innecesario configurar reglas de marcado o grupos de reglas de marcado en mensajería unificada. Office Communications Server 2007 R2 y Lync Server están diseñados para efectuar el enrutamiento de llamadas y la traducción de los números de los usuarios de su organización y seguirán haciéndolo cuando se realicen las llamadas en nombre de los usuarios.

    
      - **Reglas internacionales**   Use este cuadro de texto para agregar, quitar o editar grupos de reglas de marcado internacional usadas por las directivas de buzón de mensajería unificada.
        
          - **Nombre de la regla de marcado**   Use el cuadro de texto para escribir el nombre de la regla de marcado que esté creando. Puede usar el mismo nombre para recopilar varias reglas en un grupo y después habilitar o deshabilitarlas en **Autorización de marcado**. El nombre puede tener hasta 32 caracteres.
        
          - **Patrón de número para transformar (máscara de número)**   Use el cuadro de texto para escribir el patrón de número para transformar antes de marcar, por ejemplo 91425xxxxxxx. Si un usuario escribe un número que coincide con el patrón, la mensajería unificada transformará el marcado del número en un número marcado antes de realizar la llamada. Sólo puede introducir números y el carácter comodín, ”x”.
        
          - **Número marcado**   Use este cuadro de texto para ingresar el número que quiere marcar que coincida con el patrón de número que estableció en **Patrón de número para transformar (máscara de número)**. El número marcado se usa para determinar la cadena de marcado real que se envía a la puerta de enlace VoIP o a IP PBX. Este número puede ser diferente al número que obtiene la mensajería unificada para la llamada saliente. Sin embargo, la PBX o IP PBX también se puede configurar para omitir el código de área para las llamadas locales y para planes de numeración de voz privados. Todos los caracteres comodín (*x*) de la cadena de marcado se sustituyen por los dígitos del número original que coinciden con la máscara de número en la regla de marcado. Un ejemplo de un número marcado válido es 9*xxxxxxx*. Este campo solo puede contener números y el carácter *x*.
        
          - **Comentario**   Use este cuadro de texto para introducir un comentario o una descripción para la regla de marcado que esté agregando o modificando. De forma predeterminada, este cuadro de texto está en blanco.
            

            > [!NOTE]
            > En las implementaciones locales, si está integrando con Office Communications Server 2007 R2 o Microsoft Lync Server, probablemente encontrará innecesario configurar reglas de marcado o grupos de reglas de marcado en mensajería unificada. Office Communications Server 2007 R2 o Lync Server están diseñados para efectuar el enrutamiento de llamadas y la traducción de los números de los usuarios de su organización y seguirán haciéndolo cuando se realicen las llamadas en nombre de los usuarios.



9.  **Autorización de marcado**   Use esta página para seleccionar las reglas de marcado para los autores de llamadas que llaman a un número de Outlook Voice Access configurado en un plan de marcado de mensajería unificada. Puede restringir el tipo de llamadas que se realizan cuando un usuario no autenticado o un usuario de Outlook Voice Access llama a un número de Outlook Voice Access que esté configurado en un plan de marcado, mediante la configuración de grupos de reglas y de restricciones de marcado. Se pueden realizar las siguientes configuraciones:
    
      - **Llamadas en el mismo plan de marcado de mensajería unificada**   Active esta casilla para permitir a los usuarios que llamen a un número de Outlook Voice Access configurado en un plan de marcado, que llamen o transfieran llamadas a un número de extensión asociado a un usuario con mensajería unificada habilitada que se encuentre dentro del mismo plan de marcado. Esta opción está habilitada de forma predeterminada.
        
        Cuando se deshabilite esta opción, los usuarios que llamen al número de Outlook Voice Access no podrán realizar ni transferir llamadas a ningún usuario sin la mensajería unificada habilitada, a otros números de extensión o a usuarios con la mensajería unificada habilitada asociados al mismo plan de marcado. Esto se debe a que la opción **Permitir llamadas a cualquier extensión** está deshabilitada de forma predeterminada.
    
      - **Permitir llamadas a cualquier extensión**   Cuando esta opción está deshabilitada, los usuarios que llamen a un número de Outlook Voice Access del plan de marcado no pueden efectuar llamadas a usuarios sin la mensajería unificada habilitada o a otros números de extensión no asociados a un usuario con la mensajería unificada habilitada. Sin embargo, pueden realizar una llamada o transferirla a números de extensión asociados con usuarios habilitados para mensajería unificada. Esto se debe a que la configuración de **Llamadas en el mismo plan de marcado de mensajería unificada** está habilitada de forma predeterminada. De forma predeterminada, la opción **Permitir llamadas a cualquier extensión** está deshabilitada.
        
        Cuando esta opción está habilitada, los usuarios que llamen a un número de Outlook Voice Access configurado en el plan de marcado pueden realizar llamadas a usuarios sin mensajería unificada habilitada, a otros números de extensión no asociados a un usuario con mensajería unificada habilitada y a usuarios habilitados para mensajería unificada. Esto se debe a que la configuración de **Llamadas en el mismo plan de marcado de mensajería unificada** está habilitada de forma predeterminada.
        
        Puede habilitar esta opción en un entorno en el que no se hayan habilitado todos los usuarios para mensajería unificada. Esta opción también resulta útil si desea dar a los usuarios que llamen a un número de Outlook Voice Access configurado en un plan de marcado la opción de llamar a números de extensión que no estén asociados.
    
      - **Grupos de reglas de marcado nacionales/regionales autorizados**   Use esta sección para agregar o quitar grupos de reglas de marcado nacionales o regionales permitidos. De forma predeterminada, no existen grupos de reglas de marcado nacionales ni regionales configurados en los planes de marcado de mensajería unificada.
        
        Los grupos de reglas de marcado nacionales o regionales se utilizan para permitir o restringir los números de teléfono dentro de un país o región que puede marcar cualquier usuario que haya marcado el número de acceso de suscriptor. Esto ayuda a evitar llamadas de teléfono y gastos innecesarios o no autorizados.
        
        Para agregar grupos de reglas de marcado nacionales o regionales, es necesario crear primero los grupos de reglas de marcado nacionales o regionales en el plan de marcado apropiado y, a continuación, agregar las entradas de las reglas de marcado correspondientes en la regla de marcado. Después de crear las reglas de marcado necesarias en el plan de marcado, es necesario agregar la regla de marcado a la lista de autorizaciones de marcado en la página **Autorización de marcado** del plan de marcado.
        
        Se pueden usar los grupos de reglas de marcado nacionales o regionales para permitir o restringir el acceso a números de teléfono dentro de un país o región. Esto se aplica a todos los usuarios que hayan llamado a un número de acceso de Outlook Voice Access.
    
      - **Grupos de reglas de marcado internacional autorizados**   Use esta sección para agregar o quitar las reglas de marcado internacional permitidas. De forma predeterminada, no hay grupos de reglas de marcado internacionales configurados en los planes de marcado de mensajería unificada.
        
        Los grupos de reglas de marcado internacionales se usan para permitir o restringir los números de teléfono fuera de un país o región que puede marcar cualquier usuario que haya marcado el número de Outlook Voice Access. Esto ayuda a evitar llamadas de teléfono y gastos innecesarios o no autorizados.
        
        Para agregar grupos de reglas de marcado internacional, es necesario crear primero los grupos de reglas de marcado internacional en el plan de marcado y, a continuación, agregar las entradas de las reglas de marcado correspondientes. Después de crear las reglas de marcado necesarias en el plan de marcado, es necesario agregar la regla de marcado a la lista de autorizaciones de marcado en la página **Autorización de marcado** del plan de marcado.
        
        Los grupos de reglas de marcado internacionales se pueden usar para permitir o restringir el acceso a números de teléfono fuera de un país o de una región. Esto se aplica a todos los usuarios que hayan llamado a un número de acceso de Outlook Voice Access.

10. **Transferir y \&buscar**   Use esta página para configurar las características del plan de marcado de mensajería unificada. Pueden configurarse varias funciones en el plan de marcado de UM. Estos incluyen la transferencia de llamadas, el envío de mensajes de voz y la búsqueda de usuarios. Se pueden realizar las siguientes configuraciones:
    
      - **Permitir que los autores de llamadas**   Use estas opciones para determinar cómo se van a comunicar los usuarios que llamen a un número de Outlook Voice Access con los usuarios. Se pueden realizar las siguientes configuraciones:
        
          - **Transferir a los usuarios**   Seleccione esta casilla para habilitar a los usuarios de Outlook Voice Access para que transfieran llamadas a los usuarios. Esta opción está habilitada de manera predeterminada. Permite a los usuarios asociados con el plan de marcado transferir llamadas a usuarios del mismo plan de marcado UM. Después de marcar esta casilla, puede establecer el grupo de usuarios que los autores de llamadas pueden buscar seleccionando la opción adecuada en la sección **Permitir a los autores de llamadas buscar usuarios por nombre o alias** de esta página.
            
            Si deshabilita esta opción, Outlook Voice Access no permitirá que los autores de llamadas se transfieran a ningún usuario en el plan de marcado.
        
          - **Dejar mensajes de voz sin que el teléfono de un usuario suene**   Seleccionar esta casilla para permitir que los autores de llamadas envíen mensajes de voz a los usuarios. Esta opción está habilitada de manera predeterminada. Permite a los usuarios de Outlook Voice Access asociados con el plan de marcado enviar mensajes de voz a usuarios del mismo plan de marcado de mensajería unificada. Después de marcar esta casilla, puede establecer el grupo de usuarios que los autores de llamadas pueden buscar seleccionando la opción adecuada en la sección **Permitir a los autores de llamadas buscar usuarios por nombre o alias** de esta página.
            
            Si deshabilita esta opción, Outlook Voice Access no invitará a los autores de llamada a enviar un mensaje de voz durante el mensaje del sistema.
    
      - **Permitir a los autores de llamadas buscar usuarios por nombre o alias**   Use estas opciones para determinar los grupos de usuarios que se pueden buscar. La opción **En este plan de marcado únicamente** está seleccionada de manera predeterminada. Sin embargo, puede cambiar la agrupación de usuarios. Seleccione una de las opciones siguientes:
        
          - **En este plan de marcado únicamente**   Use esta opción para permitir que los autores de llamadas que se conecten a Outlook Voice Access ubiquen y se comuniquen con los usuarios que están dentro del plan de marcado del que ellos son miembros.
        
          - **En toda la organización**   Use esta opción para permitir que los autores de llamadas que se conecten con Outlook Voice Access ubiquen y se comuniquen con cualquier persona que esté listada en toda la organización. Esto incluye a todos los usuarios que son usuarios habilitados para los buzones de correo o los usuarios habilitados para la mensajería unificada en todos los planes de marcado.
        
          - **Solo en este operador automático**   Use esta lista para permitir a los usuarios de Outlook Voice Access que se conecten con un operador automático de mensajería unificada y después se conecten con otro operador automático que haya configurado. Debe crear este operador automático para permitir a las personas que llaman ser transferidas a otro operador automático indicado.
        
          - **Solo para esta extensión**   Use esta opción para permitir a los usuarios de Outlook Voice Access que se conecten con un número de extensión que usted haya indicado en el campo de esta opción. Este campo solo acepta números. El número de dígitos que defina en este campo debe coincidir con el número de dígitos configurados en el plan de marcado asociado con el operador automático.
    
      - **Información para incluir para usuarios con el mismo nombre**   Use este campo para seleccionar cómo diferencia el plan de marcado a los usuarios que tienen el mismo nombre o nombres similares. Cuando un autor de la llamada debe escribir letras o decir el nombre de una persona para encontrar a un usuario particular de la organización, a veces coincide más de un nombre con la entrada del autor de la llamada. Si hay dos usuarios con el mismo nombre, la mensajería unificada usa una de las siguientes maneras de agregar información adicional al nombre de usuario. Por ejemplo, si selecciona **Departamento**, cuando un usuario de Outlook Voice Access llama a Outlook Voice Access y busca un usuario y hay nombres duplicados o similares en el directorio, el autor de la llamada escuchará el nombre y el departamento del usuario por ejemplo:
        
        1.  Sistema: “Bienvenido a Outlook Voice Access. Ingrese su PIN y presione almohadilla."
        
        2.  Los autores de llamadas ingresan su PIN seguido de la tecla \#.
        
        3.  Sistema: "Por favor, diga correo de voz, correo electrónico, calendario, contactos personales, directorio u opciones personales."
        
        4.  Autor de la llamada: “Directorio”
        
        5.  Sistema: "Búsqueda de directorio. Tenga en cuenta que para las siguientes tareas el sistema requiere que use el teclado del teléfono en vez de hablar. Use el teclado para deletrear el nombre de la persona que está intentando encontrar, el apellido primero o deletree la primera parte de su dirección de correo electrónico, presione dos veces la almohadilla, si conoce la extensión, presione almohadilla."
        
        6.  El autor de la llamada utiliza el teclado y escribe "smithtony" y presiona la tecla \#.
        
        7.  Sistema: "Para Tony Smith, investigación, presione 1. Para Tony Smith, administración, presione 2. Para Tony Smith, soporte técnico, presione 3."
        
        8.  El autor de la llamada presiona la tecla apropiada en el teclado y la llamada se transfiere al usuario.
        
        De manera predeterminada, los operadores automáticos de UM asociados con este plan de marcado heredarán esta configuración. Sin embargo, puede modificar esta configuración en cada operador automático de mensajería unificada que cree.
        
        Seleccione uno de los métodos siguientes para ofrecer a la persona que llama más información que le ayude a localizar al usuario correcto de la organización:
        
          - **Nada**   No se ofrece información adicional cuando se enumeran las coincidencias. Este método está seleccionado de forma predeterminada.
        
          - **Cargo**   El sistema de correo de voz incluye el cargo de cada usuario cuando se enumeran las coincidencias.
        
          - **Departamento**   El sistema de correo de voz incluye el departamento de cada usuario cuando se enumeran las coincidencias.
        
          - **Ubicación**   El sistema de correo de voz incluye la ubicación de cada usuario cuando se enumeran las coincidencias.
        
          - **Pedir el alias**   El sistema de correo de voz solicita al autor de la llamada el alias del usuario.

11. Después de establecer las configuraciones requeridas, haga clic en **Guardar** para guardar los cambios.

## Use el Shell para configurar las configuraciones del plan de marcado de mensajería unificada

En este ejemplo se configura un plan de marcado de UM denominado `MyDialPlan` para usar 9 para el código de acceso a línea externa.

    Set-UMDialplan -Identity MyDialPlan -OutsideLineAccessCode 9

En este ejemplo se configura un plan de marcado de UM denominado `MyDialPlan` para usar un saludo de bienvenida.

    Set-UMDialplan -Identity MyDialPlan -WelcomeGreetingEnabled $true -WelcomeGreetingFilename welcome.wav

En este ejemplo configura un plan de marcado de UM denominado `MyDialPlan` con reglas de marcado.

    $csv=import-csv "C:\MyInCountryGroups.csv"
    Set-UMDialPlan -Identity MyDialPlan -ConfiguredInCountryGroups $csv
    Set-UMDialPlan -Identity MyDialPlan -AllowedInCountryGroups "local, long distance"

## Use el Shell para ver las configuraciones del plan de marcado de mensajería unificada

En este ejemplo se muestra una lista de todos los planes de marcado de mensajería unificada.

    Get-UMDialplan

En este ejemplo se muestra una lista formateada de todas las configuraciones en un plan de marcado de mensajería unificada denominado `MyUMDialPlan`.

    Get-UMDialplan -Identity MyUMDialPlan | Format-List

