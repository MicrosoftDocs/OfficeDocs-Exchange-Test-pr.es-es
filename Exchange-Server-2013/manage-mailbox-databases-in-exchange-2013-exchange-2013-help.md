---
title: 'Administrar bases de datos de buzones en Exchange 2013: Exchange 2013 Help'
TOCTitle: Administrar bases de datos de buzones en Exchange 2013
ms:assetid: ead4a96b-1717-435b-bcfc-9901ac4e3b58
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ150580(v=EXCHG.150)
ms:contentKeyID: 48268839
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Administrar bases de datos de buzones en Exchange 2013

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2013-04-29_

Una base de datos de buzones de correo es una unidad de granularidad donde se crean y se almacenan buzones. Una base de datos de buzones se almacena como archivo de base de datos de Exchange (.edb). En Microsoft Exchange Server 2013, cada base de datos de buzones cuenta con sus propias propiedades que pueden configurarse.

En este tema se muestra cómo realizar tareas de configuración relacionadas con la administración de bases de datos de buzones en Microsoft Exchange Server 2013.

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento: 10 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Bases de datos de buzones" en el tema [Permisos de destinatarios](recipients-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Crear una base de datos de buzones

## Usar el EAC para crear una base de datos de buzones

1.  Desde el Centro de administración de Exchange, vaya a **Servidores**.

2.  Seleccione **Bases de datos** y, a continuación, haga clic en el símbolo **+** para crear una base de datos.

3.  Use el Asistente para nuevas bases de datos para crear la base de datos.

## Usar el Shell para crear una base de datos de buzones

