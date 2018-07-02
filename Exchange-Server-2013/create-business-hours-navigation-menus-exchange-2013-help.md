---
title: 'Crear menús de navegación de horario comercial: Exchange 2013 Help'
TOCTitle: Crear menús de navegación de horario comercial
ms:assetid: f76472fd-aa1a-4cd8-8e26-cc674421d375
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb232203(v=EXCHG.150)
ms:contentKeyID: 49896019
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Crear menús de navegación de horario comercial

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2012-11-05_

Puede habilitar asignaciones de claves en horario comercial para un operador automático de mensajería unificada (MU). Después de crear un operador automático de mensajería unificada, se usará un aviso del sistema predeterminado para el texto del menú principal en horario comercial que las personas que llaman escucharán después de que se reproduzca el saludo de bienvenida en horario comercial. El texto del menú principal en horario comercial dice algo similar a: "Bienvenido al operador automático de Microsoft Exchange." Debido a que de forma predeterminada no hay asignaciones de tecla, las personas que llaman no tienen opciones de menú, solo escuchan el mensaje del sistema predeterminado.

Cuando configure las asignaciones de claves, defina las opciones y operaciones que se realizarán si una persona que llama dice una frase cuando usa un operador automático habilitado para voz o pulsa la tecla en el teclado del teléfono cuando usa un operador automático que no está habilitado para voz.

