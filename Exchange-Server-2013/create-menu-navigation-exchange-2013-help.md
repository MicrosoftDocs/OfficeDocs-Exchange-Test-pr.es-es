---
title: 'Crear la navegación del menú: Exchange 2013 Help'
TOCTitle: Crear la navegación del menú
ms:assetid: 3cfc9a01-0a61-4d15-9561-621568dc30d9
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa997471(v=EXCHG.150)
ms:contentKeyID: 49895584
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.UnifiedMessaging.AutoAttendantKeyMappingControl
ms.translationtype: MT
---

# Crear la navegación del menú

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2012-11-05_

Puede utilizar la página de la **nueva entrada del menú de navegación** para crear una sola o varias asignaciones de clave para el negocio o menú principal de horario no laborable pide operadores automáticos. Puede definir la acción que se realizará cuando se presiona una tecla del teclado del teléfono es, por ejemplo, transferir la llamada a un número de extensión u otro operador automático.

Para conocer tareas de administración adicionales relacionadas con los operadores automáticos de mensajería unificada, consulte [Procedimientos operador automático de mensajería unificada](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/automatically-answer-and-route-calls/um-auto-attendant-procedures).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el contenido "Operadores automáticos de MU" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-dial-plan).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un operador automático de mensajería unificada. Para conocer los pasos detallados, consulte [Crear un operador automático de mensajería unificada](create-a-um-auto-attendant-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Utilice el CEF para configurar los menús de navegación de operador de automático de mensajería unificada

1.  En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**. En la vista de lista, seleccione el plan de marcado de mensajería unificada que desea cambiar y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

2.  En la página **Plan de marcado de mensajería unificada**, en **Operadores automáticos de mensajería unificada**, seleccione al operador automático de mensajería unificada para el que desea crear la navegación del menú. En la barra de herramientas, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página de la **Mensajería unificada de Operador automático**, haga clic en **exploración del menú**, seleccione **Habilitar la exploración del menú de horario comercial** o **Habilitar la exploración del menú de horario no laborable** y, a continuación, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").

4.  En la página de la **nueva entrada del menú de navegación**, configure lo siguiente:
    
      - **Preguntar**   Use esta casilla para escribir el nombre del nuevo menú de navegación. El nombre del menú de navegación se usa solamente para la visualización. Es un campo obligatorio.
        
        Como es posible que desee especificar varios menús de navegación nuevos, se recomienda el uso de nombres significativos para designar asignaciones de claves. La longitud máxima del nombre para la asignación de clave es de 64 caracteres y pueden incluirse espacios. No obstante, no pueden incluirse ninguno de los caracteres siguientes: " / \\ \[ \] : ; | = , + \* ? \< \>.
    
      - **Cuando se presione esta tecla**   Use esta lista para habilitar la asignación de teclas. La asignación de claves es la tecla numérica que presiona una persona que llama para que un operador automático realice una operación específica, por ejemplo, desviar a la persona que llama a otro operador automático o a un operador. De forma predeterminada, no hay entradas definidas.
        
        Utilice la lista desplegable para seleccionar la tecla numérica (de 1 a 9) que el llamador debe presionar. Cero (0) está reservado para el operador operador automático.
        
        Si selecciona **Tiempo de espera** de la lista desplegable, las personas que llamen podrán ser transferidas a un número de extensión o a otro operador automático si no presionan una tecla del teclado del teléfono. Por ejemplo, "Por favor, permanezca en línea y su llamada será contestada por el siguiente agente disponible." El valor predeterminado es 5 segundos. Si habilita esta opción, se creará una asignación de clave en blanco.
    
      - **Reproducir el siguiente archivo de audio**    Utilice esta opción para seleccionar un archivo de audio previamente grabado para los llamadores. Haga clic en **cambiar** y, a continuación, haga clic en **Examinar** para buscar el archivo de audio.
    
      - **Realizar esta acción adicional**   Seleccione una de las siguientes opciones para definir la acción que desea que el operador automático realice para la persona que llama:
        
          - **Ninguno**    Si no desea el operador automático para transferir la llamada a una extensión o a otro operador automático o dejar un mensaje para un usuario, utilice esta opción.
        
          - **Transferir a esta extensión**   Seleccione esta opción para que se pueda transferir las personas que llaman a un número de extensión. Si habilita esta opción, utilice el cuadro para escribir la extensión donde se transferirá la llamada. Este campo solamente permite caracteres numéricos. No pueden incluirse ninguno de los caracteres siguientes: " / \\ \[ \] : ; | = , + \* ? \< \>.
        
          - **Transferencia a este operador automático de mensajería unificada**   Seleccione esta opción para transferir la llamada a un operador automático. Haga clic en **Examinar** para localizar el operador automático que desea usar. Antes de habilitar esta opción, deberá crear y configurar el operador automático. Esta opción se usa cuando se crea una estructura principal/secundaria de operadores automáticos de mensajería unificada.
        
          - **Dejar un mensaje de voz para este usuario**   Seleccione esta opción para que una persona que llame pueda dejar un mensaje de correo de voz para un usuario que se encuentra en el mismo plan de marcado que el operador automático de mensajería unificada que está configurando. Cuando la persona que llama elija esta opción de un menú de operador automático, se le pedirá que deje un correo de voz para el usuario que se seleccionó. Haga clic en **Examinar** para ubicar el buzón habilitado para mensajería unificada.
        
          - **Anunciar ubicación de la empresa**   Seleccione esta opción para permitir que la persona que llama seleccione una opción del menú de operador automático y escuche la ubicación de la empresa que se encuentra configurada en el operador automático de mensajería unificada. Para permitir que esto funcione correctamente, primero debe escribir la ubicación de la empresa en la casilla **Ubicación de la empresa** de la pestaña **General** del operador automático de mensajería unificada.
        
          - **Anunciar horario comercial**   Seleccione esta opción para permitir que la persona que llama elija una opción del menú de operador automático y escuche el horario de atención de la empresa configurado en el operador automático de mensajería unificada. Para permitir que esto funcione correctamente, primero debe configurar el horario comercial en la página **Horario comercial** del operador automático de mensajería unificada.

5.  Haga clic en **Aceptar** para crear la nueva navegación de menús.

6.  En la página **Operador automático de mensajería unificada**, haga clic en **Guardar** para guardar sus cambios.

## Usar el Shell para configurar asignaciones de teclas operador de automático de mensajería unificada

Este ejemplo permite asignaciones de teclas en horario de oficina para que:

  - Cuando los llamadores presione 1, se reenviará a otro operador automático de mensajería unificada denominado `SalesAutoAttendant`.

  - Cuando presiona la tecla 2, se reenviarán al número de extensión 12345 para soporte.

  - Cuando presiona la tecla 3, se enviará a otro operador automático que se reproducirá un archivo de audio.

<!-- end list -->

    Set-UMAutoAttendant -id MyAutoAttendant -BusinessHoursKeyMappingEnabled $true -BusinessHoursKeyMapping "1,Sales,,SalesAutoAttendant","2,Support,12345","3,Directions,,,directions.wav"

Este ejemplo establece las asignaciones de teclas definidas en un archivo de valores separados por comas (.csv). Primero debe crear el archivo .csv con los siguientes encabezados y la entrada correcta: \< clave \>, \< Descripción \> \[\< extensión \>\], \[\< nombre de operador automático \>\], \[\< promptfilenamepath \>\], \[\< asrphrase1; asrphrase2 \>\], \[\< leavevoicemailfor \>\], \[\< transfertomailbox \>\]. Los valores entre corchetes son opcionales. Después de crear el archivo .csv, importar el archivo .csv con el cmdlet **Import-csv** .

    $o = Import-csv -path "C:\UMFiles\AutoAttendants\keymappings.csv"
    Set-UMAutoAttendant MyAutoAttendant -BusinessHoursKeyMapping $o

Este ejemplo exporta asignaciones de teclas de un operador automático de mensajería unificada existente a un archivo .csv y, a continuación, importa las mismas asignaciones clave en otro operador automático de mensajería unificada. Puede exportar también las asignaciones de teclas a un archivo .csv, editar o modificar las asignaciones de teclas en el archivo .csv y, a continuación, importar las asignaciones de teclas en otro operador automático de mensajería unificada.

    $aa = Get-UMAutoAttendant -id MyAutoAttendant
    $aa1 = Get-UMAutoAttendant -id MyAutoAttendant2
    $aa.BusinessHoursKeyMapping | Export-csv -path "C:\UMFiles\AutoAttendants\keymappings.csv"
    $aa1.BusinessHoursKeyMapping = (Import-csv -path "C:\UMFiles\AutoAttendants\keymappings.csv")

