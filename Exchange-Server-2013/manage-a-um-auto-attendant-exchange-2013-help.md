---
title: 'Administrar a un operador automático de mensajería unificada: Exchange 2013 Help'
TOCTitle: Administrar a un operador automático de mensajería unificada
ms:assetid: 4809ff56-ae34-4ce6-8e39-9193311c3f83
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa997867(v=EXCHG.150)
ms:contentKeyID: 49895604
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.UnifiedMessaging.AutoAttendantGeneralPropertyPage
ms.translationtype: MT
---

# Administrar a un operador automático de mensajería unificada

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2013-04-30_

Después de crear un operador automático de mensajería unificada (MU), podrá ver o configurar diversos ajustes de configuración. Por ejemplo, puede agregar, quitar y editar números de extensión que estén asociados con el operador automático. También puede habilitar y deshabilitar el reconocimiento de voz automático (ASR) para el operador automático y cambiar los saludos utilizados para horarios comerciales y no comerciales.

Para conocer tareas de administración adicionales relacionadas con los operadores automáticos de mensajería unificada, consulte [Procedimientos operador automático de mensajería unificada](um-auto-attendant-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el contenido "Operadores automáticos de MU" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un operador automático de MU. Para conocer los pasos detallados, consulte [Crear un operador automático de mensajería unificada](create-a-um-auto-attendant-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar el EAC para ver o para configurar la configuración del operador automático de mensajería unificada

1.  En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**. En la vista de lista, seleccione el plan de marcado de mensajería unificada que desee modificar y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

2.  En la página **Plan de marcado de la mensajería unificada**, en **Operadores automáticos de mensajería unificada**, seleccione el operador automático de mensajería unificada que desee ver o configurar y, a continuación, en la barra de herramientas, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  
    
    En la pestaña **Operador automático de mensajería unificada**, haga clic en **General** para ver la información solo para mostrar acerca del operador automático de mensajería unificada y para realizar tareas de administración en un operador automático de mensajería unificada de la siguiente forma:
    
      - **Plan de marcado de la mensajería unificada**   Este cuadro muestra el plan de marcado de mensajería unificada asociado con el operador automático. Después de haber creado un operador automático, el plan de marcado asociado con el operador automático no se puede cambiar. Si necesita asociar un operador automático con un plan de marcado diferente debe eliminar el plan de marcado y volver a asociar el operador automático con el plan de marcado correcto después de haberlo creado de nuevo.
    
      - **Nombre**   Este cuadro muestra el nombre que se asignó al operador automático cuando se creó. Es el nombre que aparecerá en el EAC.
    
      - **Estado**   Este cuadro muestra si el operador automático de MU está habilitado o deshabilitado. Para habilitar o deshabilitar el operador automático, cierre la página **Operador automático de mensajería unificada** y use la barra de herramientas en **Operadores automáticos de mensajería unificada** en la página **Plan de marcado de la mensajería unificada**.
    
      - **Números de acceso   **Use este cuadro para escribir un número de extensión o número de acceso que dirige a los usuarios al operador automático. De forma predeterminada, no se configura ningún número de extensión ni de acceso al crear un operador automático.
        
        El número de dígitos de los números de extensión o de los números de acceso que proporcione debe coincidir con el número de dígitos de un número de extensión configurado en el plan de marcado de mensajería unificada (MU) asociado con el operador automático de mensajería unificada. También puede agregar una dirección de protocolo de inicio de sesión (SIP) en este cuadro. Algunas centrales de conmutación IP (PBXs), PBX con SIP habilitado y Microsoft Office Communications Server 2007 R2 o Microsoft Lync Server usan una dirección SIP.
        
        Puede crear un operador automático nuevo sin indicar un número de extensión o número de acceso. Para agregar una extensión, escriba el número en este cuadro y, a continuación, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono"). Puede asociar más de un número con un operador automático. También puede editar o quitar un número de acceso existente. Para editar un número existente, selecciónelo y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar"). Para quitar un número de extensión existente de la lista, selecciónelo y haga clic en **Quitar**![Icono de quitar](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "Icono de quitar").
    
      - **Configurar el operador automático para responder a los comandos de voz**    Seleccione esta casilla de verificación para habilitar a los las personas que llaman para que respondan verbalmente a los mensajes del operador automático para navegar por el menú del sistema. De forma predeterminada, cuando se crea un operador automático, no está habilitado para voz.
        
        Si decide crear un operador automático de mensajería unificada, pero no quiere habilitarlo para voz, puede usar el EAC o el Shell para habilitarlo para voz cuando se cree.
    
      - **Use este operador automático cuando los comandos de voz no funcionen correctamente**   Haga clic en **Examinar** para seleccionar el operador automático que desea usar en caso de que los comandos de voz no funcionen correctamente. También se conoce como un operador automático de reserva DTMF. Un operador automático de reserva DTMF se puede usar si la opción **Configurar el operador automático para responder a los comandos de voz que no funcionan correctamente** se selecciona. Primero debe crear un operador automático de retroceso con multifrecuencia de tono dual y hacer clic en **Examinar** para ubicar el operador automático con multifrecuencia de tono dual adecuado.
        
        Un operador automático de retroceso con multifrecuencia de tono dual se utiliza cuando un operador automático de MU habilitado para voz no entiende ni reconoce las entradas de voz de quienes llaman. Si se utiliza el operador automático con multifrecuencia de tono dual, la persona que llama debe usar entradas de multifrecuencia de tono dual para navegar por el sistema de menús, deletrear el nombre de usuario o usar un mensaje del menú personalizado. La persona que llama no podrá usar comandos de voz para desplazarse por este operador automático.
        
        Si no configura un operador automático de retroceso con multifrecuencia de tono dual, le recomendamos que configure un número de extensión de operador en el operador automático. Si no configura un número de extensión de operador, cuando las personas que llaman utilicen un operador automático habilitado para voz y el sistema no reconozca sus entradas de voz, no podrán navegar por el sistema ni se transferirán a un operador para recibir ayuda.
        
        Aunque no sea necesario, es aconsejable que configure un operador automático de retroceso con multifrecuencia de tono dual que tenga la misma configuración que el operador automático habilitado para voz. El operador automático de retroceso con multifrecuencia de tono dual no debe estar habilitado para voz.
    
      - **Idioma para la interfaz de voz automatizada**   Use esta lista para seleccionar el idioma que escucharán las personas que llamen al operador automático. El idioma predeterminado se define al instalar Microsoft Exchange. De manera predeterminada, para implementaciones locales e híbridas, se utiliza el inglés de EE. UU. ya que el operador automático utiliza la configuración de idioma del plan de marcado de mensajería unificada. Para tener otros idiomas disponibles, deberá instalar el paquete de idiomas para MU correspondiente de los idiomas que desee incluir. Para obtener más información acerca de cómo instalar un paquete de idioma de UM, consulte [Instalar un paquete de idioma de mensajería unificada](install-a-um-language-pack-exchange-2013-help.md). Para la mensajería unificada de Office 365, no se necesita instalar ningún paquete de idioma de MU adicional.
        
        Aunque puede seleccionar un idioma diferente al seleccionado para el plan de marcado de MU asociado con el operador automático, es recomendable que la configuración de ambos idiomas coincida. Si la configuración de idioma no coincide, cuando se llame a un número de extensión definido en el plan de marcado, la comunicación será en un idioma y si se marca un número de extensión asociado con un operador automático, la comunicación será en otro idioma.
    
      - **Nombre comercial   **Use este cuadro para escribir el nombre de la empresa. De manera predeterminada, no se introduce ningún nombre comercial. Si escribe un nombre comercial en este cuadro, se reproducirá un mensaje con el nombre comercial a las personas que llaman, en lugar del saludo predeterminado.
    
      - **Ubicación comercial   **Use este cuadro para escribir la ubicación de la empresa. De manera predeterminada, no se introduce ninguna ubicación empresarial. Si escribe la ubicación comercial en este cuadro, se reproducirá a las personas que llaman.

4.  
    
    Use **Saludos** en el operador automático para administrar saludos grabados. Puede seleccionar saludos predeterminados o personalizados que haya grabado previamente para horarios comerciales y no comerciales. Se pueden realizar las siguientes configuraciones:
    
      - **Saludo en horario comercial**   Este es el saludo inicial que se reproduce cuando una persona llama al operador automático durante el horario comercial de su organización. De forma predeterminada, el horario comercial es de 12:00 A.M. a 12:00 A.M. y no se establece horario no comercial. Si no especifica un saludo personalizado, las personas que llaman reciben un mensaje del sistema que dice, "Bienvenido al operador automático de Exchange". Los horarios comerciales y no comerciales se configuran en la pestaña **Horario comercial** del operador automático.
        
        Es posible que desee personalizar este saludo para que represente a su compañía, por ejemplo, "Gracias por llamar a Woodgrove Bank". Puede configurar un saludo personalizado para el horario comercial haciendo clic en **Cambiar** para seleccionar un archivo de saludo personalizado grabado previamente. El saludo personalizado se debe haber grabado como un archivo .wav o .wma.
    
      - **Saludo en horario no comercial**   Este es el saludo inicial que se reproduce cuando una persona llama al operador automático durante el horario no comercial de su organización. De forma predeterminada, no hay horarios no comerciales configurados. Por lo tanto, no existe ningún saludo predeterminado para el horario no comercial. Puede configurar los horarios comerciales y no comerciales en la ficha **Horario comercial** del operador automático.
        
        Es posible que desee personalizar este saludo para que represente a su empresa, por ejemplo, "Gracias por llamar a Woodgrove Bank, pero en este momento la empresa está cerrada" o "Ha llamado a Contoso, Ltd. en horario no comercial. El horario comercial es de 8:00 a. m. a 5:00 p. m., de lunes a viernes". Puede configurar un saludo personalizado para el horario no comercial haciendo clic en **Cambiar** para seleccionar un archivo de saludo personalizado grabado previamente. El saludo personalizado se debe haber grabado como un archivo .wav o .wma.
    
      - **Mensaje informativo**   Cuando está habilitada, esta grabación opcional se reproduce inmediatamente después del saludo para horarios comerciales y no comerciales. Un mensaje informativo puede indicar los horarios comerciales de la organización, por ejemplo, "El horario de nuestra empresa es de 8:30 a 17:30, de lunes a viernes, y de 8:30 a 13:00 los sábados." Un anuncio informativo también puede proporcionar información necesaria para el cumplimiento de las directivas de la empresa, por ejemplo, \&quot;Se pueden controlar las llamadas con fines de formación\&quot;. Si es importante que las personas que llaman escuchen todo el mensaje informativo, puede marcarlo como ininterrumpible, solicitando que la persona que llame escuche todo el mensaje.
        
        De forma predeterminada, no hay ningún mensaje informativo configurado en los planes de marcado de mensajería unificada u operadores automáticos. Si habilita un mensaje informativo y usa un archivo de audio personalizado específico para su organización, la opción **Permitir la interrupción del anuncio** estará disponible. Los mensajes deben haberse grabado previamente como archivos .wav o .wma. Haga clic en **Cambiar** para localizar un archivo de aviso informativo personalizado que se haya grabado previamente.
        
        **Permitir la interrupción del anuncio**   Seleccione esta casilla de verificación para permitir a la persona que llame interrumpir el anuncio informativo. Esto deberá habilitarse si tiene mensajes informativos largos. Las personas que llaman pueden frustrarse si el mensaje informativo es largo y no pueden interrumpirlo para tener acceso a las opciones que ofrece el operador automático.

5.  Use **Horario comercial** para determinar el horario de apertura de la organización. Durante el horario comercial, las personas que llaman escuchan el saludo predeterminado del horario comercial o uno personalizado, y el menú principal de horario comercial pregunta si están configuradas las asignaciones de claves comerciales adecuadas en **Navegación de menús**. Se pueden realizar las siguientes configuraciones:
    
      - **Zona horaria**   Use esta lista para seleccionar la zona horaria. Cuando establezca el horario, considere si el plan de marcado asociado con el operador automático cubre varias zonas horarias.
        
        De forma predeterminada, para implementaciones locales e híbridas, la zona horaria se configura con la hora del sistema del servidor local cuando el servidor de buzones que ejecuta el servicio de mensajería unificada de Microsoft Exchange está instalado.
    
      - **Horario comercial**   Haga clic en **Configurar el horario comercial** y, a continuación, en la página **Configurar el horario comercial**, use la cuadrícula para configurar el horario comercial de su organización.
    
      - **Programación de vacaciones**   Úsela para definir los días, desde las 00:00 hasta las 23:59 (de 12:00 a. m. a 11:59 p. m.), en los que la organización cerrará por vacaciones. Las personas que llamen y escuchen al operador automático en las horas especificadas en la página **Nuevo día festivo** escucharán el archivo de audio de saludo de vacaciones personalizado que defina. Cuando configure el horario de vacaciones, debe definir el nombre de las vacaciones, el archivo de audio del saludo de vacaciones grabado, y la **Fecha de inicio** y la **Fecha de finalización**. Los saludos deben haberse grabado previamente como archivos .wav o .wma.

6.  Use **Navegación de menús** para especificar las opciones de menú que se ofrecen a las personas que llaman durante los horarios comercial y no comercial. Si desea habilitar el menú de navegación, debe hacerlo independientemente del horario comercial y del horario no comercial. Por ejemplo, si desea habilitar la navegación en horario comercial, debe agregar una grabación de audio personalizada en el mensaje de menú, seleccione la casilla de verificación **Habilitar navegación de menús en horario comercial**, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") y, a continuación, establezca las opciones en la página **Nueva entrada de navegación de menús**.
    
      - **Navegación de menús de horario comercial**   Es la lista de opciones que las personas que llaman escuchan durante el horario comercial que se definen en la página **Horario comercial**. Por ejemplo, "Para asistencia técnica, presione o diga 1. Para oficinas corporativas y administración, presione o diga 2. Para el departamento comercial, presione o diga 3."
        
        Para habilitar la navegación de menús de horario comercial, debe realizar los siguientes pasos:
        
        1.  **Mensaje de menú**   Use esta opción para especificar un archivo de audio con el mensaje de menú personalizado. Para usar un mensaje de menú de horario comercial grabado previamente, haga clic en **Cambiar** y, a continuación, haga clic en **Examinar** para localizar la grabación del mensaje de menú.
        
        2.  **Habilitar navegación de menús en horario comercial**   Seleccione esta casilla para habilitar las opciones de navegación del menú que se usarán en horario comercial. Si habilita la navegación del menú de horario comercial, puede agregar nuevas entradas en el menú de navegación de horario comercial.
        
        3.  Haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") para crear una nueva entrada del menú de navegación. En la página **Nueva entrada de navegación de menús** use las siguientes opciones para crear una nueva entrada de navegación de menús:
            
              - **Preguntar**   Use esta casilla para escribir el nombre del nuevo menú de navegación. El nombre del menú de navegación se usa solamente para la visualización. Es un campo obligatorio.
                
                Como es posible que desee especificar varios menús de navegación nuevos, se recomienda el uso de nombres significativos para designar asignaciones de claves. La longitud máxima del nombre para la asignación de clave es de 64 caracteres y pueden incluirse espacios. No obstante, no pueden incluirse ninguno de los caracteres siguientes: " / \\ \[ \] : ; | = , + \* ? \< \>.
            
              - **Cuando se presione esta tecla**   Use esta lista para habilitar la asignación de teclas. La asignación de claves es la tecla numérica que presiona una persona que llama para que un operador automático realice una operación específica, por ejemplo, desviar a la persona que llama a otro operador automático o a un operador. De forma predeterminada, no hay entradas definidas.
                
                Use la lista desplegable para seleccionar la tecla numérica (de 1 a 9) que la persona que llama debe presionar. Cero (0) está reservado para el operador automático.
                
                Si selecciona **Tiempo de espera** de la lista desplegable, las personas que llamen podrán ser transferidas a un número de extensión o a otro operador automático si no presionan una tecla del teclado del teléfono. Por ejemplo, "Por favor, permanezca en línea y su llamada será contestada por el siguiente agente disponible." El valor predeterminado es 5 segundos. Si habilita esta opción, se creará una asignación de clave en blanco.
            
              - **Reproducir el siguiente archivo de audio**   Use esta opción para seleccionar un archivo de audio que se grabó con anterioridad para las personas que llaman. Haga clic en **Cambiar** y, a continuación, haga clic en **Examinar** para ubicar el archivo de audio. Si deja el archivo de audio establecido en el valor predeterminado \<Ninguno\>, el motor de conversión de texto a voz (TTS) de mensajería unificada sintetizará el texto del menú principal en horario comercial. De forma alternativa, puede crear un archivo de audio personalizado que pueda usarse para el texto del menú principal en horario comercial para un operador automático habilitado con voz que diría, por ejemplo, "Para el departamento comercial, diga 1. Para soporte técnico, diga 2. Para administración, diga 3."
            
              - **Realizar esta acción adicional**   Seleccione una de las siguientes opciones para definir la acción que desea que el operador automático realice para la persona que llama:
                
                  - **Ninguno**   Use esta opción si desea que el operador automático no transfiera la llamada a ninguna extensión, a otro operador automático, ni deje un mensaje para el usuario.
                
                  - **Transferir a esta extensión**   Seleccione esta opción para que se pueda transferir las personas que llaman a un número de extensión. Si habilita esta opción, utilice el cuadro para escribir la extensión donde se transferirá la llamada. Este campo solamente permite caracteres numéricos. No pueden incluirse ninguno de los caracteres siguientes: " / \\ \[ \] : ; | = , + \* ? \< \>.
                
                  - **Transferencia a este operador automático de mensajería unificada**   Seleccione esta opción para transferir la llamada a un operador automático. Haga clic en **Examinar** para localizar el operador automático que desea usar. Antes de habilitar esta opción, deberá crear y configurar el operador automático. Esta opción se usa cuando se crea una estructura principal/secundaria de operadores automáticos de mensajería unificada.
                
                  - **Dejar un mensaje de voz para este usuario**   Seleccione esta opción para que una persona que llame pueda dejar un mensaje de correo de voz para un usuario que se encuentra en el mismo plan de marcado que el operador automático de mensajería unificada que está configurando. Cuando la persona que llama elija esta opción de un menú de operador automático, se le pedirá que deje un correo de voz para el usuario que se seleccionó. Haga clic en **Examinar** para ubicar el buzón habilitado para mensajería unificada.
                
                  - **Anunciar ubicación de la empresa**   Seleccione esta opción para permitir que la persona que llama seleccione una opción del menú de operador automático y escuche la ubicación de la empresa que se encuentra configurada en el operador automático de mensajería unificada. Para permitir que esto funcione correctamente, primero debe escribir la ubicación de la empresa en la casilla **Ubicación de la empresa** de la pestaña **General** del operador automático de mensajería unificada.
                
                  - **Anunciar horario comercial**   Seleccione esta opción para permitir que la persona que llama seleccione una opción del menú de operador automático y escuche el horario de atención de la empresa que se encuentra configurado en el operador automático de mensajería unificada. Para que esta opción funcione correctamente, debe configurar primero el horario comercial en la página **Horario comercial** del operador automático de mensajería unificada.
    
      - **Navegación de menús de horario no comercial**   Es la lista de opciones que las personas que llaman escuchan durante el horario no comercial que se definen en la página **Horario comercial**. Por ejemplo, "Su llamada es muy importante para nosotros. Sin embargo, ha llamado a Woodgrove Bank fuera del horario comercial normal. Si desea dejar un mensaje, presione o diga 1 y le devolveremos la llamada lo antes posible."
        
        Para habilitar la navegación de menús de horario no comercial, debe realizar los siguientes pasos:
        
        1.  **Mensaje de menú**   Use esta opción para especificar un archivo de audio con el mensaje de menú personalizado. Para usar un mensaje de menú de horario no comercial grabado previamente o personalizado, haga clic en **Examinar**.
        
        2.  **Habilitar navegación de menús en horario no comercial**   Seleccione esta casilla para habilitar las opciones de navegación del menú que se usarán en horario no comercial. Si habilita la navegación del menú de horario no comercial, puede agregar nuevas entradas en el menú de navegación de horario no comercial.
        
        3.  Haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono") para crear una nueva entrada del menú de navegación. En la página **Nueva entrada de navegación de menús** use las siguientes opciones para crear una nueva entrada de navegación de menús:
            
              - **Preguntar**   Use esta casilla para escribir el nombre del nuevo menú de navegación. El nombre del menú de navegación se usa solamente para la visualización. Es un campo obligatorio.
                
                Como es posible que desee especificar varios menús de navegación nuevos, se recomienda el uso de nombres significativos para designar asignaciones de claves. La longitud máxima del nombre para la asignación de clave es de 64 caracteres y pueden incluirse espacios. No obstante, no pueden incluirse ninguno de los caracteres siguientes: " / \\ \[ \] : ; | = , + \* ? \< \>.
            
              - **Cuando se presione esta tecla**   Use esta lista para habilitar la asignación de teclas. La asignación de claves es la tecla numérica que presiona una persona que llama para que un operador automático realice una operación específica, por ejemplo, desviar a la persona que llama a otro operador automático o a un operador. De forma predeterminada, no hay entradas definidas.
                
                Use la lista desplegable para seleccionar la tecla numérica (de 1 a 9) que la persona que llama debe presionar. Cero (0) está reservado para el operador automático.
                
                Si selecciona **Tiempo de espera** de la lista desplegable, las personas que llamen podrán ser transferidas a un número de extensión o a otro operador automático si no presionan una tecla del teclado del teléfono. Por ejemplo, "Por favor, permanezca en línea y su llamada será contestada por el siguiente agente disponible." El valor predeterminado es 5 segundos. Si habilita esta opción, se creará una asignación de clave en blanco.
            
              - **Reproducir el siguiente archivo de audio**   Use esta opción para seleccionar un archivo de audio que se grabó con anterioridad para las personas que llaman. Haga clic en **Cambiar** y, a continuación, haga clic en **Examinar** para ubicar el archivo de audio. Si deja el archivo de audio establecido en el valor predeterminado \<Ninguno\>, el motor de conversión de texto a voz (TTS) de mensajería unificada sintetizará el texto del menú principal en horario no comercial. De forma alternativa, puede crear un archivo de audio personalizado que pueda usarse para el texto del menú principal en horario no comercial para un operador automático habilitado con voz que diría, por ejemplo, "Ha llamado a Contoso fuera del horario comercial. Para dejar un mensaje de voz para el departamento comercial, diga 1. Para soporte técnico, diga 2. Para administración, diga 3. Para hablar con un operador en horario no comercial, presione cero."
            
              - **Realizar esta acción adicional**   Seleccione una de las siguientes opciones para definir la acción que desea que el operador automático realice para la persona que llama:
                
                  - **Ninguno**   Use esta opción si desea que el operador automático no transfiera la llamada a ninguna extensión, a otro operador automático, ni deje un mensaje para el usuario.
                
                  - **Transferir a esta extensión**   Seleccione esta opción para que se pueda transferir las personas que llaman a un número de extensión. Si habilita esta opción, escriba en el cuadro el número de extensión al que se transferirá la llamada. Este campo solamente permite caracteres numéricos. No pueden incluirse ninguno de los caracteres siguientes: " / \\ \[ \] : ; | = , + \* ? \< \>.
                
                  - **Transferencia a este operador automático de mensajería unificada**   Seleccione esta opción para transferir la llamada a un operador automático existente. Haga clic en **Examinar** para localizar el operador automático que desea usar. Antes de habilitar esta opción, deberá crear y configurar el operador automático. Esta opción se usa cuando se crea una estructura principal/secundaria de operadores automáticos de mensajería unificada.
                
                  - **Dejar un mensaje de voz para este usuario**   Seleccione esta opción para que una persona que llame pueda dejar un mensaje de correo de voz para un usuario que se encuentra en el mismo plan de marcado que el operador automático de mensajería unificada que está configurando. Cuando la persona que llama elija esta opción de un menú de operador automático, se le pedirá que deje un correo de voz para el usuario que se seleccionó. Haga clic en **Examinar** para ubicar el buzón habilitado para mensajería unificada.
                
                  - **Anunciar ubicación de la empresa**   Seleccione esta opción para permitir que la persona que llama seleccione una opción del menú de operador automático y escuche la ubicación de la empresa que se encuentra configurada en el operador automático de mensajería unificada. Para permitir que esto funcione correctamente, primero debe escribir la ubicación de la empresa en la casilla **Ubicación de la empresa** de la pestaña **General** del operador automático de mensajería unificada.
                
                  - **Anunciar horario comercial**   Seleccione esta opción para permitir que la persona que llama seleccione una opción del menú de operador automático y escuche el horario de atención de la empresa que se encuentra configurado en el operador automático de mensajería unificada. Para que esta opción funcione correctamente, debe configurar primero el horario comercial en la página **Horario comercial** del operador automático de mensajería unificada.

7.  Use **Libreta de direcciones y acceso de operador** para definir las características disponibles para las personas que llaman que marcan en un operador automático de mensajería unificada. Puede configurar características de operador automático como el idioma que se utiliza cuando alguien llama al operador automático y la capacidad para que la persona que llama pueda transferir a un número de extensión de operador. Se pueden realizar las siguientes configuraciones:
    
      - **Opciones para ponerse en contacto con los usuarios**   Use estas opciones para determinar cómo las personas que llaman pueden contactar con los usuarios de correo de voz cuando llaman a un operador automático de mensajería unificada
        
          - **Permitir que los autores de llamadas marquen a usuarios**   Seleccione esta casilla para permitir que las personas que realizan las llamadas puedan transferir llamadas a otros usuarios. De manera predeterminada, esta opción está habilitada y permite a los usuarios asociados con el plan de marcado transferir llamadas a usuarios del mismo plan de marcado de mensajería unificada. Si activa esta casilla, podrá establecer el grupo de usuarios a los que las personas que llaman pueden realizar transferencias seleccionando la opción adecuada de la sección **Opciones para las búsquedas en la libreta de direcciones** de esta página.
            
            Si deshabilita esta opción y deshabilita la opción **Permitir que los autores de llamadas dejen mensajes de voz para los usuarios**, las opciones en **Opciones para las búsquedas en la libreta de direcciones** también se deshabilitan.
        
          - **Permitir que los autores de llamadas dejen mensajes de voz para los usuarios**   Seleccione esta casilla para permitir a las personas que llaman enviar mensajes de voz a los usuarios. De manera predeterminada, esta opción está habilitada y permite a los usuarios asociados con el plan de marcado enviar mensajes de voz a usuarios del mismo plan de marcado de MU. Si activa esta casilla, podrá establecer el grupo de usuarios a los que las personas que llaman pueden enviar mensajes de voz seleccionando la opción adecuada de la sección **Opciones para las búsquedas en la libreta de direcciones** de esta página.
            
            Si deshabilita esta opción y deshabilita la opción **Permitir que los autores de llamadas marquen a usuarios**, las opciones en **Opciones para las búsquedas en la libreta de direcciones** también se deshabilitan.
            
            Si deshabilita esta opción, el operador automático no invitará a las personas que llaman a enviar un mensaje de voz durante el mensaje del sistema.
    
      - **Opciones para las búsquedas en la libreta de direcciones**   Use estas opciones para determinar una agrupación de usuarios. De forma predeterminada, se selecciona **Permitir que las personas que llaman busquen usuarios por nombre o por alias** junto con la opción **En este plan de marcado únicamente**. Sin embargo, puede cambiar las agrupaciones de usuarios para permitir a las personas que llamen transferir llamadas o enviar mensajes a los usuarios ubicados en la lista global de direcciones (GAL) de una organización. Se puede elegir entre las opciones siguientes:
        
          - **Permitir a los autores de llamadas buscar usuarios por nombre o alias:**     De forma predeterminada, esta opción está seleccionada. Permite a las personas que llamen llamar en este operador automático para realizar una búsqueda de directorio de usuarios por nombre o por alias. Se asigna un alias a un usuario cuando se crea un buzón de correo para él. El alias es la primera parte de una dirección SMTP, por ejemplo, tonysmith@contoso.com. La dirección SMTP es tonysmith@contoso.com, mientras que el alias es tonysmith. La elección de esta opción sólo afecta a las personas que llaman que usan este operador automático y no las que usan Outlook Voice Access.
            
              - **En este plan de marcado únicamente**   Seleccione esta opción para permitir a las personas que llaman que conectan con el operador automático de mensajería unificada ubicar y ponerse en contacto con usuarios del mismo plan de marcado asociado con el operador automático del mensajería unificada. De forma predeterminada, esta opción está habilitada en el pan de marcado y en el operador automático. Esto significa que los usuarios de Outlook Voice Access y las personas que llaman al operador automático pueden buscar usuarios dentro del mismo plan de marcado.
            
              - **En toda la organización**    Seleccione esta opción para permitir a los usuarios llamar en este operador automático de mensajería unificada buscar y ponerse en contacto con cualquier persona que aparezca en la GAL de la organización. Esto incluye no sólo a los usuarios habilitados para mensajería unificada sino a todos los usuarios que están habilitados para buzón de correo. Esta opción permite contactar con usuarios en varios planes de marcado. Esta característica no está habilitada de forma predeterminada. Esta configuración también está disponible en un plan de marcado para los usuarios de Outlook Voice Access.
        
          - **Información a incluir para nombres similares**   Use esta lista desplegable para seleccionar la opción que se debe utilizar para el operador automático de mensajería unificada cuando los usuarios tienen el mismo nombre o nombres similares. Esta configuración se usa cuando dos o más usuarios con el mismo nombre están en el directorio. También se denomina un nombre coincidente o un campo para anular ambigüedades. Puede establecer esta configuración o dejar la configuración predeterminada en el operador automático. De forma predeterminada, el operador automático heredará esta configuración de la configuración del plan de marcado vinculado al operador automático. A continuación tiene un ejemplo de un operador automático habilitado para voz:
            
            1.  Sistema: "Bienvenido a Contoso. Si conoce el nombre de la persona a la que llama, dígalo en cualquier momento.\&quot;
            
            2.  La persona que llama dice "Tony Smith".
            
            3.  Hay varias personas con este nombre. Seleccione una de las opciones: Para Tony Smith, de desarrollo, pulse 1. Para Tony Smith, de administración, pulse 2. Para Tony Smith, de soporte técnico, pulse 3.
            
            4.  La persona que llama pulsa la tecla adecuada en el teclado y la llamada se transfiere al usuario.
                

                > [!NOTE]
                > En un operador automático no habilitado para voz, el sistema indicará a la persona que llame que use el teclado para introducir el nombre del usuario (primero el apellido) y, a continuación, buscar al usuario. Si hay varias personas en el directorio con el mismo nombre, se indica a la persona que llama que pulse la tecla adecuada para ser transferido al usuario. Opcionalmente podría crear un operador automático de reserva DTMF que use sólo el teclado para introducir un nombre o un alias.

            
            Para que se use esta configuración, debe agregar la información de usuario correcta. Por ejemplo, si desea que el operador automático use un título para dos usuarios con el mismo nombre, debe agregar dicha información a la cuenta del usuario. Seleccione uno de los siguientes métodos para proporcionar más información de ayuda a la persona que llama para seleccionar al usuario correcto de la organización:
            
              - **Heredar del plan de marcado**   Seleccione esta opción para que el operador automático utilice la configuración predeterminada del plan de marcado asociado con el operador automático.
            
              - **Puesto**   Seleccione esta opción para que el operador automático incluya el puesto de todos los usuarios al enumerar las coincidencias.
            
              - **Departamento**   Seleccione esta opción para que el operador automático incluya el departamento de todos los usuarios al enumerar las coincidencias.
            
              - **Ubicación**   Seleccione esta opción para que el operador automático incluya la ubicación de todos los usuarios al enumerar las coincidencias.
            
              - **Ninguna**   Seleccione esta opción para que no se agregue información adicional al enumerar las coincidencias.
            
              - **Solicitar el alias**   Seleccione esta opción para que el operador automático solicite a la persona que llama el alias de usuario.

8.  En **Acceso de operado**, puede especificar la configuración del operador automático incluyendo lo siguiente:
    
      - **Extensión de operador**   Use este cuadro para escribir el número de extensión que se utilizará para llamar a un operador. Este número de extensión puede conectar a quienes llaman con un operador humano o un buzón con mensajería unificada habilitada, o se puede configurar para que llame a un número de teléfono externo. De manera predeterminada, la extensión del operador no se incluye en este cuadro.
    
      - **Permitir transferir al operador durante el horario comercial**  Use esta casilla para permitir la transferencia de llamadas a un operador humano durante el horario comercial mediante el número de extensión configurado en el cuadro **Extensión de operador**. De forma predeterminada, esta opción está deshabilitada.
        
        Es útil habilitar esta opción para que una persona pueda dejar un mensaje de voz o conectarse con un operador humano cuando no consigue seguir las instrucciones del menú ni localizar en el directorio a la persona deseada durante el horario comercial. Una vez habilitada esta opción, puede configurar el número de extensión de operador en un buzón habilitado para MU supervisado. La persona que llama puede dejar un mensaje de voz, o bien un operador humano que posee el número de extensión puede ayudar a la persona que llama.
    
      - **Permitir transferir al operador durante el horario no comercial**  Use esta casilla para permitir la transferencia de llamadas a un operador humano después del horario comercial mediante el número de extensión configurado en el cuadro **Extensión de operador**. De forma predeterminada, esta opción está deshabilitada.
        
        Es útil habilitar esta opción para que una persona pueda dejar un mensaje de voz o conectarse con un operador humano cuando no consigue seguir las instrucciones del menú ni localizar en el directorio a la persona deseada después del horario comercial. Una vez habilitada esta opción, puede configurar el número de extensión de operador configurado en un buzón habilitado para MU supervisado. La persona que llama puede dejar un mensaje de voz, o bien un operador humano que posee el número de extensión puede ayudar a la persona que llama.

9.  
    
    Use **Autorización de marcado** para configurar las reglas de marcado de las personas que llaman a un operador automático de mensajería unificada. Puede usar esta configuración para controlar los números de extensión a los que se puede obtener acceso desde un operador automático o para controlar los números de teléfono que pueden marcar las personas que llaman que hayan marcado al operador automático. Se pueden realizar las siguientes configuraciones:
    
      - **Llamadas en el mismo plan de marcado de mensajería unificada**   Seleccione esta casilla para permitir a los usuarios que llamen a un operador automático realizar o transferir llamadas a un número de extensión asociado con un usuario habilitado para mensajería unificada que esté asociado con el mismo plan de marcado que el operador automático. Esta opción está habilitada de manera predeterminada.
        
        Al deshabilitar esta opción, los usuarios que llamen a un operador automático podrán realizar llamadas o transferir llamadas a usuarios que no tengan MU habilitada o a otros números de extensión que no estén asociados a un usuario con MU habilitada. Los usuarios no pueden transferir llamadas a usuarios con MU habilitada que estén asociados al mismo plan de marcado que el operador automático. Esto se debe a que, de forma predeterminada, la opción **Permitir llamadas a cualquier extensión** está habilitada.
    
      - **Permitir llamadas a cualquier extensión**   Al deshabilitar esta opción, los usuarios que llaman a un operador automático no pueden realizar ni transferir llamadas a usuarios que no tengan mensajería unificada habilitada ni a otros números de extensión que no estén asociados a un usuario con mensajería unificada habilitada. Sin embargo, pueden realizar llamadas o transferirlas a números de extensión asociados con usuarios habilitados para mensajería unificada. Esto se debe a que la configuración de **Permitir llamadas en el mismo plan de marcado de mensajería unificada** está habilitada de forma predeterminada. La configuración **Permitir llamadas a cualquier extensión** está habilitada de forma predeterminada.
        
        Si esta opción está habilitada, los usuarios que llamen a un operador automático pueden realizar llamadas a usuarios que no están habilitados para MU, a otros números de extensión que no están asociados a un usuario habilitado para MU y a usuarios habilitados para MU. Esto se debe a que la configuración de **Permitir llamadas en el mismo plan de marcado de mensajería unificada** está habilitada de forma predeterminada.
        
        Puede habilitar esta opción en un entorno en que no se han habilitado todos los usuarios para mensajería unificada. Esta opción también resulta útil si desea permitir a los usuarios que llamen a un número de teléfono configurado en un operador automático llamar a números de extensión que no estén asociados con un usuario habilitado para MU.
    
      - **Grupos de reglas de marcado nacionales/regionales autorizados**   Use esta sección para agregar o quitar grupos de reglas de marcado nacionales o regionales permitidos. De forma predeterminada, no hay grupos de reglas de marcado nacionales o regionales configurados en operadores automáticos de mensajería unificada.
        
        Los grupos de reglas de marcado nacionales o regionales se usan para permitir o restringir los números de teléfono de un país o región que puede marcar un usuario que haya llamado a un operador automático de mensajería unificada. Esto ayuda a evitar llamadas de teléfono y gastos innecesarios no autorizados.
        
        Para agregar grupos de reglas de marcado nacionales o regionales, antes debe crear los grupos de reglas de marcado nacionales o regionales adecuados en el plan de marcado de llamadas asociado al operador automático de mensajería unificada y, a continuación, agregar el grupo de reglas de marcado adecuado.
        
        La mensajería unificada puede usar los grupos de reglas de llamadas nacionales o regionales para permitir o restringir el acceso a números de teléfono de un país o región. Esto se aplica a cualquier usuario que llame a un operador automático. Para obtener más información acerca de llamadas externas, consulte [Permitir que los usuarios realicen llamadas](allow-users-to-make-calls-exchange-2013-help.md).
    
      - **Grupos de reglas de marcado internacional autorizados**   Use esta sección para agregar o quitar los grupos de reglas de marcado internacionales permitidos. De forma predeterminada, no hay grupos de reglas de marcado internacionales configurados en operadores automáticos de mensajería unificada.
        
        Los grupos de reglas de marcado internacionales se usan para permitir o restringir los números de teléfono fuera de un país o región que puede marcar un usuario que haya llamado a un operador automático de mensajería unificada. Esto ayuda a evitar llamadas de teléfono y gastos innecesarios no autorizados.
        
        Para agregar grupos de reglas de marcado internacionales, antes debe crear los grupos de reglas internacionales adecuados en el plan de marcado asociado al operador automático de mensajería unificada. Tras crear los grupos de reglas de marcado necesarios en el plan de marcado, debe agregar los grupos de reglas de marcado a la lista de grupos de reglas de marcado autorizadas en el operador automático de mensajería unificada.
        
        La mensajería unificada puede usar grupos de reglas de marcado internacionales para permitir o restringir el acceso a números de teléfono fuera de un país o de una región. Esto se aplica a cualquier usuario que llame a un operador automático. Para obtener más información acerca de llamadas externas, consulte [Permitir que los usuarios realicen llamadas](allow-users-to-make-calls-exchange-2013-help.md).

10. Haga clic en **Aceptar** para crear la nueva navegación de menús.

11. En la página **Operador automático de mensajería unificada**, haga clic en **Guardar** para guardar sus cambios.

## Usar el Shell para configurar las propiedades del operador automático de MU

En este ejemplo, se configura un operador automático de mensajería unificada llamado `MySpeechEnabledAA` para que pase al operador automático `MyDTMFAA`, se configura la extensión del operador en 50100 y se habilita la transferencia de llamadas a este número de extensión después del horario comercial.

    Set-UMAutoAttendant -Identity MySpeechEnabledAA -DTMFFallbackAutoAttendant MyDTMFAA -OperatorExtension 50100 -AfterHoursTransferToOperatorEnabled $true

Este ejemplo configura un operador automático de MU llamado `MyUMAutoAttendant` que tiene: Horario comercial configurado de 10:45 a 13:15 (de 10:45 a. m. a 1:15 p. m.) los domingos, desde 09:00 hasta 17:00 (de 9:00 a. m. a 5:00 p. m.) los lunes y desde 09:00 hasta 16:30 (de 9:00 a. m. a 4:30 p. m.) los sábados; los horarios de feriados y sus saludos asociados se configuran como "Año nuevo" el 02.01.13 y "Edificio cerrado por obras" configurado desde el 24 de abril hasta el 28.04.13.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -BusinessHoursSchedule 0.10:45-0.13:15,1.09:00-1.17:00,6.09:00-6.16:30 -HolidaySchedule "New Year,newyrgrt.wav,1/2/2013","Building Closed for Construction,construction.wav,4/24/2013,4/28/2013"

## Usar el Shell para ver las propiedades del operador automático de MU

En este ejemplo se devuelve una lista formateada de todos los operadores automáticos de MU.

    Get-UMAutoAttendant | Format-List

En este ejemplo se muestra las propiedades de un operador automático de MU llamado MyUMAutoAttendant.

    Get-UMAutoAttendant -Identity MyUMAutoAttendant