Para conocer tareas de administración adicionales relacionadas con los operadores automáticos de mensajería unificada, consulte [Procedimientos operador automático de mensajería unificada](um-auto-attendant-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: Menos de 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el contenido "Operadores automáticos de MU" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un operador automático de mensajería unificada. Para conocer los pasos detallados, consulte [Crear un operador automático de mensajería unificada](create-a-um-auto-attendant-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar el EAC para permitir asignaciones de claves en horario comercial en un operador automático de mensajería unificada

1.  En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**. En la vista de lista, seleccione el plan de marcado de mensajería unificada que desea cambiar y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

2.  En la página **Plan de marcado de mensajería unificada**, en **Operadores automáticos de mensajería unificada**, seleccione el operador automático de mensajería unificada para el que desea crear un menú de navegación en horario comercial. En la barra de herramientas, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Operador automático de mensajería unificada**, haga clic en **Navegación de menús**, debajo de **Navegación de menús en horario comercial**, seleccione **Habilitar navegación de menús en horario comercial** y, a continuación, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").

4.  En la página **Nueva entrada de navegación de menús**, use las siguientes opciones para crear una nueva entrada de navegación de menús:
    
      - **Aviso**   Use este cuadro para escribir el nombre del nuevo menú de navegación. El nombre del menú de navegación se usa solamente para la visualización. Es un campo obligatorio.
        
        Como es posible que desee especificar varios menús de navegación nuevos, se recomienda el uso de nombres significativos para designar asignaciones de claves. La longitud máxima del nombre para la asignación de clave es de 64 caracteres y pueden incluirse espacios. No obstante, no pueden incluirse ninguno de los caracteres siguientes: " / \\ \[ \] : ; | = , + \* ? \< \>.
    
      - **Cuando se presione esta tecla**   Use esta lista para habilitar la asignación de claves. La asignación de claves es la tecla numérica que presiona una persona que llama para que un operador automático realice una operación específica, por ejemplo, desviar a la persona que llama a otro operador automático o a un operador. De forma predeterminada, no hay entradas definidas.
        
        Use la lista desplegable para seleccionar la tecla numérica (de 1 a 9) que la persona que llama debe presionar. Cero (0) está reservado para el operador automático.
        
        Si selecciona **Tiempo de espera** en la lista desplegable, las personas que llaman serán transferidas a un número de extensión o a otro operador automático si no presionan una tecla del teléfono. Por ejemplo, "Por favor, permanezca en línea y su llamada será contestada por el siguiente agente disponible." El valor predeterminado es 5 segundos. Si habilita esta opción, se creará una asignación de clave en blanco.
    
      - **Reproducir el siguiente archivo de audio**   Use esta opción para seleccionar un archivo de audio grabado con anterioridad para las personas que llaman. Haga clic en **Cambiar** y, a continuación, en **Examinar** para encontrar el archivo de audio. Si deja el archivo de audio establecido en el valor predeterminado \<Ninguno\>, el motor de conversión de texto a voz (TTS) de mensajería unificada sintetizará el texto del menú principal en horario comercial. De forma alternativa, puede crear un archivo de audio personalizado que pueda usarse para el texto del menú principal en horario comercial para un operador automático habilitado con voz que diría, por ejemplo, "Para el departamento comercial, diga 1. Para soporte técnico, diga 2. Para administración, diga 3."
    
      - **Realizar esta acción adicional**   Seleccione una de las siguientes opciones para definir la acción que desea que el operador automático realice para la persona que llama:
        
          - **Ninguna**   Use esta opción si no desea que el operador automático transfiera la llamada a una extensión u otro operador automático, ni deje un mensaje para el usuario.
        
          - **Transferir a esta extensión**   Seleccione esta opción para permitir que las llamadas se puedan transferir a un número de extensión. Si habilita esta opción, escriba en el cuadro el número de extensión al que se transferirá la llamada. Este campo solamente permite caracteres numéricos. No pueden incluirse ninguno de los caracteres siguientes: " / \\ \[ \] : ; | = , + \* ? \< \>.
        
          - **Transferencia a este operador automático de mensajería unificada**   Seleccione esta opción para transferir la llamada a un operador automático. Haga clic en **Examinar** para localizar el operador automático que desea usar. Antes de habilitar esta opción, deberá crear y configurar el operador automático. Esta opción se usa cuando se crea una estructura principal/secundaria de operadores automáticos de mensajería unificada.
        
          - **Dejar un mensaje de voz para este usuario**   Seleccione esta opción para permitir que la persona que llama deje un mensaje de correo de voz para un usuario que se encuentra en el mismo plan de marcado que el operador automático de mensajería unificada que está configurando. Cuando la persona que llama elija esta opción de un menú de operador automático, se le pedirá que deje un correo de voz para el usuario que se seleccionó. Haga clic en **Examinar** para encontrar el usuario habilitado para mensajería unificada.
        
          - **Anunciar ubicación de la empresa**   Seleccione esta opción para permitir que la persona que llama elija una opción del menú de operador automático y escuche la ubicación de la empresa configurada en el operador automático de mensajería unificada. Para permitir que esto funcione correctamente, primero debe escribir la ubicación de la empresa en el cuadro **Ubicación de la empresa** de la página **General** del operador automático de mensajería unificada.
        
          - **Anunciar horario comercial**   Seleccione esta opción para permitir que la persona que llama elija una opción del menú de operador automático y escuche el horario de atención de la empresa configurado en el operador automático de mensajería unificada. Para permitir que esto funcione correctamente, primero debe configurar el horario comercial en la página **Horario comercial** del operador automático de mensajería unificada.

5.  Haga clic en **Aceptar** para crear la nueva navegación de menús.

6.  En la página **Operador automático de mensajería unificada**, haga clic en **Guardar** para guardar los cambios.

## Uso del Shell para habilitar asignaciones de tecla en horario comercial en un operador automático de mensajería unificada

En este ejemplo, se configura un operador automático de mensajería unificada denominado `MyAutoAttendant` y se habilitan las asignaciones de tecla en horario comercial de modo que, cuando la persona que llama presiona 1, se la reenvía a otro operador automático de mensajería unificada denominado `SalesAutoAttendant`. Cuando la persona presiona 2, se la reenvía al número de extensión 12345 para soporte y cuando presiona 3, se la envía a otro operador automático que reproduce un archivo de audio.

    Set-UMAutoAttendant -Identity MyAutoAttendant - BusinessHoursKeyMappingEnabled $true -BusinessHoursKeyMapping "1,Sales,,SalesAutoAttendant","2,Support,12345","3,Directions,,,directions.wav"

