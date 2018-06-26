---
title: 'Ver o configurar las propiedades de directiva de buzón de Outlook Web App: Exchange 2013 Help'
TOCTitle: Ver o configurar las propiedades de directiva de buzón de Outlook Web App
ms:assetid: be012ffe-8fdb-4fb7-aebd-78b3a55593fa
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd351097(v=EXCHG.150)
ms:contentKeyID: 49895882
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Ver o configurar las propiedades de directiva de buzón de Outlook Web App

 

_**Se aplica a:**Exchange Online, Exchange Server 2013_

_**Última modificación del tema:**2016-04-13_

Después de haber creado una directiva de buzón de Outlook Web App, podrá configurar una amplia variedad de opciones para controlar las funciones que tienen disponibles los usuarios en Outlook Web App. Por ejemplo, podrá habilitar o deshabilitar las reglas de la Bandeja de entrada, o bien crear una lista de los tipos de archivos permitidos para datos adjuntos.

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento:  3 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Directivas de buzones de correo de Outlook Web App" en el tema [Permisos de dispositivos móviles y clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Uso de EAC para ver o configurar directivas de buzón de Outlook Web App

1.  En el EAC, haga clic en **Permisos** \> **Directivas de Outlook Web App**.

2.  En el panel de resultados, haga clic para seleccionar la directiva de buzón que desea ver o configurar.

3.  Haga clic en el botón **Editar**.

4.  
    
    En la ficha **General**, se puede ver y editar el nombre de la directiva.

5.  
    
    En la ficha **Características**, use las casillas para habilitar o deshabilitar las características. Las funciones más comunes se muestran de forma predeterminada. Para ver todas las características que se pueden habilitar o deshabilitar, haga clic en **Más opciones**.
    

    > [!NOTE]
    > La configuración de las características de las Outlook Web Appdirectivas de buzón invalida la configuración del directorio virtual Outlook Web App. Puede cambiar la configuración de la segmentación de usuarios concretos mediante el uso del cmdlet <STRONG>Set-CASMailbox</STRONG> en el Shell.



6.  
    
    En la pestaña **Acceso a los archivos**, use las casillas **Acceso directo a archivos** para configurar el acceso a los archivos y ver las opciones de los usuarios. El acceso a los archivos permite que un usuario abra o vea el contenido de los archivos adjuntos a un correo electrónico.
    
    El acceso a archivos se puede controlar en función de si el usuario inició sesión en un equipo público o privado. La opción para que los usuarios seleccionen el acceso mediante equipo privado o el acceso mediante equipo público sólo está disponible cuando se está usando la autenticación basada en formularios. El resto de formas de autenticación están establecidas de forma predeterminada en el acceso mediante equipo privado.

7.  En la ficha **Acceso sin conexión**, use los botones de opción para configurar la disponibilidad del acceso sin conexión.

8.  Haga clic en **Guardar** para actualizar la directiva.

## Uso del Shell para configurar directivas de buzón de Outlook Web App

En este ejemplo se habilita el acceso a calendarios en la directiva de buzón predeterminada.

    Set-OwaMailboxPolicy -Identity Default -CalendarEnabled $true

Para obtener más información sobre sintaxis y parámetros, consulte [Set-OwaMailboxPolicy](https://technet.microsoft.com/es-es/library/dd297989\(v=exchg.150\)).

## Uso del Shell para ver directivas de buzón de Outlook Web App

En este ejemplo se recuperan las propiedades de la directiva de buzones `Executives` de Outlook Web App en la organización `Fabrikam`.

    Get-OwaMailboxPolicy -Identity Fabrikam\Executives

Para obtener más información sobre sintaxis y parámetros, consulte [Get-OwaMailboxPolicy](https://technet.microsoft.com/es-es/library/dd351095\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que editó correctamente una directiva de buzón de Outlook Web App:

1.  En el EAC, haga clic en **Permisos** \> **Directivas de Outlook Web App** y luego elija una directiva de buzón de Outlook Web App específica.

2.  Haga clic en el botón **Editar** para ver las propiedades de la directiva de buzón.

3.  Haga clic en **Guardar** o **Cancelar** para cerrar la página de propiedades.

