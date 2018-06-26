---
title: 'Administrar una directiva de buzones de correo de mensajería unificada: Exchange 2013 Help'
TOCTitle: Administrar una directiva de buzones de correo de mensajería unificada
ms:assetid: 704b001c-3e6f-4ed5-bbe5-42a778f6ac0d
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa998829(v=EXCHG.150)
ms:contentKeyID: 50556815
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Servers.UnifiedMessaging.UMMailboxPolicyGeneralTab
ms.translationtype: HT
---

# Administrar una directiva de buzones de correo de mensajería unificada

 

_**Se aplica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2013-02-22_

Después de crear una directiva de buzón de mensajería unificada (MU), puede ver y configurar diversas opciones. Por ejemplo, puede configurar características de MU, como Vista previa de correo de voz o Reproducir en teléfono, y otras opciones relacionadas con la seguridad, como opciones de configuración de directivas de PIN y Correo de voz protegido.

Para conocer tareas de administración adicionales relacionadas con las directivas de buzones de mensajería unificada, consulte [Procedimientos de políticas de buzón de mensajería unificada](um-mailbox-policy-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Directivas de buzón de MU" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de mensajería unificada. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de mensajería unificada. Para conocer los pasos detallados, consulte [Crear una directiva de buzón de mensajería unificada](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Uso del Centro de Administración de Exchange para administrar una directiva de buzón de MU

1.  En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**. En la vista de lista, seleccione el plan de marcado de mensajería unificada que desea modificar y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

2.  En la página **Plan de marcado de MU**, en **Directivas de buzón de MU**, en la barra de herramientas, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").
    
      - Use **General** para ver y configurar opciones de una directiva de buzón de MU. Por ejemplo, puede ver los planes de marcado asociados con la directiva de buzón de MU o deshabilitar las notificaciones de llamadas perdidas para los usuarios que se encuentran asociados con una directiva de buzón de MU. Cuando modifica las opciones de una directiva de buzón de MU, las opciones se aplican a todos los usuarios que se encuentran asociados con dicha directiva. Puede ver o configurar lo siguiente:
        
          - **Plan de marcado de MU**   Muestra el nombre del plan de marcado asociado a la directiva de buzón de MU. Éste es el nombre del plan de marcado que se muestra en el Shell.
            
            Cuando se crea una nueva directiva de buzón de mensajería unificada, se debe asociar con un plan de marcado. Después de crear y asociar una directiva de buzón de MU con un plan de marcado, las opciones definidas en la directiva de buzón se aplican a los usuarios que se encuentran asociados con el plan de marcado. De forma predeterminada, cuando se crea un plan de marcado de MU mediante el Shell, también se creará una directiva de buzón de MU.
        
          - **Nombre**   Escriba el nombre del plan de marcado. El nombre de un plan de marcado de mensajería unificada es necesario y debe ser exclusivo. Sin embargo, se usa solamente para la visualización en el EAC y en el Shell. Si tiene que cambiar el nombre para mostrar del plan de marcado después de crearlo, antes debe eliminar el plan de marcado de mensajería unificada y, a continuación, crear otro plan de marcado con el nombre adecuado. Si la organización usa varios planes de marcado de mensajería unificada, es recomendable usar nombres significativos para los planes. La longitud máxima del nombre de un plan de marcado de mensajería unificada es de 64 caracteres y puede incluir espacios. (Si está integrándolo con Microsoft Office Communications Server 2007 R2 o Microsoft Lync Server, no se recomienda usar espacios). No obstante, no pueden incluirse ninguno de los caracteres siguientes: " / \\ \[ \] : ; | = , + \* ? \< \>.
        
          - **Límite en los saludos principales (en minutos)**   Use este cuadro de texto para especificar el número máximo de minutos que pueden usar los usuarios asociados con la directiva de buzón de MU cuando graban su saludo de correo de voz. Puede modificar esta opción una vez que se crea la directiva de buzón de mensajería unificada. Solo están permitidos los caracteres numéricos. El intervalo permitido para el saludo es de 1 a 10 minutos. El valor predeterminado es 5 minutos.
        
          - **Permitir la vista previa del correo de voz**   Active o desactive esta casilla para habilitar o deshabilitar la característica Vista previa del correo de voz para los usuarios asociados con la directiva de buzón de MU. Si se habilita esta opción, los usuarios podrán recibir el mensaje de un correo de voz en el cuerpo del mensaje de un correo electrónico o mensaje de texto. De forma predeterminada, esta opción está habilitada.
        
          - **Permitir a los usuarios configurar reglas de contestador automático**   Active esta casilla para permitir a los usuarios asociados con la directiva de buzón de MU crear reglas de contestador automático. Si esta opción está deshabilitada en el plan de marcado de MU, esta característica no estará disponible para los usuarios habilitados para MU asociados con la directiva de buzón de MU. De forma predeterminada, esta opción está habilitada.
        
          - **Permitir el indicador de mensaje en espera**   Active o desactive esta casilla para habilitar o deshabilitar el indicador de mensaje en espera para los usuarios asociados con la directiva de buzón de MU. Indicador de mensaje en espera es una función incluida en la mayoría de los sistemas de correo de voz heredados. En su formato más común, enciende una luz en el teléfono del usuario de correo de voz para indicar la presencia de un nuevo mensaje de voz. El indicador de mensaje en espera también puede ser un mensaje de texto al teléfono móvil del usuario habilitado para mensajería unificada. De forma predeterminada, esta opción está habilitada.
        
          - **Permitir Outlook Voice Access**   Active o desactive esta casilla para habilitar o deshabilitar el acceso a Outlook Voice Access para los usuarios asociados con esta directiva de buzón de MU. Outlook Voice Access es una función que usan los usuarios habilitados para mensajería unificada para obtener acceso a su buzón a través de un teléfono. Esta opción está habilitada de forma predeterminada.
        
          - **Permitir notificaciones de llamadas perdidas**   Active o desactive esta casilla para habilitar o deshabilitar las notificaciones de llamadas perdidas para los usuarios asociados con la directiva de buzón de MU. Una notificación de llamada perdida es un mensaje de correo electrónico que se envía al buzón de un usuario cuando este no responde a una llamada entrante. Se trata de un mensaje de correo electrónico diferente del mensaje de correo electrónico que contiene el mensaje de correo de voz que se deja para un usuario.
            

            > [!NOTE]
            > Al integrar la mensajería unificada y Lync Server localmente, las notificaciones de llamadas perdidas no estarán disponibles para los usuarios que tengan un buzón en un servidor de buzones de Exchange 2007 o Exchange 2010. Se genera una notificación de llamada perdida cuando un usuario se desconecta antes de que la llamada se envíe a la mensajería unificada.

            
            Normalmente, cuando un usuario pierde una llamada entrante, recibe dos mensajes de correo electrónico: un mensaje que contiene el mensaje de voz de correo y un mensaje de notificación de llamada perdida. De forma predeterminada, las notificaciones de llamadas perdidas están habilitadas cuando se crea una directiva de buzón de mensajería unificada.
        
          - **Permitir Reproducir en teléfono para el correo de voz**   Active o desactive esta casilla para habilitar o deshabilitar la función Reproducir en teléfono para los usuarios asociados con la directiva de buzón de MU. Esta opción está habilitada de manera predeterminada y permite a los usuarios reproducir su mensaje de voz en cualquier teléfono, incluidos teléfonos móviles o de oficina.
        
          - **Permitir faxes entrantes**   Active o desactive esta casilla para habilitar o deshabilitar los faxes entrantes para los usuarios asociados con la directiva de buzón de MU. De manera predeterminada, cuando habilita la mensajería unificada para los usuarios, su buzón de correo puede recibir faxes. Sin embargo, si está opción está deshabilitada en el plan de marcado de MU, los usuarios habilitados para MU asociados con la directiva de buzón de MU no podrán recibir faxes. La configuración predeterminada de la directiva del buzón de correo de MU está deshabilitada.
            
            Después de habilitar la opción **Permitir faxes entrantes**, deberá especificar el URI para el servidor de fax asociado. Si la directiva de buzón de correo de MU está vinculada a un plan de marcado que emplea TCP y TLS, deberá especificar los URI para TCP y TLS.
        
          - **Ayudar a Microsoft a mejorar la vista previa del correo de voz**   Estas opciones permiten a Microsoft mejorar la calidad de la vista previa del correo de voz. Puede habilitar la siguiente configuración:
            
              - **Permitir análisis de mensajes de correo de voz de los autores de llamadas**   Use esta opción para ayudar a mejorar la calidad de la vista previa del correo de voz en las versiones futuras de Microsoft Exchange mediante el reenvío de copias de mensajes de voz a Microsoft para su análisis. No puede establecer esta opción si están protegidos todos los mensajes de voz.
            
              - **Avisar a los autores de llamadas que los mensajes de voz pueden ser analizados**   Use esta opción para avisar a los autores de llamadas que Microsoft puede analizar los mensajes que dejen a fin de mejorar la calidad de la vista previa del correo de voz y permitirles no participar.
    
      - 
        
        Use **Texto del mensaje** para configurar los ajustes del texto del mensaje para los usuarios asociados con una directiva de buzón de MU. Por ejemplo, puede especificar el texto del mensaje de correo electrónico que se envía a los usuarios después de restablecer su PIN de mensajería unificada. Se pueden realizar las siguientes configuraciones:
        
          - **Cuando un usuario está habilitado para la mensajería unificada**   El texto que se escribe en este cuadro de texto aparece en el mensaje de correo electrónico que se envía a los usuarios cuando se los habilita para la mensajería unificada. Cuando el buzón de correo de un usuario está habilitado para la MU y el usuario está habilitado para el correo de voz, se le envía un mensaje de voz que le da la bienvenida a la mensajería unificada. Este cuadro de texto está limitado a 512 caracteres y puede contener formato HTML simple. De forma predeterminada, no se define texto en este cuadro de texto.
            
            Este mensaje de bienvenida contiene un texto de bienvenida y la información de PIN que el usuario usará para obtener acceso al sistema de correo de voz o de mensajería unificada. El texto escrito en este cuadro de texto se incluye en la parte inferior de este mensaje de bienvenida. Puede usar este cuadro de texto para incluir información como los números de teléfono de la asistencia técnica del correo de voz o los números de Outlook Voice Access.
            
            Si no se escribe texto en el cuadro, se incluye en el mensaje de correo electrónico el texto predeterminado generado por el sistema de correo de voz o de MU.
            
            El texto que escriba en este cuadro puede ser texto sin formato. También puede contener etiquetas de formato HTML sencillas si desea resaltar texto o agregar hipervínculos a otro contenido.
            
            **Ejemplo 1:** Si tiene alguna duda o sugerencia sobre el servicio de correo de voz, llame a la extensión 4200 del servicio de asistencia técnica.
            
            **Ejemplo 2:** Si tiene alguna duda o sugerencia sobre el \<b\>servicio de correo de voz\</b\>, llame al servicio de asistencia técnica a la extensión 4200 o visite nuestro sitio web en \<a href=”http://emp.contoso.com/itinfo/vmail”\>\</a\>.
        
          - **Cuando se restablece el PIN de Outlook Voice Access de un usuario**   El texto que se escribe en el cuadro de texto se incluye en el mensaje de correo electrónico que se envía a los usuarios habilitados para mensajería unificada cuando se restablece su PIN de MU.
            
            Un PIN se restablece mediante el sistema de correo de voz o de MU si el número de intentos de inicio de sesión con error es mayor que 10 (de manera predeterminada) o si los usuarios restablecen su PIN mediante las características de MU incluidas en Microsoft Outlook, Outlook Web App o Outlook Voice Access desde un teléfono. Puede usar este cuadro de texto para incluir información tal como los avisos de seguridad u otra información relacionada con la seguridad en el mensaje de correo electrónico.
            
            Si no se escribe texto en el cuadro, se incluye en el mensaje de correo electrónico el texto predeterminado generado mediante el sistema de MU.
            
            Este cuadro de texto está limitado a 512 caracteres. De forma predeterminada, no se define texto en este cuadro de texto.
            
            El texto que escriba en este cuadro puede ser texto sin formato. También puede contener etiquetas de formato HTML sencillas si desea resaltar texto o agregar hipervínculos a otro contenido.
        
          - **Cuando un usuario recibe un mensaje de voz**   El texto que se escribe en este cuadro de texto se incluye en el mensaje de correo electrónico que se envía a los usuarios cuando reciben un mensaje de voz de una llamada entrante. Por ejemplo, este texto puede incluir renuncias que contengan información acerca del reenvío de mensajes de voz o directivas de seguridad de sistemas que describan el modo correcto de administrar los mensajes de voz en su organización.
            
            Si no se escribe texto en el cuadro, se incluye en el mensaje de correo electrónico el texto predeterminado generado por el sistema. Este cuadro de texto está limitado a 512 caracteres. De forma predeterminada, no se define texto en este cuadro de texto.
            
            El texto que escriba en este cuadro puede ser texto sin formato. También puede contener etiquetas de formato HTML sencillas si desea resaltar texto o agregar hipervínculos a otro contenido.
        
          - **Cuando un usuario recibe un mensaje de fax**   El texto que se escribe en este cuadro de texto se incluye en el mensaje de correo electrónico que se envía a los usuarios cuando reciben un mensaje de fax entrante en su bandeja de entrada. Puede usar este cuadro de texto para incluir renuncias que contengan información acerca del reenvío de mensajes de fax u otras directivas de seguridad del sistema sobre el modo correcto de administrar mensajes de fax en la organización.
            
            Si no se escribe texto en el cuadro, se incluye en el mensaje de correo electrónico el texto predeterminado generado por el sistema. Este cuadro de texto está limitado a 512 caracteres. De forma predeterminada, no se define texto en este cuadro de texto.
    
      - 
        
        Use **Directivas de PIN** para configurar las opciones de PIN para los usuarios asociados con una directiva de buzón de MU. Los PIN de la MU permiten a los usuarios obtener acceso a sus buzones por medio de un teléfono. Al configurar los valores de esta página, puede especificar el número mínimo de dígitos de un PIN de mensajería unificada o el número de intentos de inicio de sesión con error antes de bloquear el buzón de mensajería unificada a los usuarios.
        
        Asegúrese de planear cuidadosamente las directivas de PIN de mensajería unificada que implemente en su entorno. Si no planea ni implementa las directivas de PIN de mensajería unificada adecuadas, puede generar amenazas para la seguridad y permitir por error el acceso no autorizado a su red. Se pueden realizar las siguientes configuraciones:
        
          - **Longitud mínima de PIN (dígitos)**   Use este cuadro de texto para especificar el número mínimo de dígitos que puede contener el PIN de un usuario de MU. El valor predeterminado es seis dígitos. El intervalo está comprendido entre 4 y 24 dígitos numéricos. Esta configuración no se puede deshabilitar.
            
            Al aumentar el número de dígitos necesarios para un PIN, aumenta el nivel de seguridad del sistema de MU. Al disminuir el número de dígitos necesarios para un PIN, se reduce el nivel de seguridad de la red. Cuantos menos dígitos sean necesarios en un PIN, más fácil le resultará a un posible atacante adivinarlo.
            
            Si el valor es demasiado alto, los usuarios podrían tener problemas para recordar sus PIN. Sin embargo, si es demasiado bajo, se arriesga a sufrir accesos no autorizados al sistema de MU.
        
          - **Recuento de reciclaje de PIN**   Use este valor para establecer el número de PIN únicos que deben usar los usuarios antes de volver a usar un PIN antiguo. Para la mayoría de las organizaciones, este valor se debería establecer, de forma predeterminada, en 5, que es la cantidad de PIN que el sistema recordará. No se puede deshabilitar el historial de PIN.
            
            Puede establecer este valor entre 1 y 20. Si es demasiado alto, los usuarios pueden sentirse frustrados, puesto que les puede resultar difícil memorizar muchos PIN. Si es demasiado bajo, puede suponer una amenaza para la seguridad de la red.
        
          - **Permitir patrones comunes de PIN**   Use esta configuración para establecer los requisitos de complejidad de PIN para la MU. Estos requisitos se aplican en cambios de PIN o cuando se crean nuevos PIN.
            
            Si esta opción está deshabilitada, se rechazarán los números secuenciales y repetidos, así como el sufijo de la extensión de buzón. Si esta opción está habilitada, solo se rechazará el sufijo de la extensión de buzón.
            
            Como medida de seguridad, se recomienda deshabilitar esta opción. Si está deshabilitada, los PIN de los usuarios no pueden contener lo siguiente:
            
            Números consecutivos (por ejemplo, 123456 o 456789).
            
            Números repetidos (por ejemplo, 111111 u 8888888).
            
            Sufijo de la extensión de buzón.
        
          - **Exigir la vigencia de PIN (días)**   Use este cuadro de texto para configurar el número de días que deben transcurrir antes de que el PIN del usuario con MU expire. Una vez que el PIN ha expirado, el usuario debe crear uno nuevo. Para la mayoría de las organizaciones, este valor se debería establecer en un valor predeterminado de 60 días.
            
            El valor de esta opción puede ser entre 0 y 999. Si se establece en 0, los PIN no expiran nunca. Si el valor es demasiado bajo, los usuarios podrían sentirse molestos por tener que crear y memorizar nuevos PIN con tanta frecuencia.
        
          - **Número de inicios de sesión incorrectos antes del restablecimiento del PIN**   Use este cuadro de texto para escribir el número de intentos de inicio de sesión consecutivos con error o incorrectos antes de que el sistema de MU restablezca automáticamente el PIN de un usuario. Para la mayoría de las organizaciones, este valor se debería establecer en un valor predeterminado de 5 intentos.
            
            El valor de esta opción puede ser entre 0 y 999. Si se establece en 0, la opción se deshabilita y el sistema no restablecerá automáticamente los PIN de los usuarios. Si es demasiado bajo, los usuarios pueden sentirse frustrados; si es demasiado alto, los usuarios malintencionados tienen más posibilidades de averiguar el PIN.
            
            Este valor se debe configurar en un número menor que el número configurado en el valor **Número de errores al intentar iniciar sesión antes del bloqueo**. Este valor está diseñado para ayudar a prevenir ataques a los PIN de los usuarios.
        
          - **Número de inicios de sesión incorrectos antes del bloqueo**   Use este cuadro de texto para escribir el número máximo de intentos de inicio de sesión consecutivos con error o incorrectos antes de que se bloquee un buzón al usuario.
            
            Por ejemplo, si un usuario intenta iniciar la sesión en su buzón incorrectamente cinco veces, según el valor **Número de inicios de sesión incorrectos antes del restablecimiento del PIN**, el sistema restablecerá el PIN del usuario. Si el usuario intenta usar su nuevo PIN cinco veces más de manera incorrecta, el sistema volverá a restablecerlo. Si el usuario intenta usar este nuevo PIN cinco veces más de manera incorrecta, se le bloquea el buzón. Después de bloquear a un usuario, el administrador debe restablecer o desbloquear manualmente su buzón.
            
            Este valor se puede establecer entre 1 y 999. Si es demasiado bajo, los usuarios pueden sentirse frustrados; si es demasiado alto, los usuarios malintencionados tiene más posibilidades de averiguar el PIN. Para la mayoría de las organizaciones, este valor se debería establecer en un valor predeterminado de 15 intentos.
            
            Este número debe ser mayor que el número configurado en el valor **Número de inicios de sesión incorrectos antes del restablecimiento del PIN**. Este valor está diseñado para ayudar a prevenir ataques a los PIN de los usuarios.
    
      - 
        
        Use **Autorización de marcado** para configurar las reglas para los usuarios habilitados para la MU que están asociados con esta directiva de buzón de MU.
        
        Puede usar esta configuración para controlar los números de extensión que se pueden marcar o los números telefónicos que pueden marcar los usuarios habilitados para la MU que están asociados con la directiva de buzón de MU. Se pueden realizar las siguientes configuraciones:
        
          - **Llamadas en el mismo plan de marcado de MU**   Seleccione esta casilla para permitir a los usuarios habilitados para la MU que llamen a un número de acceso de suscriptor configurado en un plan de marcado y con la sesión iniciada correctamente en sus buzones, realizar o transferir llamadas a usuarios habilitados para la MU que tengan números de extensión dentro del mismo plan de marcado. Esta opción está habilitada de forma predeterminada.
            
            Cuando se deshabilita esta opción, los usuarios habilitados para MU que llamen a un número de acceso de suscriptor configurado en un plan de marcado y que hayan iniciado sesión correctamente en su buzón pueden realizar o transferir llamadas a usuarios sin MU habilitada o a otros números de extensión no asociados a un usuario habilitado para MU. Sin embargo, no pueden transferir a usuarios habilitados para MU que se encuentran dentro del mismo plan de marcado. Esto se debe a que, de manera predeterminada, la opción **Llamadas a cualquier extensión** está habilitada.
        
          - **Llamadas a cualquier extensión**   Cuando esta opción está habilitada, los usuarios que llamen a un número de acceso de suscriptor configurado en un plan de marcado, y que hayan iniciado sesión correctamente en su buzón, podrán realizar llamadas a usuarios sin MU habilitada, a otros números de extensión no asociados con un usuario habilitado para MU y a usuarios habilitados para MU en el mismo plan de marcado. Esto se debe a que la configuración de **Llamadas en el mismo plan de marcado de mensajería unificada** está habilitada de forma predeterminada.
            
            Cuando esta opción está deshabilitada, los usuarios que llamen a un número de Outlook Voice Access configurado en un plan de marcado, y que hayan iniciado sesión correctamente en su buzón, no podrán realizar llamadas a usuarios sin MU habilitada ni a otros números de extensión no asociados a un usuario habilitado para MU. Sin embargo, pueden realizar llamadas o transferirlas a números de extensión asociados con usuarios habilitados para mensajería unificada. Esto se debe a que la configuración de **Llamadas en el mismo plan de marcado de mensajería unificada** está habilitada de forma predeterminada. La configuración **Llamadas a cualquier extensión** está habilitada de manera predeterminada.
            
            Puede habilitar esta opción en un entorno en el que no se hayan habilitado todos los usuarios para mensajería unificada. Esta opción también resulta útil si desea permitir a los usuarios que llamen a un número de Outlook Voice Access configurado en un plan de marcado para llamar a números de extensión no asociados con un usuario habilitado para mensajería unificada.
        
          - **Grupos de reglas de marcado nacionales/regionales autorizados**   Use esta sección para agregar o quitar grupos de reglas de marcado nacionales o regionales permitidos. De forma predeterminada, no hay grupos de reglas de marcado nacionales o regionales configurados en directivas de buzones de mensajería unificada.
            
            Los grupos de reglas de marcado nacionales o regionales se usan para permitir o restringir los números de teléfono de un país o región que pueden marcar los usuarios de Outlook Voice Access. Esto ayuda a evitar llamadas de teléfono y gastos innecesarios o no autorizados.
            
            Para agregar grupos de reglas de marcado nacionales o regionales, primero debe crear los grupos de reglas de marcado nacionales o regionales adecuados en el plan de marcado asociado con la directiva de buzón de MU y, a continuación, agregar las entradas de regla de marcado apropiadas en el grupo de reglas de marcado. Después de crear los grupos de reglas de marcado necesarios en el plan de marcado, debe agregar los grupos de reglas de marcado a la lista de restricciones de marcado en **Autorización de marcado** de la directiva de buzón de MU.
            
            Se pueden usar los grupos de reglas de llamadas nacionales o regionales para que la mensajería unificada permita o restrinja el acceso a números de teléfono dentro de un país o región. Esto se aplica a usuarios de Outlook Voice Access que hayan llamado a un número de Outlook Voice Access.
        
          - **Grupos de reglas de marcado internacional autorizados**   Use esta sección para agregar o quitar los grupos de reglas de marcado internacionales permitidos. De forma predeterminada, no hay grupos de reglas de marcado internacionales configurados en directivas de buzones de mensajería unificada.
            
            Para agregar grupos de reglas de marcado internacionales, primero debe crear los grupos de reglas de marcado internacionales adecuados en el plan de marcado asociado con la directiva de buzón de MU y, a continuación, agregar las entradas de regla de marcado apropiadas en el grupo de reglas de marcado. Después de crear los grupos de reglas de marcado necesarios, debe agregar los grupos de reglas de marcado a las restricciones de marcado en la directiva de buzón de MU.
            
            Los grupos de reglas de marcado internacionales pueden usarse para que la mensajería unificada permita o restrinja el acceso a números de teléfono fuera de un país o de una región. Esto se aplica a usuarios de Outlook Voice Access que hayan llamado a un número de Outlook Voice Access.
            
            Los grupos de reglas de marcado internacionales se usan para permitir o restringir los números de teléfono fuera de un país o región que pueden marcar los usuarios de Outlook Voice Access. Esto ayuda a evitar llamadas de teléfono y gastos innecesarios o no autorizados.
    
      - 
        
        Use **Correo de voz protegido** para configurar las siguientes opciones:
        
          - **Proteger los mensajes de voz de las personas que llaman sin autenticación**   Seleccione una de las siguientes opciones de la lista desplegable para determinar si una llamada entrante que contesta la mensajería unificada protegerá los mensajes de voz. Esta configuración se aplica a los mensajes de voz enviados a los usuarios habilitados para mensajería unificada cuando éstos no responden el teléfono. Esta opción también se aplica a los mensajes de voz enviados directamente a los usuarios habilitados para mensajería unificada cuando la persona que llama utiliza un operador automático de MU. Se pueden realizar las siguientes configuraciones:
            
            **Ninguno**   Use esta configuración para dejar sin efecto la aplicación de protección a los mensajes de voz enviados a los usuarios habilitados para mensajería unificada.
            
            **Privado**   Use esta configuración si desea aplicar protección únicamente a los mensajes de voz marcados como privados por la persona que llama.
            
            **Todos**   Use esta configuración si desea aplicar protección a todos los mensajes de voz, incluidos aquellos no marcados como privados.
        
          - **Proteger los mensajes de voz de autores de llamada autenticados**   Seleccione una de las siguientes opciones de la lista desplegable para determinar si una llamada entrante que contesta la mensajería unificada protegerá los mensajes de voz. Esta configuración se aplica a los mensajes de voz enviados a los usuarios habilitados para mensajería unificada cuando éstos no responden el teléfono. Este parámetro también se aplica cuando las personas que llaman inician sesión en su buzón mediante Outlook Voice Access, y desde ahí crean y envían un mensaje de voz. Se pueden realizar las siguientes configuraciones:
            
            **Ninguno**   Use esta configuración para dejar sin efecto la aplicación de protección a los mensajes de voz enviados a los usuarios habilitados para mensajería unificada.
            
            **Privado**   Use esta configuración si desea aplicar protección únicamente a los mensajes de voz marcados como privados por la persona que llama.
            
            **Todos**   Use esta configuración si desea aplicar protección a todos los mensajes de voz, incluidos aquellos no marcados como privados.
        
          - **Solicitar Reproducir en teléfono para los mensajes de voz protegidos**   Active esta casilla si desea forzar a los usuarios que reciben mensajes de voz protegidos a usar la función Reproducir en teléfono. O bien, si el software cliente no admite la administración de derechos, los usuarios deben usar Outlook Voice Access. La función Reproducir en teléfono solo se aplica a los clientes que ejecutan una versión de Outlook que admite la administración de derechos. Para Outlook 2007 y versiones anteriores que no admiten la administración de derechos, y para clientes de Outlook Web App, Outlook Voice Access es la única forma que tienen los usuarios para escuchar el correo de voz protegido.
            
            La configuración predeterminada requiere que todos los usuarios asociados con la directiva de buzón de MU usen la función Reproducir en teléfono para escuchar los mensajes de voz protegidos. De esta forma, se impide que otras personas escuchen el mensaje de voz mediante un reproductor multimedia con los altavoces del equipo o mediante un reproductor multimedia de un teléfono móvil. Incluso si esta opción está habilitada, un usuario habilitado para mensajería unificada podrá usar Outlook Voice Access para escuchar el correo de voz protegido.
            
            Esto resulta especialmente útil cuando los usuarios habilitados para mensajería unificada usan equipos públicos, equipos portátiles en lugares públicos o el reproductor multimedia de sus teléfonos móviles para escuchar correo de voz protegido que puede contener información privada.
        
          - **Permitir respuestas de voz a los elementos de calendario y correo electrónico**   Use esta opción para permitir a los usuarios habilitados para MU enviar respuestas de voz a mensajes de voz protegidos. El valor predeterminado es habilitado. Si lo deshabilita, si un usuario habilitado para la MU recibe un mensaje de correo de voz protegido, no podrá usar Outlook Voice Access para responder a elementos de calendario y correo electrónico.
        
          - **Mensaje que se enviará a usuarios que no son compatibles con Windows Rights Management**   Solo pueden obtener acceso al correo de voz protegido los clientes de correo que son compatibles con Information Rights Management (IRM) o si un usuario habilitado para MU usa Outlook Voice Access para obtener acceso al mensaje de correo de voz protegido.
            
            Si se envía un mensaje de correo de voz protegido a un cliente de correo electrónico que no admite IRM, el texto que se incluye en esta casilla se enviará al usuario en un mensaje de correo electrónico. Esta información debe incluir instrucciones acerca de las acciones que se pueden realizar para recibir el mensaje de correo de voz protegido.

## Uso del Shell para administrar una directiva de buzón de MU

Este ejemplo establece la configuración de PIN para usuarios asociados con una directiva de buzón de MU denominada `MyUMMailboxPolicy`.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -LogonFailuresBeforePINReset 8 -MaxLogonAttempts 12 -MinPINLength 8 -PINHistoryCount 10 -PINLifetime 60 -ResetPINText "The PIN that is used to allow you access to your mailbox using Outlook Voice Access has been reset."

En este ejemplo se seleccionan los grupos de países o regiones y los grupos internacionales de los configurados en el plan de marcado de MU que está asociado con la directiva de buzones de MU. Los usuarios habilitados para mensajería unificada asociados con esta directiva de buzón de MU podrán realizar llamadas salientes de acuerdo con las reglas definidas en estos grupos.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -AllowDialPlanSubscribers $true -AllowedInCountryOrRegionGroups InCountry/RegionGroup1,InCountry/RegionGroup2 -AllowedInternationalGroups InternationalGroup1,InternationalGroup2 -AllowExtensions $true 

En este ejemplo, se configura el texto de los mensajes de correo de voz enviados a los usuarios habilitados para MU y el texto de un mensaje de correo electrónico enviado a un usuario que esté habilitado para MU.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -UMEnabledText "You have been enabled for Unified Messaging." -VoiceMailText "You have received a voice message from Microsoft Exchange 2013 Unified Messaging." 

## Usar el Shell para ver las propiedades de las directivas de buzón de MU

Este ejemplo devuelve una lista formateada de todas las directivas de buzón de mensajería unificada del bosque Active Directory.

    Get-UMMailboxPolicy | Format-List

En este ejemplo, se devuelven las propiedades y los valores de una directiva de buzón de MU denominada `MyUMMailboxPolicy`.

    Get-UMMailboxPolicy -Identity MyUMMailboxPolicy