Para ver un ejemplo acerca de cómo crear una base de datos de buzones, consulte el Ejemplo 1 en [New-MailboxDatabase](https://technet.microsoft.com/es-es/library/aa997976\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que la base de datos se creó correctamente, siga estos pasos:

  - En el EAC, compruebe que la base de datos de buzones creada aparece en la página **Bases de datos**.

  - En el Shell, ejecute el siguiente comando para comprobar que la base de datos se creó en el servidor Mailbox01.
    
        Get-MailboxDatabase -Server "Mailbox01"

## Obtener las propiedades de una base de datos de buzones

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Get-MailboxDatabase](https://technet.microsoft.com/es-es/library/bb124924\(v=exchg.150\)).

## Usar el Shell para obtener las propiedades de una base de datos de buzones

Para ver un ejemplo acerca de cómo obtener las propiedades de una base de datos de buzones, consulte el Ejemplo 2 en [New-MailboxDatabase](https://technet.microsoft.com/es-es/library/aa997976\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que la información de la base de datos de buzones se recuperó correctamente, siga estos pasos:

En la Consola, compruebe que toda la información de la base de datos de buzones aparece correctamente.

## Establecer las propiedades de una base de datos de buzones

## Usar el EAC para establecer las propiedades de una base de datos de buzones

1.  En el EAC, vaya a **Servidores**.

2.  Seleccione **Bases de datos** y, a continuación, haga clic para seleccionar la base de datos de buzones que desea configurar.

3.  Haga clic en **Editar** ![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar") para configurar los atributos de una base de datos de buzones.

4.  
    
    Use la ficha **General** para visualizar el estado de la ruta de acceso a la base de datos de buzones, incluso el estado de la base de datos de buzones, la ruta de acceso a la copia de base de datos de buzones y la última copia de seguridad:
    
      - **Ruta de acceso a la base de datos**   Este campo de sólo lectura muestra la ruta completa al archivo de la base de datos de Exchange 2013 (.edb) de la base de datos de buzones seleccionada. Para ver la ruta completa, puede hacer clic en la ruta y usar la tecla de flecha derecha. Este campo no se puede usar para cambiar la ruta. Para cambiar la ubicación de los archivos de la base de datos, use el cmdlet [Move-DatabasePath](https://technet.microsoft.com/es-es/library/bb124742\(v=exchg.150\)).
    
      - **Última copia de seguridad completa**   Este campo de sólo lectura muestra la fecha y la hora de la última copia de seguridad completa de la base de datos de buzones.
    
      - **Última copia de seguridad incremental**   Este campo de sólo lectura muestra la fecha y la hora de la última copia de seguridad incremental de la base de datos de buzones.
    
      - **Estado**   Este campo de sólo lectura muestra si la base de datos de buzones está montada o desmontada.
    
      - **Montada en el servidor**   Este campo de sólo lectura muestra el servidor en que la base de datos está montada.
    
      - **Maestro** Este campo de sólo lectura muestra el servidor principal de la base de datos de buzones. El servidor de buzón de correo que hospeda la copia activa de una base de datos se conoce como el patrón de base de datos de buzones.
    
      - **Tipo de patrón** Este campo de sólo lectura muestra el tipo de patrón de la base de datos de buzones.
    
      - **Modificado**   Este campo de sólo lectura muestra la última fecha y hora en que se modificó la base de datos.
    
      - **Servidores que hospedan una copia de esta base de datos**   Este campo de sólo lectura muestra los demás servidores que tienen una copia de esta base de datos.

5.  Use la ficha **Mantenimiento** para configurar todos los parámetros de la base de datos de buzones, entre ellos, la especificación de un destinatario del diario, la configuración de un programa de mantenimiento y el montaje de la base de datos en el inicio:
    
      - **Destinatario del diario**   Haga clic en **Examinar** para especificar un destinatario a fin de habilitar el registro en diario en esta base de datos de buzones. Quite el destinatario enumerado para deshabilitar el registro en diario.
    
      - **Programación de mantenimiento**   Use esta lista para seleccionar una de las programaciones de mantenimiento preestablecidas. También puede configurar una programación personalizada. Para configurar una programación personalizada, haga clic en **Personalizar**.
    
      - **Habilitar mantenimiento de base de datos en segundo plano (Análisis de ESE las 24 horas, los 7 días de la semana)**   Active esta casilla para habilitar el análisis en línea de la base de datos, que se ejecuta continuamente en segundo plano. El análisis en línea de la base de datos efectúa una suma de comprobación de la base de datos y realiza operaciones que permiten a Exchange buscar espacio perdido en la base de datos y recuperarlo. Si activa esta casilla, Exchange analizará la base de datos una vez al día como máximo y producirá un evento de advertencia si no puede completar el análisis en un plazo de siete días.
    
      - **No montar esta base de datos en el inicio**   Seleccione esta casilla para impedir que Exchange monte esta base de datos de buzones al momento del inicio.
    
      - **Una restauración puede sobrescribir esta base de datos**   Seleccione esta casilla para permitir la sobrescritura de la base de datos de buzones durante un proceso de restauración.
    
      - **Habilitar registro circular**   Seleccione esta casilla para habilitar el registro circular.

6.  Use la ficha **Límites** para especificar los límites de almacenamiento, el intervalo entre mensajes de advertencia y la configuración de la eliminación para una base de datos de buzones:
    
      - **Emitir advertencia al llegar a (GB)**   Active esta casilla para advertir automáticamente a los usuarios que su buzón está por alcanzar el límite de almacenamiento. Para especificar el límite de almacenamiento, active la casilla y, a continuación, especifique en gigabytes (GB) cuánto contenido puede almacenarse en el buzón antes de que se envíe un mensaje de correo electrónico de advertencia a los usuarios de buzones. Puede escribir un valor del 0 al 2.097.151 MB (2,0 terabytes).
    
      - **Prohibir envío al llegar a (GB)**   Active esta casilla para impedir que los usuarios envíen nuevos mensajes de correo electrónico una vez que el tamaño del buzón alcanza el límite especificado. Para especificar este límite, active la casilla y, a continuación, escriba en GB el tamaño del buzón a partir del que desea prohibir el envío de nuevos mensajes de correo electrónico y notificar al usuario. Puede escribir un valor del 0 al 2.097.151 MB (2,0 terabytes).
    
      - **Prohibir envío y recepción al llegar a (GB)**   Active esta casilla para impedir que los usuarios envíen y reciban mensajes de correo electrónico una vez que el tamaño del buzón alcanza el límite especificado. Para especificar este límite, active la casilla y, a continuación, escriba en GB el tamaño del buzón a partir del que desea prohibir el envío y la recepción de mensajes de correo electrónico y notificar al usuario. Puede escribir un valor del 0 al 2.097.151 MB (2,0 terabytes).
    
      - **Guardar los elementos eliminados durante (días)**   Active esta casilla para establecer el número de días que se guardarán los elementos eliminados en un buzón. Puede escribir un valor de 0 a 24.855 días.
    
      - **Guardar los buzones eliminados durante (días)**   Active esta casilla para establecer el número de días que se guardarán los buzones eliminados. Puede escribir un valor de 0 a 24.855 días.
    
      - **No eliminar elementos de forma permanente hasta que se haya realizado una copia de seguridad de la base de datos**   Active esta casilla para impedir que se eliminen buzones y mensajes de correo electrónico hasta que se haya realizado una copia de seguridad de la base de datos de buzones.

7.  Utilice la pestaña **Configuración de cliente** para seleccionar la libreta de direcciones sin conexión (OAB) para el buzón:
    
      - **Libreta de direcciones sin conexión**   Para seleccionar una libreta de direcciones sin conexión, haga clic en **Examinar** y, a continuación, seleccione la libreta de direcciones sin conexión.

## Usar el Shell para establecer las propiedades de una base de datos de buzones

Para ver un ejemplo acerca de cómo establecer las propiedades de una base de datos de buzones, consulte el Ejemplo 1 en [Set-MailboxDatabase](https://technet.microsoft.com/es-es/library/bb123971\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que los atributos se establecieron correctamente, siga estos pasos:

  - Compruebe que los cambios se han guardado en el EAC.

  - En el Shell, ejecute el siguiente comando para recuperar las propiedades de la base de datos de buzones.
    
        Get-MailboxDatabase -Identity MailboxDatabase01 -Status | Format-List

## Mover una ruta de acceso a la base de datos de buzones

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Move-DatabasePath](https://technet.microsoft.com/es-es/library/bb124742\(v=exchg.150\)).

## Usar el Shell para mover la ruta de acceso a una base de datos de buzones

Para ver un ejemplo acerca de cómo establecer las propiedades de una base de datos de buzones, consulte el Ejemplo 1 en [Move-DatabasePath](https://technet.microsoft.com/es-es/library/bb124742\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que la ruta de acceso a la base de datos se movió correctamente, realice lo siguiente:

1.  En el EAC, seleccione **Servidores** \> **Bases de datos** y, a continuación, haga clic para seleccionar el buzón adecuado.

2.  Haga clic en el símbolo del **lápiz** y compruebe que la ruta de acceso a la base de datos es correcta.

## Montar una base de datos de buzones

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Mount-Database](https://technet.microsoft.com/es-es/library/aa998871\(v=exchg.150\)).

## Usar el Shell para montar una base de datos de buzones

Para ver un ejemplo acerca de cómo montar una base de datos de buzones, consulte el Ejemplo 1 en [Mount-Database](https://technet.microsoft.com/es-es/library/aa998871\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que la base de datos de buzones se montó correctamente, siga los siguientes pasos.

  - En el Shell, ejecute el siguiente comando para recuperar las propiedades de la base de datos de buzones para todas las bases de datos de buzones.
    
        Get-MailboxDatabase -IncludePreExchange2013

## Desmontar una base de datos de buzones

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Dismount-Database](https://technet.microsoft.com/es-es/library/bb124936\(v=exchg.150\)).

## Usar el Shell para desmontar una base de datos de buzones

Para ver un ejemplo acerca de cómo desmontar una base de datos de buzones, consulte el Ejemplo 1 en [Dismount-Database](https://technet.microsoft.com/es-es/library/bb124936\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que la base de datos se desmontó correctamente, siga estos pasos:

1.  En el EAC, seleccione **Servidores** \> **Bases de datos** y, a continuación, haga clic para seleccionar el buzón adecuado.

2.  Haga clic en el símbolo del **lápiz** y compruebe que el estado de la base de datos es **Desmontado**.

## Quitar una base de datos de buzones

## Usar el EAC para quitar una base de datos de buzones

1.  En el EAC, seleccione **Servidores** \> **Bases de datos** y, a continuación, haga clic para seleccionar el buzón adecuado.

2.  Haga clic en **Eliminar**![Eliminar icono](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Eliminar icono") para quitar la base de datos de buzones.

## Uso del Shell para quitar una base de datos de buzones

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Remove-MailboxDatabase](https://technet.microsoft.com/es-es/library/aa997931\(v=exchg.150\)).

1.  Ejecute el siguiente comando para quitar la base de datos de buzones MyDatabase.
    
        Remove-MailboxDatabase -Identity "MyDatabase"

2.  Cuando se le pregunte si está seguro de que desea realizar la acción, escriba **Y**.

3.  Cuando aparezca el cuadro de diálogo que informa que la base de datos se quitó correctamente, anote la ubicación del archivo de base de datos de Exchange 2013 (.edb). Si desea quitar este archivo de la unidad de disco duro, debe quitarlo manualmente.

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que la base de datos de buzones se eliminó correctamente, siga estos pasos:

  - En el EAC, seleccione **Servidores** \> **Bases de datos**.

  - Compruebe que se ha eliminado la base de datos de buzones.

